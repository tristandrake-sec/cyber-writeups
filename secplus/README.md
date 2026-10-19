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

## Gap Anslysis

**## What it is**

- A gap analysis is a study of where we are vs where we want to be. We study this to know exactly what security will be needed in the future.
- Before starting a gap analysis it's important to have a **baseline** — gives you something to work toward, a goal.
- Examples of baselines: NIST Special Publication 800-171 Revision 2, ISO/IEC 27001.

**## What a baseline consists of**

- An analysis of employees — experience, training, and knowledge of security policies and procedures.
- An evaluation of the existing IT system and how it correlates with the current IT system.

**## The analysis**

- Begins with a comparison of the existing systems against the current system, identifying weaknesses and how to compensate for them.
- Make a detailed analysis of broad security systems and break them down into smaller pieces.
- Once you've gathered info across all locations, produce a final document summarizing everything discovered.
- Start with a comparison of the baseline objectives to where you want to be, and how you'll get there.
- Create a final **gap analysis report** — a formal description of the baseline, what's required, and how you'll achieve the goal.

**## What I mixed up**

- Missed the reasoning for why a baseline is needed before starting the analysis. A baseline is necessary to display the starting point and the distance between the starting point and the goal.

## Zero-Trust

**## What it is**

- In many networks, once you're through the firewall it's pretty open — no checks or balances. This lets both authorized and unauthorized/malicious software move freely.
- **Zero trust** means you have to authenticate any time you access a particular resource. Applies to every device, user, and process.
- Nothing is trusted. Adds multi-factor authentication, encryption, security policies, additional firewalls, monitoring, etc.

**## Planes of operation**

- One way to implement zero trust is to break security devices down into smaller individual components, or separate planes of function. Applies to physical, virtual, and cloud components.
- **Data plane** — the part of the device actually performing the security process. Processes frames, packets, network data. Processing, forwarding, trunking, encrypting, NAT.
- **Control plane** — manages all the actions in the data plane. Policies, rules, determining how packets should be forwarded, routing tables, session tables, NAT tables.
- Both can be implemented virtually or through hardware.

**## Controlling access**

- **Adaptive identity** — examine the identity of an individual and apply security controls based on the user plus outside info beyond the authentication itself. Look at the source; risk indicators include physical location, type of connection, IP address, relationship to the organization.
- Another approach is to **limit possible entry points**.
- Once the info is collected you create **policy-driven access control** — examines all these individual data points, then decides what authentication should be required.
- **Security zones** — qualify a user by understanding where they're connecting from. Looks at the overall path: where you're coming from and where you're going. Set up as trusted/untrusted, internal/external, VPNs, or splitting departments. Zones can automatically block a connection from a certain zone, or grant trusted access through others.

**## Policy enforcement**

- **Policy Enforcement Point (PEP)** — any subject or system is subjected to evaluation by the PEP. Think of it as a gatekeeper, or multiple devices working together to provide identification. It doesn't make the decision — it gathers the info and passes it to the policy decision point.
- **Policy Decision Point** — responsible for examining the authentication and deciding whether it should be allowed on the network.
- **Policy Engine** — looks at all requests coming through, compares them to a set of policies, and decides granted or denied.
- **Policy Administrator** — takes that decision and provides it to the PEP.

**## What I mixed up**

- Missed that the PEP comes first and gathers info, then passes it to the PDP. The PDP has two parts: the **policy engine**, which compares the request against policies and returns an allow or deny, and the **policy administrator**, which relays that allow/deny back to the PEP.

## Physical Security

**## Barricades / bollards**

- Prevent access, channel people through a specific access point, act as a security notice.
- Often installed as concrete, but can also be water around a building forcing people to cross a bridge to reach the facility.

**## Access control vestibule**

- A room you must pass through to gain access to the rest of the building. May have higher security where you badge in.
- Can be configured so all doors are unlocked, all locked, or one door open while the rest are locked.
- Designed to control access through a particular area, whether for a single person or a group.

**## Fences**

- Build a perimeter. Obvious, but provides a way to deny access.
- May be transparent or opaque.
- Need to be robust and prevent climbing — razor wire, or a very tall fence.

**## Video surveillance**

- CCTV (closed circuit television).
- May have motion detection and can provide detailed object detection.
- Most setups have multiple cameras sending data back to one storage point.

**## Security guards**

- Provide physical security, validate whether people are allowed in.
- Usually work in twos or more.
- **Access badge** — identification proving you have access, provides detail about yourself.

**## Lighting**

- Illuminating a dark area prevents access. Attackers avoid light, and it's easier to see when lit.

**## Sensors**

- **Infrared** — detects infrared radiation in both light and dark.
- **Pressure** — notices a change in force.
- **Microwave** — for a very wide area, may be more efficient.
- **Ultrasonic** — sends signals and looks for reflected sound waves. Useful in a parking lot.

**## What I mixed up**

- Missed being able to identify the difference between a deterrent and a preventive physical control. A **deterrent** is a psychological measure used to discourage malicious behavior. A **preventive** control is a physical barrier designed to stop unauthorized access.

## Deception and Disruption

**## Honeypot**

- Attracts attackers and traps them there. Lets you view the security techniques they're trying to use against you.
- In most cases the attacker is an automated process, so you get to see what process it is and what machines it's targeting.
- Honeypots create a virtual world to explore. Constant battle between building believable virtual worlds and attackers trying to discern whether they're on a real system or stuck in a honeypot. More realistic is better.

**## Honeynet**

- A combination of multiple honeypots. May consist of servers, routers, switches, and firewalls rather than a single device.
- Makes a much more believable environment and keeps attackers busy.

**## Honeyfiles**

- Files with fake info, or that appear to be very important or contain sensitive info.
- In normal production, no one should have access to the honeyfiles — so any access is a signal.

**## Honeytokens**

- Traceable data added to a honeynet. If the data is copied, you know where it came from.
- Might use fake email addresses or API tokens.

**## What I mixed up**

- Missed the difference between a honeyfile and a honeytoken. A **honeyfile** is a file containing fake sensitive info. A **honeytoken** is traceable data where the owner of the honeynet can track where the data is copied to.

## Change Management

**## What it is**

- When making a change to an application or OS, the scope on your own machine is a single computer. In the corporate world it can be thousands.
- Changes include firewall modifications, software updates, patching an application, or modifying switch ports.
- One of the most common risks is in the enterprise. It's important to have a formal process for making changes — these are often overlooked or ignored.
- Have clear policies (frequency, duration). Hard to manage without a formal change control process. These processes exist to avoid downtime, confusion, and mistakes.

**## A typical change process**

- Complete a request form
- Determine the purpose of the change
- Identify the scope
- Schedule a date and time
- Determine affected systems and impact
- Analyze the risk associated with the change
- Get approval from the change control board
- Get end-user acceptance after the change is complete

**## Roles**

- **Owner** — usually the one wanting the change. Doesn't control the change control process or make the change itself; they manage it, and test it once complete.
    - Example: address labels need upgrading. Shipping and receiving owns it; IT handles the actual change.
- **Stakeholders** — those impacted by the change. They want input/control over when it happens. A single change can affect one person or many.

**## Risk**

- Every change has a different impact on the company. Assess by determining risk value — risks can be minor or far-reaching.
- The fix might not fix anything, might break something else, cause an OS to fail, or corrupt data.
- Also determine the risk of _not_ making the fix.

**## Testing**

- Do testing before implementing, using a **sandbox** — a technological safe space with no connection to production or the real world.
- Inside the sandbox you can duplicate the system, make the change, and see the effect.
- Good time to test the **backout plan** — if something goes wrong, you revert to a previous version. Not as easy as it sounds; always good to have a full, complete backup.

**## Maintenance window**

- The maintenance window is when the change occurs. During non-working hours is best.

**## Why it matters**

- Change management is critical. Must be well documented so anyone can view it, and reflected in the standards.

**## What I mixed up**

- Mixed up three roles. The **change control board** authorizes the change, the **owner** manages it and tests when completed (doesn't implement it), and the **IT / technical team** actually implements it.

## Technical Change Management

**## What it is**

- When making changes to tens, hundreds, or thousands of devices, a simple update can get complex.
- The change control process is concerned with _what_ needs to be changed; the technician actually performs the changes.

**## Allow / deny lists**

- A list of applications that are allowed or not allowed in your environment.
- Add malicious applications to a **deny list**, or add only the necessary applications to an **allow list**.
- A deny list is more flexible — you can run any application not on it.

**## Scope**

- When a change is submitted, it has a very specific scope: only make changes to what's listed in the documentation.
- Can't change other applications, but there are times you have to expand the scope to complete the primary goal.
- This is why it's important to have very specific, documented change control.

**## Downtime**

- Services are unavailable during the change window. That's why changes happen during non-work hours if possible.
- If no downtime is allowed, switch to a secondary system, make the change, then switch back to the primary once complete. Lets you monitor the change — if anything goes wrong, you stay on the secondary.
- Make sure everyone is aware of the downtime.

**## Restarts**

- Common to require a restart/reboot. Also helps confirm whether the system can recover from something like a power outage.
- Stopping and restarting just a service may only take seconds or minutes.
- For applications, users may need to fully log out and restart with the new version.

**## Legacy applications**

- Usually run for a very long time and may no longer be supported by the developer.
- Usually no changes are made because of the unknowns. Understand it through documentation and bring it into the normal cycle — but it may be quirky.

**## Dependencies**

- You may have to change one application or service before another, or it won't work unless a secondary service/application is installed.
- May require multiple updates to work, and the dependency may not be on the same system.

**## Documentation**

- The only constant is change, so documentation is important to keep up with what's been implemented. May include updating diagrams, policies, and procedures.

**## Version control**

- Dealing with change control also means dealing with version control — a way to track all versions installed.
- Documents changes to router configs, Windows OS patches, application registry entries. Not always straightforward.

**## What I mixed up**

- Mixed up flexibility vs security with allow/deny lists. The **allow list** gives more security, since only applications on it can run. The **deny list** gives more flexibility, since you can run any application not on it.

## Key Exchange

**## The problem**

- How do you share the encryption key between two people without transferring it insecurely, like over the internet?

**## Out-of-band exchange**

- Not sending the key over the internet — telephone or in person instead.

**## In-band exchange**

- The key goes over the network, but you protect it with additional encryption.
- Use asymmetric encryption to deliver a symmetric key.

**## Session keys**

- Used on a temporary basis. A new one is made per session.
- To implement them safely they need to be changed often and be unpredictable.

**## Public key cryptography**

- Lets both sides of the conversation create the same symmetric key without ever sending it across the network.

**## What I mixed up**

Why use both asymmetric and symmetric instead of asymmetric the whole way: it combines the best of both worlds. Symmetric is efficient at delivering info at incredibly fast speeds; asymmetric is slower but ensures a secure key exchange. Combining the two gives fast delivery and a proper exchange of keys.

---

## Encryption Technologies

**## TPM (Trusted Platform Module)**

- Provides cryptographic functions for computers.
- Has persistent memory and versatile memory, and is password protected.

**## HSM (Hardware Security Module)**

- Used in large-scale environments. Usually clustered together with redundant power.
- Allows thousands of keys to be stored securely.
- Usually a plug-in card or separate hardware device. Has key backup.
- Cryptographic accelerators can also be used for real-time environments.

**## Centralized key management**

- Services are everywhere, so management matters. A centralized key management system lets all keys be managed from one area and kept separate from the data.
- Can create keys for a specific service or cloud provider, associate keys with specific users, rotate keys on regular intervals, and log key use and other important data.

**## Challenges**

- Keeping data private is hard because data is spread across many systems.
- Attackers are always finding new techniques — a race to stay ahead.
- The forms data takes are always changing.

**## Secure enclave**

- Often implemented as a hardware processor, isolated from the main processor. Many different technologies and names for it.
- Provides extensive security features: its own boot ROM, monitors the boot process, true random number generator, real-time memory encryption, root cryptographic keys, and performs AES encryption on the hard drive.

**## What I mixed up**

- The difference between TPM and HSM: a **TPM** is used on a smaller, local scale, like individual laptops and servers. An **HSM** is an external device used in data centers for high-volume transactions.

## hashing-and-digital-signatures

**## Hashing**

- A cryptographic hash represents data as a short string of text, like a fingerprint.
- It's a one-way trip: it's impossible to recover the original message.
- Provides integrity. You can verify a downloaded document is the same as the original.
- Example: **SHA-256** gives 256 bits, written as 64 hexadecimal characters.
- A hash function takes an input of any size and creates a fixed-size string, called a message digest or checksum.
- Every different input should produce a different hash. If two inputs produce the same hash, that's a **collision**.
- MD5 has a collision problem, so don't use it for anything important.

**## Practical uses**

- **Verifying a download:** match the hash from the website to the hash of your file.
- **Password storage:** store the hash instead of the password, so nobody knows your actual password.

**## Salting**

- Salt is extra, often random, info added to further randomize the hash. Every user gets their own bit of salt.
- **Rainbow tables** are precomputed tables used to reverse hashes.
- Salted hashes stop rainbow tables from unlocking hashes and finding passwords, and they slow the attacker down. They slow the brute force process.

**## Digital signatures**

- Prove the message wasn't changed (**integrity**), help prove the source (**authentication**), and make sure the signature isn't fake (**non-repudiation**).
- Made with a **private key** and verified with the matching **public key**.

**## What I mixed up**

- Thought a hash could be used as a digital signature by itself. A bare hash only proves integrity. It becomes a signature when the hash is encrypted with the sender's **private key**, which adds proof of who sent it.

## Blockchain

**## What it is**

- Blockchain is a distributed ledger that keeps track of transactions. Everyone has a copy of the ledger, and it's distributed to everyone who wants it.
- Many practical uses: payment processing, digital identification, supply chain monitoring.

**## How it works**

- A transaction is required for the process. Instead of sending the info to one party, you send it to everyone in the blockchain/ledger.
- The transaction is added to a larger block, which is then processed.
- A hash is added to complete the block, which keeps its integrity.
- The hash is very important. If someone tries to modify the block, the hash is no longer valid, and an invalid hash means the block gets thrown out.

## Certificates

**## Digital certificates**

- A digital certificate contains a digital signature and a public key.
- A digital signature adds trust. The certificate carries that trust, and a **certificate authority (CA)** adds further trust by signing it.
- **Web of trust** adds other users for additional trust.
- Certificate creation can be built into the OS (like Windows) or done through third-party websites.
- A certificate contains the X.509 format, serial number, version, signature algorithm, issuer, name of the cert holder, public key, extensions, etc.

**## Root of trust**

- Establishing trust with someone trying to gain access is a fundamental part of IT security.
- One way to provide trust is through a third party: if a third party trusts it, then we can. This overall concept is called the **root of trust**.
- Can be done through hardware or software, such as an HSM (Hardware Security Module), secure enclave, or CA.

**## Certificate authorities**

- To confirm whether a website can be trusted, we use a CA that has digitally signed the website's certificate. Provides real-time verification.
- The process a browser uses to trust a website is built into the browser.
- You can purchase a website certificate and add it to your browser. What you're paying for isn't the certificate itself, it's the validation process the CA goes through.

**## Certificate signing request (CSR)**

- To get a certificate signed, create a key pair, then create a **CSR** containing the public key.
- The CSR is sent to the CA, which does the validation process, then digitally signs the certificate.

**## Private CA**

- With a private CA, you are your own CA. It's built in-house and devices must trust the internal CA. Common for medium to small companies.
- You can self-sign certificates for a private CA. They don't have to be signed by a public CA.
- This requires installing the CA certificate/trusted chain on all devices.

**## SAN and wildcard**

- **SAN (Subject Alternative Name)** is an extension to the X.509 certificate that lists additional identification info. Allows one certificate to support many different domains.
- **Wildcard certificate** — uses an asterisk in place of the server name and applies to all server names in a domain.

**## Revocation**

- **CRL (Certificate Revocation List)** — a list of all certificates that have been revoked. There are many different reasons to revoke.
- **OCSP (Online Certificate Status Protocol)** checks a certificate's status in real time. It requires the CA to respond to every client's OCSP request, which doesn't scale well.
- **OCSP stapling** fixes this. The certificate holder verifies their own status, and the response is "stapled" into the SSL/TLS handshake, which is where the name comes from.
- Most newer browsers support OCSP.

**## What I mixed up**

- OCSP stapling exists to speed things up and let OCSP scale. Without it, the CA has to respond to every request sent by every client.

## Threat Actors

**## What it is**

- A threat actor is an entity responsible for an event that affects the security of others. Often called a malicious actor.
- When looking at an attack, it helps to know who the threat actor is so you can understand their goal.

**## Attributes of threat actors**

- **Internal vs external:** sometimes they work for the company and are inside. Others are outside, trying to gain access through public resources.
- **Resources / funding:** depending on the funding and money they have, you can get a sense of how they're trying to gain access.
- **Level of sophistication:** ranges from blindly running scripts, to building their own tools and capabilities, to somewhere in the middle.

**## Motivations**

- Data exfiltration
- Espionage
- Service disruption
- Blackmail
- Financial gain
- Political reasons
- Ethical
- Revenge
- Disruption/chaos
- War

**## Types of threat actors**

**Nation state**

- An entire government carrying out an attack.
- Many possible reasons: data exfiltration, philosophical, revenge, disruption, war.
- Might have constant attacks and massive resources. Also known as an **APT (Advanced Persistent Threat)**.
- Very dangerous because they have the financial backing of an entire government.
- Usually target military control, utilities, and financial control.

**Unskilled attacker**

- Not sophisticated. Runs scripts without any knowledge of how they work. If the script doesn't work, they don't have the skills to understand why.
- Motivated by the attack itself.
- Usually external, but can be internal.
- Usually doesn't have a lot of resources. Looking for the easiest way in.

**Hacktivist**

- A hacker with a purpose: philosophy, revenge, disruption, etc.
- Often an external attacker, but could potentially be looking to get hired by the company and become an internal attacker.
- Can be sophisticated and look for very specific hacks, including DoS, website defacing, and private document release.
- Funding is usually limited, but some organizations will look for fundraising.

**Insider threat**

- Hard to find, and has extensive resources because they have access to all the resources.
- It's important during the hiring process to avoid hiring someone who becomes a threat.
- Usually medium sophistication, but dangerous because they know where the resources are.

**Organized crime**

- Categorized by money. Professional criminals who are very sophisticated.
- Many different people doing very different things in different ways to gain financial gain.

**Shadow IT**

- A group or department that works around the rules.
- Might build its own infrastructure without anyone knowing. Doesn't have many limitations except the company budget.
- Usually medium sophistication.

**## What I mixed up**

- Not fully understanding how to categorize the six types of threat actors:
    - **Nation state:** sophisticated, many resources, external.
    - **Unskilled attacker:** not sophisticated, few resources, usually external.
    - **Hacktivist:** can be sophisticated, limited resources, usually external.
    - **Insider threat:** medium sophistication, many resources, internal.
    - **Organized crime:** very sophisticated, many resources, usually external.
    - **Shadow IT:** medium sophistication, limited only by the company budget, usually internal.

## Common Threat Vectors

**## What it is**

- A threat vector is a method an attacker uses to gain access. Also called an attack vector.
- Some vectors are more vulnerable than others. IT professionals spend a lot of time protecting existing vectors and finding new ones.

**## Message-based**

- One of the biggest ways attacks begin.
- Delivered through email (they want you to click a link), phishing, or text messages (SMS).
- Phishing works very well because it communicates with you directly and wants you to click links that look real but aren't.
- Malware can be embedded in the message itself, or in what the link downloads.
- Can also be social engineering, like invoice or crypto scams.

**## Image-based**

- Can be done through **SVG** (Scalable Vector Graphics). The image is described in **XML** (Extensible Markup Language).
- Attackers can use HTML injection or JavaScript attack code inside the description of the image.

**## File-based**

- **PDF:** a file format that contains other objects, so things can be hidden in it.
- **ZIP/RAR or any compression file:** can contain many different files.
- **Microsoft Office:** documents with macros, or add-in files.

**## Voice call**

- **Vishing** (phishing over the phone).
- Spam over IP: large-scale phone calls.
- War dialing and call tampering.

**## Removable device (USB)**

- An attacker can get around security products with a USB drive and can infect air-gapped networks.
- A USB device can act as a keyboard, so the attacker can type on your computer.
- Makes it very easy to transfer large amounts of data: plug in, copy, remove, and walk away with it.

**## Vulnerable software**

- **Client-based:** infected executables, known or unknown vulnerabilities. May require constant updates.
- **Agentless:** no installed executable. Compromised software on the server can affect all users, and the client runs a new instance each time.
- Patching is a great way to prevent attacks, but some systems are unsupported or unpatchable. Even a single system can be an entry point.

**## Unsecure networks**

- The network connects to everything, which makes it easy for an attacker.
- On wireless, make sure you're running the newest security protocols. Even wired and Bluetooth connections can be a gateway.

**## Open service ports**

- Most network-based services run on UDP and TCP ports. Once a port is open, an attacker can use it as a gateway into that computer.
- Every application has its own port, which is why port-based firewalls exist as prevention.

**## Default credentials**

- An easy way to gain access. Configure your own credentials.
- Default credentials are very easy to find, even on websites.

**## Supply chain**

- A way for an attacker to get into an organization's infrastructure by going through a third party.
- **MSP (Managed Service Provider):** has access to many different customer networks through one location.

**## What I mixed up**

- An air-gapped network still isn't safe from a **USB vector**. An air gap only blocks network access, and a USB drive is carried in physically and plugged in, so it bypasses network-based security. Once it's plugged in, the attacker can copy data off the computer or have the device act like a keyboard and type on it.

## Phishing

**## What it is**

- Phishing is social engineering with a touch of spoofing. It can be delivered by email or text.
- The goal is usually to extract data from you, like a password or email.
- Don't be fooled when checking or clicking links. Usually something isn't right. You can spot differences in text font and size, or certain aspects missing.

**## Why it works**

- We trust the sources these emails pretend to be (like Apple). Attackers typically use spoofed email addresses that are very similar to the real domain name.
- They succeed through tricks and misdirection.
- **Typosquatting** is a type of URL hijacking.
- Attackers are good at **pretexting**, which is lying. They act as a character.

**## Financial fraud**

- Someone who gains access can send emails with updated bank info or modify wire transfer details.

**## Variations**

- **Vishing** (voice phishing): done over the phone or by voicemail.
- **Smishing** (SMS phishing): done through text messages.
- They can also phish by acting as a CEO or someone higher up.

**## What I mixed up** 

- Phishing, vishing, and smishing differ by **delivery**. Phishing is usually email, vishing is voice calls, and smishing is SMS or text messages.
- **Pretexting** isn't a fourth type of phishing. It's a technique: fabricating a scenario that gives the victim a reason to hand over information.

## Impersonation

**## What it is**

- **Impersonation** is when an attacker pretends to be someone they're not.
- A common **pretext** is where they set the trap, made up of an actor and a story.
- They use some details to gain a level of trust. They may impersonate someone higher up in the company, or use bigger technical terms to make you stop and think about the conversation.
- The attacker's goal is to elicit information from the victim.
- Often seen with vishing, and uses well-documented psychological techniques.

**## Identity fraud**

- Another use of impersonation: credit card fraud, bank fraud, loan fraud, or government benefits fraud.

**## Prevention**

- Don't volunteer information, like giving away a password or personal info over the phone, by text, etc.
- Always verify before revealing info, which can be done through third-party services.
- This should be a normal process in your company and your life

## Watering Hole Attacks

**## What it is**

- An attacker gains access to a system that you'll visit later. They poison the "water hole" and let you come to it.
- Requires the attacker to do some research: understand which third-party sites you visit, then try to gain access to one of them. This requires a vulnerability on the third-party site.
- They may poison the "water" for all visitors to make sure they catch you.

**## Prevention**

- Use layered defense, also called **defense in depth**. This can include antivirus, a firewall, and multiple layers of security. That's why these are often bundled together.

**## What I mixed up**

- Watering hole vs phishing: in phishing, the attacker reaches out to the victim by email or message. In a watering hole, the attacker targets a third-party site the victim trusts and waits for the victim to come to it. Defense in depth is the answer because no single control can stop it.

## Other Social Engineering Attacks

**## Misinformation / disinformation**

- An effective social engineering attack, used to create confusion and division. Typically seen in politics, and can also be delivered through social media and advertising.
- How it typically works:
    - Make fake accounts.
    - Post content from one of the fake accounts.
    - Amplify the message through likes and shares.
    - Real users share the content with other people.
    - Once it gets enough traction, mass media picks it up and makes its own stories.

**## Brand impersonation**

- Attackers make hundreds or thousands of impersonated sites and direct users to them.
- Visitors are then shown pop-ups to download malware.

## Memory Injections

**## What it is**

- Malware runs in memory. It doesn't run unless the CPU processes it.
- Memory contains running processes, including DLLs (Dynamic Link Libraries), threads, buffers, memory management functions, etc.
- The malware is hidden somewhere: it either runs in its own process, or injects itself into a legitimate process.
- To inject into a legitimate process, it has to hide itself between the process's starting and ending address. It then gains the same permissions as that process.

**## DLL injection**

- A DLL is a Windows library containing code and data.
- The attacker puts the path to the malicious DLL somewhere on a storage drive, then gets that path inside the target process.
- The target process goes out to disk, pulls the malicious DLL into memory, and now the malware is running.

**## What I mixed up**

- Malware hides in a legitimate process because it's harder to detect than a suspicious executable, and it inherits that process's permissions.

## Buffer Overflows

**## What it is**

- A buffer overflow is when an attacker writes more than what's expected into a particular area of memory, and the additional data overflows into another area of memory.
- Developers need to perform **bounds checking** to make sure this doesn't happen.

**## Why it's hard to pull off**

- Attackers spend a lot of time looking for openings. It isn't a simple exploit: even once you find an opening, it takes time to avoid crashes.
- The attacker is looking for an overflow that is repeatable and always gives them a function that provides an advantage.

**## What I mixed up**

- Preventing buffer overflows is the developer's job. Bounds checking verifies that input or data length doesn't exceed the allocated buffer size.

## Race Conditions

**## What it is**

- A race condition is when two events happen at the same time and the application doesn't account for the fact that they may be running simultaneously.
- Race conditions can cause big problems.

**## TOCTOU**

- **TOCTOU (Time-of-check to time-of-use)** is a type of race condition.
- The application checks the system for a value, then later uses that value to carry out a function.

**## Real examples**

- January 2004: the Mars rover "Spirit."
- Pwn2Own Vancouver 2023: the Tesla Model 3

**## What I mixed up**

- What changes between the check and the use can be a file, permission, path, or system variable. That's a problem because the program then acts on stale or invalid info. Not every race condition is a TOCTOU. To count as one, it has to follow a check-then-use pattern.

## Malicious Updates

**## What it is**

- Always make sure operating systems and applications are updated. But installing an update always carries a security concern, because an attacker can embed malicious code in the patch or update.

**## Best practices**

- Have a backup, and install from a trusted source.
- Consider your actions every time you download or update, since any installation could be malicious. A random pop-up is a hint that something could be malicious.
- Visit the developer's site directly. Many operating systems will only allow digitally signed apps.
- Automatic updates usually have security checks and digital signatures, and carry a high level of trust because the update comes directly from the developer. It's still not a 100% guarantee.

**## Example**

- The **SolarWinds Orion** supply chain attack.

**## What I mixed up**

- A signed automatic update isn't a 100% guarantee, because a signature only verifies the publisher's identity and the file's integrity at the time of signing. In the SolarWinds attack, the attackers compromised the internal build pipeline and put malicious code into the update before it was digitally signed.

## OS Vulnerabilities

**## What it is**

- Operating systems are fundamental computing systems and everyone is running one, which makes them a very attractive target for attackers.
- They're super complex, with millions of lines of code, which means more opportunities for security issues.

**## Patching**

- Patches usually come once a month. For example, Windows has **Patch Tuesday**, the second Tuesday of each month.
- Best practice is to always plan to update. It's a race between you and the attackers.
- Have a backup. If it involves many machines, test before deployment, since a patch may break something.

## SQL Injection

**## Code injection**

- A code injection attack is a common application attack where the attacker puts their own code into information that gets input into the application.
- This is enabled by bad programming.
- Examples of injection: HTML, SQL, XML, LDAP, etc.

**## SQL injection**

- **SQL (Structured Query Language)** is the most common language for relational database management systems.
- **SQLi** works by an attacker putting their own SQL requests into an existing application. Your application shouldn't allow this.
- Can often be executed in a web browser.
- Can be very bad: the attacker can get all the database info, delete database info, add users, cause DoS, etc.

**## What I mixed up**

- Preventing SQL injection is the developer's job. The application should treat all user input as untrusted, regardless of the source, and validate it. (Add what you'd do with the input, like parameterized queries, in your own words.)

## Cross-Site Scripting

**## What it is**

- **XSS** is the abbreviation used to tell Cross-Site Scripting apart from Cascading Style Sheets (CSS).
- It was originally called “cross-site” because of security flaws. It’s one of the most common web app vulnerabilities.
- It takes advantage of the trust the user has in the site, and usually uses JavaScript.

**## How an attack works**

- The attacker sends the victim a link containing a malicious script.
- The link sends the victim to a legitimate site. The site loads and runs the malicious script as well.
- The script then sends data back to the attacker, such as session cookies.

**## Non-persistent XSS**

- A website allows scripts to run in user input.

**## Persistent XSS**

- The attacker posts a message to something like a social network. It’s “persistent” because the attacker stores it on the third-party site.
- There’s no specific target. It hits everyone who visits that site.
- The attacker may include other code that lets people share the malicious code.
- **Example:** the Subaru hack. When you log in to Subaru you get a token that never expires, and the token lets you request any service. That let you add your own email to someone else’s car and get full access to it.

**## Protection**

- Don’t click untrusted links.
- Consider disabling or limiting JavaScript.
- Keep browsers and applications updated to the newest versions.
- Validate input.

**## What I mixed up**

- XSS exploits the user’s trust in a site. The script is delivered through the legitimate site but runs in the victim’s browser. A persistent attack hits everyone who visits the site, with no specific target. A non-persistent attack hits whoever clicks the crafted link.

## Hardware Vulnerabilities

**## What it is**

- We’re surrounded by hardware devices where we generally don’t have access to the OS. Since they’re connected to the network, they can be a security risk.
- Everything is connected (garage doors, refrigerators, etc.), so the security landscape has grown.
- **Firmware** is software inside the hardware. Vendors are really the only ones who can fix their hardware.

**## EOL vs EOSL**

- **EOL (end of life):** the manufacturer stops selling the product, but you can still receive updates and security patches.
- **EOSL (end of service life):** support fully stops, and there are no new security patches or updates.
- Technology reaching EOSL is a significant concern, since security patches are part of normal operation.

**## Legacy platforms**

- Equipment that stays installed for a very long time, and may be running end-of-life software.
- Determine the risk of running it. It may need extra security protections based on how important the device is, like additional firewalls or IPS signatures.

**## What I mixed up**

- EOSL means support fully stops and patches stop. That makes it worse than EOL, because if an attacker finds a vulnerability, no security patch will ever be released to fix it.

## Virtualization Vulnerabilities

**## What it is**

- Virtualization security is quite different from non-virtual machines, since VMs can appear anywhere.
- VMs may have different capabilities, memory, and storage, but they’re similar to physical machines.
- Specific virtualization vulnerabilities: local privilege escalation, command injection, and information disclosure.

**## VM escape**

- A VM is self-contained, but an attacker can escape it. That means breaking out and interacting with the host system or hardware.
- Once out of the VM, you have great control. This would be a massive exploit.

**## Resource reuse**

- The **hypervisor** manages the relationship between physical and virtual resources, but those resources can be reused between VMs.
- That means data can be shared between VMs.

**## What I mixed up**

- **VM escape** means breaking out of the VM to interact with the host system or hardware, which is a massive exploit because of the control it gives. **Resource reuse** means the hypervisor reuses physical resources between VMs, so data left behind, like uncleaned memory, can be exposed to another VM.

## Cloud Specific Vulnerabilities

**## What it is**

- Cloud adoption is nearly universal, but it comes at a cost: putting sensitive data into the cloud.
- The issue is that a lot of companies aren’t using the right protections or simple best practices to keep that sensitive data confidential.

**## Common attacks**

- **DoS (denial of service):** a fundamental attack type.
- **Authentication bypass:** the attacker takes advantage of faulty or weak authentication.
- **Directory traversal:** manually moving around the structure of the web server, into various folders or subdirectories.
- **Remote code execution.**

**## Web application exploits**

- These have increased because they’re easy to exploit and the rewards are massive.
- **XSS (cross-site scripting):** the attacker takes advantage of poor input validation.
- **Out-of-bounds write:** can cause data corruption, crashing, or code execution.
- **SQL injection:** gives the attacker direct access to the database.

**## What I mixed up**

- Directory traversal lets an attacker reach files outside the web server’s intended folders. Remote code execution lets an attacker run commands or scripts directly on the server, which gives them control of the system.

## Supply-Chain Vulnerabilities

**## What it is**

- The supply chain is the process of getting raw materials to a consumer: raw materials, suppliers, manufacturers, distributors, customers, and consumers.
- Attackers can infect any step along the way, and one exploit can infect the entire chain.
- Service providers often have access to internal services, which is an opportunity for the attacker. Many companies consider ongoing security audits of all providers.
- **Example:** the 2013 Target Corp. breach, where 40 million credit cards were stolen.

**## Hardware**

- Can you trust your new firewall, server, router, switch, or software? All network traffic flows through switches and routers.
- The best ways to build trust: a smaller supply base, strict controls over policies and procedures, and security as part of the overall design.

**## Software**

- With software providers, trust is a foundation of security. A digital signature helps with that trust.
- With updates and patches, ask: how secure are the updates?

**## What I mixed up**

- In the Target breach, the attacker got in through a third-party HVAC supplier. Two ways to reduce that risk: assess third-party vendors, and keep systems like the credit card and HVAC systems on separate networks.

## Misconfiguration Vulnerabilities

**## Open data**

- An easy way to get data into an attacker’s hands is leaving it unsecured, like an open door. This is increasingly common with cloud storage.

**## Admin accounts**

- Unsecured admin accounts: the Linux root account, the Windows Administrator account, also called a superuser account.
- A misconfiguration can be as simple as a weak password.
- Best practice: disable direct access to the root account, and protect and minimize root or admin accounts.

**## Insecure protocols**

- Telnet, FTP, SMTP, and IMAP all send data in plaintext. You can verify security with a packet capture.
- Use the encrypted versions: SSH, HTTPS, SFTP.

**## Default configurations**

- Make sure default usernames and passwords on devices are changed.
- The **Mirai botnet** takes advantage of default configs.

**## Open ports**

- Limit the open ports others can reach, for example with a firewall. But firewall rulesets add complexity, so always test and audit your firewalls.

**## What I mixed up**

- SFTP replaces FTP and SSH replaces Telnet. You can prove a protocol is leaking data with a packet capture in Wireshark, since Telnet and FTP send data in plaintext while SSH and SFTP are encrypted.

## Mobile Device Vulnerabilities

**## What it is**

- Mobile devices are challenging to secure. They often need additional security policies and systems.
- They’re easily hidden, always moving, contain sensitive info (personal and organizational), and are constantly connected to the internet.

**## Jailbreaking / rooting**

- Mobile devices are purpose-built systems, but the OS can be replaced through jailbreaking or rooting. This replaces the OS with a third-party OS.
- It provides uncontrolled access and circumvents the security features that were in place.

**## Sideloading**

- Installing apps from outside the allowed app store and its security checks.
- Installing malicious apps can be a significant security concern. The OS typically manages which sources apps can be installed from.

**## What I mixed up**

- **Jailbreaking/rooting** replaces the device’s OS with a third-party OS, which gives uncontrolled access and circumvents the built-in security features. **Sideloading** installs apps from outside the allowed app store, which skips its security checks. Both are risky because malicious content can get onto the device.

## Zero-Day Vulnerabilities

**## What it is**

- Many applications have vulnerabilities. Every day, people are trying to find unknown vulnerabilities before attackers do.
- Attackers are constantly looking for unknown vulnerabilities, and they won’t share what they find with the vendor.
- From the vendor’s perspective there is no vulnerability, so there’s no patch. This is called a **zero-day attack**: an attack with no patch or method of mitigation.

**## Example**

- From the CVE website: the Chrome browser in April 2023, which had memory corruption and a sandbox escape.

**## What I mixed up**

- A zero-day is a vulnerability the vendor doesn’t know about, so no patch exists. The “zero” refers to the days the vendor has had to fix it. The vendor can’t patch it because, from their point of view, there’s no vulnerability, and attackers don’t share what they find.

## Malware Overview

**## What it is**

- Malware is any malicious software. It can gather info, show you advertising, or be a virus or worm.
- Examples: viruses, worms, ransomware, trojan horse, rootkit, keylogger, spyware, bloatware, logic bomb.
- Malware isn’t one single event. The pieces work together.
- To infect your system, malware has to find a way to run a program, whether through an email, a pop-up, a drive-by download, or a worm.
- Malware exists because the data we have is very valuable, both personal and organizational.

**## Ransomware**

- A particularly nasty kind of malware. It encrypts your data files, like photos, movies, and documents.
- The OS keeps working normally, so you may not know you’ve been infected until your files are locked.
- Attackers usually demand money in exchange for the decryption key.
- **Protection:** keep an offline backup, keep the OS and applications up to date, and keep antivirus/malware signatures up to date.

## Viruses and Worms

**## Viruses**

- A virus is malware that can replicate itself. It reproduces through the file system or the network, and may or may not cause problems.
- Antivirus is very common on the operating systems we use.
- **Types:** program viruses, boot sector viruses, script viruses, macro viruses.
- **Fileless virus:** does a great job of avoiding antivirus. It operates in memory but is never installed in a file or application.

**## Worms**

- Malware that self-replicates. It doesn’t need you to do anything, uses the network as its transmission, and spreads quickly.
- Very bad, since they can take over systems very quickly.
- Firewalls and IDS/IPS can mitigate many worm infections, but they don’t help much once the worm is inside.

**## What I mixed up**

- A virus needs human interaction to spread, but a worm self-replicates over the network without any. Firewalls and IDS/IPS help before a worm gets in, since they watch traffic coming in from outside. Once it’s inside, they struggle to catch it moving between internal systems.

## Spyware and Bloatware

**## Spyware**

- Malware that spies on you and watches everything on your system.
- It can trick you into installing it, and it’s very good at browser monitoring.
- May install keyloggers, where every keystroke is captured and sent back to the attacker in a file.
- **Protection:** keep your antivirus/anti-malware up to date, always understand what you’re installing, keep a known good backup, and run scans with third-party software.

**## Bloatware**

- Shows up on new devices like computers or phones: unexpected applications installed by the manufacturer, which can use up valuable storage.
- **Managing it:** identify and remove it through the built-in installer, the app’s own uninstaller, or third-party software.

## Other Malware Types

**## Keyloggers**

- Keystrokes contain valuable info like passwords and email messages.
- Keyloggers circumvent encryption protections. They can do a lot more too: take screenshots, capture stored messages, and record anything searched in a search engine.

**## Logic bomb**

- Waits for a particular event or time to occur. It can reboot a system or erase data, and it’s difficult to identify.
- **Prevention:** set up and configure processes and procedures, use electronic monitoring, and audit constantly.

**## Rootkit**

- Originally a Unix technique.
- Generally hides itself in the kernel, as part of the OS, which makes it hard to identify with typical anti-malware. It also modifies core system files.
- Not all rootkits are part of the OS. Some run as a traditional process.
- **Finding and removing:** look for the unusual, use a remover specific to that rootkit, and use Secure Boot with UEFI.

**## What I mixed up**

- A keylogger gets around encryption because it captures the data at the point of entry, before any encryption happens.
- A rootkit hides in the kernel as part of the OS and modifies core system files, so typical anti-malware doesn’t find it. Secure Boot with UEFI helps because it blocks unverified code from loading at startup.

## Physical Attacks

**## What it is**

- Old-school security: no keyboards, mice, or command line.
- If you have physical access to a server, you have full control. Door locks only keep out the honest people.

**## Brute force (physical edition)**

- An attacker physically pushes through a door or window to gain access.

**## RFID cloning**

- **RFID** is the underlying technology of access badges and key fobs.
- RFID cloning can get you access, it’s cheap and easy to find the equipment, and duplicating a badge takes seconds.
- This is another reason we have **MFA (multi-factor authentication)**.

**## Environmental attacks**

- Attacks on the surrounding environment, like shutting off power to a data center, or attacking the HVAC or fire suppression systems.

**## What I mixed up**

- MFA reduces the risk of RFID cloning because a cloned badge is only one factor. The attacker would also have to get another independent form of identification.

## Denial of Service

**## What it is**

- DoS occurs when an attacker forces a service to fail.
- Reasons: taking advantage of a design failure or vulnerability, causing a system to fail for a competitive advantage, or creating a smokescreen for another vulnerability.

**## Friendly DoS**

- Unintentional. Examples:
    - **Network:** a layer 2 loop without STP (Spanning Tree Protocol).
    - **Bandwidth:** downloading multi-gigabyte Linux distros over a DSL line.
    - A water line breaks.

**## DDoS (Distributed Denial of Service)**

- Launched with an army of computers to bring down a service.
- Attackers typically have **botnets**: networks of computers controlled by the attacker.
- Also described as an **asymmetric** attack.

**## Reflection and amplification**

- A small attack turns into a big attack. It’s possible because attackers take advantage of internet services available to anyone.

**## What I mixed up**

- A DoS comes from a single source, and a DDoS is distributed across many sources. A friendly DoS is still a DoS because the service is denied regardless of intent.

## DNS Attacks

**## DNS poisoning**

- Modifying the DNS server itself. Requires some crafty hacking.
- Another form: modifying the **host file** on the client computer. Requires access plus elevated rights.
- Another form: sending a fake response to a valid DNS request. Requires the attacker to sit in between the conversation in real time.

**## Domain hijacking**

- Another way to affect DNS is to gain access to the **domain registration**, which gives the attacker control of the traffic flow.
- Ways to get in: brute force, social engineering the password, gaining access to the email address tied to the person who manages the account, etc.

**## URL hijacking**

- Another way to direct users to a malicious site. The attacker can make money off your mistakes:
    - Sell the badly spelled domain to the actual owner.
    - Redirect traffic to competitors of the legitimate site.
    - Use it as a phishing site.
    - Infect visitors with a drive-by download.
- Types include **typosquatting** and **brandjacking**.

**## What I mixed up**

- DNS poisoning gives users a wrong answer for a name, by modifying the DNS server, editing the client’s host file, or sending a fake response to a valid request. Domain hijacking gets control of the domain registration, so the attacker controls where all traffic for that domain goes.

## Wireless Attacks

**## Deauthentication**

- A wireless deauthentication attack is a type of DoS attack that completely disconnects a device from the wireless network.
- The main vulnerability is the **management frames** sent between the access point and devices. Management frames are very important for wireless connectivity (802.11 networks).
- **Protection:** newer standards (you noted 802.11ac) now encrypt management frames. But not every management frame is encrypted, such as authentication frames.

**## RF jamming**

- Attacks all devices trying to communicate over the wireless network.
- Accidental disruption is called **interference**, not jamming. Jamming is intentional.
- Types: constant random bits, constant legitimate frames, random timing, or **reactive** (based on noise).
- To perform it, the attacker needs to be close to the access point. Finding the source of the jamming is known as a **fox hunt**.

**## What I mixed up**

- Deauth exploits management frames to disconnect devices from the wireless network. Jamming interferes with the radio signal itself. Encrypting management frames helps against deauth but not jamming, because jamming doesn’t rely on exploiting those frames.

## On-Path Attacks

**## On-path attack**

- Lets an attacker sit between two devices and watch all the traffic going back and forth. Also known as a man-in-the-middle attack.
- The attacker can redirect or modify your traffic.

**## ARP poisoning (spoofing)**

- ARP has no security, so ARP poisoning is an on-path attack on the local IP subnet.

**## On-path browser attack**

- The attacker performs the on-path attack on the same device as the victim. Malware or a Trojan does all the proxy work.
- Even if the network traffic is encrypted, the malware sees all the info in plaintext, since it’s on the same device as the victim.
- The malware waits for you to enter your credentials and gains access to them. It can also create sessions behind you that you’d have no idea about.

**## What I mixed up**

- In an on-path attack, the attacker sits on the network between two devices. In an on-path browser attack, the attacker sits on the victim’s own device through malware. Encryption doesn’t stop the browser version because the malware sees the data in plaintext on the same device.