Feature: Sign-up and Login (Google SSO and Email/Password)
Field	Details
Feature ID	FEAT-002
Owner (Product)	[Name]
Tech lead	[Name]
Designer	[Name]
Status	Draft
Related feature	FEAT-001 Sign-up and Account Onboarding (starts after a successful sign-up or first login)
Last updated	[Date]
1. Summary
Users can create an account and log in using either Google sign-in (SSO) or an email and password. After sign-up, the account becomes active once the phone number (and, for email/password sign-ups, the email) is verified with a 6-digit OTP; active users continue to onboarding (FEAT-001). Returning users go straight to the product.
2. Problem and Goals
Problem: Users need a quick, secure way to create an account and return to it, without being forced to manage yet another password if they do not want to.
Goals:
•	Let users sign up and log in in under a minute.
•	Offer two familiar methods: Google and email/password.
•	Keep accounts secure (verified emails, strong passwords, safe password recovery).
•	Make sure one person ends up with one account, even if they use both methods.
3. Users
User	Description
Resource owner	Owns a resource and runs it, or provides space for our application to run the resources
Resource user	Wants to use the software and access the resources
New user	Has no account and wants to sign up (either type above)
Returning user	Has an account and wants to log in
User who forgot their password	Has an email/password account and cannot log in
Invited user	Received an invitation to an organisation and signs up or logs in to accept it
Role field at sign-up: the role names stay Host (resource owner) and Customer (resource user). The role the user picks decides which onboarding path they see first (see section 6.1).
Decided:
•	One Host type. A Host can either run the resource themselves or provide space for our application to run it, and can be in both sub-types. This choice is made after sign-up, in the settings or on the resources page when the Host opens it after login. The choice is required before a Host can create a resource or list their property.
•	Host and Customer can be combined. A Host can also be a Customer and the other way round. At sign-up the user chooses one pathway. To open the other later, the user clicks the button for that part of the application (as on Airbnb), confirms with "Yes, continue as Customer" or "Yes, continue as Host", and then completes the steps for that pathway.
•	Organisations: Host / Customer applies to the whole organisation. An organisation always has an organisation admin, who is set when the organisation is created.
•	Admin transfer: the admin role is transferred by sending a confirmation to both the old and the new admin's email. The confirmation stays valid for 10 minutes, and the new admin must already be a member of the organisation. If the old admin's email is no longer reachable, we, as the application owner, make the transfer through backend calls.
•	Personal accounts: the user has only one role. A personal account has one user and no team members, so it has the full access that an organisation admin has, but the interface does not label the user as an admin.
4. Scope
In scope:
•	Sign-up and login with Google
•	Sign-up and login with email and password
•	Email OTP verification (email/password sign-ups only) and phone SMS OTP verification (all sign-ups); both required to activate the account
•	Forgot and reset password
•	Logout and session handling
•	Handling of accounts that use both methods
Out of scope (this version):
•	Multi-factor authentication (MFA)
•	Passwordless login (magic links)
•	Phone number sign-in
5. User Flows
5.1 Sign up with Google
1.	The user opens the sign-up page and clicks Continue with Google.
2.	The user chooses their Google account and grants the basic permissions (name, email, profile picture).
3.	The system creates the account using the Google email, marked as verified.
4.	The user adds the remaining mandatory details (phone number, address, country, role, consent) and verifies the phone number with a 6-digit SMS OTP, which can be done at any time. Once the phone number is verified, the account becomes active and the user continues to onboarding (FEAT-001).
5.2 Sign up with email and password
1.	The user opens the sign-up page and enters email and password (and name, if required).
2.	The system validates the input and creates the account as inactive.
3.	A verification OTP is sent to the email address.
4.	The user enters the 6-digit OTP, the email becomes verified. The user also verifies the phone number with a 6-digit SMS OTP. Both OTPs can be requested and entered at any time; once both are verified, the account becomes active and the user continues to onboarding (FEAT-001).
5.3 Log in
•	Google: the user clicks Continue with Google and is logged in if an account exists for that email.
•	Email/password: the user enters email and password and is logged in if they match. If the account is not active yet, they are taken to the verification step to finish verifying their email and phone number.
•	On success, a first-time user is sent to onboarding if it is not completed; otherwise to the dashboard.
5.4 Forgot password
1.	The user clicks Forgot password and enters their email.
2.	The system always shows the same message ("If an account exists, we sent a reset link"), whether or not the email exists.
3.	The user opens the emailed link, sets a new password, and can log in.
5.5 Logout
The user clicks Log out, the session ends, and they return to the login page.
6. Functional Requirements
ID	Requirement	Priority	Acceptance criteria
FR-1	As a new user, I can sign up with Google	Must	Given I click Continue with Google and approve access, then an account is created with my Google name and email and I am asked to complete my remaining details and verify my phone number
FR-2	As a new user, I can sign up with email and password	Must	Given I enter a valid email and a password that meets the rules, when I submit, then an account is created in an inactive state and a verification OTP is sent to my email
FR-3	As a user, I must verify my phone number with an SMS OTP (and my email with an OTP if I signed up with email/password) so that my account becomes active	Must	Given I request an OTP at any time and enter the correct 6-digit code, then that email or phone number is verified and shows a verified tick; given every required verification is complete, then my account becomes active; given any required verification is missing, then my account stays inactive and I can request a new OTP
FR-4	As a returning user, I can log in with Google	Must	Given an account exists for my Google email, when I continue with Google, then I am logged in
FR-5	As a returning user, I can log in with email and password	Must	Given correct credentials, then I am logged in (if my account is not active yet, I am taken to the verification step); given incorrect credentials, then I see a generic "incorrect email or password" error
FR-6	As a user, I can reset my password if I forget it	Must	Given I request a reset, then a reset link is emailed; given I open a valid link and set a new password, then I can log in with it and the link can no longer be used
FR-7	As a user, I can log out	Must	Given I click Log out, then my session ends and protected pages are no longer accessible
FR-8	As a user, my password must meet security rules	Must	Given I enter a password that is too weak, then I see which rules are not met and the form does not submit
FR-9	As a user, I do not end up with duplicate accounts for the same email	Must	See section 7 (account linking)
FR-10	As a user, I stay logged in for a sensible time on my device	Should	Given I log in, then my session lasts [X] days of activity, or until I log out
FR-11	As a user, I get clear errors and loading states	Should	Given a failure (network, provider error), then I see a friendly message and can retry
FR-12	As an invited user, I am added to the organisation after I sign up or log in	Should	Given I follow an invitation link and complete sign-up or login with the invited email, then I join the organisation
6.1 Mandatory sign-up fields
All eight fields below are collected at sign-up. The account becomes active only after the phone number is verified and, for email/password sign-ups, the email is verified too.
Field	Data type	Purpose and validation rules	Why it is mandatory
Full legal name	Text (string)	First and last name, matching the user's government ID	Legal contracts, tax records and fraud prevention
Email address	Email (string)	Email/password sign-ups: verified with a 6-digit OTP sent to the email address (Google sign-ups are already verified by Google)	Account identification, transactional alerts and password recovery
Phone number	Numeric, E.164 format	Collected at sign-up and verified with a 6-digit SMS OTP, which can be requested at any time after sign-up (all sign-up methods)	Real-time booking updates, emergency contact and multi-factor authentication (MFA)
Account password	String (encrypted)	Minimum 8 characters, with 1 uppercase letter, 1 symbol and 1 number (or an OAuth provider token)	Secures the account against unauthorized access
Country of residence	Enum / dropdown	ISO country code	Determines local tax rules (VAT/GST), currency defaults and the legal Terms of Service
Address	Text (structured)	Street address, city, state or region and postal code; the country comes from Country of residence [exact format and validation to be confirmed]	Legal and tax records, billing and location-based features [reason to be confirmed]
Terms and privacy consent	Boolean	Explicit checkbox consent, stored with a timestamp	Establishes the legally binding platform agreement and data-usage consent
User role selection	Enum	Host / Customer / Both	Routes the user to the correct initial onboarding flow (listing creation vs. browsing)
How this applies to each sign-up method
•	Email and password: the user completes all eight fields, then verifies the email with a 6-digit OTP and the phone number with a 6-digit SMS OTP.
•	Google: name and email are prefilled and the OAuth token replaces the password. The email counts as verified because Google has already verified it, so there is no email OTP. The user adds the phone number, address, country, role and consent, then verifies the phone number with a 6-digit SMS OTP.
•	OTPs at any time: OTPs can be requested and verified at any point after sign-up, not only right after it. Completing them is mandatory.
•	OTP limits: an OTP is valid for 10 minutes and allows a maximum of 3 wrong attempts per code. A user must wait 1 minute between resends and can request up to 3 resends per day, counted across email and SMS together.
•	Account status: a new account starts as inactive. It becomes active only when every required verification is done: phone number for all sign-ups, plus email for email/password sign-ups. If either is missing, the account stays inactive.
•	Inactive users: an inactive user can see only the home page of the application, with a message to verify the account in order to start using it.
•	Verified tick: once the email or the phone number is verified, a verified tick appears next to it on the user profile.
•	Changing email or phone: a changed email or phone number must always be verified again. While the new value waits for verification, the account stays inactive and the verified tick disappears until it is verified.
•	Clean-up: an inactive account can be deleted after 3 months, counted from the last login. The user gets a warning email 10 days before deletion and another 5 days before deletion if no action has been taken, and a final email after the account is deleted.
Points to confirm with the team
1.	MFA: phone verification is used to activate the account. MFA is out of scope for this version, so decide whether the phone number is later used as a second login factor.
2.	Phone rules: supported countries, SMS cost, whether one number can be used on more than one account, and whether the user can change the number if verification fails.
3.	Legal name: it must match a government ID. Decide whether the ID is checked (identity verification) or the name is self-declared at sign-up.
4.	Role vs. account type: decide the order of the Host / Customer choice and the Personal / Organisation choice in FEAT-001 (see section 3).
5.	Consent record: store the timestamp and the version of the Terms and Privacy Policy that was accepted.
6.	Country changes: can the country of residence be changed later, given it sets tax rules and currency?
7.	Address: confirm the format (street, city, state or region, postal code), whether it is a residential or billing address, whether it is checked for validity, and whether it can be changed later.
7. Account Linking Rules
The same person may try both methods with the same email. Proposed rules (to be confirmed):
Situation	Expected behavior
User signed up with email/password, later clicks Continue with Google using the same email	Log them into the same account and link Google to it (Google verifies the email)
User signed up with Google, later tries email/password sign-up with the same email	Do not create a second account; tell them an account exists and to log in with Google, or offer to set a password
User signed up with Google and uses Forgot password	Send a reset link that lets them add a password to the same account
Google account email differs from the email they used before	Treated as a different account (no automatic linking)
8. Security and Non-Functional Requirements
•	Passwords: stored only as salted hashes (e.g. bcrypt or argon2); never logged or shown.
•	Password rules: minimum 8 characters with at least 1 uppercase letter, 1 number and 1 symbol (see section 6.1); not required for Google sign-ups, which use the OAuth provider token.
•	Reset links and OTPs: reset links are single-use, random and expire after [1] hour; email and SMS OTPs are 6-digit codes, single-use, expire after 10 minutes, allow 3 wrong attempts per code, require a 1-minute wait between resends, and are limited to 3 resends per day across email and SMS together.
•	Brute-force protection: rate limit login attempts and lock or slow down after [X] failed attempts.
•	Transport: all authentication traffic over HTTPS; secure, HTTP-only session cookies.
•	Google sign-in: request only basic profile and email permissions; validate tokens on the server.
•	Privacy: do not reveal whether an email is registered (except where required for sign-up, handled carefully).
•	Performance: login responds in under [2] seconds for 95% of requests.
•	Accessibility: forms usable with keyboard and screen readers; error messages linked to fields.
•	Compatibility: latest two versions of Chrome, Safari, Firefox, Edge; responsive on mobile.
•	Audit and monitoring: log sign-ups, logins, failures and password resets (without sensitive data) and alert on unusual spikes.
9. UI Notes
•	One page can serve both sign-up and login, with a clear toggle.
•	Continue with Google button shown prominently, followed by an "or" divider and the email/password form.
•	Show/hide password toggle and live password-rule hints.
•	Links: Forgot password, Terms of Service and Privacy Policy (consent text at sign-up).
•	Wireframes: [link]
10. Edge Cases and Error Handling
Scenario	Expected behavior
Invalid email format	Inline error, no submission
Email already registered (sign-up)	Message that an account exists, with a link to log in
Wrong password	Generic "incorrect email or password"; count toward rate limit
Inactive account (email or phone not verified) tries to log in	Prompt to verify, with a Resend OTP option (1-minute wait between resends, 3 resends per day)
Expired, wrong or already-used OTP (email or SMS)	Explain and offer to send a new one
Expired or used reset link	Explain and offer to request a new reset
User cancels or closes the Google popup	Return to the login page without an error loop
Google returns an error or is unavailable	Friendly message and the option to use email/password
Google account has no verified email	Block sign-up and explain why
Too many failed attempts	Temporary lockout or delay with a clear message
Session expired while using the app	Redirect to login and return the user to where they were
Network failure during submit	Show a retry option and keep entered data (except the password)
11. Analytics Events
Event	When
signup_started (method)	User begins sign-up with Google or email
signup_completed (method)	Account created
email_verified	Email OTP verified
login_succeeded (method)	Successful login
login_failed (method, reason)	Failed login
password_reset_requested / completed	Reset flow steps
phone_verified	Phone SMS OTP verified
12. Success Metrics
Metric	Target
Sign-up completion rate (started to account created)	[X]%
Share of new accounts that become active (all required verifications done)	[X]%
Login success rate on first attempt	[X]%
Password reset requests per 100 active users	Under [X]
Share of sign-ups using Google vs email	Tracked, no target
13. Dependencies and Risks
Item	Type	Impact	Mitigation
Google OAuth app configuration and approval	Dependency	Sign-in cannot launch without it	Set up and verify the app early
Email delivery service	Dependency	Verification and reset emails may be delayed or land in spam	Use a reliable provider; configure SPF, DKIM and DMARC
Duplicate accounts from mixed methods	Risk	Confusion and support load	Implement the linking rules in section 7
Account takeover through weak passwords	Risk	Security incident	Password rules, rate limiting, consider MFA later
Users blocked if Google is down	Risk	Cannot log in	Email/password remains available
SMS delivery service	Dependency	Phone OTPs may be delayed or fail in some countries, so accounts cannot be activated	Use a reliable provider; confirm supported countries; allow resends within the limits
14. Rollout Plan
•	Release behind a feature flag to internal users first, then to all users.
•	If this replaces an existing login, migrate existing users without forcing a password change; keep existing sessions valid where possible.
•	Update help articles and support scripts (verification, reset, linking).
•	Rollback plan: disable the feature flag and revert to the previous login.
•	Set up the scheduled clean-up of inactive accounts: deletion after 3 months from the last login, with warning emails 10 days and 5 days before and a final email after deletion.
15. Open Questions
#	Question	Owner	Answer
1	Do we add Microsoft sign-in, and when? (Suggested: decide using the email-domain data of current users)	Product	
2	Decided: minimum 8 characters with 1 uppercase letter, 1 number and 1 symbol. Is a common-password check also required?	Product / Security	
3	Decided: the account is active only after email OTP and phone SMS OTP are both verified. Inactive users see only the home page with a message to verify their account.	Product	
4	Confirm account linking rules in section 7	Product / Tech	
5	Session length and "remember me" behavior?	Tech	
6	Do we add MFA for admins or all users? When?	Security	
7	Are there legal or consent requirements at sign-up (terms, marketing opt-in, region-specific rules)?	Legal	
8	What should happen to existing users when this launches?	Product / Tech	
16. Decision Log
Date	Decision	Reason	Decided by
[Date]	Launch with Google and email/password only	Current available methods	Product
[Date]	An account becomes active only after the phone number is verified, and for email/password sign-ups also the email (6-digit OTPs)	Google already verifies its emails, so the email OTP is only needed for email/password sign-ups	Product
[Date]	Inactive accounts are deleted 3 months after the last login, with warning emails 10 and 5 days before and a final email after deletion	Keeps accounts clean while giving users notice	Product
[Date]	Two sign-up roles: Host (resource owner) and Customer (resource user); a user can use both and opens the second pathway later	A Host can also be a Customer and the other way round	Product
[Date]	Host / Customer applies to the whole organisation; every organisation has an admin; admin transfer needs confirmation from the old and new admin (valid 10 minutes)	Every organisation always has an admin	Product
17. Change Log
Date	Version	Change	Author
[Date]	0.1	Initial draft	
[Date]	0.2	Added mandatory sign-up fields, OTP verification and account activation rules, user types and roles, and account clean-up	

