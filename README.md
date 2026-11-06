<!--
author:   ICoBC - International Council on Badges and Credentials
email:    info@icobc.net
version:  1.0.0
language: en
narrator: UK English Female
comment:  A knowledge course on why credentials that stay valid for decades face cryptographic ageing, which migration options exist for signatures and keys, and when to start planning.
@style
:root { --icobc-navy:#02375B; --icobc-orange:#F78222; --icobc-cyan:#5DCAE7; --icobc-lime:#B1CF37; --icobc-mist:#F1F5F8; --icobc-line:#D8E2E9; --icobc-muted:#4F6576; }
body { font-family: "Open Sans", Arial, sans-serif; }
h1, h2, h3, h4 { color: var(--icobc-navy); }
a { color: var(--icobc-navy); }
table th { background: var(--icobc-mist); color: var(--icobc-navy); }
blockquote { border-left: 4px solid var(--icobc-orange); background: var(--icobc-mist); padding: 8px 16px; }
@end
-->

# Long-Lived Credentials and Post-Quantum Cryptography

*Planning for signatures that must outlast their algorithms.*

## About this course

**Course ID:** ICB-H06. **Framework alignment:** ICoBC Credentialing Skills Framework (ICSF), skill SECP "Security, privacy and data protection" (VRITE pillar: Trustworthiness), level L4 "Assure", stage K "Knowledge".

At level L4, a person leads threat modelling and fraud prevention for credential systems and advises on key management and long-term validity. At stage K, the focus is understanding: concepts, rules, standards and the reasons behind them. After this course you can explain and recognise the issues. You are not asked to implement a migration.

**Who this course is for**

- HR and learning technology owners who commission or run credential programmes.
- Education IT and credential operations staff who run issuing and verification services.
- Members of the standards and wallet community who shape how credentials are signed, stored and checked.

**Prerequisite:** ICB-P07 Open Badges 3.0 and Verifiable Credentials: Hands-on Lab. You should already know what an issuer, a holder, a verifier, a signature and a public key are.

**Learning outcomes**

1. Explain why credentials valid for decades face cryptographic ageing.
2. Describe migration options for signatures and keys.
3. Identify when to start planning a migration.

**Workload:** self-paced, about 1.5 hours of notional learning. Live or workshop elements are described in facilitator notes. They are optional extras for a group setting and are not needed for the badge.

**Assessment:** a final knowledge check with 10 single-choice questions. Each module also has a short quiz for practice.

**Badge:** "Long-Lived Credentials and Post-Quantum Cryptography (Knowledge, L4)", alignment code ICSF-SECP-L4-K. Evidence: passed knowledge check.

**A note on status.** Post-quantum cryptography is on the ICoBC watch list. Standards have been published for some algorithms. Migration in credential ecosystems is not yet planned at scale. Status as of November 2026; check before publishing.

| Outcome | Module | How it is assessed |
|---|---|---|
| 1. Explain why credentials valid for decades face cryptographic ageing | The problem | Module 1 quiz, final knowledge check questions 1 to 4 |
| 2. Describe migration options for signatures and keys | Options | Module 2 quiz, final knowledge check questions 5 to 7 |
| 3. Identify when to start planning a migration | Planning | Module 3 quiz, final knowledge check questions 8 to 10 |

<details>
<summary>Facilitator notes</summary>

If you run this course as a workshop, schedule 60 minutes of live discussion on top of the self-paced part. Ask each participant to bring a short list of the credential types their organisation issues or verifies, with the intended validity period of each. Use this list in the practice activities. Participants from companies, education providers and the standards community often hold different assumptions about validity, so mixed groups work well.

</details>

## The problem

### Credentials live longer than algorithms

A credential is a statement that someone holds a skill, a qualification or a role. A digital credential carries a digital signature. The signature lets a verifier check two things: who issued the credential, and that nobody has changed it since.

The signature relies on cryptography, and cryptography ages. An algorithm is chosen because, at the time, nobody can forge signatures with it at a realistic cost. That judgement can change. Researchers find weaknesses, computers become faster, and new kinds of computers appear. Standards bodies then advise moving to something stronger.

Many credentials are meant to last much longer than any single algorithm is recommended. Think of a degree certificate, a safety licence, a professional registration or a long-service record. A learner may need to prove such a credential 20, 30 or 40 years after it was issued. The lifetime of the credential and the lifetime of the algorithm are different things, and the credential can outlive the algorithm by a wide margin.

Three terms help here:

- **Validity period:** how long the issuer states the credential is valid. Some credentials never expire.
- **Verification window:** the period in which somebody may want to check the credential. This can be much longer than the validity period. A degree that never expires may be checked for the whole career of its holder and beyond.
- **Algorithm lifetime:** the period in which the signature algorithm and key size are considered safe to use.

The risk appears when the verification window is longer than the algorithm lifetime. At that point, a signature that was sound at issue time may no longer give the same assurance.

<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Timeline: credential life compared with algorithm life</title>
  <desc>A horizontal timeline from issue to 40 years later. A long navy bar shows a credential that may be checked for 40 years. A shorter orange bar shows a signature algorithm recommended for about 15 years. A label marks the gap between the end of algorithm recommendation and the end of the credential's verification window. The values are illustrative.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <text x="40" y="40" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="bold" fill="#02375B">Credential life and algorithm life (illustrative)</text>
  <line x1="60" y1="360" x2="740" y2="360" stroke="#D8E2E9" stroke-width="2"/>
  <line x1="60" y1="350" x2="60" y2="370" stroke="#02375B" stroke-width="2"/>
  <line x1="740" y1="350" x2="740" y2="370" stroke="#02375B" stroke-width="2"/>
  <line x1="332" y1="350" x2="332" y2="370" stroke="#02375B" stroke-width="2"/>
  <text x="60" y="395" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">Year 0: issue</text>
  <text x="332" y="395" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">Year 16</text>
  <text x="740" y="395" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">Year 40</text>
  <rect x="60" y="110" width="680" height="50" rx="6" fill="#02375B" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="141" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#FFFFFF" text-anchor="middle">Credential: may be checked for 40 years</text>
  <rect x="60" y="200" width="272" height="50" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="196" y="231" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B" text-anchor="middle">Algorithm: recommended 16 years</text>
  <rect x="332" y="200" width="408" height="50" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2" stroke-dasharray="6 4"/>
  <text x="536" y="231" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B" text-anchor="middle">Gap: 24 years of weaker assurance</text>
  <text x="400" y="300" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#4F6576" text-anchor="middle">Orange = employer-issued credential example. Numbers are illustrative.</text>
</svg>

### Why quantum computers matter

Most digital signatures used today in credentials rely on mathematical problems that are hard for ordinary computers. Examples are factoring large numbers and computing discrete logarithms on elliptic curves. Researchers have shown that a sufficiently large quantum computer could solve these problems efficiently using a known method, Shor's algorithm. Such a computer would be able to derive a private key from a public key, and then forge signatures.

Whether and when such a computer will exist is uncertain, and this course does not predict a date. What matters for planning is that the possibility is taken seriously by standards bodies and public authorities. They have run public processes to select new algorithms that resist attack by quantum computers. This area is called **post-quantum cryptography**. Standards have been published for some algorithms. Migration in credential ecosystems is not yet planned at scale. Status as of November 2026; check before publishing.

<!-- VERIFY: confirm the current names and publication status of the post-quantum signature standards from the national standards body before publishing. -->

Two attack ideas are worth knowing:

- **Forgery after the fact.** If an attacker can later break an old algorithm, they could create a fake credential that appears to be signed by the issuer. If the credential carries no trustworthy proof of when it was signed, a verifier cannot tell the fake from a real old one.
- **Harvest now, break later.** This idea mostly concerns confidentiality. An attacker records encrypted data today and decrypts it once the technology exists. It matters for credentials when personal data in them is encrypted or sent over a channel that is recorded.

Signatures and encryption are different tools, and they need different migration plans. This course concentrates on signatures and the keys that support them, because that is where long-lived credentials are most exposed.

### Cryptographic ageing in practice

Quantum computing is one reason algorithms age, and not the only one. Algorithms also age through:

- new mathematical attacks on the algorithm itself;
- faster ordinary computers, which make shorter keys unsafe;
- flaws in software libraries or hardware that hold the keys;
- changes in regulation or in the rules of a trust framework.

Cryptographic agility is the ability to change algorithms without redesigning the whole system. A credential system that hard-codes one algorithm everywhere has low agility. A system that records the algorithm in each credential and lets verifiers support several has higher agility.

Ask a simple question of any credential type: "If the signature algorithm were declared unsafe next year, what would happen to every credential already issued?" The honest answer shows the exposure.

**Worked example: The corporate academy safety certificate**

A corporate academy in a large manufacturing firm issues a "Machine safety operator" credential. The compliance officer says employees may need to show it for the whole length of a 35-year career, and that former employees may need it for liability questions for longer. The academy signs credentials with a widely used elliptic curve signature algorithm.

The academy's credential operations lead lists three dates, all illustrative: issue in year 0, the algorithm's recommended retirement around year 15, and the end of the verification window around year 40 or later. She sees that in years 15 to 40, a verifier would be trusting a signature produced with an algorithm that official guidance no longer recommends. She decides that the academy needs a plan, even though no break has happened. She records this as a risk on the programme risk register, with the HR learning technology owner as accountable role.

**Practice activity: Compare two lifetimes**

Choose one credential type from your own organisation, or use the corporate academy certificate above. Write down:

1. the intended validity period;
2. the longest realistic verification window;
3. the signature algorithm in use today, if you know it, and when official guidance suggests retiring it;
4. whether the verification window is longer than the algorithm lifetime.

If you do not know the algorithm, write "unknown" and note who could tell you. Naming that person is a useful result.

<details>
<summary>Facilitator notes</summary>

In a group session, ask each person to place their credential type on a wall timeline using sticky notes in two colours, one for credential life and one for algorithm life. Discuss which credentials show the biggest gaps. Keep the talk on concepts. Do not let the group drift into predicting dates for quantum computers.

</details>

### Check your understanding: The problem

**Question 1.** What does the term "verification window" describe?

[( )] The time an issuer needs to sign a credential.
[(X)] The period in which someone may want to check a credential.
[( )] The time a wallet takes to display a credential.
[( )] The period in which a private key is stored in a vault.
[[?]] Think about how long a degree certificate may be relevant to its holder.
****
The verification window is the period in which a credential may be checked. It can be much longer than the validity period, and it is the key figure when comparing credential life with algorithm life.
****

**Question 2.** Why can a credential with no expiry date still face cryptographic ageing?

[( )] Because credentials without expiry are never signed.
[( )] Because wallets delete old credentials automatically.
[(X)] Because the signature algorithm may be considered unsafe long before the credential stops being relevant.
[( )] Because issuers must renew every credential each year.
[[?]] Compare the life of the credential with the life of the algorithm.
****
A credential without expiry may be checked for decades. The algorithm that signed it may be declared unsafe much earlier, so the assurance the signature gives can weaken over time.
****

**Question 3.** Which statement about quantum computers and credential signatures is accurate?

[( )] A date for a break of current signatures is known and fixed.
[( )] Quantum computers affect only the colour of a badge image.
[( )] Post-quantum cryptography has no published standards at all.
[(X)] A large enough quantum computer could break signature algorithms based on factoring or elliptic curve problems, so standards bodies have worked on new algorithms.
[[?]] The status note in this module says standards exist for some algorithms.
****
The risk comes from a known method that a large quantum computer could run against widely used signature algorithms. Nobody can fix a date, but standards bodies have published standards for some post-quantum algorithms.
****

**Question 4.** What does cryptographic agility mean?

[( )] Using the fastest algorithm available at all times.
[( )] Storing every key in the same place.
[( )] Issuing credentials only to a small group of people.
[(X)] The ability to change algorithms without redesigning the whole system.
[[?]] Think about the word "agile" applied to how a system can change.
****
Cryptographic agility means a system can move to new algorithms without a full redesign, for example because the algorithm is recorded in each credential and verifiers can support several.
****

## Options

### Where the weak points are

A credential system has several places where cryptography does its work. Before choosing a migration option, list them:

- **The issuer's signing key.** It signs each credential. If it is exposed or its algorithm is broken, forged credentials become possible.
- **The signature on each credential.** It stays attached to the credential for as long as the credential exists.
- **Key discovery and identifiers.** Verifiers find the issuer's public key through an identifier or a published document. If this link is tampered with, verifiers may trust the wrong key.
- **Status and revocation information.** Lists or services that say whether a credential is still valid also use signatures or secure channels.
- **Wallets and holder keys.** If the holder proves control of a credential with a key, that key also uses an algorithm that can age.
- **Transport.** The channels that carry credentials between parties use encryption.

A migration plan works through each of these. Changing only the issuing key and leaving the rest untouched can leave weak links in place.

<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Four migration options for long-lived credentials</title>
  <desc>Four labelled boxes arranged in a row. Option A: keep and monitor. Option B: re-issue with a new algorithm. Option C: add a second signature, called hybrid or dual signing. Option D: add a trusted timestamp or archive proof. An arrow from each box points to a navy circle labelled long-term trust. The options are not ranked.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#F1F5F8"/>
  <text x="40" y="40" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="bold" fill="#02375B">Four migration options</text>
  <rect x="30" y="80" width="170" height="110" rx="6" fill="#FFFFFF" stroke="#02375B" stroke-width="2"/>
  <text x="115" y="115" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="bold" fill="#02375B" text-anchor="middle">A. Keep</text>
  <text x="115" y="140" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">and monitor</text>
  <text x="115" y="165" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#4F6576" text-anchor="middle">review on a schedule</text>
  <rect x="220" y="80" width="170" height="110" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="305" y="115" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="bold" fill="#02375B" text-anchor="middle">B. Re-issue</text>
  <text x="305" y="140" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">with a new</text>
  <text x="305" y="165" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">algorithm</text>
  <rect x="410" y="80" width="170" height="110" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="495" y="115" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="bold" fill="#02375B" text-anchor="middle">C. Hybrid</text>
  <text x="495" y="140" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">two signatures,</text>
  <text x="495" y="165" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">old and new</text>
  <rect x="600" y="80" width="170" height="110" rx="6" fill="#B1CF37" stroke="#02375B" stroke-width="2"/>
  <text x="685" y="115" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="bold" fill="#02375B" text-anchor="middle">D. Prove time</text>
  <text x="685" y="140" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">timestamp or</text>
  <text x="685" y="165" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">archive proof</text>
  <line x1="115" y1="190" x2="400" y2="320" stroke="#02375B" stroke-width="2"/>
  <line x1="305" y1="190" x2="400" y2="320" stroke="#02375B" stroke-width="2"/>
  <line x1="495" y1="190" x2="400" y2="320" stroke="#02375B" stroke-width="2"/>
  <line x1="685" y1="190" x2="400" y2="320" stroke="#02375B" stroke-width="2"/>
  <circle cx="400" cy="350" r="45" fill="#02375B" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="346" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#FFFFFF" text-anchor="middle">Long-term</text>
  <text x="400" y="364" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#FFFFFF" text-anchor="middle">trust</text>
  <text x="400" y="425" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#4F6576" text-anchor="middle">Options can be combined. They are not ranked.</text>
</svg>

### Four families of option

There is no single correct migration. Four families of option exist, and organisations often combine them.

**A. Keep and monitor.** The issuer continues with the current algorithm and sets up a regular review. It watches guidance from standards bodies and public authorities, and keeps an inventory of keys and credentials. This is a legitimate choice for credentials with short verification windows. It is a poor choice on its own for credentials that must be checked for decades.

**B. Re-issue with a new algorithm.** The issuer creates a new credential, signed with a new algorithm and key, to replace the old one. The holder receives it, usually through the wallet. This gives a clean result, but it needs a way to reach holders, and some holders may be hard to reach years later. It also raises a question: what does the new credential say about the date of the original achievement? The issuance date and the achievement date should stay distinct and truthful.

**C. Hybrid or dual signing.** The credential carries two signatures at once, one from a classical algorithm and one from a post-quantum algorithm. A verifier can check either or both. If one algorithm is broken later, the other still gives assurance. The cost is larger credentials and verifiers that must understand both. Support for such combinations in credential formats is still developing.

<!-- VERIFY: check whether the credential securing formats used in Open Badges 3.0 and Verifiable Credentials currently define post-quantum or hybrid proof types, and describe the position neutrally. -->

**D. Prove the time of signing.** A trusted timestamp or archive proof shows that a signature existed at a time when its algorithm was still sound. Verifiers can then accept an old credential as genuine even if the algorithm has since weakened. This approach is well known from long-term archiving of signed documents. It depends on trustworthy time services and on keeping the evidence safe for as long as needed.

Options B, C and D change what the credential carries. Option A changes how the organisation watches and decides. A solid plan usually includes A as a standing activity, plus one or more of B, C and D for the credentials that need them.

### Keys, identifiers and trust anchors

Signatures depend on keys, and keys depend on how verifiers find them. Three questions guide key planning.

**How is the issuer's key published?** If the public key is published in a document linked to the issuer's identifier, then replacing the key means updating that document. Verifiers must be able to see both old and new keys, so that old credentials still verify against the old key and new ones against the new key. Removing old keys too early breaks verification of every credential they signed.

**How is key history kept?** An issuer needs a record of which keys were used in which period, and when each was retired. This record supports later disputes and audits. It should be held by named roles with clear duties.

**How are keys protected?** Keys held in secure hardware or a managed key service are harder to steal than keys stored in files. Whatever the method, access should be limited, logged and reviewed. Key protection matters on top of algorithm choice. A strong algorithm with a leaked key gives no protection.

Revocation and status are part of the picture. If credentials can be revoked, the status mechanism must keep working for the whole verification window, or the issuer must state what verifiers should do when it cannot be reached.

A practical rule: never delete a retired key's public part while credentials signed with it may still be checked. Retire the key for signing, and keep it for verifying.

**Worked example: The college and the learner record**

A college issues digital diplomas and keeps a learner records office. The credential operations manager reviews the options for the diploma, which graduates may present for 40 years or more. Option A alone is rejected, because the verification window is too long. Option B is attractive, but the college knows that many graduates change email address and stop using their wallet, so re-issue will not reach everyone. The manager notes that option D, trusted timestamps stored by the college, suits older diplomas, while option C suits newly issued ones once the formats support it.

She also asks the IT team to confirm how the college's public keys are published, and asks for a rule that retired public keys stay available for verification. She presents the options to the registrar with a one-page summary, and the registrar asks for a costed plan.

**Practice activity: Match options to credentials**

Take three credential types: a one-year training attendance badge, a professional licence valid for life, and a degree certificate. For each, choose which of the four options, or which combination, you would recommend, and write one sentence of reasoning. Then note one risk of your choice, for example "holders may not respond to a re-issue request".

<details>
<summary>Facilitator notes</summary>

In a workshop, split the group into three teams. Give each team one of the credential types and ask them to present a recommendation in three minutes. Encourage the other teams to challenge the recommendation with a "what if the holder cannot be reached" question. Stay vendor-neutral: discuss approaches, not products.

</details>

### Check your understanding: Options

**Question 1.** Which option adds a second signature made with a different algorithm to the same credential?

[( )] Keep and monitor.
[( )] Re-issue with a new algorithm.
[(X)] Hybrid or dual signing.
[( )] Prove the time of signing.
[[?]] The word "hybrid" suggests combining two kinds.
****
Hybrid or dual signing attaches two signatures, for example one classical and one post-quantum, so that assurance remains if one algorithm is later broken.
****

**Question 2.** What is a main weakness of re-issuing credentials with a new algorithm?

[( )] It makes credentials smaller.
[(X)] The issuer must be able to reach holders, and some may be unreachable years later.
[( )] It removes the need for any key management.
[( )] It works only for credentials with a short life.
[[?]] Think about whether every holder will still use the same wallet or email address in 20 years.
****
Re-issue needs a route to each holder. Over decades, contact details and wallets change, so some holders may not receive the new credential.
****

**Question 3.** Why should an issuer keep the public part of a retired signing key available?

[( )] Because public keys can sign new credentials.
[( )] Because it saves storage in the wallet.
[(X)] Because credentials signed with that key may still be checked.
[( )] Because standards forbid deleting any file.
[[?]] Who needs the old public key, and for what?
****
Verifiers need the old public key to check credentials that it signed. The key is retired for signing but kept for verifying.
****

**Question 4.** What does a trusted timestamp or archive proof add to an old signature?

[( )] A new private key for the holder.
[( )] A guarantee that the credential content is true.
[(X)] Evidence that the signature existed at a time when its algorithm was still sound.
[( )] Automatic renewal of the credential every year.
[[?]] The proof is about time, not about the truth of the claim.
****
A trusted timestamp shows when a signature existed. A verifier can then accept it as genuine even if the algorithm has weakened since, provided the time evidence itself is trustworthy and preserved.
****

## Planning

### When to start

The question "when should we start planning?" has a practical answer. Start when the time needed to migrate, plus the time your data must stay protected, is close to or longer than the time before the algorithm may no longer be trusted.

Security specialists use a simple way of thinking about this, often called Mosca's inequality. Three quantities are compared:

- **X:** how long the credentials must remain trustworthy, which for us is the verification window.
- **Y:** how long it takes the organisation to migrate.
- **Z:** how long until the algorithm can no longer be trusted.

If X plus Y is greater than Z, the organisation is already late. The numbers are estimates and Z is uncertain. The value of the exercise is in seeing that a long X and a long Y can make early planning necessary, even when Z is far away.

The migration time Y is often underestimated. It includes finding every place that uses signatures, agreeing a standard, waiting for formats and wallets to support it, testing with partners, communicating to holders and verifiers, and retiring the old setup. Credential ecosystems have many parties, so Y is shaped by the slowest important partner.

<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>When to start planning: three quantities</title>
  <desc>Three horizontal bars stacked in a row, labelled X for how long credentials must stay trustworthy, Y for how long migration takes, and Z for time until the algorithm is no longer trusted. A note states that if X plus Y is greater than Z, planning is already late. Values are illustrative.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <text x="40" y="40" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="bold" fill="#02375B">Start planning when X + Y is close to Z (illustrative)</text>
  <text x="40" y="100" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">X: credentials must stay trustworthy, 25 years</text>
  <rect x="40" y="110" width="500" height="40" rx="6" fill="#02375B" stroke="#02375B" stroke-width="2"/>
  <text x="290" y="136" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#FFFFFF" text-anchor="middle">X = 25 years</text>
  <text x="40" y="195" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">Y: time the organisation needs to migrate, 7 years</text>
  <rect x="540" y="205" width="140" height="40" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="610" y="231" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">Y = 7 years</text>
  <text x="40" y="290" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">Z: time until the algorithm is no longer trusted, 20 years</text>
  <rect x="40" y="300" width="400" height="40" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="240" y="326" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">Z = 20 years</text>
  <line x1="440" y1="285" x2="440" y2="350" stroke="#02375B" stroke-width="2" stroke-dasharray="6 4"/>
  <line x1="680" y1="170" x2="680" y2="350" stroke="#02375B" stroke-width="2" stroke-dasharray="6 4"/>
  <rect x="40" y="375" width="720" height="50" rx="6" fill="#F1F5F8" stroke="#D8E2E9" stroke-width="2"/>
  <text x="400" y="406" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B" text-anchor="middle">X + Y = 32 years is greater than Z = 20 years: planning is already late.</text>
</svg>

### Triggers and a planning roadmap

A planning start does not mean a migration start. Planning is cheap, migration is not. Several triggers justify beginning the planning work:

- You issue credentials with a verification window of more than about ten years. <!-- VERIFY: the ten year figure is a rule of thumb for this course, not a published threshold; confirm or reword before publishing. -->
- Standards bodies or public authorities publish guidance with target dates for moving away from your current algorithms.
- Your credential format, wallet or trust framework adds support for new algorithms.
- Regulators, auditors or large customers ask about your plans.
- You are about to build or buy a new credential system. This is the cheapest moment to require agility.

A simple roadmap has five steps:

1. **Inventory.** List credential types, signing keys, algorithms, formats, wallets, status services and partners. Record the verification window of each credential type.
2. **Assess.** Compare X, Y and Z for each credential type. Rank the types by exposure.
3. **Choose.** Select options from the four families for each ranked type. Agree the approach with partners where interoperability matters.
4. **Prepare.** Write requirements for new systems, such as support for several algorithms and for key history. Run small pilots when formats allow.
5. **Review.** Set a regular review date, for example every year, and a named owner. Update the plan when standards or guidance change.

Because post-quantum migration in credential ecosystems is not yet planned at scale, the early steps, inventory and assessment, are the sensible work today. Status as of November 2026; check before publishing.

### Roles, evidence and responsible communication

Migration planning crosses teams. Typical roles are:

- the **programme owner**, often in HR or learning technology, who accepts the risk and funds the work;
- the **security lead**, who advises on algorithms and key protection;
- the **credential operations lead**, who runs issuing and status services;
- the **standards or architecture lead**, who tracks formats and wallet support;
- the **communications lead**, who prepares holders and verifiers for any change.

Keep evidence of your decisions: the inventory, the comparison of X, Y and Z, the options considered and the reasons for the choice. This record shows due care and helps later reviews. It also supports the VRITE pillar of Trustworthiness: people can rely on a credential only if its issuer plans for its long-term assurance and says so openly.

Communicate carefully. Avoid alarm, and avoid false comfort. Say what is known, for example that standards exist for some algorithms and that a plan is in place, and say what is uncertain, for example the date at which current algorithms will be unsafe. Do not promise that credentials will stay verifiable forever. Promise the review and the actions you can keep.

Finally, remember the limits of this topic. A signature protects the integrity and origin of a credential. It does not show that the claim in it is true, that the person is competent in a job, or that the issuer followed good assessment practice. Long-term signature planning supports trust and is one part of a wider quality system.

**Worked example: The HR department's roadmap**

The HR learning technology owner of a multinational company issues digital credentials for leadership programmes and for mandatory compliance training. Leadership credentials are shown to future employers for the whole career of the holder. Compliance credentials are rarely checked after three years.

She runs the inventory with the security lead and finds two signing keys, one algorithm, and one external wallet partner. For leadership credentials, X is about 30 years, Y is estimated at 6 years, and Z is uncertain, so she treats it as 15 years for planning. X plus Y exceeds Z, so these credentials are high priority. For compliance credentials, X is 3 years, so she chooses option A: keep and monitor. All numbers are illustrative.

She adds a requirement to the next procurement round that any credential platform must support several signature algorithms and keep key history. She sets an annual review and names the security lead as the owner of the guidance watch.

**Practice activity: Run the inequality**

Pick one credential type. Estimate X (verification window), Y (migration time) and Z (time until the algorithm is no longer trusted). Use ranges if you are unsure, for example "Y between 4 and 8 years". Decide whether X plus Y exceeds Z at the low end, the high end or both. Write one sentence that says what you would do next, and name the role responsible.

<details>
<summary>Facilitator notes</summary>

In a workshop, ask participants to share their estimates in a round, then discuss why the migration time Y is usually the least reliable number. Invite participants from wallet and standards backgrounds to describe how long format changes typically take to reach production. Capture one agreed next step per organisation on a shared sheet, with an owner and a date.

</details>

### Check your understanding: Planning

**Question 1.** In the planning inequality, what does Y stand for?

[( )] The number of credentials issued per year.
[(X)] How long it takes the organisation to migrate.
[( )] The size of a signature in bytes.
[( )] The age of the oldest credential.
[[?]] X is the credential life, Z is the algorithm life, so Y is the remaining quantity.
****
Y is the time the organisation needs to migrate. It includes inventory, decisions, partner agreement, testing, communication and retirement of the old setup.
****

**Question 2.** An organisation has X = 20 years, Y = 5 years and expects Z = 15 years. What follows?

[( )] Planning can wait, because Z is shorter than X.
[( )] Planning is needed only if Y is zero.
[(X)] X plus Y is 25 years, which is greater than Z, so planning is already late.
[( )] Nothing follows, because the numbers cannot be compared.
[[?]] Add X and Y, then compare with Z.
****
X plus Y equals 25 years, which is more than 15 years. The organisation is late and should begin planning now. The numbers are estimates, but the comparison shows the exposure.
****

**Question 3.** Which step comes first in a sensible planning roadmap?

[( )] Re-issue all credentials at once.
[( )] Choose a vendor.
[( )] Announce a date for retiring all current algorithms.
[(X)] Inventory credential types, keys, algorithms, formats and partners.
[[?]] You cannot assess what you have not listed.
****
An inventory comes first. It shows where signatures and keys are used and what verification windows apply, which makes assessment and choice possible.
****

**Question 4.** Which communication approach fits the VRITE pillar of Trustworthiness?

[( )] Promise that credentials will stay verifiable forever.
[( )] Say nothing until a break has happened.
[(X)] State what is known, what is uncertain and which actions and reviews you will carry out.
[( )] Tell holders that long-term signatures prove job competence.
[[?]] Honest and specific statements build trust.
****
Open, measured communication says what is known, what is uncertain and what the issuer commits to do. It avoids both alarm and false guarantees.
****

## Assessment and badge

### Final knowledge check

The final knowledge check has 10 single-choice questions. Each question has four options and one correct answer. It covers all three learning outcomes. Answer from your own understanding of the course. You may reread the modules before you start.

**Question 1.** Which situation shows cryptographic ageing most clearly?

[( )] A wallet app changes its logo.
[( )] A credential expires after one year as planned.
[(X)] A credential with no expiry is checked 30 years after issue, and its signature algorithm is no longer recommended.
[( )] An issuer changes its email address.
[[?]] Look for a gap between credential life and algorithm life.
****
Cryptographic ageing is the weakening of assurance as an algorithm ages while the credential is still in use. A long verification window against a retired algorithm is the clearest case.
****

**Question 2.** What is the verification window?

[( )] The time an issuer takes to prepare a credential.
[(X)] The period in which someone may want to check the credential.
[( )] The time a signing key remains in secure hardware.
[( )] The period before a wallet shows a warning.
[[?]] It can be longer than the validity period.
****
The verification window covers the whole period in which the credential may be checked, which can far exceed any stated validity period.
****

**Question 3.** Why does a possible large quantum computer matter for credential signatures?

[( )] It would make all credential images unreadable.
[( )] It would make wallets unable to store credentials.
[( )] It would only affect printed certificates.
[(X)] It could break signature algorithms based on factoring or elliptic curve problems, allowing forged signatures.
[[?]] Think about what an attacker could derive from a public key.
****
A sufficiently large quantum computer could run a known method against these mathematical problems and derive private keys, which enables forgery. Nobody can fix a date for this, but planning takes it seriously.
****

**Question 4.** What does cryptographic agility mean for a credential system?

[( )] The system issues credentials faster than others.
[( )] The system avoids using any keys.
[(X)] The system can change algorithms without a full redesign.
[( )] The system accepts only one algorithm for all time.
[[?]] Agile means able to change.
****
Cryptographic agility is the ability to move to new algorithms without redesigning everything, for example by recording the algorithm in each credential and supporting several in verifiers.
****

**Question 5.** Which migration option places two signatures, one classical and one post-quantum, on the same credential?

[( )] Keep and monitor.
[( )] Re-issue with a new algorithm.
[(X)] Hybrid or dual signing.
[( )] Prove the time of signing.
[[?]] The name suggests a mix of two kinds.
****
Hybrid or dual signing carries two signatures so that assurance continues if one algorithm is later weakened. It needs larger credentials and verifiers that understand both.
****

**Question 6.** What is the main purpose of a trusted timestamp or archive proof on an old credential?

[( )] To prove the claim in the credential is true.
[( )] To give the holder a new private key.
[(X)] To show the signature existed at a time when its algorithm was still sound.
[( )] To make the credential expire sooner.
[[?]] The proof concerns when, not whether the claim is true.
****
A timestamp or archive proof gives evidence of when a signature existed. A verifier can accept the credential as genuine even if the algorithm has weakened since, if the time evidence is trustworthy and preserved.
****

**Question 7.** An issuer retires a signing key and deletes its public part at once. What is the likely result?

[( )] Nothing, because verification does not need the public key.
[( )] All credentials become more secure.
[(X)] Credentials signed with that key can no longer be verified.
[( )] The wallet automatically re-issues every credential.
[[?]] Verifiers use the public key to check a signature.
****
Verifiers need the public key to check signatures. A retired key should stop signing but remain available for verifying as long as its credentials may be checked.
****

**Question 8.** When should an organisation start planning a migration?

[( )] Only after a break of its algorithm has been reported.
[( )] Only when all partners have finished their migration.
[(X)] When the time credentials must stay trustworthy plus the time to migrate is close to or longer than the time until the algorithm may not be trusted.
[( )] Only when the credentials have just been issued.
[[?]] Compare X, Y and Z.
****
Planning should begin when X plus Y is close to or exceeds Z. Waiting for a reported break is too late if migration takes years.
****

**Question 9.** A programme owner has X = 10 years, Y = 3 years and estimates Z = 25 years. What is a sensible conclusion?

[( )] Planning is already late.
[(X)] X plus Y is 13 years, which is less than Z, so there is time. A regular review is still sensible, because Z is uncertain.
[( )] The credentials should be re-issued immediately.
[( )] The comparison is meaningless.
[[?]] Add X and Y and compare with Z, then think about uncertainty.
****
X plus Y is 13 years, below the estimated 25 years. There is time, but Z is uncertain, so a review date and a guidance watch remain good practice.
****

**Question 10.** Which statement about communicating long-term credential plans matches the VRITE pillar of Trustworthiness?

[( )] Promise that every credential stays verifiable forever.
[( )] Hide planning work from holders to avoid worry.
[(X)] Say what is known, what is uncertain and what reviews and actions you commit to.
[( )] State that a signed credential proves competence in a job.
[[?]] Trust grows from honest, specific statements.
****
Open and measured communication builds trust. A signature supports integrity and origin of a credential. It does not prove job competence or the truth of every claim.
****

### Rubric

The knowledge check is scored automatically. Use this table to understand the standard.

| Criterion | Meets the standard | Does not yet meet the standard |
|---|---|---|
| Cryptographic ageing (outcome 1) | Answers questions 1 to 4 correctly in the main, showing that credential life, verification window and algorithm life are different and can conflict | Confuses validity period with verification window, or cannot say why old signatures lose assurance |
| Migration options (outcome 2) | Answers questions 5 to 7 correctly in the main, showing the purpose and trade-offs of keep and monitor, re-issue, hybrid signing and trusted time evidence, and the need to keep old public keys | Cannot tell the options apart or states that deleting retired public keys is safe |
| Planning (outcome 3) | Answers questions 8 to 10 correctly in the main, showing how to compare X, Y and Z and how to communicate responsibly | Cannot apply the comparison or promises permanent verifiability |

### Pass rule and evidence

- **Pass rule:** 8 or more of the 10 questions answered correctly, and at least one correct answer for each learning outcome (outcome 1: questions 1 to 4, outcome 2: questions 5 to 7, outcome 3: questions 8 to 10).
- **Attempts:** you may retake the check after rereading the modules.
- **Badge evidence:** passed knowledge check.
- **Badge:** "Long-Lived Credentials and Post-Quantum Cryptography (Knowledge, L4)", alignment code ICSF-SECP-L4-K.

Passing this check shows that you understand the concepts taught in this course. It does not show that you can carry out a migration, and it does not prove competency in a job.

<details>
<summary>Facilitator notes</summary>

If you offer a live debrief, run it after the knowledge check. Ask participants which question they found hardest and why. Use the answers to refine the next run of the course. Record the pass decision and the badge evidence in the Kursbibliothek according to the ICoBC badge issuing procedure.

</details>

## Sources and further reading

Status as of November 2026; check before publishing. Confirm current editions, titles and publication status of each item before release.

- National Institute of Standards and Technology (NIST), Post-Quantum Cryptography project pages and the published standards for post-quantum signature and key-establishment algorithms. <!-- VERIFY: confirm current standard numbers and titles on the NIST website before publishing. -->
- World Wide Web Consortium (W3C), Verifiable Credentials Data Model, current Recommendation. <!-- VERIFY: confirm the current version and status on the W3C website. -->
- 1EdTech Consortium, Open Badges Specification, version 3.0. <!-- VERIFY: confirm the current version and status on the 1EdTech website. -->
- European Telecommunications Standards Institute (ETSI), publications on quantum-safe cryptography and on long-term preservation of digital signatures. <!-- VERIFY: confirm specific document titles and numbers before citing individually. -->
- Internet Engineering Task Force (IETF), working group documents on post-quantum use in protocols. <!-- VERIFY: confirm specific working groups and document numbers before citing. -->
- ICoBC, Credentialing Skills Framework (ICSF), skill SECP "Security, privacy and data protection". Available from the ICoBC Kursbibliothek.
