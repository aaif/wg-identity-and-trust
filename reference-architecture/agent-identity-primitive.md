---
title: Agent Identity Primitives
status: Draft
version: "0.1"
date: 2026-10-21
working-group: Identity & Trust | Agentic AI Foundation
chairs:
  - Grant Miller (IBM)
  - Alper Dedeoglu (SAP SE)
---

# Agent Identity Primitives

| | |
|---|---|
| **Status** | Draft |
| **Version** | 0.1 |
| **Date** | 2026-10-21 |
| **Working Group** | Identity & Trust, Agentic AI Foundation |
| **Chairs** | Grant Miller (IBM), Alper Dedeoglu (SAP SE) |
| **Workstream Lead** | Brian Malone |
| **Contributors** | Hiroshi Yamakawa (AI Alignment Network (ALIGN), JAPAN)<br>Marc Molas Carol (Identity Attestation - MintID)<br>Filip Blagojević (Apex Fusion Foundation)<br>Yoshiyuki Tabata (Hitachi, Ltd.)<br>Julianna Mealin (interop.io) |

*Add your name and affiliation to the Contributors row when you open your first PR.*

---

## Abstract

AI agents are becoming first-class actors in enterprise and consumer systems. They initiate requests, hold credentials, operate across trust domains, and take actions on behalf of people and organizations. Yet the field lacks a shared understanding of what an agent's identity actually consists of — what a system needs to be able to name, locate, verify, and revoke an agent.

This document defines those primitives. It is focused on identity, not on what an agent is permitted to do.

---

## 1. Introduction

### 1.1 Why Agent Identity Is a Distinct Problem

Traditional identity infrastructure was built for two kinds of actors: humans and software services. Agents fit neither model cleanly.

An agent differs from a human user in that it may spawn subagents and operate across multiple systems without a human in the loop. It differs from a conventional workload or API client in that it carries delegated human authority — it acts on behalf of a person or organization, and that relationship needs to be represented in its identity and verifiable by the systems it interacts with. An agent also has provenance that a service account does not: it was built by a provider, potentially distributed through a third party, operated by a responsible party, and authorized by a principal. Each of those relationships is part of what the agent is.

When agents orchestrate other agents, these relationships chain across organizational and trust-domain boundaries in ways that existing identity models were never designed to handle. The practical result is that systems receiving requests from agents have no common framework to answer the question "who are you, on whose behalf, and how can I verify that?"

### 1.2 Scope

This document defines six identity primitives — Identifier, Accountability, Discovery Metadata, Attestation, Delegation, and Revocability — and identifies the interoperability gaps each one is meant to address. Definitions use the AAIF Taxonomy for terms shared across working groups.

The following are out of scope: authorization models (what an agent is permitted to do), evidence, reputation, and security controls or threat modeling. Those are addressed by separate working group efforts.

### 1.3 Audience

This document is written for:

- architects and engineers building systems that interact with agents
- platform providers and registries that need to store and resolve agent identities
- standards bodies building protocols that reference agent identity
- policy teams defining accountability requirements for agentic AI

---

## 2. Taxonomy

**Accountable Party** — an entity in an agent's accountability chain that answers for the agent's actions within a stated scope and period.

**Agent** — an AI-driven software entity that perceives its environment, makes decisions, and takes actions, potentially including invoking tools, calling APIs, spawning subagents, and acting on behalf of a principal.

**Attestation** — a verifiable assertion, bound to its subject and issuer, about an agent, its properties, or actions taken with respect to it.

**Authentication** — the process of verifying that an entity is who it claims to be at the moment of a request, consistent with RFC 4949. Distinct from attestation: authentication confirms a claimed identity at runtime; attestation provides the underlying evidence that makes those claims trustworthy.

**Credential** — a verifiable artifact (token, certificate, or signed assertion) that carries identity or delegation claims and enables authentication.

**Delegation** — the act of one entity granting another entity, including an agent, the right to act on its behalf within defined constraints.

**Distributor** — an entity, other than the provider, that makes an agent or its underlying model available to others (for example, a marketplace, platform, or reseller) without configuring or operating it for a particular deployment. A distributor that configures or operates the agent is also a responsible party.

**Identity** — the set of verifiable claims that define who an agent is and the parties accountable for it.

**Identifier** — a unique, stable, resolvable value that names a specific agent instance or agent type.

**Principal** — a human or organization that has an identity and can authorize an agent to act on its behalf; the origin of the agent's delegated authority.

**Provider** — an entity that built the underlying AI model or agent software, accountable for capabilities and behaviors at the model or software level.

**Relying Party** — an entity that receives an agent's identifier, credentials, or attestations and depends on their validity to decide whether and how to interact with the agent.

**Responsible Party** — an entity accountable for how an agent is configured and operated in a given context (also called operating party or deployer). An agent may have more than one, each for a stated scope. A principal is also a responsible party when it configures or operates the agent.

**Root Authority** — an authority that a trust domain recognizes as able to verify a principal and issue agent credentials bound to it (for example, an enterprise identity provider, a public administration, or a sector authority). Issuing a credential does not by itself make the root authority an accountable party.

**Subagent** — an agent that is initiated by a single parent agent and not addressable by other agents. The lifespan of the subagent cannot exceed that of the parent agent.

**Trust Domain** — a scope within which a common set of policies, identity authorities, and trust decisions apply.

**Trust Boundary** — a dividing line between two areas of a system, network, or component that have different levels of trust or security. On one side of this line, data or entities may be considered trusted; on the other side, they are considered untrusted or less trusted.

---

## 3. Agent Identity Primitives

The six primitives below are the foundational building blocks of agent identity. Together they allow a system to answer: who is this agent, how can it be found, who is responsible for it, how can its claims be verified, what authority does it carry, and can that authority be revoked?

### 3.1 Identifier

An agent's identifier is a unique, stable value that names it — distinct from the identity of its provider, responsible party, or principal. It must be resolvable: any relying party holding the identifier must be able to retrieve the agent's associated metadata and credentials.

In practice, an agent identifier takes different forms depending on context. As a workload, the agent may be identified by a workload credential scoped to its execution environment. In delegation flows, the identifier distinguishes the delegator from the delegatee in an on-behalf-of (OBO) relationship. In OAuth and OIDC contexts, familiar values like Client ID and the `sub` (subject) claim serve as scoped identifiers. An agent may carry multiple identifiers across these contexts, but there must be a defined and verifiable relationship among them.

The identifier must be cryptographically or otherwise verifiably bound to its provider and to the responsible party accountable for the agent's actions, and must be distinct from workload identifiers in traditional senses. An agent is a first-class actor, not a proxy for its provider, its responsible party, or its principals.

The core requirements are uniqueness (unambiguous globally or when scopes are combined), stability across invocations and version updates with explicit auditable rotation, resolvability to current metadata and public keys, historically verifiable, and separability from the identities of the agent's provider, responsible party, and principals.

A vehicle identification number (VIN) is a useful analogy: it identifies a specific car independent of its owner or driver, and any authorized party can use it to look up the vehicle's history and certifications.

**Relevant and proposed standards:** DIDs (W3C Decentralized Identifiers), SPIFFE/SPIRE SVIDs, X.509/PKI certificates, signed "agent passport" credentials, ANS (Agent Name Service), DNS-AID, DNSid, ERC-8004 Identity Registry (ERC-721-based agent ID).

### 3.2 Accountability

Accountability is the verifiable relationship between an agent's identifier and the parties that answer for the agent at a given time. Identifier says which agent; Delegation says on whose authority it acts; Accountability says who stands behind it. For any given scope and point in time, there must be one entity that is the ultimate accountable party: the entity that ultimately answers for the agent's actions in that scope. That party is reached through an accountability chain — an ordered sequence of accountable parties. The chain begins with the party most directly accountable for an action, typically the principal who issued the instruction or the responsible party that configured the agent. It ends with the ultimate accountable party. An employee who makes a mistake using an agent is accountable first, for example, but the organization they act for is ultimately accountable. Accountability is independent of runtime delegation and must be verifiable across trust domains under an explicit trust policy.

Each link in the chain must identify the accountable party, the party it is accountable to, the scope and effective period, the issuer, and the proof by which a relying party validates it. A link must be asserted or accepted by the party taking on accountability: no organization can be placed in an agent's accountability chain without its own verifiable assertion. Financial assurers, such as insurers or guarantors, may be attached to a link to show that a party's obligations are backed up to a stated limit. They back accountability but do not become the ultimate accountable party. A relying party must be able to resolve the chain to the ultimate accountable party at a stated assurance level, without necessarily learning the identities of intermediate parties. These primitives record the structure of accountability. How liability is allocated among those parties in a given incident is determined by contract and law, and is out of scope.

The binding between an agent's identifier and its responsible party must be asserted by the responsible party or an authority acting on its behalf. Where the agent controls an operational key, the binding must include proof that the subject key participated in or accepted it. Operational-key rotation, version updates, and platform or runtime changes must not silently replace the agent's identity. A change of ownership or control must create a verifiable succession record, so that the ultimate accountable party remains identifiable at every point in the agent's lifecycle, including after retirement. The identifier namespace must have documented registration, transfer, and dispute processes. Accountability bindings apply to agent instance identifiers; an agent type identifier may reference its provider but cannot by itself identify a responsible party.

A company car illustrates the chain. The VIN identifies the vehicle. The employee at the wheel answers first for how it was driven. The company, as registered owner, ultimately answers for it. The company's insurer covers the financial loss up to the policy limit. Title history records who held ownership at each point, and a transfer changes the owner without erasing the prior record.

**Relevant and proposed standards:** DNS-anchored accountable identifiers (DNSid; the accountability layer of ANS), LEI / vLEI, X.509 organization validation, registry-backed ownership records, domain-control validation, and append-only verifiable logs.

### 3.3 Discovery Metadata

Discovery metadata is structured information that allows a relying party to locate an agent and decide whether to interact with it, before any interaction begins. It describes what the agent is, who is responsible for it, what it is capable of, and how to access it.

For discovery to work across organizational boundaries, the metadata format must be registry-agnostic. A relying party should be able to resolve an agent identifier to its metadata regardless of which platform registered the agent. The metadata must be signed or integrity-protected to prevent tampering, and must carry or reference the provenance chain — who provides, distributes, and operates this agent — so trust decisions can be made without contacting the provider, distributor, or responsible party directly.

A vehicle registration record linked to a VIN captures the same idea: it describes the make, model, certifications, and operating permissions, and a checkpoint can look it up without calling the manufacturer.

**Relevant and proposed standards:** DNS-AID, ANS/ARD (Agent Name Service / Agent Resource Discovery), OpenID Connect Discovery, Model Card / Agent Card formats, `.well-known` URIs (RFC 8414).

### 3.4 Attestation

In an interoperable environment, attestation is a verifiable assertion, bound to its subject and issuer, about an agent, its properties, or actions taken with respect to it, made by a party with standing to make that claim. It goes beyond naming the agent: it provides evidence that the agent's identity claims are true — that it was built and configured as claimed, and optionally that it is running in the expected environment.

Attestation is distinct from authentication. Authentication confirms a claimed identity at the moment of a request. Attestation provides the underlying evidence that makes those claims trustworthy in the first place.

There are many types of attestation:

- **Identity attestation** — a claim that a specific identifier belongs to a specific agent, issued by an authority with standing such as the provider or a trusted registry; this is the minimum required for an agent to authenticate to a relying party.
- **Provenance attestation** — a verifiable record of who built the agent, from what model or codebase, with what training or configuration; lets relying parties evaluate the trustworthiness of the agent's origins.
- **Software attestation** — a cryptographic measurement of the software running as the agent (model weights hash, system prompt hash, tool configuration), allowing relying parties to confirm the agent matches a known approved configuration.
- **Environment and hardware attestation** — a verifiable claim about the platform where the agent runs, such as a Trusted Execution Environment or attested hardware; optional but recommended for high-assurance deployments.
- **Approval (consent) attestation** — a verifiable assertion that a given principal approved a given delegation or consequential action: who, when, on what evidence.
- **Intervention attestation** — a verifiable statement, issued by a responsible party, that it altered the agent's decision-governing configuration (system prompt, memory, policy, weights) at a given time, under which authority. Software attestation shows that the artifact changed; this records who changed it.

Attestation claims must be signed by a key traceable to a trusted authority and carry freshness evidence to prevent replay. Claims should support granular selective disclosure and be verifiable by relying parties without contacting the attesting party. For composed agents, attestation may span multiple layers — provider, distributor, responsible party — and must be evaluated as a chain.

A vehicle certification process illustrates this layering: the manufacturer attests to the build, a regulator certifies safety compliance, and on-board diagnostics confirm runtime integrity. An insurer or regulator can verify each layer independently.

**Relevant and proposed standards:** IETF RATS (RFC 9334), OIDC ID Tokens / JWTs, X.509 certificates, TPM/TEE attestation, SLSA, in-toto / SBOM, Transaction Tokens (draft-ietf-oauth-transaction-tokens).

### 3.5 Delegation

#### 3.5.1 Elements of a Delegation

Every delegation, whether granted by the principal or by an agent passing authority on, has a delegator that grants authority and a delegatee that receives it, within constraints the delegator sets (actions, counterparties, limits, and validity period). The delegator keeps the power to withdraw the grant. At the moment of use, a relying party must be able to verify five elements: the delegator and its standing to grant the authority; the delegatee; the constraints; the credential that carries the grant; and the grant's state (in force, expired, or revoked). Authority is established from that evidence at the time of use, not from the agent's own account of it. Handing work to a process or workload the agent spawns is not delegation: it transfers execution, not authority. Where a delegation authorizes a consequential action, the principal's approval should be shown by an approval attestation (Section 3.4). This primitive covers how delegated authority is represented and verified as part of an agent's identity. The policies that decide what a given grant permits are authorization concerns and are out of scope.

#### 3.5.2 Delegation Chains and Accountability Chains

Two chains are easily confused. A delegation chain is a sequence of credentials, each issued by some party and each verifiable on its own terms; it records where an agent's authority came from. An accountability chain (Section 3.2) is the sequence of parties that answer for an agent; it records who stands behind the agent's actions. Each hop in a delegation chain adds an issuer whose own authority, scope, and revocation state must be proven. Unless every hop can be verified independently, the relying party is left trusting the last hop's account of the hops before it. Even when every hop verifies, a delegation chain written by agents cannot show who stands behind an action. A relying party must therefore never read a delegation chain as an accountability chain. Accountability links must be asserted or accepted by the parties taking on accountability, as Section 3.2 requires.

#### 3.5.3 Multi-hop Delegation

An agent may pass authority it holds to another agent or a subagent, which may pass it on again. Each hop must identify the delegator and delegatee by their identifiers, state the constraints of the grant, and carry proof that those constraints are no wider than the delegator's own. A delegatee can never hold more authority than its delegator, so constraints may narrow at each hop but never widen. Each hop must be signed by its delegator and be verifiable on its own terms. A relying party must be able to verify the full chain back to the principal from the credential presented, including every hop, its constraints, its validity period, and its state, across trust domains and without contacting each delegator. Each hop must have a declared revocation time bound, and revoking a hop invalidates all authority derived from it (Section 3.6).

#### 3.5.4 Root Issuance

Where a trust domain can support it, chains can be shortened by root issuance: agent credentials, including subagent credentials, are issued directly by a root authority rather than by other agents. The root authority issues under the principal's verified identity or on the principal's verified instruction. Each credential's scope is fixed at issuance and can be no wider than its parent credential's scope, nor wider than the principal's identity assurance level permits. A subagent's credential is bound to its parent's lifecycle: when the parent's credential is revoked or expires, the subagent's is no longer in force, so the cascade required by Section 3.6 follows from issuance itself rather than from coordination between systems.

Within a trust domain, root issuance satisfies the principles of Section 5 by construction: no agent-written hop can widen authority, every action traces to the root authority in one step, and each agent has a single revocation point with a declared time bound. Across trust domains, a relying party decides which root authorities it accepts and at what assurance level. The cost is availability: a new agent or subagent can be created only when the root authority is reachable, or under a mandate the root authority signed in advance that fixes the subagent's scope and lifecycle. Designs may combine both patterns, using root issuance within a trust domain and multi-hop delegation across trust domains.

A valet key illustrates attenuated delegation: the owner hands the valet a key that starts the car but cannot open the trunk or glovebox, and the valet cannot hand anyone a key with more access than the one they were given. A fleet office illustrates root issuance: every driver's key card is issued by the fleet office, limited to the vehicles and hours that driver needs, and deactivated centrally.

**Relevant and proposed standards:** OAuth 2.0 Token Exchange (RFC 8693), GNAP (RFC 9635), Transaction Tokens (draft-ietf-oauth-transaction-tokens), Agent Authorization Protocol (draft-hardt-aauth-protocol).

### 3.6 Revocability

Revocability is the independent ability to invalidate an agent's identity credential, delegated authority, or active session — without requiring coordination with every downstream system that has already accepted that credential. It is a property of the identity infrastructure, not of any individual credential.

Revocation must be enabled for any party with standing — the principal who delegated, the responsible party, an accountable party higher in the agent's accountability chain, or the provider — without the agent's cooperation. It must propagate within a bounded time window; long-lived credentials without revocation mechanisms are a design anti-pattern. Revocation may target a specific credential, a specific delegation hop, or all authority derived from a given principal, and cascades to all agents and subagents in that delegation tree. Every revocation event should be logged in a tamper-evident record. Critically, revocation must hold across organizational and trust-domain boundaries — an agent operating in an external system must lose access when its authority is revoked, not only within the issuing domain.

A vehicle safety recall that pulls self-driving certification across all affected models — not just in the manufacturer's systems but across every road authority and tolling system that accepted it — illustrates what cross-domain propagation requires in practice.

**Relevant and proposed standards:** OCSP (RFC 6960), CRLs (RFC 5280), OAuth 2.0 Token Revocation (RFC 7009), push-based revocation notices, short-lived credentials with mandatory refresh, OIDC Back-Channel Logout 1.0.

---

## 4. Interoperability Gaps

The primitives defined above are motivated by concrete gaps in current standards and deployed infrastructure.

- There is no common schema that binds an agent name to its provider organization, responsible party, and version in a portable, resolvable form. Existing workload identifiers — SPIFFE IDs, OAuth client IDs — were not designed to carry agent-specific provenance.
- There is no interoperable discovery path allowing a relying party to resolve an agent identifier to its metadata across registries, platforms, and organizations. Each platform implements proprietary discovery today.
- There is no standard way to represent an accountability chain, or to attach financial backing such as insurance, in a form a relying party can verify.
- Existing delegation standards such as OAuth 2.0 Token Exchange (RFC 8693) were designed for human-to-service delegation. RFC 8693's nested `act` claims record prior actors for information only and are not used in access decisions. No standard carries a verifiable, multi-hop agent delegation chain whose constraints narrow at each hop. Nor is there a standard way for a relying party in one trust domain to recognize the root authorities of another, and at what assurance level.
- Existing identity infrastructure treats agents either as OAuth clients or as users. No standard primitive represents an agent as distinct from both — carrying its own provenance, its responsible party, and its delegated authority in a single verifiable artifact.
- There is no standard protocol for registering an agent identity with the resource servers, registries, and tool providers it needs to operate with — the equivalent of dynamic client registration for OAuth clients, adapted for agents.
- When a principal authorizes an agent within their organization's systems, that delegation does not carry across organizational boundaries. An agent operating externally cannot present its principal-delegated authority in a form the external system can verify.
- There is no common format for the agent-specific attestations in Section 3.4 — approval and intervention attestations in particular — or for evaluating a layered attestation chain across provider, distributor, and responsible party.
- Existing revocation mechanisms are either pull-based or confined to the issuing authorization server. There is no standard way to push revocation to every system across trust domains that has accepted an agent's credential, or to cascade it through a multi-hop delegation chain.

---

## 5. Design Principles

1. Agent identity must be distinct from, but relatable to, any service or workload identity the agent also holds. Systems should treat agents as a separate identity class rather than mapping them onto existing human or application identity models.
2. Every agent action must be traceable through the delegation chain to the principal that authorized it, and through the accountability binding to the ultimate accountable party that answers for it (today, each a natural or legal person). A relying party must be able to verify that both exist, at a stated assurance level, without necessarily learning who they are. Untraceable agents should not be trusted.
3. No delegation hop may grant authority the delegator does not hold, and each hop must carry proof that its constraints are no wider than the delegator's. Subagents are bounded by the authority of their parent, which is bounded by the principal.
4. Identity credentials and delegated authority must be revocable. Long-lived or non-revocable agent credentials are a design anti-pattern.
5. Agent identity primitives must be implementable without dependency on any single vendor, platform, or proprietary protocol. Where open standards apply, they should be adopted or extended rather than replaced.
6. The infrastructure should support selective disclosure — proving specific claims without revealing more than necessary to the relying party.
7. Agent identity primitives should compose with existing enterprise infrastructure: IdPs, PKI, OAuth authorization servers, and directory services. Adoption cost matters.
8. Where the operating environment allows it — TEE, HSM, cloud enclave — hardware attestation provides a stronger root of trust. This is not required in all deployments but should be architecturally accommodated.

---

## 6. Open Points

**Subagent identity** — When a parent agent spawns a subagent, it is not yet defined how that subagent's identity should be structured. Does it carry its own identifier bound to its provider, inherit or derive one from the parent, or receive a scoped identifier tied to the delegation? How does its identity relate to the delegation chain, and what is the minimum identity a subagent must present to a relying party? This needs resolution before the delegation primitive can be fully specified.

---

## 7. Related Work and References

### Identity and Naming

- W3C Decentralized Identifiers (DIDs) v1.0
- SPIFFE / SPIRE — Secure Production Identity Framework for Everyone
- DNS-based Agent Identity Landscape
- DNSid — DNS-Anchored Durable Identity for AI Agents
- ANS v2 — Agent Name Service (draft-narajala-courtney-ansv2-00)

### Discovery

- OpenID Connect Discovery 1.0
- OAuth 2.0 Authorization Server Metadata (RFC 8414)

### Attestation

- IETF RATS Architecture (RFC 9334)
- SLSA — Supply-chain Levels for Software Artifacts

### Delegation

- OAuth 2.0 Token Exchange (RFC 8693)
- GNAP — Grant Negotiation and Authorization Protocol (RFC 9635)
- Transaction Tokens (draft-ietf-oauth-transaction-tokens)
- Agent Authorization Protocol (draft-hardt-aauth-protocol-01)

### Revocation

- Online Certificate Status Protocol — OCSP (RFC 6960)
- OAuth 2.0 Token Revocation (RFC 7009)
- OIDC Back-Channel Logout 1.0

---

*This document is a working draft of the Agentic AI Foundation Identity & Trust Working Group. Feedback, corrections, and contributions are welcome via the working group's GitHub repository and mailing list.*
