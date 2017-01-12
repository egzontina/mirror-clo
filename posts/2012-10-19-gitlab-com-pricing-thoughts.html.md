---
title: Your thoughts on Gitlab.com pricing
tags: []
status: publish
type: post
published: true
meta:
  publicize_reach: a:2:{s:7:"twitter";a:1:{i:1532919;i:41;}s:2:"wp";a:1:{i:0;i:2;}}
  publicize_twitter_user: gitlabhq
  _wpas_done_1532919: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:776273100;b:1;}}
  _wpas_skip_1532919: '1'
  _elasticsearch_indexed_on: '2012-10-19 15:15:56'
---
The beta of Gitlab is going well and to date, more than 100 projects were created. People asked about the pricing of Gitlab.com and I would love to hear what you think about this subject. For me the 3 goals of the pricing are:

1. The pricing should **encourage using** Gitlab.com as much as possible
2. The pricing model should be** fair and easy** to understand
3. The price should be** related to** **the** **benefit** of using Gitlab.com

To achieve the first goal of encouraging usage I propose we have** unlimited free private repos** and offer a **free usage tier**. With free private repos, you never have to think twice about adding another repo. Of course public repos will be free as well when we start offering them. To achieve the second goal of making things fair and easy I think we should differentiate the plans only on **one dimension**. I never like when I'm charged by two dimensions (for example the number of users and the total file size) and I have to upgrade because I hit one limit but not the other. With one dimension (either users or total file size), you never have any waste. In addition, some people told me they hate having to upgrade to a much more expensive plan just to add one more user. A fair system would just **charge per user** without any arbitrary plan sizes. To relate the price to the benefit, we need to differentiate the offering. I believe that you get more benefit from version control when you work with more people on a project. So it would be logical to charge by the **number of users** on the private project with the largest number of collaborators. I also think that when you use Gitlab.com with an organisation, you get more benefit. Therefore, I would like to create** two plans**, professional and business. The business plan would get access to tools to quickly manage multiple people like groups and teams. Groups of projects will be introduced in Gitlab 3.0 and the introduction of teams of people is on the readmap. Two different plans would allow us to charge a **lower price** for people that use Gitlab without these tools. Considering the above, I think of the following pricing model:
- **Unlimited repositories**
- **Unlimited disk space**
- The price is based on the **number of collaborators on the private repo** with the most collaborators.
- For each plan the first **2 collaborators are free**, in this case you pay nothing.
- The **professional** plan (what is currently online for the beta test) is **$3 per additional user** per month (i.e. 5 collaborators are $9 per month).
- The business edition plan, which has groups and teams, is** $9 per additional user** (i.e. 10 collaborators are $72 per month).
- There will be a 1 month** free trail**.

What do you think we should do for our **beta users?** Maybe a discount, a free period or something else, please let me know what you think. We also want to encourage people to **participate** in the the Gitlab open source project. Maybe we can give [ everyone that committed to the project](https://github.com/gitlabhq/gitlabhq/graphs/contributors) a credit of $100? Please let me know what you think about the pricing plans, the amounts, the naming, the goals, the free tier, the beta user discount, etc. Please **comment on this post**.