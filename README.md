# Explicit Memory LinkedIn Workflow

> A demonstration of explicit memory management for AI systems through n8n
>
> Built for O'Reilly's Context Engineering event

This n8n workflow showcases how AI systems can build genuine expertise through **explicit memory management** rather than token optimization. It generates engaging LinkedIn posts while learning and improving from user feedback.

## What This Demonstrates

This workflow is a practical implementation of the concepts from O'Reilly's "Explicit Memory Management: Building AI Systems That Learn From Experience" presentation. It illustrates:

- **Selective Context Engineering**: Loading only relevant context (client bio, style guide, source material, past learnings) rather than dumping token limits
- **Iterative Learning**: Capturing feedback, synthesizing patterns, and updating memory rather than accumulating raw examples
- **Three-Tier Memory Architecture**: Immutable core framework (Tier 1), living learnings that evolve (Tier 2), and smart synthesis logic (Tier 3)
- **Pattern Over Accumulation**: The system gets smarter by extracting generalizable principles, not just storing everything

## How It Works

```
1. Webhook Trigger (from Slack)
   ↓
2. Gather Context (4 Google Docs: client info, style guide, source material, memory bank)
   ↓
3. Generate 10 Hook Variations (Claude) → User selects one
   ↓
4. Write Full LinkedIn Post (Claude with selected hook)
   ↓
5. Validate Checklist (Claude verifies against style guide)
   ↓
6. Refine Issues (Claude auto-fixes any flagged problems)
   ↓
7. Send for Review (Slack) → User provides feedback or approves
   ↓
8. Learning Loop (if feedback):
   - Refine feedback into structured guidelines
   - Synthesize new guidelines with existing learnings
   - Update memory bank with evolved patterns
   ↓
9. Complete (confirmation notification)
```

## Key Features

✨ **Multi-Stage Generation**
- Hook generation with 10 variations (different angles)
- Full post composition
- Automatic validation and refinement
- All feedback integrated back into the system

🧠 **Explicit Memory Management**
- Preserves immutable core framework (your style guide)
- Appends synthesized learnings (not raw feedback)
- Intelligently merges new patterns with historical ones
- Recency-weighted synthesis (60% new, 40% historical patterns)

🔄 **Feedback-Driven Improvement**
- Captures structured feedback: what worked, what needs adjustment, specific preferences
- Converts feedback into actionable guidelines
- Intelligently handles conflicts (most frequent or recent pattern wins)
- Continuously evolves without losing core principles

📊 **Production Ready**
- Error handling and retries
- Checklist validation before sending
- Complete audit trail (all feedback logged)
- Configurable for different clients/voices

## Quick Start

### Prerequisites
- n8n (cloud or self-hosted)
- Google account with Docs access
- Anthropic API key (Claude)
- Slack workspace access

### Setup
1. Download `explicit-memory-linkedin-workflow.json`
2. In n8n, import the workflow
3. Follow the [detailed setup guide](SETUP.md) to configure:
   - Google Docs OAuth credentials
   - Anthropic API key
   - Slack integration
   - Your Google Docs (client context, style guide, memory bank)

### First Run
```
In Slack: /create_linkedin_angelina [google_doc_url]
```

Replace `[google_doc_url]` with a Google Doc containing the topic/article for the post.

## File Structure

```
explicit-memory-linkedin-workflow/
├── README.md                              # This file
├── SETUP.md                               # Detailed configuration guide
├── explicit-memory-linkedin-workflow.json # The n8n workflow (import this)
├── .gitignore                             # Git ignore patterns
└── docs/
    ├── ARCHITECTURE.md                    # Technical deep-dive
    ├── MEMORY-SYSTEM.md                   # Memory management details
    └── CUSTOMIZATION.md                   # How to adapt for other use cases
```

## Configuration

All sensitive information (API keys, credential IDs, webhook IDs) are represented as placeholders in the JSON:

- `YOUR_GOOGLE_DOCS_CREDENTIAL_ID` → Your Google Docs OAuth credential
- `YOUR_ANTHROPIC_API_CREDENTIAL_ID` → Your Anthropic API credential
- `YOUR_SLACK_CREDENTIAL_ID` → Your Slack OAuth credential
- `YOUR_SLACK_USER_ID` → Your Slack user ID (where messages are sent)
- `YOUR_WEBHOOK_ID_*` → Auto-generated webhook endpoints

**See [SETUP.md](SETUP.md) for complete configuration instructions.**

## Memory System Architecture

The workflow implements intelligent memory management through a three-tier system:

**Tier 1: Core Framework** (immutable)
```markdown
# Writing Standards
- Writing framework principles
- Your core style rules
- Non-negotiable guidelines
```

**Tier 2: Living Learnings** (evolves)
```markdown
## Learning starts here:
- Synthesized feedback patterns
- Emerging style preferences
- Contextual rules that improve
- Added/updated after each feedback cycle
```

**Tier 3: Synthesis Logic**
- Recency weighted 60%, historical 40%
- Conflicts resolved by frequency or recency
- Specific feedback → generalizable principles
- No contradictions; old rules updated, not appended

Each feedback cycle:
1. Your feedback is captured
2. Claude refines it into guidelines
3. New guidelines are compared to existing ones
4. Intelligent synthesis merges them coherently
5. Memory bank is updated with evolved version

This is **not accumulation** (storing every piece of feedback). It's **learning** (extracting patterns, updating understanding).

## Use Cases

- **LinkedIn post generation** with learning (as demonstrated)
- **Email copywriting** that improves over time
- **Content creation** with evolving style preferences
- **Customer communication** that learns from feedback
- **Any workflow** where you want AI to improve through explicit feedback

## Customization

The workflow is designed to be adapted. You can:
- Change the style guide and validation rules
- Modify the number/format of generated options
- Adjust the memory synthesis logic (recency weighting, conflict resolution)
- Add additional validation steps
- Extend to other platforms (not just LinkedIn/Slack)

See [docs/CUSTOMIZATION.md](docs/CUSTOMIZATION.md) for detailed examples.

## Technical Details

- **Base Model**: Claude 3.5 Opus
- **Execution Model**: n8n (workflow automation)
- **Storage**: Google Docs (context, learnings, feedback log)
- **Interface**: Slack
- **Memory Architecture**: Three-tier system with intelligent synthesis

## What Makes This Different

Most AI workflows optimize for token efficiency or automation speed. This one prioritizes **genuine learning**:

- ✅ Loads full context upfront (not streaming)
- ✅ Stores synthesized patterns (not raw data)
- ✅ Updates memory based on feedback (not just logging)
- ✅ Handles contradictions intelligently (not just appending)
- ✅ Builds toward expertise (not just faster outputs)

The tradeoff: slightly higher token usage upfront. The benefit: a system that actually gets smarter over time.

## Demo & Presentation

This workflow was built for O'Reilly's **Context Engineering** conference (February 26, 2026), where it demonstrates practical principles of building agentic AI systems through:

- **Explicit Memory Management**: Choosing what to remember vs. what to optimize away
- **Pattern Synthesis**: Converting feedback into evolving system intelligence
- **Context Engineering**: Loading the right information at the right time
- **Iterative Improvement**: Building systems that learn without accumulation

## License

MIT License - Use, modify, and share freely. See LICENSE file for details.

## Contributing

Found a bug? Have an improvement? Contributions welcome:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Questions?

- For n8n setup issues: [n8n Documentation](https://docs.n8n.io/)
- For workflow logic: Check the inline code comments in each node
- For context engineering concepts: See [ARCHITECTURE.md](docs/ARCHITECTURE.md)

---

**Built for the O'Reilly Context Engineering Conference**

*"Memory is not about storing more. It's about understanding better."*
