# Team SA:  Zulip Project Proposal

# Team Members:  Lisa Bazis, Gary Roth, Tyler Mayberry

# Security Needs

* Identification and Authentication (home, enterprise, regulated)
* Access Control (home, enterprise, regulated)
* Audit (enterprise, regulated)
* System Integrity (enterprise, regulated)
* Data Integrity (enterprise, regulated)
* Reliability of Service (enterprise, regulated)
* Product Development Assurance (enterprise, regulated)
* Product Documentation Assurance (enterprise, regulated)

# Exiting Security Features of Zulip
* Traffic between clients (web, desktop and mobile) and the Zulip is encrypted using HTTPS. By default, all Zulip services talk to each other either via a localhost connection or using an encrypted SSL connection.
* Zulip requires CSRF tokens in all interactions with the web API to prevent CSRF attacks.
* The preferred way to login to Zulip is using an SSO solution like Google Auth, LDAP, or similar, but Zulip also supports password authentication. See the authentication methods documentation for details on Zulip’s available authentication methods.
* Zulip stores user passwords using the standard PBKDF2 algorithm.
* Zulip message content is rendered using a specialized Markdown parser which escapes content to protect against cross-site scripting attacks.
* Zulip supports both public streams and private streams. Any Zulip user can join any public stream in the realm, and can view the complete message history of any public stream without joining the stream.
* A private stream is hidden from users who are not subscribed to the stream.
* Zulip supports editing the content and topics of messages that have already been sent. As a general philosophy, our policies provide hard limits on the ways in which message content can be changed or undone. In contrast, our policies around message topics favor usefulness (e.g. for conversational organization) over faithfulness to the original.  (##INTEGRITY ISSUES##)

# Motivation for selecting Zulip

Motivation for selecting this software was the fact that collaboration/chat is now a requirement and normal means of communication for users in all environments.  From home use of communication of family members, volunteer groups, corporate/enterprise use, law enforcement etc.  All groups need to effectively communicate if they are to succeed.  With the world becoming borderless, the need to collaborate at anytime and anywhere has resulted in numerous applications such as this to be created.  However, as the threat environments become more restrictive, the security requirements become more important and therefore the software needs to become more restrictive.  Zulip claims to be enterprise ready.  We are evaluating the software to see if their claim is accurate and can be attested to.

# Project Description

This project involves contributing to an open source community and addressing the security needs of its end users in the intended threat environment of the deployed software. To this end, we chose to contribute to [Zulip](https://zulip.org/), a real-time chat and productivity application, similar to Slack with support for threaded conversation and file-sharing. Zulip is written using Python as the primary language with a JavaScript-based client interface. It has a healthy, active community consisting of over 300 contributors and averaging 500 commits per month, and boasts a number of beginner friendly issues to be solved.


# License and contributor agreements

Licensed under the Apache License, Version 2.0 

# Security Related History

Zulip has had 7 vulnerabilities specified in the CVE database going back to March 2017 consisting of issues with access control and cross-site scripting. The earliest CVE-2017-0881 covers an access issue in which users could subscribe to a private conversation stream without an authorized invitation from the conversation members through "an error in the implementation of an autosubscribe feature in the check_stream_exists route of the Zulip group chat application server before 1.4.3". In CVE-2017-0896 pubilished in June 2017, it was discovered that an autnenticated user could invite other users to their organization's domain even if the orgnaization had configured the domain to prevent this. This flaw was due to an implementation error in the invite_by_admins_only setting in the Zulip group chat application server in version 1.5.1. A month later in July 2017, all versions prior to Zulip Server 1.7.1 allowed for an authorized user to invite any user from any different realm (domain) to their realm within the same server. The remaining four vulnerabilites all published in 2018 described different instances of cross-site scripting. CVE-2018-9986, 	CVE-2018-9990, and CVE-2018-9999 found XXS issues with the with the frontend markdown processor, with stream names in topic typeahead, and with user uploads and the default LOCAL_UPLOADS_DIR storage backend respectively in all versions of Zulip server prior to 1.7.2. In the middle of these discoveries, it was found that versions 1.5.x, 1.6.x, and 1.7.x before 1.7.2, had an XSS issue with muting notifications described by CVE-2018-9987.


[Zulip CVEs](https://www.cvedetails.com/vulnerability-list/vendor_id-16270/Zulip.html)

# Repository

