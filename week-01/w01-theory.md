
# QA Theory: Week 1

## 1. QA, QC, Testing:

* QA - focuses on the process: we work to prevent bugs from occurring. The entire team is responsible.
* QC - focuses on the product: we inspect the finished product and identify issues.
* Testing - the primary method of QC.

---

## 2. Error-Defect-Failure:

* Error - a person made a mistake (example: misunderstood a requirement).
* Defect (bug) - a flaw in the code or documentation caused by this error.
* Failure - the user observes incorrect system behavior. (Not every defect manifests as a failure.)

---

## 3. Seven Principles of Testing:

1. Presence, not absence - tests reveal bugs, but they do not prove that none exist.
2. Exhaustive testing is impossible - it's impossible to test everything; we set priorities based on risk.
3. Early testing - the sooner a bug is found, the cheaper it is to fix.
4. Defects cluster - bugs tend to cluster in a few modules (80/20).
5. Pesticide paradox - the same tests eventually stop finding
new defects.
6. Context-dependent - a banking system and a game are tested differently.
7. Absence-of-defects fallacy - a product without bugs but useless to the user is still a failure.

---

## 4. Levels and Types of Testing:

* Levels answer "on what scale": unit (a single component),
integration (components together), system (the entire system), system integration (with
external services), acceptance (is it ready for the customer, UAT).
* Types answer "what we`re testing": functional, non-functional, black-box, white-box.

---

## 5. Functional vs. non-functional, black-box vs. white-box:

* Functional - what the system does (login works, order is created).
* Non-functional - how well: speed (performance), security,
usability, reliability.
* Black-box - tests based on requirements; we don't look at the code. White-box - tests based on the code; we measure code coverage.

---

## 6. Confirmation, Regression, Smoke:

* Confirmation (re-testing) - we verify that a specific bug has been fixed.
* Regression - we verify that the fix hasn't broken anything else. There are more and more of these tests with each release, so they are automated: that's a large part of an AQA's work.
* Smoke - a quick check of the main functions of a new build: to determine whether it's even possible to continue testing.

---

## 7. Test pyramid:

* At the bottom are many fast unit tests; in the middle are API/integration tests; at the top are a few slow UI/E2E tests.
* The higher the layer, the slower, more expensive, and less stable the test, so there should be fewer of these tests.
* Ice cream cone antipattern: an inverted pyramid, with many UI tests and few unit tests.

---

## 8. Shift left, CI/CD:

* Shift left - test earlier: requirements reviews, tests before code, automated tests for every commit. It's more expensive at first, but pays off later. Tests at the end aren't skipped.
* CI - every commit is automatically built and verified by tests.
* Continuous Delivery - the product is always ready for release; deployment is at the click of a button.
* Continuous Deployment - automatic deployment.
* DevOps - a culture where development, operations, and testing work together and automate delivery.

---

## 9. Agile and Scrum:

* Agile - an approach: short iterations, a working product, readiness for changes.
* Scrum is a framework within Agile.
* Roles: Product Owner (what we`re doing), Scrum Master (process), Developers (including testers).
* Events: Sprint, Planning, Daily, Review (demo), Retrospective (what to improve).

---

## 10. Severity vs. Priority:
* Severity - how serious the bug is for the system.
* Priority - how urgent the fix is from a business perspective.  

"Smoke" is broad and superficial, while "sanity" is narrow and deeper.  

Example: A typo in the company name on the home page (low severity, high priority) and a crash of a rarely used admin feature (high severity, low priority).  

Flaky test: a test that sometimes passes and sometimes fails without any changes to the code (reasons: "sleep", data dependencies, test order, network issues).

*Additional topics covered: UAT/alpha/beta, ISO 25010, integration strategies, stubs and drivers, types of reviews, maintenance testing, Kanban, TDD/BDD.*