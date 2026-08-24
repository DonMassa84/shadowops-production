# AI Governance – ShadowOps Production

Status: ACTIVE

## Control flow

`Input -> Data classification -> Local/Cloud decision -> Secrets/PII filter -> Model/Tool execution -> Human approval for external effect -> Output -> Audit log`

## Mandatory controls

- Classify data as public, internal, confidential or restricted before processing.
- Restricted data must not be routed to external models without explicit approval.
- Prefer local inference for internal/confidential data where feasible.
- Never persist credentials, tokens, API keys or unnecessary personal raw data.
- Agents operate with least privilege.
- Human approval is required before external effects such as sending messages, changing credentials, payments, deployments, destructive infrastructure actions or publication.
- Trigger, data class, model/tool path, approval state, result and errors must be auditable.
- Fail closed when classification, permissions, secrets handling or approval state is unclear.

## Green gate

A workflow is GREEN only when source, classification, secrets handling, permission scope, approval rule, rollback path and audit evidence are known.

`AI_GOVERNANCE=ACTIVE`
`HUMAN_APPROVAL_EXTERNAL_EFFECT=REQUIRED`
`FAIL_CLOSED=YES`
