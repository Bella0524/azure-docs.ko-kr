---
title: What&quot;s new in Azure Stack | Microsoft Docs
description: What&quot;s new in Azure Stack
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 872b0651-0a92-4d28-b2e6-07d0a4a9a25a
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: helaw
translationtype: Human Translation
ms.sourcegitcommit: c9cc04a692a75bd821fc28a06eb9ef6fb2fbd2b8
ms.openlocfilehash: 56139980e5997c8b08b03ce07c885cd696372a84


---
# <a name="whats-new-in-azure-stack-technical-preview-2"></a>What's new in Azure Stack Technical Preview 2
This release provides new features for both tenants and administrators.

## <a name="network"></a>Network
* [iDNS](azure-stack-understanding-dns-in-tp2.md) provides internal network name registration and Domain Name System (DNS) resolution without additional DNS infrastructure.
* [Virtual network gateways](azure-stack-create-vpn-connection-one-node-tp2.md) provide VPN connectivity options to Azure or on-premises resources.
* User Defined Routes can route network traffic through firewalls, security, other appliances, and other services.
* You can create network resources from the Marketplace.   

## <a name="storage"></a>Storage
* [Azure Queues](https://msdn.microsoft.com/library/dd179353.aspx) enable reliable and persistent service messaging.
* [Storage analytics](https://msdn.microsoft.com/library/azure/hh343270.aspx) capture storage performance data. You can use this data to trace requests, analyze usage trends, and diagnose issues with your storage account.
* Blob storage supports [append block operation](https://msdn.microsoft.com/library/azure/mt427365.aspx).
* Premium Storage API account support.
* Tenant storage service support for common tools and SDKs, such as Azure CLI, PowerShell, .NET, Python, and Java SDK. 
* [Storage Account Shared Access Signature](https://msdn.microsoft.com/library/azure/mt584140.aspx) enable granular delegation of access to your storage services without having to share your full account key.  
* Storage services now use [Group Managed Service Accounts](https://technet.microsoft.com/library/hh831477.aspx) for strong security with low management overhead.
* You can reclaim unused tenant resources on-demand.
* Deleted storage account retention length is configurable.
* You can recover deleted tenant storage accounts.

## <a name="compute"></a>Compute
* You can deallocate virtual machines.
* You can redeploy virtual machine extensions for troubleshooting and configuration management purposes.
* You can resize virtual machine disks.
* Virtual machines can have multiple network interfaces.

## <a name="portal-experience"></a>Portal Experience
* Azure Stack Regions are a logical unit of scale and management within Azure Stack. In this preview, you can view information on services like compute, network, and storage by region.
* You can now preview the [updates](azure-stack-updates.md) interface.

## <a name="key-vault"></a>Key Vault
* [Key Vault in Azure Stack](azure-stack-kv-intro.md) provides secure management of your keys and passwords for cloud apps.
* You can audit and monitor key usage by apps and VMs.

## <a name="billing-and-usage"></a>Billing and usage
* [Billing and consumption APIs](azure-stack-billing-and-chargeback.md) expose data on how your services are consumed.  
* Delegated Providers enable resellers to offer your Azure Stack services to their customers.

## <a name="monitoring-and-health"></a>Monitoring and health
* New monitoring capabilities available in the portal and APIs allow you to proactively view and manage alerts on your environment.  

## <a name="next-steps"></a>Next steps
* [Understand Azure Stack POC Architecture](azure-stack-architecture.md)      
* [Understand deployment prerequisites](azure-stack-deploy.md)
* [Deploy Azure Stack](azure-stack-run-powershell-script.md)




<!--HONumber=Nov16_HO3-->


