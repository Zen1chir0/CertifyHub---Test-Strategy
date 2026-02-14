# CertifyHub Test Strategy

| Document Info | Details |
| :--- | :--- |
| **Project** | CertifyHub |
| **QA Lead** | Kenneth Flororita |
| **Version** | 1.0 |
| **Estimated Duration** | TBD |

---

## 1. Executive Summary
The test will focus on verification of end-to-end services together with both ends of the system (frontend (UI level of the application) as well as the backend (logic level of the application)). The test will revolve around the objective of ensuring the system delivers high quality performance while maintaining its stability throughout the test. 

The project name is entitled "Test Strategy: CertifyHub", straightforward and concise. The test will cover the primary goal of the system which is to fasten and simplify the issuance of certificates and will also act as the database of certificates. These certificates are issued to OJT applicants, work immersionists, and other events.

---

## 2. Scope of Testing
The test will cover end-to-end test of system stability while the admin issues certificates and the user verifies them via QR code.

### In Scope
#### **Certificate Issuance and Database**
* **Admin Management:**
    1. Verify successful issuance of certificates using the sole Admin account.
    2. Verify accurate data entry and storage of OJT applicants and work immersionists in the system database.
    3. Verify system response for bulk issuance to ensure stability during multiple requests.
* **Email Delivery Service:**
    1. Verify that the system correctly sends the certificate to the recipient's email account.
    2. Verify attachment integrity and readability of the issued certificate within the email.

#### **Verification System**
* **QR Code Functionality:**
    1. Verify that the generated QR code on the certificate is scannable and contains the correct URL.
    2. Verify redirection to the issuer website upon scanning the QR code.
* **Authenticity Logic:**
    1. Verify the system displays a "legit" or verified status for valid certificates.
    2. **Negative Testing:** Verify that unauthorized or modified URLs/IDs result in a failed verification message.

### Out of Scope
* **User Registration:** The system is designed for a sole Admin user; public account creation is not required.
* **Payment Processing:** No financial transactions are involved in the issuance of these certificates.
* **Stress Testing:** Testing for thousands of concurrent issuers is not required for this current scope.

---

## 3. Test Environment
* **System/App URL:** https://certifyhub-api.azurewebsites.net/
* **Primary Browser:** Google Chrome (Latest Version)
* **Mobile Verification:** QR code scanning and verification page testing will be performed on mobile devices (Android/iOS) to ensure real-world usability.

---

## 4. Testing Approach Utilized
The test will implement "Black Box Testing" to verify the functional requirements of the certificate lifecycle without needing to view the internal code structure.

| Testing Phase | Type | Testing Objective |
| :--- | :--- | :--- |
| **Issuance Flow** | **Functional** | Verify that the Admin can create and send a certificate without system errors. |
| **Email Integration** | **Integration** | Ensure the backend logic successfully triggers the email service and delivers the correct file. |
| **QR Verification** | **End-to-End** | Verify that the physical/digital certificate can be traced back to the database for authenticity. |
| **Data Integrity** | **Database** | Ensure that the info displayed on the verification site matches the record stored in the database. |

---

## 5. Defect Management / Bug Process
All defects found will be documented to properly handle issues. The issues found are sought to be classified in:

* **Critical (Severity 1): Complete App Block**
    * The Admin cannot issue certificates or the verification site is down. Marked as critical because the core purpose of the system is not met.
* **High (Severity 2): Major feature breakage**
    * Certificates are issued but emails are not received, or QR codes lead to 404 pages. The system functions but the end-to-end goal fails.
* **Medium (Severity 3): UI/UX Issue**
    * Misalignment of the certificate layout or verification page distortion on mobile devices. Affects the company's professional image.
* **Low (Severity 4): Minor Typo or QA suggestion**
    * Simple typos in the certificate template or footer information that do not affect functionality.

---

## 6. Risks & Mitigation
The main risks lie on the delivery and validation components of the system.

| Identified Risk | Mitigation Strategy |
| :--- | :--- |
| **Email Spammability** | Automated emails might be flagged as spam by providers (Gmail/Yahoo). The QA will test delivery across multiple email platforms to ensure inbox arrival. |
| **URL Persistence** | Changes in the website domain could break existing QR codes. Verify that the URL structure is intended for long-term use. |
| **Data Accuracy** | Input errors during issuance could result in permanent wrong data in the database. Implement validation checks for name and email formats. |

---

## 7. Entry & Exit Criteria
### Entry Criteria (Start)
1. Admin credentials and system URL are provided and accessible.
2. The database is ready for test data insertion and cleanup.

### Exit Criteria (Stop)
1. 100% of functional test cases regarding Issuance and Verification are executed.
2. Zero "Critical" or "High" bugs remain open.
3. Verification of QR code redirection is successful across both Desktop and Mobile browsers.
