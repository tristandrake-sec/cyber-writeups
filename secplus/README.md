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