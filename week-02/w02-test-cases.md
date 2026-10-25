# Test Cases: ParaBank Registration Form

## 1. Test object
- Site: https://parabank.parasoft.com/parabank/register.htm
- Demo site for software testing practice
- Scope: the customer registration form

## 2. Environment
- Browser: Chrome 155.0.8059.39 (official build) (x86_64)
- OS: Fedora Linux (KDE Plasma)
- Date: 2026-10-14

## 3. Fields observed

| Field | Input tried | Observed result | Matches assumption? |
| --- | --- | --- | --- |
| First Name | `123@#` | Form submitted, account created | No (AR-01: names should contain letters only) |
| Phone # | `abc` | Form submitted, account created | No (AR-02: digits only) |
| Zip Code | `abcde` | Form submitted, account created | No (AR-03: digits only) |
| First Name | 100 × `a` (username `mrmr_test_04`, new; other fields valid) | Message "This username already exists" | No (AR-04: names up to 50 characters should be rejected with a clear message). Suspicious: the message is about username, not name length |
| Username | mrmr_test (first registration, unique) | Account created | Yes (AR-05) |

## 3.1 Recon observations

- OBS-01: Submitting an empty form shows a "First name is required", "Last name is required", "Address is required", "City is required", "State is required", "Zip Code is required", "Number is required", "Username is required", "Password is required", "Password confirmation is required" messages.
- OBS-02: Submitting a form with valid data redirects to a page with "Welcome `username`. Your account was created successfully. You are now logged in."
- OBS-03: First Name, Last Name and Phone # accepted values that break AR-01 and AR-02 (digits and symbols in names, letters and symbols in the phone number), see TC-REG-001 to 005. Zip Code accepted letters (TC-REG-007), but symbols led to the "Error! An internal error has occurred and has been logged." page (TC-REG-006).
- OBS-04: Required-field checks work: empty fields show "... is required" messages next to the field, and mismatching passwords show "Passwords did not match" (TC-REG-011, 014 to 019).
- OBS-05: Address, City, State and SSN were not checked for invalid characters or length.

## 3.2 Out of scope (noticed, not tested)

- "Customer Care" form: email format is not validated.
- Home page links "ATM Services" and "Online Services" show raw XML: "This XML file does not appear to have any style information associated with it."

## 4. Assumed requirements
- AR-01: names should contain letters only.
- AR-02: phone should contain digits only.
- AR-03: zip code should contain digits only.
- AR-04: First Name accepts 1 to 50 characters.
- AR-05: Username must be unique.
- AR-06: All fields are required.
- AR-07: Password and Confirm must match.
- AR-08: A validation message is shown next to the field that failed.

## 5. Test cases

### Valid data set
| Field | Value |
| --- | --- |
| First Name | Anna |
| Last Name | Test |
| Address | 1 Test Street |
| City | Testville |
| State | TS |
| Zip Code | 12345 |
| Phone # | 5550001111 |
| SSN | 000-00-0000 |
| Username | kar_test_NN (NN is a unique number) |
| Password | Test1234 |
| Confirm | Test1234 |

### TC-REG-001: First Name with digits is rejected
- **Requirement:** AR-01
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: `123`; all other fields valid; Username: `kar_test_01`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to First Name
- **Actual result:** Account was created; no validation message was shown next to First Name; the page "Welcome kar_test_01" opened
- **Status:** Failed

### TC-REG-002: First Name with symbols is rejected
- **Requirement:** AR-01
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: `@!#`; all other fields valid; Username: `kar_test_02`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to First Name
- **Actual result:** Account was created; no validation message was shown next to First Name; the page "Welcome kar_test_02" opened
- **Status:** Failed

### TC-REG-003: Last Name with invalid characters is rejected
- **Requirement:** AR-01
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Last Name: `372;#`; all other fields valid; Username: `kar_test_03`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Last Name
- **Actual result:** Account was created; no validation message was shown next to Last Name; the page "Welcome kar_test_03" opened
- **Status:** Failed

### TC-REG-004: Phone with symbols is rejected
- **Requirement:** AR-02
- **Priority:** Medium
- **Preconditions:** Registration page is open
- **Test data:** Phone #: `!@#`; all other fields valid; Username: `kar_test_04`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Phone
- **Actual result:** Account was created; no validation message was shown next to Phone; the page "Welcome kar_test_04" opened
- **Status:** Failed

### TC-REG-005: Phone with letters is rejected
- **Requirement:** AR-02
- **Priority:** Medium
- **Preconditions:** Registration page is open
- **Test data:** Phone #: `abc`; all other fields valid; Username: `kar_test_05`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Phone
- **Actual result:** Account was created; no validation message was shown next to Phone; the page "Welcome kar_test_05" opened
- **Status:** Failed

### TC-REG-006: Zip Code with symbols is rejected
- **Requirement:** AR-03
- **Priority:** Medium
- **Preconditions:** Registration page is open
- **Test data:** Zip Code: `!@#`; all other fields valid; Username: `kar_test_06`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Zip Code
- **Actual result:** Account is not created; no validation message was shown next to Zip Code; the page "Error! An internal error has occurred and has been logged" opened
- **Status:** Failed

### TC-REG-007: Zip Code with letters is rejected
- **Requirement:** AR-03
- **Priority:** Medium
- **Preconditions:** Registration page is open
- **Test data:** Zip Code: `abc`; all other fields valid; Username: `kar_test_07`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Zip Code
- **Actual result:** Account was created; no validation message was shown next to Zip Code; the page "Welcome kar_test_07" opened
- **Status:** Failed

### TC-REG-008: First Name with 1 character is accepted
- **Requirement:** AR-04
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: `A`; all other fields valid; Username: `kar_test_08`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is created; the welcome page opens
- **Actual result:** Account was created; the page "Welcome kar_test_08" opened
- **Status:** Passed

### TC-REG-009: First Name with 50 characters is accepted
- **Requirement:** AR-04
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: 50*`A`; all other fields valid; Username: `kar_test_09`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is created; the welcome page opens
- **Actual result:** Account is not created; a "This username already exists" message was shown next to Username
- **Status:** Failed

### TC-REG-010: First Name with 51 characters is rejected
- **Requirement:** AR-04
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: 51*`A`; all other fields valid; Username: `kar_test_10`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to First Name
- **Actual result:** Account is not created; a "This username already exists" message was shown next to Username
- **Status:** Failed

### TC-REG-011: First Name with 0 characters is rejected
- **Requirement:** AR-04, AR-06
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** First Name: (empty); all other fields valid; Username `kar_test_11`
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to First Name
- **Actual result:** Account is not created; a "First name is required" message was shown next to First Name
- **Status:** Passed

### TC-REG-012: Username must be unique
- **Requirement:** AR-05
- **Priority:** High
- **Preconditions:** Registration page is open; Username `kar_test_01` is already registered (TC-REG-001)
- **Test data:** Username: `kar_test_01`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Username
- **Actual result:** Account was created; the page "Welcome kar_test_01" opened
- **Status:** Failed

### TC-REG-013: Username must be unique (with a different text case)
- **Requirement:** AR-05
- **Priority:** High
- **Preconditions:** Registration page is open; Username `kar_test_01` is already registered (TC-REG-001)
- **Test data:** Username: `Kar_test_01`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Username
- **Actual result:** Account was created; the page "Welcome Kar_test_01" opened
- **Status:** Failed

### TC-REG-014: Blank form is not accepted
- **Requirement:** AR-06
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** All fields are empty
- **Steps:**
  1. Leave all fields empty
  2. Click "Register"
- **Expected result:** Account is not created; validation messages are shown next to the fields 
- **Actual result:** Account is not created; a "First name is required", "Last name is required", "Address is required", "City is required", "State is required", "Zip Code is required", "Number is required", "Social Security Number is required", "Username is required", "Password is required", "Password confirmation is required" messages shown next to fields 
- **Status:** Passed

### TC-REG-015: Blank Last Name is not accepted
- **Requirement:** AR-06
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Last Name: (empty); Username: `kar_test_14`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Last Name 
- **Actual result:** Account is not created; a "Last name is required" message is shown next to Last Name 
- **Status:** Passed

### TC-REG-016: Blank Password is not accepted
- **Requirement:** AR-06
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Password: (empty); Username: `kar_test_15`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Password 
- **Actual result:** Account is not created; a "Password is required" message is shown next to Password
- **Status:** Passed

### TC-REG-017: Passwords that do not match are not accepted
- **Requirement:** AR-07
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Password: `Test1234`; Confirm: `Test123`; Username: `kar_test_16`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Confirm 
- **Actual result:** Account is not created; a "Passwords did not match" message is shown next to Confirm
- **Status:** Passed


### TC-REG-018: Blank Confirm is not accepted
- **Requirement:** AR-07
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Confirm: (empty); Username: `kar_test_17`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Confirm
- **Actual result:** Account is not created; a "Password confirmation is required" message is shown next to Confirm
- **Status:** Passed

### TC-REG-019: Passwords that differ in case are not accepted
- **Requirement:** AR-07
- **Priority:** High
- **Preconditions:** Registration page is open
- **Test data:** Password: `Test1234`; Confirm: `test1234`; Username: `kar_test_18`; all other fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is not created; a validation message is shown next to Confirm
- **Actual result:** Account is not created; a "Passwords did not match" message is shown next to Confirm
- **Status:** Passed

### TC-REG-020: All fields are valid; Succesful registration
- **Requirement:** All (baseline positive flow)
- **Priority:** Medium
- **Preconditions:** Registration page is open
- **Test data:** Username: `kar_test_20`; all fields valid
- **Steps:**
  1. Fill all fields with the test data
  2. Click "Register"
- **Expected result:** Account is created; the welcome page opens
- **Actual result:** Account was created; the page "Welcome kar_test_20" opened
- **Status:** Passed


## 6. Execution summary

- Run date: 25.10.2026
- Environment: see section 2

| Total | Passed | Failed | Blocked | Not run |
| --- | --- | --- | --- | --- |
| 20 | 9 | 11 | 0 | 0 |


## 7. Requirements coverage

| Requirement | Test cases | Result |
| --- | --- | --- |
| AR-01 | TC-REG-001, 002, 003 | 3 Failed |
| AR-02 | TC-REG-004, 005 | 2 Failed |
| AR-03 | TC-REG-006, 007 | 2 Failed |
| AR-04 | TC-REG-008, 009, 010, 011 | 2 Passed, 2 Failed (009, 010 to be rechecked) |
| AR-05 | TC-REG-012, 013 | 2 Failed |
| AR-06 | TC-REG-011, 014, 015, 016 | 4 Passed (see note on SSN) |
| AR-07 | TC-REG-017, 018, 019 | 3 Passed |
| AR-08 | checked inside negative cases (006, 011, 014–019) | not a separate case |