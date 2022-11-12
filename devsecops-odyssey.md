# Close Encounters of the Vulnerable Kind - A DevSecOps Odyssey

Pranshu Bajpai
- twitter: amirootyet
- linkedin: pranshubajpai

---

About

- basic CI/CD has no security built in
- a lot of it builds for functinoality, but no security (this is when security is sitting at the end of the pipeline)
    - this way security is seen as an impediment to business, rather than an enabler
- enter DevSecOps
    - pre-commit hooks, not waiting until the end to tell developers what they need to know
    - SCA, SAST, etc.


## Common Security Risks

- dependency management
    - businesses asked: “wehre do we use log4j and are we vulnerable?”
    - it was hard, unless you’re running SBOM or SCA really well
- Ex: “so which of our apps use log4j?”
- what libraries are you bringing in?
- OWASP Dep Checker, debricked
    - these should be telling you:
        - what libraries
        - what versions
        - what is vulnerable

- Static Analysis (SAST)
    - white box test
    - beware of false positives and alert fatigue!
    - it’s a good first pass, but not some silver bullet
    - false negatives exist…which highlight the need for security training
    - bandit, brakeman
        - these are some open-source ones
    - enterprise-grade SAST solutions
        - CodeQL (GitHub)

- DAST
    - gray box testing
    - able to detect deployment related risks
    - may require complex configuration
    - false negatives on blind and/or async bugs
    - tools
        - Burp Suite
        - OWASP ZAP

- IaC Security
    - IaC = infra as code
    - create and maintain secure infra
    - secure configuration of provisioned infra
    - secure deployment of application within infra
    - attack surfaces massively increase
        - especially around container-based environments

- Secrets Management
    - secrets are necessary for authentication
    - secrets can be exposed throughout the pipeline
    - exposure can be difficult to detect since secrets come in all shapes, sizes, forms
    - watch for:
        - basic key hygiene
        - don’t put sensitive stuff in console
        - use Key Vaults and reference strings
        - tools sometimes aren’t tuned properly to catch these secrets, due to a lot of this relying on regex and pattern matching
    - tools
        - gitleaks
        - talisman
        - _try to integrate these into pre-commit hooks_

- Build Systems
    - these are _**trusted**_ systems
    - epehemeral vs persistent build systems
    - risk of vulnerable 3rd party extensions
    - importance of patch management and hardening
    - least privileges in build environments
    - example
        - SolarWinds attack scenario
        - we all focused on sunburst (which sat on endpoints), but the “sunspot” sat on the build servers…and waited to push things to the right endpoints
        - CLI args to msbuild.exe
        - the hack waited to detect for the known vulnerability to be built in the CI/CD pipeline (build server) and exploited appropriately
    - tools
        - Jenkins (persistent)
        - GitHub Actions (ephemeral)

- Access Control
    - it’s a natural part of CI/CD
    - not everyone needs to have admin access to every piece
        - also think of people who leave the company
        - people could collect permissions over time
    - local accounts being created outside scope of policies
    - peer review all changes

- Documentation
    - encourage and incentivize teams to document
    - little documentation is better than no docs
    - do not seek perfections while documenting
    - little documentation is still better than none

- Artifact Signing
    - not many people are signing code these days
        - less than 5%
    - validation issues can occur on the backend of this
    - people want to do this, but they don’t have the right guidelines for this
    - who answers questions about which encryptions to use (elliptic curve vs RSA?)—this has to be the security team (**Please don’t use MD5 or SHA1**!)
    - _**Don’t just preach. Do.**_ **And show**.

- CI/CD pipeline
    - as you move through this pipepline, you need different gates, different controls
    - watch your access tokens…when do they expire?
    - only dependencies from specific on-prem servers (do you need this?)
        - dependency hijacking
    - typo-squatting (on names of repos, etc.)
    - any place high critical vulns can break the builds?
    - scan container-based images

- Visibility
    - build processes are automated and rapid
    - log and monitor events in SIEM systems to enable threat detection and response
    - adversairies prersis where logs are absent
    - collect metrics on vulnerability management
    - tools (vuln management tools)
        - Archery (open source)
        - Nessus
    - do you accept, mitigate, or transfer the risk
        - accept: oh well
        - mitigate: fix it
        - transfer: buy insurance, lol

## DevOps Culture

- security teams are still viewed as outside…so we gotta work against that
- When speaking with devs
    - try to first why the risks developers have before fixing them
    - you have to define the constraints of the problem
    - provide impementation details __to enable developers!_
- create and support security champions programs
    - this reduces the need for external security resources to be necessary for the business
    - remember security isn’t their full-time job, but they _are interested_


## Golden Order of Impact

- People are first
- Process
    - don’t make things so process heavy that they can’t move
- Tools
    - they fix a lot, but not everything
    - new and better ones are always coming out
        - effective
        - efficient
        - execution (fast)
    - learn to separate “fact” from “claim” in marketing speak from vendors

## Conclusion

- identify tools using a visual framework
- “DevSecOps” might need to be something else
    - this seems to artifically inject security in the middle of things, as if security isn’t or can’t be built in from the ground up