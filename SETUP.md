# Explicit Memory LinkedIn Workflow - Setup Guide

This n8n workflow demonstrates explicit memory management for AI-driven LinkedIn post generation. The system learns from user feedback to improve quality over time through pattern synthesis rather than simple accumulation.

## Prerequisites

- **n8n** (self-hosted or cloud instance)
- **Google Account** with access to Google Docs (for context storage)
- **Anthropic API Key** (for Claude integration)
- **Slack Workspace** with permission to create/authenticate apps
- **Google Docs with template structure** (see below)

## Installation

1. Clone or download this repository
2. In your n8n instance, go to **Workflows** → **Import from file**
3. Select `explicit-memory-linkedin-workflow.json`
4. You'll see warnings about missing credentials - these need to be configured

## Configuration Steps

### 1. Google Docs OAuth Setup

The workflow reads from multiple Google Docs to gather context for post generation.

**In n8n:**
1. Go to **Credentials** → Create new → Search "Google Docs OAuth2"
2. Authenticate with your Google account
3. Copy the credential ID (shown as `YOUR_GOOGLE_DOCS_CREDENTIAL_ID` in the workflow)

**Nodes affected:**
- "Get base context"
- "Get client context"
- "Get memory and learnings"
- "Get past learned context"
- "Update memory bank"

### 2. Anthropic API Setup

The workflow uses Claude for hook generation, post writing, refinement, and feedback synthesis.

**In n8n:**
1. Go to **Credentials** → Create new → Search "Anthropic API"
2. Paste your Anthropic API key
3. Copy the credential ID (shown as `YOUR_ANTHROPIC_API_CREDENTIAL_ID` in the workflow)

**Nodes affected:**
- "Draft hook" (generates 10 hook variations)
- "Generate post" (writes complete LinkedIn post)
- "Run checkList" (validates against style guide)
- "Post refinement" (fixes issues from checklist)
- "Learning from feedback" (structures feedback into guidelines)
- "Synthesis feedback context" (merges new feedback with historical patterns)

### 3. Slack Integration Setup

The workflow sends messages to Slack for hook selection, post review, and feedback collection.

**In n8n:**
1. Go to **Credentials** → Create new → Search "Slack OAuth2"
2. Create a Slack app in your workspace (or use existing)
3. Authenticate and authorize the connection
4. Copy the credential ID (shown as `YOUR_SLACK_CREDENTIAL_ID` in the workflow)

**Your Slack User ID:**
1. In Slack, open your profile
2. Click **Edit profile** → **About** tab
3. At the bottom, find your user ID (format: `U08UP5SLDFH`)
4. Replace `YOUR_SLACK_USER_ID` in the workflow with your actual user ID

**Nodes affected:**
- "Send message and wait for response" (choose hook)
- "Send post for review" (get feedback)
- "Workflow complete" (completion notification)
- "Ask for user instruction" (optional additional instructions)
- "Workflow completed" (learning complete notification)

### 4. Google Docs Configuration

Create three Google Docs with the following structure:

#### Document 1: Client Context
- Contains your bio, background, expertise
- Include any personal voice characteristics or style notes
- Example format:
  ```
  # Angelina Yang - West Operators
  
  ## Background
  Co-founder of West Operators, focused on AI discoverability...
  
  ## Voice & Style
  Technical but accessible, conversational, data-driven...
  ```

#### Document 2: Style Guide & Checklist
- Must include the section marker: `## LinkedIn Post Self-Check Verification`
- Include your writing guidelines, format preferences, dos/don'ts
- Include your preferred framework or custom guidelines
- Include the section marker: `# 🔄 LIVING LEARNINGS` (for memory storage)
- Then: `## Learning starts here:` (where new learnings get appended)

Example structure:
```
# LinkedIn Writing Standards

## Writing Rules
1. Hook under 10 words
2. Single core message
3. Clear call-to-action
...

## LinkedIn Post Self-Check Verification
- [ ] Hook is under 10 words
- [ ] Post has a single core message
- [ ] Visual rhythm varies
...

# 🔄 LIVING LEARNINGS

## Learning starts here:
[New learnings will be appended here by the workflow]
```

#### Document 3: Memory/Learnings Bank
- Start with your framework (custom style)
- Include the section markers exactly as in Document 2
- This is where the workflow appends synthesized learnings

**In the workflow, replace:**
- `YOUR_GOOGLE_DOC_ID` (in "Get base context") → Your Client Context doc ID
- `YOUR_GOOGLE_DOC_ID` (in "Get memory and learnings") → Your Style Guide doc ID
- `YOUR_GOOGLE_DOC_ID` (in "Get past learned context" and "Update memory bank") → Your Memory Bank doc ID

**How to get Google Doc IDs:**
1. Open the Google Doc
2. Copy the URL: `https://docs.google.com/document/d/[ID]/edit`
3. The ID is the long string between `/d/` and `/edit`

### 5. Webhook IDs

The workflow includes multiple webhook endpoints for Slack interactions. These are auto-generated when you import.

**After import:**
1. Open each node with a webhook (marked with 🔗 in the node name)
2. Click the **Copy URL** button
3. The webhook ID field will auto-populate

**Nodes with webhooks:**
- Webhook (initial trigger from Slack)
- Send message and wait for response
- Send post for review
- Ask for user instruction

## Running the Workflow

### First Run (Initial Testing)

1. Go to your workflow in n8n
2. Click the **Test** button
3. The webhook trigger will be ready
4. From Slack, send: `/create_linkedin_angelina [google_doc_url]`
   - Replace `[google_doc_url]` with a link to a Google Doc containing the article/topic for the post

### Workflow Steps Explained

1. **Extract Context** - Fetches client info, source material, style guide, memory bank
2. **Draft Hooks** - Claude generates 10 different hook angles
3. **Select Hook** - Slack message with hook options; you choose the best one
4. **Generate Post** - Claude writes the complete post using the selected hook
5. **Verify Checklist** - Claude validates against your style guide
6. **Refine** - Any identified issues are fixed automatically
7. **Send for Review** - Post appears in Slack; you provide feedback or approve
8. **Learning Loop** (if feedback provided):
   - Feedback is refined into actionable guidelines
   - New learnings are synthesized with existing patterns
   - Memory bank is updated with synthesized guidelines
9. **Complete** - Slack notification confirms success

## Understanding the Memory Architecture

The workflow implements **three-tier memory management:**

**Tier 1: Core Framework** (immutable)
- Your base style guide and whoever-you-like-top-voice framework
- Preserved at the top of the memory bank
- Never changes; only learnings section grows

**Tier 2: Living Learnings** (evolving)
- New synthesis guidelines added after each feedback cycle
- Marked by the section: `## Learning starts here:`
- Automatically updated by the workflow

**Tier 3: Synthesis Logic**
- Recency weighs 60%, historical patterns 40% (or however setting you prefer)
- When rules conflict, most frequent/recent wins
- Specific feedback converted to generalizable principles

Each time you provide feedback, the workflow:
1. Captures your feedback exactly as given
2. Refines it into structured guidelines
3. Compares against existing learnings
4. Synthesizes into evolved rules
5. Updates the memory bank with the complete synthesis

## Customization

### Changing the Post Style

Edit the "Draft hook" node prompt to change:
- Number of hooks (currently 10)
- Hook format and structure
- Any specific constraints

### Adding Custom Validation

Edit the checklist in your Style Guide document. The "Run checkList" node will validate against whatever checklist you define there.

### Modifying the Learning Synthesis

Edit the "Synthesis feedback context" node to change:
- Recency weighting (currently 60/40)
- How conflicts are resolved
- Output format for guidelines

## Troubleshooting

**"Document not found" error:**
- Verify Google Doc IDs are correct (no `/edit` or extra characters)
- Confirm the Google Docs OAuth credentials have access to these documents
- Ensure documents aren't in a shared drive with limited permissions

**Webhook authentication errors:**
- Re-authenticate the Slack OAuth credential
- Confirm your Slack user ID is correct
- Check that your Slack app has the necessary permissions

**Claude API errors:**
- Verify your Anthropic API key is valid and active
- Check that your account has available quota
- Review the API response in the node execution logs

**"Memory starts here" not found:**
- Ensure your Memory Bank document has exactly this text: `## Learning starts here:`
- Check that the document structure matches the expected format

## Tips for Best Results

1. **Clear feedback format:** When providing feedback, use the structured format:
   - What worked well (to repeat)
   - What needs adjustment (to change)
   - Any specific preferences

2. **Consistent context:** Keep your client context, style guide, and source material well-organized and up-to-date

3. **Regular synthesis:** Run multiple posts through the workflow to build a robust pattern of learnings. The system improves with feedback cycles.

4. **Monitor memory growth:** Periodically review your memory bank to ensure learnings are accurate and actionable

## Security Notes

- This workflow JSON contains placeholders for all credentials
- **Never commit actual API keys, tokens, or IDs to version control**
- All credentials are stored securely in your n8n instance
- Webhook IDs are unique per instance; regenerate before sharing

## Support & Questions

For issues with the workflow logic, refer to the inline code comments in each node. For n8n-specific issues, consult the [n8n documentation](https://docs.n8n.io/).
