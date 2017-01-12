---
title: "Proposed server purchase for GitLab.com"
author: Sid Sijbrandij
author_twitter: sytses
categories: gitlab
image_title: '/images/default-blog-image.png'
description: "What hardware we're considering purchasing now that we have to move GitLab.com to metal."
---

We want to make GitLab.com fast and we [knew it was time to leave the cloud](https://about.gitlab.com/2016/11/10/why-choose-bare-metal/) and purchase our own servers.
In this post is our thinking about what chassis, rack, memory, CPU, network, power, and hosting to buy.
We wanted to share what we learned and get your feedback on our proposal and questions.
When you reply to a question in the comments on our blog or Hacker News please reference it with the letter and number: 'Regarding R1'.
We'll try to update the questions with preliminary answers as we learn more.

<!-- more -->

# Overview

Today, GitLab.com hosts 96TB of data, and that number is growing rapidly. We
are attempting to build a fault-tolerant and performant CephFS cluster. We are
also attempting to move GitLab application servers and supporting services
(e.g. PostgreSQL) to bare metal.

Note that for now our CI Runners will stay in the cloud. Not only are they are
much less sensitive to latency, but autoscaling is easier with a cloud service.

# Chassis

One of the team members that will join GitLab in 2017 recommended using a [6028TP-HTTR SuperMicro 2U Twin2 server](https://www.supermicro.nl/products/system/2U/6028/SYS-6028TP-HTTR.cfm) chassis that has 4 dual processor nodes and is 2 [rack units](https://en.wikipedia.org/wiki/Rack_unit) (U) high. The advantages are:

1. Great density, 0.5U per dual processor server
1. You have one common form factor
1. Power supplies are shared for great efficiency similar to [blade servers](https://en.wikipedia.org/wiki/Blade_server)
1. The network is per node for more bandwidth and reliability (like individual server)

We use the [2U Twin2](https://www.supermicro.com/products/nfo/2UTwin2.cfm) instead of the [1U Twin](https://www.supermicro.com/products/nfo/1UTwin.cfm) because it fits one more 3.5" hard drive (3 per node instead of 2).

This server is on the list of global SKU's for SuperMicro.
We'll also ask for quotes from other vendors to see if they have a competitive alternative.
For example HPE has the [Apollo 2000 series](https://www.hpe.com/h20195/v2/getpdf.aspx/c04542552.pdf?ver=7).

C1 Should we use another version of the chassis than HTTR?

C2 What is the best Dell equivalent? => [C6320](http://www.dell.com/us/business/p/poweredge-c6320/pd)

# Servers

We need the following servers:

1. 32x File storage (CephFS OSD)
1. 3x File Monitoring (CephFS MON)
1. 8x Application server ([Unicorn](https://bogomips.org/unicorn/))
1. 7x Background jobs ([Sidekiq](http://sidekiq.org/))
1. 5x Key value store ([Redis Sentinel](https://redis.io/topics/sentinel))
1. 4x Database (PostgreSQL)
1. 3x Load balancers (HAproxy)
1. 1x Staging
1. 1x Spare

For a total of 64 nodes.

We would like to have one common node so that they are interchangable.
This would mean installing only a few disks per node instead of having large fileservers.
This would distribute failures and IO.

![IOPS on GitLab.com](/images/blogimages/write_iops.png)

The above picture shows the currently number of Input/output Operations Per
Second (IOPS) on GitLab.com. On our current NFS servers, our peak write IOPS
often hit close to 500K, and our peak read IOPS reach 200K. These numbers
suggest that using spinning disks alone may not be enough; we need to use
high-performance SSDs judiciously.

One task that we could not fit on the common nodes was PostgreSQL.
Our current plan is to make PostgreSQL distributed in 2017 with the help of [Citus](https://www.citusdata.com/).
But for now, we need to scale vertically so we need a lot of memory and CPU.
We need at least a primary and secondary database.
We wanted to add a second pair for testing and to ensure spares in case of failure.
Details about this are in the following sections.

Choosing a common node will mean that file storage servers will have too much CPU and that application servers will have too much disk space.
We plan to remedy that by running everything on Kubernetes.
This allows us to have a blended workload using all CPU and disk.
For example we can combine file storage and background jobs on the same server since one is disk heavy and one is CPU heavy.
We will start by having one workload per server to reduce complexity.
This means that when we need to grow we can still unlock almost twice as much disk space and CPU by blending the workloads.
Please note that this will be container based, to get maximum IO performance we won't virtualize our workload.

S1 Shall we spread the database servers among different chassis to make sure they don't all fail when one chassis fails?

S2 Does Ceph handle running 60 OSD nodes well or can this cause problems?

# CPU

The [SuperServer 6028TP-HTTR](https://www.supermicro.nl/products/system/2U/6028/SYS-6028TP-HTTR.cfm) supports dual E5-2600v4 processors per node.
We think the [E5-2630v4](http://ark.intel.com/products/92981/Intel-Xeon-Processor-E5-2630-v4-25M-Cache-2_20-GHz) is a good blend of power and cost.
It has 20 virtual cores at 2.20Ghz, 25MB cache, and costs about $669 per processor.
Every physical core is two virtual cores due to [hyperthreading](https://en.wikipedia.org/wiki/Hyper-threading).
A slightly more powerful processor is the [E5-2640v4](https://ark.intel.com/products/92984/Intel-Xeon-Processor-E5-2640-v4-25M-Cache-2_40-GHz) but while the [SPECint score](https://en.wikipedia.org/wiki/SPECint) increases from 845 to 887 the costs increase from $669 to $939.
You can find the scores by entering a [search on spec.org](https://www.spec.org/cgi-bin/osgresults?conf=rint2006) with 'Hewlett Packard Enterprise' as the hardware vendor and looking for ProLiant DL360 Gen9 as the platform.

Our current SQL server has one E5-2698B v3 with 32 virtual cores.
PostgreSQL commonly uses about 20-25 virtual cores.
Moving to dual processors should already help a lot.
To give us more months to grow before having to distribute the database we want to purchase some headroom.
That is why we're getting a [E5-2687Wv4](https://ark.intel.com/products/91750/Intel-Xeon-Processor-E5-2687W-v4-30M-Cache-3_00-GHz) for the database servers.
This processor costs $2100 instead of $670 but has 4 extra virtual cores and runs continuously on 3 Ghz instead of 2.2 Ghz.
Comprated to the E5-2630v4 that leads to a SPEC score or 1230 instead of 845 and 51.3 SPEC per virtual core instead of 42.3.
For the 4 dual processor database servers this upgrade will cost $11k.
We think it is worth it since the 20-40% of extra performence will buy us the month or two of extra time to distribute the database that we need.

# Disk

Every node can fit 3 larger (3.5") harddrives.
We plan to purchase the largest one available, a 8TB Seagate with 6Gb/s SATA and 7.2K RPM.
At 60 nodes this will give us 1.4PB of raw storage.
At a replication factor of 3 for Ceph this is 480TB of usable storage.
Right now GitLab.com uses 96TB (54TB for repo's, 21TB for uploads, 21TB for LFS and build artifacts) so we can grow by a factor of almost 5.

Disks can be slow so we looked at improving latency.
Higher RPM hard drives typically come in [GB instead of TB sizes](http://www.seagate.com/enterprise-storage/hard-disk-drives/enterprise-performance-15k-hdd/).
Going all SSD is too expensive.
To improve latency we plan to fit every server with an SSD card.
On the fileservers this will be used as a cache.
We're thinking about using [Bcache](https://en.wikipedia.org/wiki/Bcache) for this.

We plan to use [Intel DC P3700 series](http://www.intel.com/content/www/us/en/solid-state-drives/ssd-dc-p3700-spec.html) or slight less powerful [P3600 series](http://www.intel.com/content/www/us/en/solid-state-drives/ssd-dc-p3600-spec.html) of SSD's because they are recommended by the CephFS experts we hired.
For most servers it will be the [800GB SSDPEDMD800G4](http://www.supermicro.com/products/nfo/PCI-E_SSD.cfm?show=Intel).
For the database servers we plan to use the the 1.6TB variant to have more headroom.
The endurance we need for the database server is 90TB/year, the 3600 series is already above 4PB of endurance.

We plan to add a 64GB [SSD SATADOM boot drive](https://www.supermicro.com/products/nfo/SATADOM.cfm) to the servers to boot from.
This way we can keep the large SSD as a separate volume.

D1 We plan to configure the disks as just a bunch of disks (JBOD) but heard that this caused performance problems with some controllers. Is this likely to impact us?

D2 Should we use Bcache to improve latency on on the Ceph OSD servers with SSD? => Make sure you're using a kernel >= 4.5, since that's when a bunch of stability patches landed (https://lkml.org/lkml/2015/12/5/38).

D3 We heard concerns about fitting the PCIe 3.0 x 4 SSD card into [our chassis](https://www.supermicro.nl/products/system/2U/6028/SYS-6028TP-HTTR.cfm) that supports a PCI-E 3.0 x16 Low-profile slot. Will this fit? => [Florian Heigl](http://disq.us/p/1eedj2n): "Somewhat unlikely you will be able to fit a P3700. I have a Twin^2 too and the only SSD I could fit there was a consumer NVME with a PCIe adapter board."

D4 Should we ask for 8TB HGST drives instead of Seagate since they seem [more reliable](https://www.backblaze.com/blog/hard-drive-reliability-stats-q1-2016/).

D5 Is it a good idea to have a boot drive or should we use [PXE boot](https://en.wikipedia.org/wiki/Preboot_Execution_Environment) every time it starts? => [dsr_](https://news.ycombinator.com/item?id=13153336): You want a local boot drive, and you want it to fall back to PXE booting if the local drive is unavailable. Your PXE image should default to the last known working image, and have a boot-time menu with options for a rescue image and an installer for your distribution of choice.

D6 Should we go for the 3700 series SSD or save some money and go for the 3600 series? Both for the normal and the SQL servers?

D7 We're planning on one SSD per node. For the OSD nodes (file server) that would mean having the Ceph journal and bcache on the same SSD. Is this a good idea?

# Memory

Suppose one node runs both as application server and fileserver.
We recommend virtual cores + 1 instances of Unicorn of about 0.5GB each, for a total of 21GB per node (2 processors * 21 unicorns per processor * 0.5GB).
Ceph recommends about 1GB per TB of data which comes out to 24 per node.
So theoretically we can fit everything in 45GB so 64GB should be enough.

But in practice we've seen 24TB OSD nodes use 79GB of memory.
And the rule of thumb is have about 2GB per virtual core for background jobs available (40GB).
So in order not to be to low we'll spend the extra $30k to have 128GB of ECC memory per node instead of 64GB.

For the SQL nodes we'll need much more memory, we currently give it 440GB and it uses all of that.
The database is about 250GB in size and growing with 40GB per month.
At 250GB of server memory we redlined the server, probably because it no longer fits into memory.
Theoretically the server supports 2TB of memory but it needs to fit in 16 memory slots per node.
We wanted to start with 1TB per server but we're not sure if we should go from a 64GB DIMM to 128GB to be able to expand later.
By having only half of the memory banks full you get half the bandwidth.
And 64GB DIMMs already cost twice as much per GB as 32GB DIMMs, let alone 128GB ones.
At a price of about $940 per 64 DIMM the cost for 1TB of memory already is $15k per server.

Note that larger sizes such as 64GB come in the form of LRDIMM that has a [small performance penalty](https://www.microway.com/hpc-tech-tips/ddr4-rdimm-lrdimm-performance-comparison/) but this looks acceptable.

M1. Should we use 128GB DIMMS to be able to expand the database server later even though the will double the cost and half the bandwidth?

# Network

The servers come with 2x 10Gbps RJ45 by default (Intel X540 Dual port 10GBase-T).
We want to [dual bound](https://docs.oracle.com/cd/E37670_01/E41138/html/ch11s05.html) the network connections to increase performance and reliability.
This will allow us to take routers out of service during low traffic times, for example to restart them after a software upgrade.
We think that 20Gbps is enough bandwidth to handle our data access and replication needs, right now our higest peaks are 1 Gbps.
This is important because we want to have minimal latency between the Ceph servers so network congestion would be a problem.

Ceph reference designs recommend a seperated front and back network with the back network reserved for Ceph traffic.
We think that this is not needed as long as there is enough capacity.
We do want to have user request termination in a DMZ, so our HA proxy servers will be the only ones with a public IP.

Each of the two physical network connections will connect to a different top of rack router.
We want to get a Software Defined Networking (SDN) compatible router so we have flexibility there.
We're considering the [10/40GbE SDN SuperSwitch (SSE-X3648S/SSE-X3648SR)](https://www.supermicro.com/products/accessories/Networking/SSE-X3648S.cfm) that can switch 1440 Gbps.

Apart from those routers we'll have a separate router for a 1Gbps management network.
For example to make [STONITH](https://en.wikipedia.org/wiki/STONITH) reliable when there is a lot of traffic on the normal network.
Each node already has a separate 1Gbps connection for this.

We have 64+1 nodes (1 for backup) and most routers seem to have 48 ports.
Every node has 2 network ports so that is a need for 130 ports in total.
We're not use if we can use 3 routers with 48 ports each (144 in total) to cover that.

N1 Which router should we purchase?

N2 How do we interconnect the routers while keeping the network simple and fast?

N3 Should we have a separate network for Ceph traffic?

N4 Do we need an SDN compatible router or can we purchase something more affordable?

N5 What router should we use for the management network?

# Backup

We're still early in figuring out the backup solution so there are still lots of questions.

Backing up 480TB of data (expected size in 2017) is pretty hard.
We thought about using [Google Nearline](https://cloud.google.com/storage-nearline/) because with a price of $0.01 per GB per month means that for $4800 we don't have to worry about much.
But restoring that over a 1Gbps connection takes 44 days, way too long.

We mainly want our backup to protect us against human and software errors.
Because all the files are already replicated 3 times hardware errors are unlikely to affect us.
Of course we should have a good [Ceph CRUSH map](http://docs.ceph.com/docs/jewel/rados/operations/crush-map/) to prevent storing multiple copies on the same chassis.

We're most afraid of human error or Ceph corruption. For that reason we don't want to replicate on the Ceph level but on the file level.

We're thinking about using [Bareos backup software](https://www.bareos.org/en/) to replicate to a huge fileserver.
We're inspired by the posts about the [latest 480TB Backblaze storage pod 6.0](https://www.backblaze.com/blog/open-source-data-storage-server/) and these are available for $6k without drives from [Backuppods](https://www.backuppods.com/).
But SuperMicro offers a [comparable solution in the form of a SuperChassis that can hold 90 drives](https://www.supermicro.com/products/chassis/4U/946/SC946ED-R2KJBOD).
At 8TB per drive that is 720TB of raw storage.
Even with RAID overhead it should be possible to have 480TB of usable storage (66%).

The SuperChassis is only hard drives, it still needs a controller. In a [reference architecture by Nexenta (PDF download)](https://nexenta.com/sites/default/files/docs/Nexenta_SMC_RA_DataSheet.pdf) two [SYS6028U](https://www.supermicro.com/products/system/2u/6028/sys-6028u-tr4_.cfm) with E5-2643v3 processors and 256GB of RAM is recommended. Unlike smaller configurations this one doesn't come with an SSD for [ZFS L2ARC](https://blogs.oracle.com/brendan/entry/test).

Since backups are mostly linear we don't need an SSD for caching. In general 1GB of memory per TB of raw ZFS disk space is recommended. That would mean getting 512GB of RAM, 16x 32GB. Unlike the reference architecture we'll go with one controller. We're considering the [SuperServer 1028R-WC1RT](https://www.supermicro.com/products/system/1U/1028/SYS-1028R-WC1RT.cfm) since it is similar to our other servers, 1U, has 2x 10Gbps, 16 DIMM slots, and has 2 PCI slots. We'll use our regular [E5-2630v4](http://ark.intel.com/products/92981/Intel-Xeon-Processor-E5-2630-v4-25M-Cache-2_20-GHz) processor.

The question is if this controller can saturate the 20 Gbps uplink.
For this it needs to use both 12 Gbps SAS buses.
And each drive has to do at least 30 MBps which seems reasonable for a continuous read.

The problem is that even at 20Gbps a full restore takes 2 days.
Of course many times you need to restore only part of the files (uploads).
And most of the time it won't contain 480TB (we'll start at about 100TB).
The question is if we can accept this worst case scenario for GitLab.com.

An alternative would be to use multiple controllers.
But you can't aggregate ZFS pools over multiple servers.
Another option would be to have one controller with more IO.
We can use multiple disk enclosures and multiple SAS buses.
And we can add more network ports and/or switch to 40Gbps.
But this all seems pretty complicated.

B0 Are we on the right track here or is 20 Gbps of restore speed not OK?

B1 Should we go for the [90 or 60 drive SuperChassis](https://www.supermicro.com/products/chassis/4U/?chs=946)? It looks like 60 drive one has more peak power (1600W vs. 800W) to start the drives.

B2 How should we configure the SuperChassis? [ZFS on Linux](http://zfsonlinux.org/) with [RAIDZ3](https://icesquare.com/wordpress/zfs-performance-mirror-vs-raidz-vs-raidz2-vs-raidz3-vs-striped/)?

B3 Will the SuperChassis be able to saturate the 20Gbsp connection?

B4 Should we upgrade the networking on the SuperChassis to be able to restore even faster?

B5 Is Bareos the right software to use?

B6 How should we configure the backup software?  Should we use incremental backups with parallel jobs to speed things up?

B7 Should we use the live filesystem or [CephFS snapshots](http://docs.ceph.com/docs/master/dev/cephfs-snapshots/) to back up from?

B8 How common is it to have a tape or cloud backup in addition to the above?

B9 Should we pick the top load model or [one of the front and rear access models](https://www.supermicro.com/products/chassis/JBOD/index.cfm?show=SELECT&storage=90).

B10 Can we connect two SAS cables to get 2x 12 Gbps?

B11 What [HBA card](https://www.supermicro.com/products/nfo/storage_cards.cfm) should be added to the controller or does it come with an LSI 3108?

B12 Is it smart to make the controller a seperate 1U box or should we repurpose some of our normal nodes for this?

B13 Any hints on how to test the backup restore (on AWS or our hardware, how often, etc.)?

# Rack

The default rack height seems to be 45U nowadays (42U used to be the standard).

It is used as follows:

- 32U for 16 chassis with 64 nodes
- 3U for three network routers
- 1U for the management network
- 4U for the disk enclosure
- 1U for the disk controller
- 4U spare for 2 new chassis (maybe distributed PostgreSQL servers)

# Power

Each chassis has a 2000 watt power supply (comes to 1kW per U), 32kW in total.
Normal usage is guessed at 60% of the rated capacity, about 19kW.
That doesn't account for the routers and backup.
Both hosting providers quoted 4 x 208v 30A power supplies (2 for redundancy).

P1 Does the quoted supply seem adequate for our needs?

# Hosting

We've worked in [an issue](https://gitlab.com/gitlab-com/infrastructure/issues/732) to see where we should host.

Apart from the obvious (reliable, affordable) we had the following needs:

- [AWS Direct connect](https://aws.amazon.com/directconnect/details/) so we can use the cloud for temporary application server needs
- Based on the east coast of the USA since it provides the best latency tradeoff for most of our users
- Advanced remote hands service so we don't have to station people near the datacenter at all times
- Ability to upgrade from one rack to a private cage

The following networking options are a plus:

- Carrier neutral (all major global network providers in its meet-me facility)
- Backbones to other locations to provide cheap 2nd site transit
- CDN services to reduce origin bandwidth costs

So far we've gotten quotes from [QTS in Ashburn, VA](http://www.qtsdatacenters.com/data-centers/ashburn) and [NYI in Bridgewater, NJ](https://www.nyi.net/datacenters/new-jersey/).

H1 Any watchouts when selecting hosting providers?

H2 Should we install the servers ourselves or is it OK to let the hosting provider do that?

H3 How can we minimize installation costs? Should we ask to configure the servers to PXE boot?

H4 Is there an Azure equivalent for AWS Direct Connect? => Azure will let you work with a provider to "peer into" the Azure network at a data center of your choice. So for example we could pay to have a circuit established in a data center that was linked into the Azure 'US East 2' data center (where we currently host out of) for direct connectivity needs.

# Expense

We can't give cost details since all the quotes we receive are confidential.
The cloud hosting for GitLab.com excluding GitLab CI is currently costing us about $200k per month.
The capital needed for going to metal would be less than we pay for 1 quarter of hosting.
The hosting facility costs look to be less than $10k per month.
If you spread the capital costs over 2.5 years (10 quarters) it is 10x cheaper to host your own.

Of course the growth of GitLab.com will soon force us to buy additional hardware.
But we would also have to pay extra for additional cloud capacity.
Our proposed buying plan is about 5x the capacity we need now.
Having your own hardware means you're always overprovisioned.
And we could probably have reduced the cost of cloud hosting by focussing on it.

The bigger expense will be hiring more people to deal with the additional complexity.
We'll probably need to hire a couple of people more to deal with this.
We're hiring [production engineers](https://about.gitlab.com/jobs/production-engineer/) and if you're spotting mistakes in this post we would love to talk to you (and if you didn't spot many mistakes but think you can help us we also want to talk to you).

We looked into initially having disks in only half the servers but that saves only $20k ($225 per disk) and it would create a lot of work when we eventually have to install them.

E1 If we want to look at leasing should we do that through SuperMicro or third party?

E2 Are there ways we can save money?

# Details

Our detailed calculations and notes can be found in a [public Google sheet](https://docs.google.com/spreadsheets/d/1XG9VXdDxNd8ipgPlEr7Nb7Eg22twXPuzgDwsOhtdYKQ/edit#gid=894825456).
