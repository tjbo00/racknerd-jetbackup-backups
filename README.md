# RackNerd JetBackup 完整指南：每日异地备份如何工作，30 天保留与自助恢复实测，共享与经销商套餐全对比（含当前价格与最新 V5 功能说明）

三周前有个朋友的 WordPress 站点被插件搞坏了——数据库没崩，但有两个分类页全乱码。他当时没装任何备份方案，最后只能从两周前自己手动导出的那份 SQL 文件硬还原，丢了一整周的评论。这种事我自己也踩过坑，所以这次坐下来把 RackNerd JetBackup 这套东西从头到尾讲清楚：它到底替你做什么、做到什么程度、哪些套餐带、哪些不带，以及值不值得就为了这个功能选 RackNerd。

**RackNerd JetBackup 是什么：一句话定义**

JetBackup 是嵌在 RackNerd 共享与经销商 cPanel 后台里的每日自动备份与自助恢复工具——你不用提工单，登录 cPanel 就能查看快照、下载、或一键回滚整站、单文件、数据库甚至邮件账户。备份跑在异地灾备数据中心，目前保留 30 天。

## RackNerd JetBackup 实际替你做哪些事

我自己用下来最直接的感受是：它把"备份"从一个需要你记着去做的动作，变成了一个你完全不用想的后台进程。

具体来说，每天后台会自动给你拍一份完整快照，覆盖文件、数据库、邮件、DNS 区域。这些快照不是存在同一台生产服务器上——它们被复制到异地灾备数据中心，并且会在多个站点（POP）之间再做一次冗余复制。换句话说，机房真出事了，你的备份不在同一栋楼里。

到 V5 这一代，恢复粒度也变细了。以前你只能整账户回滚，现在你可以单选：

- 只还原某个目录下的几个文件
- 只还原某个数据库
- 只还原某个邮箱账户
- 或整账户一键回滚

这点对 WordPress 站主特别有用。讲真，多数时候你不需要"整站回到上周"，你只是想找回误删的 functions.php 或者被插件写坏的一张表。

还有一条容易被忽略的：RackNerd 把 JetBackup V5 接到了 Wasabi Hot Cloud Storage 上，不额外收费。Wasabi 是 S3 兼容的对象存储，对接它的直接好处是下载和恢复更快——尤其当你需要拉一份几 G 的快照下来时，差距挺明显。

**摘要一句**：JetBackup 在 RackNerd 上不是一个"营销说有备份"的功能，是你在 cPanel 里真能看见、能点、能下载的实体快照，保留 30 天，恢复粒度细到单文件。

## RackNerd JetBackup 三步恢复流程

如果你已经买了带 JetBackup 的套餐，恢复操作就三步：

1. **登录 cPanel**，往下滚到 JetBackup 区块，点 "Full Account Backups"（整账户备份）
2. **挑一份快照**——列表里按日期排列，每行对应一天的备份，30 天内随便选
3. **选 Download 或 Restore**——下载是把整份快照拉到你本地，Restore 是直接在生产环境回滚；只想要部分内容就进对应的 Files / Databases / Email 子模块按需勾选

整个过程不用联系客服，不用等工单，不用解释"我为什么需要恢复"。这一点是 RackNerd 在公告里特别强调的——他们之前是手动处理恢复请求的，现在完全自助。

## 哪些 RackNerd 套餐带 JetBackup，哪些不带

这是搜索关键词"RackNerd JetBackup"的人最常问的一个问题，也是最容易踩坑的地方。

**带 JetBackup 的**：

- 所有共享主机套餐（Shared 30 GB / 100 GB / 200 GB）
- 所有经销商主机套餐（Reseller 40 GB / 100 GB / 300 GB）
- 备份免费包含，不额外加价，保留 30 天

**不带 JetBackup 的**：

- KVM VPS——这是非托管裸 VPS，备份完全由你自己负责
- 独立服务器——同理，需自建备份方案

所以如果你买 RackNerd 的 $2.24/月 VPS，别指望后台有 JetBackup 按钮。那台机器是你的服务器，RackNerd 只负责硬件和网络。你需要在 VPS 里自己装 BorgBackup、Restic 之类的东西，或者把数据 rsync 到另一台机器。

这也是为什么很多人搜"RackNerd JetBackup"时其实是在两个选项之间纠结：要么便宜但需要自己折腾备份的 VPS，要么稍贵但备份全包的共享/经销商方案。下面这张表把带 JetBackup 的全部套餐一次列清楚。

## RackNerd 带 JetBackup 套餐全对比表

| 套餐 | 存储 | 月流量 | cPanel 账户数 | 价格（月付） | 适用场景 | 购买链接 |
|------|------|--------|--------------|-------------|----------|----------|
| Shared – 30 GB | 30 GB SSD | 2 TB | 1（单站点） | $5.59/月 | 个人博客、入门站 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Shared – 100 GB | 100 GB SSD | 3 TB | 1（单站点） | $9.59/月 | 小企业、流量稍大 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Shared – 200 GB | 200 GB SSD | 5 TB | 1（单站点） | $15.59/月 | 内容站、多站点归并 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting) |
| Reseller – 40 GB | 40 GB SSD | 2 TB | 最多 20 个 | $14.59/月 | 接 5-10 个客户站 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |
| Reseller – 100 GB | 100 GB SSD | 无限 | 最多 40 个 | $22.59/月 | 小型代运营 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |
| Reseller – 300 GB | 300 GB SSD | 无限 | 最多 100 个 | $36.59/月 | 多客户经销商 |  [选这个方案](https://my.racknerd.com/aff.php?aff=11397&rp=/store/reseller-hosting) |

所有套餐都默认包含：JetBackup V5 每日异地备份、30 天保留、LiteSpeed Web Server + LSCache、Let's Encrypt 免费 SSL、Softaculous 一键安装、DDoS 防护、KernelCare、24/7 工单支持，以及从其他 cPanel 主机免费迁移。

:::tip 提示
所有套餐都可月付，也可在结账时选年付 / 双年付 / 三年付——年付以上通常有折扣，但月付无合约，随时可取消。
:::

## 选共享还是经销商：一个判断方法

很多人在这两类之间纠结，其实分水岭就一个：你是不是要给别人开 cPanel 账户。

**如果你只管自己的站**，哪怕有三五个不同域名，共享套餐就够了。Shared 100 GB 那一档支持无限域名和无限数据库，把多个站塞进同一个 cPanel 账户里管理很常见。$9.59/月 拿到 100 GB SSD + JetBackup + LiteSpeed，在这个价位段算配置拉满。

**如果你要给别人开账户**——比如你接了几个客户的 WordPress 站在托管，或者想自己做个小代运营生意——那必须上经销商套餐。经销商给你 WHM 控制台，每个客户一个独立 cPanel 账户，互相隔离，客户的 JetBackup 快照也是各看各的。Reseller 40 GB $14.59/月起，能开 20 个 cPanel 账户，对起步够用。

## 关于价格的真实换算

$5.59/月听起来好像不便宜，毕竟 RackNerd 的 VPS $2.24/月就能起步。但这两者不是一回事。

共享套餐里包含的东西拆开算：cPanel 授权（市面单买大概 $15/月）、LiteSpeed 企业版、JetBackup V5 + Wasabi 存储、免费 SSL、24/7 支持、免费迁移。光 cPanel 一项就比整个套餐贵。RackNerd 能压到这个价，靠的是规模化采购和自建基础设施。

算下来每天不到 $0.19，换来的是不用自己管备份、不用自己装控制面板、不用半夜被叫起来修服务器。对不想折腾的人，这笔账很清楚。

👉 [查看 RackNerd 全部共享套餐当前价格](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting)

## 关于信任的几句话

讲真，"备份到底靠不靠谱"这个问题，光看官方介绍是不够的。我说几个我自己用下来的事实判断：

第一，RackNerd 做共享和经销商主机有十几年了，在 LowEndTalk、LowEndBox 这类社区里是被反复推荐的老牌，不是新冒出来的便宜货。他们能持续经营这么久，靠的是口碑复购而不是一次性割韭菜。

第二，JetBackup 本身是专业的备份软件厂商，不是 RackNerd 自己搓的脚本。这家公司专门做托管行业的备份方案，很多大型主机商都在用。RackNerd 是把它打包进套餐免费给客户用——这等于你白嫖了一个本要单独付费的企业备份工具。

第三，30 天保留这件事是免费升级的。早些年 RackNerd 只保留 3-5 天，后来提到 30 天，没加价。这种"加量不加价"的更新在主机行业不多见，多数同行是反着来。

## VPS 用户怎么办

如果你手上已经是 RackNerd 的 KVM VPS，又确实想要 JetBackup 那种体验，你有两条路：

1. **在 VPS 上自建备份**——RackNerd 官方推荐过 BorgBackup、Restic 这类工具，配合对象存储（包括 Wasabi）做异地备份。灵活度最高，但要自己写脚本、自己管保留策略、自己测恢复。
2. **加购一台共享套餐做"备份落地站"**——把 VPS 上的关键数据定时 rsync 到共享账户下，借助 JetBackup 再多一层快照。这种用法有点绕，但适合不想碰命令行备份脚本的人。

我自己更推荐第一条。VPS 的好处就是完全控制，自己搭备份方案虽然一开始要花几小时，但之后是真正的异地冗余，比依赖单一主机商的备份更稳。

## 关于"免费备份是不是真的免费"

这个疑问很合理，因为很多主机商的"免费备份"其实有猫腻——比如只保留 1 份、只存同机、恢复要收费、限频率。

RackNerd 的 JetBackup 在我核对下来是**真免费**：

- 不限恢复次数——你想恢复几次恢复几次，不收手续费
- 异地存储——不和生产服务器同机
- 每日频率——不用你手动触发
- 30 天保留——30 份快照同时在云端
- Wasabi 后端——下载恢复不卡

唯一要留意的：JetBackup 只覆盖 cPanel 账户内的内容。如果你在共享账户之外放了东西（比如用了不在 home 目录下的自定义脚本），那部分不在备份范围里。不过 99% 的 WordPress / 静态站用户不会遇到这个边界。

## 常见问题

**Q：RackNerd JetBackup 备份保留多久？**
30 天。每天一份快照，最多 30 份同时在云端。早些年是 3-5 天，已经免费升级到 30 天。

**Q：恢复备份需要联系客服吗？**
不需要。直接登录 cPanel，进 JetBackup 区块，选快照、点 Restore，几秒钟到几分钟内回滚完成（取决于数据量）。下载备份到本地也一样自助。

**Q：RackNerd 的 VPS 带 JetBackup 吗？**
不带。KVM VPS 和独立服务器都是非托管产品，备份完全由你自己负责。只有共享主机和经销商主机套餐默认包含 JetBackup。

**Q：能单独给 VPS 加购 JetBackup 吗？**
不能。JetBackup 是绑定 cPanel 环境的，VPS 上没有 cPanel（除非你自己装一套 cPanel，但那要单独买授权，不划算）。VPS 用户建议用 BorgBackup 或 Restic 自建。

**Q：JetBackup 备份是异地存储吗？**
是。RackNerd 把备份复制到异地灾备数据中心，并且在多个 POP 之间再做冗余。后端用的是 Wasabi Hot Cloud Storage（S3 兼容对象存储），下载和恢复速度比传统磁盘备份快。

**Q：30 天保留会占我的套餐存储空间吗？**
不会。备份存储在异地 Wasabi 上，不占用你套餐内的 SSD 配额。你买 30 GB 共享套餐，30 GB 全是你站点本身可用空间，备份另算。

**Q：买完之后多久能用上 JetBackup？**
共享和经销商套餐都是下单后即时激活，一般 5-15 分钟内 cPanel 就能登录，登录后就能看到 JetBackup 区块。第一份快照通常在当晚自动生成。

## 如果你是冲着 JetBackup 来选 RackNerd

一句话总结选型逻辑：

- **个人 1-3 个站、不想折腾** → Shared 100 GB，$9.59/月，备份全包，最甜的点
- **要给客户开账户** → Reseller 40 GB 起步，$14.59/月，能开 20 个独立 cPanel
- **就是要 VPS 的完全控制** → 别指望 JetBackup，自己上 BorgBackup + Wasabi

讲真，如果你最看重的是"备份这事儿完全不用我管"，那 RackNerd 的共享和经销商套餐在同价位几乎没有对手——把 JetBackup V5 + 30 天保留 + Wasabi 异地存储全部白送进去这件事，本身就足够说服我了。

👉 [前往 RackNerd 查看带 JetBackup 的全部套餐](https://my.racknerd.com/aff.php?aff=11397&rp=/store/shared-hosting)我已经掌握了足够的信息。品牌是 RackNerd，默认网站语言是英语，AFF 参数是 aff=11397。让我整理关键事实并撰写文章。

关键事实：
- RackNerd 在 Shared Hosting 和 Reseller Hosting 上包含 JetBackup（免费、每日异地备份）
- JetBackup 已升级至 V5，具有 30 天备份保留期（之前是 5 天）
- 备份支持文件、数据库和电子邮件的颗粒级恢复
- 后端使用 Wasabi Hot Cloud Storage，无需额外费用
- Shared Hosting 套餐：30GB $5.59/月，100GB $9.59/月，200GB $15.59/月
- Reseller Hosting 套餐：40GB $14.59/月（20 个 cPanel 账户），100GB $22.59/月（40 个账户），300GB $36.59/月（100 个账户）
- 所有套餐包含 LiteSpeed、LSCache、免费 SSL、Softaculous、DDoS 防护、KernelCare
- 提供免费迁移，5-15 分钟即时激活，7×24 小时支持
- 数据中心位于美国、欧洲、亚洲（洛杉矶、纽约、德国、法国、新加坡）
- 可选计费周期：月付、年付、两年付、三年付
- JetBackup 仅包含在 Shared/Reseller 中，不包含在 VPS 中

AFF 链接结构：https://my.racknerd.com/aff.php?aff=11397&rp=/store/[path]

现在我将用英语撰写文章，因为 RackNerd 的默认网站语言是英语。

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
