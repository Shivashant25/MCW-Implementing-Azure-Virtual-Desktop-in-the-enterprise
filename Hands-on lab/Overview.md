# Implementing Azure Virtual Desktop for the enterprise hands-on lab step-by-step

## Abstract and learning objectives

In this hands-on lab, you will implement an Azure Virtual Desktop (formerly Windows Virtual Desktop) Infrastructure and learn how-to setup a working AVD environment end-to-end in a typical Enterprise model. At the end of the lab, attendees will have deployed an Azure Active Directory Tenant with Azure AD Connect to an Active Directory Domain Controller that is running in Azure. You will also deploy the Azure infrastructure for the Azure Virtual Desktop Tenant(s), Host Pool(s) and session host(s), and connect to an AVD session utilizing different supported devices and browsers. You will publish desktops and remote apps, and configure user profiles and file shares with FSLogix.  Finally, you will configure monitoring and security for the Azure Virtual Desktop infrastructure and understand the steps to manage the gold images.

## Overview

In this lab, attendees will deploy the [Azure Virtual Desktop (AVD)](https://azure.microsoft.com/en-us/services/virtual-desktop/) solution. Exclusively available as an Azure cloud service, Azure Virtual Desktop allows you to choose a flexible end user virtualized application or desktop delivery model that best aligns with your enterprise Azure cloud strategy. AVD simplifies the IT model to virtualize and deploy modern and legacy desktop app experiences with unified management without needing to host, install, configure, and manage components such as diagnostics, networking, connection brokering, and gateway. AVD brings together Microsoft Office 365 and Azure to provide users with the only multi-session Windows 10 experience with exceptional scale and reduced IT costs while empowering today's modern digital workspace.

## Solution architecture

![This is the Solution architecture diagram as described in the text below.](images/avdsolutiondiagramv2.png "Solution architecture") 

This diagram shows an Azure Virtual Desktop architecture with on-premises servers for Active Directory.  In the diagram, the host pools are providing the AVD session to the different supported devices. Azure Monitor, Network Watcher, and Log Analytics are monitoring and logging activity and performance metrics.

## Requirements

Before you start setting up your Azure Virtual Desktop workspace, make sure you have the following items:

-   The Azure Active Directory tenant ID for Azure Virtual Desktop users.

-   A global administrator account within the Azure Active Directory tenant.

    -   This also applies to Cloud Solution Provider (CSP) organizations that are creating an Azure Virtual Desktop workspace for their customers. When you are in a CSP organization, you must be able to sign in as global administrator of the customer\'s Azure Active Directory tenant.

    -   The administrator account must be sourced from the Azure Active Directory tenant in which you are trying to create the Azure Virtual Desktop workspace. This process does not support Azure Active Directory B2B (guest) accounts.

    -   The administrator account must be a work or school account.

-   An Azure subscription.

    -   Enough Quota Cores to build four 4-core servers.

    -   Access to the Azure Active Directory Global Admin account for your new or existing Azure Active Directory Tenant.

    -   Owner rights on all Azure subscription(s).

## Before the hands-on lab

-   Refer to the Before the hands-on lab setup guide before continuing to the lab exercises.
  
-   Make sure to keep track of what user accounts you are using and where you are using them.

-   Regions and locations, make sure to stay consistent as much as possible.

## Troubleshooting

When you run into issues with your Azure Virtual Desktop (AVD) environment, there will periodically be troubleshooting tips at the end of the current exercise.  If the issues are not directly addressed, please feel free to reach out to your instructor or teacher.

Review the article, [Troubleshooting overview, feedback, and support for Azure Virtual Desktop](https://docs.microsoft.com/en-us/azure/virtual-desktop/troubleshoot-set-up-overview). Part of the article will cover steps used in [Exercise 8](#exercise-8-setup-monitoring-for-avd) and can help diagnose issues you may encounter.

>**Important! Please note**: The change from Windows Virtual Desktop (WVD) to Azure Virtual Desktop (AVD) is recent, and some resources do not yet reflect the change.  As a result, some images may be slightly different.  WVD and AVD are interchangeable, and we will update our documents once the transition is complete.


Click on the **Next** button present in the bottom-right corner of this lab guide.
