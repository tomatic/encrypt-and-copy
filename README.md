# Encrypt & Copy

Static HTML webpage that lets users encrypt and copy text so they can safely send it via email. Main use-case is allowing people to email you confidential stuff like login credentials without knowing anything about encryption, PGP, etc. Works entirely in the browser, nothing is processed or saved server-side.

# Installation

1. Generate an encryption key: `openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048`.
2. Store the key somewhere safe (like in your password manager).
3. Extract the public key from your encryption key: `openssl rsa -pubout -in private_key.pem -out public_key.pem`.
4. Replace the public key in `encrypt.html` with the public key you just generated.
5. Host the files anywhere you can host HTML. Only requirement is serving them via HTTPS, otherwise the Web Crypto API used to encrypt/decrypt will not work.

# Usage

1. Have the person who wants to send you confidential information go to `encrypt.html`.
2. They enter their confidential info and click "Encrypt and Copy".
3. They paste the encrypted data into an email and send it to you.
4. You go to `decrypt.html`.
5. You enter your private key (the one you stored in a safe place earlier) and the JSON from the person's email and click "Decrypt".
6. The decrypted text is displayed at the bottom of the page.
