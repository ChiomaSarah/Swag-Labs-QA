# 🧪 Swag Labs – QA Testing Project

> A comprehensive QA testing project on [Swag Labs](https://www.saucedemo.com) — a purpose-built e-commerce demo application by Sauce Labs. This project covers end-to-end QA methodology: requirements analysis, test planning, test case design, manual execution, defect reporting, and automated E2E testing in both Cypress and Playwright.

---

## Project Overview

| Field | Details |
|---|---|
| **Application** | Swag Labs – saucedemo.com |
| **Application Type** | Web-Based E-Commerce Demo |
| **Testing Types** | Manual QA · Cypress Automation · Playwright Automation |
| **Programme** | The Bug Detective – Software Testing For Beginners (STFB) · Accelerated Programme |
| **Test Cases** | 49 across 8 modules |
| **Defects Found** | 14 (3 Critical · 5 High · 4 Medium · 2 Low) |
| **Pass Rate** | 78% (38 passed · 11 failed) |
| **User Accounts Tested** | 5 |
| **Tester** | Osuji Chioma Sarah |

---

## Repository Structure

```
swag-labs-qa/
│
├── docs/
│   ├── Swag_Labs_Test_Plan.docx
│   ├── Swag_Labs_QA_Project_Workbook.xlsx
│   └── Swag_Labs_Project_Presentation.pptx
│
├── screenshots/
│   ├── defect-report.png
│   └── test-cases.png
│
└── README.md
```

---

## Documentation Deliverables

### 1. Test Plan (`Swag_Labs_Test_Plan.docx`)
A professional test plan document structured across three parts:
- **Cover Page** — project identity, tester, role, testing types, and portfolio link
- **Executive Summary & Metrics Dashboard** — headline results, key facts, metric boxes (49 TCs · 38 passed · 11 failed · 78% pass rate · 14 defects), severity breakdown, and pass rate by module
- **Full QA Test Plan** — objectives, skills demonstrated, test scope, 8 testing types, 6 techniques, execution order, test environment, automation approach (Cypress + Playwright), browser coverage table, custom commands, non-automatable test cases, exit criteria, defect summary, and risk register

### 2. QA Project Workbook (`Swag_Labs_QA_Project_Workbook.xlsx`)
A 6-tab Excel workbook:

| Tab | Contents |
|---|---|
| **Test Cases** | 49 test cases with ID, module, scenario, user account, preconditions, steps, test data, expected result, actual result, result (Pass/Fail/Blocked), and Bug ID |
| **Defect Report** | 14 defects with ID, affected account, module, title, steps to reproduce, expected vs actual result, severity, priority, and colour-coded status |
| **Test Summary Report** | Execution results by module, defect summary by severity, top 3 critical issues, and overall assessment |
| **Feature Inventory** | All application features documented with expected behaviour and test steps |
| **Business Rules** | 15 business rules governing application behaviour |
| **User Flow Summary** | 8 end-to-end user flows with preconditions, steps, alternate paths, and pass/fail criteria |

### 3. Presentation (`Swag_Labs_Project_Presentation.pptx`)
10 slides covering the full project — application overview, test plan summary, test case breakdown, execution results, defect log, top 3 critical issues, and test summary.

---

## Automation Repos

| Tool | Repo | Browser Coverage |
|---|---|---|
| **Cypress** | [swag-labs-cypress](https://github.com/ChiomaSarah/swag-labs-automation-cypress) | Chrome · Firefox · Edge |
| **Playwright** | [swag-labs-playwright](https://github.com/ChiomaSarah/swag-labs-automation-playwright) | Chromium · Firefox · WebKit |

All 49 test cases were automated in both tools. 4 test cases were marked `test.skip` with documented rationale where automation was not feasible (TC-020C, TC-041, TC-043, TC-044).

---

## Test Coverage

| Module | Test Cases | Pass | Fail | Pass Rate |
|---|---|---|---|---|
| Login | 8 | 8 | 0 | 100% |
| Logout | 2 | 2 | 0 | 100% |
| Product Listing | 14 | 8 | 6 | 57% |
| Cart | 9 | 7 | 2 | 78% |
| Checkout | 11 | 9 | 2 | 82% |
| Navigation | 3 | 2 | 1 | 67% |
| Session | 1 | 1 | 0 | 100% |
| Performance | 1 | 1 | 0 | 100% |
| **TOTAL** | **49** | **38** | **11** | **78%** |

---

## 👤 User Accounts Tested

| Account | Password | Behaviour |
|---|---|---|
| `standard_user` | `secret_sauce` | Normal — all features work as expected. Used as the baseline for cross-account comparison |
| `locked_out_user` | `secret_sauce` | Blocked at login — lock-out error displayed |
| `problem_user` | `secret_sauce` | **3 Critical + 2 High defects** — wrong images on all cards, sort opens but does not sort, Last Name overwrites First Name in checkout, cart limited to 3 items |
| `error_user` | `secret_sauce` | **3 High defects** — sort triggers browser alert, Last Name field unresponsive, cart limited to 3 items |
| `visual_user` | `secret_sauce` | **2 Medium defects** — sort order non-deterministic, layout breaks on smaller screens |
| `performance_glitch_user` | `secret_sauce` | Intentional 3–5s delay on all actions — used for performance comparison |

---

## Defect Summary

| Severity | Count | Key Findings |
|---|---|---|
| 🔴 Critical | 3 | Wrong images on all 6 product cards · Sort dropdown opens but does not sort · Last Name input overwrites First Name in checkout — all `problem_user` |
| 🟠 High | 5 | Cart limited to 3 items on `problem_user` and `error_user` · Sort triggers browser alert on `error_user` · Last Name field unresponsive on `error_user` · Sort order non-deterministic on `visual_user` |
| 🟡 Medium | 4 | Layout breaks on small screens (UI/UX) · Sort dropdown incomplete hit area — UI/UX · Session expiry error message uses raw URL path · Reset App State resets badge but Remove buttons don't revert until page reload |
| 🟢 Low | 2 | No confirmation after Reset App State · No order reference number on confirmation screen |

### 🔴 Top 3 Critical Issues

**BUG-001 — Wrong image on all 6 product cards (`problem_user`)**
All product cards display the same unrelated photo — a dog with a ball — regardless of the product name. Product names and prices are correct; only images are wrong.
Root cause: Image-product mapping not applied for `problem_user`

**BUG-002 — Sort dropdown opens but does not sort (`problem_user`)**
The sort dropdown opens and accepts a selection, but the product order does not change. Sort has no effect for this account.
Root cause: Sort dropdown opens and accepts selection but the sort function does not execute

**BUG-003 — Last Name input overwrites First Name in checkout (`problem_user`)**
Typing in the Last Name field replaces the First Name value. Last Name stays empty. Checkout cannot proceed past Step 1.
Root cause: Classic input binding bug — both fields share the same state variable

---

## 🔍 Notable Exploratory Findings

**Sort dropdown incomplete hit area (all users)**
The sort button shows a pointer cursor across its full visible area, but click events only register on the filter icon or text label — not the button background. Discovered during unscripted exploratory testing.

**`error_user` sort alert**
`error_user` is the only account that explicitly surfaces its sort defect via a browser alert: *"Sorting is broken! This error has been reported to Backtrace."* Unlike `problem_user` where sorting silently fails, `error_user` actively notifies the user — effectively a debug message left visible in production.

---

## Skills Demonstrated

- **Requirements Analysis** — documented features, user flows, business rules, and scope from scratch
- **Test Planning** — scope definition, approach, entry/exit criteria, risk assessment, and execution order
- **Test Case Design** — 49 structured test cases with preconditions, steps, test data, expected and actual results
- **Exploratory Testing** — unscripted testing across all 5 user accounts to surface intentional defects
- **Defect Reporting** — 14 defects with severity, priority, reproduction steps, and fix recommendations
- **Cross-Account Testing** — systematic comparison across all user types to isolate account-specific defects
- **Test Automation (Cypress)** — all 49 test cases automated in Cypress across Chrome, Firefox, and Edge
- **Test Automation (Playwright)** — all 49 test cases automated in Playwright across Chromium, Firefox, and WebKit
- **Automation Judgement** — 4 test cases identified as non-automatable and documented with `test.skip` and clear rationale
- **Documentation** — full QA documentation suite: RAD, Test Plan, Test Cases, Defect Report, Test Summary

---

## How to View

1. Clone or download this repository
2. Open `docs/Swag_Labs_QA_Project_Workbook.xlsx` — start with the **Test Cases** tab, then **Defect Report**, then **Test Summary Report**
3. Open `docs/Swag_Labs_Test_Plan.docx` for the full test plan including the automation section
4. Open `docs/Swag_Labs_Project_Presentation.pptx` for the slide deck
5. See the automation repos above for the Cypress and Playwright test suites

To explore the application yourself: visit [https://www.saucedemo.com](https://www.saucedemo.com) and log in with any of the test credentials above.

---

## 👩‍💻 About

**Osuji Chioma Sarah** — Full-Stack Software Engineer & QA Tester

Understanding how software is built makes you a sharper tester. This project demonstrates that quality assurance is not separate from engineering — it is part of it.

---

*Application under test: [Swag Labs](https://www.saucedemo.com) by Sauce Labs — a demo e-commerce application intentionally built with defects for QA training purposes. All defects documented here are intentional features of the application.*
