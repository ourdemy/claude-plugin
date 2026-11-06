# Ourdemy for Claude

[日本語](#日本語) | [English](#english)

## 日本語

Ourdemy のアカデミーを、Claude との会話だけで準備できるプラグインです。
お店や教室のことを Claude に話したり、チラシ・ホームページ・レッスン一覧を
見せたりすると、Claude がアカデミーの名前やデザイン、最初のコースの下書きを
作ります。内容を確認して「お願いします」と言うまで、アカデミーには何も保存されません。

### できること

- **アカデミーの初期設定**: 事業についてのインタビュー、またはチラシなどの
  資料から、アカデミーのデザインとコースを下書きし、確認後に反映します。
  作られたコースは「無料・非公開」なので、受講生にはまだ見えません。今あるコースや設定が置き換えられたり削除されたりすることはありません。
- **コースの編集**: コース名や講義の文章の変更、講義やセクションの追加・並べ替え・削除。
  削除は元に戻せないため、必ず事前に確認します。Claude が削除せず、管理画面のリンクを案内する場合もあります。
- **価格設定と公開**: コースの価格を決めて公開します。価格の設定と公開は、
  それぞれ確認してから行います。

### インストール

**Claude(ブラウザ版・デスクトップ版)**
1. 「カスタマイズ」→「プラグイン」を開きます。
2. 「Ourdemy」を検索して追加します。

**Claude Code**
```
/plugin marketplace add ourdemy/claude-plugin
/plugin install ourdemy@ourdemy
```

### アカデミーとの接続

インストールしただけでは、まだアカデミーにはつながっていません。

1. Claude の「コネクタ」設定で **ourdemy-academy** の「接続」を押します
   (Claude Code では `/mcp` を開き、ourdemy-academy を選んでサインインします)。
2. Ourdemy の画面が開くので、アカデミーの管理者アカウントでログインします。
3. 確認画面にアカデミー名とあなたの名前が表示されます。正しければ「許可」を押します。
4. Claude に戻ったら、「アカデミーを作りたい」などと話しかけてください。

接続は Ourdemy 管理画面の「設定」→「Claude 連携」で確認・解除できます。
解除すると、次に Claude を使うときに再接続を求められます。

### できないこと(管理画面で行ってください)

次の操作は、安全のため Claude からはできません。Claude が管理画面のリンクを案内します。

- Stripe・PayPay の決済の接続
- プランの変更
- 独自ドメインの設定
- パソコンからのロゴ・画像のアップロード
- 動画ファイル・PDF のアップロード(YouTube などの動画リンクは Claude から追加できます)

サイトのページを Claude で変更した場合、エディタのリンクから「公開」するまでは下書きのままです。

### ご注意

- **IP アドレスで管理画面へのアクセスを制限しているアカデミー**は、Claude と接続できません。
- **講師アカウント**で接続した場合、講師の権限でできる操作だけが行えます。
- 利用中のプランの上限を超える操作(コース数など)はできません。
- **一度に接続できるアカデミーは1つです。** 複数のアカデミーをお持ちの場合は、使いたいアカデミーの管理画面にログインしてから、Claude のコネクタ設定で ourdemy-academy を「切断」→「接続」し直してください。確認画面に表示されるアカデミー名を必ずご確認ください。

---

## English

This plugin lets you set up your Ourdemy academy just by talking to Claude.
Tell Claude about your studio, school or coaching business, or show it a
flyer, your website or a lesson list, and it drafts your academy's name, look
and first course. Nothing is saved to your academy until you have seen the
draft and said yes.

### What it does

- **Set up your academy**: Claude interviews you, or reads the material you
  share, drafts your branding and courses, shows you a preview and applies it
  only after you approve. New courses are created free and unpublished, so
  learners do not see them yet. Nothing you already have is replaced or deleted.
- **Edit a course**: rename a course, rewrite a lesson, add, reorder or remove
  sections and lessons. Claude always asks before deleting, because a
  deletion cannot be undone, and may give you the admin link to delete it yourself.
- **Price and publish a course**: set a price and open the course to
  learners. Claude asks before each of the two steps.

### Install

**Claude (web and desktop)**
1. Open Customize → Plugins.
2. Search for "Ourdemy" and add it.

**Claude Code**
```
/plugin marketplace add ourdemy/claude-plugin
/plugin install ourdemy@ourdemy
```

### Connect your academy

Installing does not sign you in yet.

1. In Claude's connector settings, click **Connect** on **ourdemy-academy**
   (in Claude Code, open `/mcp`, pick ourdemy-academy and sign in).
2. The Ourdemy page opens. Sign in with your academy admin account.
3. The consent screen shows your academy and your name. If they are right,
   click Allow.
4. Back in Claude, say something like "I want to set up my academy".

You can see and revoke the connection in the Ourdemy admin under
Settings → Claude 連携. After revoking, Claude asks you to connect again.

### What it cannot do (use the admin)

For safety, these are not available from Claude. Claude gives you the admin
link instead.

- Connecting Stripe or PayPay for payments
- Changing your plan
- Custom domains
- Uploading a logo or images from your computer
- Uploading video files and PDFs (a link to a video you already host, such as YouTube, can be added from Claude)

A site page changed through Claude stays a draft until you publish it from
the editor link.

### Good to know

- An academy that **limits admin access by IP address** cannot connect to Claude.
- If you connect with a **teacher account**, you can do only what a teacher's role allows.
- Actions beyond your plan's limits (such as the number of courses) are refused.
- **One academy at a time.** If you run more than one academy, sign in to the admin of the one you want, then disconnect and connect ourdemy-academy again in Claude's connector settings. Check the academy name on the consent screen.

### プライバシー / Privacy

[Ourdemy for Claude プライバシーポリシー](https://ourdemy.com/privacy-policy-for-ourdemy-claude-plugin/)
