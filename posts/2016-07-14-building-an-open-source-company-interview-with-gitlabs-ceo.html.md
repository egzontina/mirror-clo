---
title: "Building an Open Source Company: Interview with GitLab's CEO"
author: Jason Chen
author_twitter: jhchen
categories: inside GitLab
image_title: '/images/team_gitlab.png'
---

Please note that while we think of ourselves as an open source company it would be more accurate to call it an open core company since we ship both the open source GitLab Community Edition and the close source GitLab Enterprise Edition. Thanks to paxcoder for [pointing this out on Hacker News](https://news.ycombinator.com/item?id=12129626).

[GitLab] began as a labor of love from [Dmitriy Zaporozhets] and [Valery Sizov], who built the first version together in 2011. Like many open source authors, they were only able to work on the project part time. [Sid Sijbrandij] joined forces a year later and created [GitLab.com], the first SaaS offering and first experiment with monetization.

<!-- more -->

Today GitLab is a model for open source sustainability and [stewardship]. It is being used in over 100,000 organizations including RedHat, NASA, Intel, Uber, and VMWare, to name just a few. Large organizations buy [enterprise licenses], sustaining and growing both the company and the free open source project. GitLab now has over 90 employees, including Sid and Dmitriy who serve as CEO and CTO, respectively.

**There has been a lot of discussion recently around long term sustainability in open source. Naturally, some of these conversations have turned towards companies. GitLab is one of the most successful examples of a company born out of and supporting an open source project. How do you think about open source in GitLab’s DNA and other similar open source companies?**
{: .alert .alert-info}

**Sid:** I think people are realizing more and more that open source is not just a license. It is also a way your company behaves. I think if you want to get the benefits of open source, it’s better to have an open development process. Everyone can see what’s going on all the time — what features are planned, who’s working on them, what was the decision process of how they would be implemented. We sometimes then receive comments on our issue tracker from real users explaining that a feature, given the way we designed and planned to build it, does not address their need. We learn from that and we get a better end product.

We took that a bit further at GitLab. We also just try to be very open as a company. Our complete company handbook — with many, many pages describing everything from sales, marketing, infrastructure — is completely open. We’re even going so far that our issue trackers for finance and marketing are open as well, so you can see what they are working on too. I’m not sure this is necessary, but being open is something we enjoy. It helps us be better and helps attract great new people to work with us.

**For open source projects that have gone down the company path, do you think open source itself is enough of a differentiator to be competitive against a similar proprietary product?**
{: .alert .alert-info}

**Sid:** I don’t think open source by itself is enough. Open source is wind in your back. It’s something that users and customers prefer. It’s a great go-to market, so it makes it a lot easier for people to adopt. It allows you, compared to previous enterprise software plays, to focus more on building a great product, and a bit less than previously on building a sales force. You’ll always need both the product and sales and marketing to be able to build a sustainable company.

We think GitLab is already the best product but we want to keep building to make it even better and communicate its value. GitLab is now the most popular solution for single-tenant installations. Our immediate goal is most revenue for single-tenant installations. Then we want to focus on private repositories through SaaS, then maybe someday public repositories. We’re not going to get there by just the power of open source.

**How did GitLab’s business model come about?**
{: .alert .alert-info}

**Sid:** At first I thought SaaS would be the sustainable business model for GitLab. People were using it, but mostly with smaller teams, not larger teams. The larger organizations were all running single tenant installations in house. They had a lot of feature requests so we kind of pivoted towards serving them better. Listening to those customers worked out really well. We built what they needed but shipped most of the features to everyone. The ones that were more appropriate for very large organizations with 100+ users, we put them into our proprietary enterprise product.
We then looked at the SaaS product and realized most of the revenue is going to come from single-tenant installations, so we decided to make the GitLab.com totally free — no restrictions on the number of private projects or collaborators and free CI.

**How did GitLab figure out its pricing?**
{: .alert .alert-info}

**Sid:** By making lots of mistakes. The common mistake that we’ve also made is that we priced too low. GitLab used to be $20/user/year, now it’s $40. I think it’s probably still on the low side.

**At Salesforce, I was told by an SVP if 20% of your customers are not upset at you over pricing, you are leaving money on the table.**
{: .alert .alert-info}

**Sid:** I think we have very few. I actually can’t think of a customer that’s really upset at us for our pricing, so probably we’re leaving too much money on the table. The great thing is we can make it work right now and we’re always close to being cash flow positive. We give away a lot, but that also helps companies adopt a product quickly. If it’s great value for money, it will spread faster.

**GitLab has a pretty impressive list of customers. How did they find out about GitLab? Did you do any marketing or outbound?**
{: .alert .alert-info}

**Sid:** No, nothing. They just found the open source project. If you wanted proper version control, single tenant, and open source, GitLab was and is the best option. We are just now beginning to do sales and hired three inbound SDRs and an outbound SDR Lead in the last two months, so we're just now starting to build those teams.

**Does GitLab’s success with the on premise model challenge the conventional wisdom that everything, including the enterprise is moving to the cloud?**
{: .alert .alert-info}

**Sid:** Yeah, I think it challenges it a bit. We still believe in the cloud, as in computing infrastructure. I think most GitLab installations run on AWS. But if you look according to research, in 2019, 80 cents of every dollar spent on software will go to on premises or single tenant software.

It differs for the product as well. I think right now everybody has accepted a cloud CRM solution. But we see that, for various reasons, source control is one of the last movers. Sometimes it’s for security reasons — companies want to put it behind a VPN — and sometimes it’s for legal reasons — companies want to know exactly where it’s hosted, and who has access to it.

**With so many of your users behind private installations, how do you get analytics and feedback from them?**
{: .alert .alert-info}

**Sid:** That’s hard. We don’t have a lot of data since GitLab doesn’t call home per se and we don’t want it to, as a good steward of the open source project. What GitLab does have is a version check. It shows you an image whether your version is up to date, out of date, or whether there’s a security problem with it. We receive those checks, so we can see what is out there in the wild, which helps a bit.

**Do you have to rely on users asking for features then?**
{: .alert .alert-info}

**Sid:** Yeah, we want to make user feedback easier by having open issue tracking. Anything we do feature-wise, it’s all happening on our issue tracker. When a sales person is talking with a customer and they have a request, we’ll post a public issue about it. We won’t tell you who the customer is, but the issue will be linked in our CRM system so internally we can all see who it is and what the interaction is or reach out to the customer to get more information. We really try to make everything happen in public. Before we used to have internal and external issue trackers, and we found there was a lot of duplication. This way, whatever we’re making, we get the best input. We get to get input from our developers, from the community, from our sales people and sometimes customers actually engage on the issue tracker themselves too.

**Has GitLab’s open source and SaaS offering been a good funnel into the enterprise offering?**
{: .alert .alert-info}

**Sid:** We actually crunched some numbers the other day, with some help of external people. We kind of expected our open source version to be a really good indicator of people getting the enterprise version. But it turned out that GitLab.com was an even better indicator. It was a lot more important than we thought as a go-to market and making people aware. Which is, for us, kind of nice, because we have e-mail addresses of the people using GitLab.com, so we can reach out to them. We don’t have that for people that download the community edition. So that finding was a relief to us.

**How did you decide to take GitLab from the sustainable business path, onto the venture funded company track?**
{: .alert .alert-info}

**Sid:** In 2014, we had a customer that was using GitLab, who then switched to GitHub, not because they didn’t like it, but because somewhere up the corporate hierarchy, it was decided that the whole company should use GitHub.

They were super happy with GitLab, but they still had to switch. We were like “Oh, wow. This might happen with all our large customers,” because every company in the world is going to standardize on one solution within the company. We want that to be GitLab. So we need to grow a lot faster to be able to convince those people at the top that make the decisions — the CIOs. And to reach them we need sales and marketing. We don’t have 10 years to do this, this standardization will happen in the next three years.

That’s why we decided to apply to YCombinator to grow faster. I think that’s been a good decision. By March of 2015, we were 9 people and fit into one large car. Now we’re 93 people and it takes two buses. We’ve since won back this customer, so we’re very glad about that. We don’t want to leave any customer behind. Our mission right now is to make sure all those large enterprises, who are probably using a couple of solutions internally right now, standardize on GitLab.

**It has been said that lot of software markets is winner takes all. Do you think, in the git hosting space, there will be a winner takes all?**
{: .alert .alert-info}

**Sid:** I think there’s room for multiple solutions. I think most companies will standardize on one thing for the whole company. I’ve talked to a few venture capitalists, and they say it’s common that 70% of the profit in the market goes to **#1**. Then **#2** has something, and number **3** ends up with very little.

As soon as you take VC money, you want to make sure you end up as **#1**. Also, we think it makes a lot of sense for developer collaboration software to be open source. And so we want people to use GitLab.

We’re excited. We think we have a great product, and we’re even more excited of what’s coming out next month and the month after that. We just want to make it a little bit better every month. That served us well so far, and that’s what we’re going to continue to do. We think there’s a big advantage to having the whole flow in one product, so we’re going to try to make the market aware of that.

_This post was originally posted on [medium.com] by [Jason Chen] himself._

<!-- Identifiers -->

[Jason Chen]: https://medium.com/@jhchen
[medium.com]: https://medium.com/@jhchen/290180d172da#.niptat9rb
[GitLab]: https://about.gitlab.com
[GitLab.com]: https://gitlab.com/users/sign_in
[Dmitriy Zaporozhets]: https://twitter.com/dzaporozhets
[Valery Sizov]: https://twitter.com/Sizov_Valeriy
[Sid Sijbrandij]: https://twitter.com/sytses
[stewardship]: https://about.gitlab.com/about/#our-stewardship-of-gitlab-cea-namestewardshipaa-nameour-stewardship-of-gitlab-cea
[enterprise licenses]: https://about.gitlab.com/pricing/
