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

## Replay Attacks

**## What it is**

- Useful info is transmitted over the network, and a crafty attacker will take advantage of that.
- To perform a **replay attack**, the attacker needs access to the raw network data. They may get it through a network tap or ARP poisoning.
- This is not an on-path attack.

**## Pass the hash**

- A form of replay attack.
- When someone sends a normal authentication request to the server, the attacker captures the authentication and gets the credentials.
- The attacker replays the credentials to the server. Now they have access to the server, posing as the original person.
- **Defense:** salt or encryption.

**## Cookies and session IDs**

- Attackers also want your cookies and session IDs. Cookies are used for tracking, personalization, and session management, and could be considered a privacy risk.
- Session IDs are often stored in the cookie. If the attacker gets the session ID, they pose as the victim.

**## Header manipulation**

- Attackers can gather header info with Wireshark, exploit through cross-site scripting, modify headers, and modify cookies.
- **Prevention:** encrypt everything, from start to destination.

**## What I mixed up**

- In an on-path attack, the attacker sits in the middle of the conversation. In a replay attack, the attacker captures the data once, then resends it to the server later, posing as the original sender. Salt helps against pass the hash because the authentication data is different each time it’s sent, so a captured copy is useless when replayed.

## Malicious Code

**## What it is**

- Attackers can use many things to exploit a vulnerability: social engineering, default credentials, misconfigurations. These don’t require a huge amount of technical skill.
- Malicious code takes many forms: executables, scripts, macro viruses, worms, trojan horses, etc.
- Since there are many ways to attack, we use many protections: firewalls, anti-malware, patches and updates.

**## Example**

- The **WannaCry** ransomware.

## Application Attacks

**## Injection**

- Very common. Code injection is caused by bad programming. Many forms: HTML, SQL, XML, LDAP, etc.

**## Buffer overflow**

- Overwriting a buffer of memory, or spilling over.
- Not an easy exploit, and once again caused by developers not performing checks. The really useful kind of buffer overflow is repeatable.

**## Replay attack**

- Needs raw network data. Not an on-path attack.

**## Privilege escalation**

- Gaining higher-level access to a system, meaning more capabilities. Very common and high priority for attackers.
- **Horizontal privilege escalation:** not moving up, but going from one user’s access to another’s.
- **Mitigation:** patch quickly, keep antivirus/anti-malware updated, use **DEP (data execution prevention)**, and use **ASLR (address space layout randomization)**.

**## Cross-site request forgery (CSRF)**

- Cross-site requests are common and legitimate. Websites are separated into client-side and server-side code. Client side is usually HTML/JavaScript, server side usually HTML/PHP. Attackers can take advantage of this difference, which is known as cross-site request forgery.
- Also called a **one-click attack** or **session riding**.
- It takes advantage of the trust the web application has in the user.

**## Directory traversal / path traversal**

- Not an application vulnerability, but a web server vulnerability. It lets the attacker read files outside the website’s file directory.
- Sometimes it’s a software vulnerability inside the web server, or a vulnerability in application code.

**## What I mixed up**

- XSS abuses the user’s trust in the site. CSRF abuses the site’s trust in the user.
- Vertical privilege escalation jumps to a higher role like admin. Horizontal goes from one user’s access to another’s.
- DEP marks memory regions as non-executable. ASLR randomizes memory addresses so an attacker can’t predict where things load.

## Cryptographic Attacks

**## What it is**

- The difference between data being secure or insecure is the key. Instead of getting the key, attackers try to break the safe.
- Attackers often focus on the implementation of the cryptography, since it’s usually the weakest component.

**## Birthday attack**

- A form of cryptographic attack. In a group of 30 students, there’s about a 70% chance two share a birthday. In the digital world, the same math applies to hashes.
- The attacker looks for a **hash collision** using brute force.
- A larger hash output size makes this much harder.
- Hash digests are supposed to be unique, but collisions were found with **MD5**.

**## Downgrade attack**

- Forces the two systems that are communicating to downgrade their security.
- A common form is **SSL stripping**, an on-path attack that strips the S from HTTPS. This leaves the victim’s browser connection unencrypted.

**## What I mixed up**

- A birthday attack looks for two different inputs that produce the same hash, which is a collision. A larger hash output makes collisions less likely. MD5 is a problem because collisions have actually been found.
- SSL stripping is both an on-path attack, because the attacker sits in the middle, and a downgrade attack, because it pushes the connection from HTTPS to unencrypted HTTP.

## Password Attacks

**## Storing passwords**

- Never store passwords in plaintext, but some applications still do. If an application stores them in plaintext, get a new application.
- All passwords should be stored as a hash, so there’s no way to reverse a password from only the hash.
- **SHA-256** is now used instead of MD5.

**## Password spraying**

- The attacker tries the most common passwords across accounts, without getting locked out, raising concern, or setting off flags.

**## Brute force**

- Trying every possible combination until the hash is matched. Time-consuming.
- **Online:** most accounts eventually lock out after many attempts.
- **Offline:** attackers do this instead, against the captured hash. They can spend any amount of time and attempts until the hash matches.

**## What I mixed up**

- Brute force avoids lockouts by running offline on the attacker’s own hardware against a captured hash, so they can try as many passwords as they need. Spraying avoids lockouts by trying a few common passwords against many different accounts instead of many passwords against one.

## Indicators of Compromise

**## What it is**

- An **IOC (indicator of compromise)** is an event that indicates an intrusion.
- Examples: an unusual amount of traffic, changes to file hashes, irregular international traffic, changes to DNS data, unusual login patterns, spikes in read requests to certain files.

**## Account indicators**

- **Account lockout:** a telling indicator, especially with too many login attempts. An account can also be locked out **administratively**, which is a bigger concern and can be part of a larger plan.
- **Concurrent session usage:** you can’t be in two places at once. Signs are multiple logins from multiple locations.
- **Authentication logs:** logins from parts of the world the user couldn’t have traveled to are easy to spot.

**## System indicators**

- **Blocked updates:** attackers want to stay logged in as long as possible. Malware usually disables anti-malware and antivirus updates to stay on the system. If you can’t update, that’s usually a sign of compromise.
- **Resource consumption:** there’s always something an attacker is doing that you should be able to identify, like transferring files. Firewall logs should show the outgoing transfer.
- **Resource inaccessibility:** a server is down, a network disruption, or a server outage. Also data that isn’t usually encrypted suddenly is.

**## Log indicators**

- **Out-of-cycle logging:** activity at an unexpected time, like security patches happening outside the scheduled time. Common in firewall logs.
- **Missing logs:** attackers delete log info to hide the compromise, since logs may incriminate them.

**## Leaked data**

- A very clear sign of compromise is private organizational data appearing on the public internet, typically done with ransomware.

**## What I mixed up**

- An administrative lockout is a bigger concern than a failed-attempt lockout because it means someone with admin rights deliberately locked the account, which can be part of a larger plan. Malware blocks anti-malware updates so it can stay on the system as long as possible.

## Segmentation and Access Control

**## Segmentation**

- To limit the scope of any security event, segment your network into different pieces.
- Can be **physical**, **logical**, or **virtual** segmentation.
- Also done for performance optimization. Sometimes it’s required for compliance, as **mandated segmentation**.

**## ACLs (access control lists)**

- An easy way to segment. Used to allow or deny traffic and to restrict access to network devices. Be very careful when configuring ACLs.
- Examples: one person is allowed to read, one is allowed to access the network, and one is allowed on the network only through certain ports.
- Many operating systems use ACLs for file access.

**## Application allow / deny lists**

- Many applications have an allow/deny list, which can be done through a security policy.
- **Allow list:** only the listed applications can run. **Deny list:** anything can run except what’s on the list.
- Examples of what a list can be based on: application hash, certificate, path, and network zone.

**## What I mixed up**

- Segmentation limits the scope of a security event by splitting the network into pieces, so a problem doesn’t hit everything. Two other reasons to do it are performance optimization and compliance requirements.

## Mitigation Techniques

**## What it is**

- Mitigation is the process of reducing the impact of a security event or a potential security event.

**## Patching**

- Incredibly important, and it helps keep your system more stable.
- Can be monthly updates, third-party updates, auto updates, or emergency **out-of-band** updates.

**## Encryption**

- Prevents access to application data files. Types: file-level encryption, **FDE (full disk encryption)**, and application data encryption.

**## Monitoring / logging**

- Done through devices like switches, servers, routers, and firewalls, or through built-in sensors.
- Logs are often consolidated into one place, like a **SIEM**.

**## Least privilege**

- Rights and permissions should be set to a minimum.
- All user accounts should be limited, and users shouldn’t be able to run administrative privileges.

**## Enforce configuration**

- Perform a **posture assessment**: an extensive check for the OS patch version, **EDR (endpoint detection and response)** version, firewall status, and certificate status.
- Systems that are out of compliance are quarantined.

**## Decommissioning**

- Should follow a formal policy. Don’t throw your data in the trash.

**## What I mixed up**

- A posture assessment checks a device against preconfigured policies: OS patch version, EDR version, firewall status, and certificate status. Systems that fail are quarantined.

## Hardening Techniques

**## Operating systems (Windows / Linux)**

- Keep updates current.
- Secure user accounts with a password policy and limited access.
- Limit network access and security.
- Monitor and secure with antivirus/anti-malware.

**## Encryption**

- Encrypt application data files, use FDE, and encrypt all network traffic through a VPN.

**## Endpoints**

- Think about the many different devices that need hardening, and apply hardening based on that.

**## EDR (endpoint detection and response)**

- Detects threats in different ways: signatures, behavior analysis, machine learning, and process monitoring, with a lightweight agent on the endpoint.
- Can do root cause analysis on the threat.
- Can respond immediately: isolate the system, quarantine the threat, and roll back to a previous config. This can all be done through an API, with no user or technician needed.

**## Host-based firewall**

- A software-based firewall. Allows or denies incoming or outgoing application traffic, and identifies and blocks unknown processes.

**## HIPS (host-based intrusion prevention system)**

- Recognizes and blocks known attacks, secures OS and application configs, and is often built into endpoint protection software.
- Looks for signatures, behavioral changes, buffer overflows, registry changes, and modified files.

**## Ports and software**

- Every open port is an entry point, so close everything except the required ports. You can control access through a firewall.
- Use **nmap** to see whether certain ports are open or closed.
- Change default passwords, or add extra security through an additional logon or third-party authentication.
- Remove unnecessary software, since every piece of software has a bug, known or unknown.

**## What I mixed up**

- **Host-based firewall** allows or denies incoming and outgoing application traffic and blocks unknown processes. **HIPS** recognizes and blocks known attacks by watching for signatures, behavior changes, buffer overflows, registry changes, and modified files. **EDR** detects threats, does root cause analysis, and responds automatically by isolating the system, quarantining the threat, or rolling back to a previous config.
- Closing unneeded ports and removing unnecessary software are the same idea: allow only what’s necessary and close or remove everything else, which reduces the attack surface.

## Cloud Infrastructure

**## Responsibility matrix**

- The cloud responsibility matrix covers IaaS, PaaS, SaaS, etc.
- Security responsibilities should be well documented, and they can vary. Each one is managed by either the customer or the provider.

**## Hybrid cloud**

- Private plus public. Provides more flexibility but adds more complexity.
- **Mismatches in protection** can happen across platforms: authentication, firewall configs, server settings.
- It can also be difficult to manage logs from various providers.
- Each time data moves from one provider to another, there can be data leakage, since it crosses the public network.

**## Third-party risk**

- Third-party attacks are a risk. Mitigations: ongoing vendor risk assessments, including third-party impact in incident response, and constant monitoring.

**## Infrastructure as code (IaC)**

- Used to describe an infrastructure. It lets you modify it and create versions, and use the code to build other application instances.

**## FaaS (function as a service)**

- Applications are separated into individual, autonomous functions. It removes the OS from the equation.
- Most of the work with serverless architecture happens in the cloud.

**## Monolithic applications**

- One big application that does everything: user interface, business logic, data input and output.
- This can create code challenges, since you have a massive codebase.

**## APIs**

- API stands for application programming interface.
- APIs are the glue for the microservices and make the application much more scalable and resilient.

**## What I mixed up**

- In IaaS the customer manages more, and in SaaS the provider manages more. Documentation matters because it removes confusion about who owns which controls.
- Hybrid cloud adds complexity because of mismatches in protection (authentication, firewall configs, server settings) and scattered logs. The data leakage risk comes from data crossing the public network when it moves between providers.
- A monolith is one huge codebase, which makes changes hard. APIs are the glue that lets independent microservices communicate, which makes the application more scalable and resilient.

## Network Infrastructure

**## Physical isolation**

- Two devices are physically separate. If they need to communicate, they have to be connected in some way.
- Separate devices mean multiple units and separate infrastructure.

**## VLANs**

- A VLAN (virtual local area network) lets you configure interfaces on your switch.
- VLANs can’t communicate with each other without a layer 3 device or router.

**## SDN (software-defined networking)**

- Networking devices have different planes of function: data, control, and management.
- **Data plane:** processes network frames and packets. Does the forwarding, trunking, encrypting, and NAT.
- **Control plane:** manages the actions of the data plane. Routing tables, session tables, NAT tables.
- **Management plane:** configures and manages the device, through SSH, a browser, or an API.

**## What I mixed up**

- VLANs need a layer 3 device or router to communicate because each VLAN is its own separate network configured on a layer 2 switch. The control plane manages the data plane’s actions (routing, session, and NAT tables), and the management plane is how admins configure the device.

## Other Infrastructure Types

**## Cloud vs on-premises**

- There are two main categories for IT security.
- **Cloud security:** centralized and costs less.
- **On-premises:** puts the security burden on the client and costs more. You can customize your security posture, an on-site IT team can manage security better, and a local team maintains uptime and availability. But security changes can take time.

**## Centralized vs decentralized**

- Most organizations are decentralized, but it’s hard to maintain security with so many devices in different places.
- A **centralized** approach allows correlated alerts, consolidated log file analysis, and a comprehensive status (maintenance and patching).
- Drawbacks: it creates a single point of failure and can cause scalability concerns.

**## Virtualization and containers**

- Virtualization lets you run different systems and build or tear them down whenever you want. Each application needs its own OS, so it’s relatively expensive.
- To address virtualization’s inefficiencies, some organizations move to **containerized** environments, which let you run multiple applications on the same hardware.
- Every container is an isolated process in a sandbox.

**## IoT**

- Internet of Things: sensors, smart devices, wearable technology, facility automation.
- Convenient, but with weak security defaults.
- A single exploited IoT device can affect your whole network.

**## SCADA / ICS**

- **SCADA:** Supervisory Control and Data Acquisition. **ICS:** Industrial Control Systems.
- Computers manage this equipment, and it uses distributed control systems. These systems need to be segmented for security purposes.

**## RTOS**

- **Real-time operating system:** an OS with a deterministic processing schedule, with no time to wait for other processes.
- Extremely sensitive to security issues, and very self-contained.

**## Embedded systems**

- Hardware and software designed for a specific function, built with only that task in mind.

**## High availability**

- One way to provide uptime. Redundancy doesn’t always mean availability.
- **HA (high availability)** may involve many different components working together. Higher availability usually means higher costs.

**## What I mixed up**

- Centralizing security makes maintenance and patching easier but creates a single point of failure. On-premises gives more control but puts the security burden on my own team, and security changes can take time.
- A container avoids needing a full guest OS for each application. Each container is an isolated process in a sandbox.

## Infrastructure Considerations

**## Resilience**

- Eventually something will happen. How quickly can we recover?
- Depends on many variables: the root cause, replacement hardware installation, software patches, redundancy systems.
- **MTTR** stands for mean time to repair.

**## Cost**

- How much money is required? Initial installation cost can be very different across platforms.
- Also: ongoing maintenance, replacement or repair costs, and tax implications.

**## Responsiveness**

- How quickly can we get a response? Speed is a very important metric, especially for interactive applications.

**## Scalability**

- How quickly can we increase or decrease capacity? This is also called **elasticity**.
- There’s always a resource challenge with scalability, and it needs to include security monitoring.

**## Ease of deployment**

- An application has many moving parts: a web server, database, caching server, and firewall.
- Deployment might be an involved process because of hardware resources, cloud budgets, and change control, or it might be simple with something cloud-based.

**## Risk transference**

- Transferring the risk to a third party.
- **Cybersecurity insurance** can help with recovering internal losses and with protection against legal issues from customers.

**## Ease of recovery**

- Time is money. How fast can you recover?

**## Patch availability**

- Software isn’t usually static, and patching is often the first task after installation.

**## Inability to patch**

- Can include embedded systems like HVAC controls. Consider adding extra security around unpatchable devices.

**## What I mixed up**

- Embedded systems like HVAC controls can’t be patched easily, so they need extra security around them, such as additional firewalls. Transferring risk can mean buying cyber insurance or moving it to a third party.

## Secure Infrastructures

**## What it is**

- Every network is different, but there are some similarities.
- **Firewalls** separate trusted from untrusted and provide additional security checks.

**## Security zones**

- More flexible and more secure than an IP address range.
- Each area of the network is associated with a zone, like untrusted/trusted or internal/external.
- This simplifies security policies and makes them easier to maintain.

**## Attack surface**

- Think about how an attacker might get in. Ways include application code, open ports, the authentication process, and human error. This is the **attack surface**.
- It should be minimized by auditing, blocking ports, and monitoring traffic in real time.

**## Network connectivity**

- Integrating security into network connectivity is essential. Options: secure network cabling, application-level encryption, and network layer encryption.

**## What I mixed up**

- The attack surface is every way an attacker might get in: application code, open ports, the authentication process, and human error. It’s minimized by auditing, blocking ports, and monitoring traffic in real time.

## Intrusion Prevention

**## IPS vs IDS**

- An **IPS** watches traffic traverse the network in real time. Intrusions may include exploits against the OS or applications, buffer overflows, and XSS.
- An **IDS (intrusion detection system)** can’t block anything. It only alarms.

**## Fail open vs fail closed**

- **Fail open:** data continues to flow even though the device failed, with no security processes running.
- **Fail closed:** data doesn’t continue to flow.
- Fail open is essential to think about when a device is inline or doing active monitoring.

**## Passive vs inline**

- **Passive monitoring:** devices communicate normally through a switch, and the switch sends a copy of the traffic to the IPS. Data can’t be blocked in real time, but it doesn’t cause downtime.
- **Inline:** when an IDS/IPS sits inline, all traffic passes through it.

**## What I mixed up**

- Fail open keeps data flowing with no security processes running. Fail closed stops the data flow. A passive monitoring device gets a copy of the traffic from the switch, so it can’t block in real time, but it causes no downtime because the real traffic doesn’t pass through it.

## Network Appliances

**## Jump server**

- Provides an access mechanism to a protected network. It’s inside the network and accessible from the outside.
- Highly secured, and a major security concern.
- People SSH, tunnel, or VPN to the jump server.

**## Proxies**

- Sit between the users and the external network. A proxy receives the user’s request and sends it on their behalf.
- Useful for caching, access control, URL filtering, and content scanning.
- **Explicit:** applications need to know how to use the proxy. **Transparent:** some proxies are invisible.
- One of the simplest proxies is **NAT**, a network-level proxy.
- Most proxies are **application proxies**. They may know only one application or a few, like HTTP, HTTPS, and FTP.
- **Forward proxy (internal proxy):** commonly used to protect and control user access to the internet.
- **Reverse proxy:** controls inbound traffic from the internet to your internal service.
- **Open proxy:** a third-party, uncontrolled proxy. A massive security concern, and often used to circumvent existing security controls.

**## Load balancer**

- Distributes the load across multiple servers, usually in large-scale implementations. Also provides fault tolerance, so server outages have no effect.
- **Active/active:** many are configured this way. It can distribute the load, perform TCP offload and SSL offload, provide caching, prioritize traffic, and do content switching.
- **Active/passive:** some servers are active while others are on standby. If an active server fails, a passive one takes over.

**## Sensors and collectors**

- They aggregate info from network devices.
- Data from sensors, like authentication logs, is sent to a collector, which feeds one database through a **SIEM**.

**## What I mixed up**

- A forward proxy controls and protects user access to the internet. A reverse proxy controls inbound traffic from the internet to an internal service. An open proxy is a third-party, uncontrolled proxy, and it’s a security concern because it’s often used to circumvent existing security controls.
- In active/active, all servers handle traffic, so the others keep going if one fails. In active/passive, some servers are on standby, and a passive one takes over when an active one fails.

## Port Security

**## What it is**

- Port security refers to the individual interfaces on a switch or connections to a wireless access point.
- Commonly used on wireless networks, but not limited to them. It can be added to switches.

**## EAP and 802.1X**

- **EAP (Extensible Authentication Protocol)** is an authentication protocol. Its most common integration is with **802.1X**.
- 802.1X is also called **Port-Based Network Access Control (NAC)**. You can’t gain access to the network unless you authenticate.
- Commonly used with RADIUS, LDAP, TACACS+, and Kerberos.

**## Three components**

- **Supplicant:** the client.
- **Authenticator:** the device that provides access.
- **Authentication server:** validates the client’s credentials.

**## What I mixed up**

- 802.1X has three components: the supplicant (the client), the authenticator (the device that provides access), and the authentication server (validates the client’s credentials). A device that hasn’t authenticated can’t gain access to the network.

## Firewall Types

**## Firewalls in general**

- A firewall is standard issue. It controls the flow of network traffic, and everything passes through it.
- Also provides corporate control of outbound and inbound data, control of inappropriate content, and protection against “evil” (anti-malware).

**## Network-based firewalls**

- Filter traffic by port number or application (OSI layer 4 or 7).
- Can encrypt traffic. Most can act as layer 3 devices, and they often sit at the ingress/egress of the network.

**## UTM (Unified Threat Management) / Web security gateway**

- Can do URL filtering, content inspection, malware inspection, spam filtering, CSU/DSU, router, switch, firewall, IDS/IPS, bandwidth shaper, and VPN endpoint.
- Many only function at layer 4 and look at port numbers.

**## NGFW (next-generation firewall)**

- Works at layer 7 and looks at applications. Requires advanced decodes.
- A network-based firewall. It has a list of known vulnerabilities, so it also works as an intrusion prevention system, and it does content filtering.

**## WAF (web application firewall)**

- Not like a “normal” firewall. It allows or denies traffic based on expected input.
- Can identify SQL injections.

**## What I mixed up**

- A layer 4 firewall filters on port numbers, and an NGFW filters at layer 7 by application. A WAF isn’t like a normal firewall. It allows or denies traffic based on expected input, which lets it catch attacks like SQL injection in web traffic.

## Secure Communication

**## VPN (Virtual Private Network)**

- Encrypts all private data traversing a public network.
- The **VPN concentrator** is the endpoint. It’s often integrated into a firewall and often used with client software.
- An **encrypted tunnel** keeps data private across the public network. It encrypts your data by adding headers and trailers. When the packet is received, it’s decrypted on the other side.

**## SSL/TLS VPN**

- Uses common protocols and runs over TCP port 443.
- Commonly used for remote access. It authenticates users and can be run from a browser.
- Provides on-demand access from a remote device.

**## Site-to-site IPsec VPN**

- Always on, or mostly always on. The firewalls often act as the VPN concentrators.

**## SD-WAN**

- Software-Defined Wide Area Network.
- Allows cloud-based applications to communicate directly with the cloud.

**## SASE (Secure Access Service Edge)**

- Updates secure access for cloud services, letting people connect securely from different locations.
- The security technologies are in the cloud, and SASE clients are on all devices.

**## What I mixed up**

- An SSL/TLS VPN is used for remote access, like a worker on a laptop, and runs over TCP port 443. A site-to-site IPsec VPN is always on and connects two offices.
- SD-WAN lets cloud-based applications communicate directly with the cloud. SASE updates secure access for cloud services so people can connect securely from different locations, with the security technologies in the cloud and SASE clients on all devices.

## Data Types and Classifications
'
**## Data types**

- **Regulated data:** managed by a third party.
- **Trade secrets:** an organization’s secret formulas, often unique to that organization.
- **Intellectual property:** may be publicly visible and carry copyright and trademark restrictions.
- **Legal info:** can be court documents. Personally identifiable info may be stored in a separate area.
- **Financial info:** should be private.
- **Human-readable data:** clear and obvious. **Non-human-readable data:** something like a barcode, which can’t be easily understood. Sometimes there’s a mix of both.
- **Proprietary data:** data that is the property of the organization.
- **PII (personally identifiable information):** something that can tie back to a person, like your name.
- **PHI (protected health information):** health info associated with an individual.

**## Data classifications**

- Not all data has the same level of categorization, and different levels require different security and handling.
- **Sensitive:** data like PII or PHI.
- **Confidential:** very sensitive, and requires approval to view.
- **Public / unclassified:** data anyone can see.
- **Private / classified:** restricted access, and may require an NDA.
- **Critical:** should always be available.

**## What I mixed up**

- PII is info that can tie back to a person, like a name. PHI is health info associated with an individual.
- Confidential data is very sensitive and requires approval to view. Private/classified data has restricted access and may require an NDA. Critical data should always be available.

## States of Data

**## Data at rest**

- Data on a storage device, like a hard drive.
- Encryption is necessary: whole disk encryption, database encryption, or file-level encryption.
- You can also apply permissions, like ACLs.

**## Data in transit**

- Data moving across the network.
- There isn’t much protection as it travels. Ways to protect it: a firewall or IPS (allow good traffic through, deny unusual traffic), and transport encryption through **TLS** or **IPsec**.

**## Data in use**

- Data actively being processed in memory, like system RAM.
- It’s almost always decrypted so it can be seen, which is why attackers like to attack data in use.

**## Data sovereignty**

- Data stored inside a country is subject to all of that country’s laws. These laws may prohibit where data can be stored.

**## Geolocation**

- It’s important to know where data is stored and where it’s being accessed from.
- Ways to identify location: GPS, 802.11, etc. Knowing the location can be used to manage data access or the level of control.

**## What I mixed up**

- Data in use is the hardest state to protect because it’s almost always decrypted in memory so it can be seen, which is why attackers like to attack it. Data at rest is protected with encryption, and data in transit with a firewall/IPS or transport encryption (TLS or IPsec).

## Protecting Data

**## Geographic restrictions**

- Restrict by subnet or IP address.
- Accuracy of location: **GPS** is the most accurate, **802.11** is a little less accurate, and **IP address** is not very accurate.
- **Geofencing** allows or restricts access when the user is in a particular location.

**## Why it’s hard**

- Protecting data is a primary job task. It’s difficult because data is everywhere: on a storage drive, on the network, or in a CPU.

**## Encryption**

- Takes plaintext and turns it into ciphertext. You can also decrypt it, so it’s a two-way street.
- Encrypted data looking very different from unencrypted data is called **confusion**.

**## Hashing**

- Represents data as a short string of text. A one-way trip that provides integrity.

**## Obfuscation**

- Makes something understandable very difficult to understand. It can turn perfectly readable code into nonsense. Attackers can also use it to hide malicious code.
- **Masking:** a type of obfuscation. Protects PII and other sensitive data. It doesn’t automatically mask the data in storage, only in view.
- **Tokenization:** replaces sensitive data with a non-sensitive placeholder, a token. It isn’t encryption or hashing.

**## Segmentation**

- Many organizations use a single data source, one large database, so one breach puts all the data at risk.
- Segmentation splits the data into different areas, so you can set security based on the value of the data.

**## Permission restrictions**

- Control access to an account, using the authentication process.

**## What I mixed up**

- Masking leaves the original data stored unchanged and only masks what’s shown in the view. Tokenization replaces the sensitive data with a placeholder that isn’t mathematically related to it.
- Keeping everything in one large database means one breach exposes all the data.

## Resiliency

**## High availability**

- Essential. Redundancy doesn’t always mean always available.
- **HA** is always on, always available. It includes many different components but comes with additional costs.

**## Server clustering**

- Two or more servers, but users only see one device.
- Allows an easy increase in capacity and availability. The servers usually run the same OS.

**## Load balancing**

- One central load balancer distributes the load between individual servers. The servers can run different operating systems.
- The load balancer can add or remove devices based on need.

**## Site resiliency**

- Physical. When a disaster occurs, the organization can move its entire data center to another location, keep operating normally during the disaster, and move back to the original data center afterward.
- **Hot site:** an exact replica. Constantly stocked with hardware, with applications and software duplicated.
- **Cold site:** no hardware, just an empty building. You have to provide everything: people, hardware.
- **Warm site:** a middle ground. May contain some hardware, but you still have to move things over for everything to operate.
- These sites are usually far away so that something like a hurricane or flood doesn’t affect the recovery site. This can be a logistical issue.

**## Platform diversity**

- Many vulnerabilities are linked to an OS like Windows or Linux. Using different operating systems means one OS risk doesn’t affect everything.

**## Multi-cloud**

- Plan for cloud outages. Same idea as OS risk: spread across cloud providers to maintain uptime and availability.

**## COOP (continuity of operations planning)**

- A failback plan that provides an alternative. It needs to be documented and tested before it’s implemented.

**## What I mixed up**

- A hot site recovers fastest and costs the most. A cold site has no hardware, so you have to provide everything: people and hardware.
- Server clustering is two or more servers that appear to users as one device, usually running the same OS. A load balancer is one central device that distributes the load between individual servers, which can run different operating systems.

## Capacity Planning

**## What it is**

- Capacity planning means matching supply to demand.
- **Too much demand** causes application slowdowns and outages. **Too much supply** means you spend too much money.
- It requires a balanced approach: the right amount of people, appropriate technology, and the best infrastructure.

**## People**

- Important, especially for call centers. Hiring is expensive.

**## Technology**

- It’s a necessity to pick technology that has scalability.
- **Web servers:** distribute the load with a load balancer.
- **Database services:** split the databases to increase capacity.

**## Infrastructure**

- The underlying framework: CPU, network, storage, physical devices, and cloud-based devices.

**## What I mixed up**

- Too much demand causes slowdowns and outages, and too much supply wastes money. For a web server, use a load balancer. For a database, split the databases to increase capacity.

## Recovery Testing

**## What it is**

- It’s essential to test yourself before an actual event. Use well-defined rules of engagement and evaluate the response.

**## Tabletop exercises**

- A full-scale disaster drill can be costly and time-consuming. You don’t have to physically go through it.

**## Failover test**

- Checks whether redundant configurations can switch over if there’s a failure.
- Requires a redundant infrastructure, which may include firewalls, switches, and routers.

**## Simulations**

- Testing with a simulated event, like a phishing email sent to your employees to see if they click the links.
- This tests internal security, including whether the email even makes it to the employees.

**## Parallel processing**

- A process split across multiple (parallel) CPUs. Provides improved performance and recovery.

**## What I mixed up**

- A failover test checks whether redundant configurations actually switch over after a failure. A simulation tests with a simulated event, like a phishing email sent to employees to see whether it gets through and whether they click. (Tabletop: confirm in the video and add your own wording.)

## Backups

**## Onsite vs offsite**

- **Onsite backup:** the data and the backup media are in the same place. The data is immediately available, and it’s less expensive.
- **Offsite backup:** the data is transferred to a separate location, over the internet or a WAN link. It’s available after a disaster.
- Most companies use both.

**## Frequency**

- How often do you back up? It may differ for different devices, and there may be multiple backup sets (daily, weekly, monthly). This requires significant planning.

**## Encryption**

- Vital. A history of data sits on the backup media, which makes it an easy target for an attacker, especially in transit.
- Especially important for cloud backups and storage.

**## Snapshots**

- Very popular with virtual machines and cloud-based backups. They give you an instant backup with one click.
- Since it’s such an easy process, it’s a good idea to take a snapshot every 24 hours.

**## Recovery testing**

- Essential: test your backups to make sure they work.
- Once data is restored you’re only halfway. Make sure the applications and data can actually be used.

**## Replication**

- Takes a single source of data and copies it to multiple locations, almost in real time.
- Data is always available and recoverable, and it can be stored locally for all users.

**## Journaling**

- Corrupted data can make recovery complicated and time-consuming. That’s why journaling is essential.
- The data is first written to a journal. Once it’s written, it can be copied into the final version.

**## What I mixed up**

- Onsite backups are cheaper and available immediately. Offsite backups keep data available after a disaster at the main site. Encryption matters more for cloud backups because the data travels over the internet and sits on someone else’s infrastructure, and a backup holds a history of the data, which makes it an easy target.
- Replication keeps data available by copying it to multiple locations almost in real time. A snapshot is an instant, one-click backup. Journaling writes data to a journal first and copies it into the final version afterward, so a failure partway through doesn’t corrupt the final copy.

## Power Resiliency

**## What it is**

- Power is the foundation of technology, so it’s important to engineer and plan properly for outages.
- There are ways to mitigate power outages both short term and long term.

**## UPS (uninterruptible power supply)**

- A short-term power outage solution.
- **Types:** offline/standby, line-interactive, and online/double-conversion.
- **Features:** auto shutdown, battery capacity, outlets, and phone-line suppression.

**## Generators**

- A long-term power outage solution. Capable of powering an entire building.
- Most organizations use both a UPS and a generator, since a generator can take a little while to power up.

**## What I mixed up**

- A UPS is the short-term solution and a generator is the long-term one. Most organizations use both, because a UPS gives immediate power during an outage while a generator can take a little while to start.

## Secure Baselines

**## What it is**

- The security of an application environment should be well defined. This includes a baseline, firewall settings, patch levels, and OS file versions, and it may require constant updates.
- Security baselines are often available from the manufacturer and can be modified for your specific needs.
- Many OS settings have extensive options and configs.

**## Deploying baselines**

- Usually managed through a centrally administered console, but some may need multiple deployment mechanisms, such as **AD group policy** or **MDM**. Automation is the key.

**## Maintaining baselines**

- Once deployed, you need to maintain these best practices. Many baselines require constant updates because of changes: new vulnerabilities, updated applications, or a new OS being installed.
- It’s necessary to test and measure to avoid conflicts.

**## What I mixed up**

- Baselines need constant updates because of new vulnerabilities, updated applications, and new OS installations. Testing and measuring before rollout avoids conflicts.
- Automation is the key to deploying baselines: it lets them roll out faster and at the same time. They’re usually deployed from a centrally administered console, using mechanisms like AD group policy or MDM.

## Hardening by Device Type

**## What it is**

- No system is secure with its default configurations.
- Hardening guides are specific to the software or platform.

**## Mobile devices**

- Must be hardened. Updates are critical because of bug fixes and patches.
- Segmentation can protect data: company data and user data are separated.
- Controlled with an **MDM (mobile device manager)**.

**## Workstations**

- Hardening user desktops and laptops is essential.
- Constant monitoring and updates are essential. Automated monthly updates are common.
- Removing unnecessary software is essential.

**## Network infrastructure (switches / routers)**

- Change and configure the default configs.
- Check with the manufacturer for updates and patches.

**## Cloud management workstation**

- Secure it with least privilege and a configured **EDR**.
- Always have a backup in case of an outage.

**## Servers**

- Always update systems, including service packs and security patches.
- Use proper passwords for user accounts, limit network access, harden security, and run anti-malware/antivirus.

**## SCADA / ICS**

- **SCADA (Supervisory Control and Data Acquisition)** manages large-scale equipment and requires extensive segmentation.

**## Embedded systems**

- A challenge to harden because the hardware and software are designed for a specific function.
- Can be difficult to upgrade or patch. If there is a patch, always try to update.
- Also a good idea to put them on their own network behind a firewall.

**## RTOS (real-time operating system)**

- Should be isolated and run with the minimum amount of services.
- Use a secure configuration through a host-based firewall.

**## IoT**

- Weak defaults, so deploy patches as soon as possible.
- Segment IoT devices on their own network.

**## What I mixed up**

- Embedded systems are difficult to patch, but I should still update when a patch exists. Embedded systems, RTOS, and IoT devices are all hardened by isolating them on their own network with a firewall. RTOS also runs the minimum amount of services, and IoT needs patches deployed as soon as possible.

## Securing Wireless and Mobile

**## Site surveys**

- Determine the existing wireless landscape.
- One of the first steps is identifying existing access points. If some are outside your control, you may have to work around their existing frequencies.
- Plan for ongoing site surveys.
- **Heat maps** are a good way to visualize a site survey and show signal strengths.
- Wireless survey tools give a summary of signal coverage and can identify potential interference. Operating systems have built-in tools, and there are a number of third-party tools. You can also use a **spectrum analyzer**.

**## MDM (mobile device manager)**

- Useful for managing company-owned or user-owned mobile devices.
- Centralized management of mobile devices. Can set policies on apps, data, the camera, etc., and can manage access control.

**## Deployment models**

- **BYOD (bring your own device):** difficult to secure because the employee owns the device.
- **COPE (corporate-owned, personally enabled):** the company buys the device and assigns it to the employee. The organization keeps full control, and the info is protected using corporate policies.

**## Mobile / cellular concerns**

- Mobile devices create a challenge, and cellular networks are separated into “cells.”
- Security concerns include location tracking and traffic monitoring.

**## Wi-Fi**

- Wi-Fi devices have similar concerns. Make sure your data is encrypted.
- Attackers can be in the general area and perform an on-path attack or a DoS.

**## Bluetooth**

- **PAN (personal area network):** connects our devices, including mobile devices.
- Make sure you don’t connect to unknown Bluetooth devices.

**## What I mixed up**

- With BYOD the employee owns the device. With COPE the company buys the device and assigns it to the employee, so it keeps full control and protects the info with corporate policies.
- A heat map shows signal strengths across a space. Site surveys need to be ongoing because the wireless landscape changes, including interference and access points outside my control.
- An attacker in the general area of a Wi-Fi network can perform an on-path attack or a DoS. With Bluetooth, don’t connect to unknown devices.

## Wireless Security Settings

**## What it is**

- Authenticating users before granting access to the wireless network is essential.
- All communication also needs to be confidential (encrypted) and verified for integrity with a **MIC (message integrity check)**.

**## WPA2**

- Has a brute force security concern.
- **PSK** means pre-shared key. Once you have the PSK, you have everyone’s wireless key.

**## WPA3**

- What we use now.
- **GCMP** was used to stop brute force attacks through better encryption, with a MIC using GCMP (Galois Message Authentication Code).
- There’s no four-way handshake or hash, which means no more brute force attacks.
- **SAE (Simultaneous Authentication of Equals):** uses a Diffie-Hellman-derived key exchange with an authentication component. Everyone uses a different session key.

**## Network authentication**

- Provided in two ways: a pre-shared key (PSK), or centralized authentication using 802.1X.
- You provide security by configuring the authentication on the WAP or wireless router.
- **WPA3-Personal** is for home use. **WPA3-Enterprise** is for office use.
- The difference: Personal uses a PSK, and Enterprise uses 802.1X.

**## AAA, RADIUS, 802.1X, EAP**

- **AAA framework:** authentication (username/password), authorization (what resources you have access to), and accounting (resources used, like login time).
- **RADIUS (Remote Authentication Dial-In User Service):** a common AAA protocol. Provides centralized authentication for users and is available on almost any OS.
- **802.1X** works on wireless and wired networks, and is used in conjunction with an access database.
- **EAP (Extensible Authentication Protocol):** flexible and common. It integrates with 802.1X.

**## What I mixed up**

- A PSK’s weakness is that once an attacker has the shared key, they have everyone’s wireless key. SAE changes that by giving everyone a different session key.
- WPA3-Personal is for home and uses a PSK. WPA3-Enterprise is for the office and uses 802.1X.
- RADIUS is the AAA protocol, and 802.1X controls access to the network port.

## Application Security

**## Input validation**

- Checks for the expected input across many forms. It should check for and correct all input (**normalization**).

**## Cookies**

- Info stored inside your browser, used for tracking, personalization, and session management.
- Many browsers use **secure cookies**, which are only sent over secure protocols like HTTPS.
- Sensitive info shouldn’t be saved in cookies.

**## SAST (static application security testing)**

- Tests for security vulnerabilities like buffer overflows or database injections.
- Not everything can be found by the analyzer, and its output may not be perfect.

**## Code signing**

- Lets you check that the code was sent by the proper developer, who provides a digital signature.

**## Sandboxing**

- The application can’t access unrelated resources. Commonly used in deployment.
- Used in many ways: VMs, mobile phones, browser iframes, and UAC (User Account Control).

**## Monitoring**

- Essential. It provides real-time info, shows blocked attacks, provides extensive logs, and detects anomalies.

**## What I mixed up**

- SAST tests for security vulnerabilities like buffer overflows and database injections, but it can’t be fully relied on because it won’t find everything and its output may not be exact.
- Code signing proves the code came from the proper developer, who provides a digital signature. Sandboxing keeps an application from accessing unrelated resources.

## Asset Management

**## Acquisition / procurement**

- The purchasing process: a request from the user, then negotiation with a supplier, the purchase, an invoice, and payment.

**## Tracking**

- A central asset tracking system holds the ownership and classification of hardware or software.
- Asset tracking involves an inventory of every asset, including every hardware component. It helps associate a support ticket with every device, and allows for **enumeration** (listing all the parts of an asset).

**## Disposal and reuse**

- When reusing a device, you may need to remove all company data. This is done through **sanitization**. The sanitization method depends on the use case: completely disposing of the device, or reusing it.
- To guarantee no one ever sees the data, use **physical destruction**. For large-scale applications this is often done by a third-party vendor, who destroys the assets and confirms with a **certificate of destruction**.

**## Data retention**

- Involves copies, versions of copies, the lifecycle of data, and purging old data.
- Also involves regulatory compliance and operational needs, and can differ by type and application.

**## What I mixed up**

- Sanitization removes the company data so a device can be reused. Physical destruction is for when no one should ever be able to see the data. A certificate of destruction is the third-party vendor’s confirmation that the assets were destroyed.

## Vulnerability Scanning

**## What it is**

- A vulnerability scan determines whether a machine is susceptible to an attack. It’s usually minimally invasive compared to a penetration test. An example is a port scan.
- Good at identifying systems. Scans can come from outside and inside, and they try to gather as much info as possible.

**## SAST (static application security testing)**

- Helps identify vulnerabilities written in the code, like buffer overflows and database injections.
- Not everything can be identified, such as authentication security or insecure cryptography. You still need to verify everything.

**## Dynamic analysis / fuzzing**

- Designed to put random input into an application.
- It looks for the application to respond in an out-of-the-ordinary way, like an application crash or a server error.
- Fuzzing can be very time-consuming and resource-heavy.

**## Package monitoring**

- Some applications are provided as a package, like an executable. That’s where package monitoring comes from.
- Confirm the package is legitimate and safe before deployment.

**## What I mixed up**

- SAST is static. It finds vulnerabilities written in the code, like buffer overflows and database injections, without running the application. It misses things like authentication security and insecure cryptography. Fuzzing is dynamic analysis. It feeds random input to a running application and looks for crashes or server errors, and it’s time-consuming and resource-heavy.

## Threat Intelligence

**## What it is**

- Research the threat and the threat actors too. Data is everywhere, and you need to make decisions based on this threat intelligence.

**## OSINT (open-source intelligence)**

- Publicly available to everyone. Can come from the internet, government data, or commercial data.

**## Proprietary / third-party intelligence**

- Someone else has already compiled the threat info. They provide threat intelligence services like threat analytics or correlation across different data sources, plus constant threat monitoring.

**## Sharing**

- Organizations can work together to share public and classified data, including critical security details. An example is the **CTA (Cyber Threat Alliance)**.

**## Dark web**

- An overlay network that uses the internet. You can find a number of hacking groups and services, and forums for their activity.

**## What I mixed up**

- OSINT is publicly available to everyone (internet, government, or commercial data). Proprietary/third-party intelligence is compiled by someone else, with analytics, correlation, and constant monitoring. The CTA is a group of organizations that share critical security details.

## Penetration Testing

**## What it is**

- A **pentest (penetration test)** simulates an attack on our system.
- It’s similar to vulnerability scanning, but you actually try to exploit the vulnerabilities. It’s often a compliance mandate.
- You’ll only be sure you’re vulnerable if you can bypass security.

**## Rules of engagement**

- Before starting, you must have rules of engagement. They list the scope and purpose of the test, the type of testing, the schedule, and specific rules.

**## Be careful**

- Penetration testing needs care so you don’t cause a DoS or data loss. You may need to try different vulnerability types.

**## The process**

- Initial exploitation → lateral movement → persistence → the pivot (moving on to other systems).

**## Disclosure**

- It takes time to fix a vulnerability, so it’s essential to have a **responsible disclosure** program.
- **Bug bounty programs** reward people who find bugs.

**## What I mixed up**

- A pentest is more invasive than a vulnerability scan, and it tells me whether I can actually be broken into.
- Rules of engagement list the scope and purpose, the type of testing, the schedule, and specific rules.
- Pivoting means using a compromised system to reach other systems. Lateral movement is not user-to-user, which is horizontal privilege escalation.
- Responsible disclosure gives the vendor time to fix a vulnerability before details go public. A bug bounty program rewards people who find bugs. They aren’t hired.

## Analyzing Vulnerabilities

**## False results**

- A challenge with vulnerabilities is dealing with **false positives**: a vulnerability that’s identified but doesn’t really exist. This is different from a low-severity vulnerability, which does exist.
- **False negatives** occur when a vulnerability exists but isn’t detected.

**## Planning a scan**

- When planning a vulnerability scan, update to the latest signatures and work with the manufacturer.
- Scans can check various things: application scans, web application scans, and network scans.

**## Rating vulnerabilities**

- Not every vulnerability is the same. They’re rated high, medium, and low.
- **CVSS (Common Vulnerability Scoring System):** rates a vulnerability on a scale. It’s an industry collaboration.
- **CVE (Common Vulnerabilities and Exposures):** another way to spot vulnerabilities.

**## Determining how risky it is**

- **Exposure factor:** rated as a percentage.
- **Environmental variables:** for example, whether it’s in the cloud or on a single system.
- **Industry / organizational impact** can also change the rating.

**## Managing security patches**

- You need to set a priority.
- **Risk tolerance:** how much risk an organization is willing to take.
- The timing of security patches is also essential, and testing takes time.

**## What I mixed up**

- A false positive is a vulnerability the scanner flags that doesn’t exist, and a low-severity vulnerability is real but ranks low. A false negative is more dangerous, because a real vulnerability exists and the scanner misses it.
- CVSS scores vulnerabilities, and CVE is a list of commonly known ones.
- Patch priority depends on exposure factor, environmental variables, and industry or organizational impact. (Add risk tolerance in your own words.)

## Vulnerability Remediation

**## Patching**

- The most common mitigation technique. Usually scheduled, but a zero-day can be an unscheduled patch.

**## Cybersecurity insurance**

- Helps recover lost revenue, data recovery costs, etc., but doesn’t cover everything.

**## Segmentation**

- Limits the scope by separating devices onto their own networks or VLANs, so a breach has limited scope. An **NGFW** is a great way to implement this.
- **Physical segmentation:** completely separate devices.
- **Logical segmentation (VLANs):** separated logically, not physically. VLANs can’t communicate without a layer 3 device or router.

**## When you can’t patch**

- Compensate by disabling the service, revoking access to the application, limiting external access, or modifying internal security controls and software firewalls.

**## Validating the patch**

- Perform a vulnerability scan, an audit, and verify.

**## Reporting**

- Large organizations need a reporting system for ongoing checks, including ongoing and newly discovered vulnerabilities.

**## What I mixed up**

- If a system can’t be patched, I can compensate by revoking access to the application or disabling the service. I validate a patch afterward with a vulnerability scan and an audit.
- Segmentation limits a breach by putting devices on their own networks. Physical segmentation uses completely separate devices. Logical segmentation (VLANs) separates them without separate hardware, and VLANs can’t communicate without a layer 3 device or router.

