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
15. Padding Models: (1) PKCS5 (2) PKCS7.
16. Asymmetric Key Algorithms: (1) RSA with Optional Asymmetric Encryption Padding (OAEP) should be used whenever possible.
17. Common Hash Functions: MD5, SHA-1, SHA-2, SHA-3, SHA-224, SHA-256. SHA-384, SHA-512, SHA3-224, SHA3-256, SHA3-384, SHA3-512.
18. Hash functions are irreversible, commonly used to store passwords altough the sole usage is not enough.
19. Using Salt to add some protection layer (1) Salt + HMAC (Data with secret key) or (2) without secret key (Salt + Adaptive Hash).
20. Hash Functions: (1) Checksums, (2) Message Authentication Codes, (3) Digital Signatures.
21. Hashes Algorithms (The general ones are the unkeyed ones) give fixed length, hash while MAC Hashes provivdes cryptograpchic algorithm (assymmetric key encryption algorithms)
22. Common Digital Signature Algorithms: RSA, Digital Signature Algorithm, Elliptic Curve Digital Signature algorithm, ElGamal.
23. Choosing Protocols and Algorithms: Avoid proprietaary crpythographic algorithms and protocols. Avoid using outdated algorithms  (MD5, SHA-0, SHA-1), symmetric encryptions (DES, RC4), and protocols (SSL 1.0, 2.0, 3.0, TLS 1.0)
24. Source of Troubles (Connectivity, Complexity, Extensibility).
25. Encryption Better Pratices: (1) Use TLS, HTTPS, Implements HTTP Strict Transport Security Header, Use `Secure` flag on all over cookies, Do not pass sensitive information in the URL, use private key to generate HTTPS Certificates, use strong HTTPS Protocol and chiper configurations.
26. Protect Sensitive Keys (never expose sensitve keys in source code and configuration files).
27. AES-GCM over AES-CBC.
28. Full disk encryption where sensitive data is stored.
29. Source of Injection Attacks (SQL Statements, LDAP Queries, OS Shell Commnds (string-based commands), XML Parser (XML, DTD, XPath Queries), Cross-Site Scripting (XSS): Accessing the Session ID Value, fake login popups, ketystokes.
30. Avoid URL Redirects if it's possible. Or explicitly declare the URL (whitelisting) and deny all other routes, redirect validation.
31. Password protection: (1) Strong password, (2) Change and Reset Controls, (3) Adaptive One-Way Functions, (4) Multi Factor Authentication, (5) Reauthentication, (6) Access Denial by Default, (7) Least Privilege.
32. Don'ts: Exposing the cookie to insecure traansfer protocol, multiple applications, Cookies without expiration, Predictable Session ID, allowing Cookie to be accessed by client-side scripts.
34. Cross-Site Request Forgery: Bypassing Sessioned Https Requests, Avoid this by: Use framework specific protection method, implement synchronizer token in a hidden HTML field, include CSRF tokens in Javascript Requests, do Re-authentications, Do state-changing functions only via POST, Double-submit cookie pattern.
35. Add cookie flags: `SameSite`, `HttpOnly`.
36. Session ID Timeouts: Absolute Timeouts, Idle Timeouts.
37. Session ID should never be predictable.
38. Check **OWASP Dependency Check** for info about third party libraries.
39. Tools: Firewalls, Alerts and Logging, Detection, Honeypots.
40. Cookie vulnerability example: intercepting proxy to modify certain cookie value.
41. Owasp Top 10: (1) Injection, (2) Broken Authenticartion, (3) Sensive Data Exposure, (4) XML External Entities, (5) Broken Access Control, (6) Security Misconfigurations, (7) Cross-Site Scripting, (8) Insecure Desentriaaalization, (9) Components or thired party libraries with Known Vulberabilities, (10) Insufficient Logging and Monitoring.
