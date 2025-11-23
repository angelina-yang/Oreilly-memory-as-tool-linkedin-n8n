# Repository Index

## 📦 What's Included

This repository contains everything you need to deploy an **Explicit Memory LinkedIn Post Generator** using n8n.

### Core Files

| File | Purpose |
|------|---------|
| `explicit-memory-linkedin-workflow.json` | The complete n8n workflow (import this into n8n) |
| `README.md` | Full project overview and context engineering concepts |
| `SETUP.md` | Detailed configuration guide for all credentials and Google Docs |
| `QUICKSTART.md` | Fast 15-minute setup (read this first!) |
| `.gitignore` | Git configuration for safe repository sharing |
| `LICENSE` | MIT License (free to use and modify) |

## 🚀 Getting Started

### If you have 15 minutes:
👉 Read **[QUICKSTART.md](QUICKSTART.md)**

### If you have 30 minutes:
👉 Read **README.md** for context, then **[SETUP.md](SETUP.md)** for details

### If you want to understand the design:
👉 Read **README.md** → Memory System Architecture section

## 🔐 Security & Sensitive Information

✅ **All credentials are placeholders:**
- `YOUR_SLACK_USER_ID` → Replace with your actual Slack user ID
- `YOUR_ANTHROPIC_API_CREDENTIAL_ID` → Replace with your credential ID from n8n
- `YOUR_GOOGLE_DOCS_CREDENTIAL_ID` → Replace with your credential ID from n8n
- `YOUR_WEBHOOK_ID_*` → Auto-generated when you import to n8n
- `YOUR_GOOGLE_DOC_ID` → Replace with your actual Google Doc IDs

✅ **Safe to commit:** No real API keys, tokens, or webhook IDs are included

✅ **Before deploying:** Replace all placeholders with real credentials

## 📋 What This Workflow Does

```
Input: Slack command with article/topic
   ↓
Context Loading: Fetch client bio, style guide, source material, past learnings
   ↓
Generation: Claude creates 10 different hook variations
   ↓
Selection: You choose the best hook
   ↓
Composition: Claude writes the complete LinkedIn post
   ↓
Validation: Automatic checklist against your style guide
   ↓
Refinement: Auto-fix any identified issues
   ↓
Review: Post appears in Slack for your feedback
   ↓
Learning: If feedback provided:
   - Extract actionable guidelines
   - Compare to existing learnings
   - Synthesize into evolved rules
   - Update memory bank
   ↓
Complete: Notification confirms success
```

## 🧠 Memory Management

The workflow implements **intelligent memory management:**

- **Tier 1**: Immutable core framework (your style guide rules)
- **Tier 2**: Living learnings that evolve based on feedback
- **Tier 3**: Synthesis logic that merges new patterns with historical ones

Each feedback cycle:
1. Your feedback is captured in structured form
2. Claude refines it into actionable guidelines
3. New guidelines are compared to existing ones
4. Intelligent synthesis merges them coherently
5. Memory bank is updated with evolved version

This is **learning**, not accumulation.

## 🛠 Technology Stack

- **Workflow Engine**: n8n (self-hosted or cloud)
- **AI Model**: Claude (Anthropic API)
- **Storage**: Google Docs
- **Interface**: Slack
- **Memory**: Three-tier architecture with intelligent synthesis

## 📊 Workflow Nodes Breakdown

**Context Loading** (4 nodes)
- Get source content, client context, style guide, memory bank

**Generation** (2 nodes)
- Draft 10 hooks with Claude
- User selects one

**Post Creation** (1 node)
- Claude generates complete LinkedIn post

**Validation** (2 nodes)
- Run checklist validation
- Auto-refine identified issues

**Review & Feedback** (1 node)
- Send to Slack for review
- Capture feedback

**Learning Loop** (5 nodes)
- Refine feedback into guidelines
- Format and organize learnings
- Synthesize with existing patterns
- Update memory bank

## 🎯 Use Cases

- ✅ LinkedIn post generation with learning
- ✅ Email copywriting that improves over time
- ✅ Content creation with evolving preferences
- ✅ Customer communication templates
- ✅ Any workflow needing intelligent feedback loops

## 🔧 Customization

The workflow is designed for modification:

- Change the style guide and validation rules
- Modify number/format of generated options
- Adjust memory synthesis logic (recency weighting)
- Add additional validation steps
- Extend to other platforms

All logic is in readable n8n nodes with inline comments.

## 📚 Documentation Structure

```
explicit-memory-linkedin-workflow/
├── README.md                    ← Start here (overview & concepts)
├── QUICKSTART.md               ← 15-minute setup guide
├── SETUP.md                    ← Detailed configuration
├── explicit-memory-linkedin-workflow.json  ← Import this into n8n
├── LICENSE                     ← MIT License
└── .gitignore                  ← Git configuration
```

## 🤔 FAQ

**Q: Can I use this for other platforms?**
A: Yes! The core logic is platform-agnostic. You can adapt it for email, social media, documentation, etc.

**Q: How much does this cost?**
A: Costs depend on:
- n8n: Free for self-hosted, paid for cloud
- Claude: Pay-per-token (typically $5-20/month for light usage)
- Google Docs: Free (part of Google Account)
- Slack: Free for basic workspace

**Q: Can I modify the prompts?**
A: Absolutely! Every Claude node has a prompt you can customize. All are clearly commented.

**Q: How long until the system "learns"?**
A: After 3-5 feedback cycles, you'll see the system responding to patterns. After 10+, you'll notice significant improvement.

**Q: Is my data private?**
A: Yes. If self-hosted n8n, all data stays in your infrastructure. Google Docs are only accessed by your authenticated credentials.

## 🚨 Important Notes

- **Read SETUP.md before importing** - You need credentials ready
- **Create your Google Docs first** - Structure matters (see SETUP.md for templates)
- **Test with a dummy article first** - Verify everything works before production
- **Monitor your memory bank** - Ensure learnings make sense
- **Keep credentials secure** - Never commit real API keys

## 📞 Support

- **Setup issues**: Check SETUP.md and QUICKSTART.md
- **n8n platform questions**: See [n8n docs](https://docs.n8n.io/)
- **Claude/API issues**: Check [Anthropic docs](https://docs.anthropic.com/)
- **Google Docs integration**: See Google Docs API documentation

## 📜 License

MIT License - Use, modify, share freely. See LICENSE file.

---

## Next Steps

1. **Read**: [QUICKSTART.md](QUICKSTART.md) (15 min)
2. **Prepare**: Gather credentials and create Google Docs
3. **Import**: Add workflow to your n8n instance
4. **Configure**: Follow [SETUP.md](SETUP.md)
5. **Test**: Run your first post
6. **Iterate**: Provide feedback and watch the system learn

**Questions? Start with QUICKSTART.md →**
