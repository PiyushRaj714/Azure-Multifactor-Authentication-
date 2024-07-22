# 1.Configure & manage Azure Multifactor Authentication (MFA) 

![image](https://github.com/user-attachments/assets/b0d5e3a2-569f-4040-90da-3970b2d70c60)

# 2.Two Factor authentication

Two-factor authentication (2FA) requires two forms of verification: something you know (password) and something you have (phone, hardware token, etc.).

# 3. Different methods of the two factor authentication
# Phone call settings
If users receive phone calls for MFA prompts, you can configure their experience, such as caller ID or the voice greeting they hear. In the INDIA, if you haven't configured MFA caller ID, voice calls from Microsoft come from the following numbers. Users with spam filters should exclude these numbers.
Default number: +91 855-330-8653
To configure your own caller ID number, complete the following steps:
1.	Go to Protection > Multifactor authentication > Phone call settings.
2.	Set the MFA caller ID number to the number you want users to see on their phones. Only US-based numbers are allowed.
3.	Select Save.
# Set up a SMS
To use your own custom messages, complete the following steps:
1.	Go to Protection > Multifactor authentication > Phone call settings.
2.	Select Add greeting.
3.	Choose the Type of greeting, such as Greeting (standard) or Authentication successful.
4.	Select the Language. See the previous section on custom messages.
5.	Browse for and select an .mp3 or .wav sound file to upload.
6.	Select Add and then Save.

# 4.	Setup self-service password reset
![Screenshot 2024-07-22 235316](https://github.com/user-attachments/assets/6e5e3569-95f2-415d-8ade-41b146dd7aa3)

# 5. Configure MFA
1.	Sign in to the Microsoft Entra admin center 
2.	Browse to Identity > Overview > Properties.
3.	Select Manage security defaults.
4.	Set Security defaults to Enabled.
5.	Select Save.
Ensure that MFA is configured correctly by checking the settings in Azure Active Directory under the "Security" section.

# 6.Configure and deploy self-service password reset 
![Screenshot 2024-07-22 235316](https://github.com/user-attachments/assets/3edb9437-deda-4c62-96fb-fa35bfef4798)

Deploy SSPR by ensuring users are aware of the feature and how to use it. Provide training materials or links to Microsoft's documentation.

# 7. Implement and manage Azure MFA settings 
# Fraud alerting
The Fraud alert feature lets users report fraudulent attempts to access their resources. When an unknown and suspicious MFA prompt is received, users can report the fraud attempt by using the Microsoft Authenticator app or through their phone.
Microsoft recommends using Report suspicious activity instead of Fraud alert due to its integration with Identity Protection for risk-driven remediation, better reporting capabilities, and least-privileged administration.
The following fraud alert configuration options are available:
•	Automatically block users who report fraud. If a user reports fraud, the Microsoft Entra multifactor authentication attempts for the user account are blocked for 90 days or until an administrator unblocks the account. An administrator can review sign-ins by using the sign-in report, and take appropriate action to prevent future fraud. An administrator can then unblock the user's account.
•	Code to report fraud during initial greeting. When users receive a phone call to perform multifactor authentication, they normally press # to confirm their sign-in. To report fraud, the user enters a code before pressing #. This code is 0 by default, but you can customize it. If automatic blocking is enabled, after the user presses 0# to report fraud, they need to press 1 to confirm the account blocking.
 # Trusted IPs
Location conditions are the recommended way to configure MFA with Conditional Access because of IPv6 support and other improvements. For more information about location conditions, see Using the location condition in a Conditional Access policy. For steps to define locations and create a Conditional Access policy, see Conditional Access: Block access by location.
The trusted IPs feature of Microsoft Entra multifactor authentication also bypasses MFA prompts for users who sign in from a defined IP address range. You can set trusted IP ranges for your on-premises environments. When users are in one of these locations, there's no Microsoft Entra multifactor authentication prompt. The trusted IPs feature requires Microsoft Entra ID P1 edition.
# Enable remember multifactor authentication
To enable and configure the option to allow users to remember their MFA status and bypass prompts, complete the following steps:
Sign in to the Microsoft Entra admin center as at least an Authentication Policy Administrator.
Browse to Identity > Users.
Select Per-user MFA.
Under Multifactor authentication at the top of the page, select service settings.
On the service settings page, under remember multifactor authentication, select Allow users to remember multifactor authentication on devices they trust.
Set the number of days to allow trusted devices to bypass multifactor authentications. For the optimal user experience, extend the duration to 90 or more days.
Select Save.
# Mark a device as trusted
After you enable the remember multifactor authentication feature, users can mark a device as trusted when they sign in by selecting Don't ask again.

# 8. Account Lockout
To configure account lockout settings, complete these steps:

1)Sign in to the Microsoft Entra admin center as at least an Authentication Policy Administrator.
2)Browse to Protection > Multifactor authentication > Account lockout. You might need to click Show more to see Multifactor authentication.
3)Enter the values for your environment, and then select Save.

# 9.Manage MFA settings for users
![image](https://github.com/user-attachments/assets/0b603bde-968c-46b7-ac57-d88a5f85f7c1)

To add authentication methods for a user in the Microsoft Entra admin center:
Sign in to the Microsoft Entra admin center as at least an Authentication Administrator.
Browse to Identity > Users > All users.
Choose the user for whom you wish to add an authentication method and select Authentication methods.
At the top of the window, select + Add authentication method.
Select a method (phone number or email). Email may be used for self-password reset but not authentication. When adding a phone number, select a phone type and enter phone number with valid format (such as +1 4255551234).
Select Add.

# 10. Extend Azure AD MFA to third party and on-premises devices
To extend Azure AD MFA to third-party applications and on-premises devices, use Azure AD Application Proxy or integrate with an on-premises MFA server.

# 11.Monitor Azure AD MFA activity 
Sign in to the Azure portal.
In the left-hand menu, select "Azure Active Directory" and then select "Audit logs" under "Monitoring."
On the "Audit logs" page, you can use the filters to specify the time range and other parameters for the logs you want to view.
In the "Activity" dropdown menu, select "User Management." This will show you all the user management activities, including when a user enabled MFA.
Look for an entry with the activity "Enable MFA for a user." The "Time" column will show you the date and time when the MFA was enabled.

# 12.OAuth Tokens
Microsoft Entra ID supports the use of OATH TOTP SHA-1 tokens that refresh codes every 30 or 60 seconds.
OATH TOTP hardware tokens typically come with a secret key, or seed, pre-programmed in the token. You need to input these keys into Microsoft Entra ID as described in the following steps. Secret keys are limited to 128 characters, which might not be compatible with all tokens. The secret key can contain only the characters a-z or A-Z and digits 1-7. It must be encoded in Base32.
Programmable OATH TOTP hardware tokens that can be reseeded can also be set up with Microsoft Entra ID in the software token setup flow.
OATH hardware tokens are supported as part of a public preview.

# After you acquire tokens, you need to upload them in a comma-separated values (CSV) file format. Include the UPN, serial number, secret key, time interval, manufacturer, and model.

Sign in to the Microsoft Entra admin center as a Global Administrator, go to Protection > Multifactor authentication > OATH tokens, and upload the CSV file.

Depending on the size of the CSV file, it might take a few minutes to process. Select Refresh to get the status. If there are any errors in the file, you can download a CSV file that lists them. The field names in the downloaded CSV file are different from those in the uploaded version.

After any errors are addressed, the administrator can activate each key by selecting Activate for the token and entering the OTP displayed in the token.

Users can have a combination of up to five OATH hardware tokens or authenticator applications, such as the Microsoft Authenticator app, configured for use at any time.
