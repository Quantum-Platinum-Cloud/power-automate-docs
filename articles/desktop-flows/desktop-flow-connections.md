---
title: Create desktop flow connections
description: See how to create connections to trigger desktop flows from cloud flows.
author: georgiostrantzas
ms.subservice: desktop-flow
ms.topic: conceptual
ms.date: 03/21/2023
ms.author: pefelesk
ms.reviewer: gtrantzas
contributors:
search.audienceType: 
  - flowmaker
  - enduser
---

# Create desktop flow connections

> [!IMPORTANT]
> Before using a machine to run desktop flows from the cloud, ensure that the machine is secured and the machine's admins are trusted.

Before using the **Run desktop flow** action in your cloud flow to trigger a desktop flow, you need to create a connection to your machine. To create a connection:

1. Sign in to [Power Automate](https://make.powerautomate.com), go to **Data** > **Connections**,  and then select **New connection**.

    :::image type="content" source="media/desktop-flows-setup/new-connection.png" alt-text="Screenshot of the option to create a new connection.":::

1. Search for **Desktop flows**, and then select the appropriate result.

There is two different methods to connect Power Automate with your machines (or groups).

## Connect with username and password

With this option, you need to provide the machine (or on-premises data gateway) information and device credentials:

   - **Connect**: Select if you want to connect to a machine, a machine group or an on-premises data gateway.

      To connect to a machine or a machine group, select **Directly to machine**, and choose the appropriate machine or machine group in  **Machine or machine group**.

      :::image type="content" source="media/desktop-flows-setup/choose-machine.png" alt-text="Screenshot of the Directly to machine option in the Connect field.":::

   - **Domain and Username**: Provide your device account. To use a local account, populate the name of the user (for example, **MACHINENAME\\User** or **local\\User**) or an Active Directory account, such as **DOMAIN\\User**.

   - **Password**: Your account’s password.

      :::image type="content" source="media/desktop-flows-setup/credentials-screen.png" alt-text="Screenshot that shows where to enter the credentials for the connection.":::
      
## Connect with sign-in (preview) for attended runs

With this option, you don't need to provide session credentials. This might be very helpful when your organization doesn't allow username and password for user sessions.

### Pre-requisites

To use connection with sign-in, you need to meet the following pre-requisites:

  - Azure AD users must be in the same tenant as the selected environment in Power Automate portal.
  - The target (machine / group) should be Azure AD or AD joined. In case of a AD joined target, AD must be synchronized with Azure AD (What is Azure AD Connect and Connect Health. - Microsoft Entra | Microsoft Learn).
  - The Azure AD user account must be granted right to open a Windows session on the target machine(s) (interactive logon). At runtime, there should a Windows interaction session matching the connection user in order to process the run (as it is today for existing connections).
  - The tenant of the target Azure AD account is configured to use modern authentication [Authentication with Azure AD - Microsoft Azure Well-Architected Framework](/azure/well-architected/).


### Setup the connection with sign-in

- Select **Connect with Sign-in** in the Connect dropdown
- Select the target (machine or machine group)
- Select **Sign in**
- Pick or provide an **Azure AD account** in the sign in pop up 
- The desktop flow connect is automatically created

### How it works
- An access / refresh token is created during the Azure AD authentication.
- The token scope is limited to executing a desktop flow.
- The Power Platform services manage the refreshment of those tokens.

### Limitations
- Connect with sign-in (preview) works **only for attended runs**. Running unattended with this connection will always fail.
- Queue time duration is limited to one hour.


> [!IMPORTANT]
> If you consistently encounter issues when creating a connection on a new machine, first try to remove it, and then [register it](/power-automate/desktop-flows/manage-machines#register-a-new-machine) again.

[!INCLUDE[footer-include](../includes/footer-banner.md)]
