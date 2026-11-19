</head>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->


Field | Details
-- | --
Feature ID | [IA-4](https://insta-ad.atlassian.net/browse/IA-4) (Jira feature). Wiki reference: FEAT-002
Jira workstream | [IA-1](https://insta-ad.atlassian.net/browse/IA-1) Accounts, Identity and Onboarding
Jira stories and tasks | See section 18
Owner (Product) | [Name]
Tech lead | [Name]
Designer | [Name]
Status | Draft
Related feature | FEAT-001 Sign-up and Account Onboarding   (starts after a successful sign-up or first login)
Related Jira features | [IA-85](https://insta-ad.atlassian.net/browse/IA-85) User Home Page, [IA-108](https://insta-ad.atlassian.net/browse/IA-108) Organisations, Teams and Workspaces
Last updated | 2026-11-16



<h2><span lang=EN-US>1. Summary<o:p></o:p></span></h2>

<!--EndFragment-->
</body>


Users can create an account and log in using either **Google sign-in (SSO) or an email and password**. Once all mandatory details are provided, the account is created and becomes active after the phone number (and, for email/password sign-ups, the email) is verified with a 6-digit OTP (online verification). Any account (Personal or Organisation) can also be verified and activated by our backend team, as an additional way to the online OTP verification. Active users continue to onboarding (FEAT-001). Returning users go straight to the product.


<h2><span lang=EN-US>2. Problem and Goals<o:p></o:p></span></h2>

**Problem:** Users need a quick, secure way to create an account and return to it, without being forced to manage yet another password if they do not want to.
**Goals:**
* Let users sign up and log in in under a minute.
* Offer two familiar methods: Google and email/password.
* Keep accounts secure (verified emails, strong passwords, safe password recovery).
* Make sure one person ends up with one account, even if they use both methods.


</head>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>3. Users<o:p></o:p></span></h2>


<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->


User | Description
-- | --
Resource owner (Host) | Host type 1: owns the resource, lists it in our application and controls it. Host type 2: provides rental space to assemble our resource and is paid for the space, with no control over the resource (we have full control)
Resource user (Customer) | Wants to use the software, book the resources and pay for their usage
New user | Has no account and wants to sign up   (either type above)
Returning user | Has an account and wants to log in
User who forgot their password | Has an email/password account and cannot   log in
Invited user | Received an invitation to an organisation   and signs up or logs in to accept it



<!--EndFragment-->
</body>

**Role selection:** the role names are **Host** (resource owner) and **Customer** (resource user). The role is the type of user, so it is separate from the account type (Personal or Organisation) in FEAT-001. Role is not a mandatory sign-up field. The user picks a role later by landing on the Host or Customer page and filling in the relevant details there (see section 6.1).

**Role flows:** there are two main user types, and each has its own page: the [Host flow](https://github.com/InstaAd/Engineering-Wiki/wiki/User-Account-Host-Flow) (Host type 1 and Host type 2) and the [Customer flow](https://github.com/InstaAd/Engineering-Wiki/wiki/User-Account-Customer-Flow). They describe what each user type does after the account is active.

**Home page:** the [User Home Page](https://github.com/InstaAd/Engineering-Wiki/wiki/Feature-%E2%80%90-User-Home-Page) describes what each user sees after the account is approved: the Personal home page, and the Organisation home page for an Admin or a Member.

**Current application mapping (observed 2026-11-16):** users first complete the account-level mandatory fields and account verification/activation under this feature ([IA-4](https://insta-ad.atlassian.net/browse/IA-4)); after activation, the signed-in app exposes the role surfaces below. Host-specific mandatory details and verification are an additional Host gate under [IA-449](https://insta-ad.atlassian.net/browse/IA-449), with Host inventory remaining inactive until approved ([IA-478](https://insta-ad.atlassian.net/browse/IA-478)).

| Current application surface | Role mapping | Existing wiki/Jira mapping |
|---|---|---|
| My Screens and Register Screen (`/devices`, `/devices/register`) | Host / screen owner, Host type 1 | [Host flow](./User-Account-Host-Flow.md); Host Pathway and Host Types [IA-177](https://insta-ad.atlassian.net/browse/IA-177), choose Host type [IA-178](https://insta-ad.atlassian.net/browse/IA-178), Host verification [IA-449](https://insta-ad.atlassian.net/browse/IA-449) |
| Rent Location and My Listings (`/rent-location/listings`) | Host / rental-location provider, Host type 2 | [Host flow](./User-Account-Host-Flow.md); related Host issues [IA-177](https://insta-ad.atlassian.net/browse/IA-177), [IA-178](https://insta-ad.atlassian.net/browse/IA-178), ownership details [IA-458](https://insta-ad.atlassian.net/browse/IA-458) |
| Campaigns and Media (`/campaigns`, `/campaigns/create`, `/ads`) | Customer / advertiser / campaign publisher | [Customer flow](./User-Account-Customer-Flow.md); Customer Pathway and Onboarding [IA-140](https://insta-ad.atlassian.net/browse/IA-140), Customer page story [IA-141](https://insta-ad.atlassian.net/browse/IA-141) |
| Signed-in dashboard and organizations/workspaces | Activated user; routes to the user's available role surfaces | [User Home Page](./User-Home-Page.md); home page [IA-85](https://insta-ad.atlassian.net/browse/IA-85), organizations/workspaces [IA-108](https://insta-ad.atlassian.net/browse/IA-108) |

This table records the current app mapping and does not replace the future requirements in this page or the linked role-flow pages. In particular, the planned Host type 2 description is rental space for an InstaAd resource, while the current app's Rent Location workflow describes a location for advertisers to rent; retain both and confirm their product/Jira alignment. Related Jira IDs above may not cover every detailed app workflow; the role pages call out where a dedicated existing issue was not identified.

**Decided:**
•	One Host role with two types. **Host type 1** owns the resource, lists it in our application and controls it. **Host type 2** provides rental space to assemble our resource and is paid for the space; this Host has no control over the resource, and we have full control. A Host can be in both types. This choice is made after sign-up, in the settings or on the resources page when the Host opens it after login. The choice is required before a Host can create a resource or list their property.
•	Host and Customer can be combined. A Host can also be a Customer and the other way round. The user does not choose a role at sign-up; the first pathway is chosen by landing on the Host or Customer page after the account is active. To open the other later, the user clicks the button for that part of the application (as on Airbnb), confirms with "Yes, continue as Customer" or "Yes, continue as Host", and then completes the steps for that pathway.
•	Organisations: Host / Customer applies to the whole organisation. An organisation always has an organisation admin, who is set when the organisation is created.
•	Admin transfer: the admin role is transferred by sending a confirmation to both the old and the new admin's email. The confirmation stays valid for 10 minutes, and the new admin must already be a member of the organisation. If the old admin's email is no longer reachable, we, as the application owner, make the transfer through backend calls.
•	Personal accounts: the user has only one role. A personal account has one user and no team members, so it has the full access that an organisation admin has, but the interface does not label the user as an admin.

<img width="900" height="587" alt="image" src="https://github.com/user-attachments/assets/85880cf5-d5d7-4e22-b505-80c19c3e8a79" />

second pathway and admin transfer · 2 flows
A user opens the other pathway with one confirmation. An admin transfer needs a confirmation from both the old and the new admin within 10 minutes; if the old admin’s email is not reachable, the application owner makes the transfer through the backend.

<h2><span lang=EN-US>4. Scope <o:p></o:p></span></h2>

**In scope:**

* Sign-up and login with Google
* Sign-up and login with email and password
* Email OTP verification (email/password sign-ups only) and phone SMS OTP verification (all sign-ups); both required to activate the account
* Backend team verification and activation of accounts (Personal and Organisation), in addition to online OTP verification
* Forgot and reset password
* Logout and session handling
* Handling of accounts that use both methods

**Out of scope (this version):**

* Multi-factor authentication (MFA)
* Passwordless login (magic links)
* Phone number sign-in

<h2><span lang=EN-US>5. User Flows <o:p></o:p></span></h2>

**Step 1: Sign up or log in** The user signs up by providing all mandatory details (section 6.1) to create the account, or logs in if they already have an account.
**Step 2: Choose account type (required, first onboarding step)** The user selects one option: **Personal **or **Organisation**. They cannot continue until they choose.
 
<img width="900" height="632" alt="image" src="https://github.com/user-attachments/assets/ed3a30bb-8b2c-44c4-a0c4-45f6131b4e05" />

choosing the account type · 1 decision
The account type is chosen first. It decides what setup the user gets, and both choices then continue to account activation and onboarding.
**Path A: Organisation**
1.	**Enter organisation details.** The user provides the organisation (company) name, the admin's full name, the legal registered address of the company and the work email from the sign-up details, for example sample-user@sample-domain.com.
2.	**Domain detected automatically.** The system extracts the domain (sample-domain.com) from the email and shows it to the user.
3.	**User confirms the domain.** The user confirms it is correct, or edits it if it is not.
4.	**Activate the account.** There are two types of verification, and the account is activated by one way or the other. **Online verification:** the user requests and enters a 6-digit SMS OTP for the phone number (and, for email/password sign-ups, a 6-digit email OTP) at any time after the account is created. **Backend verification:** our backend team verifies the account and activates it, for example when we meet the customer, to speed up the process. It is an additional way to activate the account and does not replace the online OTPs. Until the account is verified and activated it stays inactive. After activation the email can be changed, and a changed email must be verified again (see section 6.1).
5.	**Add team members (optional).** The user can enter emails and assign a role to each now, or choose Skip for now and do it later from settings.
6.	**Create workspaces (optional).** The user can create one or more workspaces inside the organisation, and assign organisation members to them. This can also be done later.
7.	Finish. The user lands in the organisation dashboard.
**Path B: Personal account**
1.	**Activate the account.** There are two types of verification, and the account is activated by one way or the other. **Online verification:** the user requests and enters a 6-digit SMS OTP for the phone number (and, for email/password sign-ups, a 6-digit email OTP) at any time after the account is created. **Backend verification:** our backend team verifies the account and activates it, for example when we meet the customer, to speed up the process. It is an additional way to activate the account and does not replace the online OTPs. Until the account is verified and activated it stays inactive. After activation the email can be changed, and a changed email must be verified again (see section 6.1).
2.	**Complete basic profile setup** (for example name and preferences).
3.	**Finish.** There is no domain step and no team member step.

<img width="900" height="904" alt="account-activation-and-onboarding" src="https://github.com/user-attachments/assets/45e6eb4f-d201-4c65-8ced-8994de48d44b" />


account activation and onboarding · 2 decisions
The mandatory sign-up details (section 6.1) are provided when the account is created and, for organisations, the domain is confirmed. OTP verification can then be requested at any time, and the account stays inactive until it is complete. Onboarding starts only once the account is active, and the email can be changed after activation. The optional organisation steps can also be done later.


<img width="900" height="625" alt="signup-and-account-activation" src="https://github.com/user-attachments/assets/d94597c2-2b5e-4b49-9638-e9039693af04" />

sign-up and account activation · 2 methods, 1 decision
Both sign-up methods create an inactive account once all mandatory details are provided. It becomes active only when the phone number (and, for email/password sign-ups, the email) is verified with a 6-digit OTP, and the OTPs can be requested and entered at any time after the account is created.

### 5.1 Sign up with Google
1.	The user opens the sign-up page and clicks **Continue with Google**.
2.	The user chooses their Google account and grants the basic permissions (name, email, profile picture).
3.	The system prefills the name and email from the Google account; the email is marked as **verified**.
4.	The user adds the remaining mandatory details (phone number, address including country, terms and privacy consent). No password is needed, as the Google token replaces it.
5.	The system creates the account as **inactive**.
6.	The user verifies the phone number with a 6-digit SMS OTP, which can be requested at any time after the account is created. Once the phone number is verified, the account becomes active and the user continues to onboarding (FEAT-001).
### 5.2 Sign up with email and password
1.	The user opens the sign-up page and enters all mandatory details: full legal name, email, password, phone number, address including country, and terms and privacy consent.
2.	The system validates the input and creates the account as **inactive**.
3.	The user can request a 6-digit verification OTP for the email at any time; it is sent to the email address.
4.	The user enters the 6-digit OTP, the email becomes **verified**. The user also verifies the phone number with a 6-digit SMS OTP. Both OTPs can be requested and entered at any time; once both are verified, the account becomes active and the user continues to onboarding (FEAT-001).
**Sample UI workflow: sign up**

<img width="900" alt="Sign up: sample UI workflow" src="https://github.com/InstaAd/Engineering-Wiki/wiki/images/ui-sign-up.png" />

**Sample UI workflow: verify and activate the account**

<img width="900" alt="Verify and activate the account: sample UI workflow" src="https://github.com/InstaAd/Engineering-Wiki/wiki/images/ui-verification.png" />

### 5.3 Log in
•	**Google**: the user clicks **Continue with Google** and is logged in if an account exists for that email.
•	**Email/password**: the user enters email and password and is logged in if they match. If the account is not active yet, they are taken to the verification step to finish verifying their email and phone number.
•	On success, a first-time user is sent to onboarding if it is not completed; otherwise to the dashboard.

<img width="900" height="672" alt="image" src="https://github.com/user-attachments/assets/72cd8873-cec5-4447-ab22-b34d611c0930" />

login flow · 3 decisions
Logging in does not skip verification: an inactive account sees the home page with a message to verify, and only active accounts continue to onboarding or the dashboard.

### **5.4 Forgot password**
1.	The user clicks Forgot password and enters their email.
2.	The system always shows the same message ("If an account exists, we sent a reset link"), whether or not the email exists.
3.	The user opens the emailed link, sets a new password, and can log in.

<img width="900" height="629" alt="image" src="https://github.com/user-attachments/assets/04e07eff-1a63-4eb4-9611-51c8ff298d09" />


### **5.5 Logout**
The user clicks Log out, the session ends, and they return to the login page.

<img width="900" height="421" alt="image" src="https://github.com/user-attachments/assets/6e2f7d79-4b3c-41f7-b929-373f46e78145" />


<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:w="urn:schemas-microsoft-com:office:word"
xmlns:m="http://schemas.microsoft.com/office/2004/12/omml"
xmlns="http://www.w3.org/TR/REC-html40">


<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>6. Functional Requirements<o:p></o:p></span></h2>


ID | Requirement | Priority | Acceptance    criteria
--   | --   | --   | --
FR-1 | As a new user, I can sign up with Google | Must | Given I click Continue with Google and approve access, then my Google name and email are prefilled and I am asked to complete my remaining mandatory details (phone number, address, consent); given all are provided, then an account is created in an inactive state
FR-2 | As a new user, I can sign up with email and password | Must | Given I enter all mandatory details (full legal name, email, a password that meets the rules, phone number, address, consent), when I submit, then an account is created in an inactive state and I can request verification OTPs
FR-3 | As a user, I must verify my phone number with an SMS OTP (and my email with an OTP if I signed up with email/password) so that my account becomes active | Must | Given my account is created with all mandatory fields, when I request an OTP at any time and enter the correct 6-digit code, then that email or phone number is verified and shows a verified tick; given every required verification is complete or the backend team has verified my account, then my account becomes active; given any required verification is missing, then my account stays inactive and I can request a new OTP
FR-4 | As a returning user, I can log in with   Google | Must | Given an account exists for my Google   email, when I continue with Google, then I am logged in
FR-5 | As a returning user, I can log in with   email and password | Must | Given correct credentials, then I am   logged in (if my account is not active yet, I am taken to the verification   step); given incorrect credentials, then I see a generic "incorrect   email or password" error
FR-6 | As a user, I can reset my password if I   forget it | Must | Given I request a reset, then a reset   link is emailed; given I open a valid link and set a new password, then I can   log in with it and the link can no longer be used
FR-7 | As a user, I can log out | Must | Given I click Log out, then my session   ends and protected pages are no longer accessible
FR-8 | As a user, my password must meet security   rules | Must | Given I enter a password that is too   weak, then I see which rules are not met and the form does not submit
FR-9 | As a user, I do not end up with duplicate   accounts for the same email | Must | See section 7 (account linking)
FR-10 | As a user, I stay logged in for a   sensible time on my device | Should | Given I log in, then my session lasts [X]   days of activity, or until I log out
FR-11 | As a user, I get clear errors and loading   states | Should | Given a failure (network, provider   error), then I see a friendly message and can retry
FR-12 | As an invited user, I am added to the   organisation after I sign up or log in | Should | Given I follow an invitation link and   complete sign-up or login with the invited email, then I join the   organisation
FR-13 | As a new user, I must provide all mandatory sign-up fields before my account is created | Must | Given I submit the sign-up form, when a mandatory field is missing or invalid, then I see an inline error, the account is not created and no OTP can be requested; password and full legal name are required for email/password sign-ups only
FR-14 | As an organisation user, I must provide the organisation name, the admin's full name and the company's legal registered address | Must | Given I chose Organisation, when the organisation (company) name, the admin's full name or the legal registered address of the company is missing or invalid, then I see an inline error and the account is not created
FR-15 | As the application owner, our backend team can verify and activate an account (Personal or Organisation) | Should | Given an account is inactive, when the backend team verifies it (for example after meeting the customer), then the account becomes active without the online OTP verification and the user continues to onboarding (FEAT-001)

<img width="900" height="509" alt="image" src="https://github.com/user-attachments/assets/13153b22-8201-4bcc-a99c-46e4ff0fa28a" />

invited user · 1 decision
An invited user joins the organisation after completing sign-up or login with the invited email (FR-12).


<h3><span lang=EN-US>6.1 Mandatory sign-up fields<o:p></o:p></span></h3>

<p class=MsoNormal><span lang=EN-US>The fields below are mandatory regardless of account type or role. All of them must be provided when the account is created, and OTP verification can be requested only after that. Verification can then be done at any time, but the account stays inactive until the phone number is verified and, for email/password sign-ups, the email is verified too. For Google sign-ups, the name and email are prefilled from the Google account and the Google token replaces the password; password and full legal name are required for email/password sign-ups only. Role selection is not a mandatory sign-up field. If the user chooses Organisation, the organisation (company) name is also mandatory, the name field is the full name of the admin, and the address is the legal registered address of the company.<o:p></o:p></span></p>

<!--EndFragment-->
</body>

</html>
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:w="urn:schemas-microsoft-com:office:word"
xmlns:m="http://schemas.microsoft.com/office/2004/12/omml"
xmlns="http://www.w3.org/TR/REC-html40">

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->


Field | Data    type | Purpose    and validation rules | Why    it is mandatory
-- | -- | -- | --
Full legal name | Text (string) | First and last name, matching the user's government ID (email/password sign-ups only; prefilled from Google for Google sign-ups). For Organisation sign-ups this is the full name of the admin. | Legal contracts, tax records and fraud   prevention
Organisation / company name | Text (string) | Organisation sign-ups only. The name of the organisation or company the domain is created for | Identifies the company the domain is created for
Email address | Email (string) | Email/password sign-ups: verified with a   6-digit OTP sent to the email address (Google sign-ups are already verified   by Google) | Account identification, transactional   alerts and password recovery
Phone number | Numeric, E.164 format | Collected when the account is created and verified with a 6-digit SMS OTP, which can be requested at any time after the account is created (all sign-up methods) | Real-time booking updates, emergency   contact and multi-factor authentication (MFA)
Account password | String (encrypted) | Minimum 8 characters, with 1 uppercase   letter, 1 symbol and 1 number (email/password sign-ups only; Google sign-ups use the OAuth provider token instead) | Secures the account against unauthorized   access
Country of residence | Enum / dropdown | ISO country code | Determines local tax rules (VAT/GST),   currency defaults and the legal Terms of Service
Address | Text (structured) | Street name, house number, pincode, city and country; the country is the Country of residence selected from the dropdown. For Organisation sign-ups this is the legal registered address of the company. [pincode format per country to be confirmed] | Legal and tax records, billing and   location-based features [reason to be confirmed]
Terms and privacy consent | Boolean | Explicit checkbox consent, stored with a   timestamp | Establishes the legally binding platform   agreement and data-usage consent

<!--EndFragment-->
</body>

</html>

the above fields are required regardless of the user type, then the user can decide the role by landing on either host / customer page and fill relevant fields there to use the functionalities.

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

Field | Data    type | Purpose    and validation rules | Why    it is mandatory
-- | -- | -- | --
User role selection | Enum | Host / Customer / Both (not mandatory at sign-up) | Not mandatory. Chosen later by landing on the Host or Customer page; routes the user to the correct initial onboarding flow (listing creation vs. browsing)
<!--EndFragment-->
</body> 

**How this applies to each sign-up method**
* **Email and password**: the user completes all mandatory fields (full legal name, email, password, phone number, address including country, and consent) and the account is created as inactive. The user then verifies the email with a 6-digit OTP and the phone number with a 6-digit SMS OTP.
* **Google**: name and email are prefilled and the OAuth token replaces the password. The email counts as verified because Google has already verified it, so there is no email OTP. The user adds the phone number, address (including country) and consent, and the account is created as inactive. The user then verifies the phone number with a 6-digit SMS OTP.
* **Organisation**: in addition to the fields above, the user provides the organisation (company) name. The name is the full name of the admin, and the address is the legal registered address of the company.
* **OTPs at any time**: OTPs can be requested and verified at any point after the account is created with all mandatory fields, not only right after it. OTPs cannot be requested before that. Completing them is mandatory.
* **Two types of verification**: *online verification* is done by the user with the phone SMS OTP (all sign-ups) and the email OTP (email/password sign-ups). *Backend verification* is done by our backend team, who verify the account and activate it, for example when we meet the customer, to speed up the process. It is an additional way to activate any account (Personal or Organisation) and does not replace the online OTPs; the account is activated by one way or the other.
* **OTP limits**: an OTP is valid for 10 minutes and allows a maximum of 3 wrong attempts per code. A user must wait 1 minute between resends and can request up to 3 resends per day, counted across email and SMS together.
* **Account status**: a new account starts as inactive. It becomes active only when every required verification is done: phone number for all sign-ups, plus email for email/password sign-ups. If either is missing, the account stays inactive. Any account can also be verified and activated by our backend team, as an additional way to the online verification.
* **Inactive users:** an inactive user can see only the home page of the application, with a message to verify the account in order to start using it.
* **Verified tick:** once the email or the phone number is verified, a verified tick appears next to it on the user profile.
* **Changing email or phone:** a changed email or phone number must always be verified again. While the new value waits for verification, the account stays inactive and the verified tick disappears until it is verified.
* **Clean-up:** an inactive account can be deleted after 3 months, counted from the last login. The user gets a warning email 10 days before deletion and another 5 days before deletion if no action has been taken, and a final email after the account is deleted.

<img width="900" height="639" alt="image" src="https://github.com/user-attachments/assets/7715aa5f-ed5f-4de6-b40d-2a4047b2c27b" />

account status and clean-up · 2 states, 4 steps
An account turns inactive again when an email or phone number changes, until the new value is verified. Inactive accounts follow the clean-up sequence, counted from the last login.

Points to confirm with the team
1.	MFA: phone verification is used to activate the account. MFA is out of scope for this version, so decide whether the phone number is later used as a second login factor.
2.	Phone rules: supported countries, SMS cost, whether one number can be used on more than one account, and whether the user can change the number if verification fails.
3.	Legal name: it must match a government ID. Decide whether the ID is checked (identity verification) or the name is self-declared at sign-up.
4.	Role vs. account type: decided. The Host / Customer role is the type of user and is separate from the account type (Personal / Organisation) in FEAT-001 (see section 3). The role is chosen after activation by landing on the Host or Customer page.
5.	Consent record: store the timestamp and the version of the Terms and Privacy Policy that was accepted.
6.	Country changes: can the country of residence be changed later, given it sets tax rules and currency?
7.	Address: the fields are street name, house number, pincode, city and country; confirm the pincode format per country, whether it is a residential or billing address, whether it is checked for validity, and whether it can be changed later.

<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:w="urn:schemas-microsoft-com:office:word"
xmlns:m="http://schemas.microsoft.com/office/2004/12/omml"
xmlns="http://www.w3.org/TR/REC-html40">
<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>7. Account Linking Rules<o:p></o:p></span></h2>

<p class=MsoNormal><span lang=EN-US>The same person may try both methods with
the same email. Proposed rules (to be confirmed):<o:p></o:p></span></p>


Situation | Expected    behavior
-- | --
User signed up with email/password, later   clicks Continue with Google using the same email | Log them into the same account and link   Google to it (Google verifies the email)
User signed up with Google, later tries   email/password sign-up with the same email | Do not create a second account; tell them   an account exists and to log in with Google, or offer to set a password
User signed up with Google and uses   Forgot password | Send a reset link that lets them add a   password to the same account
Google account email differs from the   email they used before | Treated as a different account (no   automatic linking)



<!--EndFragment-->
</body>

<img width="900" height="581" alt="image" src="https://github.com/user-attachments/assets/1a58a6fd-80c3-4ed9-b76f-fea2097eb7da" />
account linking · 4 situations

</html>

<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:w="urn:schemas-microsoft-com:office:word"
xmlns:m="http://schemas.microsoft.com/office/2004/12/omml"
xmlns="http://www.w3.org/TR/REC-html40">

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>8. Security and Non-Functional Requirements<o:p></o:p></span></h2>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Passwords:</span></b><span
lang=EN-US> stored only as salted hashes (e.g. bcrypt or argon2); never logged
or shown.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Password rules:</span></b><span
lang=EN-US> minimum 8 characters with at least 1 uppercase letter, 1 number and
1 symbol (see section 6.1); not required for Google sign-ups, which use the
OAuth provider token.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Reset links and OTPs:</span></b><span
lang=EN-US> reset links are single-use, random and expire after [1] hour; email
and SMS OTPs are 6-digit codes, single-use, expire after 10 minutes, allow 3
wrong attempts per code, require a 1-minute wait between resends, and are
limited to 3 resends per day across email and SMS together.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Brute-force protection:</span></b><span
lang=EN-US> rate limit login attempts and lock or slow down after [X] failed
attempts.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Transport:</span></b><span
lang=EN-US> all authentication traffic over HTTPS; secure, HTTP-only session
cookies.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Google sign-in:</span></b><span
lang=EN-US> request only basic profile and email permissions; validate tokens
on the server.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Privacy:</span></b><span
lang=EN-US> do not reveal whether an email is registered (except where required
for sign-up, handled carefully).<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Performance:</span></b><span
lang=EN-US> login responds in under [2] seconds for 95% of requests.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Accessibility:</span></b><span
lang=EN-US> forms usable with keyboard and screen readers; error messages
linked to fields.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Compatibility:</span></b><span
lang=EN-US> latest two versions of Chrome, Safari, Firefox, Edge; responsive on
mobile.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Audit and monitoring:</span></b><span
lang=EN-US> log sign-ups, logins, failures and password resets (without
sensitive data) and alert on unusual spikes.<o:p></o:p></span></p>

<h2><span lang=EN-US>9. UI Notes<o:p></o:p></span></h2>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>One page can serve both sign-up
and login, with a clear toggle.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><b><span lang=EN-US>Continue with Google</span></b><span
lang=EN-US> button shown prominently, followed by an &quot;or&quot; divider and
the email/password form.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Show/hide password toggle and
live password-rule hints.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Sign-up form shows all mandatory fields (password and full legal name only for email/password); with Google, the name and email are prefilled and the user completes the remaining fields before the account is created.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Links: Forgot password, Terms
of Service and Privacy Policy (consent text at sign-up).<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Wireframes: [link]<o:p></o:p></span></p>

<h2><span lang=EN-US>10. Edge Cases and Error Handling<o:p></o:p></span></h2>


Scenario | Expected    behavior
-- | --
Invalid email format | Inline error, no submission
Mandatory field missing or invalid (including phone number or address) | Inline error on the field; the account is not created and no OTP can be requested
Organisation details missing (company name, admin full name or legal registered address) | Inline error on the field; the account is not created
Backend team verifies an account before the user completes the OTPs | The account becomes active and the online OTPs are no longer required
Terms and privacy consent not accepted | Sign-up cannot be completed
Email already registered (sign-up) | Message that an account exists, with a   link to log in
Wrong password | Generic "incorrect email or   password"; count toward rate limit
Inactive account (email or phone not   verified) tries to log in | Prompt to verify, with a Resend OTP   option (1-minute wait between resends, 3 resends per day)
Expired, wrong or already-used OTP (email   or SMS) | Explain and offer to send a new one
Expired or used reset link | Explain and offer to request a new reset
User cancels or closes the Google popup | Return to the login page without an error   loop
Google returns an error or is unavailable | Friendly message and the option to use   email/password
Google account has no verified email | Block sign-up and explain why
Too many failed attempts | Temporary lockout or delay with a clear   message
Session expired while using the app | Redirect to login and return the user to   where they were
Network failure during submit | Show a retry option and keep entered data   (except the password)



<!--EndFragment-->
</body>

</html>


<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>11. Analytics Events<o:p></o:p></span></h2>


Event | When
-- | --
signup_started (method) | User begins sign-up with Google or email
signup_completed (method) | Account created
email_verified | Email OTP verified
login_succeeded (method) | Successful login
login_failed (method, reason) | Failed login
password_reset_requested / completed | Reset flow steps
phone_verified | Phone SMS OTP verified



<!--EndFragment-->
</body>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>12. Success Metrics<o:p></o:p></span></h2>


Metric | Target
-- | --
Sign-up completion rate (started to   account created) | [X]%
Share of new accounts that become active   (all required verifications done) | [X]%
Login success rate on first attempt | [X]%
Password reset requests per 100 active   users | Under [X]
Share of sign-ups using Google vs email | Tracked, no target



<!--EndFragment-->
</body>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>13. Dependencies and Risks<o:p></o:p></span></h2>


Item | Type | Impact | Mitigation
-- | -- | -- | --
Google OAuth app configuration and   approval | Dependency | Sign-in cannot launch without it | Set up and verify the app early
Email delivery service | Dependency | Verification and reset emails may be   delayed or land in spam | Use a reliable provider; configure SPF,   DKIM and DMARC
Duplicate accounts from mixed methods | Risk | Confusion and support load | Implement the linking rules in section 7
Account takeover through weak passwords | Risk | Security incident | Password rules, rate limiting, consider   MFA later
Users blocked if Google is down | Risk | Cannot log in | Email/password remains available
SMS delivery service | Dependency | Phone OTPs may be delayed or fail in some   countries, so accounts cannot be activated | Use a reliable provider; confirm   supported countries; allow resends within the limits



<h2><span lang=EN-US>14. Rollout Plan<o:p></o:p></span></h2>

<p class=MsoListParagraphCxSpFirst style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Release behind a feature flag
to internal users first, then to all users.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>If this replaces an existing
login, migrate existing users without forcing a password change; keep existing
sessions valid where possible.<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpMiddle style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Update help articles and
support scripts (verification, reset, linking).<o:p></o:p></span></p>

<p class=MsoListParagraphCxSpLast style='text-indent:-.25in;mso-list:l0 level1 lfo1'><![if !supportLists]><span
lang=EN-US><span style='mso-list:Ignore'>•<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]><span lang=EN-US>Rollback plan: disable the
feature flag and revert to the previous login.<o:p></o:p></span></p>

<span lang=EN-US style='font-size:11.0pt;line-height:107%;font-family:"Calibri",sans-serif;
mso-fareast-font-family:Calibri;mso-ansi-language:EN-US;mso-fareast-language:
EN-GB;mso-bidi-language:AR-SA'>Set up the scheduled clean-up of inactive
accounts: deletion after 3 months from the last login, with warning emails 10
days and 5 days before and a final email after deletion.</span><!--EndFragment-->
</body>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>15. Open Questions<o:p></o:p></span></h2>


No | Question | Owner | Answer
-- | -- | -- | --
1 | Do we add Microsoft sign-in, and when?   (Suggested: decide using the email-domain data of current users) | Product |  
2 | Decided: minimum 8 characters with 1   uppercase letter, 1 number and 1 symbol. Is a common-password check also   required? | Product / Security |  
3 | Decided: the account is active only after the phone SMS OTP is verified (all sign-ups) and, for email/password sign-ups, the email OTP is verified too. Any account can also be verified and activated by our backend team. Inactive users see only the   home page with a message to verify their account. | Product |  
4 | Confirm account linking rules in section   7 | Product / Tech |  
5 | Session length and "remember   me" behavior? | Tech |  
6 | Do we add MFA for admins or all users?   When? | Security |  
7 | Are there legal or consent requirements   at sign-up (terms, marketing opt-in, region-specific rules)? | Legal |  
8 | What should happen to existing users when   this launches? | Product / Tech |  
9 | Decided: backend verification is an additional way to activate an account (Personal or Organisation) and does not replace the online OTP verification; the account is activated by one way or the other. | Product |

<!--EndFragment-->
</body>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>16. Decision Log<o:p></o:p></span></h2>


Date | Decision | Reason | Decided    by
-- | -- | -- | --
[Date] | Launch with Google and email/password   only | Current available methods | Product
[Date] | An account becomes active only after the   phone number is verified, and for email/password sign-ups also the email   (6-digit OTPs) | Google already verifies its emails, so   the email OTP is only needed for email/password sign-ups | Product
[Date] | Inactive accounts are deleted 3 months   after the last login, with warning emails 10 and 5 days before and a final   email after deletion | Keeps accounts clean while giving users   notice | Product
[Date] | Two user roles: Host (resource owner)   and Customer (resource user); a user can use both and opens the second   pathway later | A Host can also be a Customer and the   other way round | Product
[Date] | Host / Customer applies to the whole   organisation; every organisation has an admin; admin transfer needs   confirmation from the old and new admin (valid 10 minutes) | Every organisation always has an admin | Product
2026-11-11 | All mandatory sign-up fields are provided when the account is created; OTP verification can be requested only after that, and at any time afterwards | Keeps OTPs from being sent for incomplete sign-ups; the account stays inactive until verified | Product
2026-11-11 | Role selection (Host / Customer) is not a mandatory sign-up field and is separate from the account type (Personal / Organisation); password and full legal name are required for email/password sign-ups only | Role is the type of user and is chosen later on the Host or Customer page; Google prefills name and email and replaces the password | Product
2026-11-12 | Two types of verification: online (phone SMS OTP, and email OTP for email/password sign-ups) and backend verification, where our backend team verifies and activates the account when we meet the customer. Backend verification is an additional way to activate any account (Personal or Organisation); the account is activated by one way or the other | Speeds up the activation process | Product
2026-11-12 | Organisation sign-ups also require the organisation (company) name, the admin's full name and the legal registered address of the company | Identifies the company the domain is created for | Product
2026-11-12 | There are two main user types, each with its own wiki page: Customer (books the resources and pays for their usage) and Host. Host type 1 owns the resource, lists it in our application and controls it; Host type 2 provides rental space to assemble our resource, is paid for the space and has no control over the resource (we have full control) | Defines the two user types and the two Host types | Product



<!--EndFragment-->
</body>

<body lang=EN-GB style='tab-interval:.5in;word-wrap:break-word'>
<!--StartFragment-->

<h2><span lang=EN-US>17. Change Log<o:p></o:p></span></h2>


Date | Version | Change | Author
-- | -- | -- | --
[Date] | 0.1 | Initial draft |  
[Date] | 0.2 | Added mandatory sign-up fields, OTP   verification and account activation rules, user types and roles, and account   clean-up |  
2026-11-11 | 0.3 | Aligned the sign-up order with FEAT-001: all mandatory fields before account creation and OTP, Google prefill, and role (type of user) no longer mandatory at sign-up |
2026-11-11 | 0.4 | Added child pages for the Host flow and the Customer flow |
2026-11-12 | 0.5 | Added the Organisation sign-up fields and the two types of verification (online and backend) |
2026-11-12 | 0.6 | Defined the two main user types (Customer and Host) and the two Host types, and updated the Host flow and Customer flow pages |
2026-11-12 | 0.7 | Added a link to the Home page |
2026-11-12 | 0.8 | Added sample UI workflows for sign-up and for verifying and activating the account |
2026-11-12 | 0.9 | Updated the link to the renamed User Home Page |
2026-11-13 | 1.0 | Set the Feature ID to the Jira feature IA-4 and added section 18 with the related Jira stories and tasks |
2026-11-16 | 1.1 | Mapped the current signed-in app surfaces to the Host type 1, Host type 2, Customer/campaign publisher and User Home Page wiki/Jira references while preserving the existing future requirements |



<p class=MsoNormal><span lang=EN-US><o:p>&nbsp;</o:p></span></p>

<!--EndFragment-->
</body>

## 18. Jira Stories and Tasks

Jira feature: [IA-4](https://insta-ad.atlassian.net/browse/IA-4) Sign-up and Login, in workstream [IA-1](https://insta-ad.atlassian.net/browse/IA-1) Accounts, Identity and Onboarding.

In Jira, stories and tasks sit under the workstream and are linked to this feature with a "relates to" link and the label `feat-sign-up-login`. Each story has sub-tasks (Backend / API, Frontend / UI, Tests and acceptance).

### 18.1 Stories

Jira | Story | Requirements | Sub-tasks
-- | -- | -- | --
[IA-5](https://insta-ad.atlassian.net/browse/IA-5) | Sign-up with Google | FR-1, section 5.1 | IA-21 to IA-23
[IA-6](https://insta-ad.atlassian.net/browse/IA-6) | Sign-up with email and password | FR-2, FR-8, section 5.2 | IA-24 to IA-26
[IA-7](https://insta-ad.atlassian.net/browse/IA-7) | Mandatory sign-up fields, validation and consent (Personal and Organisation) | FR-13, FR-14, section 6.1 | IA-27 to IA-29
[IA-8](https://insta-ad.atlassian.net/browse/IA-8) | Email and SMS OTP verification | FR-3 | IA-30 to IA-32
[IA-9](https://insta-ad.atlassian.net/browse/IA-9) | Account status, activation rules and inactive-user restrictions | FR-3, section 6.1 | IA-33 to IA-35
[IA-10](https://insta-ad.atlassian.net/browse/IA-10) | Backend team verification and activation of accounts | FR-15 | IA-36 to IA-38
[IA-11](https://insta-ad.atlassian.net/browse/IA-11) | Login with email and password (including brute-force protection) | FR-5, section 5.3 | IA-39 to IA-41
[IA-12](https://insta-ad.atlassian.net/browse/IA-12) | Login with Google | FR-4, section 5.3 | IA-42 to IA-44
[IA-13](https://insta-ad.atlassian.net/browse/IA-13) | Forgot and reset password | FR-6, section 5.4 | IA-45 to IA-47
[IA-14](https://insta-ad.atlassian.net/browse/IA-14) | Logout and session handling | FR-7, FR-10, section 5.5 | IA-48 to IA-50
[IA-15](https://insta-ad.atlassian.net/browse/IA-15) | Account linking and duplicate-account prevention | FR-9, section 7 | IA-51 to IA-53
[IA-16](https://insta-ad.atlassian.net/browse/IA-16) | Account type selection and onboarding handoff (Personal / Organisation) | Section 5 (Path A and Path B), FEAT-001 | IA-54 to IA-56
[IA-17](https://insta-ad.atlassian.net/browse/IA-17) | Invited user joins an organisation after sign-up or login | FR-12 | IA-57 to IA-59
[IA-18](https://insta-ad.atlassian.net/browse/IA-18) | Scheduled clean-up of inactive accounts | Section 6.1 (Clean-up), section 14 | IA-60 to IA-61
[IA-19](https://insta-ad.atlassian.net/browse/IA-19) | Security, audit logging and analytics events for sign-up and login | Sections 8, 11, 12 | IA-62 to IA-63
[IA-20](https://insta-ad.atlassian.net/browse/IA-20) | Sign-up and login UI, error handling and accessibility | FR-11, sections 9, 10 | IA-64 to IA-66

### 18.2 Tasks

Jira | Task | Why | Sub-tasks
-- | -- | -- | --
[IA-67](https://insta-ad.atlassian.net/browse/IA-67) | Set up the Google OAuth app and consent screen | Dependency: Google OAuth app configuration (section 13) | IA-68 to IA-69
[IA-70](https://insta-ad.atlassian.net/browse/IA-70) | Set up email delivery (SPF, DKIM, DMARC) | Dependency: email delivery service (section 13) | IA-71 to IA-72
[IA-73](https://insta-ad.atlassian.net/browse/IA-73) | Integrate the SMS provider and confirm supported countries | Dependency: SMS delivery service (section 13), open question on phone rules | IA-74 to IA-75
[IA-76](https://insta-ad.atlassian.net/browse/IA-76) | Design the auth data model and database schema | Accounts, identities, OTPs, sessions and consent records | IA-77 to IA-78
[IA-79](https://insta-ad.atlassian.net/browse/IA-79) | Implement rate limiting and lockout infrastructure | Brute-force protection (section 8) | IA-80 to IA-81
[IA-82](https://insta-ad.atlassian.net/browse/IA-82) | Plan rollout: feature flag, existing-user migration and support scripts | Rollout plan (section 14) | IA-83 to IA-84

### 18.3 Related Jira features

Jira | Feature | Wiki page
-- | -- | --
[IA-85](https://insta-ad.atlassian.net/browse/IA-85) | User Home Page | [Feature - User Home Page](https://github.com/InstaAd/Engineering-Wiki/wiki/Feature-%E2%80%90-User-Home-Page)
[IA-108](https://insta-ad.atlassian.net/browse/IA-108) | Organisations, Teams and Workspaces | [Feature - User Home Page](https://github.com/InstaAd/Engineering-Wiki/wiki/Feature-%E2%80%90-User-Home-Page) (sections 5 and 6)
[IA-140](https://insta-ad.atlassian.net/browse/IA-140) | Customer Pathway and Onboarding | [Customer flow](https://github.com/InstaAd/Engineering-Wiki/wiki/User-Account-Customer-Flow)
[IA-177](https://insta-ad.atlassian.net/browse/IA-177) | Host Pathway and Host Types | [Host flow](https://github.com/InstaAd/Engineering-Wiki/wiki/User-Account-Host-Flow)
[IA-449](https://insta-ad.atlassian.net/browse/IA-449) | Host Onboarding and Verification (mandatory Host details, verification, activation) | [Host flow](https://github.com/InstaAd/Engineering-Wiki/wiki/User-Account-Host-Flow) (sections 4 to 11)
