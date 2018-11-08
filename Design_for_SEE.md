## DFD Level 0 Diagrams
A level 0 data flow datagram was created for each of three use cases: (1) a system administrator managing user accounts, (2) a user creating a private stream, and (3) an API bot requesting data.

<img src="https://github.com/lisabazis/TeamSA/blob/master/DFD0-1.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/DFD0-2.JPG">
<img src="https://github.com/lisabazis/TeamSA/blob/master/DFD0-3.JPG">

Creation of the invididual level 0 diagrams shows similiar data flows through the same processes and data stores with the only difference being the type of request. Since all requests must be made over HTTPS, these diagrams were consolidated into a single diagram.

<img src="https://github.com/lisabazis/TeamSA/blob/master/DFD0-0.JPG">

## DFD Level 1 Diagram
A single level 1 data flow diagram was built on the consolidated level 0 diagram.

<img src="https://github.com/lisabazis/TeamSA/blob/master/DFD1.JPG">

## Threat Analyis Report
[Threat Analysis Report](https://github.com/lisabazis/TeamSA/blob/master/Threat%20Modeling%20Report.pdf)

## Alignment Observations with Zulip Project

Of the 42 identified threats, 12 needed further investigation.  10 had one commonality; they dealt with denial of service threats. The other 2 had another commonality; they required multi-factor authentication to prevent compromised credentials.

Zulip was designed with security in mind when looking at access controls, authentication methods, traffic is all encrypted, cross site scripting, etc.  However, we found that Zulip was not designed to be resilient in handling network type denial of service attacks.  Further investigation needs to occur to see if Zulip can be architected in a highly redundant, fail safe model with network controls such as load balancing to help prevent network based denial of service attacks.  

Further investigation is also required to see if Zulip could integrate with a multi-factor authentication system to ensure that the threat of compromised credentials is mitigated.

## Project Board
[Task 4 Project Board](https://github.com/lisabazis/TeamSA/projects/1)
