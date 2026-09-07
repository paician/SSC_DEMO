# R3-UX-P01 Locale Scope Reduction Result

## Result

```text
COMPLETE / READY FOR HUMAN REVIEW
```

## Product Decision

FIN-SSC Static UX Prototype 的 supported locales 由 `zh-TW`／`zh-CN`／`en-US` 縮減為 `zh-CN`／`en-US`。`zh-TW` 不再是 supported output locale。

## Changed Files

- `app.js`
- `app.bundle.js`（由 build tool 重新產生）
- `data/i18n.js`
- `index.html`
- `tools/validate-r3-sux-01.mjs`
- `tools/validate-r3-sux-02.mjs`
- `docs/context/R3_STATIC_UX_CONTEXT.md`
- `docs/results/R3_UX_P01_RESULT.md`

## Locale Contract

```text
Supported locales: zh-CN / en-US
Visible options:   简体中文 / English
HTML lang:         zh-Hans-CN / en-US
Priority:          URL lang > localStorage.portal_lang > browser / WebView language > zh-CN
Fallback:          zh-CN
```

- `ZH_TW` user-facing dictionary 已移除。
- `ZH_CN` 與 `EN` 均為完整且具有相同 key set 的 supported dictionaries。
- Locale switcher 仍只更新 `lang`，既有 query state preservation contract 保持不變。

## Legacy Compatibility

以下 legacy input 均 normalize 至 `zh-CN`，不會輸出 `zh-TW`：

```text
zh-TW
zh-Hant
zh-Hant-TW
```

相容範圍包含 URL `lang`、`localStorage.portal_lang` 與 browser／WebView language。

## Validation

| Command | Result |
| --- | --- |
| `node --check app.js` | PASS |
| `node --check data/i18n.js` | PASS |
| `node --check tools/validate-r3-sux-01.mjs` | PASS |
| `node --check tools/validate-r3-sux-02.mjs` | PASS |
| `node tools/build-bundle.mjs` | PASS |
| `node tools/validate-workbench.mjs` | PASS |
| `node tools/validate-r3-sux-01.mjs` | PASS |
| `node tools/validate-r3-sux-02.mjs` | PASS |
| `git diff --check` | PASS |

## Manual Visual Validation

```text
NOT EXECUTED
```

Human Review 尚需確認 `zh-CN`、`en-US` 與 legacy `zh-TW` URL normalization，以及 Workspace、Admin Console、View-As、Sidebar、Locale selector、Mobile／H5、英文長字串與 query state preservation。

## Known Gaps

- 尚未執行 browser／Human UX visual validation。

## Architecture Boundary

```text
RBAC Semantics Modified          NO
View-As Semantics Modified       NO
Adapter Contract Modified        NO
Workbench Semantics Modified     NO
Resource Access Matrix Modified  NO
Runtime Warning Architecture     PRESERVED
Production API Added             NO
Production Schema Added          NO
Production Integration Added     NO
Canonical Architecture Modified  NO
R3-SUX-03 Started                NO
```

## Git State

```text
Branch:       feat/r3-ux-p01-locale-reduction
Baseline:     aa4f2d508df484b8bba58416c77a3d1760daac75
Working Tree: R3-UX-P01 implementation、Context 與 Result 尚未 commit
Commit:       NONE
Push:         NONE
```

## Gate

```text
R3-UX-P01 Implementation       COMPLETE
Automated Validation           PASS
Human UX Review                PENDING
R3-UX-P01 Gate                 READY FOR REVIEW
R3-SUX-03                      NOT AUTHORIZED
Production Implementation      BLOCKED
```
