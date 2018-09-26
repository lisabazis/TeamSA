# Requirements for Software Security Engineering
## Backstory
Zulip is being used to increase efficiency inside the mortgage department of a lender.  The various teams that are origination, underwriting, closing, etc.  These teams need the ability to communicate within eachother and amongst the other teams.  They also need to be able to discuss individual mortgage cases in a private manner amongst the various teams that are handling that case.

## Essential Data Flows with Use Case Diagrams
[Use Case Diagrams](https://www.lucidchart.com/documents/edit/daaad814-8c7c-4694-b4ad-0f930d8dd7d6/0)

## Misuse Cases
[Misuse Case Diagrams](https://www.lucidchart.com/documents/edit/77fec034-2358-4698-8e4d-57e72b7f286e/0)

## Security Requirements Derived from Misuse Cases

## Alignment of Security Requirements with Zulip's Advertised Features

## Zulip Documented Security Related Configuration and Installation Issues

### Security-Related Configuration

##### Access
Zulip documentation specifies to set a policy for who is allowed to join the organization. This policy can be set to restrict the organization to those from the company’s email domain or allow anyone to join at will.

Zulip must be able to send out emails so it can confirm new users’ email addresses and send notifications. Documentation recommends using a transactional email service such as Mailgun, SendGrid, or Amazon SES rather than services like Gmail to avoid dealing with anti-spam measures. It is still possible to configure usage with Gmail, but it is not recommended. Email settings are configured in <i>/etc/zulip/settings.py</i>.

Each user has an API key available in the Settings page. The API key can be used to do anything that user is allowed to do. Removing a user’s access requires preventing the API key from being used to authenticate. This is done by deactivating the user’s account in the Organization settings page. Only changing the user's password or removing single-sign on (SSO) authentication would allow the active API key to be used by the user after authorization was revoked.

##### Authentication
Configuring methods for authenticating users is done by commenting out unwanted methods in <i>settings.py</i> and uncommenting any those are acceptable to use. Authentication methods include Google Auth, GitHub Auth, LDAP, and more. The only method that is enabled by default is EmailAuthBackend in which users authenticate using their email and password.

##### Password Strength
Zulip checks the strength of a password using the <i>zxcvbn</i> library. The open source project <i>zxcvbn</i> is a password strength estimator that uses pattern matching and conservative estimation to recognize 30,000 common passwords, common names, and common surnames. Password strength is controlled by two settings in <i>/etc/zulip/settings.py</i>. PASSWORD_MIN_LENGTH allows an administrator to set the minimum password length. Shorter passwords are rejected even if they pass the <i>zxcvbn</i> test. 

PASSWORD_MIN_GUESSES is the minimum acceptable strength of a password in terms of the estimated number of passwords an attacker has to try before guessing. If zxcvbn determines that the estimated number of guesses required is less than the setting, then the password is rejected

##### Network Configuration
Zulip requires that outgoing HTTP(S) access on ports 80 and 443 to the Internet be enabled so that it can properly manage inline image previews. Outgoing SMTP access to the company's SMTP server, typically port 587 so that Zulip can send email.

##### Configuration Changes
Documentation recommends to restart the server after any configuration change.

#### Installation Issues

##### Development Installation vs Production Installation
A Zulip server comes in two varieties, development and production. A development installation is used for testing and modifying Zulip to meet the organization's needs whereas the production server is an "as is" installation of the latest release for normal user usage.

##### Production Server Requirements
*	A dedicated server or VM running Ubuntu 16.04 Xenial 64-bit.
*	Minimum of 2 GB RAM and 10GB disk space
  *	increase to 4 GB RAM and 2 CPUs if over 100 people using it
*	A valid DNS name and SSL certificates
*	A way to send outgoing email

##### Development Server Requirements
* A development envrionment on macOS, Windows, or Linux (Debian or Ubuntu recommended)
* Minimum of 2 GB RAM (no required disk space listed; a minimum of 10GB can be assumed from the production server requirements)

Documentation recommends the use of the Vagrant development environment, developed by HashiCorp, to contain a Zulip development server for first time users.

##### Certificates
Since Zulip runs over HTTPS for communication, it is required to use an SSL/TLS certificate. If the organization already has its own certificate, it can be manually installed. The certificate file must include its full chain to ensure that the Zulip server will work with all browsers.

Organizations without their own certificate can use an automated Let’s Encrypt client called CertBot to get certificate from Let’s Encrypt, a free, automated CA which can be enabled during installation by giving the install script the --certbot flag.

Any errors that occur during installation are logged in <i>/var/log/zulip/errors.log</i>. Once the errors have been corrected, rerunning the install script will clean things up.

## Project Board
[Task 2 Project Board](https://github.com/lisabazis/TeamSA/projects/1)
