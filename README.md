# exchange online backup: what Microsoft's native option really costs, and when a $4/month Acronis plan is the smarter pick

People searching **exchange online backup** usually fall into one of two camps: those who just realized Microsoft 365's built-in retention mechanisms won't save them from accidental deletion, a disgruntled admin, or ransomware, and those already comparing third-party backup tools by price. Here's the short version up front: Microsoft now has a native product called Microsoft 365 Backup, priced at $0.15 per GB per month with free restores. Separately, Sharktech sells hosted Acronis Cyber Protect starting at $4/month with 200GB included, covering servers and Exchange Online mailboxes under one platform. That's a huge price gap, and the right answer depends entirely on what you're protecting. This article breaks down both options: real costs, the limitations that only show up in vendor documentation, and who each one actually fits.

> **Quick verdict:** If you're backing up servers (or already host with Sharktech) and want mailbox protection on the same bill, Sharktech's Acronis plan has the lowest entry cost — $4/month for 200GB, or $24/year on annual billing. If you only need to protect Microsoft 365 data and refuse to touch an agent, Microsoft's native backup is easier, but 500GB of protected data runs about $900 a year.
> 👉 Check the 200 GB Acronis plan and your configured total price

## Why Exchange Online still needs a backup

Microsoft's infrastructure redundancy for Exchange Online is excellent, but redundancy and backup solve different problems. Infrastructure resilience covers the case where Microsoft's own systems fail. When a person actually deletes your mailbox data — whether by accident, malice, or ransomware encrypting everything — the data is gone once Microsoft's retention windows run out. The clearest evidence that this gap is real: Microsoft built and now sells its own backup product, Microsoft 365 Backup. Official documentation describes it as a backup service, and the backup data lives in Append-Only storage that client processes (Outlook, OWA, MFCMAPI) cannot touch, so attackers can't corrupt historical copies.

So the question "do I need third-party backup for Exchange Online?" has already been answered by Microsoft themselves — with a paid product.

## Microsoft 365 Backup: what the official option actually costs

Microsoft 365 Backup is billed at **$0.15 per GB per month** across all protected data — Exchange mailboxes, OneDrive, and SharePoint — with restores free of charge.

Run the numbers and the weight of that price becomes obvious:

| Protected data | Monthly cost | Annual cost |
| --- | --- | --- |
| 100 GB | $15 | $180 |
| 500 GB | $75 | $900 |
| 1 TB | ~$150 | ~$1,800 |

What you get in return is one of the fastest restore experiences on the market. Microsoft claims restore throughput of up to 1–3 TB per hour for up to 1,000 average-sized mailboxes. Exchange gets a restore point every 10 minutes across the previous 52 weeks. Retention defaults to 1 year and is configurable per policy to 3 months, 6 months, 1 year, or 2 years. Backup data never leaves the Microsoft 365 trust boundary and respects your tenant's geographic data residency settings.

The fit here is clear: everything lives in Microsoft 365, you have no servers to protect, and you want restore speed and compliance backed by Microsoft itself. The tradeoff is that costs scale linearly with data volume — and the product does nothing for the servers, VMs, and local files outside your tenant.

## What third-party Exchange Online backup tools look like

Beyond Microsoft's native option, a few categories of vendors dominate this market, and their product shapes differ a lot:

- **ManageEngine** (M365 Security Plus, M365 Manager Plus, RecoveryManager Plus): Exchange Online backup is a paid add-on you purchase separately. Backup frequency runs daily, weekly, or monthly; retention can be set in days, months, or years, or configured to "back up forever" so nothing is ever discarded. Covered items include emails, calendar entries, contacts, and tasks, and backups can be exported as password-protected PST files.
- **Druva, NAKIVO, CrashPlan, Commvault, and Acronis**: standalone backup platforms that cover Exchange Online mailboxes along with much broader workloads.

One deployment detail most review articles skip: ManageEngine's Exchange Online backup in some cases requires the service account to hold the **ApplicationImpersonation** role — a role that, by default, is assigned to no user or group in Microsoft 365. You have to grant it manually through the admin center or PowerShell, and a newly assigned role **can take up to 48 hours to take effect**. If your deployment plan assumes "buy it and it runs," those 48 hours are enough to wreck a weekend migration window. RecoveryManager Plus also enforces a hard floor: the minimum item-level retention for Exchange Online backups is 30 days.

## Sharktech's Acronis plan: one provider for servers and backups

Sharktech was founded in 2003 and builds its business on cloud hosting, dedicated servers, and colocation, with five data centers across North America and Europe and a network architected around DDoS protection rather than bolting it on afterward. Its backup product wraps Acronis Cyber Protect into a hosted service: you get the genuine Acronis platform, managed through the Acronis web console, running independently of any server control panel.

For Exchange Online specifically, the capability comes from the Acronis platform itself. Per Acronis's official documentation, Microsoft 365 backup covers:

- Exchange Online **user mailboxes and shared mailboxes** (including mailboxes of users on Kiosk plans and mailboxes on litigation hold)
- Group mailboxes, archive mailboxes, and public folders
- Individual items: emails, attachments, contacts, tasks, and calendar entries
- The same platform also protects OneDrive, SharePoint, and Teams

How it works in practice: Acronis's Microsoft 365 agent must be installed on an internet-connected Windows machine, which connects to your tenant and runs the backups, storing data in the Acronis cloud storage behind Sharktech's service. Day-to-day operations happen in the Acronis console — registering systems, applying protection plans, setting backup schedules and retention, and checking failed jobs and storage consumption.

The published pricing covers every tier currently listed — this is a storage-based product, with four billing cycles sharing the same 200GB base capacity:

| Plan | Price | Billing cycle | Included storage | Overage rate | Buy |
| --- | --- | --- | --- | --- | --- |
| Monthly | $4.00/mo | Monthly | 200 GB | $0.02/GB | [Configure the monthly plan](https://bit.ly/SharKtech) |
| Quarterly | $8.00/quarter | Quarterly | 200 GB | $0.04/GB | [Configure the quarterly plan](https://bit.ly/SharKtech) |
| Semi-Annual | $12.00/6 mo | Semi-annually | 200 GB | $0.06/GB | [Configure the semi-annual plan](https://bit.ly/SharKtech) |
| Annual | $24.00/yr | Annually | 200 GB | $0.12/GB | [Configure the annual plan](https://bit.ly/SharKtech) |

Sharktech's official wording is "Services start at $4/month," with the final price depending on the capacity and service options you select at checkout — the cart shows an itemized total before you confirm. There's also an optional File Sync & Share add-on (starting at an additional $0.03/GB/month on top of backup pricing) that turns your backup target into a shareable cloud drive. Most dedicated-server users won't need it; only tick it if you actually do.

## Choosing a billing cycle: base price vs. overage rate

Here's the single most useful thing to know about this pricing structure, and something most reseller articles never spell out: **the longer the billing cycle, the cheaper the base price — but the higher the per-GB overage beyond 200GB.** Monthly overage runs $0.02/GB; annual overage runs $0.12/GB. That's a 6x spread.

At exactly 200GB, the annualized cost across cycles is straightforward: monthly billing costs $48 a year, quarterly costs $32, and both semi-annual and annual come to $24. If your backup footprint stays near the base capacity, annual billing effectively halves your cost.

Once your backup footprint clearly exceeds 200GB, though, the overage rate becomes the dominant variable. Every extra GB bills at $0.02/GB on monthly or $0.12/GB on annual, and that gap widens as your data grows. Sharktech's pages don't publish the finer details of how overage accrues per cycle, so the reliable approach is: estimate your real backup volume first (every protected machine plus mailbox data, multiplied by whatever retention policy creates in copies), then 👉 configure the annual Acronis plan and check the live total, and compare it against the monthly total in the same session. The cart displays the complete itemized price, and this step costs nothing.

Another way to reduce the guesswork: start on **monthly**. The monthly rate structure is the friendliest to growth, so run it for a month or two, see your actual storage consumption, and only then commit to a longer cycle.

## Limitations to know before you commit

Acronis's Exchange Online backup has several details that live only in official documentation but materially affect deployment:

1. **Some system folders are never backed up.** Mailbox folders like Deletions, Versions, Purges, Audits, DiscoveryHold, and Calendar Logging (and their subfolders) are excluded from mailbox backups. This rarely affects business data recovery, but if you have compliance or audit expectations, don't assume those folders exist in your backups.
2. **Recovery to a new mailbox requires a manual step.** Acronis can't restore data directly into a brand-new Microsoft 365 mailbox — you must first create the new user manually in Microsoft 365, then recover items into it. Factor that into any disaster recovery drill.
3. **The agent needs an internet-connected Windows machine.** The Microsoft 365 backup agent doesn't run on Linux or macOS, so plan for a Windows host somewhere in your deployment.
4. **Restore time depends on data volume.** Sharktech states explicitly that recovery time varies with data size and the restore method chosen, and recommends making recovery testing part of your regular operations — not something you try for the first time during an actual incident.
5. **No published money-back guarantee.** Sharktech's product pages don't advertise a refund policy, and third-party feedback has flagged this as well. The silver lining: the monthly tier is $4, so the cost of finding out it doesn't fit is trivially low — validate on monthly billing before locking a longer cycle.

Points 1 and 2 rarely appear in articles about Acronis resellers, but they directly determine whether your recovery runbook works the way you expect.

## Who this fits — and who it doesn't

Honestly, this plan has sharp edges, and pretending otherwise wouldn't help anyone.

**A good fit if:**

- You already rent (or are about to rent) a Sharktech dedicated server or VPS. Your servers and backup target sit on the same provider's network, and when something breaks you're dealing with one support team — available 24/7/365 with human engineers.
- Compliance or client contracts require "Acronis Cyber Protect" to appear on the invoice. You're getting the real Acronis platform — native console, native recovery workflows.
- You want a cheap, self-service cloud backup target where you control retention and schedules. The $4/month entry point is aimed squarely at small-workload operators.
- Your budget sits somewhere between "tape drive" and "enterprise Veeam deployment," but you still want ransomware scanning on the restore side.

**A poor fit if:**

- You only protect Microsoft 365 data and own no servers. Standing up an Acronis agent and managing a Windows machine just for mailbox backup costs more in effort than it saves — Microsoft's native backup or a pure-M365 tool like ManageEngine's is the smoother path there.
- You want a fully managed, hands-off service. Sharktech positions this as a self-service add-on; the technical team is reachable around the clock, but day-to-day backup policy management is on you.
- You need more than 2 years of retention without any configuration work. Microsoft's native option tops out at 2 years and works out of the box; Acronis retention is flexible but only as good as the policy you set up yourself.

## FAQ

**Doesn't Microsoft already back up Exchange Online?**
Microsoft's built-in mechanisms are infrastructure redundancy and limited data retention, designed for failures on Microsoft's side. Admin or user deletion, ransomware encryption, and similar scenarios need an independent backup product — which is exactly why Microsoft now sells Microsoft 365 Backup itself.

**How fast is Microsoft 365 Backup's restore?**
Microsoft claims up to 1–3 TB per hour for up to 1,000 average-sized mailboxes or sites, with a restore point every 10 minutes for Exchange across the previous 52 weeks. Restore speed is its main advantage over most third-party options.

**Can Acronis back up shared mailboxes and mailboxes on litigation hold?**
Yes. Acronis's official documentation explicitly covers Exchange Online user and shared mailboxes, including Kiosk-plan users and litigation hold, plus group mailboxes, archive mailboxes, and public folders.

**How is Sharktech's plan different from buying Acronis directly?**
Buying directly from Acronis typically means per-workload licensing with storage billed separately. Sharktech's plan bills by storage — 200GB to start, with no separate charge for the number of machines. If you have many workloads with modest data each, storage-based billing is usually the easier one to budget.

## Before you click buy

Three sentences cover the decision. Only protecting Microsoft 365, want zero setup and the fastest restores → go with Microsoft's native option. Protecting servers and mailboxes together, watching the budget, comfortable managing your own policies → Sharktech's Acronis plan, starting at $4/month to validate. Backup volume stable around 200GB → lock in annual billing once you've confirmed, since $24/year is the lowest total cost on the board. 👉 Open Sharktech's Acronis backup configurator, enter your real capacity, and check the total before picking a billing cycle — it costs nothing, and it prevents about 90% of the bill surprises down the line.
