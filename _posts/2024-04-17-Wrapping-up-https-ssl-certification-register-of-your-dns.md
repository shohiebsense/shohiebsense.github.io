1. Sign Up your account to cloudflare
2. Add the website (dns you make to cloudflare) [example reference](https://contabo.com/blog/how-to-configure-cloudflare/)
3. Login to domain registrar
4. Find the DNSSEC at the registrar, turn DNSSEC off, after at least 24 hours. Turn it back on
5. Find the list of nameservers at your registrar, and add Cloudflare nameserver, remove if theres existing nameserver.
6. If the DNSSEC is already off, to turn it on [reference](https://developers.cloudflare.com/dns/dnssec/), has something to do with CNAME and DS Records.
7. Next you sign up to ssl provider, claim your webserver / website ownership, I do it by using web server and upload to http webserver at certain location.
8. You finally can get the certifications and private key to enable TLS
