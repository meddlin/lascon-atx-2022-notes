# Hacking and Defending APIs - Red and Blue Make Purple

Talk w/ Scott over lunch

multi-tiered approach

- AppSec really doesn’t need to involved containers, cloud-ops, etc.
    - AppSec → application
    - Jenkins, GitHub Actions, build servers
    - containers and deployment (the running prod servers)
    - AWS and larger infrastructure security

Why attack APIs?

- APIs are simple and “easy”
- when you do them for real they get a lot more complicated, though
    - WAF, web app, API gateway, API endpoints, etc.
- the venn diagram of AppSec vs API Sec means you could be missing a lot

It’s all about the data

- APIs are the pipes for that data (heard of: data is the new oil?)
- why SQL inject when I could just make a REST call?
- browsers are pretty good and hardned, but now we have to put that similar level of hardening to the APIs


3 pillars

- API security posture
- API runtime security
- API security testing
- _this is mostly DAST testing, because SAST already has your source code covered_


## Attacking APIs

Recon

- finding APIs to attack
- passive recon
    - not sending packets to the target
    - think of your OSINT resources
    - or your “how to use our API” docs that so emany people have
    - defnder
        - you can’t do much here
        - you already want to advertise your API anyway
- active recon
    - attacker
        - initial traffic looks harmless
        - look at: robots.txt, devtools, memory/performance, etc.
    - defender
        - this looks like normal noise
        - for SPAs, DevTools are just a fact of life
        - posture: understand the scary parts of your API
        - runtime: discover
        - testing: proactive

Discovery

- attacker
    - you’re gonna burn cycles learning how to talk to the thing
    - Swagger file?
    - is there an API client? proxy it to find the documentation for how the client is talking to the API since it isn’t documented well
- defender
    - look for unclever user agents
        - generally curl isn’t on a phone
    - lots and lots of failed requests (someone is poking)
    - posture: no what/which your APIs are
    - runtime: discover the “Discovery” things

_Discovery seems easy but can be a time sink_

Active Attacks

- Getting malicious
- BOLA (broken object level authorization)
    - a user using someone else’s token to get secured assets
    - this is checking a token is valid, rather than valid and correct
    - attacker
        - try user1 and user2
        - change IDs
        - time to respond
        - length of response?
    - defense
        - you need really deep inspection
        - WAF will generally fail
        - shaped like a legit request with IDs swapped
        - likely going to find lots of Auth-Z failures looking for BOLA

- Broken User Authentication
  - this is being able to “login to an API”
  - Attacker
      - look for no anti-automation
      - password spraying
      - APis are made to respond quickly…hijack that
      - Base-64 “protections”
      - JWT is like a drawer of knives in a dark room…lots of room for big mistakes
          - it’s like the broken TLS days, lol
          - jwt_tool
          - cracking JWT secrets
  - Defender
      - generally these attacks are really noisy
      - “JWT Best Practices RFC”
      - consider rmeovign Auth-N from the API
      - Ex: GitHub just removed AuthN from their API because they saw so much noise spin up every time they started their API in the wild

- Excessive Data Exposure
  - this is a hard one
  - sending more data than necessary from the database
  - attacker
      - mobile apps are great…because you’re generally not expecting a computer to be talking to your mobile app
      - profile pages
      - linked users
      - internal metadata
      - you have to read the data and understand the data responses though
  - defender
      - single requests attacks…so _very_ hard to identify
      - SAST can help find some of these “toJSON” problems
      - don’t rely on clients filtering data
      - separate data objects for app and API

- Lack of Resource & Rate Limiting
  - no limits on calls, lol
  - attacker
      - if you can add items…add 1000s of items…and then ask for a list
      - denial of API use (client)
      - play with origination IPs
          - can you forge the IP packet header info?
      - are rate limits set too high?
  - defender
      - requests will look normal but response will be BIG
      - unsusual requests on headers, encoding, etc.
      - app observability will show usage spikes
      - many bypass methods stand out from normal traffic

- Broken Function Level Authorization
  - failure to restrict access by group, role
  - attacker
      - focus on APIs with multiple roles/groups
      - read the docs…and then ignore the “suggested” uses
          - do they accept git? ok, use it on DELETE requests
      - play with headers, etc.
  - defender
      - anything in API with 2 or more roles?
      - calls to unsupported methods?
      - clients switching roles in short set of time??
      - failures for guest admin or “backplane-y” paths

- Mass Assignment
  - why not accept more data?
  - taking data in from a request, and sending it to the DB…so an attacker could throw in a bunch of extra stuff
  - attacker
      - most APIs will ignore all the “guesses”
      - look for request/response differences
      - erorr messages can be fun and give info
      - fuzzing can help
      - if you can combine this one with other stuff…_that’s a good time!_
  - defender
      - expecting 5 elements and you get 7? that’s obvious
      - will see more failed requests

- Security Misconfiguration
  - these are infrastructure style stuff
  - recon and discovery can help find this stuff
  - attacker
      - make bad requests and look for errors
      - try to determine which framework they’re using
          - can you turn on debug?
      - intermediate devices?
          - WAF, API gateway?
      - things with X-Remote-Addr can be helpful
  - defender
      - basic network vuln scans
      - increase in malformed requests or errors

- Injection
  - treat data like code!
  - attacker
      - place injection strings into tokens, api keys, headers, etc.
      - recon, discovery can help
  - defender
      - WAFs aren’t bad at helping here
      - overly trusting east/west calls (API to API)
          - north/south would be going to the DB
          - APIs are generally trusted…and therefore can be exploited

- Improper Assets Management
    - know what you have
    - attacker
        - undocumented APIs?
        - if an API has v2?…try v1!
        - was your pentesting fun and easy? they likley don’t have an inventory
    - defender
        - API gateways can help
        - public vs internal APIs
        - solid posture management goes a long way against this
- Insufficient Logging & Monitoring
    - change guesses to decisions with data
    - attacker
        - fuzzing doesn’t always alert who it should
        - so try everything…even stuff that makes literal no sense
    - defender
        - no attacks are seen/noticed
        - unplanned downtime or resource consumption
        - validate your logging (_be rude to it!_)

Bonus Material

- Fuzzing
    - values to the extreme
    - throw random crap
    - negative numbers…play type games
    - non-native (non-American) characters
    - target fuzzing strings
    - response code, response size
    - defender
        - lots of requests form a single client over a short period of time!!!
        - fuzzing is SUPER noisy
- Structural vs Data Attacks
    - swapping data (data attack)
        - QA tools, Postman, etc.
    - being crazy (structural attack)
        - 32MB XML document in broken pieces of the API
        - multiple of the same XML text just submitted
        - non-printing chars
        - take out portions of the data structure
        - _think of what you can do manually crafting requests_
        - most “normal” tools want to do relatively “normal” things even with responses
- GraphQL
    - introspection is now available—you could potentially tell an attacker what data is available
    - GraphQL is a query language…clients define the data they want

## Conclusion

if you already know how to test web apps, you’re way ahead for testing APIs

Check out OWASP’s API Security Tools cheat sheet

- [https://owasp.org/www-community/api_security_tools](https://owasp.org/www-community/api_security_tools)