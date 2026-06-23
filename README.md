# Exposure Response Consultant Agent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blue)](https://claude.ai/code)
[![Tenable](https://img.shields.io/badge/Tenable-Vulnerability%20Management-red)](https://www.tenable.com/)

> **AI-powered vulnerability strategist that analyzes Tenable scan data and recommends top 10 Exposure Response Initiatives to jumpstart your remediation program.**

## 🎯 Overview

The **Exposure Response Consultant Agent** is a strategic vulnerability management advisor that transforms overwhelming scan data into a clear, prioritized action plan. After your initial Tenable vulnerability scans complete, this agent analyzes 10,000+ assets and thousands of findings to recommend the 10 most impactful Exposure Response Initiatives—complete with business justification, affected assets, success metrics, and implementation timelines.

This agent helps security teams:
- 🎯 **Focus on what matters** - Prioritize remediation based on business risk, not just CVE severity
- ⚡ **Get started fast** - From scan completion to action plan in minutes
- 💼 **Align with business** - Every recommendation maps to business impact
- 📊 **Measure success** - Clear metrics for tracking risk reduction
- 🤖 **Automate scoping** - Tag assets for easy initiative creation in Tenable UI

### Key Features

✅ **Strategic Analysis** - Identifies patterns across crown jewels, volume issues, EOL software, legacy protocols  
✅ **Top 10 Recommendations** - Ranked by impact score (asset count × AES × business risk)  
✅ **Business Justification** - Every initiative explains "why this matters"  
✅ **Success Metrics** - Measurable targets for tracking progress  
✅ **Automated Tagging** - Creates initiative-scoping tags for easy UI filtering  
✅ **Multiple Outputs** - Console, Markdown report, HTML dashboard, CSV asset lists  
✅ **Dual Authentication** - Tenable MCP Server or Direct API  
✅ **Quarterly Cadence** - Re-run as your environment evolves

---

## 📋 Table of Contents

- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [How It Works](#-how-it-works)
- [Initiative Types](#-initiative-types)
- [Usage Examples](#-usage-examples)
- [Output Formats](#-output-formats)
- [Best Practices](#-best-practices)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚀 Installation

### Prerequisites

- **Claude Code** installed ([claude.ai/code](https://claude.ai/code))
- **Tenable VM or Tenable One** account
- **Completed vulnerability scans** (wait 24-48 hours after initial deployment)
- **API Access Keys** OR **Tenable MCP Server** configured
- **"Can View" permissions** on Vulnerabilities and Assets in Tenable

### Method 1: Install from GitHub (Recommended)

```bash
# Clone the repository
git clone https://github.com/dpickenstenable/exposure-response-consultant-agent.git

# Copy agent to Claude Code agents directory
cp exposure-response-consultant-agent/agent.md ~/.claude/agents/exposure-response-consultant.md

# Verify installation
ls -la ~/.claude/agents/exposure-response-consultant.md
```

### Method 2: Manual Installation

1. Download `agent.md` from this repository
2. Place it in your Claude Code agents directory:
   - **macOS/Linux:** `~/.claude/agents/exposure-response-consultant.md`
   - **Windows:** `%USERPROFILE%\.claude\agents\exposure-response-consultant.md`

---

## ⚡ Quick Start

### Using with Tenable MCP Server (Recommended)

```
In Claude Code:
> Run the Exposure Response Consultant
```

The agent will:
1. Analyze your vulnerability landscape (critical/high findings)
2. Identify patterns (crown jewels, volume issues, EOL software, legacy protocols)
3. Calculate impact scores for potential initiatives
4. Recommend top 10 initiatives ranked by business impact
5. Offer to create initiative-scoping tags automatically
6. Generate comprehensive reports for implementation

### Using with Direct API Authentication

```bash
export TENABLE_ACCESS_KEY="your_access_key"
export TENABLE_SECRET_KEY="your_secret_key"
export TENABLE_URL="https://cloud.tenable.com"
```

Then run:
```
> Run the Exposure Response Consultant
```

---

## 🔍 How It Works

### Phase 1: Vulnerability Landscape Analysis

The agent performs comprehensive intelligence gathering:

**Data Collection:**
- Critical vulnerabilities (severity = critical)
- High vulnerabilities (severity = high)
- Asset inventory sorted by AES/ACR (highest risk first)
- Existing tags (to leverage for scoping)
- Software inventory (to identify EOL products)

**Pattern Recognition:**
- **Crown Jewels** - Domain Controllers, Exchange, Databases (highest AES)
- **Volume Issues** - Browser/OS patches affecting 50+ assets
- **EOL Software** - Windows 7, Silverlight, Flash, unsupported OS versions
- **Legacy Protocols** - SSLv2/v3, weak TLS configurations
- **Network Infrastructure** - Cisco/Juniper/Palo Alto devices with critical vulns
- **Internet-Facing** - Web applications, VPN endpoints, public services
- **Compliance Gaps** - PCI DSS, HIPAA, SOX violations

### Phase 2: Initiative Recommendation Engine

**Impact Scoring Algorithm:**
```
Impact Score = (Asset Count × 0.3) + (Avg AES × 0.4) + (Business Risk × 0.3)

Business Risk Factors:
- Domain Controllers: 100
- Exchange/Email: 95
- Databases: 90
- Production Apps: 85
- Web Applications: 80
- Network Devices: 75
- Workstations: 60
- Test/Dev Systems: 40
```

**Initiative Prioritization:**
1. Calculate impact score for every detected pattern
2. Rank initiatives by score (highest = most impactful)
3. Select top 10 for recommendation
4. Assign priority tiers (P0, P1, P2, P3)
5. Generate business justification and success metrics

### Phase 3: Implementation Support

**Since Tenable doesn't support programmatic initiative creation via API**, the agent provides:

1. **Tag-Based Scoping** - Creates tags and applies to assets so you can filter in Tenable UI
2. **Creation Checklist** - Step-by-step instructions for each initiative
3. **Asset Lists** - CSV exports for import into tools
4. **Comprehensive Report** - Executive-ready documentation

---

## 🏷️ Initiative Types

The agent identifies 10 common initiative archetypes:

### 1. Crown Jewel Protection
**Focus:** Highest AES assets (Domain Controllers, Exchange, Databases)  
**Why:** These assets control your entire environment—compromise = total breach  
**Example:** "Domain Controller Hardening Initiative" (5 DCs with AES 947-948)

### 2. Volume Remediation
**Focus:** Single vulnerability family affecting 50+ assets  
**Why:** High efficiency—one patch campaign eliminates massive risk  
**Example:** "Microsoft Edge Fleet Update" (139 endpoints with critical browser vulns)

### 3. EOL Decommissioning
**Focus:** Unsupported software without vendor patches  
**Why:** Permanent risk—can't be patched, only removed/isolated  
**Example:** "Microsoft Silverlight Removal" (56 assets with EOL software)

### 4. Protocol Hardening
**Focus:** Legacy SSL/TLS elimination  
**Why:** Compliance requirement (PCI DSS) + exploit risk  
**Example:** "Legacy Protocol Elimination" (70 assets with SSLv2/v3)

### 5. Network Security
**Focus:** Infrastructure device patching (routers, switches, firewalls)  
**Why:** Network devices = persistent backdoor risk + lateral movement  
**Example:** "Cisco Infrastructure Overhaul" (4 devices with AES 649-778)

### 6. Web Application Security
**Focus:** Internet-facing apps with high AES  
**Why:** Direct exposure = data breach risk  
**Example:** "Production WordPress Hardening" (WordPress with AES 760)

### 7. Compliance Alignment
**Focus:** Regulatory requirement gaps (PCI DSS, HIPAA, SOX)  
**Why:** Avoid audit findings, fines, and business disruption  
**Example:** "PCI DSS Compliance Initiative" (assets in cardholder data environment)

### 8. Patch Management
**Focus:** OS/application update campaigns  
**Why:** Monthly patch cycles, Windows/Linux updates  
**Example:** "Windows Server 2019 Patch Campaign" (92 servers needing KB5063877)

### 9. Third-Party Risk
**Focus:** Vendor software vulnerabilities  
**Why:** Supply chain attacks target third-party components  
**Example:** "SQLite Memory Corruption Remediation" (63 assets with SQLite < 3.50.2)

### 10. Zero-Day Response
**Focus:** Actively exploited vulnerabilities (CISA KEV)  
**Why:** Real-world attacks happening now—patch immediately  
**Example:** "CISA KEV Emergency Response" (vulnerabilities under active exploitation)

---

## 📖 Usage Examples

### Example 1: First-Time Setup After Initial Scans

```
User: "Run the Exposure Response Consultant"

Agent:
✓ Retrieved 1,783 critical vulnerabilities
✓ Retrieved 10,875 assets
✓ Identified 5 crown jewel assets (AES 900+)
✓ Detected 139 endpoints with critical browser vulnerabilities
✓ Found 56 end-of-life software installations
✓ Identified 70 assets with legacy SSL/TLS protocols

Analysis complete! Here are your top 10 recommended initiatives:

| # | Initiative | Priority | Assets | Risk | Timeline |
|---|-----------|----------|--------|------|----------|
| 1 | Domain Controller Hardening | P0 | 5 | CRITICAL | 30 days |
| 2 | Exchange Server Remediation | P0 | 3 | CRITICAL | 14 days |
| 3 | Microsoft Edge Fleet Update | P1 | 139 | HIGH | 48 hours |
| 4 | Production Infrastructure | P1 | 5 | HIGH | 7 days |
| 5 | Legacy Protocol Elimination | P2 | 70 | MEDIUM | 30 days |
| 6 | EOL Software Decommissioning | P2 | 56 | MEDIUM | 90 days |
| 7 | Web Application Security | P2 | 7 | HIGH | 30 days |
| 8 | Cisco Network Overhaul | P3 | 4 | HIGH | 45 days |
| 9 | SQLite Remediation | P3 | 63 | MEDIUM | 45 days |
| 10 | .NET Framework Baseline | P3 | 53 | MEDIUM | 21 days |

[Detailed breakdown of each initiative with business justification, scope, metrics...]

What would you like to do?
1. Create initiative-scoping tags (recommended)
2. Export comprehensive report
3. Get creation checklist for manual setup
4. Adjust recommendations
```

**Result:** Clear action plan with prioritized initiatives ready for implementation.

---

### Example 2: Creating Initiative-Scoping Tags

```
User: "Create the tags"

Agent:
Creating initiative-scoping tags in Tenable...

✓ Created tag category: "Initiative"
✓ Created 10 tag values:
  - initiative-dc-hardening (5 assets)
  - initiative-exchange-remediation (3 assets)
  - initiative-edge-update (139 assets)
  - initiative-prod-infrastructure (5 assets)
  - initiative-legacy-protocol (70 assets)
  - initiative-eol-software (56 assets)
  - initiative-web-security (7 assets)
  - initiative-network-devices (4 assets)
  - initiative-sqlite (63 assets)
  - initiative-dotnet (53 assets)

✓ Applied tags to 405 total assets

Tags created successfully! Now to create initiatives in Tenable UI:
1. Go to Exposure → Initiatives → + New Initiative
2. Filter assets by tag category "Initiative"
3. Select specific tag value (e.g., "initiative-dc-hardening")
4. Assets automatically populate

I've also generated a comprehensive report at:
📄 Exposure-Response-Initiatives-2026-06-23.md
```

**Result:** Assets are tagged and ready for easy initiative creation in Tenable UI.

---

### Example 3: Quarterly Re-Assessment

```
User: "Run the consultant again—it's been 3 months"

Agent:
Re-analyzing your environment...

✓ Retrieved 1,245 critical vulnerabilities (↓538 from last run!)
✓ Retrieved 11,104 assets (↑229 new assets)
✓ Previous initiatives:
  - DC Hardening: COMPLETE (AES reduced 948→672)
  - Exchange Remediation: COMPLETE (AES reduced 836→584)
  - Edge Update: 95% COMPLETE (132/139 patched)

Great progress! Your average AES dropped 28% this quarter.

New recommendations based on current landscape:
1. **Kubernetes Container Security** - 45 new K8s pods detected (no existing initiative)
2. **GCP Cloud Asset Hardening** - 30 new GCP instances (no cloud provider initiative yet)
3. **Log4Shell Remediation** - 23 assets still vulnerable to Log4j RCE
...

Would you like to create initiatives for these new patterns?
```

**Result:** Adaptive recommendations that evolve with your infrastructure.

---

## 🎨 Output Formats

The agent supports multiple output formats:

### 1. Interactive Console
Real-time analysis presented in the conversation with approval workflow.

### 2. Markdown Report
Comprehensive documentation suitable for sharing with teams:
```markdown
# Exposure Response Consultant - Initiative Recommendations
**Date:** 2026-06-23
**Assets Analyzed:** 10,875
**Critical Vulnerabilities:** 1,783

## Executive Summary
[Business-level summary of risk posture and recommendations]

## Top 10 Initiatives
[Detailed breakdown with scope, metrics, timelines]

## Implementation Roadmap
[Phased rollout plan: Week 1-2, Week 3-4, Month 2, Month 3]

## Asset Lists by Initiative
[CSV-formatted asset lists for each initiative]
```

### 3. HTML Dashboard
Executive-friendly visual report with charts and interactive elements:
- Risk trend charts
- Initiative priority matrix
- Asset exposure heatmap
- Progress tracking dashboard

### 4. CSV Asset Lists
Asset exports for each initiative, importable into patch management tools:
```csv
Initiative,Asset Name,Asset ID,AES,ACR,Primary Vulnerability
"Domain Controller Hardening",win-vuln-dc,17650dcf-...,948,9,"Windows Server 2019 KB5063877"
```

### 5. JSON Export
Structured data for integration with SIEM, ticketing, or automation platforms:
```json
{
  "initiatives": [
    {
      "name": "Domain Controller Hardening",
      "priority": "P0",
      "assets": 5,
      "avg_aes": 947,
      "timeline": "30 days",
      "affected_assets": [...],
      "vulnerabilities": [...]
    }
  ]
}
```

---

## 🎯 Best Practices

### When to Run

✅ **After Initial Scans** - Wait 24-48 hours after Tenable deployment for full scan coverage  
✅ **Quarterly Cadence** - Re-run every 90 days to adapt to changing landscape  
✅ **After Major Changes** - New acquisitions, cloud migrations, infrastructure overhauls  
✅ **Post-Incident** - After security incidents to identify remaining gaps

### Implementation Tips

**Start Small:**
- Focus on P0 initiatives first (crown jewels)
- Get quick wins with low-effort/high-impact (e.g., Edge updates)
- Build momentum before tackling complex EOL decommissioning

**Executive Communication:**
- Use HTML report for leadership presentations
- Emphasize business impact, not just technical details
- Show risk reduction metrics (AES before/after)

**Track Progress:**
- Weekly initiative review meetings
- Monitor AES reduction over time
- Celebrate completed initiatives with team

**Tag Hygiene:**
- Remove initiative tags as assets are remediated
- Archive completed initiative tags (don't delete—useful for historical tracking)
- Create new tags as new initiatives emerge

### Common Pitfalls to Avoid

❌ **Don't create all 10 initiatives on Day 1** - Start with P0/P1, add P2/P3 as capacity allows  
❌ **Don't ignore business context** - A low-AES production asset may need higher priority than high-AES test system  
❌ **Don't patch blindly** - Test in dev/QA first, especially for crown jewels  
❌ **Don't forget change control** - Document and approve production changes properly  
❌ **Don't set unrealistic timelines** - 30-day timeline for 1,000 assets is unlikely to succeed

---

## 🐛 Troubleshooting

### Issue: "No vulnerabilities found"

**Cause:** Scans haven't completed or no critical/high findings

**Solution:**
- Wait for scans to complete (check scan status in Tenable)
- Lower severity threshold to include medium vulnerabilities
- Verify scan policies include authenticated checks

### Issue: "Insufficient data to provide recommendations"

**Cause:** Not enough assets or vulnerabilities for pattern detection

**Solution:**
- Minimum 50 assets required for meaningful analysis
- Wait 24-48 hours after initial deployment
- Ensure scans are running and completing successfully

### Issue: "Authentication failed"

**Cause:** Invalid API keys or MCP server not running

**Solution:**
```bash
# Test MCP Server
curl http://localhost:3000/health

# Test Direct API
curl -H "X-ApiKeys: accessKey=$TENABLE_ACCESS_KEY; secretKey=$TENABLE_SECRET_KEY" \
  https://cloud.tenable.com/session
```

### Issue: "Tag creation failed - permission denied"

**Cause:** User account lacks "Can Manage" permission on Tags

**Solution:**
1. Contact Tenable administrator
2. Request "Can Manage" under Tags in Access Control
3. Retry after permissions are updated

### Issue: "Initiative scoring seems incorrect"

**Cause:** Business risk factors may not match your environment

**Solution:**
- Adjust business risk factors in the agent (edit agent.md)
- Provide feedback: "I think production apps should be scored higher than 85"
- Agent will recalculate with adjusted weights

---

## 📊 Success Metrics

Track these KPIs to measure consultant effectiveness:

**Risk Reduction:**
- Average AES: Target 20-30% reduction per quarter
- Critical Vulnerabilities: Target 50%+ reduction in 90 days
- Crown Jewel Protection: Target zero critical vulns on top 10 assets

**Operational Efficiency:**
- Time to First Initiative: Target <24 hours after scan completion
- Initiative Completion Rate: Target 80%+ within recommended timeline
- Patching SLA Compliance: Target 95%+ for P0/P1 initiatives

**Business Alignment:**
- Executive Engagement: Present quarterly reports to leadership
- Budget Justification: Use risk metrics to secure remediation resources
- Audit Readiness: Demonstrate continuous improvement for compliance

---

## 🤝 Contributing

Contributions welcome! Areas for enhancement:

- **CISA KEV Integration** - Auto-detect actively exploited vulnerabilities
- **Attack Path Analysis** - Integrate Tenable Attack Path data for prioritization
- **Exposure Card Generation** - Auto-create Exposure Cards for tracking
- **SIEM Integration** - Export to Splunk, Sentinel, QRadar formats
- **Compliance Mapping** - Enhanced PCI DSS, HIPAA, SOX, FedRAMP support

### Reporting Issues

- Include asset count and vulnerability count
- Attach sanitized output (remove sensitive hostnames/IPs)
- Describe expected vs. actual recommendations

### Submitting Pull Requests

1. Fork the repository
2. Create feature branch (`git checkout -b feature/enhancement`)
3. Test with real Tenable environments
4. Commit with clear messages
5. Push and open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Claude Code** by Anthropic - AI-powered development environment
- **Tenable** - Vulnerability Management and Exposure Management platform
- **Tenable MCP Server** - Model Context Protocol integration for Tenable API

---

## 📞 Support

- **Issues:** [GitHub Issues](https://github.com/dpickenstenable/exposure-response-consultant-agent/issues)
- **Tenable Support:** [Tenable Community](https://community.tenable.com/)
- **Claude Code:** [claude.ai/code](https://claude.ai/code)

---

## 🗺️ Roadmap

- [ ] CISA KEV auto-detection and emergency initiative creation
- [ ] Attack Path Analysis integration for multi-hop risk assessment
- [ ] Automated Exposure Card configuration generation
- [ ] Slack/Email notifications for new high-priority initiatives
- [ ] Integration with ITSM tools (ServiceNow, Jira) for ticket creation
- [ ] Historical trending dashboard (track AES reduction over 6+ months)
- [ ] Custom initiative templates (user-defined scoring algorithms)

---

## 🔗 Related Projects

- [Tenable MCP Server](https://github.com/tenable/mcp-server-tenable) - Model Context Protocol server for Tenable API
- [Tenable Audit Log Review Agent](https://github.com/dpickenstenable/tenable-audit-log-review-agent) - Daily audit log analysis
- [Tenable Tag Optimizer Agent](https://github.com/dpickenstenable/tenable-tag-optimizer-agent) - Intelligent tag taxonomy creation

---

**Made with ❤️ for the Tenable community**

Transform vulnerability data into strategic action. If this agent helps your remediation program, please ⭐ star the repository!
