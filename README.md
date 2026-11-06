# Ourdemy Claude plugin

[日本語](#日本語) | [English](#english)

## 日本語

Ourdemy のアカデミーオーナー向けの Claude プラグインです。Ourdemy のアカデミー
コネクタと、アカデミーの初期設定・コース編集・価格設定と公開を会話で進めるための
スキルをまとめています。URL をコピーしてコネクタを手動で追加する必要はありません。

使い方・インストール方法・できないことは
[plugins/ourdemy/README.md](plugins/ourdemy/README.md) をご覧ください。

```
/plugin marketplace add ourdemy/claude-plugin
/plugin install ourdemy@ourdemy
```

## English

A Claude plugin for Ourdemy academy owners. It bundles the Ourdemy academy
connector with skills that walk you through setting up your academy,
editing a course, and pricing and publishing it, so you do not have to copy
a connector URL and add it by hand.

See [plugins/ourdemy/README.md](plugins/ourdemy/README.md) for what it does,
how to install and connect it, and what it cannot do.

## Layout

```
.claude-plugin/marketplace.json   marketplace listing the one plugin
plugins/ourdemy/
  .claude-plugin/plugin.json      plugin manifest
  .mcp.json                       the academy connector (production URL, no secrets)
  skills/                         setup-academy, edit-course, publish-course
```

`.mcp.json` is shipped to every installer. Never put a token or secret in it.
