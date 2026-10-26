# Infomaniak — Challenge #5 Managed Kubernetes: work plan

Companion to `SCOPE.md` (same folder). `SCOPE.md` is the authority on
rules, scope and exclusions; this file is only the plan. If they
disagree, `SCOPE.md` (and the live program page) wins.

## Instructions for the assistant using this file

- Help the hunter follow this plan step by step; do not skip ahead to
  exploitation.
- Every request you build or suggest carries the User-Agent
  `Infomaniak-YWH-Bugbounty` (for kubectl, the hunter's own proxy or
  tooling must add it; check before testing).
- Only the hunter's own two test accounts (A and B) and their own
  clusters/projects may be touched. Never suggest accessing, copying
  or modifying another customer's data, even as proof.
- Do not suggest scanners, mass fuzzing, brute force, load tests, or
  anything that could stress shared infrastructure.
- Anything touching shared infrastructure, the managed control plane
  internals, or isolation between customers: the program asks to
  **contact them first** (security@infomaniak.com). Tell the hunter to
  do that instead of testing it in production.
- Draft reports only from facts the hunter observed. Run `triage`
  before any submission.

## Scope open question — resolve before testing

The program page announces Challenge #5 and invites testing at
https://www.infomaniak.com/en/hosting/public-cloud/kubernetes, but the
scope list in `SCOPE.md` has **no asset named Kubernetes**. Related
listed items:

- In scope: `manager.infomaniak.com/v3/*` (Critical),
  `api.infomaniak.com` (Critical), `api.pub1.infomaniak.cloud` and
  `api.pub2.infomaniak.cloud` (Medium).
- Out of scope: OpenStack dashboard (Horizon); customer S3
  (`s3.pub*.infomaniak.cloud`); customer DBaaS
  (`*.dbaas.infomaniak.cloud`).

**Action:** ask the program (YesWeHack program contact or
security@infomaniak.com) which asset Kubernetes findings are filed
under, and whether the managed cluster API endpoints are in scope.
Write the answer here before testing.

## What public docs say (verify on the live pages)

- Ordered and installed from the Manager.
- Access via a kubeconfig file (kubectl), Terraform/OpenTofu, a web
  Kubernetes Manager, and the Infomaniak CLI.
- Control-plane plans; worker instances, block storage and snapshots
  billed at Public Cloud rates.
- The API server certificate is renewed yearly; a new kubeconfig is
  then downloaded from the Manager.

Sources:
https://www.infomaniak.com/en/support/faq/2819/installer-kubernetes-sur-public-cloud
https://www.infomaniak.com/de/support/faq/2906/troubleshooting-an-api-server-inaccessible-error-on-kubernetes-as-a-service

Challenge details (program page): free trial offer; the first report
on this scope gets a 50% bonus.

## Week 1 — setup and understanding the product

- [ ] Resolve the scope question above.
- [ ] Burp or Caido on the computer, User-Agent
      `Infomaniak-YWH-Bugbounty` set globally (match-and-replace).
- [ ] Two test accounts with `@yeswehack.ninja` aliases:
      **A** = attacker, **B** = victim. Both belong to the hunter.
- [ ] Use the free trial; create the smallest cluster that works.
      Watch costs: workers and storage are billed separately.
- [ ] Walk the full flow as a normal user: create cluster, download
      kubeconfig, deploy a simple app, scale, delete. Record the
      Manager/API requests each action makes.
- [ ] Keep these notes — they become the mandatory
      "Discovery methodology" section of any report.

## Week 2 — feature map

For every action a customer can take on their own cluster in the
Manager/API, note who should be allowed to do it. Areas the program
says it cares about:

- [ ] **Access control in Manager/API for Kubernetes resources:** can
      account A see or change anything belonging to account B
      (clusters, kubeconfigs, node pools, settings)? Test only with
      account B's resources.
- [ ] **Insufficiently protected credentials:** how kubeconfigs and
      other secrets are issued, shown, stored and revoked in the
      Manager — check only on your own account data.
- [ ] **Server misconfiguration** observable from your own cluster.
- [ ] Anything involving the managed control plane internals, shared
      infrastructure or isolation between customers → email
      security@infomaniak.com first and ask for testing conditions.
      Do not test it on your own in production.

## Week 3 — verification and report

- [ ] Reproduce any result from scratch 2–3 times.
- [ ] Check against `SCOPE.md` and the scope answer: asset in scope?
      qualifying class? real impact on another account (B), not only
      on yourself?
- [ ] Write the report with every section the program requires:
      description, discovery methodology, complete steps, screenshots
      showing the final impact, remediation advice.
- [ ] Run `triage`. Submit only on **READY TO SUBMIT**.

## Week 4 — buffer and cleanup

- [ ] Nothing valid found → do not force a report. A lost credit (2 of
      10) costs more than a week without results.
- [ ] Delete clusters, instances, volumes and snapshots you created so
      you are not billed after the trial.

## Always

- No scanners, mass fuzzing or brute force; nothing that loads the
  servers.
- Touch only the resources of your two accounts.
- If you accidentally reach another customer's data: stop, do not
  keep it, report it immediately.
