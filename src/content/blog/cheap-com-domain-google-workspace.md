---
title: 'A .com for about $1 a year? How the Google Workspace route works'
description: 'A summary of a video tutorial on registering a .com for about $1 a year (75 Turkish lira) through Google Workspace, moving it to Cloudflare, and keeping only the domain.'
pubDate: 'Nov 17 2026'
---

A .com domain usually costs around $10 to $21 a year to renew, depending on the registrar. This video shows a very different number: about **$1 a year**.

The video is [每年仅需11元！通过 Google 官方渠道低价注册 .com 域名全教程 | 可托管至Cloudflare](https://youtu.be/wWqbL-CnHFg) — "Only 11 yuan a year! A full tutorial on registering a .com at a low price through Google's official channel, hostable on Cloudflare" — by SEVEN. It is in Chinese, with this timeline:

- 00:00 Opening
- 00:23 Buying a domain through Google Workspace
- 05:37 Verifying the domain and its Squarespace connection
- 06:59 Workspace Business Standard: keep it or not?
- 08:38 Managing DNS records and hosting on Cloudflare
- 12:02 Cancelling the Workspace subscription

This post is a summary of what the video teaches, not a word-for-word transcript. Prices and rules change, so check the checkout page before you pay anything.

## The headline number

The price in the video is **75 Turkish lira a year for a .com**, roughly $1 to $2 at recent exchange rates — usually quoted as about 11 yuan, or about $1.

For comparison, the video and its companion guide put the usual renewal prices roughly like this, in dollars converted from the yuan prices they give, at about 7 yuan to $1:

| Registrar | Renewal, roughly |
| --- | --- |
| GoDaddy | About $21 a year, after a cheap first year |
| Namecheap | About $17 a year |
| Cloudflare Registrar | About $11 a year |
| Google Workspace, Turkey pricing | About 75 lira, about $1 a year |

The saving is not a cheaper first year. It is the renewal price staying low, year after year, if the regional pricing still applies.

## Why it is that cheap

The trick is regional pricing, not a loophole in the usual sense. Google Workspace lets you buy a domain during signup, and the price depends on the region you choose. Choose Turkey, pay in Turkish lira, and some suffixes, including .com, show up at about 75 lira a year.

Two things make the flow more complicated than a normal domain purchase:

1. **Google no longer runs the registrar itself.** Google sold its domain registration business to Squarespace. After you buy, the domain is managed in Squarespace, not in a pure Google interface. Email verification, DNS, and nameserver changes all happen there.
2. **The domain and the Workspace subscription are two separate charges.** The domain is charged on the day you buy it. The Workspace subscription, on a Flexible plan, is billed by the days you use it, at the end of the billing cycle. Cancelling one does not automatically cancel the other.

## What you need before you start

- A credit card that can pay internationally, Visa or Mastercard. The guide recommends a physical card over a virtual card, which is more likely to trigger a risk check.
- A Turkey address to enter during signup. The guide suggests using an address generator for a correctly formatted address.
- An email address to receive the verification mail.
- Patience for jumping between Workspace and Squarespace. The whole flow runs through both.

## The steps, in order

### 1. Buy the domain in Google Workspace

Go to workspace.google.com and start the free trial. Create a new account for this domain, fill in the company information, and **choose Turkey as the region**. That region choice is what makes the price low.

Choose "Get a new custom domain", search for the name you want, and look for a .com priced in lira, usually 75 lira a year. If a name is taken, it will say so. Fill in the business information — WHOIS privacy is on by default — create a user like `name@yourdomain.com`, and keep that account password safe. You will need it again for Workspace and for Squarespace.

Then choose the plan. Workspace Business Standard comes with a 14-day free trial, and billing only starts after the trial. On the order summary, the Workspace charge should be 0 for now, and the domain charge should be 75 lira. Add your card and check out. You can skip adding extra users and the personalisation questions.

### 2. Verify the email in Squarespace

Squarespace, not Workspace, will send an activation email to the contact email you gave. Click **verify now** in that email, sign in with Continue with Google using the new `name@yourdomain.com` account, and finish the verification.

Squarespace asks for this within 15 days. Until it is done, the domain purchase is not really finished.

### 3. Do not cancel Workspace yet

This is the step the video stresses most. After buying, you will see two separate subscriptions: Workspace Business Standard, still in its trial, and the domain registration.

**Do not cancel Workspace before you have moved the domain to Cloudflare**, even if you only want the domain and have no use for Workspace. The reason is in the next step.

### 4. Move the domain to Cloudflare

In Cloudflare, add the domain and choose the free plan. Cloudflare will scan the existing DNS and give you two nameservers. Keep that page open.

In Squarespace, go to Domains, DNS, Domain Nameservers, and choose **Use Custom Nameservers**. This step asks you to sign in with Google again, using the new account you just created.

If you cancelled Workspace before this step, that sign-in is blocked with `accounts.google.com is blocked`, and you cannot change the nameservers. That is the trap.

If the sign-in works, paste in the two Cloudflare nameservers and save. If DNSSEC is on, changing nameservers will turn it off. That is expected at this point. Close the prompt about enabling DNSSEC for now.

Back in Cloudflare, confirm that you have updated the nameservers. Cloudflare says it can take 1 to 2 hours, but in practice it is often a few minutes. When Cloudflare says the domain is protected, hosting has worked.

### 5. DNSSEC, optional

DNSSEC stops DNS records from being tampered with. It is optional, and it has to be set up after the nameservers have actually moved to Cloudflare.

In Cloudflare, turn on DNSSEC for the domain and copy the DS record it generates: key tag, algorithm, digest type, and digest. In Squarespace, go to DNS, DNSSEC, Add Record, and enter those four values exactly as Cloudflare gave them.

### 6. Cancel Workspace, keep the domain

Only now, once Cloudflare hosting is working, cancel Workspace if you do not need it.

Go to admin.google.com, Billing, Subscriptions. You will see both the Workspace subscription and the domain registration. Open the Workspace subscription, go to More, and choose Cancel Subscription. Follow the prompts, give a reason, and use the new account as the admin email.

After cancelling, the subscription list should show only the domain registration. The domain stays yours, and renewal is charged at the same lira price, according to the reports in the video and guide.

The video also notes that this long-term behaviour after cancelling has not been fully proven over years. After cancelling, watch the site and DNS for a few days to confirm everything still resolves.

### If you cancelled too early

If you already cancelled Workspace and Squarespace now blocks the Google sign-in, the fix in the guide is to resubscribe to the cheapest Workspace plan, for example Business Starter, in admin.google.com under Billing, Subscriptions. Once the subscription is active again, the Squarespace verification should work, and you can change the nameservers as in step 4.

## Workspace Business Standard: keep it or not?

The video spends a section on this, at 06:59. Workspace Business Standard is a business suite: business email, Drive, Docs, and Gemini Pro. That is the reason to keep it, if you will actually use it.

The video also looks at its limits, including a smaller context window and usage-rate limits on Gemini Pro compared with what some people expect. The point is to decide on use, not on price alone. If you only want the domain, the subscription is an extra monthly cost you can cancel after the trial, as long as you cancel it in the right order.

## Before you pay: check these

- **The checkout currency must be lira.** If the checkout page shows dollars or another currency, the Turkey pricing has not applied. Stop, check the region and your setup, and do not pay.
- **The renewal price is not a Google guarantee.** Reports so far say renewal is also 75 lira, but this is regional pricing and exchange-rate arithmetic, not a promise. Google can change the rules, and the price could rise to normal levels. If it does, you can transfer the domain out.
- **You cannot usually renew for several years at once.** Reports say it is one year at a time.
- **Keep the new account safe.** The username and password you create during Workspace signup are used for Workspace, Squarespace, and the DNS change. Losing them makes the later steps much harder.
- **Watch the trial end date.** The 14-day Workspace trial is free, but the subscription starts charging after it if you have not cancelled it.

## Is it worth it?

If you want a .com for a personal site or a small project, and you are happy to follow a multi-step flow across Workspace, Squarespace, and Cloudflare, the saving is real: roughly $9 a year compared with a typical $10-plus renewal, every year the pricing holds.

If you want the simplest possible purchase, with one dashboard and no subscription to cancel, a registrar with transparent first-year and renewal pricing, such as Cloudflare Registrar, NameSilo, or Spaceship, is the easier choice, at a higher yearly price.

## Links

- Video: [每年仅需11元！通过 Google 官方渠道低价注册 .com 域名全教程 | 可托管至Cloudflare](https://youtu.be/wWqbL-CnHFg)
- Google Workspace: https://workspace.google.com
- Squarespace: https://squarespace.com
- Cloudflare: https://dash.cloudflare.com
- Companion guide with the same flow, in Chinese: [每年不到11元的.com域名——Google官方渠道购买，设置+托管到Cloudflare全教程](https://smallstep.one/turkey-google-workspace-cheap-domain/)
