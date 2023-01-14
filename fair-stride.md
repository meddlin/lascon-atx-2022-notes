# FAIR STRIDE - Building Business Relevant Threat Models

> LASCON Recorded video: [https://www.youtube.com/watch?v=kfB98Cnkn_w](https://www.youtube.com/watch?v=kfB98Cnkn_w)

Arthur Loris, Sr. Manager of Product Security at Ping Identity

The point of this talk: “Not to predict the future, but to educate decision making.”


## Background

- these are the pieces that gave inspiration for this talk, tool
    - “How to 10X your security”, Clint Gibler
    - “How to measure anything in cybersecurity risk”—a great sorta-textbook, kind of a CISO view, it’s scoped to the whole enterprise
    - FairU

What are we doing today?

- STRIDE started by Microsoft in the early 2000s
    - it’s great for repeatability scaled at more than 2 people
    - build a diagram of your application or [thing]
    - and then identify which threats fit in the STRIDE acronym…and highlight accordingly within your diagram

## Risk Ratings

- ignoring 5000 “lows” can still have impact, so ignoring them likely isn’t a good idea

These risks are important for technical reasons

- but how do we translate those to dollar amounts…that’s what we’re focusing on today


## FAIR-Factor Analysis in Information Risk

- Note: this model is also easily found on Google
- the dotted-line is kind of a trustworthy line…based on what you have available: data, SMEs, people, etc.

### Loss magnitude

- estimate of how much money you’ll be losing
- primary loss
    - implemented on the business itself
- secondary loss
    - think: resonsible disclosure, PR campaigns
- each of these always expressed as a 90% confidence interval
    - what are you 90% confident of what the cost will be, with 5% error on either “side”. So, we’re talking ranges here.

### Loss event frequency

- important to time-box this
    - likelihood you get breached/attacked in 1 week is near 0%, but within 15 years is near 100%
- contact frequency
    - how often is an attacker making contact with your asset?
    - probability of action—the conversion of contact to threat events (ESPP application here?)


## Monte Carlo Simulation

- These simulations were developed during the Manhattan project
    - they had no historical data to rely on…so they developed Monte Carlo simulations
    - So, the reasoning is that _we_ can use these simulations
- take our simulations, and generate and simulate the “historical” data we need
    - take what we know about our company and create 1000s years of “data” on our company
- they will be bound by the upper/lower bounds of your confidence intervals

tl;dr
1. Model threats with STRIDE
2. Feed output from STRIDE into a FAIR simulation rather than CVSS score calculator
3. Use LECs to define a goal post, a baseline, and progress from one to the other

## Demo

- check the URL i took a picture of
    - these are a lot of free tools
- check here for spreadsheet: https://www.howtomeasureanything.com/cybersecurity
- this will likely look like a bunch of stuff in a spreadsheet once it’s done being calculated

- Also keep in mind, if you’re doing this…you’re likely already an organization that is doing all of the low-hanging fruit stuff
    - your assumptions could still be broken due to technology innovations
    - ex: how many years has there been a CVE that broke confidentiality of HTTPS, etc.
        - then this can drive decisions about how “protected” people, assets are on encrypted internal networks (i.e. passing creds around in plain text, but only internally)

- Then we could ask important questions:
    - what is the probability that we will lose $200k (for example) on a single application
    - and then we just count the number of years this happened
    - also, “what’s the least number of dollars we lost any given year?”
- potentially gives us loss exedance curves, too
- Remember AppSec serves business interestes and risk…so this model speaks the same language as those who invest in your applications (the business)
    - example
        - show you’re already accepting 20% risk at $$
        - can you accept 25% at $$$?
        - then we can negotiate how much risk, correlate the changes to literal dollars, and have an apples-to-apples conversation
    - This also allows certain process and technical pieces to talk to each other
        - if we know the things that need to change for a proposed process
        - and we know what technical things cost
        - then we can correlate all of that back to money with this model


How does FAIR STRIDE help?

- in multiple ways
- also burnout
    - this helps us build a picture for when things are not always on fire
    - show a productive image…and when things can be okay, or make progressive changes instead of always being reactive
- Justify investment
    - Is a vendor asking for a lot of money? —we can simulate what that investment will be and what the simulated changes will be, thus to see what could potentially be saved


Call to action

- run this now
- and then annually, every 12 months
    - lots of things will change
    - it’s going to be difficult to automate this…and things like log4shell will change it


Q/A

What is this is too heavy handed for the org?

- it’s up to who is running the simulations
- you get to control the estimations…or use a completely different roadmap if this is too much

Other threat models

- this is more strategic
- absolutely use other smaller threat models on inidividual features

Can you use EPSS with this model?

- you could augment this model via Beta distributions (a math, stats term)
- you could absolutely use EPSS data within this…just takes some time to figure it out per CVE

Yes, some room for correlation to financial analysis—just not sure where/how yet