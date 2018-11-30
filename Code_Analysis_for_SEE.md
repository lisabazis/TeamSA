## Code Analysis

## Code Review Strategy

## Automated Code Review

### Cross Site Request Forgery (CSRF)
Bandit did not find any CSRF security issues.

### Cross-Site Scripting (XSS)
Bandit found three instances of XSS security issues.
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss01.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss02.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss03.JPG">

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

## Summary of Key Findings

## Links to Pull Requests

## Project Board
