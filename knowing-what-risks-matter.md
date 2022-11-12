# Knowing What Risks Matter-and don't-In Your Open Source

Naomi Buckwalter, Director of Product Security

- Contrast Security
- twtter: @ineedmorecyber
- “How do we actually get better at this?”
- CVSS is likely a broken system…

Software Factory Risk Dimensions

- normal circle of software development, production
    - and devs can introduce bugs, problems
- but now other bad stuff happens with open source
    - ex: Solar Winds issue in the build systems
- and “dependency confusion” is a whole category of these problems, too

Open Source Threat Matrix

- on average it takes 4 years for a vulnerability to be discovered and fixed in open source
- only 2% of CVEs of all time have exploit code written for them
- this is why handing a list of CVEs is a heavy burden
- and CVSS scores trend high (avg. score is about ~7)

_**Yes, there is a better way!**_

Contrast has a “state of open source security report”

- based on aggregate telemetry collected by them (Java, .NET, and Node)
- Risk 1: Active and Incative Libraries
- Risk 2: Active and Inactive Library Classes
- Risk 3: Library Age
- Risk 4: Vulns in libraries
- Risk 5: licensing risk

Complexity of library counts (direct deps.)

- insights and takewaywa
    - java: avg of 125 libraries
    - top 25 libraries in 50% of applications
    - .net nearly all have <14 libraries

## Risk Layer 1 - Active and Inactive Libraries

- SCA is good, but it doesn’t tell you the full story!
- SCA tools have overreported Log4J
    - so think of the false positives
    - you could definitely have Log4j in places where it is never reached, but we freak out because of hte crazy reactions
- Log4j by the numbers
    - 50% of java applications package a vulnerable version of log4j…but very few use it (37%)
- Spring4Shell by the numbers
    - 74% of java apps package spring core
    - 71% of psring spps on Tomact
    - 85% of java spring apps package a vulnerable version

## Risk Layer 2 - Active & Inactive Library Classes

- only 31% of classes in active libraries are actually invoked
- only 10% of overall apps code is active library code
- **So most of your time should be focused on the code you wrote! because SCA is important, but actual dependencies are “it depends” for how dangerous they are**

## Risk Layer 3 - Library Age

- Old libraries don't get patched

## Risk Layer 4 - Vulns in Libraries

- look at apps with at least one CVE vs. % of active libraries with CVEs
- so, there are TONS of false positives
    - sure it’s vulnerable, but what’s the likelihood that it will actually be exploited??


### Other Factors:  CVSS vs. EPSS

- EPSS: exploit prediction scoring system
    - T*his system looks at how likely something will be exploited*
    - This is how the model is constructed — [https://www.first.org/epss/model](https://www.first.org/epss/model)
    - It’s from the same people who do CVSS
    - Check out the REST call too
    - You can also make these calls for specific CVEs
- [cvetrends.com](https://cvetrends.com/)
    - check this out
    - like “threat intel for CVEs”
    - looking at the chatter for specific CVEs
- EPSS API — check out: https://api.first.org
    - API definition: [https://www.first.org/epss/api](https://www.first.org/epss/api)
    - Here’s one example: [https://api.first.org/data/v1/epss?cve=CVE-2022-27225](https://api.first.org/data/v1/epss?cve=CVE-2022-27225)


### Log4Shell—let’s look at the specifics

- CVSS
    - 4 distinct CVEs, on avg. a 10 score
- EPSS
    - mostly 99th percentile, but provides better context for likelihood
    - see an EPSS of 0.4 or higher? go ahead and fix that
        - this equates to 40% likelihood of being exploited
    - these EPSS scores can increase over time, but they likely decrease due to other CVEs being published, etc.

## Risk Layer 5 - Licensing

- not quite security, but definitely a business risk
- Apian (sp?) recently won ~$2Bn due to wrongful use of someone using their software with copy-left licensing
- GPLv3, APLv2 (?)
- talk to legal counsel about these licenses


## Recommendations: How to fix?

- set comprehensive policies for libraries, frameworks, and licensing
    - don’t just throw things over the wall
    - give them data
    - and share your reasoning
- establish continuous observability
- use all the data available to you for making risk-based decisions
- embed controls in CI/CD processes