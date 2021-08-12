![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Implementing Azure Virtual Desktop in the enterprise
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step guide
</div>

<div class="MCWHeader3">
June 2021
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2021 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.


**Contents**

<!-- TOC -->

- [Implementing Azure Virtual Desktop for the enterprise hands-on lab step-by-step](#implementing-azure-virtual-desktop-for-the-enterprise-hands-on-lab-step-by-step)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
  - [Troubleshooting](#troubleshooting)
  - [Exercise 1: Configuring Azure AD Connect with AD DS](#exercise-1-configuring-azure-ad-connect-with-ad-ds)
    - [Task 1: Connecting to the domain controller](#task-1-connecting-to-the-domain-controller)
    - [Task 2: Disabling IE Enhanced Security](#task-2-disabling-ie-enhanced-security)
    - [Task 3: Creating a domain admin account](#task-3-creating-a-domain-admin-account)
    - [Task 4: Configuring Azure AD Connect](#task-4-configuring-azure-ad-connect)
  - [Exercise 2: Create Azure AD groups for AVD](#exercise-2-create-azure-ad-groups-for-avd)
    - [Task 1: Creating Azure AD groups](#task-1-creating-azure-ad-groups)
    - [Task 2: Assign users to groups](#task-2-assign-users-to-groups)
  - [Exercise 3: Create an Azure Files Share for FSLogix](#exercise-3-create-an-azure-files-share-for-fslogix)
    - [Task 1: Create a storage account](#task-1-create-a-storage-account)
    - [Task 2: Create an Azure file share](#task-2-create-an-azure-file-share)
    - [Task 3: Enable AD authentication for your storage account](#task-3-enable-ad-authentication-for-your-storage-account)
    - [Task 4: Configure share permissions](#task-4-configure-share-permissions)
    - [Task 5: Configure NTFS permissions for the file share](#task-5-configure-ntfs-permissions-for-the-file-share)
    - [Task 6: Configure NTFS permissions for the containers](#task-6-configure-ntfs-permissions-for-the-containers)
  - [Exercise 4: Create a gold image for AVD](#exercise-4-create-a-gold-image-for-avd)
    - [Task 1: Create a new Virtual Machine (VM) in Azure](#task-1-create-a-new-virtual-machine-vm-in-azure)
    - [Task 2: Run Windows Update](#task-2-run-windows-update)
    - [Task 3: Prepare an AVD image](#task-3-prepare-an-avd-image)
    - [Task 4: Run Sysprep](#task-4-run-sysprep)
    - [Task 5: Create a managed image from the gold Image VM](#task-5-create-a-managed-image-from-the-gold-image-vm)
    - [Task 6: Provision a Host Pool with a custom image](#task-6-provision-a-host-pool-with-a-custom-image)
  - [Exercise 5: Create a host pool for personal desktops](#exercise-5-create-a-host-pool-for-personal-desktops)
    - [Task 1: Create a new Host Pool and Workspace](#task-1-create-a-new-host-pool-and-workspace)
    - [Task 2: Create a friendly name for the workspace](#task-2-create-a-friendly-name-for-the-workspace)
    - [Task 3: Assign an Azure AD group to an application group](#task-3-assign-an-azure-ad-group-to-an-application-group)
  - [Exercise 6: Create a host pool and assign pooled remote apps.](#exercise-6-create-a-host-pool-and-assign-pooled-remote-apps)
    - [Task 1: Create a new host pool and workspace](#task-1-create-a-new-host-pool-and-workspace-1)
    - [Task 2: Create a friendly name for the workspace](#task-2-create-a-friendly-name-for-the-workspace-1)
    - [Task 3: Add Remote Apps to your Host Pool](#task-3-add-remote-apps-to-your-host-pool)
  - [Exercise 7: Connect to AVD with the web client](#exercise-7-connect-to-avd-with-the-web-client)
    - [Task 1: Connecting with the HTML5 web client](#task-1-connecting-with-the-html5-web-client)
  - [Exercise 8: Setup monitoring for AVD](#exercise-8-setup-monitoring-for-avd)
    - [Task 1: Create a Log Analytics workspace](#task-1-create-a-log-analytics-workspace)
    - [Task 2: Enabling diagnostic logging for AVD](#task-2-enabling-diagnostic-logging-for-avd)
    - [Task 3: Enable logging for host pools](#task-3-enable-logging-for-host-pools)
    - [Task 4: Enable logging for application groups](#task-4-enable-logging-for-application-groups)
    - [Task 5: Enable logging for workspaces](#task-5-enable-logging-for-workspaces)
    - [Task 6: Enabling Azure Monitor for the session hosts](#task-6-enabling-azure-monitor-for-the-session-hosts)
  - [Exercise 9: Improving your AVD environment](#exercise-9-improving-your-avd-environment)
    - [Task 1: Enabling Autoscale](#task-1-enabling-autoscale)
    - [Task 2: Utilizing Application Packages (MSIX)](#task-2-utilizing-application-packages-msix)
    - [Task 3: Protect AVD with Microsoft Defender for Endpoint](#task-3-protect-avd-with-microsoft-defender-for-endpoint)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete Resource groups to remove lab environment](#task-1-delete-resource-groups-to-remove-lab-environment)

<!-- /TOC -->


Click on the **Next** button present in the bottom-right corner of this lab guide.
