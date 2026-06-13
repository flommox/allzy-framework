# User Login Example

## Purpose

This folder contains User Login Yin/Yang reference artifacts for one bounded email-and-password login module.

## Contents

Expected files:

- [`user_login_intent.md`](./user_login_intent.md)
- [`user_login_core_contract.md`](./user_login_core_contract.md)
- [`user_login_full.md`](./user_login_full.md)

## How to Use

Start with [`user_login_full.md`](./user_login_full.md) for the quickest single-file overview. Then compare it with [`user_login_intent.md`](./user_login_intent.md) and [`user_login_core_contract.md`](./user_login_core_contract.md) to see how the same module is separated into paired artifacts.

These files are reference artifacts, not canonical templates. Use [`../../templates/`](../../templates/) when creating new work.

## Canonical vs Supporting

| File | What it shows | Related template |
|---|---|---|
| [`user_login_intent.md`](./user_login_intent.md) | Filled Yin Page | [`../../templates/yin/yin-page/02_yin_template.md`](../../templates/yin/yin-page/02_yin_template.md) |
| [`user_login_core_contract.md`](./user_login_core_contract.md) | Filled Yang Core Module | [`../../templates/yang/yang-core-module/03_yang_template.md`](../../templates/yang/yang-core-module/03_yang_template.md) |
| [`user_login_full.md`](./user_login_full.md) | Filled combined Yin/Yang Document | [`../../templates/yin-yang/yin-yang-document/04_yin_yang_template.md`](../../templates/yin-yang/yin-yang-document/04_yin_yang_template.md) |

## Not Included / Do Not Confuse

- [`user_login_intent.md`](./user_login_intent.md) keeps only the Yin intent layer.
- [`user_login_core_contract.md`](./user_login_core_contract.md) keeps only the Yang execution contract.
- [`user_login_full.md`](./user_login_full.md) combines both in one file.
- This example does not include OAuth, SSO, MFA, password reset, UI code, database implementation, or compact artifact variants.
