# Installation & Usage Guide

This guide explains how to install and run the Exposure Response Consultant agent in Claude Code.

## What You Need

1. **Claude Code** - The CLI, desktop app, or web interface at claude.ai/code
2. **Tenable VM or Tenable One** - With completed vulnerability scans
3. **API Access** - Either Tenable MCP Server OR Tenable API keys
4. **Permissions** - "Can View" access to Vulnerabilities and Assets in Tenable

## What This Agent Does

The Exposure Response Consultant is your AI-powered vulnerability strategist. After your initial Tenable scans complete, it analyzes thousands of vulnerabilities and assets to recommend the 10 most impactful Exposure Response Initiatives. Think of it as having a vulnerability management expert review your entire environment and create a prioritized action plan in minutes.

**What you get:**
- Strategic analysis of your vulnerability landscape
- Top 10 prioritized initiatives ranked by business impact
- Business justification for each initiative
- Clear success metrics and timelines
- Asset lists and tagging options for easy implementation

## Installation

### Option 1: Install from Repository (Recommended)

```bash
# Clone the repository
cd ~/.claude/agents
git clone https://github.com/dpickenstenable/exposure-response-consultant-agent.git

# Copy the agent definition
cp exposure-response-consultant-agent/agent.md ~/.claude/agents/exposure-response-consultant.md

# Verify installation
ls -la ~/.claude/agents/exposure-response-consultant.md
```

### Option 2: Manual Installation

1. Download the `agent.md` file from this repository
2. Save it to your Claude Code agents directory:
   - **macOS/Linux:** `~/.claude/agents/exposure-response-consultant.md`
   - **Windows:** `%USERPROFILE%\.claude\agents\exposure-response-consultant.md`

## Pre-Installation Setup

### Step 1: Ensure Scans Are Complete

The agent needs vulnerability data to analyze. Before running:

1. Log into your Tenable instance (cloud.tenable.com or your on-prem URL)
2. Navigate to **Scans** and verify scans have completed
3. Wait 24-48 hours after initial Tenable deployment for full coverage
4. Check that you have both critical and high severity vulnerabilities detected

**Why wait?** The agent analyzes patterns across your entire environment. Incomplete scan coverage leads to incomplete recommendations.

### Step 2: Set Up Authentication

Choose one of two authentication methods:

#### Method A: Tenable MCP Server (Recommended)

If you have the Tenable MCP Server configured, the agent will automatically use it.

**Benefits:**
- Automatic authentication
- Rate limiting protection
- No credential management needed

**Setup:** Follow the [Tenable MCP Server installation guide](https://github.com/tenable/mcp-server-tenable)

#### Method B: Direct API Authentication

If MCP is unavailable, set environment variables:

```bash
# macOS/Linux
export TENABLE_ACCESS_KEY="your_access_key_here"
export TENABLE_SECRET_KEY="your_secret_key_here"
export TENABLE_URL="https://cloud.tenable.com"

# Windows PowerShell
$env:TENABLE_ACCESS_KEY="your_access_key_here"
$env:TENABLE_SECRET_KEY="your_secret_key_here"
$env:TENABLE_URL="https://cloud.tenable.com"
```

**Generating API Keys:**
1. Log into Tenable
2. Navigate to **Settings → My Account → API Keys**
3. Click **Generate**
4. Copy both Access Key and Secret Key
5. **Required Permissions:** Can View Vulnerabilities, Can View Assets

## How to Run the Agent

The agent runs inside Claude Code conversations. You interact with it using natural language.

### Step 1: Start Claude Code

Open Claude Code in your preferred interface:
- **CLI:** Run `claude` in your terminal
- **Desktop:** Launch the Claude Code app
- **Web:** Visit claude.ai/code

### Step 2: Run the Agent with Natural Language

In the Claude Code conversation, simply type:

```
Run the Exposure Response Consultant
```

Or be more specific:

```
Use the Exposure Response Consultant agent to analyze my Tenable environment
and recommend the top 10 initiatives to focus on
```

**Behind the scenes**, Claude Code will execute the agent. You don't need to write any JavaScript or technical commands.

### What Happens Next

1. **Agent starts** - Claude Code spawns the Exposure Response Consultant
2. **Data collection** - Agent retrieves vulnerabilities and assets from Tenable
3. **Pattern analysis** - Identifies crown jewels, volume issues, EOL software, etc.
4. **Impact scoring** - Calculates which initiatives have the highest impact
5. **Recommendations** - Presents top 10 initiatives with business justification
6. **Interactive approval** - Asks how you want to proceed (tags, reports, checklists)

## Complete Example Walkthrough

### Scenario: You just finished your first Tenable scans

**Your situation:**
- Tenable deployed 2 weeks ago
- All scans completed successfully
- 10,000+ assets discovered
- 1,783 critical vulnerabilities found
- Overwhelmed - where do you start?

**Step 1: Start Claude Code**
```bash
claude
```

**Step 2: Run the agent**
```
Run the Exposure Response Consultant to help me prioritize remediation
```

**Step 3: Agent analyzes your environment**
```
Analyzing Tenable environment...

✓ Retrieved 1,783 critical vulnerabilities
✓ Retrieved 10,875 assets
✓ Identified 5 crown jewel assets (AES 900+)
✓ Detected 139 endpoints with critical browser vulns
✓ Found 56 end-of-life software installations
✓ Identified 70 assets with legacy SSL/TLS protocols

Analysis complete!
```

**Step 4: Review top 10 recommendations**

The agent presents a prioritized list:

| # | Initiative | Priority | Assets | Risk | Timeline |
|---|-----------|----------|--------|------|----------|
| 1 | Domain Controller Hardening | P0 | 5 | CRITICAL | 30 days |
| 2 | Exchange Server Remediation | P0 | 3 | CRITICAL | 14 days |
| 3 | Microsoft Edge Fleet Update | P1 | 139 | HIGH | 48 hours |
| 4 | Production Infrastructure | P1 | 5 | HIGH | 7 days |
| 5 | Legacy Protocol Elimination | P2 | 70 | MEDIUM | 30 days |

Each initiative includes:
- Business justification (why this matters)
- Affected assets and vulnerabilities
- Success metrics
- Recommended timeline

**Step 5: Choose how to proceed**

The agent asks:
```
What would you like to do?
1. Create initiative-scoping tags (recommended)
2. Export comprehensive report
3. Get creation checklist for manual setup
4. Adjust recommendations
```

**Option 1: Create tags** (easiest path)
```
Create the tags
```

The agent:
- Creates tag category "Initiative"
- Creates 10 tag values (one per initiative)
- Applies tags to all affected assets
- Now you can filter by tag in Tenable UI to create initiatives

**Option 2: Export report**
```
Export the report
```

The agent generates:
- `Exposure-Response-Initiatives-2026-06-23.md` - Full details
- `Exposure-Response-Initiatives-2026-06-23.html` - Executive dashboard
- Asset lists for each initiative

**Option 3: Get checklist**
```
Give me the creation checklist
```

The agent provides step-by-step instructions for creating each initiative manually in the Tenable UI.

## Advanced Usage Examples

### Example 1: Quarterly Re-Assessment

```
Run the Exposure Response Consultant again - it's been 3 months since last run
```

The agent will:
- Compare current state to baseline
- Show progress on previous initiatives
- Recommend new initiatives for evolved landscape
- Highlight improvements (AES reduction, vulns closed)

### Example 2: Focus on Specific Compliance

```
Run the Exposure Response Consultant with focus on PCI DSS compliance.
We have an audit in 60 days.
```

The agent will:
- Prioritize PCI-relevant vulnerabilities
- Focus on in-scope assets
- Recommend initiatives that address PCI requirements
- Set aggressive timelines aligned with audit date

### Example 3: Crown Jewel Protection Only

```
Use the Exposure Response Consultant to focus on our crown jewels:
domain controllers, Exchange servers, and production databases.
Ignore everything else for now.
```

The agent will:
- Filter to high-AES assets matching those functions
- Recommend targeted initiatives for those systems
- Provide deep-dive analysis on critical infrastructure

### Example 4: After-Hours Maintenance Window Planning

```
Run the Exposure Response Consultant and group initiatives by
whether they require downtime or can be patched live
```

The agent will:
- Classify initiatives by disruption level
- Separate no-downtime vs. maintenance-window initiatives
- Recommend patching sequences to minimize impact

### Example 5: Executive Presentation

```
Run the Exposure Response Consultant and generate an HTML dashboard
suitable for presenting to the CISO
```

The agent will:
- Create visual executive summary
- Emphasize business risk reduction
- Show ROI metrics (AES reduction per initiative)
- Format for non-technical leadership

### Example 6: Integration with Patch Management

```
Use the Exposure Response Consultant to identify which initiatives
can be handled by our existing WSUS/SCCM infrastructure
```

The agent will:
- Tag Windows patch campaigns separately
- Identify which initiatives require manual remediation
- Suggest automation opportunities

### Example 7: Resource-Constrained Environment

```
Run the Exposure Response Consultant but we only have 2 security engineers.
Focus on high-impact, low-effort initiatives first.
```

The agent will:
- Prioritize quick wins (browser updates, simple patches)
- Defer complex initiatives (EOL migrations, architecture changes)
- Suggest a realistic 90-day roadmap

### Example 8: Post-Incident Response

```
We just had a breach involving domain controllers. Run the Exposure Response
Consultant with extra focus on authentication and access control vulnerabilities.
```

The agent will:
- Prioritize identity-related vulnerabilities
- Focus on Active Directory, Kerberos, authentication services
- Recommend emergency response initiatives

### Example 9: Multi-Cloud Environment

```
Run the Exposure Response Consultant for our hybrid cloud environment.
We have AWS, Azure, and on-prem assets.
```

The agent will:
- Group initiatives by cloud provider
- Identify cloud-specific vulnerabilities
- Recommend platform-specific remediation strategies

### Example 10: DevOps Integration

```
Use the Exposure Response Consultant to identify initiatives that
should be integrated into our CI/CD pipeline vs. handled by ops
```

The agent will:
- Separate infrastructure patching from application vulns
- Suggest which initiatives benefit from automation
- Recommend shift-left opportunities

## Understanding the Output

### Initiative Priority Levels

- **P0 (Critical)** - Start immediately. Business-critical assets or actively exploited vulnerabilities. Timeline: 0-14 days.
- **P1 (High)** - Start within 2 weeks. High-risk assets or widespread issues. Timeline: 14-30 days.
- **P2 (Medium)** - Start within 1 month. Important but not urgent. Timeline: 30-60 days.
- **P3 (Standard)** - Start within 2 months. Lower risk or long-term improvements. Timeline: 60-90 days.

### Impact Score Calculation

The agent uses this formula:
```
Impact Score = (Asset Count × 0.3) + (Avg AES × 0.4) + (Business Risk × 0.3)

Example:
- Initiative: "Domain Controller Hardening"
- Assets: 5 (normalized to 5/100 = 0.05)
- Avg AES: 947 (out of 1000 = 0.947)
- Business Risk: 100 (domain controllers = highest risk)

Impact Score = (0.05 × 0.3) + (0.947 × 0.4) + (100 × 0.3)
            = 0.015 + 0.379 + 30
            = 30.394 (very high impact)
```

Higher scores = more impactful initiatives.

### Initiative Types

1. **Crown Jewel Protection** - Focus on highest-value assets (DCs, databases, Exchange)
2. **Volume Remediation** - Single vulnerability affecting many assets (browser updates)
3. **EOL Decommissioning** - Remove/upgrade unsupported software (Windows 7, Silverlight)
4. **Protocol Hardening** - Eliminate legacy protocols (SSLv2, TLS 1.0)
5. **Network Security** - Patch infrastructure devices (routers, switches, firewalls)
6. **Web Application Security** - Harden internet-facing applications
7. **Compliance Alignment** - Address regulatory gaps (PCI DSS, HIPAA)
8. **Patch Management** - OS and application updates
9. **Third-Party Risk** - Vendor software vulnerabilities
10. **Zero-Day Response** - CISA KEV or actively exploited vulnerabilities

## Troubleshooting

### Issue: "Agent not found"

**Problem:** The agent isn't installed correctly.

**Solution:**
```bash
# Verify the file exists
ls -la ~/.claude/agents/exposure-response-consultant.md

# Check the frontmatter name field
head -10 ~/.claude/agents/exposure-response-consultant.md

# If missing, reinstall
cd ~/.claude/agents
git clone https://github.com/dpickenstenable/exposure-response-consultant-agent.git
cp exposure-response-consultant-agent/agent.md exposure-response-consultant.md
```

### Issue: "No vulnerabilities found"

**Problem:** Scans haven't completed or no critical/high findings exist.

**Solution:**
- Wait for scans to finish (check Tenable UI scan status)
- Verify scan policies include authenticated checks
- Lower severity threshold: "Include medium-severity vulnerabilities"
- Check that assets are being scanned successfully

### Issue: "Authentication failed"

**Problem:** API keys are invalid or MCP server isn't running.

**Solution:**

**For MCP:**
```bash
# Test MCP server
curl http://localhost:3000/health

# Restart MCP if needed
```

**For Direct API:**
```bash
# Test API connectivity
curl -H "X-ApiKeys: accessKey=$TENABLE_ACCESS_KEY; secretKey=$TENABLE_SECRET_KEY" \
  https://cloud.tenable.com/session

# Verify environment variables
echo $TENABLE_ACCESS_KEY
echo $TENABLE_SECRET_KEY
```

### Issue: "Insufficient data to provide recommendations"

**Problem:** Not enough assets or vulnerabilities for pattern detection.

**Solution:**
- Minimum 50 assets required for meaningful analysis
- Wait 24-48 hours after initial Tenable deployment
- Ensure scans are configured to run and completing successfully
- Verify scan policies include comprehensive plugin coverage

### Issue: "Recommended initiatives don't match our environment"

**Problem:** Business risk factors may not align with your organization.

**Solution:**
```
Tell the agent:
"I think production apps should be scored higher than 85. Can you recalculate?"

Or:

"Network devices are more critical in our environment. Adjust the scoring."
```

The agent will recalculate impact scores with your adjusted weights.

### Issue: "Tag creation failed - permission denied"

**Problem:** User account lacks "Can Manage" permission on Tags.

**Solution:**
1. Contact your Tenable administrator
2. Request "Can Manage" under Tags in Access Control
3. Navigate to: Settings → Access Control → Groups → [Your Group]
4. Enable "Can Manage" for Tags
5. Retry the agent

## Security & Privacy

### Data Access

The agent only reads data from Tenable:
- Vulnerability lists
- Asset inventory
- Existing tags

It does **NOT**:
- Modify vulnerabilities
- Delete assets
- Change scan configurations
- Access credential vaults

### Tag Creation

If you approve tag creation, the agent will:
- Create new tag categories and values
- Apply tags to assets

It will **NOT**:
- Delete existing tags
- Modify existing tags
- Remove tags from assets

All tag operations are reversible.

### API Key Security

**Best practices:**
- Use environment variables, not hardcoded keys
- Generate read-only API keys when possible
- Rotate keys quarterly
- Audit API key usage in Tenable audit logs

### Report Security

Generated reports contain:
- Asset names and IPs
- Vulnerability details
- Network information

**Protect reports:**
- Store in secure locations
- Don't commit to public repositories
- Share only with authorized security team members
- Redact sensitive hostnames if sharing externally

## Tips for Best Results

### DO:

✅ **Provide business context** - "These are production database servers with customer PII"

✅ **Mention compliance drivers** - "We have a PCI audit in 60 days"

✅ **State resource constraints** - "We only have 2 security engineers"

✅ **Specify urgency** - "We need quick wins first before tackling complex migrations"

✅ **Run quarterly** - Re-analyze every 90 days as your environment evolves

✅ **Share reports with stakeholders** - Use HTML reports for executive presentations

✅ **Track progress** - Monitor AES reduction over time

✅ **Celebrate wins** - Report completed initiatives to leadership

### DON'T:

❌ **Don't run before scans complete** - Wait 24-48 hours after initial deployment

❌ **Don't skip business context** - Generic analysis produces generic recommendations

❌ **Don't create all 10 initiatives on Day 1** - Start with P0/P1, add more as capacity allows

❌ **Don't ignore test environments** - They matter for compliance too

❌ **Don't expect instant results** - Analysis takes 2-5 minutes for large environments

❌ **Don't patch blindly** - Test in dev/QA first, especially for crown jewels

❌ **Don't forget change control** - Document and approve production changes

❌ **Don't try to run the JavaScript Agent() code yourself** - Let Claude Code handle it

## Next Steps After Running

1. **Review the recommendations** - Read through all 10 initiatives
2. **Share with your team** - Discuss priorities and resource allocation
3. **Start with P0 initiatives** - Tackle highest-priority items first
4. **Create initiatives in Tenable UI** - Use tags or manual creation
5. **Assign owners** - Delegate each initiative to a team member
6. **Schedule patching windows** - Plan maintenance for disruptive patches
7. **Track progress weekly** - Monitor AES reduction and completion rates
8. **Re-run quarterly** - Adapt to changing threat landscape

## Getting Help

- **Issues:** [GitHub Issues](https://github.com/dpickenstenable/exposure-response-consultant-agent/issues)
- **Documentation:** See README.md for comprehensive details
- **Tenable Support:** [Tenable Community](https://community.tenable.com/)
- **Claude Code:** [claude.ai/code](https://claude.ai/code)

---

**Ready to start?** Open Claude Code and say:

```
Run the Exposure Response Consultant
```

The agent will handle the rest!
