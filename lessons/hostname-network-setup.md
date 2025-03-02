Changing the Hostname & Strengthening My Network

Big Picture: Changing the Hostname and Structuring My Network

Today’s focus was on changing the hostname of my Raspberry Pis, refining my network structure, and ensuring secure access through my jump server. The ultimate goal was to:

✅ Change the hostname properly across my setup without breaking access.
✅ Use the right tools to execute commands efficiently.
✅ Ensure my main desktop can only access the network through the jump server.
✅ Set up firewall rules for security while still maintaining functionality.
✅ Lay the groundwork for future security upgrades, including pfSense.

I learned that making fundamental changes, like renaming a machine, can be more involved than expected. It’s not just about executing a command—it’s about understanding what’s happening behind the scenes and why certain restrictions exist.

What Actually Happened (And Why It Wasn’t That Simple)

I assumed renaming my Raspberry Pi would be straightforward, but as usual, it wasn’t.

1. Git Bash vs. Windows CMD

🚫 Windows CMD wasn’t cutting it.
✅ I needed Git Bash for proper SSH functionality and command execution.

2. Root Access & Temporary Admin Workaround

I ran into an issue where I couldn’t log in as root using just a password. This was by design—good security practice prevents direct root login via SSH. However, to rename the device properly, I needed root privileges. The solution?

🛠 Workaround: I created a temporary admin user with sudo privileges, changed the hostname through that account, and then switched back to my primary adminuser account. Now everything is standardized under adminuser, ensuring consistency across my devices.

🔹 Lesson Learned: Security restrictions exist for a reason. Instead of trying to bypass them, it’s better to work within the system and use proper administrative methods.

Refining My Home Network Security

As I thought more about security, I decided to structure my home network so that all access must go through the jump server. This setup ensures:

✅ My desktop can only communicate with my Raspberry Pis through the jump server.
✅ The Pis cannot be accessed directly from the network—only via the jump server.
✅ The jump server serves as a single access point, reducing attack surfaces.

To achieve this, I:

Installed iptables on my jump server.

Used UFW (Uncomplicated Firewall) on my other two Raspberry Pis.

Restricted network access so that my desktop cannot directly connect to them.

This setup creates a controlled environment where I act as the only administrator, enforcing strict access rules.

Firewalls & Future Plans

Right now, my network uses:

iptables on the jump server.

UFW on the Raspberry Pis.

🔹 But I’m planning to replace UFW with pfSense later.

This brought up an interesting lesson: when switching firewalls, it’s important to purge the old one. Simply removing it doesn’t always clean up all configurations. Even after purging UFW, I found some lingering UFW chains in iptables that I had to manually delete. This is something I’ll likely have to deal with again when transitioning to pfSense.

Final Network Setup & Lessons Learned

✔ Jump Server as a Gatekeeper: My desktop can now only connect to the Raspberry Pis via the jump server.
✔ Authentication Enforcement: Even from the jump server, I still need to enter a password to access any computer.
✔ Windows Firewall Quirk: Windows allows outbound SSH but blocks inbound by default—not a problem for me, but interesting.
✔ Security Requires Iteration: This setup is functional, but I know I’ll refine it as I learn more.

Next Steps & Future Exploration

🔹 Brainstorming what comes next. Now that I have a structured network, I want to:

Improve security rules and logging.

Learn more about pfSense and how it compares to iptables and UFW.

Automate some of my security policies.

Today was a solid step forward in locking down my lab and understanding how my devices should communicate. More to come! 🚀
