---
name: edit-course
description: Make one change to an existing course in an Ourdemy academy through the Ourdemy academy connector, such as renaming a course, rewriting a lesson, adding or reordering sections and lessons, or removing one. Use when an academy owner or teacher wants to edit, fix, update, add to or reorganise a course they already have. Also triggers on コースを編集 / 講義を追加 / 講義の内容を直して / セクションの順番を変えて / この講義を削除して.
---

# Edit a course

The person is an academy owner or teacher, not a developer. They want one
change to a course they already have. Make that change, show it, and leave
everything else as it was.

The connector's own instructions describe the tools and their rules. Follow
them. This skill is about how to talk to the person.

## 1. Find out who and where you are

Call `whoami` and `get_setup_status` before anything else, even when the
request already names a course. Write in the academy's language
(Japanese unless `whoami` says otherwise), in plain words: コース, セクション,
講義, 公開, 下書き. Never say MCP, API, tool, ID or slug.

## 2. Find the course and the exact spot

Call `list_courses`. If more than one course could be meant, ask which one,
using the course titles. Then `get_course`, and `get_lecture` for a lesson
whose text you will change.

Restate the change in one sentence before making it, for example
「『基礎編』セクションの3番目に『呼吸の練習』という講義を追加します」.
If the request is unclear (which lesson, where it goes), ask one short
question rather than guess.

## 3. Make the change

Use the matching `update_*`, `add_*` or `reorder_*` call. Keep the course's
existing tone and style in any text you write. Do not invent facts about the
academy or its teachers.

Changes the person asked for can be made straight away, because they can be
changed back. Afterwards, say what changed and show the new order or text
briefly.

If the course is already **published**, say that learners will see the
change, and mention it before saving if the change is large.

## 4. Deleting needs a clear yes

`delete_section` and `delete_lecture` cannot be undone. Before calling
either:

- say exactly what will be removed, by title, and for a section how many
  lessons are inside it;
- say that it cannot be undone;
- ask, and wait for a clear yes, for example
  「『応用編』セクション(講義5本)を削除します。元に戻せません。削除してよろしいですか?」.

One yes covers that one deletion only. Ask again for the next one.

If you will not delete it yourself, or the person prefers to, give them the
course's curriculum link in the admin and say nothing has been deleted.

## 5. Hand over what only the admin can do

Video files and PDFs are uploaded in the admin, not here. You can create
the lesson and its text, or link a video they already host; tell them to
add the file from the admin link in `get_setup_status`. Payments, the plan and custom domains also live in the
admin. A site page change is only a draft until they publish it from the
editor link.

To change a price or publish the course, use the `publish-course` skill.

## When something is refused

Explain it in plain words. Do not retry, and do not work around it.

- **Teacher role**: this change needs a different role, such as the owner.
- **Plan limit**: the current plan does not allow it; the plan is changed
  in the admin.
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

If you are not sure whether a change was saved, call `get_course` and say
what is there now.
