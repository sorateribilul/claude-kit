# Infomaniak Bug Bounty (YesWeHack) — program reference

Source: the program page on YesWeHack, as pasted by the hunter on
2026-10-26 (page shows "Last update on 2026-10-26"). The program page
is the authority: if it changed, re-read it before testing. Do not add
rules, assets or exclusions that are not on the page.

---

## 0. Instructions for the assistant using this file

- Treat this file as the scope and rules of engagement for
  `triage` and `write`. A finding on an asset not listed in §3, or of
  a class listed in §5 "Non-qualifying", is **DO NOT SUBMIT**.
- Every HTTP request you build or suggest must carry the User-Agent
  `Infomaniak-YWH-Bugbounty` (§1).
- Never suggest automated scanners, high-volume fuzzing, brute force,
  or anything that could degrade the service (§1).
- Every report must include the program's required elements (§2),
  including **remediation advice** and **discovery methodology** —
  for this program these are required, not optional.
- Before suggesting submission, remind the hunter about credits (§7).

---

## 1. Rules of engagement (violations can get the account/IP blocked)

- **User-Agent:** `Infomaniak-YWH-Bugbounty` on **all** requests.
  - curl: `curl -A "Infomaniak-YWH-Bugbounty" ...`
  - Burp/Caido: set a match-and-replace rule on the `User-Agent` header.
- **Accounts:** create test accounts **only** with your YWH aliases
  (`*@yeswehack.ninja`). Reuse existing accounts; no mass account
  creation.
- **Forbidden:**
  - DoS/DDoS, brute force, tests that degrade or interrupt services.
  - Automated scanners or tools generating large amounts of traffic.
  - Leaking, manipulating or destroying user data or files.
  - Copying files from their applications/servers and disclosing them.
  - Any disclosure of a vulnerability (full, partial or otherwise).
  - Intensive testing of support channels (kChat, Mail support tickets).
- **Ticketing:** never test real customers' shops. Create Shop A on
  your organization and Shop B on a second organization; test
  cross-organization scenarios only between them.
- **Site Creator:** test only the hunter instances provided:
  - https://5k8vrbdyje.infomaniak.site
  - https://tb7pxbdyjg.infomaniak.site
  - https://fv3lfbdyjh.infomaniak.site
  - https://l75pvbdyjo.infomaniak.site
  Customers' site creators are not part of the program.
- Testing something critical for production: contact them first.
- In doubt: security@infomaniak.com

## 2. Report requirements (for reward eligibility)

- First reporter of the vulnerability.
- Qualifying vulnerability (§5).
- The report must contain:
  - Clear description of the vulnerability, how it can be exploited,
    its security impact on the application, its users and the
    organisation, **and remediation advice**.
  - **Proof of exploitation:** screenshots showing the exploit was
    performed and showing the **final impact**.
  - Complete reproduction steps (code snippets, payloads, commands as
    needed).
  - **Discovery methodology:** how you found the vulnerable endpoint or
    asset (e.g. directory fuzzing, client-side JS analysis, exposed
    source code, external repository). Reports lacking it may be
    delayed.
- Same vulnerability found several times → one report, use comments.
- **One Fix One Reward:** if several endpoints share the same code and
  one fix covers all, only one is rewarded; the others are closed as
  Informative/Duplicate.
- Reward is based on the asset's reward grid and on CVSS + actual
  business impact.
- Former/current employees and contractors are not eligible.

## 3. In-scope assets (asset value as shown on the page)

**Critical**
- api.infomaniak.com (API)
- login.infomaniak.com
- manager.infomaniak.com/v3/*
- shop.infomaniak.com
- ksuite.infomaniak.com
- *.kdrive.infomaniak.com
- swiss-backup*.infomaniak.com
- www.infomaniak.com

**High**
- *.kchat.infomaniak.com
- calendar.infomaniak.com
- chk.infomaniak.com
- contacts.infomaniak.com
- etickets.infomaniak.com
- kmeet.infomaniak.com
- kpaste.infomaniak.com
- mail.infomaniak.com
- player-radio.infomaniak.com
- storage*.infomaniak.com
- sync.infomaniak.com
- swisstransfer.infomaniak.com
- vod.infomaniak.com
- *.vod2.infomaniak.com
- welcome.infomaniak.com
- www.swisstransfer.com
- euria.infomaniak.com
- Android kDrive — com.infomaniak.drive
- iOS kDrive — apps.apple.com/app/infomaniak-kdrive/id1482778676
- Desktop kDrive — https://github.com/Infomaniak/desktop-kDrive
- Android Mail — com.infomaniak.mail
- iOS Mail — apps.apple.com/fr/app/infomaniak-mail/id1622596573
- Android Authenticator — com.infomaniak.auth
- iOS Authenticator — apps.apple.com/fr/app/infomaniak-authenticator/id1478424817

**Medium**
- kdrive.infomaniak.com/app/*/preview/*
- kdrive.infomaniak.com/app/office*/*
- ksuite.infomaniak.com/*/kdrive/*/preview/*
- infomaniak.events
- hosting-ik.com
- ix2smbdyjt.infomaniak.site
- 5k8vrbdyje.infomaniak.site
- fv3lfbdyjh.infomaniak.site
- l75pvbdyjo.infomaniak.site
- Desktop kChat — https://github.com/Infomaniak/desktop-kChat
- Android kChat — com.infomaniak.chat
- iOS kChat — apps.apple.com/fr/app/infomaniak-kchat/id6443845553
- Android Euria — com.infomaniak.euria
- iOS Euria — apps.apple.com/fr/app/infomaniak-euria/id6754152858
- Android SwissTransfer — com.infomaniak.swisstransfer
- iOS SwissTransfer — apps.apple.com/fr/app/infomaniak-swisstransfer/id6737686335
- Android Sync — com.infomaniak.sync
- *.infomaniak.com
- api.pub1.infomaniak.cloud
- api.pub2.infomaniak.cloud
- manager.infomaniak.com/*proxy*

Note: `tb7pxbdyjg.infomaniak.site` is listed as a hunter Site Creator
instance in the description but does not appear in the scope list.
Confirm with the program before reporting on it.

**Third-party code:** any vulnerability in OnlyOffice code is assessed
against the OnlyOffice asset at the **Medium** value, whatever product
or endpoint it is reached through.

## 4. Out of scope

**Assets / services**
- Any asset not listed in §3.
- OpenStack dashboard (Horizon) — e.g. XSS there is out of scope.
  (Misconfigurations / unprotected data in OpenStack resources you
  create may be reported, per the program text.)
- ov-XX.infomaniak.ch and od-XX.infomaniak.ch
- https://drive.infomaniak.com/app/office/:folder:/:file:
- Customer FTP (*.ftp.infomaniak.com), VPS (*.vps.infomaniak.com),
  MySQL (*.myd.infomaniak.com), S3 (s3.pub*.infomaniak.cloud), DBaaS
  (*.dbaas.infomaniak.cloud)
- Jelastic: *.jcloud.ik-server.com, *.jpc.infomaniak.com,
  *.jpe.infomaniak.com
- acronis.infomaniak.com
- storage*.infomaniak.com/newsletter/thumbnails/*
- Services: Housing, Very high availability Hosting, Synology,
  Jelastic cloud, Debian community servers (buster-*.infomaniak.ch,
  bookworm-*.infomaniak.ch)
- Infomaniak Mirror Server

**Behaviours explicitly declared by design / not eligible**
- User email verification (emails are intentionally not verified).
- Websocket IPS-public credentials (MQTT, info-mq, IPS_RABBIT,
  ips-public).
- Partner program: partner-finding / offer pages and data already
  public in the partner directory. (Missing authorization on
  partner-program routes exposing private data remains in scope.)
- Data returned by `/get-tickets-infos` (organizer, event_name,
  event_date, command_date, masked email).
- Moving/copying calendar events or contacts between containers by
  read-write collaborators.
- kMeet: moderator rights for all participants, no demoderation;
  ANONYMOUS SASL / unauthenticated XMPP; exposed client-side config and
  public API keys (unless they give unauthorized access to private
  resources or critical Infomaniak-managed interfaces).
- Ticketing editor / Page editor / Site Creator: JS/HTML injected by
  an admin against their own site's users.
- HTML injection in emails (temporarily excluded).
- SwissTransfer: re-downloads by the same session within the 2-hour
  window despite `max_download`.
- Burn-after-read kPaste: self-destructs on first link resolution with
  or without password.
- Public links: guessing/brute-forcing high-entropy identifiers
  (UUIDs, tokens); access via a valid public link; exploits requiring
  prior knowledge of a non-guessable UUID → closed as RTFS.
- **Business Logic Errors:** not in scope except serious cases leaking
  PII or customer/confidential data.
- **Broken Access Control** between admins/employees/external users:
  not in scope except critical leaks of significant personal data or
  major business/financial impact.
- Leaks sourced from archive.org, Wayback Machine, VirusTotal, Google
  dorking, urlscan.io → not accepted.

**Mobile & desktop apps**
- Requires local user access on the same machine.
- Requires a malicious third-party app installed by the victim.
- Requires an unofficial/modified client.
- Symlink synchronization with absolute paths / traversal (intended).
- Findings must be demonstrated **end to end on the build currently
  distributed to users**; local builds are only a starting point.

## 5. Vulnerability types

**Qualifying**
- SQL Injection
- Cross-Site Scripting (XSS)
- Remote Code Execution
- IDOR
- Horizontal and vertical privilege escalation
- Authentication bypass & broken authentication
- Business Logic Errors with real security impact
- LFI, RFI, XXE, SSRF, XSPA
- CORS with directly exploitable vulnerability and security impact
- CSRF with real security impact
- Open Redirect
- Exposed secrets/credentials/sensitive info from an asset under their
  control
- AI: influencing/changing the model in ways that impact other users;
  perturbing inputs so the model gives incorrect outputs to other
  users; bypassing history protections/deletion to access other users'
  history; poisoning the model or its data
- User enumeration (email addresses or user accounts), account
  existence oracles on an asset under their control

**Non-qualifying**
- HTML injection in emails; content/text injection
- Sandboxed XSS without working PoC; self-XSS or XSS that cannot
  impact other users; XSS on Page editor
- Tabnabbing; clickjacking/UI redressing; mixed content
- Missing cookie flags; missing security headers without direct
  vulnerability; HSTS
- DoS; lack of rate limiting, brute-forcing or captcha issues
- Known CVEs without working PoC; outdated libraries without
  demonstrated impact; 0-days patched less than 14 days ago
- Open ports without real impact
- Social engineering of staff/contractors
- Autocomplete on forms; password policy; password re-validation for
  sensitive actions; session expiration policies
- Outdated browsers/platforms; unsupported Android/iOS versions;
  jailbroken/rooted devices
- Hypothetical flaws / best practices without exploitable PoC
- TLS/SSL certificate issues and best practices
- Unexploitable issues (e.g. XSS or open redirect in Host header)
- Anything requiring MITM or physical access to the victim's device
- Unauthenticated / logout / login / other low-severity CSRF
- SPF / DKIM / DMARC
- Information disclosure without direct impact (stack traces, paths,
  directory listings, versions, IPs, 3rd-party secrets)
- CSV injection
- Subdomain takeover without full working PoC
- Blind SSRF without direct exploitable impact (DNS/HTTP pingback only)
- User enumeration via alias, GUID, phone number
- Spamming users (email/SMS/DM flooding)
- Disclosed/misconfigured Google API keys (incl. Maps)
- Password reset token leak to trusted third party via Referer
- Task hijacking; crashing your own app
- Stolen secrets from third-party assets they don't control
- Lack of client-side mobile protections (SSL pinning, obfuscation,
  root/jailbreak detection, anti-debugging…); unencrypted local
  databases/preference files
- Exploits requiring a malicious third-party app installed by the
  victim, or an unofficial/malicious version of their apps
- Race conditions without critical PII risk
- Business logic errors without critical PII/confidential data risk
- AI: prompt injection affecting only the attacker; system prompts;
  hallucinations; unsafe/inaccurate/offensive outputs; revealing model
  internals without sensitive information
- CORS without a working PoC reading authenticated victim data (200,
  cookie-based auth) from an attacker-controlled origin
- Content/certificates on hostnames resolving to their infra without
  active hosting (incl. zones on Infomaniak DNS managed by another
  account)

## 6. Rewards

Bounty grid as displayed (rows = asset value; the four columns match
the page header Low / Medium / High / Critical severity):

| Asset value | Low  | Medium | High   | Critical |
|-------------|------|--------|--------|----------|
| Critical    | €100 | €600   | €2,000 | €7,000   |
| High        | €100 | €400   | €1,500 | €3,500   |
| Medium      | €100 | €300   | €600   | €1,000   |

Page also shows: average reward €716.7, max reward €15,000.

**Systemic issues** (similar issue already reported, by you or others):
1st 100% · 2nd 100% · 3rd 75% · 4th 50% · 5th 25% · 6th+ 10%.

**Challenges in progress** (first valid report on the perimeter gets a
+50% bonus):
- #6 Node.js Hosting — 30 days free:
  https://www.infomaniak.com/en/hosting/nodejs-hosting
  Docs: https://faq.infomaniak.com/2537
- #5 Managed Kubernetes — free trial:
  https://www.infomaniak.com/en/hosting/public-cloud/kubernetes

**Areas of particular interest** (program text): personal data leaks,
horizontal/vertical privilege escalation, SQLi, server
misconfiguration, SSRF, insufficiently protected credentials, network
misconfiguration between customers and internal servers.

## 7. Credits and activity (as of the paste)

- Current credits: **10**. Submission cost: **2**, refunded only if the
  report is valid. Five invalid reports = no credits left.
- Program activity: 4,147 reports total, 409 this month, 143 last
  week, 26 in the last 24h, first response < 1 day. High duplicate
  risk on the most-tested assets.
- Supported report languages: English, French.
- Up to 5 collaborators per report, with a reward split you define.

## 8. Pre-submission checklist

- [ ] Asset is in §3 and not excluded in §4.
- [ ] Vulnerability class is in §5 "Qualifying", not "Non-qualifying".
- [ ] All traffic used `Infomaniak-YWH-Bugbounty`; accounts used
      `@yeswehack.ninja` aliases; only your own accounts/shops touched.
- [ ] Impact shown on another user/account you own, not only on
      yourself.
- [ ] Screenshots show the **final impact**, not only the request.
- [ ] Reproduction steps are complete and replayable from zero.
- [ ] Discovery methodology section written.
- [ ] Concrete remediation advice written.
- [ ] Not a variant of something you already reported (One Fix One
      Reward / systemic decrease).
- [ ] `triage` verdict is READY TO SUBMIT.
