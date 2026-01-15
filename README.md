# 🐍 s3rp (Serpent) | Red Team Tactical Manual

**Author:** oxbv1 | 0xb0rn3  
**AI Collaboration:** This toolkit was developed in cooperation with Google Gemini. The AI assisted with code refinement, syntax optimization, and structural organization, but the tactical methodology and red team approach are rooted in real-world penetration testing experience.

---

## What You're Looking At

This isn't just a collection of bash scripts. What you're seeing is my evolution as a developer and penetration tester, captured in code. From scan01 to scan09, you're watching me learn in real-time—from basic reconnaissance to full-scale automated exploitation frameworks.

I want to be transparent: I built this with Google Gemini's help. The AI cleaned up syntax, optimized logic, and structured the code. But it didn't decide tactical approaches, evasion techniques, or which flags matter in the field. That came from real experience dodging IDS systems and understanding how blue teams think.

---

## Repository Structure

```
s3rp/
├── scan01          # Foundation - Basic nmap wrapper with menus
├── scan02          # Evolution - Aggressive presentation, tactical configs
├── scan03          # Enhancement - Dependency management, root checks
├── scan04          # Evasion - Searchsploit integration, fragmentation
├── scan05          # Anonymity - ProxyChains integration, MSF resources
├── scan06          # Automation - Exploit mapping, resource generation
├── scan07          # Integration - Web enumeration with Gobuster
├── scan08          # Refinement - Polished workflows, better parsing
├── scan09          # Apex - Complete integration, listener modules
├── C2              # Persistence - Shell catching and session management
├── sampleframework.sh  # UNIFIED FRAMEWORK - All features combined
└── README.md       # This file
```

---

## Feature Matrix: What Each Script Does

| Feature | scan01 | scan02 | scan03 | scan04 | scan05 | scan06 | scan07 | scan08 | scan09 | Unified |
|---------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|
| Basic Scanning | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| NSE Integration | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Multiple Output Formats | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Dependency Checks | - | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Auto-install Tools | - | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Evasion Techniques | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Packet Fragmentation | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Decoy IPs | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Searchsploit Integration | - | - | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ProxyChains Support | - | - | - | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metasploit RC Generation | - | - | - | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Web Enumeration (Gobuster) | - | - | - | - | - | - | ✓ | ✓ | ✓ | ✓ |
| Auto Web Discovery | - | - | - | - | - | - | ✓ | ✓ | ✓ | ✓ |
| HTML Report Generation | - | - | - | - | - | ✓ | ✓ | ✓ | ✓ | ✓ |
| Vulnerability Assessment | - | - | - | - | - | - | - | - | - | ✓ |
| Session Management | - | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Comprehensive Reporting | - | - | - | - | - | - | - | - | ✓ | ✓ |
| Modular Architecture | - | - | - | - | - | - | - | - | - | ✓ |

---

## The Learning Path

### Phase One: Building the Foundation (scan01-03)

**What you're learning:** The basics of wrapping nmap in a user-friendly interface.

**scan01** is your starting point. It's a menu-driven wrapper that eliminates the need to memorize nmap flags. Look at the `grep -v "Starting Nmap"` filter—that's not aesthetic, it's practical. When you're managing multiple scans, noise becomes a serious problem.

**scan02** introduced tactical configurations with aggressive visual presentation. The color scheme changes aren't just for looks—when you're running multiple terminals during an engagement, visual differentiation is operational necessity.

**scan03** added dependency management and auto-installation. In the field, discovering you're missing a tool mid-scan is unacceptable. The script handles it or fails gracefully with clear instructions.

**Key modifications to try:**
- Change grep filters to match your noise tolerance
- Modify color schemes for your terminal setup
- Adjust the dependency list for your toolkit
- Customize output directory structures

### Phase Two: Learning to Be Invisible (scan04-06)

**What you're learning:** Evasion techniques and operational security.

**scan04** introduced packet fragmentation (`-f`), MTU manipulation (`--mtu 8`), source port spoofing (`-g 53`), and decoy IPs (`-D RND:10`). Each flag serves a specific evasion purpose:

- **Fragmentation (`-f`)**: Breaks packets into pieces that many IDS systems can't reassemble
- **MTU manipulation (`--mtu 8`)**: Sets extremely small packet sizes for deeper evasion
- **Source port 53 (`-g 53`)**: Mimics DNS traffic to bypass firewall rules
- **Decoys (`-D RND:10`)**: Creates phantom scanners to hide your real IP

**scan05** integrated ProxyChains for IP anonymization and added Metasploit resource file generation—automating hours of manual MSF configuration.

**scan06** refined the exploit automation with better Searchsploit integration and intelligent parsing.

**Key modifications to try:**
- Adjust decoy count (try `-D RND:3` vs `-D RND:20`)
- Experiment with MTU values (8, 16, 24)
- Test different source ports (53 for DNS, 80 for HTTP)
- Configure ProxyChains with different proxy chains

### Phase Three: Automation and Integration (scan07-09)

**What you're learning:** Chaining tools into complete workflows.

**scan07** automated web enumeration. When ports 80, 443, or 8080 are detected, Gobuster launches automatically. No manual intervention required.

**scan08** polished the integration with better error handling and cleaner output parsing.

**scan09** represents the apex—complete integration of all previous features plus refined reporting and session management.

**Key modifications to try:**
- Swap Gobuster wordlists (`/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`)
- Adjust thread counts (`-t 50` to `-t 100` or `-t 25`)
- Add additional web ports to scan (8000, 8888, 9090)
- Customize the MSF resource file templates

---

## The Unified Framework: `sampleframework.sh`

This is everything from scan01-09 combined into a single, modular, production-ready framework. It includes features that weren't in the individual scripts:

### New Features in the Unified Framework

1. **Comprehensive Vulnerability Assessment**
   - Automatic detection of SMB signing issues
   - Weak SSL/TLS protocol identification  
   - Default credential checks
   - Database exposure detection
   - RDP and Telnet warnings

2. **Advanced Session Management**
   - Organized directory structures
   - Session metadata tracking
   - Automatic archiving options
   - Resume capability (partial)

3. **Intelligent Results Parsing**
   - Color-coded port importance (red for critical services)
   - Service version extraction
   - Clean, actionable output format
   - Automated report generation

4. **Enhanced Error Handling**
   - Graceful degradation when tools are missing
   - Interrupt handling with cleanup
   - Proxy verification before use
   - File existence checks

5. **Modular Architecture**
   - Each function is self-contained
   - Easy to copy individual functions
   - Clear section headers for navigation
   - Extensive inline documentation

---

## Building Your Own Toolkit: The Skeleton Approach

Instead of giving you another full script, here's how to think about building your own:

### The Function Library Approach

```bash
#!/bin/bash
# My Custom Security Framework
# Built by [Your Name] using s3rp as reference

# ====================================
# CONFIGURATION SECTION
# ====================================
# Copy this from the unified framework and modify:
# - Color schemes
# - Default tool paths
# - Your preferred flags
# - Custom wordlist locations

RED='\033[1;31m'
GRN='\033[1;32m'
NC='\033[0m'

MY_DEFAULT_WORDLIST="/path/to/my/favorite/wordlist.txt"
MY_DEFAULT_TIMING="-T4"

# ====================================
# FUNCTION LIBRARY
# ====================================
# Copy functions you need from s3rp and customize them

# From scan01: Basic scanning
scan_target() {
    # Your custom implementation
    echo "Scanning $1 with my preferred settings..."
}

# From scan04: Evasion techniques  
stealth_scan() {
    # Copy the evasion logic but adjust to your needs
    local target=$1
    nmap -sS -f -g 53 -D RND:5 "$target"
}

# From scan07: Web enumeration
enumerate_web() {
    # Use your preferred web scanner
    # Maybe you prefer ffuf over gobuster?
    local url=$1
    ffuf -u "$url/FUZZ" -w "$MY_DEFAULT_WORDLIST"
}

# ====================================
# YOUR CUSTOM WORKFLOW
# ====================================
# This is where you combine functions YOUR way

my_workflow() {
    local target=$1
    
    # Your unique approach
    echo "Phase 1: Quick recon"
    scan_target "$target"
    
    echo "Phase 2: Web attack"
    enumerate_web "http://$target"
    
    echo "Phase 3: Your custom step"
    # Add whatever makes sense for YOUR engagements
}

# Run it
my_workflow "$1"
```

### What to Customize

1. **Tool Selection**
   - Replace Gobuster with ffuf, dirsearch, or feroxbuster
   - Use masscan instead of nmap for speed
   - Swap searchsploit for CVE API lookups

2. **Workflow Order**
   - Maybe you always start with masscan for speed, then detailed nmap
   - Perhaps you enumerate web first, scan second
   - Your engagement methodology should drive the flow

3. **Output Format**
   - Some people want JSON for parsing
   - Others want markdown for reporting
   - You might want database integration

4. **Notification Systems**
   - Add Slack notifications when interesting ports are found
   - Email reports automatically
   - Discord webhooks for team coordination

---

## Missing Features & Future Enhancements

These features aren't in the current scripts but would be valuable additions:

### Not Yet Implemented

1. **Advanced Reporting**
   - PDF generation with graphics
   - Executive summary auto-generation
   - Risk scoring matrix
   - Compliance mapping (PCI-DSS, HIPAA)

2. **Database Integration**
   - PostgreSQL backend for tracking multiple engagements
   - Historical comparison ("this network last month vs now")
   - Asset management integration

3. **API Integration**
   - Shodan API for additional intelligence
   - VirusTotal for hash checking
   - CVE database automatic lookups
   - MITRE ATT&CK mapping

4. **Cloud Platform Support**
   - AWS security group enumeration
   - Azure AD reconnaissance
   - GCP project discovery
   - Kubernetes cluster scanning

5. **Advanced Evasion**
   - Timing randomization
   - Traffic shaping to match legitimate patterns
   - Protocol-specific evasion (SMB, RDP, etc.)
   - Automated IDS detection and adaptation

6. **Team Collaboration**
   - Shared session state
   - Real-time collaboration features
   - Role-based access control
   - Audit logging

7. **Post-Exploitation Integration**
   - Automatic credential harvesting from results
   - Password spraying based on discovered users
   - Lateral movement path mapping
   - Privilege escalation suggestion engine

8. **Machine Learning**
   - Port prediction based on initial scan
   - Anomaly detection in responses
   - Optimal scan timing learning
   - False positive reduction

### How to Add These Features

If you want to implement any of these, here's the approach:

```bash
# Example: Adding Shodan API integration

search_shodan() {
    local target=$1
    local api_key="YOUR_SHODAN_API_KEY"
    
    echo "[*] Querying Shodan for: $target"
    
    # Use curl to hit Shodan API
    local response=$(curl -s "https://api.shodan.io/shodan/host/${target}?key=${api_key}")
    
    # Parse JSON (requires jq)
    echo "$response" | jq -r '.data[] | "\(.port): \(.product) \(.version)"'
}

# Integrate into workflow
configure_target() {
    # ... existing code ...
    
    # Add Shodan check
    if [ -n "$SHODAN_API_KEY" ]; then
        search_shodan "$TARGET"
    fi
}
```

---

## Quick Reference: Which Script for Which Job

**Learning nmap basics?** → Start with `scan01`

**Need stealth/evasion?** → Use `scan04` or `scan06`

**Want full automation?** → Use `scan09` or the unified framework

**Building your own tool?** → Use the unified framework as a function library

**Quick recon on limited time?** → Use `scan03` with profile #4 (Quick Survey)

**Full infrastructure audit?** → Use `scan09` or unified framework with "Total War" profile

**Just need web enumeration?** → Use `scan07` or `scan08`

**Setting up for exploitation?** → Use `scan09` to auto-generate MSF resources

**Need persistent shells?** → Use the `C2` script for listener management

---

## Practical Advice for Beginners

### Start Here

1. **Run scan01 against a practice target**
   - Set up Metasploitable2 or DVWA
   - Run scan01 and examine every output file
   - Read through the script, look up every command you don't know

2. **Make one small change**
   - Change the banner
   - Add a new color variable
   - Modify one grep filter
   - Test it and see what breaks

3. **Progress to scan04**
   - Run it in "Ghost Mode"
   - Compare the speed to scan01
   - Look at the flags and understand why each one is there

4. **Build your own skeleton**
   - Copy the structure from the unified framework
   - Replace the banner with your own
   - Add one custom function
   - Make it yours

### Learning Exercises

**Exercise 1: Modify the Evasion Profile**
- Open scan04
- Find the "Ghost Recon" profile
- Change `-D RND:10` to `-D RND:3`
- Run both versions and compare timing
- Learn: More decoys = slower scan = more stealth

**Exercise 2: Custom NSE Script Combination**
- Open scan01
- Add a new NSE profile option
- Combine your favorite scripts
- Test against a target
- Learn: How NSE scripts provide intelligence

**Exercise 3: Build a Notification System**
- Take the unified framework
- Add a function that runs when port 22 is found
- Send yourself an email or Slack message
- Learn: Event-driven automation

**Exercise 4: Create a Client-Specific Profile**
- Copy scan09
- Create a profile for a specific client type (e.g., "WordPress Sites")
- Add WordPress-specific NSE scripts
- Use a WordPress-focused wordlist for Gobuster
- Learn: Customization for specific targets

---

## Philosophy: Why Customize?

The best security tools aren't the ones with the most features—they're the ones that match YOUR workflow and thinking style.

When I started, I copied commands from tutorials verbatim. I was slow and didn't understand what I was doing. The breakthrough came when I started modifying tools to fit how MY brain works.

Some people like verbose output. I prefer minimal, actionable data. Some like manual control. I prefer automation with decision points. Neither is wrong—they're different.

That's why I'm giving you these scripts with the expectation that you'll CHANGE them. I don't want you running scan09 forever. I want you to:

1. Understand how it works
2. Identify what doesn't fit your style  
3. Modify it
4. Break it
5. Fix it
6. Learn from the process

Every time you change something, you have to understand what that code does. You'll break things. You'll fix them. You'll discover edge cases. **That's learning.**

---

## Real-World Usage Examples

### Scenario 1: External Penetration Test

```bash
# Day 1: Initial reconnaissance
./scan09  # Use "Ghost Mode" to avoid detection
# Let it run overnight

# Day 2: Web enumeration
./scan07  # Focuses on web services discovered
# Review results, identify attack surface

# Day 3: Exploitation
msfconsole -r s3rp_OP_*/metasploit_resources/auto_setup.rc
# Use the auto-generated resource file
```

### Scenario 2: Internal Network Assessment

```bash
# Speed is OK, no need for stealth
./scan09  # Use "Quick Survey" mode
# Scan entire /24 network quickly

# Identify critical systems
# Use the HTML report to prioritize

# Deep dive on interesting hosts
./scan09  # Use "Vulnerability Hunt" on specific IPs
```

### Scenario 3: Bug Bounty Hunting

```bash
# Target: example.com and subdomains
./scan07  # Web-only enumeration
# Use custom wordlist for tech stack

# If API endpoints found:
# Modify scan07 to use API-specific wordlists

# When interesting findings:
# Use scan04 Searchsploit integration to find exploits
```

### Scenario 4: Red Team Engagement

```bash
# Need maximum stealth over weeks
./scan04  # "Ghost Recon" with proxychains
# Spread scans over days

# Document everything
# Use unified framework's reporting

# Generate MSF resources for team
# Share the .rc file with team members
```

---

## Common Pitfalls & Solutions

### Pitfall 1: Running Too Fast
**Problem:** `-T5` timing triggers IDS  
**Solution:** Use `-T2` or `-T3` for production networks  
**Learn:** Speed vs stealth is always a trade-off

### Pitfall 2: Too Many Decoys
**Problem:** `-D RND:50` looks suspicious  
**Solution:** Use 3-10 decoys maximum  
**Learn:** Realistic traffic patterns matter

### Pitfall 3: Wrong Wordlist
**Problem:** Using `common.txt` on a massive site  
**Solution:** Choose wordlist based on time budget  
**Learn:** `common.txt` = quick, `directory-list-2.3-medium.txt` = thorough

### Pitfall 4: Ignoring Failed Proxies
**Problem:** ProxyChains config broken, but script runs anyway  
**Solution:** The unified framework checks proxy health  
**Learn:** Always verify your anonymity layer

### Pitfall 5: Not Saving Session Data
**Problem:** Lost terminal, lost all results  
**Solution:** All scripts save to organized directories  
**Learn:** Session management is critical

---

## Contribution & Modification Guidelines

If you build something cool with this as a base:

1. **Keep the attribution**
   - Mention this was inspired by s3rp
   - Credit the AI collaboration if you use that approach
   - Link back to this repo

2. **Share your improvements**
   - Did you add a cool feature? Open a PR
   - Found a bug? Open an issue
   - Built something entirely new? Share it!

3. **Maintain the teaching spirit**
   - If you release your version, explain WHY you made changes
   - Document your thinking process
   - Help the next person learn

4. **Stay ethical**
   - Only use on authorized targets
   - Don't weaponize for malicious purposes
   - Respect the security community

---

## Final Thoughts

This toolkit represents hundreds of hours of learning, experimentation, and real-world application. I'm sharing it not because it's perfect—it's not—but because I wish someone had shared something like this with me when I was starting.

The security field is intimidating when you're new. Everyone seems to know things you don't. Everyone has custom tools that seem like magic. But here's the secret: **we all started from zero.** We all copied and modified other people's work until we understood it well enough to create our own.

This is my contribution to that cycle of learning and sharing.

Take this code, break it, fix it, improve it, and make it yours. And then, when you've learned something valuable, share it with the next person coming up behind you.

That's how we all get better.

**Stay curious. Stay ethical. Happy hacking.**

— oxbv1 | 0xb0rn3

---

## Legal Disclaimer

This toolkit is provided for **educational purposes** and **authorized security testing only**. 

⚠️ **Unauthorized access to computer systems is illegal.** 

Always ensure you have **explicit written permission** before conducting any security assessments. Unauthorized use of these tools can result in:
- Criminal prosecution
- Civil liability  
- Professional consequences
- Harm to your reputation

**The author assumes no liability for misuse of these tools.** You are solely responsible for your actions.

If you're unsure whether you have authorization, **don't do it.**

---

## Acknowledgments

- **Google Gemini** for AI-assisted development
- The **nmap team** for creating the world's best port scanner
- The **Metasploit team** for the exploitation framework
- The **Kali Linux team** for providing the foundation
- **offensive-security.com** for the education
- The **infosec community** for constant learning and sharing

---

**Repository:** github.com/0xb0rn3/s3rp  
**Contact:** [Your contact method]  
**License:** [Your chosen license]

*Built with curiosity, refined with experience, shared with purpose.*
