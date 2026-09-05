## Security-Controls

**## What it is**

- Threat modeling framework, six categories of threat
- Spoofing, Tampering, Repudiation, Info Disclosure, DoS, Elevation of Privilege
- You walk a system and ask "which of these six apply here"

**## Why it matters**

- Gives you a checklist so you don't just list the threats you happened to think of
- Used it on the DFDs at work — each trust boundary crossing, run the six

**## What I mixed up**

- Repudiation vs Info Disclosure — repudiation is "can't prove who did it," disclosure is "wrong person saw it"
- Kept forgetting elevation of privilege is about gaining rights, not using rights you already have

**## Examples**

- Firewall — technical + preventive (blocks the traffic before it lands)
- System logs — technical + detective (doesn't stop anything, tells you it happened)

## CIA-Triad

**## What it is**

- CIA triad = the fundamentals of IT security. Also called the AIC triad.
- **C — Confidentiality.** Stop someone from accessing confidential data.
- **I — Integrity.** The recipient receives exactly what was sent.
- **A — Availability.** Systems stay up and running.

**## Why it matters**

- Big topic is making data available but ensuring it's only available to the right person.
- **Confidentiality** — encryption. People "in the middle" can't see what's encrypted. Also access controls / permissions.
- **Integrity** — hashing. Sender makes a hash, sends data + hash. If the hashes match, the data wasn't changed. Enhanced with signatures and certificates, which identify devices/people. Non-repudiation provides proof of integrity.
- **Availability** — design systems to always be running. Fault tolerance means one can go down and another picks it up. Keep systems updated/patched.

**## What I mixed up**

- Mixed up non-repudiation and integrity. **Integrity** proves the content didn't change. **Non-repudiation** proves the sender can't later deny they sent it — irrefutable proof of who originated the data.
- Done through a digital signature.
