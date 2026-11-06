---
name: publish-course
description: Price and publish (or unpublish) one course in an Ourdemy academy through the Ourdemy academy connector, after checking that the academy can take payments. Use when an academy owner wants to set or change a course's price, make a course free, open a course to learners, or asks whether a course is ready to go live. Also triggers on コースを公開 / 価格を設定 / 料金を決めたい / 無料で公開 / コースを販売したい.
---

# Price and publish a course

The person is an academy owner, not a developer. They want one course to go
live, at a price they choose. Each step that changes what learners see or
pay needs their yes first.

The connector's own instructions describe the tools and their rules. Follow
them. This skill is about how to talk to the owner.

## 1. Find out who and where you are

Call `whoami` and `get_setup_status` first. Write in the academy's language
(Japanese unless `whoami` says otherwise), in plain words: 価格, 無料, 公開,
受講生, 決済. Never say MCP, API, tool or ID.

If more than one course could be meant, call `list_courses` and ask which
one, by title.

## 2. Check what is there now

Call `get_course_pricing` and, if the person is an admin, `get_payment_status`.
A teacher can read pricing but not payment status; say that the owner or an
admin can check payments.

- Tell the owner the course's current price and whether it is published.
- If `get_payment_status` shows no payment method connected (Stripe or
  PayPay), say so plainly **before** talking about a paid price: learners
  cannot pay for a paid course until one is connected, and connecting one is
  done in the admin. Relay any warning it returns, in plain words, with the
  admin link from `get_setup_status`. A free course does not need one.

## 3. Agree the price

A course can be free, have a one-time price, and/or be included in a
membership plan the academy already has (`get_course_pricing` lists them).
New membership plans, coupons and campaigns are made in the admin.

Ask what they want to charge if they have not said. Help them decide if
they ask: what similar lessons cost in their business today is a good
starting point. Do not push a price.

Before calling `set_course_price`, repeat the exact price and type
(free, one-time, or which membership plan; in the academy's currency, a
whole number of yen for JPY) and ask,
for example 「このコースを 9,800円(買い切り)に設定してよろしいですか?」.
Call it only after a clear yes. Then say what was saved, and relay any
warning it returns in plain words, for example that the academy cannot
take payments yet, or that removing a course from a membership plan means
its members lose access to it.

## 4. Publish

Before calling `publish_course`, check with the owner:

- the course title and price as they are now;
- that once published, learners can see it on the academy site
  (and buy it, if payments are connected);
- any lesson still missing its video or PDF, if `get_course` shows it. Do
  not open every lesson one by one just to check.

Ask, for example 「このコースを公開して、受講生が見られる状態にしてよろしいですか?」,
and call `publish_course` only after a clear yes. One yes for the price does
not cover publishing, and the other way round.

A priced course can be published even when no payment method is
connected, but learners then cannot buy it. Say this **before** asking, and
offer to wait until they have connected Stripe or PayPay.

Relay every warning `publish_course` returns, with its admin link (支払い方法).
Afterwards, give them the link to see the course.

To take a course down again, use `unpublish_course`, with the same clear
yes first: learners stop seeing it.

## 5. Hand over what only the admin can do

Connecting Stripe or PayPay, changing the plan, custom domains and uploading
videos or PDFs are done in the admin. Give the link from
`get_setup_status`. A site page change is only a draft until they publish it
from the editor link.

## When something is refused

Explain it in plain words. Do not retry, and do not work around it.

- **Plan limit**: the plan does not allow this (for example, paid courses or
  more published courses); the plan is changed in the admin.
- **Teacher role**: if a call is refused because of the person's role, say
  that the owner or an admin can do it. Do not assume a refusal before
  trying; the server decides what a teacher may do.
- **Payment status for a teacher**: only an admin can see payment methods.
- **Price not accepted**: a price must be above 0, a whole number for yen,
  and at most 10,000,000. Ask for a corrected price.
- **IP-restricted admin**: the academy only allows admin access from
  certain IP addresses, so it cannot connect to Claude.
- **Deactivated academy**: the academy is switched off.
- **Every call fails with a server or connection error**: do not keep
  retrying; try once more at most. Likely causes are an IP restriction
  that was turned on after connecting (Settings → Security), a deactivated
  academy, or a removed connection. Say so plainly, and suggest checking
  Settings → Security and Settings → Claude 連携 in the admin, then
  reconnecting the Ourdemy connector.
- **Expired sign-in**: reconnect the Ourdemy connector and sign in again.

If you are not sure whether a step went through, call `get_course_pricing`
and say what is there now.
