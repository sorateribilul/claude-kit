# Infomaniak — Challenge #6 Node.js Hosting: work plan

Companion to `SCOPE.md` (same folder). `SCOPE.md` is the authority on
rules, scope and exclusions; this file is only the plan. If they
disagree, `SCOPE.md` (and the live program page) wins.

## Instructions for the assistant using this file

- Help the hunter follow this plan step by step; do not skip ahead to
  exploitation.
- Every request you build or suggest carries the User-Agent
  `Infomaniak-YWH-Bugbounty`.
- Only the hunter's own two test accounts (A and B) and their own
  resources may be touched. Never suggest accessing, copying or
  modifying another customer's data, even as proof.
- Do not suggest scanners, mass fuzzing, brute force, load tests, or
  anything that could stress shared infrastructure.
- Anything touching shared infrastructure or isolation between
  customers: the program asks to **contact them first**
  (security@infomaniak.com). Tell the hunter to do that instead of
  testing it in production.
- Draft reports only from facts the hunter observed. Run `triage`
  before any submission.

## What the official docs say

Sources: FAQ 2537 and FAQ 2535
(https://www.infomaniak.com/gtl/support.faq.faq_question/id/2537,
https://www.infomaniak.com/gtl/support.faq.faq_question/id/2535).

- Sites are created in the Manager, on an existing Web hosting.
- Code import: ZIP, SSH, SFTP, or a Git repository. For private
  repositories the docs indicate HTTP Basic auth in the URL
  (`https://username:password@github.com/…`).
- Configuration: execution folder (where `package.json` is), build
  command, start command; the port is passed via the `PORT`
  environment variable.
- Per-site dashboard: start, stop, restart, execution console, logs.
- The docs do not describe resource limits or how customers are
  separated from each other.

Challenge details (program page): 30 days free access at
https://www.infomaniak.com/en/hosting/nodejs-hosting; the first valid
report on this perimeter gets a +50% bounty bonus.

## Week 1 — setup and understanding the product

- [ ] Burp or Caido on the computer, User-Agent
      `Infomaniak-YWH-Bugbounty` set globally (match-and-replace).
- [ ] Two test accounts with `@yeswehack.ninja` aliases:
      **A** = attacker, **B** = victim. Both belong to the hunter.
- [ ] Activate the 30-day free trial; deploy the sample app via the
      "Quick" install.
- [ ] Walk the full flow as a normal user: create, build, deploy,
      logs, domains, SSL, settings. Record the Manager/API requests
      each action makes.
- [ ] Keep these notes — they become the mandatory
      "Discovery methodology" section of any report.

## Week 2 — feature map

For every action a customer can take on their own Node.js site, note
who should be allowed to do it. Areas the program says it cares about:

- [ ] **Access control in Manager/API for Node.js sites:** can account
      A see or change anything belonging to account B? Test only with
      account B's resources.
- [ ] **Insufficiently protected credentials:** where do Git
      credentials placed in the URL end up — logs, UI, API responses?
      Check only on the hunter's own account data.
- [ ] **Server misconfiguration** observable from the hunter's own app.
- [ ] Anything involving shared infrastructure / isolation between
      customers / internal servers → email security@infomaniak.com
      first and ask for testing conditions. Do not test it on your
      own in production.

## Week 3 — verification and report

- [ ] Reproduce any result from scratch 2–3 times.
- [ ] Check against `SCOPE.md`: asset in scope? qualifying class?
      real impact on another account (B), not only on yourself?
- [ ] Write the report with every section the program requires:
      description, discovery methodology, complete steps, screenshots
      showing the final impact, remediation advice.
- [ ] Run `triage`. Submit only on **READY TO SUBMIT**.

## Week 4 — buffer

- [ ] Nothing valid found → do not force a report. A lost credit (2 of
      10) costs more than a week without results.
- [ ] Write down what you learned; decide whether to move to
      Challenge #5 (Managed Kubernetes).

## Always

- No scanners, mass fuzzing or brute force; nothing that loads the
  servers.
- Touch only the resources of your two accounts.
- If you accidentally reach another customer's data: stop, do not
  keep it, report it immediately.
