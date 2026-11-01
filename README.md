# office 365 email backup：what Microsoft's native tools miss, how automated backup actually works, and what a plan really costs

If you're searching for office 365 email backup, here's the short answer: Microsoft 365 has no built-in mailbox backup. Microsoft keeps the service running and replicates your data across datacenters, but under its shared responsibility model, protecting the data itself — against deletion, ransomware, or plain user error — is your job. That's why every serious guide on this topic, from university IT knowledge bases to backup vendors, lands on the same conclusion: native retention features are not a backup, and you need either manual exports or a third-party backup service.

This guide walks through what Microsoft's tools actually do, where they fall short, what a proper third-party backup costs, and how to pick between them. The pricing below comes from Sharktech's Acronis-powered backup service, which uses a per-capacity model starting at **$4/month** — a different structure from most per-seat tools, and worth understanding before you commit either way.

> **Quick pick:** Most small teams wanting set-and-forget mailbox backup should look at an automated cloud-to-cloud tool. Sharktech's Acronis Cyber Protection plans start at **$4/month for 200 GB** with monthly, quarterly, semi-annual, and annual billing, and scale by capacity rather than per user — 👉 [check current Sharktech backup pricing and configure your capacity](https://bit.ly/SharKtech)

## Doesn't Microsoft 365 already back up my email?

No. Microsoft mirrors your data for service availability, but that replication is not a backup you can use. If an email is deleted, corrupted by malware, or wiped by a misconfigured retention policy, the damage syncs everywhere — there's no clean copy to roll back to. Acronis puts it bluntly in its own documentation: Microsoft ensures your data is available; the service isn't concerned with whether the data is still readable.

Several native features get mistaken for backup. They aren't:

- **Archive mailboxes (In-Place Archiving)** move old emails to a second folder. No copy is created, and archive mailboxes have a default storage limit of 100 GB. Both your primary and archive mailboxes face the same threats.
- **Retention policies and litigation hold** control how long content lives in place. A hold keeps deleted items recoverable for a set period, which helps with accidental deletion — but Microsoft's own guidance says eDiscovery and holds shouldn't be used for long-term retention. They're compliance tools, not disaster recovery.
- **OneDrive sync** is actively counterproductive here: delete a file locally or get infected by ransomware, and the deletion or infection syncs to the cloud and every connected device.

And when Microsoft's infrastructure itself has a bad day, you're exposed. In January 2023, a Microsoft 365 outage took Outlook and Teams down for nearly six hours. Anything without a copy outside Microsoft's environment was unreachable for that entire window.

Microsoft did launch its own **Microsoft 365 Backup**, generally available since mid-2024. It's better than nothing, but it stores backup copies inside Microsoft's own infrastructure — the same trust boundary your live data sits in. Its storage option carries fixed one-year retention, recovers whole mailboxes, accounts, or sites rather than single emails, and bills per GB consumed. A third-party comparison from Acronis highlights the gap: independent copies with flexible (even indefinite) retention and single-email granular recovery versus Microsoft's whole-item restores on a fixed clock.

## Your three realistic options

Every top-ranking guide covers some version of this, so here's the compressed version with the trade-offs made explicit.

**1. Manual export to PST files.** Outlook can export mail, calendars, and contacts to a .pst (Windows) or .olm (Mac) archive. University IT departments classify this as a temporary measure — something you do before losing account access, or once a quarter at most. With dozens of mailboxes there's no automation, no consistency, and a PST file is a single corruptible file sitting on one machine.

**2. Native retention and holds.** Free-ish (bundled with plans that include Purview features, which requires Business Premium or E3 and up — $22 and $33.75 per user per month respectively at the time of NAKIVO's 2024 guide). Works for compliance, fails for recovery: no point-in-time snapshots, no copies outside Microsoft.

**3. Third-party automated backup.** Cloud-to-cloud tools that snapshot mailboxes on a schedule to storage outside Microsoft. This is the category where Sharktech's Acronis service sits, along with vendors like NAKIVO and MSP360. Typical coverage includes Exchange Online mailboxes (user, shared, group, public folders), OneDrive, SharePoint, and Teams, with single-email restore and flexible retention.

A few reference points from that third category, so you know the landscape: NAKIVO listed per-user pricing of $0.80/user/month at the time of its 2024 guide. MSP360 includes 1 TB of AWS-backed storage with a 30-day free trial and supports immutable backups. MailStore Server takes a different approach entirely, archiving mailboxes to local storage — relevant if compliance rules require an on-premises copy.

## Sharktech backup plans and pricing

Sharktech sells Acronis Cyber Protection as a hosted service with **capacity-based pricing** — you pay for storage volume, not seat count. Plans start at $4/month, and the final recurring price depends on the capacity and protection options you select at checkout.

A May 2023 post on Sharktech's blog laid out the tier structure that the service is built around:

| Billing cycle | Included storage | Price | Additional storage | Buy |
| --- | --- | --- | --- | --- |
| Monthly | 200 GB | $4/mo | +$0.02/GB | [ Configure a monthly backup plan](https://bit.ly/SharKtech) |
| Quarterly | 200 GB | $8/quarter | +$0.04/GB | [ Configure a quarterly plan](https://bit.ly/SharKtech) |
| Semi-annual | 200 GB | $12/half-year | +$0.06/GB | [ Configure a semi-annual plan](https://bit.ly/SharKtech) |
| Annual | 200 GB | $24/year | +$0.12/GB | [ Configure an annual plan](https://bit.ly/SharKtech) |

One honesty note before you anchor on those numbers: that tier breakdown comes from a 2023 blog post. Sharktech's current product page confirms plans still start at $4/month and that the final price is confirmed in the customer portal at checkout — so treat the table as the pricing structure, and the checkout page as the final word.

### What the per-GB model costs in practice

Here's the math most per-seat reviews skip. A 1 TB setup on the monthly plan works out to $4 for the included 200 GB, plus 824 extra GB at $0.02/GB — roughly **$20.50/month**.

Now compare that to the per-seat model: at NAKIVO's listed $0.80/user/month, 25 mailboxes cost about the same $20/month. Below roughly 25 mailboxes, per-seat pricing tends to be cheaper. Above it — especially if you're also backing up OneDrive and SharePoint data that eats storage under any model — capacity pricing starts winning. If you're a 6-person company, a per-seat tool will likely cost less. If you're a 40-person company or a team also protecting servers and VMs, Sharktech's model gets more attractive fast.

### What Acronis's Microsoft 365 backup covers

Sharktech's service runs on Acronis Cyber Protect, and Acronis's platform documentation details what its Microsoft 365 backup supports. Worth knowing before ordering, since exact workload availability depends on the options in your Sharktech plan:

- **Exchange Online**: user mailboxes, shared mailboxes (including Kiosk-plan and litigation-hold mailboxes), group mailboxes, and public folders
- **OneDrive** user files and folders, **SharePoint Online** sites and individual data items, and **Teams** — channels, team mailboxes, files, meetings, and team sites, with OneNote notebooks included
- Backup scheduling up to **6 times per day** (the cloud agent defaults to once daily), with flexible retention by date, backup count, or indefinite
- AES-256 encryption, granular restore of individual emails and files, and optional immutability windows on deleted backups as ransomware protection

Scale-wise, the cloud-agent route supports up to 50,000 protected workloads per company, and it can automatically include new users, groups, and sites when you apply a protection plan to "all users." Cross-organization restore within the same tenant is supported too.

> The one thing to verify before buying: Sharktech's product page describes the service around machines, applications, and cloud data generally, so confirm which Microsoft 365 workloads your chosen configuration includes in the customer portal. Acronis's platform clearly supports Exchange Online through Microsoft 365, but you want your specific plan to include it — not to discover otherwise after your first restore attempt. File Sync & Share and some protection add-ons are priced separately, and the checkout shows the itemized total before you confirm.

If that checks out and you want the capacity model, 👉 [open Sharktech's Acronis backup portal and configure your plan](https://bit.ly/SharKtech). Sharktech's technical team is available 24/7 if you'd rather have someone walk you through the workload selection.

## Setting it up: what to expect on day one

Setup is where cloud-agent backups differ most from the old agent-based world, and it's genuinely simpler:

1. Sign in to the backup console with an account holding the **global administrator** role in Microsoft 365. The cloud agent doesn't log in to Office 365 or store your credentials — Microsoft grants permissions directly, and you confirm once. Changing or even deleting that admin account afterward doesn't break your backups.
2. Apply a protection plan to your mailboxes first, then OneDrive accounts, then Teams, then SharePoint sites. Acronis recommends this order explicitly.
3. Wait out the first full backup. It can take several days depending on data volume, and each backup needs to finish before the next starts. Plan the initial run for a quiet week, not the night before an audit.

The local-agent route (installed on a Windows machine) exists if you want backups landing on local or network folders, but it only covers Exchange Online mailboxes, skips archive mailboxes, and caps out at 5,000 mailboxes per company when writing to cloud storage. For pure Microsoft 365 backup, the cloud agent is the better fit for most teams.

## The fine print worth knowing before an incident

This is the part most vendor blogs leave out, and it's pulled straight from Acronis's own documentation:

- **The Recoverable Items folder is never backed up.** Mailbox backups cover user-visible folders only — the Deletions, Versions, Purges, Audits, and DiscoveryHold subfolders are excluded. This rarely matters day to day, but if your compliance team expected those contents in backups, adjust expectations now.
- **Restores don't create missing objects.** If a SharePoint site was deleted, you must recreate the site first, then restore into it. Same for users, groups, and public folders.
- **Cloud-agent manual runs are capped at 10 per hour**, with up to 10 concurrent restore operations. Fine for normal use; worth knowing if you planned on ad-hoc backups as a workflow.
- **You can't restore to on-premises Exchange Server.** If a hybrid migration out of Microsoft 365 is in your roadmap, factor that in.

None of these are dealbreakers — they're just the kind of thing you want to learn from an article instead of during a recovery.

## Who Sharktech's plan fits — and who it doesn't

It fits if you want one console protecting mailboxes alongside servers, VMs, or workstations, since Acronis Cyber Protect handles both in the same interface. It fits if your mailbox count makes per-seat pricing annoying, or if you value predictable per-GB costs and 24/7 human support over self-serve SaaS.

It fits less well if you're a very small team — under ~10 mailboxes, a per-seat tool like NAKIVO's will likely cost less each month, and MSP360's 30-day trial lets you test the workflow before paying anything. And if your compliance regime demands an on-premises archive copy, a local-archiving tool like MailStore Server does that specific job; some teams even pair a local archive with a cloud backup rather than choosing one.

A few questions that come up repeatedly:

**Is Microsoft 365 Backup enough on its own?** It's the strongest native option, and if your budget is zero, enable it. But its copies live inside Microsoft's infrastructure with fixed one-year retention and whole-item recovery — so a serious Microsoft-side failure or an attacker with tenant access can reach your backup too.

**How often should mailboxes back up?** Acronis's cloud agent defaults to daily and allows up to 6 runs per day. Daily is enough for most businesses; the real protection comes from retention length and keeping copies outside Microsoft.

**What happens to emails deleted before backup was enabled?** Gone, unless they're still inside the retention window or Recoverable Items. Backup protects forward from the day it starts — another reason not to defer the first full backup.

## Before you click buy

Three things to line up: confirm your account has global admin (you'll need it for the one-time consent), estimate your total data across mailboxes plus OneDrive and SharePoint so the 200 GB starting point makes sense, and sanity-check the itemized price in the portal — extra capacity beyond 200 GB and any File Sync & Share add-ons are billed separately.

From there the decision is short: a handful of mailboxes with simple needs → a per-seat tool will likely be cheaper; growing teams, mixed workloads, or a preference for capacity pricing → Sharktech's $4/month entry point is an easy place to start, and 👉 [you can configure your backup capacity and see the exact price at Sharktech's portal](https://bit.ly/SharKtech) before anything is billed. Just don't leave the first full backup until after the first incident — that's the one mistake this whole guide can't fix afterward.
