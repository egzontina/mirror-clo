---
title: "Setting up GitLab CI for Android projects"
author: Greyson Parrelli
author_twitter: greyson_p
categories: GitLab CI
image_title: '/images/blogimages/setting-up-gitlab-ci-for-android-projects/banner.jpg'
twitter_image: '/images/tweets/setting-up-gitlab-ci-for-android-projects.png'
description: "Learn how to set up GitLab CI for your Android projects."
---

Have you ever accidentally checked in a typo that broke your Android build or unknowingly broke an important use case with a new change? Continuous Integration is a way to avoid these headaches, allowing you to confirm that changes to your app compile, and your tests pass before they're merged in.

<!-- more -->

[GitLab CI](https://about.gitlab.com/gitlab-ci/) is a wonderful [Continuous Integration](https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/) built-in solution, and in this post we'll walk through how to set up a basic config file (`.gitlab-ci.yml`) to ensure your Android app compiles and passes unit and functional tests. We assume that you know the process of creating an Android app, can write and run tests locally, and are familiar with the basics of the GitLab UI.

## Our sample project

Here's the [sample project](https://gitlab.com/greysonp/gitlab-ci-android) we'll be working with today. It's very simple. The app allows you to input two numbers, and then click "Calculate" to view the sum in a separate Activity. This is of course a very silly way to structure an app, but it allows us to write some clear examples of different kinds of tests.

![Sample app screenshot](/images/blogimages/setting-up-gitlab-ci-for-android-projects/sample-app-screenshot.png){:.shadow}

### Unit tests

[Unit tests](https://developer.android.com/training/testing/unit-testing/index.html) are the fundamental tests in your app testing strategy, from which you can verify that the logic of individual units is correct. They are a fantastic way to catch regressions when making changes to your app. They run directly on the Java Virtual Machine (JVM), so you don't need an actual Android device to run them.

If you already have working unit tests, you shouldn't have to make any adjustments to have them work with GitLab CI. You can see some example unit tests in the [sample app](https://gitlab.com/greysonp/gitlab-ci-android/tree/master/app/src/test/java/com/greysonparrelli/gitlabciandroid). The sample doesn't use [Robolectric](http://robolectric.org/), but nothing stops you from doing so.

### Functional tests

[Functional tests]((https://developer.android.com/training/testing/ui-testing/index.html)), sometimes called UI tests or emulator tests, are great for those times when unit tests aren't practical. They are often used when you want to test a distinct user path that would be difficult to unit test. In our [sample app](https://gitlab.com/greysonp/gitlab-ci-android/blob/master/app/src/androidTest/java/com/greysonparrelli/gitlabciandroid/AddingTest.java), we test the path of a user inputting numbers, pressing "Calculate", and seeing the result in the next Activity. Functional tests run on an actual Android device or emulator and can therefore be slow to execute, meaning that are typically only used when other testing methods aren't sufficient.

Because functional tests run on an actual Android device or emulator, they tend to be finnicky. Any number of things could happen to screw up the test, including the screen locking. To help prevent this, the sample project includes a [base class](https://gitlab.com/greysonp/gitlab-ci-android/blob/master/app/src/androidTest/java/com/greysonparrelli/gitlabciandroid/TestBase.java) for tests to ensure the screen is unlocked when the tests are run. The base class contains this `@Before`-annotated method, meaning that it is run before each of your tests:

```java
@Before
public void setup() {
    // Unlock the screen if it's locked
    UiDevice device = UiDevice.getInstance(InstrumentationRegistry.getInstrumentation());
    try {
        device.wakeUp();
    } catch (RemoteException e) {
        e.printStackTrace();
    }

    // Set the flags on our activity so it'll appear regardless of lock screen state
    final Activity activity = getActivityRule().getActivity();
    Runnable wakeUpDevice = new Runnable() {
        public void run() {
            activity.getWindow().addFlags(WindowManager.LayoutParams.FLAG_TURN_SCREEN_ON |
                    WindowManager.LayoutParams.FLAG_SHOW_WHEN_LOCKED |
                    WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
        }
    };
    activity.runOnUiThread(wakeUpDevice);
}
```

Now that we've got the project set up, let's look at how we integrate GitLab CI.

## Setting up GitLab CI

We want to be able to configure our project so that our app is built, and it has both the unit and functional tests run upon check-in. To do so, we have to create our GitLab CI config file, called `.gitlab-ci.yml`, and place it in the root of our project.

So, first things first: If you're just here for a snippet to copy-paste, here is a `.gitlab-ci.yml` that will build and test your app:

```yml
image: openjdk:8-jdk

variables:
  ANDROID_COMPILE_SDK: "25"
  ANDROID_BUILD_TOOLS: "24.0.0"
  ANDROID_SDK_TOOLS: "24.4.1"

before_script:
  - apt-get --quiet update --yes
  - apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1
  - wget --quiet --output-document=android-sdk.tgz https://dl.google.com/android/android-sdk_r${ANDROID_SDK_TOOLS}-linux.tgz
  - tar --extract --gzip --file=android-sdk.tgz
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter android-${ANDROID_COMPILE_SDK}
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter platform-tools
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter build-tools-${ANDROID_BUILD_TOOLS}
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-android-m2repository
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-google_play_services
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-m2repository
  - export ANDROID_HOME=$PWD/android-sdk-linux
  - export PATH=$PATH:$PWD/android-sdk-linux/platform-tools/
  - chmod +x ./gradlew

stages:
  - build
  - test

build:
  stage: build
  script:
    - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/

unitTests:
  stage: test
  script:
    - ./gradlew test

functionalTests:
  stage: test
  script:
    - wget --quiet --output-document=android-wait-for-emulator https://raw.githubusercontent.com/travis-ci/travis-cookbooks/0f497eb71291b52a703143c5cd63a217c8766dc9/community-cookbooks/android-sdk/files/default/android-wait-for-emulator
    - chmod +x android-wait-for-emulator
    - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter sys-img-x86-google_apis-${ANDROID_COMPILE_SDK}
    - echo no | android-sdk-linux/tools/android create avd -n test -t android-${ANDROID_COMPILE_SDK} --abi google_apis/x86
    - android-sdk-linux/tools/emulator64-x86 -avd test -no-window -no-audio &
    - ./android-wait-for-emulator
    - adb shell input keyevent 82
    - ./gradlew cAT
```

_[Source](https://gitlab.com/greysonp/gitlab-ci-android/blob/master/.gitlab-ci.yml)_

Well, that's a lot of code! Let's break it down.

### Understanding `.gitlab-ci.yml`

#### Defining the Docker Image
{:.special-h4}

```yml
image: openjdk:8-jdk
```

This tells [GitLab Runners](https://docs.gitlab.com/ee/ci/runners/README.html#runners) (the things that are executing our build) what [Docker image](https://hub.docker.com/explore/) to use. If you're not familiar with [Docker](https://hub.docker.com/), the TL;DR is that Docker provides a way to create a completely isolated version of a virtual operating system running in its own [container](https://www.sdxcentral.com/cloud/containers/definitions/what-is-docker-container-open-source-project/). Anything running inside the container thinks it has the whole machine to itself, but in reality there can be many containers running on a single machine. Unlike full virtual machines, Docker containers are super fast to create and destroy, making them great choices for setting up temporary environments for building and testing.

This [Docker image (`openjdk:8-jdk`)](https://hub.docker.com/_/openjdk/) works perfectly for our use case, as it is just a barebones installation of Debian with Java pre-installed. We then run additional commands further down in our config to make our image capable of building Android apps.

#### Defining variables

```yml
variables:
  ANDROID_COMPILE_SDK: "25"
  ANDROID_BUILD_TOOLS: "24.0.0"
  ANDROID_SDK_TOOLS: "24.4.1"
```

These are variables we'll use throughout our script. They're named to match the properties you specify in your app's [`build.gradle`](https://gitlab.com/greysonp/gitlab-ci-android/blob/master/app/build.gradle).

- `ANDROID_COMPILE_SDK` is the version of Android you're compiling with. It should match `compileSdkVersion`.
- `ANDROID_BUILD_TOOLS` is the version of the Android build tools you are using. It should match `buildToolsVersion`.
- `ANDROID_SDK_TOOLS` is a little funny. It's what version of the command line tools we're going to download from the [official site](https://developer.android.com/studio/index.html). So, that number really just comes from the latest version available there.

#### Installing packages
{:.special-h4}

```yml
before_script:
  - apt-get --quiet update --yes
  - apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1
```

This starts the block of the commands that will be run before each job in our config.

These commands ensure that our package repository listings are up to date, and it installs packages we'll be using later on, namely: `wget`, `tar`, `unzip`, and some packages that are necessary to allow 64-bit machines to run Android's 32-bit tools.

#### Installing the Android SDK

```yml
  - wget --quiet --output-document=android-sdk.tgz https://dl.google.com/android/android-sdk_r${ANDROID_SDK_TOOLS}-linux.tgz
  - tar --extract --gzip --file=android-sdk.tgz
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter android-${ANDROID_COMPILE_SDK}
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter platform-tools
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter build-tools-${ANDROID_BUILD_TOOLS}
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-android-m2repository
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-google_play_services
  - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-m2repository
```

Here we're downloading the Android SDK tools from their official location, using our `ANDROID_SDK_TOOLS` variable to specify the version. Afterwards, we're unzipping the tools and running a series of `android` commands to install the necessary Android SDK packages that will allow our app to build.

#### Setting up the environment

```yml
  - export ANDROID_HOME=$PWD/android-sdk-linux
  - export PATH=$PATH:$PWD/android-sdk-linux/platform-tools/
  - chmod +x ./gradlew
```

Finally, we wrap up the `before_script` section of our config with a few remaining tasks. First, we set the `ANDROID_HOME` environment variable to the SDK location, which is necessary for our app to build. Next, we add the platform tools to our `PATH`, allowing us to use the `adb` command without specifying its full path, which is important when we run a downloaded script later. Finally, we ensure that `gradlew` is executable, as sometimes Git will mess up permissions.

#### Defining the stages

```yml
stages:
  - build
  - test
```

Here we're defining the different [stages](https://docs.gitlab.com/ce/ci/yaml/README.html#stages) of our build. We can call these anything we want. A stage can be thought of as a group of [jobs](https://docs.gitlab.com/ce/ci/yaml/README.html#jobs). All of the jobs in the same stage happen in parallel, and all jobs in one stage must be completed before the jobs in the subsequent stage begin. We've defined two stages: `build` and `test`. They do exactly what you think: the `build` stage ensures the app compiles, and the `test` stage runs our unit and functional tests.

#### Building the app

```yml
build:
  stage: build
  script:
    - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/
```

This defines our first job, called `build`. It's the only job in the `build` stage. It just builds the debug version of the app and makes the outputs of the build available for download via the `artifacts` field.

#### Running unit tests

```yml
unitTests:
  stage: test
  script:
    - ./gradlew test
```

This defines a job called `unitTests` that runs during the `test` stage. Nothing crazy here – we're just running unit tests.

#### Running functional tests

```yml
functionalTests:
  stage: test
  script:
    - wget --quiet --output-document=android-wait-for-emulator https://raw.githubusercontent.com/travis-ci/travis-cookbooks/0f497eb71291b52a703143c5cd63a217c8766dc9/community-cookbooks/android-sdk/files/default/android-wait-for-emulator
    - chmod +x android-wait-for-emulator
    - echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter sys-img-x86-google_apis-${ANDROID_COMPILE_SDK}
    - echo no | android-sdk-linux/tools/android create avd -n test -t android-${ANDROID_COMPILE_SDK} --abi google_apis/x86
    - android-sdk-linux/tools/emulator64-x86 -avd test -no-window -no-audio &
    - ./android-wait-for-emulator
    - adb shell input keyevent 82
    - ./gradlew cAT
  artifacts:
    paths:
    - app/build/reports/androidTests/
```

This defines a job called `functionalTests` that runs during the `test` stage. Functional tests are a little tricky to set up. First, we download a script that will allow us to detect when an emulator has finished booting. Then, we download the emulator system image we're going to use and create an instance of it. Afterwards, we start the emulator, wait for it to finish booting using our downloaded script, use `adb` to send a signal to unlock the screen, and run our tests. After running these tests, the generated test report is made available for download via the `artifacts` field.

## Run your new CI setup

After you've added your new `.gitlab-ci.yml` file to the root of your directory, just push your changes and off you go! You can see your running builds in the **Pipelines** tab of your project. You can even watch your build execute live and see the runner's output, allowing you to debug problems easily.

![Pipelines tab screenshot](/images/blogimages/setting-up-gitlab-ci-for-android-projects/artifacts-tutorial-01.png){:.shadow}

After your build is done, you can retrieve your build artifacts:

- First, click on your completed build:

![Build details button screenshot](/images/blogimages/setting-up-gitlab-ci-for-android-projects/artifacts-tutorial-02.png){:.shadow}

- Then, navigate to the **Builds** tab:

![Builds tab screenshot](/images/blogimages/setting-up-gitlab-ci-for-android-projects/artifacts-tutorial-03.png){:.shadow}

- Lastly, click on the download button for your desired job:

![Download button screenshot](/images/blogimages/setting-up-gitlab-ci-for-android-projects/artifacts-tutorial-04.png){:.shadow}

## Conclusion

So, there you have it! You now know how to create a GitLab CI config that will ensure your app:

- Compiles
- Passes unit tests
- Passes functional tests

And allows you to access your build artifacts (like your [APK](https://en.wikipedia.org/wiki/Android_application_package)) afterwards.

Enjoy your newfound app stability :)

## About Guest Author

[Greyson Parrelli](http://www.greysonparrelli.com/) is an Android developer at Snap Inc. working on [Snapchat](https://play.google.com/store/apps/details?id=com.snapchat.android&hl=en). Previously, he's worked on the [YouTube](https://play.google.com/store/apps/details?id=com.google.android.youtube&hl=en), [Yahoo! Weather](https://play.google.com/store/apps/details?id=com.yahoo.mobile.client.android.weather&hl=en), and [Yahoo! Mail](https://play.google.com/store/apps/details?id=com.yahoo.mobile.client.android.mail&hl=en) Android apps.

<!-- closes https://gitlab.com/gitlab-com/blog-posts/issues/28 -->
<!-- cover image: https://unsplash.com/photos/aso6SYJZGps -->

<style>
  img {
    display: block;
    margin: 0 auto 20px auto;
  }
  .special-h4 {
    margin-top: 20px !important;
  }
</style>
