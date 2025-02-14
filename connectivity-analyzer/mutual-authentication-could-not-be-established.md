---
title: Mutual Authentication Could Not be Established
author: bradhugh
ms.author: bradhugh
manager: tpolitis
audience: ITPro 
ms.topic: article 
ms.service: remote-connect-tool
ms.localizationpriority: medium
description: 'The Connectivity Analyzer displays the error message "Mutual Authentication could not be established."'
---


# Mutual Authentication Could Not be Established


_**Topic Last Modified:** 2009-09-01_

The Microsoft Remote Connectivity Analyzer negotiates a Secure Sockets Layer (SSL) connection with the remote host to retrieve various properties on X509 certificates. The Microsoft Remote Connectivity Analyzer tool evaluates the Subject attribute to identify the fully qualified domain name (FQDN) or Common Name that was assigned to the certificate (for example, mail.contoso.com).

If the Common Name does not match the Mutual Authentication (msstd:) string entered in the Microsoft Remote Connectivity Analyzer when testing Outlook Anywhere functionality, the Microsoft Remote Connectivity Analyzer displays the following error message.

"Mutual Authentication could not be established."

The Mutual Authentication string equates to the "Only connect to proxy servers that have this principal name in their certificate" setting in Outlook's Exchange Proxy Settings. This error can also occur when the Mutual Authentication string is valid but the CertPrincipalName attribute for the EXPR Outlook Provider stored in Active Directory is not.

Symptoms of this issue include the following:

  - You are repeatedly prompted for credentials and unable to successfully connect to Exchange Server using Outlook Anywhere.

  - You receive the following error message when you allow Outlook 2007 to automatically create the Outlook 2007 profile: "An encrypted connection to your mail server is not available. Click Next to attempt using an unencrypted connection."

<div>

## Resolution

To resolve this error, do the following:

1.  View the Web server certificate installed on the Exchange 2007 Client Access server and confirm the Common Name that the certificate was issued to, (for example, mail.contoso.com).

2.  Open the Exchange Proxy settings in Microsoft Outlook and verify that the FQDN entered in the Mutual Authentication Principal Name field is entered correctly (for example, msstd:mail.contoso.com).

3.  If necessary, use the Exchange Management Shell to modify the CertPrincipalName attribute as follows:
    
`Set-OutlookProvider EXPR -CertPrincipalName:"msstd:mail.contoso.com"`


## For More Information

  - To learn more about the Mutual Authentication Principal Name, see [Principal Names](https://go.microsoft.com/fwlink/?linkid=93417).

  - To learn more about Exchange 2007 Outlook Providers, see [The Autodiscover Service and Outlook Providers - how does this stuff work?](https://go.microsoft.com/fwlink/?linkid=161811) and [Set-OutlookProvider](https://go.microsoft.com/fwlink/?linkid=161815).

The Microsoft Remote Connectivity Analyzer has limited documentation at this time. In an effort to improve the documentation for each of the errors you might receive, we would like to solicit additional information from the community. Please use the Community Content section below to post additional reasons why you failed at this point.  If you need technical assistance, please create a post in the appropriate [Exchange TechNet forum](https://go.microsoft.com/fwlink/?linkid=73420) or contact [support](https://go.microsoft.com/fwlink/?linkid=8158).



