# North Vacation Booking — Test Plan

**Assignment:** Learning Practice 7: Test Planning

**Version:** 1.0

**Status:** Proposed plan; test execution has not occurred.

**Test basis:** The supplied [assignment README](docs/assignment-readme.md). The starter contains requirements and instructions, but no application source code or executable build.

## 1. Test Context

This plan defines the scope, people, resources, and checks needed to evaluate the North Vacation Booking release before release approval.

### Test objectives

1. Verify that a user can select a rental, enter valid dates and a valid guest count, create a booking, and view a booking whose details match the submitted values. All high-priority tests for this flow must pass.
2. Verify that applicable increase, decrease, and reset controls behave according to approved rules, and that invalid booking inputs are rejected without creating a booking. All high-priority validation and control-boundary tests must pass.

| Context | Definition |
| --- | --- |
| In scope | Rental selection; check-in and checkout fields; guest input; booking creation; the booking list; increase, decrease, and reset behavior wherever those controls exist; integration among these features; basic usability and accessibility checks. |
| Out of scope | Payment processing, cancellations, refunds, rental administration, and changes to authentication. These features are not specified in the supplied product description. Formal security, load, and full accessibility audits are outside this short testing cycle. |
| Test basis | The product description in the supplied README. Approved clarifications, designs, and source code will supplement this basis when available; they are not included in the starter. The nine assignment steps define this plan's structure. |
| Constraints | Proposed five-working-day cycle; one tester; part-time developer and product-owner support; two desktop browsers. Actual calendar dates depend on the team's release schedule. |
| Planning assumptions | A runnable web application and isolated test environment will be provided before execution. Proposed validation rules are that checkout follows check-in and guest count is a whole number from 1 to the selected rental's capacity, C. These are assumptions requiring product-owner approval, not supplied requirements. |

During the Day 1 review, the product owner must confirm required fields, date restrictions, rental capacities, which values can be increased/decreased/reset, step sizes, reset defaults, and booking-list persistence expectations. Account requirements and supported browsers also need confirmation. Do not invent expected results for unresolved rules; record affected cases as blocked until clarified.

### Requirements coverage

These identifiers are assigned for traceability to the six features in the supplied product description.

| ID | Feature | Planned checks |
| --- | --- | --- |
| R1 | Select a rental | Select each available test rental; confirm the selected rental is used in the booking. |
| R2 | Enter check-in and checkout dates | Valid date range; missing or invalid values; checkout before or equal to check-in; month/year boundaries, using approved date rules. |
| R3 | Enter number of guests | Valid whole numbers, empty input, fractions, nonnumeric input where entry is possible, and approved lower/upper boundaries. |
| R4 | Create a booking | Valid submission creates one booking with correct details; invalid submission creates none; repeated submission does not unintentionally duplicate the booking. |
| R5 | View bookings | Empty list and multiple bookings; correct rental, dates, and guest count; confirm newly created bookings appear. Test reload persistence only if required. |
| R6 | Increase, decrease, or reset applicable values | Each applicable control; approved step size, lower/upper limits, reset default, repeated reset, and resulting submitted values. |

Each test case will reference R1–R6 as applicable and include preconditions, input data, steps, expected results, priority, and actual outcome.

## 2. Roles and Responsibilities

These are planned project roles, not claims about assigned classmates.

| Role | Responsibilities | When involved | Communicates with |
| --- | --- | --- | --- |
| Tester / test lead | Plan and prioritize tests; prepare data; execute checks; record defects and results; assess exit criteria. | Days 1–5 | Developer for defects and builds; product owner for requirements, risks, and completion status. |
| Developer | Provide a testable build; maintain component/integration tests; investigate and fix defects; identify affected areas. | Setup on Days 1–2; fixes and support on Days 3–5 | Tester for reproduction and retesting; product owner for behavior decisions. |
| Product owner | Clarify expected behavior; approve scope and acceptance criteria; prioritize defects; decide release readiness and accept any residual risk. | Day 1 review, daily triage as needed, Day 5 decision | Tester and developer. |

## 3. Test Approach

Review requirements and the plan before executing tests. Prioritize booking-data accuracy, date/guest validation, and control boundaries. Run prerequisite smoke checks before dependent booking tests.

| Test level | Focus | Test types and techniques | Execution and deliverables |
| --- | --- | --- | --- |
| Component | Date and guest validation; value-changing logic. | Functional testing; equivalence partitioning and boundary value analysis. | Developer automates using the application's existing compatible framework once source is available; automated test files and results. |
| Integration | Transfer of selected rental, dates, and guests through the form, booking-creation logic, and booking list. | Functional and regression testing; decision tables for combinations of valid/invalid required inputs. | Developer automates supported interfaces; tester checks observable data flow; integration cases and results. |
| System | Complete select → enter details → create → view flow; invalid submissions; applicable controls. | Functional and regression testing; boundary checks and exploratory testing. | Tester manually executes in both planned browsers; test cases, results, screenshots when useful, and defect reports. |
| System | Labels, validation messages, keyboard operation, and visible focus on the booking flow. | Basic usability and accessibility testing; checklist-based testing. | Manual browser checks; checklist results and defect reports. |
| Acceptance | Representative valid booking and applicable control behavior against approved expectations. | Functional acceptance testing; scenarios derived from requirements. | Product owner reviews demonstrated outcomes with the tester; recorded acceptance decision. |

For the proposed guest range 1–C, boundary data includes 0, 1, 2, C−1, C, and C+1, removing duplicates as needed. Date checks include checkout before, on, and after check-in, subject to the approved rules. A decision table covers valid/invalid rental selection, dates, and guests; booking creation is expected only when all required inputs are valid. Exploratory sessions examine repeated actions, error recovery, and unexpected navigation.

After a fix, repeat the failed test to confirm the correction, then run regression tests for related features and the core booking flow. Any build change requires the high-priority booking and validation regression suite to pass again on the candidate build.

**Deliverables:** This test plan; reviewed test cases and requirements-to-test mapping; automated files and run results when implemented; manual results; defect reports; and a completion report with coverage, unresolved risks, and release recommendation. Requirements coverage is mandatory. Code coverage may be collected if the framework supports it; no unsupported code-coverage percentage is assumed.

## 4. Test Requirements and Resources

| Resource | Required preparation |
| --- | --- |
| Environment | Isolated local or staging build with recorded version/commit and configuration; separate test data; a documented reset procedure. Verify booking creation and retrieval are available. |
| Browsers/devices | Desktop Chrome and Firefox, with versions recorded at execution. Use the same fixture data in both. Product owner confirms this proposed support scope on Day 1. |
| Tools | Git, GitHub, a Markdown editor, browser developer tools, and the application's existing test runner if available. Record installation and run commands when the implementation is supplied. |
| Test data | Synthetic rentals with distinct identifiers and known approved capacities; valid/invalid dates and guest values; empty and populated booking lists; approved defaults for each resettable value. Restore fixtures between tests that change data. |
| Access/accounts | Permission to run the test build, reset test data, read relevant source, and report issues. Provide test accounts only if the application requires login; use synthetic data and keep credentials out of GitHub. |
| People/training | One tester familiar with the workflow; developer support for setup and fixes; product owner available for rule decisions. Brief the tester on the runner, reset process, severity definitions, and defect-report format. |
| Effort/budget | Initial planning estimate: 20 tester-hours over five days, plus 4 developer-hours and 2 product-owner-hours. Existing hardware and tools are assumed to require no new purchases. Re-estimate after Day 1 review and after major defects; defect repair may require additional effort. |

## 5. Risk Register

Likelihood and impact use a 1–5 scale: **1 = very unlikely / negligible**, **3 = possible / moderate**, **5 = very likely / catastrophic**. Score = likelihood × impact. Scores are initial planning judgments and will be reviewed as evidence changes. Higher scores receive earlier attention; dependencies can change execution order.

| ID | Risk | Type | Likelihood | Impact | Score | Mitigation | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |
| K1 | Invalid dates or guest counts create an unusable booking. | Product | 4 | 4 | 16 | Prioritize validation partitions and boundaries; verify rejection creates no booking; rerun after changes. | Developer; tester verifies |
| K2 | A booking contains the wrong rental/details, disappears from the booking list, or is unintentionally duplicated. | Product | 3 | 5 | 15 | Compare submitted and displayed data; test multiple bookings and repeated submission; check persistence if required. | Developer; tester verifies |
| K3 | Increase/decrease/reset controls violate limits or submit stale values. | Product | 3 | 3 | 9 | Check each applicable control at both limits and after reset; verify submitted values. | Developer; tester verifies |
| K4 | Missing builds, unavailable environment access, or contaminated data delay execution. | Project | 3 | 4 | 12 | Verify setup early; record run/reset instructions; maintain reusable fixtures and an approved local fallback when feasible. | Developer |
| K5 | Unclear date, capacity, or reset rules lead to incorrect expected results and rework. | Project | 4 | 4 | 16 | Resolve rules on Day 1; record approved decisions; block affected cases until clarified. | Product owner |

The tester reviews risks during daily triage. Unresolved high-impact concerns are escalated to the product owner; a low numerical score alone does not justify ignoring serious consequences.

## 6. Entry Criteria

Before the planned system test execution begins, mark every item **met** or **not met**, with evidence:

1. A versioned candidate build opens in both planned browsers, and all prerequisite smoke checks pass: rental selection, form access, and booking-list access.
2. The product owner has recorded the rules identified in Section 1, and all planned test cases have reviewed expected results and R1–R6 mappings.
3. Required tools and permissions work; synthetic rentals, dates, guest values, and booking-list fixtures are available; the tester has successfully reset the test data once.
4. Developer component/integration tests identified as prerequisites have completed and passed, with results recorded. Any unavailable prerequisite is documented and resolved before dependent system testing starts.

Planning, reviews, and environment setup may occur before these execution gates are met.

## 7. Exit Criteria

Testing is complete and the candidate is ready for a release recommendation only when all of these measurable conditions are met:

1. **100% of the approved planned cases are executed**, with actual results recorded; no cases remain blocked or not run. A blocked case does not count as executed.
2. **100% of high-priority cases pass** and **at least 95% of all planned cases pass** on the candidate build. High-priority cases cover the core booking flow, booking-data accuracy, and date/guest/control-boundary validation.
3. **100% requirements coverage:** all six features R1–R6 have linked, executed tests, including applicable valid/invalid and control scenarios. Coverage measures execution, not proof of defect absence.
4. **Zero open Critical or High defects.** Critical means the application/core workflow is unavailable or booking data is lost or corrupted; High means a required feature gives incorrect results or cannot be completed without a reasonable workaround. Any remaining lower-severity defects have recorded impact and explicit product-owner acceptance.
5. **100% of the high-priority regression suite passes in both planned browsers** on the final candidate. Fix confirmation results are recorded for every resolved defect.
6. The completion report includes results, coverage, outstanding defects/risks, and a documented product-owner release decision.

For execution and pass-rate calculations, count each planned test-case/configuration combination once, using its latest outcome on the candidate build. Pass rate = passed combinations ÷ all planned combinations × 100. Requirements coverage = features with executed linked tests ÷ 6 × 100.

If the time budget expires or a blocking environment failure prevents meaningful testing, pause execution and report incomplete criteria. A deadline alone does not satisfy the quality gates; the product owner decides whether to extend testing, defer the release, or explicitly accept a documented exception.

## 8. Test Schedule

Days are relative working days, not an asserted assignment due date. Tester effort totals 20 hours; developer and product-owner support are additional.

| Activity | Responsible role | When / tester effort | Dependency |
| --- | --- | --- | --- |
| Review requirements, confirm assumptions, and assess risks | Tester + product owner | Day 1 / 2 h | Supplied requirements available |
| Design cases, map R1–R6, and approve expected results | Tester + product owner | Days 1–2 / 4 h | Requirements and behavior rules reviewed |
| Prepare build, tools, access, and test fixtures | Developer + tester | Days 1–2 / 2 h | Build access; agreed environment and data rules |
| Review component/integration results and verify entry criteria | Developer + tester | Day 2 / 1 h | Cases reviewed; environment ready; prerequisite tests run |
| Execute high-priority functional and boundary tests | Tester | Day 3 / 4 h | All system-test entry criteria met |
| Complete remaining cases, browser checks, and exploratory checks | Tester | Day 4 / 3 h | Stable build; high-priority results reviewed |
| Fix defects, confirm fixes, and run final regression | Developer + tester | Days 4–5 / 3 h tester time | Defects triaged; corrected builds available |
| Evaluate exit criteria, complete report, and review release decision | Tester + product owner | Day 5 / 1 h | Current results and outstanding risks documented |

If fixes exceed the reserved time, update the estimate and schedule; report unmet exit criteria explicitly.

## 9. Communication Plan

| Information | Audience | Method | When / frequency |
| --- | --- | --- | --- |
| Scope, rules, assumptions, and requirement changes | Tester, developer, product owner | README/plan updates and linked GitHub issues | Day 1 review and whenever a decision changes |
| Progress: executed/pass/fail/blocked counts, risks, next steps | Project team | Daily written status in a GitHub tracking issue; brief team check-in | End of each testing day |
| Defects with severity, build/browser, reproduction steps, expected/actual result, and evidence | Developer; product owner for prioritization | GitHub issue linked to test and requirement IDs | When found; Critical/High defects flagged immediately through the team's agreed chat channel |
| Environment blockers or schedule/effort changes | Developer and product owner | Tracking issue plus team chat for urgent blockers | Immediately when work is blocked; review during daily triage |
| Fixes and retest outcomes | Tester and developer | Linked commit/PR and updated defect issue with test evidence | When a fix is available and after retesting |
| Completion results, unresolved risks, and release decision | Product owner and project team | Test completion report committed to the repository | End of Day 5 or when testing is stopped/completed |

Planned communication records describe future testing work; this submission does not claim that tests have passed or that a release has been approved.
