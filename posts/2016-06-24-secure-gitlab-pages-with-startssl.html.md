---
layout: post
title: "Secure GitLab Pages with StartSSL"
date: 2016-06-24 09:00:00
comments: true
categories: [technical overview, tutorial]
author: Marcia Ramos
author_twitter: virtuacreative
image_title: '/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-cover.jpg'
---

<i class="fa fa-exclamation-triangle red" aria-hidden="true"></i>
<span class="red">**WARNING**</span>
<i class="fa fa-exclamation-triangle red" aria-hidden="true"></i>
**StartCom** certificates have recently been **distrusted** by [Mozilla Firefox](https://blog.mozilla.org/security/2016/10/24/distrusting-new-wosign-and-startcom-certificates/) and [Google Chrome](https://security.googleblog.com/2016/10/distrusting-wosign-and-startcom.html). Certs issued prior to October 21st, 2016 don't seem to have been affected and are therefore still trusted.<br>
In response to my contact, StartCom affirmed they're working hard to revert this situation and hope to have a resolution by the end of January, 2017.<br>
<span class="note">Update by Marcia Ramos, on 2016/12/20.</span>
{:.alert .alert-warning .black}

With [GitLab Pages][pages] you can host your static website under your custom domain.
With a [StartSSL] digital certificate you can secure it. And that's all for **free**!

In this post, first we'll give you a quick overview on SSL/TLS certificates and StartCom CA, then
we will show you a comparison between [StartSSL Class 1][startssl-class-1] and [Let's Encrypt][lets]
to facilitate your decision to choose one over another.

Finally, we will guide you through the process of securing your GitLab Pages site
with **[StartSSL Class 1 free certificates][startssl-class-1]**.

**Note:** We assume you are familiar with web development and web hosting.
{: .note}

<!-- more -->

----------

### What's in this tutorial?
{:.no_toc}

- TOC
{: toc}

----

## HTTPS: a quick overview

### Why should I care about HTTPS?

Perhaps this might be your first question. If our sites are hosted by [GitLab Pages][pages],
therefore they are [static][ssg-post], hence we are not dealing with server-side scripts
nor credit card transactions, so why do we need secure connections? 

Back in the 1990s, where HTTPS came out, [SSL]<sup>[1](#1)</sup> was considered a "special"
security measure, necessary just for big folks, like banks and shoppings sites with financial transactions.
Now we have a different picture. [According to Josh Aas][lets-quote], [ISRG] Executive Director:

> _We’ve since come to realize that HTTPS is important for almost all websites. It’s important for any website that allows people to log in with a password, any website that [tracks its users][lets-ref1] in any way, any website that [doesn’t want its content altered][lets-ref2], and for any site that offers content people might not want others to know they are consuming. We’ve also learned that any site not secured by HTTPS [can be used to attack other sites][lets-ref3]._

How about taking Josh's advice and protecting our sites too? We will be well supported,
and we'll contribute to a safer internet.

### Organizations supporting HTTPS

There is a huge movement in favor of securing all the web. W3C fully [supports the cause][w3c-https]
and explains very well the reasons for that. Richard Barnes, a writer for Mozilla Security Blog,
suggested that [Firefox would deprecate HTTP][moz-http-deprecate], and would no longer accept
unsecured connections. Recently, Mozilla published a [communicate][moz-comm] reiterating the importance of HTTPS.

### Free SSL/TLS Certificates

As individuals, dealing with small sites for promoting ourselves and our work, we might not be
interested in buying a premium<sup>[2](#2)</sup> [TLS]<sup>[1](#1)</sup> certificate issued by
a robust [Certification Authority (CA)][wiki-ca], like [Comodo] or [Symantec]. But now we have a
choice! We can use free certificates, like the ones issued by [Let's Encrypt][lets] and [StartCom][startssl].

----

[](){: name="1"}

**Note 1:** [SSL] stands for **Secure Sockets Layer**, which is the predecessor of **Transport Layer Security** ([TLS]).
{: .note}

[](){: name="2"}

**Note 2:** Premium certificates examples: [Comodo SSL/TLS][comodo-ssl], [StartSSL SSL Class 2][startssl-class-2],
[Symantec SSL][symantec-ssl]. They offer support for e-commerce and grant a huge warranty to their customers.
{: .note}

----

## StartCom

[Start Commercial Ltd. (StartCom)][startssl] was [founded][startssl-about] by [Eddy Nigg] in 2005,
who wanted to engage in a "revolution" of the digital certification industry, making certificates
more affordable and with better quality. StartCom has become the world's sixth largest Certificate
Authority, covering nearly one million registered subscribers, and more than 400,000 websites.

[StartSSL™][startssl-class-1] is the [StartCom][startssl] service brand of its digital certificates
issuing division, it offers [free SSL certificates][startssl-about] and free email encryption certificates
for worldwide subscribers. Thus, on this post, **StartCom** refers to the **Certificate Authority**,
while **StartSSL** is attributed to **certificates** issued by **StartCom**.

Among four classes of StartSSL certificates, there is one **free**, called [Class 1][startssl-class-1].
This is the one will be referencing to in this post. But, of course, you are free to choose their premium products too.
On their website, you can find a [comparison chart][startssl-compare] for their certificates.

[StartCom Certificate Policy & Practice Statements][startssl-policy] covers a lot of procedures to make
sure they can trust their customers information. That document states rules, obligations, validations, etc.
General information can be found through their [documentation][startssl-docs].

### StartSSL Class 1 Features

- Certificates can be [issued in minutes][startssl-class-1]
- There are two methods of domain verification: email, or code file validation<sup>[3](#3)</sup> 
- [Certificates are valid for 1 year][startssl-one-year], with [unlimited renewal allowance][startssl-renewal]
- The [CSR (Certificate Signing Request)][csr] can be generated from any O.S. (Linux, Mac or Windows)
- S/MIME Client<sup>[4](#4)</sup> + Authentication
- Supported by [all browsers and servers][startssl]
- Live chat support 24/7

----

[](){: name="3"}

**Note 3:** Code file validation is a file provided by an institution, which needs to be uploaded
to the site root. It's a simple HTML file containing a token to verify that we hold that particular
domain. It's not used just by CAs. For example, it is also used by Google,
as a [method for site ownership verification][google-verif].
{: .note}

[](){: name="4"}

**Note 4:** [S/MIME][wiki-smime] client certificates are used for client authentication to
websites and for the signing, encryption and decryption of personal data. Most commonly they
are used for email signing and encryption, but also PDF and office documents. Higher validated
certificates can be used to sign contracts in digital format. Source:
[StartCom UI - Certificates][startssl-certs] (you'll need to be logged into StartCom to have access to this link).
{: .note}

----

### StartSSL Class 1 Limitations

**StartSSL Class 1** certificates cover a lot of attractive features, but have some [limitations][startssl-compare]:

- There is no support for [wildcard DNS record][wildcard], `*.example.com` 
- We are limited to issue certificates for up to 5 domains
- We can't use commercial "sensitive" names for our domains or subdomains (e.g, "store", "buy", "shop", etc)
- [Revocations carry a handling fee][startssl-revocation] of currently US$ 9.90. Though we may
use a different subdomain in order to create additional certificates without the need to
revoke a previously created certificate

### StartSSL **vs** Let's Encrypt

[Let's Encrypt][lets] is a free, automated, and open Certificate Authority (CA), provided by
[Internet Security Research Group (ISRG)][isrg]. They are the first CA to offer exclusively
free certificates. They are great, their product is awesome. However, they have some limitations
too. To facilitate our overview and compare Let's Encrypt to StartSSL Class 1 certificates,
let's take a look at the table below.

| Feature | StartSSL Class 1 | Let's Encrypt |
| ---- | :---- | :---- |
| **Cost** | Free | Free |
| **Expiration** | <i class="fa fa-check" style="color: green;"></i> [In 1 year][startssl-class-1-features] (365 days) | [In 3 months][lets-renewal] (90 days) |
| **Client Install / CSR** | <i class="fa fa-check" style="color: green;"></i> All OSs | Complicated on [Windows][lets-win] |
| **CSR method** | <i class="fa fa-check" style="color: green;"></i> Desktop App or command line | Command line only |
| **Browser Support** | <i class="fa fa-check" style="color: green;"></i> [All][startssl-about] | [Most of them][lets-browser-support] |
| **Server Support** | [All][startssl-about] | All, with [plugins][lets-plugins] | 
| **Revocation** | [Paid][startssl-revocation] | <i class="fa fa-check" style="color: green;"></i> [Free][lets-features] |
| **S/MIME Client Auth** | <i class="fa fa-check" style="color: green;"></i> [Supported][startssl-class-1-features] | [Not supported][lets-smime] |
| **Insurance** | <i class="fa fa-check" style="color: green;"></i> [$ 10,000 USD][startssl-class-1-features] | [None][lets-features] | 
| **Customer support** | <i class="fa fa-check" style="color: green;"></i> [Live Chat, Phone][startssl-support], Ticket | [Forum][lets-forum] |
| **Hash Algorithm** | <i class="fa fa-check" style="color: green;"></i> SHA-256, SHA-384, SHA-512 | [SHA-256][lets-sha-256] |
| **Domain validation** | <i class="fa fa-check" style="color: green;"></i> Email or Code file Validation | [Code file validation][lets-domain-validation] |
| **Domains limit** | [5 domains][startssl-class-1-features] | <i class="fa fa-check" style="color: green;"></i> [Limited][lets-limits] |
| **Subdomains** | Supported | Supported |
| **Free domains** | Supported | Supported |
| **Domain name** | Non-commercial names | <i class="fa fa-check" style="color: green;"></i> Unrestricted |
| **Wildcard support** | No | No | 
| **Support EV certificates** | [Upgrading (paid)][start-ssl-ev] | No |

The information gathered within the table above is available across [StartCom][startssl] website,
their [FAQ][startssl-faq] and their [Policy][startssl-policy]. 

For additional info on Let's Encrypt, you can read their [Certificate Policy][lets-cp],
their [documentation][lets-docs], and this post [Tutorial: Securing your GitLab Pages
with TLS and Let's Encrypt][gitlab-post-lets].

## StartSSL with GitLab Pages

Digital certificates are applicable to your [GitLab Pages][pages] project only when you 
se a **custom domain**, as all standard `https://namespace.gitlab.io` urls are secure by default.

With GitLab Pages we can host our static website, use custom domains (and aliases), and secure our
domains with SSL/TLS certificates **for free**. Cost zero, no credit card, no hidden fees! This is
detailed in the tutorial "[Hosting on GitLab.com with GitLab Pages][gitlab-post-pages]". Also, you can
read the [quick start guide][pages], and the [documentation][pages-doc] for GitLab Pages.

GitLab Pages supports [PEM] certificates issued by any [CA][wiki-ca], though we need to make sure
that the certificate is compatible with [NGINX], the server [where GitLab runs on][gitlab-nginx].

StartCom certificates are retrievable from their [User Interface (UI)][startssl], where you have
access to your own information, certificates requests, expiration dates, etc. 

### Before getting started

For the following steps, we assume:

- You already have your custom domain
- Your project is configured for GitLab Pages 
- Your site is accessible under `http://example.com` or `http://your.example.com` 

If you don't know how to do that, please check this tutorial first: [Hosting on GitLab.com with GitLab Pages][gitlab-post-pages].

## Step-by-step

The scheme below illustrates the steps we'll take to secure our GitLab Pages sites with StartSSL Class 1 certificates:

![StartSSL with GitLab Pages - step-by-step scheme](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-scheme.png)

### Step 1: Getting started with StartCom

#### Sign up

StartCom login is certificate-based, which is considered a [high-security user authentication][pki-google-book] method.
Unlike other mechanisms for web-based authentication, certificates ensure the person or machine is who they claim to be.
[Certificate-based authentication][startssl-user-auth] also provides data encryption capabilities between the client and the server.

- Navigate to StartCom and [sign up][startssl-sign-up]
- Enter your country and email address to the respective fields
- Verify your e-mail (follow their instructions, which are very simple)
- The system will issue a certificate for your email and save it locally, which will be your
user authentication to log in. Choose "The system generate private key and CSR", enter your
password, and download the file
- [Import the certificate to your browser][import-cert-browser]. This will allow you to log
into your account in one click from then on 

On the next screen, StartCom will present all their certificate options. Choose the box "Free - Class 1 SSL".

#### Domain Validation 

Domain validation is necessary to make sure that the domain you are issuing the certificate for, is really yours.

- Open the tab **Validation Wizard** -> **Domain Validation** -> add your domain to the field -> **Continue**. 
- Choose the method for domain validation (**a** or **b**): 
   - (a) **e-mail**: take a look at the default emails presented on the box and see if you
   have access to one of them. If you don't, jump to "method **b**". Otherwise, first open
   your email account and keep it opened. Then, choose one of the radio buttons correspondent
   to your email and click on **Send verification code**. The code will be sent to your email,
   and it will be valid for only **60 seconds**. Switch to your email, copy the code, switch
   back to StartCom, and paste it to the field **Verification code** -> **Validation**. Done!
   - (b) **code file**: choose  **website control validation** -> download the code file and
   leave StartCom opened. Push the code file to your site root in your GitLab Pages project.
   Wait until the build succeeds. Go back to StartCom and click on **the verification file is ready on website, Continue**. Done!
- Once your domain was verified, click on the link **To "Order SSL Certificate"**

#### Certificate Request

- In the box **Please enter the full hostname for SSL certificate**, enter your domain name. There are a few options:
   - you can enter only the root domain 
   - enter the root domain and some subdomains 
   - enter multiple domains (up to 5). 

   Suggestion? Issue one different certificate per domain or subdomain; if something goes wrong, it will be just one to fix.
- Choose the first option: the radio button for PEM certificates **Generate by myself**.
It will open a text area where you'll add the CSR we'll generate next. Leave the tab opened<a name="tab-step-1"></a>.

![StartCom - Certificate Wizard - CSR](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-gen-csr.png)

### Step 2: Generate the CSR

For this particular step, we have two different approaches: [Linux and Mac](#unix) (Unix), or [Windows](#win).

[](){: name="unix"}

#### On Linux and Mac

- Open the terminal and check if you have [OpenSSL] installed: `$ openssl version`.
If the response is not `OpenSSL x.x.x date`, install it before continue
- Run the command recommended by StartCom:

      openssl req -newkey rsa:4096 -keyout yourkeyname.key -out yourkeyname.csr

  Use `sudo` if needed. Alternatively, you can keep the key length at `rsa:2048`.
  The file name (`yourkeyname`) can be chosen at your will
- Enter the PEM passphrase (it's like a password)
- Verify it by typing the same passphrase again. Memorize it or make a note.
- The terminal will ask you questions. Answer the first, then you can leave the others
blank if you want (hit Enter/Return). Done!

The files you'll need next will be in the `~home` directory. Open in a text editor both `yourkeyname.key`
and `yourkeyname.csr`. The first is your private encrypted key. The last is the CSR. The `.key` file will
be necessary for [Step 5](#step-5-decrypt-your-private-key) ahead. 

[](){: name="win"}

#### On Windows

**Note:** the numbers in the parenthesys correspond to the numbers on the image below.
{: .note}

- Download the binary file **StartComTool.exe** and launch it 
- Go to the tab **CSR** (1)
- On the top right, click a small link **Professional mode** (2)
- Choose the radio button **SSL Certificate** (3)
- Enter the **Domain name** to its field and fill the country information (4)
- Choose the radio button **Generate private key** (5)
- Enter a password (passphrase) and repeat it below (6). Memorize or make a note
- Choose the hash algorithm and the key length (7)
- Click **Generate CSR** (8)
- You will be prompted to choose a file name, and a directory to store both `yourkeyname.key` and
`yourkeyname.csr`. The `.key` file will be necessary for [Step 5](#step-5-decrypt-your-private-key) ahead.

The CSR will be shown in the box on the right of the application. Copy all the content (use the button **Copy**) (9).

The image below illustrates how the desktop application looks like:

![StartCom Tool - Windows](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-windows.png)

Alternatively, you can follow [these instructions][google-gen-csr] to generate the CSR via command line on Windows.

### Step 3: Issue your certificate

- Go back to [StartCom][startssl-csr-enter]
- Copy the content of the file `yourkeyname.csr`
- Paste it into the text-area we [had left opened](#tab-step-1) on Step 1
- Click **Submit**
- Done! Your certificate must have been issued!

### Step 4: Retrieve your certificate

When you download your certificate, you'll notice that it comes within a zipped folder with 4
options for you to use: Apache, Nginx, IIS, Other. The certificate you'll use for **GitLab Pages**
is the one in the `NginxServer` directory.

- On your StartCom UI, go to **Tool Box** -> **Certificate List** -> **Retrieve**
- Download and unzip the file
- Unzip the folder named `NginxServer`, your certificate will be there. It has a `.cf_bundle` extension
- Open the certificate with a text-editor and leave it opened. We'll need it for
[Step 6](#step-6-add-domain-and-certificate-to-your-project) ahead

The certificate looks like the code below.

```
-----BEGIN CERTIFICATE-----
MQswCKIhggfrOJmJJTDEWjkfhMNU3RhcndfjdfnuNJFHUnjfhjEGJSNSInjsnxLg
... 
nEFH63o+ycNl2jR29jd8c8c+MBIWrYGH8TPy0GCIguwTEzY=
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
MQswjsdbsfbdsfnKJHUNAIHoihushdiKHJUhcnRDsjdhJBSD786523987JHSDxLg
... 
3KSjh872631903rjfefy47fh49fjjqjdjqd9e8fuufe8MbLm==
-----END CERTIFICATE-----
```

### Step 5: Decrypt your private key

The key we'd generated on [Step 2](#step-2-generate-the-csr), `yourkeyname.key`, is our private **encrypted** key.
This key should **not** be used nor exposed. It's necessary to **decrypt** it before using. To make it easier to
recognize theses keys, observe that the code for an **encrypted** private key will always begin with
`BEGIN ENCRYPTED PRIVATE KEY`, while a **decrypted** private key will always begin with `BEGIN RSA PRIVATE KEY`.

There are two ways to proceed in this case: [via command line (option A)](#cmd) and via [StartCom UI (option b)](#ui).
Choose whichever option you feel more comfortable with.

[](){: name="cmd"}

#### Option A: Via command line

In your terminal, type 

```
openssl rsa -in yourkeyname.key -out yourkeyname-decrypted.key
```

where `yourkeyname` is the name of the encrypted key and `yourkeyname-decrypted.key` will be the name of the decrypted key.
Use the same password you set up before (on Step 2) when prompted. Your new key will be in your `~home` directory.

On Windows, proceed likewise, but `cd path/to/folder` before beginning. The decrypted key will be stored in the same
directory you've just navigated to.

[](){: name="ui"}

#### Option B: Via StartCom UI

- On your [StartCom UI][startssl], navigate to the **Tool Box** tab and click **Decrypt Private Key**
- Locally, open the private encrypted key in a text-editor. Copy all its content.
- Back to the UI, paste the content to the text-area and type your passphrase (used on Step 2)
- Click **Decrypt**
- Copy the decrypted key from the new box
- Paste the key in a new document and save it. Leave it opened, we'll need it for the next step
- Done!

The image below illustrates the result of the steps above.

![StartCom - decrypt private key](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-decrypt-key.png)

### Step 6: Add domain and certificate to your project

Finally, let's add the key and the certificate to our project:

- On your GitLab UI, open your **Project's Settings** (<i class="fa fa-cog" aria-hidden="true"></i>) and navigate to **Pages**
- If your domain (the one you just issued the certificate for) is already added to that project,
**remove** it. Don't worry, we'll add it back
- Click **+ New Domain**
- Add the domain to the first field
- Copy the certificate from [Step 4](#step-4-retrieve-your-certificate), and paste it to the second field
- Copy the **decrypted** private key from [Step 5](#step-5-decrypt-your-private-key), and paste it to the third field
- Click **Create New Domain**
- Done!

![StartCom - add key and certificate to GitLab project](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-demo.png)

If we've set up everything correctly, this is the screen we'll see on our GitLab UI:

![StartSSL + GitLab - valid certificate](/images/blogimages/startssl-gitlab-pages/startssl-gitlab-pages-certificate-valid.png)

Now your domain will be accessed under secure HTTPS protocol and will display on the browser the
green lock we were looking forward to see! You can perform a test to check your certificate
with [Site 24x7][site-24-7], if you want.

Do you want to see a working example of a GitLab Pages Project secure with StartSSL Class 1?
Visit <https://gitlab.virtuacreative.com.br> and click on the green lock
(<i class="fa fa-lock" style="color:rgb(0,192,29)" aria-hidden="true"></i>) to check the certificate.
This URL is an alias for <https://virtuacreative.gitlab.io>.

## Getting Help

If you need some help regarding GitLab Pages on GitLab.com,
feel free to use one of [our channels][get-help]. You can also
open an issue on the [Pages][pages-issues] group.

## Conclusion

<!-- TO BE IMPROVED -->

Hopefully, now you understand why HTTPS protocol is important even for static sites, and you know how to issue a free
certificate from [StartCom][startssl]. With secure urls, we are contributing to a better and safer internet!

Don't you have an account on [GitLab.com][sign-up] yet? Let's create one!
Remember, we can use GitLab Pages to [build any SSG][gitlab-post-pages] for us, and host any static site for free!

Follow [@GitLab][twitter] on Twitter and stay tuned for updates!

<!-- Green lock, public domain: https://commons.wikimedia.org/wiki/File:Move_protect.svg -->

<!-- Cover image, Creative Commons Zero: http://gratisography.com/ -->

<!-- IDENTIFIERS --> 

<!-- Alphabetical, miscellaneous -->

[comodo]: https://www.comodo.com/
[comodo-ssl]: https://ssl.comodo.com/?key5sk1=8721b4e5835982357f2a40802cc408ec59a88e2b
[csr]: https://en.wikipedia.org/wiki/Certificate_signing_request
[Eddy Nigg]: https://twitter.com/eddy_nigg
[google-verif]: https://support.google.com/webmasters/answer/35179?hl=en
[google-gen-csr]: https://developers.google.com/web/fundamentals/security/encrypt-in-transit/generating-keys-and-csr#generate-a-csr
[import-cert-browser]: http://help-icc.untangle.com/Content/User%20Guide/UI_Tabs/SSLCertificateGPO_v4/Appendix%20B%20Installing%20the.htm
[isrg]: https://en.wikipedia.org/wiki/Internet_Security_Research_Group
[lets]: https://letsencrypt.org/
[lets-browser-support]: https://community.letsencrypt.org/t/which-browsers-and-operating-systems-support-lets-encrypt/4394
[lets-cp]: https://letsencrypt.org/repository/
[lets-docs]: https://letsencrypt.readthedocs.org/en/latest/intro.html
[lets-domain-validation]: https://letsencrypt.org/how-it-works/#domain-validation
[lest-faq]: https://community.letsencrypt.org/t/frequently-asked-questions-faq/26
[lets-features]: http://letsencrypt.readthedocs.org/en/latest/intro.html?highlight=revoke#current-features
[lets-forum]: https://community.letsencrypt.org/
[lets-limits]: https://community.letsencrypt.org/t/rate-limits-for-lets-encrypt/6769
[lets-quote]: https://letsencrypt.org/2015/10/29/phishing-and-malware.html
[lets-plugins]: https://letsencrypt.readthedocs.org/en/latest/using.html#plugins
[lets-ref1]: https://www.washingtonpost.com/news/the-switch/wp/2013/12/10/nsa-uses-google-cookies-to-pinpoint-targets-for-hacking/
[lets-ref2]: http://arstechnica.com/tech-policy/2014/09/why-comcasts-javascript-ad-injections-threaten-security-net-neutrality/
[lets-ref3]: http://krebsonsecurity.com/2015/04/dont-be-fodder-for-chinas-great-cannon/
[lets-renewal]: http://letsencrypt.readthedocs.org/en/latest/using.html#renewal
[lets-requirements]: http://letsencrypt.readthedocs.org/en/latest/intro.html?highlight=revoke#system-requirements
[lets-sha-256]: https://community.letsencrypt.org/t/does-the-certificate-offer-a-sha-2-signature/8914
[lets-smime]: https://community.letsencrypt.org/t/s-mime-certificates/153
[lets-win]: https://cultiv.nl/blog/lets-encrypt-on-windows/
[moz-http-deprecate]: https://blog.mozilla.org/security/2015/04/30/deprecating-non-secure-http/
[moz-comm]: https://blog.mozilla.org/security/2016/03/29/march-2016-ca-communication/
[nginx]: https://www.nginx.com/
[openssl]: https://www.openssl.org/
[pages]: https://pages.gitlab.io/
[pages-doc]: http://doc.gitlab.com/ee/pages/README.html
[pem]: https://support.ssl.com/Knowledgebase/Article/View/19/0/der-vs-crt-vs-cer-vs-pem-certificates-and-how-to-convert-them
[pki-google-book]: https://books.google.com.br/books?id=oswvyhAftLsC&pg=PA69&redir_esc=y#v=onepage&q&f=false
[sha]: https://en.wikipedia.org/wiki/Secure_Hash_Algorithm
[site-24-7]: https://www.site24x7.com/ssl-certificate.html
[ssg-post]: https://about.gitlab.com/2016/06/03/ssg-overview-gitlab-pages-part-1-dynamic-x-static/
[symantec]: https://www.symantec.com/
[symantec-ssl]: https://www.symantec.com/ssl-certificates/
[startssl]: https://startssl.com
[startssl-about]: https://startssl.com/AboutUS
[startssl-certs]: https://startssl.com/Certificates
[startssl-class-1]: https://startssl.com/Support?v=1
[startssl-class-1-features]: https://startssl.com/Support?v=39
[startssl-class-2]: https://startssl.com/Support?v=2
[startssl-compare]: https://startssl.com/#ComparisonChart
[startssl-csr-enter]: https://startssl.com/Certificates/ApplySSLCert
[startssl-docs]: https://startssl.com/policy
[start-ssl-ev]: https://startssl.com/Support?v=39
[startssl-faq]: https://startssl.com/Support?v=25
[startssl-one-year]: https://startssl.com/Support?v=33
[startssl-policy]: https://startssl.com/policy.pdf
[startssl-renewal]: https://twitter.com/startssl/status/213348291654594560
[startssl-revocation]: https://startssl.com/Support?v=25#72
[startssl-sign-up]: https://startssl.com/SignUp
[startssl-support]: https://startssl.com/ContactUS
[startssl-user-auth]: https://www.entrust.com/wp-content/uploads/2013/05/DS_MSO_UserWebAuth_web_July2012.pdf
[static webpage]: https://en.wikipedia.org/wiki/Static_web_page
[ssl]: https://en.wikipedia.org/wiki/Transport_Layer_Security#SSL_1.0.2C_2.0_and_3.0
[tls]: https://en.wikipedia.org/wiki/Transport_Layer_Security
[w3c-https]: https://w3ctag.github.io/web-https/
[wiki-ca]: https://en.wikipedia.org/wiki/Certificate_authority
[wiki-smime]: https://en.wikipedia.org/wiki/S/MIME
[wildcard]: https://en.wikipedia.org/wiki/Wildcard_DNS_record

<!-- GitLab -->

[about-gitlab-com]: https://about.gitlab.com/
[get-help]: https://about.gitlab.com/getting-help
[gitlab-com]: https://about.gitlab.com/gitlab-com/
[pages]: https://pages.gitlab.io
[pages-ee]: http://doc.gitlab.com/ee/pages/README.html
[pages-issues]: https://gitlab.com/pages/pages.gitlab.io/issues
[gitlab-nginx]: http://doc.gitlab.com/ee/install/installation.html#nginx
[gitlab-post-lets]: https://about.gitlab.com/2016/04/11/tutorial-securing-your-gitlab-pages-with-tls-and-letsencrypt/
[gitlab-post-pages]: https://about.gitlab.com/2016/04/07/gitlab-pages-setup/
[sign-up]: https://gitlab.com/users/sign_in "Sign Up!"
[twitter]: https://twitter.com/gitlab

<style>
  .red { color: red !important; }
  .black { color: black !important; }
</style>

