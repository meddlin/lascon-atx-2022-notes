# Abridged History of AppSec

> LASCON Recorded video: [https://www.youtube.com/watch?v=QbEjNqKRhCg](https://www.youtube.com/watch?v=QbEjNqKRhCg)

Jim Manico, Manicode Security
Twitter [@manicode](https://twitter.com/manicode)
jim@manicode.com — [https://manicode.com/](https://manicode.com/)

---


## InfoSec Dark Ages

1960s US government/military task force stuff
- they were building a lot of software and saw the need for security even back then
- October 1975 R-609 Declassified


## Security Testing History

- think of Enigma machine, physical security breaking ciphers, etc.
- 1960s-70s—not having security in software that runs the country
- 1979—lint is published, this is super basic static analysis
- 1990s—Windows cracking tools, Metasploit, SQLInjection, etc. …all of these things started coming out
- 2009—DevOps basically starts (Etsy started this)
- 2010—OWASP ZAP is released
- 2013—more OWASP infrastructure software starts getting pushed
- 2015-20s—OWASP dependency check (2015), threat modeling manifesto (2020)
    - ***this dependency check is a flagship tool from OWASP***
    - Threat Modeling Manifesto is really the mark of next-gen stuff

2022, Security testing is integrated into GitHub directly

AppSec is nearly in the highest demand for anything in our industry


## HTTP/S & passwords

- 1994—combination of transmission and security together
- this is where CAs come in (cert authority) they validate the identity of who is sending, moving stuff around
    - because the public key can be hijacked by people
- 1990s—TLS 1.0
- 2005, 2006—TLS 1.1, TLS 1.2
- SSL Labs (Ivan?) this guy wanted to learn TLS at the “bit level”
    - SSLLabs started in 2009
    - so with SSLLabs we could now see our servers’ security and how well we had tuned our TLSSSL security
- Chrome starts pre-loading TLS/SSL
- Firesheep comes out (hijacking Gmail?)
- 2018—TLS 1.3 this is a major update to the protocol and helps improve so much stuff
- 2021—PKI consortium was formed
    - this is where HTTPS starts being built as default
    - and now Safari will actually check if “https” is live first, even when a user types in “http”

_So, in a little over 10-20 years we’ve gone from security being a simple “hand wave” from an engineer to a leading industry force that is being put forth as default in applications to protect individual people and companies from all kinds of bad stuff._

Chrome 90 in 2021 defaults to HTTPS

Check your website with SSLLabs online grading tool

## Password History

- MIT’s CTSS in 1961, first password system being built by hand
- then we see crackers and hacks being used against it, lol
    - we’re talking privilege escalation: printing out the master password list for a PhD student to maintain their admin access to a system they had already been maintaining
- 1970s—we start seeing password salting, etc. for some advanced crypto
- Alan Share (sp?) printing out root level password files…and then we didn’t fix that until 1980s
- 1991—MD5
    - btw, big companies are rolling their own MD5 and it’s *********bad*********
- 1997—L0phtcrack
    - today’s tool is Hashcat…but it came from L0phtcrack
- Bcrypt came around
    - it has a 72-bit limit, though
- 2007—PHP has built in password utilities
- 2015—Argon2 wins a crypto contest
- 2019—this is where a lot of what we use still sits

_In a little over 50 years we went from virtually no cryptographical security to now having best cryptographic algorithms natively supported in some of the most popular programs on the web._