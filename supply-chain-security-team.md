# Supply Chain Security Team

> LASCON Recorded video: [https://www.youtube.com/watch?v=LC74RsWyBoM](https://www.youtube.com/watch?v=LC74RsWyBoM)

“everyone is talking about supply chain security, but no one is actually practicing it”

- at RSA there was a supply chain talk in every block of talks
- it’s all SBOMS and supply chain, but nothing about how to produce an SBOM either

there is an SBOM specification?

- some vendors actually take an inventory of the software, and export it…but don’t actually make it a real SBOM

4 pillars

- open source, 3rd party libraries
- third-party software
    - OSS is a big piece, but this is also purchased, close-source stuff
- suppliers
    - ex: Target breach was related to their HVAC vendor?
- software factory
    - this is your actual SDLC, CI/CD, build and dev tools, etc.


Responsibilities

- what does your team do on a daily basis?
    - maintain the actual SBOM, and generate them for external distribution
    - review dependencies for known vulnerabilities
        - stay up to date with what’s happening, current vulns, any log4j-style events?
    - define your leading practices for using OSS libraries

Maintain supplier SBOMs

- he’s been asking suppliers for SBOMs for over a year…and received virtually none
- some software suppliers have even tried to avoid providing SBOMs…even with the federal executive order being given from the US gov’t
- they also create RACI diagrams at this point

Software Factory

- focus on hardening this “software factory”
- where are secrets stored? what build tools are used? can you dump out your “pipeline.yml” file(s)?
- container security is _related_ here…but supply chain security “team” isn’t fully responsible for this
    - but _we do care about_ the open-source packages that are involved in these container images


More than just SBOMs

- team size
    - this is a full team, not some single AppSec person who has 10% of their time going towards SBOMs or supply chain stuff
    - they have 3 people
    - so if you have _some person on AppSec_ who is trying to commit 5% of their time to this, then they likely aren’t going to get very far
- where did they start?
    - 3rd party assessments
        - browsers + extensions, Slack plugins
    - OSS-library analysis
    - cloud configuration reviews
    - defining supply chain security roadmap(s)…beware this will get re-defined multiple times
- key observations
    - SBOMs are _really_ hard
        - at what level?—file out of version control, before/after compilation
        - ex: there’s an OWASP SBOM tool for this?!
        - _There’s basically no tools available for this. Or some will only do SPDX. What is CycloneDX?_
        - And then many people want you to put this in source control…so, how do you handle when development changes things?—How do you get the updated version of the new-to-be-generated SBOM
        - more on the level of SBOM—if you can produce it on 1 repo, great!—but how do you do this across multiple repos, 60 containers, a build system, and then also where do you store this? how do you publish it?
        - you really need a system to visualize these. Putting it in git is fine, but that can seriously be difficult to read, visualize, and compare against vulns or other pieces
    - SCA alone is not enough
        - it’s not enough confidence to identify libraries
        - they used: OSA + GitHub Codesearch + SBOMs for Apache-Commons-Text
            - cs.github.com
        - they had a _lot of good results_ from integrating directly with GitHub
        - pipeline scans
            - you could do this
            - but scanning in GitHub is great, so why do it a second time?
            - pipelines are cool, but how many times are you scanning things redundantly for the same stuff?
        - also, vulnerability management is virtually non-existent in this space
        - *when multiple tools, reports, or techniques start giving you the same results…then we can start trusting that data*
    - Securing the software factory
        - there are no true leading practices
        - PATs (personal access token) are troublesome
            - are these managed? by who? how? is it in a secrets vault?
            - if someone gets one of these, they are automatically authenticated, and sometimes without the possibility of using MFA via these
        - API security is its own animal
    - Metrics are hard
        - they’re already hard in AppSec
        - more difficult in supply chain
        - no tools again
    - Supply chain is not AppSec
        - there are too many concerns, takes too much time
        - they are related…but not the same thing
        - supply chain is more broad, and less tactical than AppSec (AppSec is more specialized)
        - maybe?—- SCS + AppSec == DevSecOps (possibly?)


Lessons Learned

- following least resistance isn’t always “shift left”
    - there are a lot of good ideas (dependabot in PRs)…but they don’t always lead to a better place
    - does your org live and die in their issue trackers or Jira? then living in GitHub may require more code actually—_so be careful_ that what seems good might be counter-intuitive
- What is easy for AppSec, supply chain…isn’t always good for developers
- Build partnerships, not enemies
    - do things that are good, not for the sake of doing things
- Strive for progress over perfection
    - don’t solve all of the problem all at once

- properly define what suply chain is for your org
    - there’s a lot of gray area here—is a particular issue supply chain or AppSec?
    - you won’t get things right the first time
    - evaluate your 3rd parties and the relationships there

- measure things, and improve them
    - let your data tell you which security problems to tackle next
        - repos with lost admin accounts?
    - don’t go solve problems, _and then define metrics_. No. _Define metrics_, and then let that drive problems to be solved.
    - use this to determine the story you want to tell
        - software factory compromise?—ok, what numbers drive that

- start now…and you’ll be ahead of others
    - most orgs, teams, etc. are doing _**incredibly little**_ in this space
    - no better time than now
    - no barrier to entry

What can we do?

- try some of this stuff
- if SBOMs are hard—great, try it. see where you get tripped up.
- sometimes trying these things tells you more about where you are than you knew before
    - can you define your OSS-packags? Great, now measure how long that took you to do it. That’s a good metric.
- Prevent egress
    - where is your software factory pulling images and packages from? Are they pulling from somewhere onsite or the internet?

Future?

- CIS put out a great benchmark
- there are no tools—can you help?
- can SBOMs replace your SCA practices?—that’s an interesting question