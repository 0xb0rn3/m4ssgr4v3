# 🐍 s3rp (Serpent) | Red Team Tactical Manual

**Author:** oxbv1 | 0xb0rn3  
**AI Collaboration:** This toolkit was developed in cooperation with Google Gemini. The AI assisted with code refinement, syntax optimization, and structural organization, but the tactical methodology and red team approach are rooted in real-world penetration testing experience.

---

## What You're Looking At

This isn't just a collection of bash scripts sitting in a GitHub repo. What you're seeing here is my actual evolution as both a developer and a penetration tester, captured in code form. When you look through scan01 all the way to scan09, you're literally watching me learn in real-time—from basic reconnaissance to full-scale automated exploitation frameworks.

I want to be upfront with you: I built this toolkit with the help of Google Gemini. The AI helped me clean up my syntax, optimize the logic flow, and structure everything properly. But here's what the AI didn't do—it didn't decide how to approach a target, which evasion techniques to use, or why certain flags matter in the real world. That tactical knowledge comes from actual experience in the field, from understanding how blue teams think, and from countless hours of trying to not get caught by intrusion detection systems.

---
a
## Why I'm Sharing This

Most people who release security tools either give you a polished final product with no context, or they dump some code on GitHub with a one-line README that assumes you already know everything. I wanted to do something different. I wanted to show you the messy middle part—the learning process itself.

If you're just getting into security, you need to understand that nobody starts out writing perfect reconnaissance frameworks. You start with a single nmap command that you keep forgetting the syntax for. Then you write a script so you don't have to remember it. Then you realize you want to filter the output differently. Then you discover NSE scripts. Then you learn about evasion techniques. Before you know it, you've got nine different versions of the same tool, each one teaching you something new.

That's exactly what these scripts represent.

---

## The Learning Path: Understanding Each Phase

Let me walk you through how these scripts evolved, because understanding the progression matters more than just running the final version.

### Phase One: Building the Foundation (scan01 through scan03)

**What you're learning here:** The basics of wrapping nmap in a user-friendly interface.

When you look at scan01, you'll notice it's pretty straightforward. It gives you a menu, asks what you want to scan, and executes nmap with some preset configurations. The real magic here isn't in what it does—it's in understanding why certain design decisions were made.

Look at the section where I filter out the nmap banner with `grep -v "Starting Nmap"`. That's not just about making the output prettier. When you're on a real engagement and you're juggling output from multiple scans, that "noise" becomes a serious problem. You need to see the actual data, not nmap telling you it's starting. This is the kind of thing you only learn from experience—from that moment when you're scrolling through thousands of lines trying to find which ports are open and you realize half of what you're reading is completely useless.

By scan02, I started getting more aggressive with the presentation. Notice how the banner changes, how the color scheme gets more intense. That wasn't just aesthetic—when you're running multiple terminal windows during an engagement, visual differentiation matters. You need to know at a glance which tool you're looking at.

Scan03 introduces dependency checking and automatic installation. Here's why that matters: if you're on a client site and you realize you're missing xsltproc halfway through a scan, you can't just stop and spend twenty minutes figuring out how to install it. The script needs to handle that for you, or at least fail gracefully and tell you exactly what's missing.

**What to modify when you build your own:** Start with the grep filters. Every pentester has different opinions on what constitutes "noise" in nmap output. Maybe you want to keep the "Starting Nmap" banner because you like seeing confirmation that the scan launched. Maybe you want to filter out closed ports differently. Change those grep commands to match your workflow. That's how you make it yours.

### Phase Two: Learning to Be Invisible (scan04 through scan06)

**What you're learning here:** Evasion techniques and operational security.

This is where things get serious. Up until now, we've been focused on functionality—making the tool work. But in the real world, making it work isn't enough. You need to not get detected while you're doing it.

Look at the flags in scan04's "Ghost Recon" mode: `-f --mtu 8 -g 53 -D RND:10`. Let me break down why each of these matters.

The `-f` flag fragments your packets. Most intrusion detection systems are configured to detect standard nmap signatures by looking at packet structure. When you fragment packets, you're essentially breaking them into smaller pieces that get reassembled by the target. Many IDS systems don't reassemble packets before analyzing them, so they miss what you're doing entirely.

The `--mtu 8` takes fragmentation even further by setting the maximum transmission unit to 8 bytes. This is extremely small, which makes reassembly harder and evasion more effective. But here's the catch—it also makes your scan slower. This is the eternal trade-off in red team work: stealth versus speed.

The `-g 53` flag sets your source port to 53, which is the DNS port. Why does this matter? Because most firewalls have rules that allow DNS traffic through without much scrutiny. By making your scan packets look like they're coming from DNS, you increase your chances of slipping past firewall rules.

The `-D RND:10` creates ten random decoy IP addresses that appear to be scanning alongside you. From the target's perspective, they see eleven different IP addresses hitting them simultaneously. Which one is real? They don't know. This is how you hide in the crowd.

By scan06, I introduced ProxyChains integration. This is critical for real-world work. ProxyChains routes all your traffic through a chain of proxy servers, which means the target never sees your actual IP address. But notice the script checks if ProxyChains is available and gracefully handles the case where it isn't. You can't assume every system you work from will have every tool installed.

**What to modify when you build your own:** The number of decoys in the `-D` flag is a great starting point. The value `RND:10` means ten random decoys, but that might be too many for some targets. If the target's IDS is sophisticated, having too many decoys can actually flag you as suspicious because that's not normal traffic behavior. Try different values. Start with three or four decoys and work your way up. Learn what works for different environments.

Also, look at the MTU value. I use 8 in the most aggressive stealth mode, but you can experiment with 16 or 24. The larger the value, the faster your scan but the less effective the evasion. Finding the right balance for your specific target is an art, not a science.

### Phase Three: Automation and Integration (scan07 through scan09)

**What you're learning here:** How to chain multiple tools together into a complete workflow.

This is where we stop thinking about individual tools and start thinking about entire attack workflows. In the real world, you never just run nmap and call it a day. You run nmap to discover services, then you feed those results into vulnerability scanners, then you search for exploits, then you configure your exploitation framework. Each of these steps can be automated.

Look at scan07's integration with Gobuster. The script automatically detects when ports 80, 443, or 8080 are open, then launches Gobuster against those web servers to enumerate directories. You're not manually checking the nmap output and then running a separate tool—it happens automatically. This is how you save time during engagements.

By scan08, we're generating Metasploit resource files. Let me explain why this is powerful. Every time you launch Metasploit, you have to set up your workspace, import your scan data, configure your modules, and set your options. If you're doing this manually every time, you're wasting hours. But a resource file (the .rc file) is just a script that Metasploit can execute automatically. You run `msfconsole -r yourfile.rc` and everything gets set up for you instantly.

Look at how scan09 generates these resource files. It takes the nmap XML output, feeds it through Searchsploit to find relevant exploits, then generates a Metasploit resource file that's pre-configured with the right modules for the vulnerabilities it found. You go from raw scan data to exploitation framework configuration in seconds.

**What to modify when you build your own:** The Gobuster wordlist is probably the most obvious place to start. I use `/usr/share/wordlists/dirb/common.txt` because it's available on most Kali installations, but it's also pretty basic. If you're targeting a specific type of web application—say you know it's a WordPress site—you'd want a WordPress-specific wordlist. If you're going after an IIS server, you'd want a different wordlist entirely.

The thread count in Gobuster (`-t 50`) is another variable worth adjusting. Fifty threads is fairly aggressive. Against some servers, that might trigger rate limiting or even crash the application. Against others, you could push it to 100 threads or more. Understanding your target's infrastructure matters here.

---

## Building Your Own Toolkit: A Practical Framework

Here's the thing about security tools—you should never just use someone else's toolkit without understanding it and modifying it for your needs. Every engagement is different. Every target environment has different defenses. A tool that works perfectly in one scenario might be completely wrong for another.

So I want to give you a skeleton structure that you can use as a starting point for building your own custom framework. This isn't meant to be comprehensive—it's meant to be a foundation that you can expand based on what you learn.

```bash
#!/bin/bash
# Personal Red Team Toolkit - Skeleton Version
# Author: [Your Name Here]
# This framework was inspired by s3rp by oxbv1 | 0xb0rn3

# ============================================
# SECTION ONE: DEFINE YOUR ENVIRONMENT
# ============================================
# This is where you set up colors, paths, and global variables
# that will be used throughout your script.

RED='\033[1;31m'
GREEN='\033[1;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;36m'
NC='\033[0m'  # No Color - always reset at the end

# Set your working directory structure
# Using a timestamp ensures you never overwrite previous operation data
OPERATION_DIR="engagement_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$OPERATION_DIR"

# ============================================
# SECTION TWO: DEPENDENCY MANAGEMENT
# ============================================
# Always check that your required tools are installed
# This prevents failures halfway through an engagement

check_requirements() {
    local tools=("nmap" "gobuster" "searchsploit")
    local missing_tools=()
    
    for tool in "${tools[@]}"; do
        if ! command -v "$tool" &> /dev/null; then
            missing_tools+=("$tool")
        fi
    done
    
    if [ ${#missing_tools[@]} -ne 0 ]; then
        echo -e "${RED}[!] Missing required tools: ${missing_tools[*]}${NC}"
        echo -e "${YELLOW}[?] Would you like to attempt automatic installation? (y/n)${NC}"
        read -r response
        if [[ "$response" == "y" ]]; then
            # Add your installation logic here based on your OS
            echo "Installation logic goes here"
        else
            echo -e "${RED}[!] Cannot proceed without required tools${NC}"
            exit 1
        fi
    fi
}

# ============================================
# SECTION THREE: TARGET CONFIGURATION
# ============================================
# This is where you gather information about what you're attacking

configure_target() {
    echo -e "${YELLOW}[+] Define your target:${NC}"
    read -p "Enter target IP, CIDR, or hostname: " TARGET
    
    # Validate that something was actually entered
    if [ -z "$TARGET" ]; then
        echo -e "${RED}[!] Target cannot be empty${NC}"
        configure_target  # Recursively call until we get valid input
    fi
    
    echo -e "${GREEN}[+] Target set to: $TARGET${NC}"
}

# ============================================
# SECTION FOUR: OPERATIONAL LOGIC
# ============================================
# This is the heart of your framework - where the actual work happens

execute_reconnaissance() {
    echo -e "${BLUE}[*] Beginning reconnaissance phase...${NC}"
    
    # Phase 1: Network scanning
    echo -e "${BLUE}[*] Running network scan...${NC}"
    nmap -sS -sV -O "$TARGET" -oA "$OPERATION_DIR/initial_scan" --stats-every 30s
    
    # Phase 2: Check for web services and enumerate them
    echo -e "${BLUE}[*] Checking for web services...${NC}"
    
    # This is where you'd parse the nmap output and launch
    # additional tools based on what you found
    # Example: if port 80 is open, launch gobuster
    
    # Phase 3: Search for known vulnerabilities
    echo -e "${BLUE}[*] Searching for exploits...${NC}"
    searchsploit --nmap "$OPERATION_DIR/initial_scan.xml" > "$OPERATION_DIR/potential_exploits.txt"
    
    echo -e "${GREEN}[+] Reconnaissance complete${NC}"
}

# ============================================
# SECTION FIVE: REPORTING
# ============================================
# Generate a summary of what you found

generate_report() {
    echo -e "\n${GREEN}================================${NC}"
    echo -e "${GREEN}OPERATION SUMMARY${NC}"
    echo -e "${GREEN}================================${NC}"
    echo -e "Target: $TARGET"
    echo -e "Operation Directory: $OPERATION_DIR"
    echo -e "Scan Results: $OPERATION_DIR/initial_scan.xml"
    echo -e "Potential Exploits: $OPERATION_DIR/potential_exploits.txt"
    echo -e "${GREEN}================================${NC}"
}

# ============================================
# SECTION SIX: EXECUTION FLOW
# ============================================
# This is where you tie everything together

main() {
    check_requirements
    configure_target
    execute_reconnaissance
    generate_report
}

# Start the script
main
```

Now let me explain what you should customize in this skeleton to make it your own.

**The Directory Structure:** I use a timestamped directory for each operation. You might want something different. Maybe you want to organize by client name, or by engagement type, or by date ranges. The important thing is consistency—decide on a structure and stick with it so you can always find your old data.

**The Tool Chain:** I've included nmap, gobuster, and searchsploit as examples, but your toolkit might need different tools entirely. If you do a lot of wireless assessments, you might need aircrack-ng. If you focus on web applications, you might need sqlmap or Burp Suite command-line tools. Add the tools that match your specialty.

**The Workflow Logic:** The skeleton shows a basic three-phase approach (scan, enumerate, search exploits), but real engagements are never that linear. You might need to add loops for persistent scanning, or conditional logic that changes your approach based on what you find. This is where your creativity comes in.

**Error Handling:** Notice how the target configuration function calls itself recursively if you don't enter anything? That's basic error handling. But in a real framework, you'd want much more robust error checking. What happens if nmap fails? What if the target is offline? What if you run out of disk space while logging? Think through these scenarios and handle them gracefully.

---

## The Philosophy Behind the Code

Let me share something I've learned through building this toolkit: the best security tools aren't the ones with the most features—they're the ones that match your specific workflow and mindset.

When I first started in security, I tried to use every tool exactly as the documentation said. I'd copy commands from tutorials verbatim. And you know what? I was slow, I made mistakes, and I didn't really understand what I was doing.

The breakthrough came when I started modifying tools to fit how my brain works. Some people like verbose output with every detail. I prefer minimal output that shows only critical information. Some people like to manually control every step. I prefer automation with strategic decision points. Neither approach is wrong—they're just different.

That's why I'm giving you these scripts with the explicit expectation that you'll change them. I don't want you to run scan09 as-is forever. I want you to take scan09, understand how it works, identify what doesn't fit your style, and modify it. Maybe you hate the color scheme. Change it. Maybe you want different nmap flags. Change them. Maybe you want to integrate a completely different tool. Do it.

The act of modifying these scripts is how you'll learn. Every time you change something, you'll have to understand what that part of the code does. You'll break things. You'll fix them. You'll discover edge cases. That's the learning process.

---

## Practical Advice for Beginners

If you're new to security and looking at this thinking "where do I even start," here's my advice:

**Start with scan01.** Don't jump to the advanced stuff. Run scan01 against a practice target (set up a vulnerable VM like Metasploitable or DVWA). Watch what it does. Look at the output files it generates. Open the script and read through it line by line. When you see a command you don't understand, look it up. When you see a flag you're not familiar with, check the man page.

**Make one change at a time.** Don't try to rewrite the entire script in one sitting. Pick one small thing—maybe change the color of the banner, or add a different nmap flag, or modify the output directory structure. Make that one change, test it, understand why it worked or didn't work, then move on to the next change.

**Break things intentionally.** This sounds counterintuitive, but it's incredibly valuable. Take a working script and deliberately break it. Remove a flag from the nmap command and see what happens. Delete an important function and watch it fail. Understanding how things break teaches you how they work.

**Keep a notebook.** Seriously. When you learn something new—maybe you discovered that the `-Pn` flag is critical for certain types of targets—write it down. Document why it matters, when to use it, and what happens without it. Your future self will thank you.

**Compare the versions.** Open scan01 and scan05 side by side. Look at how the same functionality is implemented differently. Ask yourself why I made those changes. Was it for better error handling? More features? Cleaner code? Understanding the evolution of the tool helps you understand the thinking behind it.

---

## Final Thoughts

This toolkit represents hundreds of hours of learning, experimentation, and real-world application. I'm sharing it not because I think it's perfect—I know it's not—but because I wish someone had shared something like this with me when I was starting out.

The security field can feel incredibly intimidating when you're new. Everyone seems to know things you don't. Everyone has custom tools and workflows that seem like magic. But here's the secret: we all started from zero. We all copied and modified other people's work until we understood it well enough to create our own. We all have scripts that started as someone else's code and gradually evolved into something uniquely ours.

This is my contribution to that ongoing cycle of learning and sharing. Take this code, break it, fix it, improve it, and make it yours. And then, when you've learned something valuable from the process, share it with the next person coming up behind you.

That's how we all get better.

Stay curious, stay ethical, and happy hacking.

**- oxbv1 | 0xb0rn3**

---

## Legal Disclaimer

This toolkit is provided for educational purposes and authorized security testing only. Unauthorized access to computer systems is illegal. Always ensure you have explicit written permission before conducting any security assessments. The author assumes no liability for misuse of these tools.
