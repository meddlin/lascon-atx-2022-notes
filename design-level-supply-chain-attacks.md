# Design-Level Supply Chain Attacks

“Software Supply Chain Security Threats at the Design”—the overlooked risk

Moshi Zioni — VP of Security Rsearch at Apiiro

- Apiiro
- twitter: dalmoz_

_**This talk’s contents, topics can fit well for starting some threat modeling discussions**_

Usually we have

- source threats
- build threats
- runtime threats
- dependency threats

SLSA—framework (or a group?) look this up

- it’s mentioned in this talk, and others mentioned it in conversations after other talks
- is this from Google?

Design threats!

- these are before “source threats”
- these could introduce global implications for the application because of where they are in the design process
- 3 types
    - environmental constraints
    - compliance & law
    - malicious influence

Environmental constraints

- ex: hardware, IoT security
    - Sonoff is a wifi switch, like a light switch, or anything similar
        - just a few bucks ($)
        - one chip (SoC, ESP8266), and some supporting electronics
    - ESP82-family is clever, developed around 2013, shares a lot with Arduino—_it accepts Python_
    - it has 2 modes: encrypted + plain text
    - TLS was disabled by default on this board, because its support was experimental, and there was a serious hardware memory limitation
        - to the point that if using SSL, then no other options could really be enabled on the chip
    - Sonoff Basic R3—a completely redesigned board
        - much more memory this time—to give developers more room for memory and comply with SSL
    - due to hardware not being fixable (unless expensive FPGA)…this makes design constraints seriously important

Compliance & Law

- standards, regulations dictating some of the security practices (or can)
    - these security practices could be outdated due to technology advancements that happen by the time regulations become finalized
- ex: Netscape
    - SSL was invented by Netscape employees
    - Netscape had to support public key cryptography
    - “supports International security”—(from their compliance disclosure) this means, this type of cryptographic scheme needed to comply with US law, and won’t be abel to tranfer the algorithm for RSA unless you’re downgrading it…to not be considered an ammunition/munitions
    - look at “crypto wars” for more of the surrounding story about this
        - such as: tatoos and shirts being considered “weapons” due to the algorithm being written on those items
    - so the regulation, was supposed to say this [item] can’t be shipped outside the US…but Netscape could clearly be “shipped” anywhere…*hence the problem*
- Freak Attack, circa 2015
    - for servers who communicate over RSA
    - this enabled servers to be able to export keys, etc.
    - exploitable on about 10% of the internet

Malicious Influence

- influence decision-making process and personnel to gain an unfair advantage
    - could be a strong lobbying group

- the Dual_EC_DRBG
    - dual elliptic curve deterministic random bit generator
    - there were a couple “bugs” in this algorithm/cryptographic scheme
- this Dual_EC_DRBG was baked into NIST
    - NIST affected more than just the US
    - it was also one of only 2 crypto schemes to be included in FIPS 140-2 security requirements
- OpenSSL wanted to be compliant with FIPS 140-2
- RSA was also trying to use this algorithm as a default

- in 2006, 2007, there was some uproar about this algorithm…researchers saw it had a serious weakness
    - mathematic research about how effective the algorithm actually was (concerns about there being a backdoor possibility)
- there was a notice given:
    - they weren’t fixing the bug
    - there was information given to fix the code for others’ own implementations…but then they wouldn’t be FIPS compliant
- also, this was all pre-Snowden era
    - so there are claims that perhaps the NSA was trying to coerce RSA to implement this Dual_EC algorithm
    - _**hence, the problem for how many downstream users of this there would be**_
    - The Snowden leaks produced that many parties knew of these bugs ahead of time.
    - RSA was holding the market on corporate crypto implementations
- So, there are collusion concerns: collusion between the NSA and RSA…thus, having world-wide repurcussions (potentially, allegedly)

- How much time did it take to rectify all of this?
    - the original algo drafts were published in 2004
    - this story, and the side effects, were divulged in 2013
    - _so, nearly a decade between it all_

- Ex: outdated React version on a website
    - perhaps the React update takes estimated 6 months
    - this could be considered too long for the business
    - and so, potential risks are introduced due to the motivation to not get caught into that