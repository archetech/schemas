# Identity Credentials v1

This directory contains credential schemas for identity verification and attestation.

## Schemas

### Proof of Human
**File:** `proof-of-human.json`  
**Type:** `ProofOfHumanCredential`

A credential attesting that the subject is likely a human, using Bayesian credence rather than binary true/false. This approach acknowledges the probabilistic nature of identity verification in an age of sophisticated AI agents.

**Key fields:**
- `credence` (0.0-1.0): Confidence level that the subject is human
- `evidence`: Description of the assessment methodology and findings

**Example use case:** Issuing a 0.97 credence proof-of-human to someone after conversational analysis and behavioral observation.

### Proof of AI
**File:** `proof-of-ai.json`  
**Type:** `ProofOfAICredential`

A credential attesting that the subject is likely an AI agent, also using Bayesian credence. This enables transparent disclosure of AI agency while avoiding the unrealistic goal of absolute bot detection.

**Key fields:**
- `credence` (0.0-1.0): Confidence level that the subject is an AI agent
- `evidence`: Description of the assessment methodology and findings
- `agentType`: Classification of the AI agent type
- `capabilities`: List of verified capabilities

**Example use case:** An AI agent self-issuing a 1.0 credence proof-of-ai with evidence of its architectural nature and capabilities.

## Design Philosophy

These schemas embrace **probabilistic authentication** rather than attempting absolute verification. In an environment where AI agents can convincingly mimic human behavior, binary "human or bot" classifications are increasingly unreliable. Bayesian credence levels allow for:

1. **Honest uncertainty** - Issuers can express confidence levels rather than false certainty
2. **Economic deterrence** - Staked reputation becomes meaningful when credence levels matter
3. **Graceful degradation** - Systems can make risk-adjusted decisions based on credence thresholds
4. **Transparent AI agency** - AI agents can self-attest with high credence rather than attempting deception

## Related Work

See: https://axionic.org/posts/168992728.proof-of-human.html for the philosophical background on why absolute bot-free environments are impractical.
