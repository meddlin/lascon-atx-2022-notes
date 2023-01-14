# DevSecOps Playbook

> LASCON Recorded video: [https://www.youtube.com/watch?v=4pIBUcwXEzQ](https://www.youtube.com/watch?v=4pIBUcwXEzQ)

Paul McCartey
- SecureStack—Austrailian company (startup) Queensland
- [SecureStack—Austrailian company (startup) Queensland](https://github.com/6mile/DevSecOps-Playbook)

- he’s been at this 31 years
- he originally was a Unix admin, and then into Linux firewalls and security space
- he started working for large organizations, and then has also worked in startups/small organizations
    - one of those being Blue Cross Blue Shield, and on-call for deployments driven by DBAs
- _Point being…his career sounds a lot like the “boring, feeling bad stuff” that I’ve been trying to avoid. So, it’s not all bad._

---

👉 _**Want to skip to the playbook?**_ -- [https://github.com/6mile/DevSecOps-Playbook](https://github.com/6mile/DevSecOps-Playbook)

## DevOps, DevSecOps — probably not the right names, but we’ll use it

- this playbook started as:
    - a list of tasks that has grown over time


## Think about what’s at stake

- startup: surviving
- corporation: compliance


### Evidence of problem

- SWEs have a lto of access to the cloud
- infosec teams not evolved to join DevOps
- we are deploying at an increasing rate & engineers often skip existing security steps under duress
- mindset that short lived things don’t need securing


DevOps is allowing Paul’s team to deploy, to prod, 80 times per day
- This is crazy good metric for a startup to be adhering to

## Software Engineer Priorities

- features
- speed
- NOT security

InfoSec didn’t move towards the center like Ops and Devs did during the DevOps Revolution

- So we’re still bolting security on \[to the end of processes\]

### Evidence of problem

- infosec teams are still focused on questioneaires
- still focused on the edge, not aligned with cloud strategy
- secuirty tooling os often sioled
    - InfoSec tools will buy a tool, but then won’t share it with engineers
    - So, software devs are running CI/CD security tools (no infosec)
    - Infosec is running security tools (no devs)
- as a results, companies have “right sized” infosec teams
    - these teams have been minimized to cost as little as possible (wrong motivation)
- devsecops is opportunity to bring InfoSEc into our world

**Operations has been devalued in the “cloud-native” world, which leads to the mess we’re in**

_You really need to embed the secuirty operations inside the software dev teams_
- because you can’t just say “DevSecOps” and then start solving problems


## Solution

Easy, step-by-step implementation guide with taskss for any role, at any organziation, prioritized by value & sorted by difficulty

- simple checklist style document
- focus on DevSecOps and collaboration
- multiple future compilance requriements, so needed a “matrix” of compliance mappings
- way to “pull” InfoSec and Ops to the playbook

- How do i bring InfoSec into this?
- How do I make AppSEc a first class citizen of InfoSec?
    - often AppSec isn’t entirely in SWE teams or InfoSEc teams
- address secuirity questionaires ahead of time
- increase CI/CD abilities….

Inspiration for this

- MVSP minimum viable secure product
- NIST, Secure software development framework
    - this one might not be approachable by “doers”, devs, etc.
- OWASP ASVS
- DSOMM (DevSecOps maturity model)
    - this one is also written for more managerial audience

_Check out OWASP’s AppSec “quick start guide” for how to build an AppSec program_

Side note: Check out [OWASP’s AppSec “quick start guide”](https://owasp.org/www-pdf-archive/OWASP_Quick_Start_Guide.pdf) for how to build an AppSec program - [https://owasp.org/www-pdf-archive/OWASP_Quick_Start_Guide.pdf](https://owasp.org/www-pdf-archive/OWASP_Quick_Start_Guide.pdf)


What is DevSecOps?

- automates the integration of secuity of every step in software development…
- Vendors, Gartner doens’t get to define DevSecOps…your organization does

Share code

- it isn’t just \[`insert team member’s`\] code, it’s the _team’s_ code

A reminder

- I’m trying to help my teams working more collaboratively. I am not trying to build an AppSec program


Some key points:
- Identify
  - what applications?
  - who owns them?
      - literally talk to them
  - draw a map
  - this is that idea of champions
- Priorities
  - find a way to evangelize and business values alignment
- Collaborate
  - who to collaborate with? and build those relationships
  - build collateral with them too
      - this is like building templates, scripts, etc. to help other teams
- Quantify
  - what does success look like?
  - find ways to know what you should be hitting
  - what are the minimum things that we need? (like KPIs)


## SDLC Map

- break up the tasks
- lay the tasks out across the SDLC
- color code who owns the tasks
- think: Security Domains…because security concerns are generally gray areas

## Certain organizations don’t have “security people” though

- because you have all this stuff…but no “security people” to do it
- so we need this to be malleable (one size does not fit all)
- for startups
    - no SMEs
    - mostly driven by developers
        - this means sprawl
    - often no real infrastructure experience at all
- how do we compensate?
    - break the tasks into “domains” of owernship
    - add a prioritization system (what should yo udo first)
    - define how difficult stuff is


## The Playbook

[https://github.com/6mile/DevSecOps-Playbook](https://github.com/6mile/DevSecOps-Playbook)

- Domains
    - dev environment
    - source code management
    - continuous improvments and automation
    - deployment
    - organizational techniques
        - maybe a bad name
    - and…? (this last one is in the repo)

- Priority 1 is what you should do right away, and then it’s in numerical order
- Lens for difficulty
    - based on his personal “lens”
    - you can fork the repo
    - ***how long and how many people it took to implement that task***
    - Ex: local static analysis
        - different stuff should be at different places
        - not well-suited for CI/CD pipelines…should be ran with specific rulesets…and because it’s not “boolean” this makes it a harder fit for CI/CD
        - it should be ran on as many dev laptops as possible


- Check out the ISM, Australian document, written by their NSA-equivalent, it’s pretty easy to read (supposedly). This document is referened in the playbook.

- organizational techniques
    - bug bounty, soveriegnety…
    - these things are higher-level decisions that require people, strategy, etc. and are thus harder to make these things reality

- deployment
    - encrypt traffic—it’s at multiple places
- the point of these things is that **you should do it**
    - not necessarily, that it needs to be done specifically or to some defined manner of grading


**If you’re interested in helping out with it—go for it! Help out with the code**

- they’re looking for a static app to allow for filtering, collapse sections, etc.
- eastside-mccarty on Twitter