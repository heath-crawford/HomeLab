Jump Server Setup - Lessons Learned
Big Picture
I set up my 2GB Raspberry Pi as a future jump server. The goal was simple:
✅ Connect to Wi-Fi for general network access.
✅ Connect to my main computer over SSH.
✅ Lock down traffic between connections for security (even if I don’t fully know how yet).

I know that separating network traffic is a good practice, even if I don’t yet understand all the ways to harden it properly. The priority was getting this thing online the right way so I could access it reliably and securely.

What Actually Happened (And Why It Wasn’t That Simple)
I had already set up two Raspberry Pis running Ubuntu, so I assumed this setup would be similar. Wrong.

This time, I installed Raspberry Pi OS Lite, which—true to its name—left out a lot of things I expected to be there:
🚫 No iptables
🚫 No Netplan (.yaml files)
🚫 No NetworkManager

Because of that, a lot of the guides online didn’t apply. Most assumed I already had those tools installed. This forced me to actually think through what was happening on a network level instead of just following instructions blindly.

I had to manually install, configure, and troubleshoot the missing pieces while also setting up:

Static IPs (so I don’t lose access if the network changes).
Persistent settings (so my configurations don’t reset on reboot).
Network priority (since the Pi has both Wi-Fi and Ethernet, I had to make sure the right one took precedence).
At first, SSH wasn’t working as expected, and I suspected a DNS issue. However, it turned out to be a combination of cached addresses, multiple network interfaces, and firewall settings interfering with connections. Restarting NetworkManager, enforcing static IPs, and fixing firewall rules eventually got everything working.

Patterns I Noticed
🔹 Things rarely work exactly how you expect.
🔹 Security is an ongoing process. Every device, every access point—it all needs to be controlled.
🔹 Hardening a system takes layers. Right now, mine is weak, but I can already see the path to making it stronger.
🔹 Networking is just controlled chaos. You have to tame it by setting clear rules and making sure only the right devices talk to each other.

What I’d Do Differently Next Time
I should have checked what’s actually included in Pi OS Lite before starting. That would’ve saved me a lot of time because I would’ve known upfront that I needed to install missing tools like iptables and NetworkManager. It really was “Lite.”

What I’m Still Unclear On
I understood what I was doing in the moment, but if you asked me to recreate some of those longer CLI commands from memory? Yeah, not happening.

There’s just so much to learn—networking, security, system administration—it feels overwhelming. But today helped me visualize how a network actually functions.

Next up: Setting up SSH key-based authentication so I don’t have to type my password every time I connect. No clue how it works yet, but I’m going to figure it out.

This is my first step toward real network control. It’s slow, but I’m learning. 🚀