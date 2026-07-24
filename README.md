

# RackNerd JetBackup Explained: How Daily Off-Site Backups Actually Work, 30-Day Retention, Self-Service Restore Walkthrough, and Every Shared & Reseller Plan Compared (with Current Pricing)

Three weeks ago a friend's WordPress site broke after a plugin update went sideways — the database didn't crash, but two category pages turned into garbled text. He had no backup solution running, and ended up hand-restoring from a SQL dump he'd exported two weeks earlier, losing a full week of comments. I've been in that exact spot myself, which is why I sat down to write this: a proper walkthrough of RackNerd JetBackup, what it actually does for you, how far it goes, which plans include it, which don't, and whether it's worth choosing RackNerd specifically for this feature.

**What RackNerd JetBackup is: a one-line definition**

JetBackup is the daily automated backup and self-service restore tool baked into the cPanel dashboard of every RackNerd Shared and Reseller hosting account — you don't open a support ticket, you log into cPanel and view snapshots, download them, or roll back the whole site, a single file, a database, or even a single email account with a click. Backups run on off-site disaster recovery infrastructure and are currently retained for 30 days.

## What RackNerd JetBackup Actually Does For You

The most direct thing I noticed using it: it turns "backup" from something you have to remember to do into a background process you can completely stop thinking about.

Here's what happens behind the scenes. Every day the system takes a full snapshot of your account — files, databases, emails, DNS zones. That snapshot doesn't sit on the same server as your live site. It gets shipped to an off-site disaster recovery datacenter and then re-replicated across multiple points of presence for redundancy. In plain terms: if the primary datacenter goes down hard, your backups are not in the same building.

With V5, restore granularity got a lot finer. Used to be you could only roll back the whole account. Now you can pick and choose:

- Restore just a few files in a specific directory
- Restore a single database
- Restore one email account
- Or roll the entire account back in one shot

That last part matters a lot for WordPress site owners. Most of the time you don't need "the whole site back to last Tuesday" — you need the functions.php you accidentally overwrote, or the one table a plugin corrupted. Granular restore turns a 40-minute panic into a 90-second fix.

**One thing people miss**: RackNerd integrated JetBackup V5 with Wasabi Hot Cloud Storage at no extra charge. Wasabi is an S3-compatible object storage service, and wiring it in means downloads and restores are noticeably faster — especially when you're pulling a multi-gigabyte snapshot down to your machine.

**Plain language summary**: JetBackup on RackNerd isn't a "we technically have backups" checkbox feature. It's a real set of snapshots you can see, click, and download inside cPanel, retained for 30 days, with restore granularity down to a single file.

## How RackNerd JetBackup Restore Works: 3 Steps

If you're on a plan that includes JetBackup, restoring takes three steps:

1. **Log into cPanel** and scroll down to the JetBackup section, then click "Full Account Backups"
2. **Pick a snapshot** from the list — they're arranged by date, one row per day, anywhere within the 30-day retention window
3. **Choose Download or Restore** — Download pulls the full snapshot to your local machine; Restore rolls it back live on the server. If you only need part of it, drill into the Files, Databases, or Email sub-sections and select what you want

No support ticket. No waiting. No explaining why you need a restore. RackNerd specifically called this out when they launched the feature — they used to handle restores manually, and the move to full self-service was the whole point of the upgrade.

## Which RackNerd Plans Include JetBackup, Which Don't

This is the question that brings most people to search "RackNerd JetBackup," and it's the easiest place to get confused.

**Plans that include JetBackup**:

- All Shared Hosting plans (Shared 30 GB / 100 GB / 200 GB)
- All Reseller Hosting plans (Reseller 40 GB / 100 GB / 300 GB)
- Backups are included at no additional charge, with 30-day retention

**Plans that do NOT include JetBackup**:

- KVM VPS — these are unmanaged bare VPS instances, backups are entirely your responsibility
- Dedicated Servers — same deal, you set up your own backup solution

So if you picked up a $2.24/month RackNerd VPS, don't expect a JetBackup button in any panel. That box is your server — RackNerd provides the hardware and network, and what happens to the data on it is on you. You'd need to install something like BorgBackup or Restic on the VPS yourself, or rsync your data to another machine.

This is why most people searching "RackNerd JetBackup" are actually weighing two options: a cheap VPS where they handle backups themselves, or a slightly pricier Shared/Reseller plan where backups are fully handled. The table below lays out every plan that includes JetBackup in one shot.

## Every RackNerd Plan With JetBackup: Full Comparison Table

| Plan | Storage | Monthly Bandwidth | cPanel Accounts | Price (monthly billing) | Best For | Get This Plan |
|------|---------|-------------------|-----------------|-------------------------|----------|---------------|
| Shared – 30 GB | 30 GB SSD | 2 TB | 1 (single account) | $5.59/month | Personal blog, entry-level site |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Shared – 100 GB | 100 GB SSD | 3 TB | 1 (single account) | $9.59/month | Small business, growing site |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Shared – 200 GB | 200 GB SSD | 5 TB | 1 (single account) | $15.59/month | Content-heavy site, multiple domains |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Reseller – 40 GB | 40 GB SSD | 2 TB | Up to 20 | $14.59/month | Hosting a handful of client sites |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |
| Reseller – 100 GB | 100 GB SSD | Unlimited | Up to 40 | $22.59/month | Small hosting reseller business |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |
| Reseller – 300 GB | 300 GB SSD | Unlimited | Up to 100 | $36.59/month | Established reseller with many clients |  [Get this plan with JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |

Every plan in this table includes the same core stack: JetBackup V5 daily off-site backups with 30-day retention, LiteSpeed Web Server with LSCache, free Let's Encrypt SSL certificates, Softaculous one-click installer, DDoS protection, KernelCare for live kernel patching, 24/7 support, and free migration from any other cPanel-based host.

:::tip Billing note
All plans are available month-to-month with no contract, or you can prepay annually / biennially / triennially during checkout for a discount. Month-to-month keeps things flexible; longer prepay locks in a lower effective rate.
:::

## Shared vs Reseller: One Quick Way To Decide

People get stuck between these two categories, but the dividing line is simple: are you going to create cPanel accounts for other people?

**If it's just your own sites** — even if you have three or five different domains — a Shared plan is enough. The Shared 100 GB plan supports unlimited domains and unlimited databases, so running multiple sites inside one cPanel account is completely normal. At $9.59/month you get 100 GB SSD storage plus JetBackup plus LiteSpeed, which is a stacked config for the price.

**If you're creating accounts for other people** — you're managing WordPress sites for clients, or starting a small hosting reseller business — you need a Reseller plan. Reseller gives you a WHM control panel where each client gets their own isolated cPanel account, and each client's JetBackup snapshots are visible only to them. The Reseller 40 GB plan starts at $14.59/month and lets you create up to 20 cPanel accounts, which is plenty for getting started.

## The Price Conversation: Worth Being Honest About

$5.59/month sounds like it's not cheap, especially when RackNerd's VPS starts at $2.24/month. But these are not the same product.

What's bundled into a Shared plan, broken out: cPanel license (which runs around $15/month if you buy it standalone), LiteSpeed Enterprise, JetBackup V5 with Wasabi storage, free SSL, 24/7 support, free migration. The cPanel license alone costs more than the entire plan at retail pricing. RackNerd can hit this price because of volume purchasing and owned infrastructure.

Works out to less than $0.19 per day, and what you get back is: you don't manage backups, you don't install a control panel, you don't get paged at 2am because the server is down. For anyone who doesn't want to babysit infrastructure, the math isn't really a question.

👉 [See all current RackNerd Shared plan pricing](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting)

## A Few Words On Trust

"Is the backup actually reliable" is a fair question, and reading marketing copy doesn't answer it. Here's what I can say from using it and from what's publicly verifiable:

First, RackNerd has been doing Shared and Reseller hosting for well over a decade. They're a known quantity in low-end hosting communities — not a brand that appeared last year with a flashy landing page. Companies that stick around that long in this market do it on repeat business, not one-time signups.

Second, JetBackup itself is a dedicated backup software vendor, not a script RackNerd cooked up. The company builds backup tooling specifically for the web hosting industry, and a lot of large hosts use it. RackNerd bundles it into plans for free — meaning you're getting an enterprise backup tool that would cost money separately, at zero additional cost.

Third, the 30-day retention was a free upgrade. RackNerd used to keep 3-5 days of snapshots, then moved everyone to 30 days without raising prices. "More for the same price" updates are uncommon in hosting — most providers trend the opposite direction over time.

## What If You Already Have A RackNerd VPS

If you're on a RackNerd KVM VPS and you want JetBackup-style protection, you have two real paths:

1. **Build your own backup on the VPS** — RackNerd's own blog references tools like BorgBackup and Restic, paired with object storage (including Wasabi) for off-site copies. Maximum flexibility, but you write the scripts, manage retention, and test restores yourself.
2. **Add a Shared plan as a backup target** — rsync your VPS data into a Shared account periodically, and let JetBackup take snapshots on top. It's a roundabout setup, but it works if you don't want to touch command-line backup tooling.

I lean toward option one. The whole point of a VPS is full control, and building your own backup, while it takes a few hours up front, gives you genuine off-site redundancy that isn't tied to a single provider's backup system.

## Is "Free Backup" Actually Free

The skepticism is reasonable, because a lot of hosts play games with "free backups" — keeping only one snapshot, storing it on the same server, charging a fee for restores, or limiting frequency.

From everything I've checked on RackNerd's JetBackup setup, it is genuinely free with no asterisks:

- Unlimited restores — restore as many times as you want, no fee
- Off-site storage — not on the same machine as your live site
- Daily frequency — no manual triggering required
- 30-day retention — 30 snapshots kept in cloud storage simultaneously
- Wasabi backend — downloads and restores aren't throttled

The one edge case to be aware of: JetBackup covers everything inside your cPanel account. If you've placed files outside your home directory (custom scripts in non-standard paths, for instance), those aren't in the backup scope. For 99% of WordPress, Joomla, or static site users, this never comes up.

## FAQ

**Q: How long does RackNerd JetBackup keep snapshots?**
30 days. One snapshot per day, up to 30 stored simultaneously. It used to be 3-5 days and was upgraded to 30 days at no extra cost.

**Q: Do I need to contact support to restore a backup?**
No. Log into cPanel, open the JetBackup section, pick a snapshot, click Restore. It completes in seconds to minutes depending on account size. Downloading a snapshot to your local machine is the same self-service process.

**Q: Does RackNerd's VPS come with JetBackup?**
No. KVM VPS and Dedicated Servers are unmanaged products where backups are your responsibility. JetBackup is included only with Shared Hosting and Reseller Hosting plans.

**Q: Can I add JetBackup to my VPS as a paid add-on?**
No. JetBackup is tied to the cPanel environment, and VPS plans don't include cPanel unless you install and license it separately, which isn't cost-effective. VPS users are better off with BorgBackup or Restic paired with object storage.

**Q: Are RackNerd JetBackup snapshots stored off-site?**
Yes. Snapshots are replicated to off-site disaster recovery datacenters and then re-replicated across multiple points of presence. The backend is Wasabi Hot Cloud Storage (S3-compatible object storage), which makes downloads and restores faster than traditional disk-based backup.

**Q: Does the 30-day backup retention eat into my plan's storage quota?**
No. Backups are stored on Wasabi's off-site infrastructure and don't count against your plan's SSD storage. If you buy the 30 GB Shared plan, you get the full 30 GB for your live site — backups are additional.

**Q: How quickly after signing up can I use JetBackup?**
Shared and Reseller plans activate within 5-15 minutes of ordering. Once cPanel is accessible, the JetBackup section is visible immediately. The first snapshot typically generates that same night during the daily backup run.

## If You're Choosing RackNerd Specifically For JetBackup

One-line decision logic:

- **Personal sites, 1-3 of them, no interest in managing infrastructure** → Shared 100 GB at $9.59/month. Backups fully handled, best value-per-dollar plan in the lineup.
- **Need to create cPanel accounts for clients** → Reseller 40 GB at $14.59/month. Up to 20 isolated cPanel accounts, each with their own JetBackup view.
- **Want full server control and don't mind self-managing backups** → Skip JetBackup entirely, go VPS, and set up BorgBackup with Wasabi yourself.

If the thing you care about most is "I never want to think about backups again," RackNerd's Shared and Reseller plans are hard to beat at this price point. Bundling JetBackup V5 with 30-day retention and Wasabi off-site storage into plans that start under $6/month is, honestly, enough of a reason on its own.

👉 [See all RackNerd plans that include JetBackup](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting)
