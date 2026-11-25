---
name: governance-baseline
description: Set a cloud project's security and governance baseline at the start, as reusable templates. Picks the service model (IaaS, PaaS, SaaS) per component from how much control the team needs versus how much patching it wants to own, then writes a GOVERNANCE.md, infrastructure templates with secure defaults, policy-as-code guardrails, compliance auditing and automatic patching. Use when starting a new cloud project, when asked for a "project standard", "landing zone", "cloud baseline" or "governance template", or when an existing project has none and resources are drifting.
---

# governance-baseline

Governance is cheapest on day one. A baseline set early keeps the environment updated, secure and well managed; one added after fifty hand-made resources is a migration. This skill turns the baseline into **templates and policies the project reuses**, so every new resource starts compliant and the standard can change in one place and roll out to everything at scale.

It is provider-agnostic: use the project's cloud (Azure, AWS, GCP) and IaC tool (Terraform/OpenTofu, Bicep, CloudFormation, Pulumi). It **proposes and writes files**; it changes live cloud resources or org-level settings only after the user approves each one.

## 1. Gather

Ask only what the repo doesn't already answer:

- Cloud provider(s), IaC tool, CI system
- Components to run (web app, API, database, queue, batch jobs, VMs) and who operates them
- Regulatory or contractual requirements (GDPR, ISO 27001, SOC 2, PCI DSS, HIPAA, data residency). "None known" is a valid answer; write it down.
- Environments (dev, staging, prod) and who may deploy to each

Read before asking: `infra/`, `terraform/`, `*.bicep`, `cdk.json`, `.github/workflows/`, existing `SECURITY.md` or `GOVERNANCE.md`.

## 2. Choose the service model per component

Pick the model that matches the security and maintenance needs, not the most familiar one. The trade-off is control versus who patches:

| Model | You manage | Provider manages | Pick when |
|---|---|---|---|
| IaaS (VMs) | OS, runtime, installed software, patches, hardening | Hardware, physical network, data center | You need OS-level control: custom kernels, licensed software, lift-and-shift |
| PaaS (app services, managed DBs, serverless, managed containers) | App code, config, data, identity and access | OS, runtime, patching, scaling | Default for new workloads: patching and maintenance happen automatically |
| SaaS | Data, users, access settings | Almost everything else | A commodity need (email, CI, monitoring, auth) someone already runs well |

For every IaaS choice, record why PaaS doesn't fit and who owns patching. "We always use VMs" is not a reason.

## 3. Write the baseline

Create these files on a branch. Keep each short; they are templates, not essays.

**`GOVERNANCE.md`**: one page.
- Service model per component, with the reason (from step 2)
- Requirements that apply, or "none known as of <date>"
- Allowed regions (data residency), required tags, naming convention
- Who owns what: patching, access reviews, cost, incident response
- How the baseline changes: edit the template or policy, open a PR, roll out with the pipeline. No hand fixes in the console.

**Infrastructure templates with secure defaults** (`infra/modules/` or the IaC tool's equivalent). Every new resource comes from a module, and the module's defaults are the compliant choice:
- Required tags: `owner`, `environment`, `cost-center`, `data-classification`
- Encryption at rest and TLS in transit on; minimum TLS 1.2
- No public endpoints, public buckets or open inbound ports unless a variable says so explicitly, with a comment saying why
- Managed identities or workload identity instead of stored keys; secrets in the provider's secret manager
- Diagnostic logs sent to one central workspace or bucket
- Region restricted to the allowed list

**Policy as code**: guardrails that block or flag what the templates prevent, so a resource made outside the templates is still caught. Use the provider's native tool (Azure Policy, AWS Config rules and SCPs, GCP Organization Policy) or a portable one (OPA/Conftest, Checkov, tfsec/Trivy) in CI. Start with:
- Deny resources outside allowed regions
- Deny missing required tags
- Deny public storage and unencrypted storage
- Audit (not deny, at first) everything else, then tighten once the audit is clean

**Compliance auditing**: something that keeps checking after deploy, not only in CI.
- Turn on the provider's posture tool (Microsoft Defender for Cloud, AWS Security Hub, GCP Security Command Center) against a named benchmark, such as CIS
- Schedule drift detection (`terraform plan` on a cron, or the provider's drift feature) and alert on changes made outside the pipeline
- Send findings with the suggested fix to an owner, not just a dashboard

**Automatic patching and updates**:
- PaaS and SaaS: confirm auto-updates are on and note the provider's maintenance window
- IaaS: enable the provider's update manager or patch baseline, with a schedule and a reboot window per environment; build images from a pipeline, not by hand
- Dependencies and base images: Dependabot or Renovate, with CI and the verify step as the gate

**Network protection**: put public entry points behind the provider's edge (load balancer, WAF, CDN), which absorbs DDoS traffic better than your own instances can. Turn on the provider's DDoS protection tier if the workload or requirements justify the cost; record the decision either way.

**CI wiring**: run IaC lint and policy checks on every PR that touches `infra/`, and read the policies from the default branch so a change can't loosen its own checks.

## 4. Check the baseline works

Prove the guardrails fire, don't assume it:
- Run the policy checks against a deliberately bad resource (public bucket, missing tags, wrong region) and confirm each one fails
- Run them against a module with default values and confirm it passes
- If an audit or posture tool is on, show one real finding or a clean report

## 5. Apply — only with approval

- Files (GOVERNANCE.md, modules, policy files, workflows): commit on a branch and open a PR if the user asks.
- Live resources and org-level settings (assigning policies, enabling Defender/Security Hub, DDoS plans, patch schedules): these affect cost and everyone's deployments. Show the exact command or IaC change and ask before each one. Start with audit mode; switch to deny only after the user agrees.
- Never weaken an existing policy or protection without an explicit request.

## Output

The service-model table, the list of files written, the guardrail test results (which bad resource each policy caught), and what was applied versus left for the user.
