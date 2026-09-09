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

## Non-Repudiation

**## What it is**

- Non-repudiation is a foundation of cryptography. When someone sends data to a third party, that party needs to confirm it's actually receiving the info from the claimed user — they view the signature and see it was signed by us.
- Cryptography gives us two things here: **proof of integrity** and **proof of origin**.
- **Proof of integrity** — we can verify the data is exactly what was sent. Accomplished through a hash.
- A hash is a short string of text created from the plaintext. Like a fingerprint (a string of letters and numbers), not an actual fingerprint.
- A hash is good, but it doesn't associate the data with a particular user — it can't verify who sent it.
- **Proof of origin** — a digital signature, signed with a private key. This is what tells you who sent it.

**## Why it matters**

- Adding a digital signature happens behind the scenes when you click the box to sign something. What's actually going on:
- A hashing algorithm creates a hash of the plaintext.
- The hash is encrypted with the sender's **private key**.
- The encrypted hash is sent alongside the plaintext message — that encrypted hash is the digital signature.
- The recipient uses the sender's **public key** to decrypt the signature, recovering the original hash.
- The recipient then runs the same hashing procedure on the message. If the hashes match, both integrity and origin check out.

**## What I mixed up**

- Missed the correct definitions for encrypting and decrypting. Encrypting is the process of putting something into code or cipher; decrypting is to decipher or decode it.
- Missed the importance of the private key. The sender is the only one who holds the private key, so if the public key decrypts the signature, only the matching private key could have produced it.
- Missed what non-repudiation actually is — it's the combination of both integrity and origin, not a replacement for either.

## AAA

**## What it is**

- **AAA framework** — Authentication, Authorization, and Accounting.
- **Identification** — you claim to be a particular user.
- **Authentication** — proving you really are what you say you are (you know the password).
- **Authorization** — what type of access you have.
- **Accounting** — a log of login time, data sent and received, logout time.

**## Authenticating systems**

- You may have to manage many devices, often ones you can't physically see.
- A system can't type a password, and you might not want to store one on it. So authentication is provided through a **certificate** on the device, which is usually digitally signed.
- Process for creating a certificate: an essential piece is a **certificate authority (CA)** — a device or software responsible for managing all certificates in the environment.
- Any time you want to perform an authentication, you use that certificate and verify it's digitally signed.
- A certificate authority has its own certificate, signed by a root CA.

**## Authorization models**

- Used to authorize devices to resources within the network.
- The problem: how do you create a relationship that scales for tens of thousands of users?
- You put an authorization model in between the users and the services, before they access data.
- Doing it directly doesn't scale — you'd have to manually configure it for each user/service pair.
- To scale, use an authorization model or an **abstraction** that separates the user from the info they're trying to access.

**## What I mixed up**

- Commonly mixed up identification and authentication. **Identification** is the process where a user claims an identity — maybe through an email. **Authentication** answers "can you prove it?" — with a password.