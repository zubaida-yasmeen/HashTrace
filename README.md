# HashTrace — Cryptographic File Integrity Verification

**Live Demo:** https://hashtrace-verifier.vercel.app/

HashTrace is a browser-based cybersecurity application that detects whether a digital file has been modified by comparing its SHA-256 cryptographic hash with a previously saved reference.

## Features

- **SHA-256 Hash Generation:** Generate a cryptographic fingerprint for any selected file.
- **File Integrity Verification:** Check whether a file matches its original reference hash.
- **Tampering Detection:** Identify changes made to a file after its hash was recorded.
- **JSON Manifest Export:** Save file details and the reference hash for later verification.
- **Local Processing:** Files are processed in the browser and are not uploaded to an application server.
- **Seal History:** View recent file seals stored in the browser.

## How It Works

1. Select the original file.
2. Click **Create seal** to generate its SHA-256 hash.
3. Export the JSON manifest containing the reference hash.
4. Select the file you want to verify and import the saved manifest if necessary.
5. Click **Verify integrity** to compare the calculated hash against the reference.

**Possible results:**
- `VERIFIED` — The calculated hash matches the saved reference.
- `MISMATCH` — The calculated hash differs from the reference.

## Technology Stack

- HTML5
- CSS3
- JavaScript
- Web Crypto API
- SHA-256 cryptographic hash function
- GitHub for version control
- Vercel for deployment

## How to Run Locally

1. Clone the repository:

   ```bash
   git clone https://github.com/zubaida-yasmeen/HashTrace.git
   ```

2. Open the project directory:

   ```bash
   cd HashTrace
   ```

3. Open `index.html` in a modern browser.

If the Web Crypto API is unavailable when opening the file directly, start a local server:

```bash
py -m http.server 8000
```

Then visit http://localhost:8000.

## Test the Application

| Test case | Expected result |
|---|---|
| Verify the original file | VERIFIED |
| Modify one character and verify against the original manifest | MISMATCH |
| Verify a different file | MISMATCH |
| Attempt verification without selecting a file | Input warning |

## Security Considerations

HashTrace demonstrates file integrity verification; it does not encrypt files or prevent modifications. The reference manifest must be protected from unauthorized replacement. If an attacker replaces both the file and its manifest, the application cannot independently establish authenticity.

For stronger assurance, the system could be extended with digital signatures or trusted reference storage.

## Academic Context

- **Course:** VTU 2022 Scheme — BCS703, Cryptography and Network Security
- **Project type:** Cryptographic hash-based file integrity verification
- **Objective:** Demonstrate how cryptographic hashing can be used to detect changes in digital files.

## Future Enhancements

- Digital signatures for manifest authenticity
- Trusted timestamps and audit logs
- Batch verification of multiple files
- Downloadable verification reports
- Integration with an assignment submission portal

## License

Developed as an educational cryptography project.
