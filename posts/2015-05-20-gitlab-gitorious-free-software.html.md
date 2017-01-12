---
title: "GitLab, Gitorious, and Free Software"
date: 2015-05-20
author: Mike Gerwitz
license: CC-BY-SA 3.0

---

*This is a guest post by [Mike Gerwitz][11], a [free software][2] hacker and
 activist, and author of [GNU ease.js][24].*

In early March of this year, it was announced that
[GitLab would acquire Gitorious][0] and shut down `gitorious.org` by 1
June, 2015.  [Reactions from the community][1] were mixed, and
understandably so: while GitLab itself is a formidable alternative to wholly
proprietary services, its acquisition of Gitorious strikes a chord with the
free software community that gathered around Gitorious in the name of
[software freedom][2].

<!-- more -->

After hearing that announcement,
[as a free software hacker and activist myself][11], I was naturally
uneasy.  Discussions of alternatives to Gitorious and GitLab ensued on the
[`libreplanet-discuss`][12] mailing list.  Sytse Sijbrandij (GitLab
B.V. CEO) happened to be present on that list;
[I approached him very sternly][13] with a number of concerns, just as I
would with anyone that I feel does not understand certain aspects of the
[free software philosophy][2].  To my surprise, this was not the case at
all.

Sytse has spent a lot of time accepting and considering community input for
both the Gitorious acquisition and GitLab itself.  He has also worked with
me to address some of the issues that I had raised.  And while these issues
won't address everyone's concerns, they do strengthen GitLab's commitment to
[software freedom][2], and are commendable.

I wish to share some of these details here; but to do so, I first have to
provide some background to explain what the issues are, and why they are
important.


## Free Software Ideology
[Gitorious][3] was (and still is) one of the most popular Git repository
hosts, and largely dominated until the introduction of GitHub.  But even as
users flocked to [GitHub's proprietary services][28], users who value freedom
continued to support Gitorious, both on `gitorious.org` and by installing
their own instances on their own servers.  Since Gitorious is
[free software][2], users are free to study, modify, and share it with
others.  But [software freedom does not apply to Services as a
Software Substitute (SaaSS)][4] or remote services---you cannot apply the
[four freedoms][2] to something that you do not yourself possess---so why do
users still insist on using `gitorious.org` despite this?

The matter boils down to supporting a philosophy:  The
[GNU General Public License (GPL)][6] is a license that turns copyright on
its head: rather than using copyright to restrict what users can do with a
program, the GPL instead [ensures users' freedoms][8] to study, modify, and
share it.  But that isn't itself enough: to ensure that the software always
remains free (as in freedom), the GPL ensures that all *derivatives* are
*also* licensed under similar terms.  This is known as [copyleft][9], and it
is vital to the free software movement.

Gitorious is licensed under the
[GNU Affero General Public License Version 3 (AGPLv3)][5]---this takes the
[GPL][6] and adds an additional requirement: if a modified version of the
program is run on a sever, users communicating with the program on that
server must have access to the modified program's source code.  This ensures
that [modifications to the program are available to all users][7]; they
would otherwise be hidden in private behind the server, with others unable
to incorporate, study, or share them.  The AGPLv3 is an ideal license for
Gitorious, since most of its users will only ever interact with it over a
network.

GitLab is also free software: its [Expat license][10] (commonly referred to
ambiguously as the "MIT license") permits all of the same freedoms that
are granted under the the GNU GPL.  But it does so in a way that is highly
permissive: it permits relicensing under *any* terms, free or not.  In other
words, one can fork GitLab and derive a proprietary version from it, making
changes that deny users [their freedoms][2] and cannot be incorporated back
into the original work.

This is the issue that the free software community surrounding Gitorious has
a problem with: any changes contributed to GitLab could in turn benefit a
proprietary derivative.  This situation isn't unique to GitLab: it applies
to all non-copyleft ("permissive") [free software licenses][26].  And this
issue is realized by GitLab itself in the form of its GitLab Enterprise
Edition (GitLab EE): a proprietary derivative that adds additional
features atop of GitLab's free Community Edition (CE).  For this reason,
many free software advocates are uncomfortable contributing to GitLab, and
feel that they should instead support other projects; this, in turn, means
not supporting GitLab by using and drawing attention to their hosting
services.

The copyleft vs. permissive licensing debate is one of the free software
movement's most heated.  I do not wish to get into such a debate here.  One
thing is clear: GitLab Community Edition (GitLab CE) is free
software.  Richard Stallman (RMS) [responded directly to the thread on
`libreplanet-discuss`][20], stating plainly:

>  We have a simple way of looking at these two versions.  The free
>  version is free software, so it is ethical.  The nonfree version is
>  nonfree software, so it is not ethical.

Does GitLab CE deserve attention from the free software community?  I
believe so.  Importantly, there is another strong consideration: displacing
proprietary services like GitHub and Bitbucket, which host a large number of
projects and users.  GitLab has a strong foothold, which is an excellent
place for a free software project to be in.

If we are to work together as a community, we need to respect GitLab's
free licensing choices just as we expect GitLab to respect ours.  Providing
respect does not mean that you are conceding: I will never personally use a
non-copyleft license for my software; I'm firmly rooted in my dedication to
the [free software philosophy][2], and I'm sure that many other readers are
too.  But using a non-copyleft license, although many of us consider it to
be a weaker alternative, [is not wrong][23].


## Free JavaScript
As I mentioned above,
[software freedom and network services are separate issues][4]---the four
freedoms do not apply to interacting with `gitlab.com` purely over a network
connection, for example, because you are not running its software on your
computer.  However, there is an overlap: JavaScript code downloaded to be
executed in your web browser.

[Non-free JavaScript][15] is a particularly nasty concern: it is software
that is downloaded automatically from a server---often without prompting
you---and then immediately executed.  Software is now being executed on your
machine, and [your four freedoms][2] are once again at risk.  This, then,
[is the primary concern][16] for any users visiting `gitlab.com`: not only
would this affect users that use `gitlab.com` as a host, but it would also
affect *any user that visits* the website.  That would be a problem, since
hosting your project there would be inviting users to run proprietary
JavaScript.

As I was considering migrating my projects to GitLab, this was the
[first concern I brought up to Sytse][14].  This problem arises because
`gitlab.com` uses a GitLab EE instance: if it had used only its Community
Edition (GitLab CE)---which is free software---then all served JavaScript
would have been free.  But any scripts served by GitLab EE that are not
identical to those served by GitLab CE are proprietary, and therefore
unethical.  This same concern applies to GitHub, Bitbucket, and other
proprietary hosts that serve JavaScript.

Sytse surprised me by stating that he would be willing to
[freely license all JavaScript in GitLab EE][17], and by offering to give
anyone access to the GitLab EE source code who wants to help out.  I took
him up on that offer.  Initially, I had submitted a patch to merge all
GitLab EE JavaScript into GitLab CE, but Sytse came up with another,
superior suggestion, that ultimately provided even greater reach.

**I'm pleased to announce that Sytse and I were able to agree on a license
change (with absolutely no friction or hesitation on his part) that
liberates all JavaScript served to the client from GitLab EE instances.**
There are two concerns that I had wanted to address: JavaScript code
directly written for the client, and any code that produced JavaScript as
output.  In the former case, this includes JavaScript derived from other
sources: for example, GitLab uses CoffeeScript, which compiles *into*
JavaScript.  The latter case is important: if there is any code that
generates fragments of JavaScript---e.g. dynamically at runtime---then that
code must also be free, or users would not be able to modify and share the
resulting JavaScript that is actually being run on the client.  Sytse
accepted my change verbatim, while adding his own sentence after mine to
disambiguate.  At the time of writing this post, GitLab EE's source code
isn't yet publicly visible, so here is the relevant snippet from its
`LICENSE` file:

> The above copyright notices applies only to the part of this Software that
> is not distributed as part of GitLab Community Edition (CE), and that is
> not a file that produces client-side JavaScript, in whole or in part. Any
> part of this Software distributed as part of GitLab CE or that is a file
> that produces client-side JavaScript, in whole or in part, is copyrighted
> under the MIT Expat license.

## Further Discussion
My discussions with Sytse did not end there: there are other topics that
have not been able to be addressed before my writing of this post that would
do well to demonstrate commitment toward [software freedom][2].

The license change liberating client-side JavaScript was an excellent
move.  To expand upon it, I wish to submit a patch that would make GitLab
[LibreJS compliant][21]; this provides even greater guarantees, since it
would allow for users to continue to block other non-free JavaScript that
may be served by the GitLab instance, but not produced by it.  For example:
a website/host that uses GitLab may embed proprietary JavaScript, or modify
it without releasing the source code.  Another common issue is the user of
analytics software; `gitlab.com` uses Google Analytics.

If you would like to help with LibreJS compliance, please [contact me][11].

I was brought into another discussion between Sytse and RMS that is
unrelated to the GitLab software itself, but still a positive demonstration
of a commitment to [software freedom][2]---the replacement of Disqus on the
`gitlab.com` blog with a free alternative.  Sytse ended up making a
suggestion, saying he'd be "happy to switch to" [Juvia][22] if I'd help with
the migration.  I'm looking forward to this, as it is an important
discussion area (that I honestly didn't know existed until Sytse told me
about it, because I don't permit proprietary JavaScript!).  He was even kind
enough to compile a PDF of comments for one of our discussions, since he was
cognizant ahead of time that I would not want to use Disqus.  (Indeed, I
will be unable to read and participate in the comments to this guest post
unless I take the time to freely read and reply without running Disqus'
proprietary JavaScript.)

Considering the genuine interest and concern expressed by Sytse in working
with myself and the free software community, I can only expect that GitLab
will continue to accept and apply community input.


## Actions Speak Louder Than Words
It is not possible to address the copyleft issue without a change in
license, which GitLab is not interested in doing.  So the best way to
re-assure the community is through action.  [To quote Sytse][18]:

> I think the only way to prove we're serious about open source is in our
> actions, licenses or statements don't help.

There are fundamental disagreements that will not be able to be
resolved between GitLab and the free software community---like their
["open core" business model][19].  But after working with Sytse and seeing
his interactions with myself, RMS, and many others in the free software
community, I find his actions to be very encouraging.

*Are you interested in helping other websites liberate their JavaScript?
 Consider [joining the FSF's campaign][27], and
 [please liberate your own][16]!*

*This post is licensed under the
 [Creative Commons Attribution-ShareAlike 3.0 Unported License][25].*


[0]: https://about.gitlab.com/2015/03/03/gitlab-acquires-gitorious/
[1]: https://news.ycombinator.com/item?id=9138419
[2]: https://www.gnu.org/philosophy/free-sw.html
[3]: https://gitorious.org/
[4]: https://www.gnu.org/philosophy/who-does-that-server-really-serve.html
[5]: https://www.gnu.org/licenses/agpl.html
[6]: https://www.gnu.org/licenses/gpl.html
[7]: https://www.gnu.org/licenses/why-affero-gpl.html
[8]: https://www.gnu.org/licenses/quick-guide-gplv3.html
[9]: https://www.gnu.org/philosophy/pragmatic.html
[10]: https://www.gnu.org/licenses/license-list.html#Expat
[11]: http://mikegerwitz.com/
[12]: https://lists.gnu.org/mailman/listinfo/libreplanet-discuss
[13]: https://lists.gnu.org/archive/html/libreplanet-discuss/2015-03/msg00075.html
[14]: https://lists.gnu.org/archive/html/libreplanet-discuss/2015-04/msg00019.html
[15]: https://www.gnu.org/philosophy/javascript-trap.html
[16]: https://www.gnu.org/software/easejs/whyfreejs.html
[17]: https://lists.gnu.org/archive/html/libreplanet-discuss/2015-04/msg00020.html
[18]: https://news.ycombinator.com/item?id=9141801
[19]: https://lists.gnu.org/archive/html/libreplanet-discuss/2015-03/msg00076.html
[20]: https://lists.gnu.org/archive/html/libreplanet-discuss/2015-03/msg00095.html
[21]: https://www.gnu.org/software/librejs/free-your-javascript.html
[22]: https://github.com/phusion/juvia
[23]: https://www.fsf.org/blogs/rms/selling-exceptions
[24]: https://gnu.org/software/easejs
[25]: http://creativecommons.org/licenses/by-sa/3.0/
[26]: https://www.gnu.org/licenses/license-list.html
[27]: https://fsf.org/campaigns/freejs
[28]: http://mikegerwitz.com/about/githubbub
