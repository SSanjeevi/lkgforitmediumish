---
toc: true
layout: post
description: 
author: Sanjeevi Subramani
categories: [Azure AD, Azure]
title: Azure AD B2C setup for API Management Developer portal
---
solution for issue in setting up AD B2C for developer portal

For setting up Azure AD B2C setup for the new API Management Developer portal follow this tutorial:
[**Authorize developer accounts by using Azure Active Directory B2C - Azure API Management**
*Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications. You…*docs.microsoft.com](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-aad-b2c)

Steps has described in this link:

 1. Under **Identities**. Click **+Add** at the top

 2. The **Add identity provider** pane appears on the right. Choose **Azure Active Directory B2C**.

 3. Copy the **Redirect URL**.

 4. In a new tab, access your Azure Active Directory B2C tenant in the Azure portal and open the **Applications** blade.

 5. Click the **Add** button to create a new Azure Active Directory B2C application.

 6. In the **New application** blade, enter a name for the application. Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**. Then paste the **Redirect URL** copied in step 3 into the **Reply URL** text box.

 7. If you’re using the new developer portal (not the legacy developer portal), include the **Given Name**, **Surname**, and **User’s Object ID** in the application claims.

 8. Click the **Create** button. When the application is created, it appears in the **Applications** blade. Click the application name to see its details.

 9. From the **Properties** blade, copy the **Application ID** to the clipboard.

 10. Switch back to the API Management **Add identity provider** pane and paste the ID into the **Client Id** text box.

 11. Switch back to the API Management **Add identity provider** pane and paste the key into the **Client Secret** text box.

 12. Specify the domain name of the Azure Active Directory B2C tenant in **Signin tenant**.

 13. The **Authority** field let you control the Azure AD B2C login URL to use. Set the value to **<your_b2c_tenant_name>.b2clogin.com**.

 14. Specify the **Signup Policy** and **Signin Policy** from the B2C Tenant policies. Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.

 15. After you’ve specified the desired configuration, click **Save**.

 16. After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.

 17. In the developer portal, sign-in with AAD B2C is possible with the **Sign-in button: OAuth** widget. The widget is already included on the sign-in page of the default developer portal content.

 18. Although a new account will be automatically created whenever a new user signs in with AAD B2C, you may consider adding the same widget to the sign-up page.

 19. The **Sign-up form: OAuth** widget represents a form used for signing up with OAuth.

 20. Re-publish the app in developer portal

All the Above where fine as per the document, but it didn’t worked for me and got **401 un-authorized** and **403 forbidden** error on signup or sign in using the B2C login in developer portal.

Later seeing this GitHub issue discussion am able to solve it:
[**OAuth SignUp 403 response (when using Identity Experience Framework) · Issue #443 ·…**
*Dismiss GitHub is home to over 50 million developers working together to host and review code, manage projects, and…*github.com](https://github.com/Azure/api-management-developer-portal/issues/443)

They are saying: Sign in works fine, but on the complete sign up page I see the error message Server error. Unable to send request. Please try again later.

caused by a HTTP 403 response to [https://my-api-name.management.azure-api.net/subscriptions/xxx/resourceGroups/xxx/providers/Microsoft.ApiManagement/service/xxx/users?api-version=2018-06-01-preview](https://my-api-name.management.azure-api.net/subscriptions/xxx/resourceGroups/xxx/providers/Microsoft.ApiManagement/service/xxx/users?api-version=2018-06-01-preview)

If used **User Flows** in **B2C**:

Here they suggested to enable **User’s Object ID** into AAD application claims.

I have used **Identity Experience Framework** to display a custom login page and inject extra claims for this we have to add the following:

Following this [guide](https://docs.microsoft.com/en-gb/azure/active-directory-b2c/custom-policy-get-started) add below:

<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>

and

<SubjectNamingInfo ClaimType="sub" />

the **Main thing **missed is adding the below one:
>  <OutputClaim ClaimTypeReferenceId=”objectId” PartnerClaimType=”oid”/>

After adding the above one in the claim am able to login and signup successfully using **Azure AD B2C** in the new **API Management Developer portal**.
