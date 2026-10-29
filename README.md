# SafeGuard
## Safe Guard 🛡️
### A Privacy Checkpoint for Responsible AI Use

**Protect the prompt. Preserve the work.**

Safe Guard is a proposed privacy-focused tool designed to help people identify and reduce the risk of exposing sensitive information when using external AI tools.

People often copy and paste work-related information into AI assistants to summarise complaints, draft reports, analyse information or solve problems. In the process, they may unintentionally share personal details, account references or confidential information.

Safe Guard aims to introduce a simple checkpoint before that information is shared, helping users recognise potential risks and create safer prompts without unnecessarily disrupting their work.

> **Project status:** Concept and design stage. The working prototype, test results and deployment readiness have not yet been established.

## The Problem

Using AI tools can improve productivity, but sharing information without reviewing it can create privacy and security risks.

For example, an employee may ask an AI assistant to summarise a customer complaint and accidentally include the customer's:

- Name or other identifying details
- Email address
- Phone number
- Identity number
- Account reference
- API key or other sensitive technical information

The employee may have a legitimate reason for using AI. The problem is that sensitive information can leave the organisation before anyone has an opportunity to identify and address the risk.

Training and security policies are important, but they may not always be enough when employees are under pressure to complete tasks quickly.

## Our Proposed Solution

Safe Guard is designed as a lightweight web application that checks text before a user shares it with an external AI tool.

Instead of banning AI use altogether, the proposed solution helps users understand what might be sensitive and gives them an opportunity to review a sanitised version of their prompt.

The intended workflow is:

1. **Compose** — Enter the text intended for an AI assistant.
2. **Scan** — Check the prompt for selected patterns associated with sensitive information.
3. **Explain** — Display detected findings with clear labels and plain-language explanations.
4. **Sanitise** — Replace detected values with placeholders such as `[EMAIL REDACTED]` or `[PHONE REDACTED]`.
5. **Review** — Compare the original and revised prompts and decide whether the revised version is still useful.

The user remains responsible for reviewing the final prompt before sharing it.

## Example: Before and After

**Before sanitisation**

```text
Please summarise the complaint from Thabo Mokoena.
Email: thabo@example.com
Phone: 071 234 5678
Account reference: 123456789
```

**Proposed sanitised version**

```text
Please summarise the complaint from [PERSON REDACTED].
Email: [EMAIL REDACTED]
Phone: [PHONE REDACTED]
Account reference: [ACCOUNT REFERENCE REDACTED]
```

The example uses fictional information to demonstrate the intended experience. It does not represent a completed or tested implementation.

Sanitisation can reduce obvious exposure, but contextual details may still identify a person. Users must review the revised prompt before sharing it.

## Systems Thinking

Safe Guard treats accidental exposure as a system problem rather than simply an employee mistake.

Several factors can contribute to the problem:

- **Time pressure:** Employees may prioritise speed over careful review.
- **Low visibility:** Sensitive information can be difficult to recognise within ordinary text.
- **Unclear rules:** Security guidance may be difficult to apply at the moment of work.
- **Control gaps:** Security teams cannot manually inspect every prompt.
- **Excessive restrictions:** Controls that disrupt legitimate work may encourage employees to find workarounds.

Safe Guard proposes a pre-sharing checkpoint at the point where the user can still review and change the information.

The goal is to make safer AI use easier without replacing organisational security policies or existing data-loss-prevention controls.

## Proposed Technical Approach

The initial prototype is intended to use a simple, transparent and testable architecture.

| Component | Proposed technology or approach |
|---|---|
| Web interface | Python with Streamlit |
| Sensitive-data detection | Local, rule-based regular expressions |
| Sanitisation | Deterministic replacement with placeholders |
| Testing | Automated tests using labelled fictional prompts |
| Version control | Git and GitHub |

The first version will focus on detecting a limited set of patterns, such as email addresses, phone numbers, South African ID-number-shaped strings and API-key-like tokens.

The detector will be designed to explain its findings rather than silently changing the user's text.

A rule-based approach is suitable for an initial prototype because it is straightforward to inspect, explain and test. However, it cannot reliably identify every form of sensitive information or understand every context.

## Privacy by Design

Privacy is a core consideration in the proposed design.

The initial prototype aims to:

- Process prompts locally within the application process.
- Avoid sending raw prompt text to a separate external AI service for analysis.
- Avoid accounts and persistent prompt storage in the first version.
- Avoid logging raw prompts by default.
- Use fictional information for demonstrations and testing.
- Explain the limitations of detection and sanitisation.
- Keep users responsible for reviewing the final prompt.

These measures are design intentions, not verified security guarantees. Hosting configuration, application logging, access controls and deployment settings will require review before real sensitive information is used.

Safe Guard is not a replacement for organisational security controls, approved AI-use policies, legal advice or a comprehensive data-loss-prevention solution. It does not guarantee compliance with POPIA or any other law.

## Testing and Validation

The prototype should be evaluated using a labelled collection of fictional prompts containing sensitive examples, non-sensitive examples and ambiguous cases.

The proposed evaluation will consider:

- **Detection recall:** How many of the labelled sensitive patterns are detected?
- **False-positive rate:** How often is harmless text incorrectly flagged?
- **Sanitisation correctness:** Are detected values replaced without unnecessarily changing the rest of the prompt?
- **Task usefulness:** Does the sanitised prompt still communicate the intended task?
- **User comprehension:** Can users understand the warning and decide what to do next?
- **Performance:** Does scanning complete quickly enough for the intended workflow?

Test results should include the size of the test set, how examples were labelled and cases where detection or sanitisation fails.

No performance figures or successful validation results are claimed at the concept stage.

## Scope of the First Prototype

### In scope

- A single-page prompt input interface.
- A scan action for selected sensitive-data patterns.
- Plain-language findings and risk indicators.
- Sanitised output with placeholder replacements.
- A before-and-after comparison.
- Copy functionality for the sanitised text.
- A visible limitations notice.
- Basic automated tests.

### Out of scope

- Direct integration with ChatGPT, Gemini, Claude or other AI platforms.
- A browser extension.
- Enterprise dashboards and policy administration.
- User accounts and persistent prompt storage.
- Machine-learning-based classification.
- Guaranteed detection of confidential information.
- Production security certification or compliance claims.

## Roadmap

**Stage 1 — Design**
- Define the user journey, detectable data patterns and warning messages.
- Finalise the initial prototype scope.

**Stage 2 — Prototype**
- Build the Streamlit interface.
- Implement detection and sanitisation rules.
- Display findings and compare original and revised prompts.

**Stage 3 — Test**
- Create labelled fictional test prompts.
- Measure detection errors and sanitisation correctness.
- Document limitations and test results.

**Stage 4 — Refine**
- Improve detection rules and user-facing explanations.
- Address issues identified during testing.

**Stage 5 — Explore future improvements**
- Assess organisation-specific policies, browser integration and deployment controls after the core workflow has been evaluated.

## Who Could Benefit?

Safe Guard is intended to support:

- **Employees and contractors** who use AI to complete everyday work.
- **Customers and data subjects** whose information should be handled responsibly.
- **IT and cybersecurity teams** seeking practical ways to reduce accidental information exposure.
- **Business leaders** who want to support productivity while managing risk.
- **Privacy and compliance teams** responsible for advising on appropriate data handling.

The exact rules and safeguards would need to be adapted to the organisation's requirements before enterprise use.

## What Makes Safe Guard Different?

Safe Guard focuses on the moment immediately before information is shared with an external AI tool.

Rather than relying only on training or blocking all AI use, it proposes a focused checkpoint that helps users:

- Identify potentially sensitive information.
- Understand why a finding matters.
- Replace obvious sensitive values with placeholders.
- Review the revised prompt before taking the next step.

Its proposed value lies in testing whether a simple, understandable intervention can reduce obvious exposure while preserving the usefulness of AI-assisted work.

Safe Guard is intended to complement existing safeguards, not replace them.

## Contributing

During prototype development, contributions may include:

- Improving detection patterns.
- Adding fictional test cases.
- Reporting false positives and missed detections.
- Improving accessibility and usability.
- Strengthening documentation and automated tests.

Contributions should not include real customer records, passwords, API keys or other confidential information.

## Current Status and Next Steps

Safe Guard is currently a concept supported by design and project documentation.

The next step is to implement the narrow prototype, test it using fictional data, document its performance and limitations, and use the findings to decide what should be improved.

The long-term goal is to explore a practical way to help people use AI more responsibly without making everyday work unnecessarily difficult.

---

**Safe Guard — Protect the prompt. Preserve the work.**
