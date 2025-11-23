# Quick Start Guide

Get your explicit memory LinkedIn workflow running in 15 minutes.

## 5-Minute Setup Checklist

### Step 1: Gather Your Credentials (5 min)

You need three things:

**Google Docs OAuth:**
- In n8n: Credentials → New → "Google Docs OAuth2" → Authenticate
- Copy the credential ID

**Anthropic API:**
- Go to https://console.anthropic.com/
- Get your API key
- In n8n: Credentials → New → "Anthropic API" → Paste key
- Copy the credential ID

**Slack Integration:**
- In n8n: Credentials → New → "Slack OAuth2" → Authenticate
- Copy the credential ID
- Get your Slack user ID: Profile → About (bottom)

### Step 2: Create Your Google Docs (5 min)

Create 3 Google Docs:

**Doc 1: Client Context**
```
# Your Name

## Background
[Your bio/expertise]

## Voice
[How you write]
```

**Doc 2: Style Guide** (include these exact sections)
```
# Writing Guidelines
[Your rules...]

## LinkedIn Post Self-Check Verification
- [ ] Hook is under 10 words
- [ ] Single core message
- [ ] Clear CTA
[Add more...]

# 🔄 LIVING LEARNINGS

## Learning starts here:
```

**Doc 3: Memory Bank**
```
# My Framework
[your writing framework...]

# 🔄 LIVING LEARNINGS

## Learning starts here:
```

Get the Google Doc IDs from the URL: `https://docs.google.com/document/d/[ID]/edit`

### Step 3: Configure Workflow (5 min)

1. In n8n, import: `explicit-memory-linkedin-workflow.json`
2. Find these nodes and update:

**"Get base context"** (code node)
- Line 3: Replace `YOUR_GOOGLE_DOC_ID` (client context) with your Doc 1 ID

**"Draft hook"** (Anthropic node)
- Credentials: Select your Anthropic credential

**"Get memory and learnings"** (HTTP node)
- URL: Replace Doc ID with your Doc 2 ID
- Credentials: Select your Google Docs credential

**"Send message and wait"** & **"Send post for review"** (Slack nodes)
- User: Enter `YOUR_SLACK_USER_ID`
- Credentials: Select your Slack credential

**"Get past learned context"** (Google Docs node)
- URL: Replace with your Doc 3 ID
- Credentials: Select your Google Docs credential

**"Update memory bank"** (Google Docs node)
- URL: Replace with your Doc 3 ID
- Credentials: Select your Google Docs credential

**"Workflow completed"** (Slack node)
- User: Enter `YOUR_SLACK_USER_ID`
- Credentials: Select your Slack credential

## Test It

1. In Slack, send:
   ```
   /create_linkedin_angelina https://docs.google.com/document/d/[ARTICLE_DOC_ID]/edit
   ```

2. Select a hook from the options
3. Review the generated post
4. Provide feedback or approve
5. Watch the memory bank update

## Common Issues

**"Document not found"**
- Check your Google Doc IDs (no `/edit` suffix)
- Confirm Google Docs OAuth has access

**"User not found"**
- Get your Slack user ID: Profile → About → (bottom of page)
- Format should be `U` followed by letters/numbers

**"Credentials not authorized"**
- Re-authenticate each credential in n8n
- Confirm you have permission for each service

**"Webhook error"**
- The webhook IDs auto-generate; they're the long UUIDs in each node
- No manual setup needed; n8n handles it

## Next Steps

- Review [SETUP.md](SETUP.md) for detailed configuration
- Check [README.md](README.md) for architecture details
- Run multiple posts to build up your memory learnings
- Customize the prompts in each Claude node for your style

## Need Help?

1. Check SETUP.md for detailed steps
2. Review the inline comments in each node (click the code)
3. Consult [n8n docs](https://docs.n8n.io/) for platform-specific issues
