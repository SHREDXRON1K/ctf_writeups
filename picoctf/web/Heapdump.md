# SSTI 1
**Category:** Web Exploitation  
**Date:** 26.04.2026  
**Difficulty:** Easy

Author: Prince Niyonshuti N.

Description
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint
that exposes a file containing a hidden flag. The application is a simple blog website where you can
read articles about various topics, including an article about API Documentation. 
Your goal is to explore the application and find the endpoint that generates files holding 
the server’s memory, where a secret flag is hidden.

Additional details will be available after launching your challenge instance.




Tools : 
1. Chrome and Google (just for visiting target website and research about headpump)
2. Claude AI (research about headpump and strings command in linux cli)


How to get Flag : 
1. Visit the website and see something interesting

2. The owner posted about backend development with #node.js, #swagger UI, #API Documentation
 
3. I clicked the #API Documentation and it redirects to endpoint /api-docs/

4. Diagnosing (located at the bottom of the page) seems interesting and it says it returns 
 a memory allocation status which what I need to look for.
 I clicked "try it out" -> "execute" -> In Responses (Details), there is a downloadable file
 Download the File and it contains json nonsense with a lot of numbers. I researched it and 
 it turns out that it is probably a garbage file
 
5. I used strings tool to gather some human-like readable words from binary/garbage file.
 command : strings <filename> | grep -i "CTF{"	// that's the pattern of the flag
 and voila, the flag is extracted


Side note : 
 The website is obviously misconfigured. The owner most likely thinks that such thing like heapdump 
 doesn't contain sensitive infos at a glance or just forgot to erase it before production cause
 it was used for debugging. Heapdump is actually a snapshot of program's memory and contains live objects
 from the program (in this case website) in a specific moment of time.
 
 Running Node.js app
        ↓
  Heap Memory contains:
  - Variables
  - Objects
  - Strings
  - Secrets / JWT keys
  - Passwords
  - Anything loaded into memory

 Basicaly it's a photograph of everything what the app knows at that moment.  

Flag : picoCTF{Pat!3nt_15_Th3_K3y_dc0756a3}


What I learned : 
1. Heapdump is a snapshot of a program's memory at specific moment of time that contains live objects
2. strings tool in linux cli, used to look for human-like readable words in a binary/garbage file

