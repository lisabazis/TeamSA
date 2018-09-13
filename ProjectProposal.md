# Team SA:  Zulip Project Proposal

# Team Members:  Lisa Bazis, Gary Roth, Tyler Mayberry

# Security Needs

The security needs of users from this software in its intended threat environment are listed below.
The threat environments include, but are not limited to home/community, enterprise, regulated.  

* Identification and Authentication (home/community, enterprise, regulated)
* Access Control (home/community, enterprise, regulated)
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

# License and contributor agreements

The software is licensed via under the Apache License, Version 2.0.

# Security Related History

# Repository

https://github.com/lisabazis/TeamSA
