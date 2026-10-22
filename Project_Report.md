# Mini-Project Report
## SubmissionSeal: Assignment Integrity Verification Using SHA-256

**Course:** VTU 2022 Scheme — BCS703, Cryptography and Network Security  
**Project type:** Cryptographic hash-based integrity verification  
**Implementation:** HTML, CSS, JavaScript, Web Crypto API  
**Execution requirement:** Modern browser; no backend or external dependencies

## 1. Abstract
SubmissionSeal is a lightweight tool that creates a SHA-256 fingerprint for an assignment file and later checks whether a selected file matches that reference. The application calculates the digest locally in the browser, saves recent reference details in browser storage, and exports a JSON manifest for later verification. A changed file produces a different digest with overwhelming probability, allowing the user to demonstrate file-integrity checking in a simple academic workflow.

## 2. Problem Statement
Assignment files may be altered accidentally or intentionally after an original version has been recorded. A filename and file size alone cannot reliably identify content changes. A repeatable cryptographic fingerprint provides a compact way to compare the file's current bytes against a previously recorded reference.

## 3. Objectives
- Compute SHA-256 digests for user-selected files.
- Store reference details locally in the browser.
- Export a portable JSON manifest.
- Verify a later file against a saved reference.
- Demonstrate how a small content modification changes the digest.

## 4. Scope
The prototype supports local file selection, digest creation, JSON manifest export/import, and integrity comparison. It is intended for a classroom demonstration and does not upload files to a server. It does not provide user accounts, remote timestamping, digital signatures, or institutional document management.

## 5. Cryptographic Principle
SHA-256 is a cryptographic hash function that maps arbitrary input bytes to a 256-bit digest, usually represented as 64 hexadecimal characters. It is designed to make it computationally infeasible to find a practical collision or recover the input from the digest. The program uses the browser's Web Crypto API (`crypto.subtle.digest("SHA-256", fileBytes)`) rather than implementing the hash algorithm from scratch.

## 6. System Design
1. **Input:** The user selects a file.
2. **Digest generation:** JavaScript reads its bytes and calculates SHA-256.
3. **Reference creation:** Filename, size, creation time, algorithm, and digest are recorded.
4. **Manifest handling:** The reference can be exported to or imported from JSON.
5. **Verification:** The selected file's digest is compared with the reference digest.
6. **Result:** A match is reported as VERIFIED; a mismatch is reported as MISMATCH.

## 7. Algorithm
1. Read the selected file as an array buffer.
2. Compute the SHA-256 digest of the bytes.
3. Convert the digest bytes to hexadecimal.
4. Save or export the digest as a reference.
5. During verification, calculate the digest of the candidate file.
6. Compare candidate and reference digests.
7. Display the result and both digest values.

## 8. Test Cases
| Test | Procedure | Expected result |
|---|---|---|
| Original file | Seal a file and verify the same file | VERIFIED |
| Changed content | Edit one character and verify against the original manifest | MISMATCH |
| Different file | Verify an unrelated file | MISMATCH |
| No file selected | Click verify without selecting a file | Input warning |
| Invalid manifest | Import JSON without a valid SHA-256 digest | Manifest error |

## 9. Advantages
- Quick to run and demonstrate.
- No package installation or server required in a modern browser.
- Files are processed locally.
- Manifest makes the reference portable.
- Clearly illustrates cryptographic integrity verification.

## 10. Limitations and Security Considerations
A digest proves only that the candidate matches the reference digest; it does not by itself identify who created the file or when it existed. If an attacker can replace both the file and the manifest, the attacker may replace the reference digest too. For stronger assurance, digitally sign the manifest or store it in a trusted, access-controlled system. Browser local storage is not a secure evidence archive. SHA-256 is an integrity primitive, not encryption, and it does not hide file contents.

## 11. Future Enhancements
- Digitally sign manifests using public-key cryptography.
- Add a trusted timestamp or append-only audit log.
- Verify multiple files in batches.
- Add a downloadable PDF verification receipt.
- Integrate with a college submission portal.

## 12. Conclusion
SubmissionSeal demonstrates the use of a cryptographic hash function for practical file-integrity verification. By recording and comparing SHA-256 digests, the prototype makes content changes visible and provides a compact, reproducible classroom demonstration of a core cryptography concept.
