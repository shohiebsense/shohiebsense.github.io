1. Software Development should keep 'secure' in mind from the start and throught SDLC process.
2. Be careful during code Reviews (access modifiers), Third party libraries usage, or modules that are developed by third-party vendors.
3. Make some technical standards, coding guidelines, and reference frameworks (find out if the third party libraaries have any issues with security vulnerabilities).
4. Things to do: Code Review, Architecture Risk Analysis, Pentests, Risk-based seecurity testing (reviewing the security of all functions), abuse cases, fraud detection, security incident response.
5. Use automated code review to reduce time-consumption.
6. Code reviews to read subtle issues.
7. Benefit of executing security assesments will be cheaper if it's done during early stage of SDLC.
8. Distinguish among a Plaintext, Chipertext, Crpytographic Primitive, Cryptographic Protocol, Encrypt and Decrypt.
9. Crpytography is useful on Confidentiality, Data Integrity, Data Origin Authentication, Entity Authentication, Non-Repudiation processes.
10. Cryptographic Primitives: Encryption, Hash Functions, Message Authentication Codes, Digital Signatures
11. Although Asymmetric Key Encryption is slower than Symmetic one, it's highly preferred.
12. Modern crptographic chipers: (1) Block Chipers = the message is longer in length than the block size, (2) Stream Chipers = a keystream (bits that is the same length as the data)
13. Swap the currently using algorithm with the better ones once a serious weakness is discovered.
14. Encryption Modes: (1). Electronic Codebook Mode (ECB), (2) Cipher Block Chaining (CBC) = the most commonly used, (3) Galois/counter Mode (GCM) = securely protect both confidentiality and integrity of data. Should be used if it's possible.
15. Padding Models: (1) PKCS5 (2) PKCS7
16. Asymmetric Key Algorithms: (1) RSA with Optional Asymmetric Encryption Padding (OAEP) should be used whenever possible.
17. Common Hash Functions: MD5, SHA-1, SHA-2, SHA-3, SHA-224, SHA-256. SHA-384, SHA-512, SHA3-224, SHA3-256, SHA3-384, SHA3-512.
18. Hash functions are irreversible, commonly used to store passwords altough the sole usage is not enough.
19. Using Salt to add some protection layer (1) Salt + HMAC (Data with secret key) or (2) without secret key (Salt + Adaptive Hash)
20. Hash Functions: (1) Checksums, (2) Message Authentication Codes, (3) Digital Signatures.
21. Hashes Algorithms (The general ones are the unkeyed ones) give fixed length, hash while MAC Hashes provivdes cryptograpchic algorithm (assymmetric key encryption algorithms)
22. Common Digital Signature Algorithms: RSA, Digital Signature Algorithm, Elliptic Curve Digital Signature algorithm, ElGamal.
23. Choosing Protocols and Algorithms: Avoid proprietaary crpythographic algorithms and protocols. Avoid using outdated algorithms  (MD5, SHA-0, SHA-1), symmetric encryptions (DES, RC4), and protocols (SSL 1.0, 2.0, 3.0, TLS 1.0)
24. 
