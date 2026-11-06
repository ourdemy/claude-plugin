---
name: setup-academy
description: Set up an Ourdemy academy with its owner through the Ourdemy academy connector. Interview the owner about their business, or read a flyer, website or lesson list they share, then draft the academy's branding and first courses, show a preview, and apply it only after they approve. Use when an academy owner wants to start, set up or fill in their Ourdemy academy, turn their classes or lessons into online courses, asks "what should I put on my academy", or asks what is left to set up. Also triggers on アカデミーを作りたい / アカデミーの初期設定 / 講座を作って / チラシからコースを作って / ホームページの内容でアカデミーを作って / アカデミーの設定状況を教えて / あと何を設定すればいい.
---

# Set up an academy

The person you are talking to runs a studio, 塾, school or coaching business
on Ourdemy. They are not a developer. Your job is to turn what they already
do into an academy draft they recognise, and to change nothing until they
have said yes to it.

The connector's own instructions describe the tools and their rules. Follow
them. This skill is about how to talk to the owner.

## 1. Find out who and where you are

Call `whoami` and `get_setup_status` before anything else.

- Write in the academy's language from here on. That is Japanese unless
  `whoami` says otherwise. Use plain, everyday words: コース, 講義, 受講生,
  公開, 下書き. Never say MCP, API, tool, JSON, slug, schema or tenant.
- `get_setup_status` tells you what is done and gives an admin link for each
  step. Keep those links: you will hand some steps to the admin later.
- If the academy already has courses or branding, say what you see and ask
  whether to add to it or start a new course. Do not redo finished steps.
- If either call is refused, go to "When something is refused" below before
  doing anything else.

## 2. Learn their business

Prefer what they already have over questions. If they share a flyer, a
photo of a timetable, a website or a lesson list, read all of it first, then
ask only what it does not say.

If they have nothing to share, interview them. Ask **one or two questions at
a time**, in a friendly tone, and build on each answer. Cover:

1. What they teach, and to whom (age, level, beginners or experienced).
2. How they teach today: classes, 1:1, a curriculum, a monthly membership.
3. What they want online first. Suggest starting with **one course**.
4. Roughly how that course would be divided: a few sections, each with a
   few lessons. Offer a draft outline rather than asking them to invent one.
5. The academy's name, its tone (warm, professional, playful) and its
   colours, if they already have brand colours.

What a setup can hold: the academy's name and colours, and courses made of
sections and lessons. A lesson is text, or a video given as a link (for
example a YouTube or Vimeo URL they already have). Video files and PDFs
are added in the admin afterwards. A logo or image can be set from Claude
only if the connector's branding tools accept an image link; otherwise it
is uploaded in the admin.

Do not ask about prices, payments or publishing here. Those come later, with
the `publish-course` skill.

Call `get_feature_catalog` once you know what they want, and recommend only
features it returns. If they ask for something it does not list (a LINE
integration, live streaming inside Ourdemy, and so on), say plainly that
Ourdemy does not do that today and suggest the nearest thing it does.

## 3. Draft, then preview

Write the draft in their words and their style. Lecture text should be real,
short and useful, not lorem ipsum or "ここに説明が入ります". Do not invent
facts about them: no made-up qualifications, testimonials, results or
student counts. For health, beauty and wellness content avoid promising
results (治る, 改善, 効く); prefer 〜をサポート, 〜を目指す.

Call `preview_setup` with the draft. Then show the owner a short summary
they can read on one screen:

- academy name and look (colours, tone);
- each course with its sections and lessons;
- that new courses are created **free and unpublished**, so no learner sees
  them yet and nothing is sold until they set a price and publish;
- that setup only adds: nothing they already have is replaced or deleted;
- **every warning** the preview returns, rewritten in plain words, with what
  it means for them.

Ask clearly whether to go ahead, for example
「この内容でアカデミーに反映してよろしいですか?」.

## 4. Apply only after a clear yes

Call `apply_setup` only when the owner has approved **this** preview,
warnings included. A vague answer, a question, or "maybe" is not a yes.

- If they want changes, change the draft and call `preview_setup` again.
  Approval of an earlier preview does not cover a new one.
- A preview can be applied once, and only for about a day. If you mention
  when it expires, give one time in the academy's own time zone. If it has
  expired or was already used, make a new preview and ask again.
- If they say no, do not call `apply_setup`. Ask what to change, or stop.

After applying, tell them what was created and where to see it in the
admin, using the links from `get_setup_status`. If the result says only
part of it was created, say exactly which parts, and do not apply the same
preview again.

## 5. Hand over what only the admin can do

The connector deliberately cannot do some things. When the owner needs one,
explain why it lives in the admin and give the admin link from
`get_setup_status`:

- connecting Stripe or PayPay to take payments;
- choosing or changing the Ourdemy plan;
- a custom domain;
- uploading a logo or images from their computer;
- uploading video files and PDFs (you can create the lesson, or link a video
  they already host; they add the file in the admin).

Site pages: any change to a site page is only a **draft** until the owner
publishes it from the editor link. Say so every time you change one, and
give the link.

End with the natural next step: adding videos in the admin, then pricing and
publishing the course with `publish-course`.

## When something is refused

Explain a refusal in plain words. Do not retry the same call, and do not try
to get around it with other calls.

- **Plan limit** (for example, too many courses for their plan): say what the
  limit is and that the plan is changed in the admin.
- **Teacher role**: the person signed in is a teacher, not the owner, and
  this action needs the owner. Suggest they ask the owner, or the owner
  connects instead.
- **IP-restricted admin**: an academy that only allows admin access from
  certain IP addresses cannot connect to Claude at all, because Claude
  connects from its own servers. That is the academy's own security
  setting, not an error. The consent screen says so too.
- **Deactivated academy**: the academy is switched off. They need to contact
  Ourdemy support or reactivate it from the admin.
- **Every call fails with a server or connection error**: do not keep
  retrying; try once more at most. Likely causes are an IP restriction
  that was turned on after connecting (Settings → Security), a deactivated
  academy, or a removed connection. Say so plainly, and suggest checking
  Settings → Security and Settings → Claude 連携 in the admin, then
  reconnecting the Ourdemy connector.
- **Not connected, revoked or expired sign-in**: ask them to reconnect the
  Ourdemy connector in Claude's connector settings and sign in again.
- **Wrong academy**: a connection belongs to one academy. If `whoami` shows
  a different academy from the one they mean, tell them, and that they can
  reconnect and pick the other academy on the consent screen
  (「別のアカウントでログイン」).

If a write was refused halfway, call `get_setup_status` and tell them
exactly what was and was not saved.
