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

- OBS-01: Submitting an empty form shows "Error! An internal error has occurred and has been logged." instead of field-level messages. Reproduced: (3 of 3 attempts).
- OBS-02: Submitting a form with valid data redirects to a page with "Welcome `username`. Your account was created successfully. You are now logged in."
- OBS-03: First Name, Phone # and Zip Code accepted letters, digits and symbols (see table above). Other fields not yet checked.

## 3.2 Out of scope (noticed, not tested)

- "Customer Care" form: email format is not validated.
- Home page links "ATM Services" and "Online Services" show raw XML: "This XML file does not appear to have any style information associated with it."

## 4. Assumed requirements
- AR-01: names should contain letters only.
- AR-02: phone should contain digits only.
- AR-03: zip code should contain digits only.
- AR-04: First Name accepts 1 to 50 characters.
- AR-05: Username must be unique.

## 5. Test cases
(on days 4–5)