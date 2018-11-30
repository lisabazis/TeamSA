## Code Analysis

## Code Review Strategy
Code review strategy is to make a checklist of the threats defined in the Threat Modeling exercise and review the code relevant to those threats.  The review will be done both manually and suing automated tools.

## Automated Code Review

### Cross Site Request Forgery (CSRF)
Bandit did not find any CSRF security issues.

### Cross-Site Scripting (XSS)
Bandit found three instances of XSS security issues.

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss01.JPG">
Jinja2 is an HTML template system for building web applications in Python. It is compatibile with Python 2.6, 2.7 and any version greater than 3.3. Jinja2 has an autoescape feature that filters input strings to escape HTML content submitted via the template's variable. When enabled, escaping HTML content in input strings prevents XSS attacks. Programmers have the option to enable or disable the autoescape. If not specified, the autoescape feature is disabled by default such that no sanitization occurs. Due to they way the code was written, it is unclear whether or not the autoescape was enabled. The use of \*\*options in the function call Environment() means it will load the parameters specified in the dictionary called options.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss02.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss03.JPG">
This is actually the same issue that was flagged by two different Bandit tests. Using the function call mark_safe() defined with django.utils.safestring.mark_safe introduces the possibility of an XSS vulnerability as it explicitly marks a string as safe for output meaning that no further escaping of HTML content will occur. There is no vulnerability as long as no HTML content can be introduced to the string after it is marked safe. Further analysis is required to confirm whether or not this is a problem.

### Information Disclosure
Bandit found no Information Disclosure security issues.

### Other
Despite not being part of checklist, it was observed that Bandit found seven instances of the usage of an insecure hash function.

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash01.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash02.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash03.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash04.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash05.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash06.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash07.JPG">

In each instance, the insecure SHA-1 hash function was implemented through the Python function call hashlib.sha1(). SHA-1 only produces a message digest with a length of 160 bits which has been proven vulnerable to collision attacks. It is recommended to update each usage of SHA-1 to one of the SHA-2 variants such as SHA-256 with the Python function hashlib.sha256() which has a message digest of 256 bits.

## Manual Code Review

### Cross Site Request Forgery (CSRF)

### Cross-Site Scripting (XSS)

### Information Disclosure

## Summary of Key Findings

## Links to Pull Requests

## Project Board
https://github.com/lisabazis/TeamSA/projects/1
