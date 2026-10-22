# SubmissionSeal — Assignment Integrity Verifier

A small, browser-only cryptography mini-project for VTU BCS703 (Cryptography and Network Security).

## Run
1. Extract `SubmissionSeal_Project.zip`.
2. Open `index.html` in a current Chrome, Edge, or Firefox browser.
3. Select an assignment under **Seal an original file** and click **Create seal**.
4. Click **Export manifest (.json)** and keep the manifest.
5. To test integrity, select the file under **Verify a file**. Import the saved manifest if needed, then click **Verify integrity**.
6. To demonstrate tampering, make a copy of a text file, change one character, save it under a different name, and verify the changed copy against the original manifest. It should report **MISMATCH — FILE DIFFERS**.

No backend, installation, or third-party library is required. The browser computes SHA-256 locally; files are not uploaded.

## Technical note
The browser Web Crypto API generally requires a secure context. If direct `file://` opening does not allow `crypto.subtle`, run a local server from this folder:
- Windows: open a terminal in the folder and run `py -m http.server 8000`
- macOS/Linux: run `python3 -m http.server 8000`
Then visit `http://localhost:8000`.

## Security limitation
A hash detects changes only when the reference digest is trusted. If an attacker can replace both the file and the manifest, the demo cannot establish authenticity. Protect the manifest separately or use digital signatures / trusted storage in a production system.
