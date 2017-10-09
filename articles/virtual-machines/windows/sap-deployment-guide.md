---
title: distribuzione di macchine virtuali per SAP in Windows aaaAzure | Documenti Microsoft
description: Informazioni su come toodeploy SAP software nelle macchine virtuali di Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>Distribuire SAP in macchine virtuali Windows in Azure
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Macchine virtuali di Azure è una soluzione di hello per le organizzazioni che necessitano di risorse di calcolo e archiviazione, in tempi minimi senza lunghi cicli di approvvigionamento. È possibile utilizzare applicazioni di toodeploy classiche macchine virtuali di Azure, come le applicazioni basate su SAP NetWeaver, in Azure. È possibile estendere l'affidabilità e la disponibilità di un'applicazione senza risorse locali aggiuntive. Macchine virtuali di Azure supporta la connettività cross-premise e quindi è possibile integrare Macchine virtuali di Azure nei domini locali, nei cloud privati e nel panorama applicativo del sistema SAP dell'organizzazione.

In questo articolo viene illustrata l'hello passaggi toodeploy le applicazioni SAP in macchine virtuali di Windows (VM) in Azure. In questo articolo si basa sulle informazioni hello [macchine virtuali di Azure la pianificazione e implementazione di SAP in Windows][planning-guide]. Inoltre, integra la documentazione di installazione di SAP e note su SAP, che sono le risorse primarie hello per l'installazione e distribuzione del software SAP.

## <a name="prerequisites"></a>Prerequisiti
La configurazione di una macchina virtuale di Azure per la distribuzione del software SAP richiede più passaggi e coinvolge diverse risorse. Prima di iniziare, assicurarsi che siano soddisfatti i prerequisiti hello per l'installazione del software SAP in macchine virtuali Windows in Azure.

### <a name="local-computer"></a>Computer locale
toomanage VM Windows o Linux, è possibile utilizzare script di PowerShell e hello portale di Azure. Per entrambi gli strumenti, è necessario un computer locale che esegue Windows 7 o una versione successiva di Windows. Se si desidera toomanage solo le macchine virtuali Linux e si desidera che un computer Linux toouse per questa attività, è possibile utilizzare l'interfaccia CLI di Azure.

### <a name="internet-connection"></a>Connessione Internet
toodownload e gli strumenti di esecuzione hello e gli script necessari per la distribuzione del software SAP, è necessario essere connessi a Internet toohello. macchina virtuale di Azure che esegue Azure Enhanced Monitoring Extension per SAP hello Hello deve inoltre toohello accesso Internet. Se hello macchina virtuale di Azure fa parte di una rete virtuale di Azure o di un dominio locale, assicurarsi che siano impostate hello le impostazioni proxy, come descritto in [configurare proxy hello][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>iscriversi a Microsoft Azure
È necessario un account Azure attivo.

### <a name="topology-and-networking"></a>Topologia e rete
È necessario toodefine hello topologia e l'architettura di hello distribuzione SAP in Azure:

* Toobe gli account di archiviazione di Azure usata
* Rete virtuale in cui si desidera sistema SAP di hello toodeploy
* Risorse gruppo toowhich si desidera toodeploy hello SAP sistema
* Area di Azure in cui si desidera sistema SAP di hello toodeploy
* Configurazione SAP (due livelli o tre livelli)
* Dimensioni delle macchine Virtuali e il numero di hello di dischi rigidi virtuali (VHD) aggiuntivi toobe montati macchine virtuali toohello
* Configurazione di SAP Correction and Transport System (CTS)

Creare e configurare gli account di archiviazione di Azure o reti virtuali di Azure prima di iniziare un processo di distribuzione del software SAP hello. Per informazioni su come toocreate e configurare queste risorse, vedere [macchine virtuali di Azure la pianificazione e implementazione di SAP in Windows][planning-guide].

### <a name="sap-sizing"></a>Dimensionamento di SAP
Conoscere le seguenti informazioni, per il dimensionamento di SAP hello:

* Prevista del carico di lavoro SAP, ad esempio, utilizzando lo strumento SAP rapido Ridimensiona hello e hello SAP applicazione prestazioni Standard () numero
* Obbligatorio consumo di memoria e risorse della CPU del sistema SAP hello
* Operazioni di input/output (I/O) al secondo necessarie
* Larghezza di banda di rete necessaria per l'eventuale comunicazione tra diverse VM in Azure
* Larghezza di banda di rete necessarie tra risorse locali e sistema SAP distribuito Azure hello

### <a name="resource-groups"></a>Gruppi di risorse
Gestione risorse di Microsoft Azure, è possibile utilizzare risorse gruppi toomanage tutte le risorse dell'applicazione hello nella sottoscrizione di Azure. Per altre informazioni, vedere [Panoramica di Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Risorse

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Risorse SAP
Quando si configura la distribuzione del software SAP, è necessario hello risorse SAP seguenti:

* Nota SAP [1928533], contenente:
  * Elenco di dimensioni di macchina virtuale di Azure sono supportati per la distribuzione del software SAP hello
  * Importanti informazioni sulla capacità per le dimensioni delle VM di Azure
  * Software SAP e combinazioni di sistemi operativi e database supportati
  * Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure

* La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.
* La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.
* Nota SAP [1409604] hello necessario versione dell'agente Host SAP per Windows in Azure.
* Nota SAP [2191498] hello necessario versione dell'agente Host SAP per Linux in Azure.
* La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.
* La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.
* La nota SAP [2002167] contiene informazioni generali su Red Hat Enterprise Linux 7.x.
* Nota SAP [1999351] contiene altre informazioni sulla risoluzione dei problemi per hello Azure Enhanced Monitoring Extension per SAP.
* [Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.
* Cmdlet di PowerShell specifici di SAP inclusi in [Azure PowerShell][azure-ps].
* Comandi dell'interfaccia della riga di comando di Azure specifici di SAP inclusi nell'[interfaccia della riga di comando di Azure][azure-cli].

[comment]: <> (MSSedusch TODO Add ARM patch level for SAP Host Agent in SAP Note 1409604)

### <a name="microsoft-resources"></a>Risorse Microsoft
Questi articoli Microsoft descrivono le distribuzioni SAP in Azure:

* [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Windows][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP in Windows (questo articolo)][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Windows][dbms-guide]
* [Portale di Azure][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Scenari di distribuzione per il software SAP in VM di Azure
È possibile distribuire le VM e i dischi associati in Azure in diversi modi. Differenze di hello toounderstand importanti tra le opzioni di distribuzione, è perché è possibile eseguire diversi passaggi tooprepare le macchine virtuali per la distribuzione in base al tipo di distribuzione hello che scelto.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Distribuzione di una macchina virtuale da hello Azure Marketplace per SAP
È possibile utilizzare un'immagine fornita da Microsoft o da terze parti in hello Azure Marketplace toodeploy la macchina virtuale. Hello Marketplace offre alcune immagini del sistema operativo standard di Windows Server e diverse distribuzioni di Linux. È anche possibile distribuire un'immagine che include SKU di sistema di gestione di database (DBMS), ad esempio, Microsoft SQL Server. Per altre informazioni sull'uso di immagini con SKU DBMS, vedere [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide].

Hello diagramma di flusso seguente viene illustrata hello SAP specifiche sequenza di passaggi per la distribuzione di una macchina virtuale da Azure Marketplace hello:

![Diagramma di flusso della distribuzione di macchine Virtuali per i sistemi SAP tramite un'immagine di macchina virtuale da hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Creare una macchina virtuale utilizzando hello portale di Azure
toocreate modo più semplice di Hello una nuova macchina virtuale con un'immagine da hello Azure Marketplace è tramite hello portale di Azure.

1.  Andare troppo<https://portal.azure.com/#create>.  In alternativa, nel menu del portale di Azure hello, selezionare **+ nuovo**.
2.  Selezionare **calcolo**e quindi selezionare il tipo di hello di cui si desidera toodeploy sistema operativo. Ad esempio, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) o Red Hat Enterprise Linux 7.2 (RHEL 7.2). visualizzazione elenco predefinito di Hello non mostra che tutti i sistemi operativi supportati. Selezionare **Visualizza tutto** per un elenco completo. Per altre informazioni sui sistemi operativi supportati per la distribuzione di software SAP, vedere la nota SAP [1928533].
3.  Nella pagina successiva di hello, esaminare i termini e condizioni.
4.  In hello **selezionare un modello di distribuzione** selezionare **Gestione risorse**.
5.  Selezionare **Crea**.

procedura guidata Hello permette di impostare la macchina virtuale hello necessario parametri toocreate hello, inoltre tooall necessarie risorse, quali le interfacce di rete e gli account di archiviazione. Ecco alcuni di questi parametri:

1. **Nozioni di base**:
  * **Nome**: nome hello della risorsa hello (nome della macchina virtuale hello).
 * **Nome utente e password** o **chiave pubblica SSH**: immettere hello utente e password dell'utente hello creati durante il provisioning di hello. Per una macchina virtuale Linux, è possibile immettere una chiave SSH (Secure Shell) pubblica hello utilizzare toosign toohello macchina.
 * **Sottoscrizione**: selezionare una sottoscrizione di hello che si desidera tooprovision toouse hello nuova macchina virtuale.
 * **Gruppo di risorse**: nome hello hello del gruppo di risorse per hello macchina virtuale. È possibile immettere il nome di hello di un nuovo nome gruppo o hello di risorse di un gruppo di risorse che esiste già.
 * **Percorso**: dove toodeploy hello nuova macchina virtuale. Se si desidera la rete locale tooconnect hello macchina virtuale tooyour, assicurarsi di selezionare il percorso di hello della rete virtuale hello che si connette rete locale tooyour Azure. Per altre informazioni, vedere [Rete di Microsoft Azure][planning-guide-microsoft-azure-networking] in [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide].
2. **Dimensione**:

     Per un elenco dei tipi di VM supportati, vedere la nota SAP [1928533]. Assicurarsi di che selezionare il tipo di macchina virtuale corretto hello se si desidera toouse archiviazione Premium di Azure. Non tutti i tipi di VM supportano Archiviazione Premium. Per altre informazioni, vedere [Archiviazione: Archiviazione di Microsoft Azure e dischi dati][planning-guide-storage-microsoft-azure-storage-and-data-disks] e [Archiviazione Premium di Azure][planning-guide-azure-premium-storage] in [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide].

3. **Impostazioni**:
   * **Account di archiviazione**: selezionare un account di archiviazione esistente o crearne uno nuovo. Non tutti i tipi di archiviazione funzionano per l'esecuzione di applicazioni SAP. Per altre informazioni sui tipi di Archiviazione, vedere [Archiviazione di Microsoft Azure][dbms-guide-2.3] in [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide].
   * **Rete virtuale** e **Subnet**: macchina virtuale di hello toointegrate con la rete intranet, hello selezionare rete virtuale rete locale connesso tooyour.
   * **Indirizzo IP pubblico**: selezionare hello indirizzo IP pubblico che si desidera toouse o immettere i parametri toocreate un nuovo indirizzo IP pubblico. È possibile utilizzare un tooaccess di indirizzo IP pubblico della macchina virtuale su hello Internet. Assicurarsi che anche creare una macchina di virtuale di rete sicurezza gruppo toohelp accesso sicuro tooyour.
   * **Gruppo di sicurezza di rete**: per altre informazioni, vedere [Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete][virtual-networks-nsg].
   * **Disponibilità**: selezionare un set di disponibilità o immettere i parametri di hello toocreate disponibilità di una nuova impostato. Per altre informazioni, vedere [Set di disponibilità di Azure][planning-guide-3.2.3].
   * **Monitoraggio**: è possibile selezionare **Disabilita** per la diagnostica del monitoraggio. Viene abilitata automaticamente quando si esegue hello comandi tooenable hello Azure Enhanced Monitoring Extension, come descritto in [Configura monitoraggio][deployment-guide-configure-monitoring-scenario-1].

4. **Riepilogo**:

  Riesaminare le selezioni e quindi fare clic su **OK**.

La macchina virtuale viene distribuita nel gruppo di risorse hello selezionato.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Creare una macchina virtuale usando un modello
È possibile creare una macchina virtuale utilizzando uno dei modelli SAP hello pubblicati in hello [repository GitHub di azure-Guida introduttiva: modelli][azure-quickstart-templates-github]. È anche possibile creare manualmente una macchina virtuale utilizzando hello [portale di Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], o [CLI di Azure ][virtual-machines-linux-tutorial].

* [**Modello per configurazione a due livelli (una sola macchina virtuale)** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]

  toocreate un sistema a due livelli utilizzando una sola macchina virtuale, utilizzare questo modello.
* [**Modello per configurazione a tre livelli (più macchine virtuali)** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  toocreate un sistema a tre livelli con più macchine virtuali, utilizzare questo modello.

Nel portale di Azure hello, immettere hello seguenti parametri per il modello di hello:

1. **Nozioni di base**:
  * **Sottoscrizione**: modello di hello sottoscrizione toouse toodeploy hello.
  * **Gruppo di risorse**: modello di risorsa gruppo toouse toodeploy hello hello. È possibile creare un nuovo gruppo di risorse oppure è possibile selezionare un gruppo di risorse esistente nella sottoscrizione hello.
  * **Percorso**: dove toodeploy hello modello. Se si seleziona un gruppo di risorse esistente, viene utilizzato il percorso di hello del gruppo di risorse.

2. **Impostazioni**:
  * **ID sistema SAP**: hello ID sistema SAP (SID).
  * **Tipo di sistema operativo**: hello del sistema operativo desiderato toodeploy, ad esempio, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) o Red Hat Enterprise Linux 7.2 (RHEL 7.2).

    visualizzazione elenco predefinito di Hello non mostra che tutti i sistemi operativi supportati. Selezionare **Visualizza tutto** per un elenco completo. Per altre informazioni sui sistemi operativi supportati per la distribuzione di software SAP, vedere la nota SAP [1928533].
  * **Dimensioni del sistema SAP**: hello dimensioni di hello sistema SAP.

    fornisce il numero di Hello del nuovo sistema SAP hello. Se non si conoscono quanti valori SAPS hello sistema richiede, chiedere al SAP tecnologia Partner o l'integratore di sistema.
  * **La disponibilità del sistema** (solo modello di livello 3): hello la disponibilità del sistema.

    Selezionare **HA** per una configurazione adatta a un'installazione a disponibilità elevata. Vengono creati due server di database e due server per ABAP SAP Central Services (ASCS).
  * **Tipo di archiviazione** (solo modello a due livelli): tipo di archiviazione toouse hello.

    Per i sistemi più grandi, è consigliabile usare Archiviazione Premium di Azure. Per altre informazioni sui tipi di archiviazione, vedere queste risorse:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP)
      * [Archiviazione di Microsoft Azure][dbms-guide-2.3] in [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]
      * [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure][storage-premium-storage-preview-portal]
      * [Introduzione tooMicrosoft di archiviazione di Azure][storage-introduction]
  * **Nome utente amministratore** e **Password amministratore**: nome utente e password dell'amministratore.
    Per la firma nella macchina virtuale toohello, viene creato un nuovo utente.
  * **Subnet nuova o esistente**: determina se vengono create una nuova rete virtuale e una nuova subnet o viene usata una subnet esistente. Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare **esistente**.
  * **ID di subnet**: hello ID di subnet hello hello le macchine virtuali si connetterà. Selezionare hello subnet della rete privata virtuale (VPN) o Azure ExpressRoute rete virtuale toouse tooconnect hello tooyour locale rete della macchina virtuale. ID Hello in genere è simile al seguente: /Subscriptions/<ID&lt;id sottoscrizione >/ResourceGroups /&lt;nome gruppo di risorse > /providers/Microsoft.Network/virtualNetworks/&lt;nome di rete virtuale > /subnets/&lt;nome subnet >

3. **Condizioni**:  
    Leggere e accettare i termini legali specifici hello.

4.  Selezionare **Acquisto**.

Hello agente VM di Azure viene distribuito per impostazione predefinita, quando si utilizza un'immagine da hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Configurare le impostazioni proxy
A seconda della configurazione della rete locale, potrebbe essere necessario tooset di proxy hello nella VM. Se la macchina virtuale è connessa tooyour rete locale tramite VPN o ExpressRoute, hello macchina virtuale potrebbe non essere in grado di tooaccess hello Internet e non essere in grado di toodownload estensioni hello richiesto o raccogliere dati di monitoraggio. Per ulteriori informazioni, vedere [configurare proxy hello][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Aggiungere a un dominio (solo per Windows)
Se la distribuzione di Azure viene connesso tooan istanza locale di Active Directory o DNS tramite una connessione VPN di Azure site-to-site o ExpressRoute (detta *cross-premise* in [pianificazione macchine virtuali di Azure e sull'implementazione di SAP in Linux][planning-guide]), è previsto che hello macchina virtuale è aggiunta a un dominio locale. Per ulteriori informazioni su considerazioni per questa attività, vedere [aggiunta a un dominio locale VM tooan (solo Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configurare il monitoraggio
che l'ambiente supporta SAP, impostare hello Azure Monitoring Extension per SAP come descritto in toobe [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5]. Verifica dei prerequisiti di hello per il monitoraggio SAP e le versioni minime richieste del Kernel SAP e dell'agente Host SAP, in risorse hello elencate in [risorse SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Controllo del monitoraggio
Controllare se il monitoraggio funziona, come descritto in [Controlli e risoluzione dei problemi per la configurazione del monitoraggio end-to-end][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Passaggi post-distribuzione
Dopo aver creato hello VM e VM hello viene distribuito, è necessario tooinstall hello necessario componenti software hello macchina virtuale. A causa di sequenza di installazione software di installazione/hello in questo tipo di distribuzione di macchine Virtuali, hello toobe di software installato deve essere già disponibili in Azure, in un'altra macchina virtuale o come un disco che può essere collegato. In alternativa, prendere in considerazione uno scenario di cross-premise, in cui la connettività toohello locale asset (condivisioni di installazione) viene fornito.

Dopo aver distribuito la macchina virtuale in Azure, seguire hello stessi strumenti e linee guida tooinstall hello il software SAP nella macchina virtuale come si sarebbe in un ambiente locale. tooinstall il software SAP in una macchina virtuale di Azure, sia SAP e Microsoft consiglia di caricare e archiviare i supporti di installazione di SAP hello in dischi rigidi virtuali di Azure o creare una macchina virtuale di Azure che funziona come un file server dotato di hello tutti necessario il supporto di installazione di SAP.

[comment]: <> (TODO MSSedusch perché sono necessarie toorecommend una gestione dei file, ad esempio, File Server o un disco rigido virtuale? Is that so different from on-premises?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Distribuzione di una VM con un'immagine personalizzata per SAP
Poiché versioni diverse di un sistema operativo o DBMS presentano requisiti di patch diverso, le immagini di hello che trova in hello Azure Marketplace potrebbero non soddisfare le proprie esigenze. È possibile invece toocreate una macchina virtuale utilizzando la propria immagine di macchina virtuale del sistema operativo/DBMS, che è possibile distribuire più tardi.
Utilizzare diversi passaggi toocreate un'immagine privata per Linux di toocreate per Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> un'immagine di Windows che è possibile utilizzare toodeploy più macchine virtuali, le impostazioni di Windows hello (ad esempio SID e il nome host) devono essere estratti o generalizzato su hello tooprepare locale macchina virtuale. È possibile utilizzare [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo questo.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare un'immagine Linux, che è possibile utilizzare toodeploy più macchine virtuali, alcune impostazioni di Linux devono essere hello astratto o generalizzato nella macchina virtuale in locale. È possibile utilizzare `waagent -deprovision` toodo questo. Per ulteriori informazioni, vedere [acquisire una macchina virtuale di Linux in esecuzione in Azure] [ virtual-machines-linux-capture-image] hello e [Guida dell'utente dell'agente Linux di Azure][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
È possibile preparare e creare un'immagine personalizzata e quindi utilizzarlo toocreate più nuove macchine virtuali. come illustrato in [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]. Set di backup del database del contenuto tramite l'utilizzo di SAP Software Provisioning Manager tooinstall un nuovo sistema SAP (Ripristina un backup del database da un disco rigido virtuale che è collegato toohello virtual machine) o ripristinando un backup del database da archiviazione di Azure, direttamente se DBMS lo supporta. Per altre informazioni, vedere [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]. Se è già stato installato un sistema SAP nella macchina virtuale locale (in particolare per sistemi a due livelli), è possibile adattare le impostazioni di sistema SAP hello dopo la distribuzione di hello di hello macchina virtuale di Azure tramite procedure di sistema rinominare hello supportate da SAP Software Provisioning Manager (nota SAP [1619720]). In caso contrario, è possibile installare il software SAP hello dopo aver distribuito hello macchina virtuale di Azure.

Hello diagramma di flusso seguente viene illustrata hello SAP specifiche sequenza di passaggi per la distribuzione di una macchina virtuale da un'immagine personalizzata:

![Diagramma di flusso della distribuzione di una VM per sistemi SAP con un'immagine di VM di marketplace privato][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Creare una macchina virtuale hello
toocreate una distribuzione tramite un'immagine del sistema operativo privata dal portale di Azure hello utilizzare uno dei seguenti modelli SAP hello. Questi modelli vengono pubblicati in hello [repository GitHub di azure-Guida introduttiva: modelli][azure-quickstart-templates-github]. È anche possibile creare una macchina virtuale manualmente usando [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Modello per configurazione a due livelli (una sola macchina virtuale)** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  toocreate un sistema a due livelli utilizzando una sola macchina virtuale, utilizzare questo modello.
* [**Modello per configurazione a tre livelli (più macchine virtuali)** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  toocreate un sistema a tre livelli con più macchine virtuali o la propria immagine del sistema operativo, utilizzare questo modello.

Nel portale di Azure hello, immettere hello seguenti parametri per il modello di hello:

1. **Nozioni di base**:
  * **Sottoscrizione**: modello di hello sottoscrizione toouse toodeploy hello.
  * **Gruppo di risorse**: modello di risorsa gruppo toouse toodeploy hello hello. È possibile creare un nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nella sottoscrizione hello.
  * **Percorso**: dove toodeploy hello modello. Se si seleziona un gruppo di risorse esistente, viene utilizzato il percorso di hello del gruppo di risorse.
2. **Impostazioni**:
  * **ID sistema SAP**: hello ID sistema SAP.
  * **Tipo di sistema operativo**: hello tipo sistema operativo da toodeploy (Windows o Linux).
  * **Dimensioni del sistema SAP**: hello dimensioni di hello sistema SAP.

    fornisce il numero di Hello del nuovo sistema SAP hello. Se non si conoscono quanti valori SAPS hello sistema richiede, chiedere al SAP tecnologia Partner o l'integratore di sistema.
  * **La disponibilità del sistema** (solo modello di livello 3): hello la disponibilità del sistema.

    Selezionare **HA** per una configurazione adatta a un'installazione a disponibilità elevata. Vengono creati due server di database e due server per ASCS.
  * **Tipo di archiviazione** (solo modello a due livelli): tipo di archiviazione toouse hello.

    Per i sistemi più grandi, è consigliabile usare Archiviazione Premium di Azure. Per ulteriori informazioni sui tipi di archiviazione, vedere hello seguenti risorse:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP)
      * [Archiviazione di Microsoft Azure][dbms-guide-2.3] in [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]
      * [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure][storage-premium-storage-preview-portal]
      * [Introduzione tooMicrosoft di archiviazione di Azure][storage-introduction]
  * **Immagine utente URI VHD**: hello URI dell'immagine del sistema operativo privata hello disco rigido virtuale, ad esempio https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Account di archiviazione immagine utente**: nome hello dell'immagine del sistema operativo privata hello memorizzazione, ad esempio, account di archiviazione hello &lt;accountname > in https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Nome utente amministratore** e **password amministratore**: hello nome utente e password.

    Per la firma nella macchina virtuale toohello, viene creato un nuovo utente.
  * **Subnet nuova o esistente**: determina se vengono create una nuova rete virtuale e una nuova subnet o viene usata una subnet esistente. Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare **esistente**.
  * **ID di subnet**: hello ID delle macchine virtuali di hello subnet toowhich hello si connetterà. Selezionare hello subnet della rete VPN o ExpressRoute rete virtuale toouse tooconnect hello macchina virtuale tooyour locale rete. ID Hello in genere è simile al seguente:

    /subscriptions/&lt;ID sottoscrizione>/resourceGroups/&lt;nome gruppo di risorse>/providers/Microsoft.Network/virtualNetworks/&lt;nome rete virtuale>/subnets/&lt;nome subnet>

3. **Condizioni**:  
    Leggere e accettare i termini legali specifici hello.

4.  Selezionare **Acquisto**.

#### <a name="install-hello-vm-agent-linux-only"></a>Installare hello agente della macchina virtuale (solo Linux)
modelli di hello toouse descritti nella precedente sezione hello, hello che agente Linux deve essere già installato, l'immagine utente hello o della distribuzione hello non riuscirà. Scaricare e installare l'agente VM hello nell'immagine utente hello come descritto in [scaricare, installare e abilitare l'agente VM di Azure hello][deployment-guide-4.4]. Se non si utilizzano modelli hello, è possibile installare hello agente della macchina virtuale in un secondo momento.

#### <a name="join-a-domain-windows-only"></a>Aggiungere a un dominio (solo per Windows)
Se la distribuzione di Azure viene connesso tooan istanza locale di Active Directory o DNS tramite una connessione VPN di Azure site-to-site o ExpressRoute di Azure (detta *cross-premise* in [macchine virtuali di Azure pianificazione e implementazione di SAP in Linux][planning-guide]), è previsto che hello macchina virtuale è aggiunta a un dominio locale. Per ulteriori informazioni su considerazioni per questo passaggio, vedere [aggiunta a un dominio locale VM tooan (solo Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configurare le impostazioni proxy
A seconda della configurazione della rete locale, potrebbe essere necessario tooset di proxy hello nella VM. Se la macchina virtuale è connessa tooyour rete locale tramite VPN o ExpressRoute, hello macchina virtuale potrebbe non essere in grado di tooaccess hello Internet e non essere in grado di toodownload estensioni hello richiesto o raccogliere dati di monitoraggio. Per ulteriori informazioni, vedere [configurare proxy hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurare il monitoraggio
che l'ambiente supporta SAP, impostare hello Azure Monitoring Extension per SAP come descritto in toobe [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5]. Verifica dei prerequisiti di hello per il monitoraggio SAP e le versioni minime richieste del Kernel SAP e dell'agente Host SAP, in risorse hello elencate in [risorse SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Controllo del monitoraggio
Controllare se il monitoraggio funziona, come descritto in [Controlli e risoluzione dei problemi per la configurazione del monitoraggio end-to-end][deployment-guide-troubleshooting-chapter].




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Spostamento di una VM locale tramite un disco rigido virtuale di Azure non generalizzato con SAP
In questo scenario, è possibile pianificare toomove un sistema SAP specifico da un tooAzure ambiente locale. È possibile farlo caricando hello disco rigido virtuale con sistema operativo, i file binari SAP hello, hello e infine hello binari DBMS, più dischi rigidi virtuali hello con dati hello e i file di hello DBMS, tooAzure di log. Diversamente dallo scenario hello descritto in [nello Scenario 2: distribuzione di una macchina virtuale con un'immagine personalizzata per SAP][deployment-guide-3.3], in questo caso, mantenere hello hostname, il SID di SAP e gli account utente SAP in VM di Azure, hello perché sono stati configurato nell'ambiente locale hello. Non è necessario toogeneralize hello del sistema operativo. Questo scenario si applica più spesso toocross locale scenari in cui parte di hello landscape SAP eseguito in locale e parte di esso viene eseguito in Azure.

In questo scenario, hello agente della macchina virtuale non viene installato automaticamente durante la distribuzione. Poiché hello agente VM e hello Azure Enhanced Monitoring Extension per SAP necessari per toorun SAP, è necessario toodownload, installare e attivare entrambi i componenti manualmente dopo la creazione di macchine virtuali hello.

Per ulteriori informazioni su hello agente VM di Azure, vedere hello seguenti risorse.

[comment]: <> (MSSedusch TODO Update Windows Link below)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Guida dell'utente dell'agente Linux di Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Hello seguente diagramma mostra hello sequenza di passaggi per lo spostamento di una macchina virtuale locale utilizzando un disco rigido virtuale Azure non generalizzato:

![Diagramma di flusso della distribuzione di una VM per sistemi SAP con un disco della VM][deployment-guide-figure-400]

Supponendo che hello disco è già caricato e definito in Azure (vedere [macchine virtuali di Azure di pianificazione e implementazione di SAP in Linux][planning-guide]), effettuare le attività di hello descritti in hello accanto sezioni.

#### <a name="create-a-virtual-machine"></a>Creare una macchina virtuale
toocreate una distribuzione utilizzando un disco del sistema operativo privato tramite hello portale di Azure, utilizzare il modello SAP hello pubblicato in hello [repository GitHub di azure-Guida introduttiva: modelli][azure-quickstart-templates-github]. È anche possibile creare una macchina virtuale manualmente usando PowerShell.

* [**Modello per configurazione a due livelli (una sola macchina virtuale)** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  toocreate un sistema a due livelli utilizzando una sola macchina virtuale, utilizzare questo modello.

Nel portale di Azure hello, immettere hello seguenti parametri per il modello di hello:

1. **Nozioni di base**:
  * **Sottoscrizione**: modello di hello sottoscrizione toouse toodeploy hello.
  * **Gruppo di risorse**: modello di risorsa gruppo toouse toodeploy hello hello. È possibile creare un nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nella sottoscrizione hello.
  * **Percorso**: dove toodeploy hello modello. Se si seleziona un gruppo di risorse esistente, viene utilizzato il percorso di hello del gruppo di risorse.
2. **Impostazioni**:
  * **ID sistema SAP**: hello ID sistema SAP.
  * **Tipo di sistema operativo**: hello tipo sistema operativo da toodeploy (Windows o Linux).
  * **Dimensioni del sistema SAP**: hello dimensioni di hello sistema SAP.

    fornisce il numero di Hello del nuovo sistema SAP hello. Se non si conoscono quanti valori SAPS hello sistema richiede, chiedere al SAP tecnologia Partner o l'integratore di sistema.
  * **Tipo di archiviazione** (solo modello a due livelli): tipo di archiviazione toouse hello.

    Per i sistemi più grandi, è consigliabile usare Archiviazione Premium di Azure. Per ulteriori informazioni sui tipi di archiviazione, vedere hello seguenti risorse:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP)
      * [Archiviazione di Microsoft Azure][dbms-guide-2.3] in [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]
      * [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure][storage-premium-storage-preview-portal]
      * [Introduzione tooMicrosoft di archiviazione di Azure][storage-introduction]
  * **URI VHD su disco SO**: hello URI del disco del sistema operativo privato hello, ad esempio https://&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Subnet nuova o esistente**: determina se vengono create una nuova rete virtuale e una nuova subnet o viene usata una subnet esistente. Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare **esistente**.
  * **ID di subnet**: hello ID delle macchine virtuali di hello subnet toowhich hello si connetterà. Selezionare hello subnet della rete VPN o Azure ExpressRoute rete virtuale toouse tooconnect hello macchina virtuale tooyour locale rete. ID Hello in genere è simile al seguente:

    /subscriptions/&lt;ID sottoscrizione>/resourceGroups/&lt;nome gruppo di risorse>/providers/Microsoft.Network/virtualNetworks/&lt;nome rete virtuale>/subnets/&lt;nome subnet>

3. **Condizioni**:  
    Leggere e accettare i termini legali specifici hello.

4.  Selezionare **Acquisto**.

#### <a name="install-hello-vm-agent"></a>Installare l'agente VM hello
hello di hello toouse modelli descritti nella sezione precedente, hello agente della macchina virtuale deve essere installato sul disco del sistema operativo hello o hello distribuzione avrà esito negativo. Scaricare e installare hello agente della macchina virtuale nella macchina virtuale, hello come descritto in [scaricare, installare e abilitare l'agente VM di Azure hello][deployment-guide-4.4].

Se non si utilizzano modelli hello descritti nella precedente sezione hello, è possibile installare anche hello agente della macchina virtuale in un secondo momento.

#### <a name="join-a-domain-windows-only"></a>Aggiungere a un dominio (solo per Windows)
Se la distribuzione di Azure viene connesso tooan istanza locale di Active Directory o DNS tramite una connessione VPN di Azure site-to-site o ExpressRoute (detta *cross-premise* in [pianificazione macchine virtuali di Azure e sull'implementazione di SAP in Linux][planning-guide]), è previsto che hello macchina virtuale è aggiunta a un dominio locale. Per ulteriori informazioni su considerazioni per questa attività, vedere [aggiunta a un dominio locale VM tooan (solo Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configurare le impostazioni proxy
A seconda della configurazione della rete locale, potrebbe essere necessario tooset di proxy hello nella VM. Se la macchina virtuale è connessa tooyour rete locale tramite VPN o ExpressRoute, hello macchina virtuale potrebbe non essere in grado di tooaccess hello Internet e non essere in grado di toodownload estensioni hello richiesto o raccogliere dati di monitoraggio. Per ulteriori informazioni, vedere [configurare proxy hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurare il monitoraggio
che l'ambiente supporta SAP, impostare hello Azure Monitoring Extension per SAP come descritto in toobe [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5]. Verifica dei prerequisiti di hello per il monitoraggio SAP e le versioni minime richieste del Kernel SAP e dell'agente Host SAP, in risorse hello elencate in [risorse SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Controllo del monitoraggio
Controllare se il monitoraggio funziona, come descritto in [Controlli e risoluzione dei problemi per la configurazione del monitoraggio end-to-end][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Aggiornare la configurazione di monitoraggio hello per SAP
Aggiornamento configurazione del monitoraggio SAP hello in uno dei seguenti scenari hello:
* il team Microsoft/SAP comune di Hello estende hello funzionalità di monitoraggio e richiede maggiore o minore di contatori.
* Microsoft ha introdotto una nuova versione di hello Azure infrastruttura sottostante che fornisce i dati di monitoraggio hello e hello Azure Enhanced Monitoring Extension per SAP esigenze toobe adattato toothose modifiche.
* Montare ulteriori dischi rigidi virtuali tooyour macchina virtuale di Azure o si rimuove un disco rigido virtuale. In questo scenario, aggiornare la raccolta di hello dei dati relativi alla memoria. Modifica della configurazione mediante l'aggiunta o eliminazione di endpoint o assegnando IP indirizzi tooa VM non influiscono sulla hello Monitoraggio configurazione.
* Modificate hello dimensione di macchina virtuale di Azure, ad esempio, dalla dimensione A5 tooany altre dimensioni della macchina virtuale.
* Aggiungere nuovo tooyour di interfacce di rete VM di Azure.

tooupdate monitoraggio impostazioni, hello aggiornamento monitoraggio dell'infrastruttura da hello seguendo i passaggi [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Attività dettagliate per la distribuzione del software SAP in una VM Windows
In questa sezione contiene passaggi dettagliati per eseguire specifiche attività nel processo di configurazione e distribuzione hello.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Distribuire i cmdlet di Azure PowerShell
1.  Andare troppo[download di Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  In **Strumenti da riga di comando**, in **PowerShell** selezionare **Windows - Installazione**.
3.  Nel Microsoft Download Manager dialogo hello, per il file scaricato hello (ad esempio, WindowsAzurePowershellGet.3f.3f.3fnew.exe), selezionare **eseguire**.
4.  Selezionare Installazione guidata piattaforma Web di Microsoft (Microsoft Web PI), toorun **Sì**.
5.  Viene visualizzata una pagina simile a questa:

  ![Pagina di installazione dei cmdlet di Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selezionare **installare**, quindi accettare condizioni di licenza Software Microsoft hello.
7.  Azure PowerShell viene installato. Selezionare **fine** installazione guidata di tooclose hello.

Controllare spesso per gli aggiornamenti toohello i cmdlet di PowerShell, che in genere, vengono aggiornati ogni mese. Hello toocheck di modo più semplice per gli aggiornamenti è hello toodo precedenti passaggi di installazione, pagina Installazione toohello illustrato nel passaggio 5. numero Hello versione data e di rilascio di hello cmdlet è disponibili nella pagina hello illustrato nel passaggio 5. Se non specificato diversamente nella nota SAP [1928533] o la nota SAP [2015553], si consiglia di lavorare con una versione più recente di hello dei cmdlet PowerShell di Azure.

versione di hello toocheck di hello cmdlet PowerShell di Azure che vengono installati nel computer in uso, eseguire questo comando di PowerShell:
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
risultato Hello è simile al seguente:

![Risultato del controllo della versione dei cmdlet di Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

Se hello cmdlet di Azure versione installata nel computer è hello corrente, prima pagina di hello dell'installazione guidata di hello indica che tramite l'aggiunta di **(installati)** titolo prodotto toohello (vedere la seguente schermata hello). I cmdlet di Azure PowerShell vengono aggiornati. tooclose hello installazione guidata, seleziona **uscita**.

![Pagina di installazione per i cmdlet PowerShell di Azure che indica la versione più recente di hello di cmdlet di Azure PowerShell sono installati][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Distribuire l'interfaccia della riga di comando di Azure
1.  Andare troppo[download di Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  In **strumenti da riga di comando**in **interfaccia della riga di comando di Azure**selezionare hello **installare** collegamento per il sistema operativo.
3.  Nel Microsoft Download Manager dialogo hello, per il file scaricato hello (ad esempio, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), selezionare **eseguire**.
4.  Selezionare Installazione guidata piattaforma Web di Microsoft (Microsoft Web PI), toorun **Sì**.
5.  Viene visualizzata una pagina simile a questa:

  ![Pagina di installazione dei cmdlet di Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selezionare **installare**, quindi accettare condizioni di licenza Software Microsoft hello.
7.  L'interfaccia della riga di comando di Azure viene installata. Selezionare **fine** installazione guidata di tooclose hello.

Controllare periodicamente la presenza di aggiornamenti tooAzure CLI, che in genere, viene aggiornato ogni mese. Hello toocheck di modo più semplice per gli aggiornamenti è hello toodo precedenti passaggi di installazione, pagina Installazione toohello illustrato nel passaggio 5.


versione di hello toocheck di CLI di Azure installata nel computer in uso, eseguire questo comando:
```
azure --version
```

risultato Hello è simile al seguente:

![Risultato del controllo della versione dell'interfaccia della riga di comando di Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Aggiunta a un dominio locale VM tooan (solo Windows)
Se si distribuiscono macchine virtuali SAP in uno scenario cross-premise, in cui vengono estese locale di Active Directory e DNS in Azure, è previsto che le macchine virtuali hello vengono aggiunti a un dominio locale. Hello dettagliato i passaggi toojoin un dominio locale VM tooan e hello toobe richiesto software aggiuntivo un membro di un dominio locale, varia in base al cliente. In genere, toojoin tooan una macchina virtuale locale dominio, è necessario software aggiuntivo tooinstall, ad esempio software antimalware e di backup o software di monitoraggio.

In questo scenario, è inoltre necessario verificare se le impostazioni proxy Internet vengono forzate quando una macchina virtuale viene aggiunto a un dominio nell'ambiente in uso, Windows hello dispone di Account di sistema locale (S-1-5-18) nella macchina virtuale Guest hello hello stesse impostazioni del proxy toomake. opzione più semplice Hello è proxy hello tooforce tramite criteri di gruppo che si applica toosystems nel dominio hello un dominio.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Scaricare, installare e abilitare hello agente VM di Azure
Per le macchine virtuali distribuite da un'immagine del sistema operativo che non è generalizzata (ad esempio, un'immagine che non derivano nello strumento di preparazione del sistema Windows, o di sysprep, hello), è necessario toomanually download, installare e abilitare hello agente VM di Azure.

Se si distribuisce una macchina virtuale da Azure Marketplace hello, questo passaggio non è obbligatorio. Le immagini da Azure Marketplace hello dispongono già di hello agente VM di Azure.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Scaricare hello agente VM di Azure:
  1.  Scaricare hello [pacchetto di installazione agente VM di Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Archiviare localmente pacchetto MSI dell'agente VM di hello su un personal computer o server.
2.  Installare l'agente VM di Azure hello:
  1.  Connettersi toohello distribuita una macchina virtuale di Azure tramite Remote Desktop Protocol (RDP).
  2.  Aprire una finestra di Esplora in hello VM e di una directory di destinazione selezionare hello per file con estensione MSI hello di hello agente della macchina virtuale.
  3.  Trascinare file con estensione MSI di programma di installazione dell'agente di Azure VM hello dalla directory di destinazione computer o server locale toohello di hello agente VM hello macchina virtuale.
  4.  Fare doppio clic sul file con estensione MSI hello in hello macchina virtuale.
3.  Per le macchine virtuali sono domini locali tooon unita in join, assicurarsi che eventuali impostazioni del proxy Internet anche applicano toohello account di sistema locale di Windows (S-1-5-18) nella macchina virtuale, hello come descritto in [configurare proxy hello] [ deployment-guide-configure-proxy]. Hello agente della macchina virtuale viene eseguita in questo contesto e deve toobe tooconnect in grado di tooAzure.

L'intervento dell'utente non è obbligatorio tooupdate hello agente VM di Azure. Ciao agente VM viene aggiornata automaticamente e non richiede un riavvio della macchina virtuale.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Utilizzare hello seguenti comandi tooinstall hello agente della macchina virtuale per Linux:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

Se è già installato l'agente hello, hello tooupdate agente Linux di Azure, hello passaggi descritti in [hello aggiornamento agente Linux di Azure in una versione più recente di toohello VM da GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configurare il proxy di hello
passaggi Hello utilizzati proxy hello tooconfigure in Windows sono diversi dalle modalità di hello che configurazione proxy hello in Linux.

#### <a name="windows"></a>Windows
Le impostazioni del proxy devono essere configurate correttamente per hello tooaccess hello Internet di account di sistema locale. Se le impostazioni del proxy non sono impostate in Criteri di gruppo, è possibile configurare le impostazioni di hello per hello account sistema locale.

1. Andare troppo**avviare**, immettere **gpedit. msc**, quindi selezionare **invio**.
2. Selezionare **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Internet Explorer**. Verificare che tale impostazione hello **renderlo impostazioni per computer (anziché per utente)** è disabilitato o non configurato.
3. In **Pannello di controllo**, andare troppo**centro rete e condivisione** > **Opzioni Internet**.
4. In hello **connessioni** scheda, seleziona hello **impostazioni LAN** pulsante.
5. Crittografato hello **rileva automaticamente impostazioni** casella di controllo.
6. Seleziona hello **utilizza un server proxy per le connessioni LAN** casella di controllo e quindi immettere l'indirizzo del proxy hello e la porta.
7. Seleziona hello **avanzate** pulsante.
8. In hello **eccezioni** , immettere l'indirizzo IP hello **168.63.129.16**. Selezionare **OK**.


#### <a name="linux"></a>Linux
Configurare il proxy corretto hello nel file di configurazione hello dell'agente Guest di Microsoft Azure, che si trova in hello \\via\\waagent.conf.

Impostare hello seguenti parametri:

1.  **Host proxy HTTP**. Ad esempio, impostare troppo**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Porta proxy HTTP**. Ad esempio, impostare troppo**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Riavviare l'agente di hello.

  ```
  sudo service waagent restart
  ```

impostazioni proxy in Hello \\via\\waagent.conf si applicano anche le estensioni VM toohello richiesto. Se si desidera toouse hello Azure repository, assicurarsi che non sarà repository toothese di hello il traffico attraverso la rete intranet locale. Se è stato creato definito dall'utente tooenable route il tunneling forzato, assicurarsi che si aggiunge una route che indirizza repository toohello traffico direttamente toohello Internet e non tramite la connessione VPN da sito a sito.

* **SLES**

  È inoltre necessario tooadd route per gli indirizzi IP hello elencate in \\via\\regionserverclnt.cfg. Hello figura riportata di seguito viene illustrato un esempio:

  ![Tunneling forzato][deployment-guide-figure-50]


* **RHEL**

  È inoltre necessario tooadd route per gli indirizzi IP hello degli host hello elencate in \\via\\yum.repos.d\\rhui bilanciamento. Per un esempio, vedere hello nella figura precedente.

Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configurare hello Azure Enhanced Monitoring Extension per SAP
Quando è stata preparata hello VM come descritto in [scenari di distribuzione di macchine virtuali per SAP in Azure][deployment-guide-3], hello agente VM di Azure viene installato nella macchina virtuale hello. passaggio successivo Hello è toodeploy hello Azure Enhanced Monitoring Extension per SAP, è disponibile in hello Repository estensioni di Azure nei Data Center di Azure globale hello. Per altre informazioni, vedere [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide-9.1].

È possibile utilizzare PowerShell o Azure CLI tooinstall e configurare hello Azure Enhanced Monitoring Extension per SAP. estensione di hello tooinstall in Windows o Linux VM utilizzando un computer Windows, vedere [Azure PowerShell][deployment-guide-4.5.1]. estensione di hello tooinstall in una VM Linux usando un desktop Linux, vedere [CLI di Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell per VM Linux e Windows
tooinstall hello Azure Enhanced Monitoring Extension per SAP con PowerShell:

1. Assicurarsi di aver installato una versione più recente di hello del cmdlet di Azure PowerShell hello. Per altre informazioni, vedere [Distribuzione di cmdlet di Azure PowerShell][deployment-guide-4.1].  
2. Eseguire hello seguente cmdlet di PowerShell.
  Per un elenco degli ambienti disponibili, eseguire `commandlet Get-AzureRmEnvironment`. Se si desidera toouse Azure pubblico, l'ambiente è **cloud**. Per Azure in Cina, selezionare **AzureChinaCloud**.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

Dopo aver immesso i dati dell'account e identificare hello macchina virtuale di Azure, script hello consente di distribuire le estensioni necessarie hello e abilita le funzionalità di hello necessario. Ciò può richiedere alcuni minuti.
Per altre informazioni su `Set-AzureRmVMAEMExtension`, vedere [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![Esecuzione corretta del cmdlet di Azure specifico di SAP Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Hello `Set-AzureRmVMAEMExtension` configuration tutti gli host di tooconfigure passaggi hello monitoring per SAP.

output di Hello script include hello le seguenti informazioni:

* Conferma che il monitoraggio di base hello disco rigido virtuale (con Buongiorno del sistema operativo) e tutti i dischi rigidi virtuali aggiuntivi montati toohello che macchina virtuale è stata configurata.
* Hello due messaggi successivi verificare la configurazione di hello di metriche di archiviazione per un account di archiviazione specifico.
* Una riga di output restituisce lo stato di hello dell'aggiornamento effettivo di hello hello della configurazione del monitoraggio.
* Un'altra riga dell'output conferma che la configurazione di hello è stata distribuita o aggiornata.
* Hello l'ultima riga dell'output è informativo. Mostra le opzioni per la configurazione del monitoraggio hello test.

toocheck che tutti i passaggi di Azure Enhanced Monitoring sono stati eseguiti correttamente e che hello infrastruttura di Azure fornisce i dati necessari hello, procedere con il controllo di conformità hello per hello Azure Enhanced Monitoring Extension per SAP, come descritto in [Controllo conformità per Azure Enhanced Monitoring per SAP][deployment-guide-5.1]. Attendere 15-30 minuti per i dati di diagnostica Azure toocollect hello pertinenti.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Interfaccia della riga di comando di Azure per VM Linux
tooinstall hello Azure Enhanced Monitoring Extension per SAP tramite l'interfaccia CLI di Azure:

1. Installare l'interfaccia CLI di Azure, come descritto in [installazione hello Azure CLI][azure-cli].
2. Accedere con l'account Azure:

  ```
  azure login
  ```

3. Cambia la modalità di gestione risorse tooAzure:

  ```
  azure config mode arm
  ```

4. Abilitare il monitoraggio avanzato di Azure:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Verificare che hello Azure Enhanced Monitoring Extension è attiva su hello VM Linux di Azure. Controllare se hello file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters esiste. Se esiste, al prompt dei comandi, eseguire questo comando toodisplay raccolti da hello monitoraggio avanzato di Azure:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

output di Hello è simile al seguente:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Controlli e risoluzione dei problemi per il monitoraggio end-to-end
Dopo aver distribuito la macchina virtuale di Azure e configurare hello infrastruttura di Azure monitoring, verificare se tutti i componenti di hello di hello Azure Enhanced Monitoring Extension funzionino come previsto.

Eseguire il controllo di conformità hello per hello Azure Enhanced Monitoring Extension per SAP, come descritto in [controllo conformità per Azure Enhanced Monitoring Extension per SAP hello][deployment-guide-5.1]. Se tutti i risultati dei controlli dello stato di preparazione sono positivi e tutti i contatori delle prestazioni pertinenti sono funzionanti, significa che il monitoraggio di Azure è stato configurato correttamente. È possibile procedere con l'installazione di hello dell'agente Host SAP descritti nelle note SAP hello in [risorse SAP][deployment-guide-2.2]. Se il controllo di conformità hello indica che i contatori sono mancanti, eseguire il controllo di integrità hello per hello Azure infrastruttura di monitoraggio, come descritto in [verifica integrità per la configurazione del monitoraggio dell'infrastruttura Azure] [ deployment-guide-5.2]. Per altre opzioni di risoluzione dei problemi, vedere [Risoluzione dei problemi di monitoraggio di Azure per SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Controllo conformità per hello Azure Enhanced Monitoring Extension per SAP
Questo controllo assicura che tutte le metriche delle prestazioni che vengono visualizzati all'interno dell'applicazione SAP vengono fornite da hello Azure monitoraggio dell'infrastruttura sottostante.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Eseguire il controllo di conformità hello in una macchina virtuale Windows

1.  Accedi toohello macchina virtuale di Azure (utilizzando un account amministratore non è necessario).
2.  Aprire una finestra del prompt dei comandi.
3.  Al prompt dei comandi di hello, Modifica cartella di installazione di hello directory toohello di hello Azure Enhanced Monitoring Extension per SAP: c:\\pacchetti\\plug-in\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versione >\\drop

  Hello *versione* in hello percorso toohello monitoraggio estensione potrebbe variare. Se le cartelle per più versioni di monitoraggio di estensione nella cartella di installazione hello, controllare la configurazione del servizio Windows di AzureEnhancedMonitoring, hello hello hello e quindi commutatore toohello cartella indicata come *tooexecutable percorso* .

  ![Proprietà del servizio in esecuzione hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-figure-1000]

4.  Al prompt dei comandi di hello, eseguire **azperflib.exe** senza parametri.

  > [!NOTE]
  > Azperflib.exe viene eseguito in un ciclo e aggiorna i contatori di hello raccolti ogni 60 secondi. ciclo di hello tooend, finestra prompt dei comandi di hello Chiudi.
  >
  >

Se hello che Azure Enhanced Monitoring Extension non è installato o hello AzureEnhancedMonitoring servizio non è in esecuzione, estensione hello non è stato configurato correttamente. Per informazioni dettagliate su come toodeploy hello estensione, vedere [Troubleshooting hello dell'infrastruttura di Azure monitoring per SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Controllare l'output di hello di azperflib.exe
L'output di azperflib.exe visualizza tutti i contatori delle prestazioni di Azure popolati per SAP. Nella parte inferiore di hello dell'elenco di hello di contatori raccolti, un indicatore di stato e di riepilogo Mostra lo stato di hello del monitoraggio di Azure.

![Output del controllo di integrità eseguito con azperflib.exe che indica che non sono presenti problemi][deployment-guide-figure-1100]
<a name="figure-11"></a>

Controllare i risultati di hello restituiti hello **totale contatori** output, che viene segnalato come vuoti e relativo **lo stato di integrità**, come mostrato nella figura precedente hello.

Interpretare i valori risultanti hello come segue:

| Valori dei risultati di azperflib.exe | Stato di integrità del monitoraggio di Azure |
| --- | --- |
| **API Calls - not available** | I contatori che non sono disponibili potrebbero essere entrambe le configurazioni di macchina virtuale non applicabile toohello o errori. Vedere **Health status**. |
| **Counters total - empty** |Hello seguenti due contatori di archiviazione di Azure può essere vuoto: <ul><li>Storage Read Op Latency Server msec</li><li>Storage Read Op Latency E2E msec</li></ul>Tutti gli altri contatori devono avere valori. |
| **Health status** |È positivo solo se lo stato restituito è **OK**. |
| **Diagnostica** |Informazioni dettagliate sullo stato di integrità. |

Se hello **lo stato di integrità** valore non è **OK**, seguire le istruzioni hello [verifica integrità per la configurazione del monitoraggio dell'infrastruttura Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Eseguire il controllo di conformità hello in una VM Linux

1.  Connettersi toohello macchina virtuale di Azure tramite SSH.

2.  Controllare l'output di hello di hello Azure Enhanced Monitoring Extension.

  a.  Eseguire `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Risultato previsto**: restituisce un elenco di contatori delle prestazioni. file Hello non deve essere vuoto.

 b. Eseguire `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Nel risultato previsto**: restituisce una riga in cui errore hello **Nessuno**, ad esempio, **3; config; Errore; 0; 0; Nessuno 0; 1456416792; tst-servercs;**

  c. Eseguire `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Risultato previsto**: viene restituito come vuoto o non esiste.

Se hello controllo precedente non è riuscita, eseguire questi controlli aggiuntivi:

1.  Verificare che il comando waagent hello viene installato e attivato.

  a.  Eseguire `sudo ls -al /var/lib/waagent/`

      **Nel risultato previsto**: Elenca il contenuto di hello della directory waagent hello.

  b.  Eseguire `ps -ax | grep waagent`

   **Risultato previsto**: visualizza una voce simile a `python /usr/sbin/waagent -daemon`

2. Verificare che tale hello estensione diagnostica per Linux viene installato e attivato.

  a.  Eseguire `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`

   **Nel risultato previsto**: Elenca il contenuto di hello di directory dell'estensione diagnostica Linux hello.

 b. Eseguire `ps -ax | grep diagnostic`

   **Risultato previsto**: visualizza una voce simile a `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   Assicurarsi che tale hello Azure Enhanced Monitoring Extension sia installato e in esecuzione.

  a.  Eseguire `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`

    **Nel risultato previsto**: Elenca il contenuto di hello della directory di Azure Enhanced Monitoring Extension hello.

  b. Eseguire `ps -ax | grep AzureEnhanced`

     **Risultato previsto**: visualizza una voce simile a `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Installare l'agente Host SAP come descritto nella nota SAP [1031096]e verificare nell'output di hello `saposcol`.

  a.  Eseguire `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Eseguire `dump ccm`

  c.  Controllare se hello **Virtualization_Configuration\Enhanced monitoraggio accesso** metrica è **true**.

Se è già installato un server applicazioni SAP NetWeaver ABAP, aprire la transazione ST06 e controllare se il monitoraggio avanzato è abilitato.

Se uno di questi controlli avranno esito negativo e per informazioni dettagliate su come tooredeploy hello estensione, vedere [Troubleshooting hello dell'infrastruttura di Azure monitoring per SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Controllo di integrità per hello Azure configurazione del monitoraggio dell'infrastruttura
Se alcuni dei dati di monitoraggio hello non vengono recapitati correttamente come indicato dal test hello descritti in [controllo conformità per Azure Enhanced Monitoring per SAP][deployment-guide-5.1]hello eseguire `Test-AzureRmVMAEMExtension` toocheck cmdlet Se hello Azure monitoring extension per SAP hello e infrastruttura di monitoraggio è configurate correttamente.

1.  Assicurarsi di aver installato una versione più recente di hello del cmdlet di Azure PowerShell hello, come descritto in [cmdlet di distribuzione di Azure PowerShell][deployment-guide-4.1].
2.  Eseguire hello seguente cmdlet di PowerShell. Per un elenco degli ambienti disponibili, eseguire i cmdlet di hello `Get-AzureRmEnvironment`. Selezionare di Azure, pubblica toouse hello **cloud** ambiente. Per Azure in Cina, selezionare **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Immettere i dati dell'account e identificare hello macchina virtuale di Azure.

  ![Pagina di input del cmdlet di Azure specifico di SAP Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. configurazione di hello Hello script test della macchina virtuale hello selezionare.

  ![Output del test riuscito di hello dell'infrastruttura di Azure monitoring per SAP][deployment-guide-figure-1300]

Verificare che il risultato di ogni controllo dell'integrità sia **OK**. Se non vengono visualizzano alcuni controlli **OK**, eseguire i cmdlet di aggiornamento hello, come descritto in [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5]. Attendere 15 minuti e ripetere hello controlli descritti in [controllo conformità per Azure Enhanced Monitoring per SAP] [ deployment-guide-5.1] e [verifica integrità per l'infrastruttura di configurazione di Azure Monitoring] [deployment-guide-5.2]. Se i controlli di hello continuano a indicare un problema con alcuni o tutti i contatori, vedere [Troubleshooting hello dell'infrastruttura di Azure monitoring per SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Risoluzione dei problemi di hello dell'infrastruttura di Azure monitoring per SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] I contatori delle prestazioni di Azure non vengono visualizzati
servizio AzureEnhancedMonitoring Windows Hello raccoglie le metriche delle prestazioni in Azure. Se il servizio di hello non è stato installato correttamente o se non è in esecuzione nella macchina virtuale, è possibile raccogliere alcuna metrica delle prestazioni.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>directory di installazione Hello di hello Azure Enhanced Monitoring Extension è vuota

###### <a name="issue"></a>Problema
directory di installazione Hello c:\\pacchetti\\plug-in\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versione >\\rilascio è vuoto.

###### <a name="solution"></a>Soluzione
estensione Hello non è installato. Determinare se si tratta di un problema del proxy (come descritto prima). Potrebbe essere necessario toorestart hello macchina o eseguire nuovamente hello `Set-AzureRmVMAEMExtension` script di configurazione.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Il servizio per il monitoraggio avanzato di Azure non esiste

###### <a name="issue"></a>Problema
servizio AzureEnhancedMonitoring Windows Hello non esiste.

L'output di azperflib.exe genera un errore:

![Esecuzione di azperflib.exe indica che il servizio di hello di hello Azure Enhanced Monitoring Extension per SAP non è in esecuzione][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Soluzione
Se il servizio di hello non esiste, hello Azure Enhanced Monitoring Extension per SAP non è stato installato correttamente. Ridistribuire l'estensione hello attenendosi alla procedura hello descritta per lo scenario di distribuzione in [scenari di distribuzione di macchine virtuali per SAP in Azure][deployment-guide-3].

Dopo aver distribuito l'estensione di hello, dopo un'ora, controllare di nuovo se i contatori delle prestazioni di Azure hello vengono forniti in hello macchina virtuale di Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Servizio per Azure Enhanced Monitoring esiste, ma ha esito negativo toostart

###### <a name="issue"></a>Problema
servizio AzureEnhancedMonitoring Windows Hello esiste ed è abilitato, ma ha esito negativo toostart. Per ulteriori informazioni, controllare il registro eventi dell'applicazione hello.

###### <a name="solution"></a>Soluzione
configurazione di Hello è corretta. Riavviare hello monitoring extension per hello macchina virtuale, come descritto in [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Alcuni contatori delle prestazioni di Azure non sono presenti
servizio AzureEnhancedMonitoring Windows Hello raccoglie le metriche delle prestazioni in Azure. servizio Hello Ottiene dati da origini diverse. Alcuni dati di configurazione vengono raccolti in locale e alcune metriche delle prestazioni vengono lette da Diagnostica di Azure. I contatori di archiviazione vengono utilizzati dalla registrazione a livello di sottoscrizione di archiviazione hello.

Se la risoluzione dei problemi con la nota SAP [1999351] hello problema persiste, eseguire di nuovo hello `Set-AzureRmVMAEMExtension` script di configurazione. Poiché i contatori di archiviazione analitica o di diagnostica potrebbero non essere creati immediatamente dopo l'abilitazione, potrebbe essere toowait un'ora. Se hello problema persiste, aprire un messaggio del supporto clienti SAP su hello componente BC-OP-NT-AZR per Windows o BC-OP-LNX-AZR per una macchina virtuale di Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] I contatori delle prestazioni di Azure non vengono visualizzati
Le metriche delle prestazioni in Azure vengono raccolte da un daemon. Se i daemon hello non è in esecuzione, non le metriche delle prestazioni possono essere raccolti.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>directory di installazione Hello di hello Azure Enhanced Monitoring extension è vuota

###### <a name="issue"></a>Problema
directory Hello \\var\\lib\\waagent\\ non dispone di una sottodirectory per hello Azure Enhanced Monitoring extension.

###### <a name="solution"></a>Soluzione
estensione Hello non è installato. Determinare se si tratta di un problema del proxy (come descritto prima). Potrebbe essere necessario macchina hello toorestart e/o eseguire di nuovo hello `Set-AzureRmVMAEMExtension` script di configurazione.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Alcuni contatori delle prestazioni di Azure non sono presenti
Le metriche delle prestazioni in Azure vengono raccolte da un daemon, che ottiene i dati da diverse origini. Alcuni dati di configurazione vengono raccolti in locale e alcune metriche delle prestazioni vengono lette da Diagnostica di Azure. I contatori di archiviazione provengono dai registri hello nella sottoscrizione di archiviazione.

Per un elenco completo e aggiornato dei problemi noti, vedere la nota SAP [1999351], che contiene informazioni aggiuntive sulla risoluzione dei problemi per il monitoraggio avanzato di Azure per SAP.

Se la risoluzione dei problemi con la nota SAP [1999351] non risolvere il problema di hello, eseguire di nuovo hello `Set-AzureRmVMAEMExtension` script di configurazione come descritto in [Configura hello Azure Enhanced Monitoring Extension per SAP][deployment-guide-4.5]. Poiché i contatori di archiviazione analitica o di diagnostica potrebbero non essere creati immediatamente dopo l'abilitazione, potrebbe essere toowait per un'ora. Se hello problema persiste, aprire un messaggio del supporto clienti SAP su hello componente BC-OP-NT-AZR per Windows o BC-OP-LNX-AZR per una macchina virtuale di Linux.
