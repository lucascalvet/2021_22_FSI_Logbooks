# Trabalho realizado na Semana #3

CVE-2017-11882

## Identification

- CVE-2017-11882 is a Microsoft Office vulnerability that allows attackers to run arbitrary code, taking advantage of a memory corruption glitch.
- It works with all unpatched Microsoft Office versions released in the past 17 years (including Microsoft Office 365).
- The vulnerability was caused by memory mishandling in the equation's editor
- The editor executable module (EQNEDT32.EXE) was compiled in late 2000s, having no further compilation for the following versions of Office. 

## Catalogation

- The exploit was dicovered in November of 2017.
- It was discovered by a group of researchers at Embedi.
- The vulnerability has been lurking for 17 years
- Microsoft released a patch immediately after the first reports, in November of 2017. Therefore all updated versions of the Office can't be exploited.

## Exploit

- The exploit allows an attacker to run arbitrary code in the context of the current user by failing to properly handle objects in memory
- Exploitation of the vulnerability requires that a user open a specially crafted file with an affected version of Microsoft Office or Microsoft WordPad software.
-  In an email attack scenario, an attacker could exploit the vulnerability by sending the specially crafted file to the user and convincing the user to open the file. In a web-based attack scenario, an attacker could host a website (or leverage a compromised website that accepts or hosts user-provided content) containing a specially crafted file designed to exploit the vulnerability.
- This vulnerability also has multiple malware associated, like Loki, FormBook and Pony/FAREIT

## Attacks

- There are countries, like China, North Korean, and Russia that are continuously taking advantage of this Office bug since at least 2016. 
- As a matter of fact, an FBI report published on May 12 2020, listed it as one of the top 10 vulnerabilities routinely getting exploited.
- An attacker who successfully exploited the vulnerability could run arbitrary code in the context of the current user. 
- If the current user is logged on with administrative user rights, an attacker could take control of the affected system. An attacker could then install programs; view, change, or delete data; or create new accounts with full user rights.
