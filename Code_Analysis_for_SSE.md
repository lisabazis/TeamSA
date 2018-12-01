## Code Analysis for Software Security Engineering

## Code Review Strategy
Code review strategy is to make a checklist of the threats defined in the Threat Modeling exercise and review the code relevant to those threats. The review will be done both manually and using automated tools.

## Automated Code Review
Automated code review was performed by running the static analysis tool Bandit on all source code files for the Zulip Production Server available for download [here](https://www.zulip.org/dist/releases/zulip-server-latest.tar.gz). Bandit specifically tests for security issues in Python source code scoring each flagged issue with a severity level of low, medium, or high and a confidence level of low, medium, or high. If the report output is formatted as HTML, each flagged issue is color coded based on the severity level.

The scope of the review was limited to a checklist of cross-site request forgery, cross-site scripting, and information disclosure as those threats were highly prevelant in the Threat modeling exercise. The full report of the automated scan is available [here](https://github.com/lisabazis/TeamSA/blob/master/Bandit_Report.pdf). Note that the color background of each finding was removed upon conversion of HTML to PDF.

### Cross-Site Request Forgery (CSRF)
Bandit did not find any CSRF security issues.

### Cross-Site Scripting (XSS)
Bandit found three instances of XSS security issues.

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss01.JPG"><br>
Jinja2 is an HTML template system for building web applications in Python. It is compatibile with Python 2.6, 2.7 and any version greater than 3.3. Jinja2 has an autoescape feature that filters input strings to escape HTML content submitted via the template's variable. When enabled, escaping HTML content in input strings prevents XSS attacks. Programmers have the option to enable or disable the autoescape. If not specified, the autoescape feature is disabled by default such that no sanitization occurs. Due to they way the code was written, it is unclear whether or not the autoescape was enabled. The use of \*\*options in the function call Environment() means it will load the parameters specified in the dictionary called options.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss02.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_xss03.JPG">

This is actually the same issue that was flagged by two different Bandit tests. Using the function call mark_safe() defined with django.utils.safestring.mark_safe introduces the possibility of an XSS vulnerability as it explicitly marks a string as safe for output meaning that no further escaping of HTML content will occur. There is no vulnerability as long as no HTML content can be introduced to the string after it is marked safe. Further analysis is required to confirm whether or not this is a problem.

### Information Disclosure
Bandit found no Information Disclosure security issues.

### Other
Despite not being part of checklist, it was observed that Bandit found seven instances of the usage of an insecure hash function.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash01.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash02.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash03.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash04.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash05.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash06.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/bandit_report_hash07.JPG">

In each instance, the insecure SHA-1 hash function was implemented through the Python function call hashlib.sha1(). SHA-1 only produces a message digest with a length of 160 bits which has been proven vulnerable to collision attacks. It is recommended to update each usage of SHA-1 to one of the SHA-2 variants such as SHA-256 with the Python function hashlib.sha256() which has a message digest of 256 bits.

## Manual Code Review
Manual review efforts were focused on confirming or disproving the inconclusive results of the automated scanning.

### Cross-Site Request Forgery (CSRF)
The automated review did not find any CSRF security issues, however, it was possible to verify that CSRF tokens are implemented as claimed by the Zulip documentation.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/manual_csrf01.JPG"><br>

This code snippet found in zproject/settings.py shows that the CSRF token is enabled for Zulip production servers and makes the extra effort to stop any Javascript from reading it.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/manual_csrf02.JPG"><br>

This code snippet found in zserver/middleware.py shows a class implmentation of handling errors with the CSRF token.<br>

### Cross-Site Scripting (XSS)
Automated results for XSS security issues were both inconclusive. It was possible to confirm that each result was a false positive.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/manual_xss01.JPG"><br>

This code snippet found in zproject/settings.py shows that the Jinja2 autoescape extension is enabled.<br>

<img src="https://github.com/lisabazis/TeamSA/blob/master/manual_xss02.JPG"><br>

This code snippet found in zerver/templatetags/app_filters.py shows a comment that the Zulip developers purposely use the make_safe() function call for rare cases to prevent software runtime errors. This does not disprove that an XSS issue exists as it is unknown if the 'unescape_rendered_html' variable can be maliciously set to true, but it does show that the programmers did not arbitrarily use an insecure function.

### Information Disclosure
Manual review did not uncover any information disclosure security issues.

## Summary of Key Findings
Manual and automated code review of the Zulip Production Server with such a limited scope did not produce many interesting results. The security issues that were focused on for this review were not found or proved to be false positives through the Bandit tool. 333 security issues were flagged by Bandit, most of which were of low severity.

[CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')](https://cwe.mitre.org/data/definitions/79.html) would apply if it can be proven with further testing that the developer's intentional usage of the mark_safe() function can be exploited by an XSS attack.

Although outside of the original scope of the review, use of the insecure SHA-1 hash function was found since one of the flagged instances was listed next to the flagged XSS issues in the report. This may not be a concern as this hash function is not being used for passwords. None the less, usage falls under [CWE-328: Reversible One-Way Hash](https://cwe.mitre.org/data/definitions/328.html).

Zulip documentation contains multiple sections pertaining to security demonstrating that it was well thought-out by the developers during the design process.

## Links to Pull Requests
No pull requests were made, but an issue was opened to direct attention to the use of the SHA-1 hash function.<br>
[Insecure SHA-1 Hashing](https://github.com/zulip/zulip/issues/10934)

## Project Board
[Task 6 Project Board](https://github.com/lisabazis/TeamSA/projects/1)
