---
title: Introduzione alle soluzioni SAP in macchine virtuali di Azure | Microsoft Docs
description: Informazioni sulle soluzioni SAP in esecuzione sulle macchine virtuali (VM) in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7a7768862defb4ab3dec65dfad3eacb985940af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a><span data-ttu-id="e4767-103">Utilizzo di Azure per l'hosting e l'esecuzione di scenari con carichi di lavoro SAP</span><span class="sxs-lookup"><span data-stu-id="e4767-103">Using Azure for hosting and running SAP workload scenarios</span></span>
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

[dbms-guide]:dbms-guide.md 
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md 
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e 
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 
[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

<span data-ttu-id="e4767-104">Scegliendo Microsoft Azure come partner cloud per SAP, sarà possibile eseguire in modo affidabile gli scenari e i carichi di lavoro SAP mission critical in una piattaforma scalabile, conforme e comprovata per le aziende,</span><span class="sxs-lookup"><span data-stu-id="e4767-104">By choosing Microsoft Azure as your SAP ready cloud partner, you are able to reliably run your mission critical SAP workloads and scenarios on a scalable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="e4767-105">nonché ottenere la scalabilità, la flessibilità e la convenienza di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-105">Get the scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="e4767-106">Grazie alla partnership estesa tra Microsoft e SAP, è possibile eseguire applicazioni SAP in scenari di sviluppo/test e di produzione in Azure con il supporto completo.</span><span class="sxs-lookup"><span data-stu-id="e4767-106">With the expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in Azure - and be fully supported.</span></span> <span data-ttu-id="e4767-107">Da SAP NetWeaver a SAP S4/HANA, SAP BI, da Linux a Windows, da SAP HANA a SQL, viene offerto supporto per tutte le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="e4767-107">From SAP NetWeaver to SAP S4/HANA, SAP BI, Linux to Windows, SAP HANA to SQL, we have you covered.</span></span> 

<span data-ttu-id="e4767-108">Oltre all'hosting di scenari SAP NetWeaver con diversi DBMS in Azure, è possibile eseguire l'hosting di diversi altri scenari di carico di lavoro SAP, come SAP BI in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-108">Besides hosting SAP NetWeaver scenarios with the different DBMS on Azure, you can host different other SAP workload scenarios, like SAP BI on Azure.</span></span> <span data-ttu-id="e4767-109">La documentazione relativa alle distribuzioni di SAP NetWeaver nelle macchine virtuali di Azure native è disponibile nella sezione "SAP NetWeaver in Macchine virtuali di Azure".</span><span class="sxs-lookup"><span data-stu-id="e4767-109">Documentation regarding SAP NetWeaver deployments on Azure native Virtual Machines can be found in the section "SAP NetWeaver on Azure Virtual Machines."</span></span> 

<span data-ttu-id="e4767-110">Le offerte di macchine virtuali di Azure native prevedono dimensioni crescenti a livello di risorse di CPU e memoria per soddisfare il carico di lavoro SAP basato su SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e4767-110">Azure has native Azure Virtual Machine offers that are ever growing in size of CPU and memory resources to cover SAP workload that leverages SAP HANA.</span></span> <span data-ttu-id="e4767-111">Per altre informazioni su questo argomento, vedere i documenti nella sezione SAP HANA sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-111">For more information on this topic, look up the documents under the section SAP HANA on Azure Virtual Machines."</span></span>

<span data-ttu-id="e4767-112">L'univocità di Azure per SAP HANA è rappresentata da un'offerta esclusiva che differenzia Azure dalla concorrenza.</span><span class="sxs-lookup"><span data-stu-id="e4767-112">The uniqueness of Azure for SAP HANA is a unique offer that sets Azure apart from competition.</span></span> <span data-ttu-id="e4767-113">Per abilitare l'hosting di scenari SAP complessi con SAP HANA che richiedono più risorse della CPU e della memoria, Azure offre l'utilizzo di hardware bare metal dedicato al cliente per eseguire distribuzioni SAP HANA che richiedono fino a 20 TB (scalabilità orizzontale di 60 TB) di memoria per S/4HANA o un altro carico di lavoro SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e4767-113">In order to enable hosting more memory and CPU resource demanding SAP scenarios involving SAP HANA, Azure offers the usage of customer dedicated bare-metal hardware for the purpose of running SAP HANA deployments that require up to 20 TB (60 TB scale-out) of memory for S/4HANA or other SAP HANA workload.</span></span> <span data-ttu-id="e4767-114">Questa esclusiva soluzione Azure di SAP HANA in Azure (istanze di grandi dimensioni) consente di eseguire SAP HANA su hardware bare metal dedicato con il livello dell'applicazione SAP o il livello del middleware dei carichi di lavoro ospitato nelle macchine virtuali di Azure native.</span><span class="sxs-lookup"><span data-stu-id="e4767-114">This unique Azure solution of SAP HANA on Azure (Large Instances) allows you to run SAP HANA on the dedicated bare-metal hardware with the SAP application layer or workload middle-ware layer hosted in native Azure Virtual Machines.</span></span> <span data-ttu-id="e4767-115">Questa soluzione è descritta in diversi documenti nella sezione "SAP HANA in Azure (istanze di grandi dimensioni)".</span><span class="sxs-lookup"><span data-stu-id="e4767-115">This solution is documented in several documents in the section "SAP HANA on Azure (Large Instances)."</span></span>   

<span data-ttu-id="e4767-116">L'hosting di scenari di carichi di lavoro SAP in Azure consente anche di creare i requisiti di integrazione della soluzione di gestione delle identità e Single Sign-On usando Azure Active Directory in vari componenti SAP e offerte SAP di tipo SaaS o PaaS.</span><span class="sxs-lookup"><span data-stu-id="e4767-116">Hosting SAP workload scenarios in Azure also can create requirements of Identity integration and Single-Sign-On using Azure Activity Directory to different SAP components and SAP SaaS or PaaS offers.</span></span> <span data-ttu-id="e4767-117">La sezione sull'integrazione della soluzione di gestione delle identità e Single Sign-On SAP AAD descrive e illustra un elenco di questi scenari di integrazione e Single Sign-On con Azure Active Directory (AAD) ed entità SAP.</span><span class="sxs-lookup"><span data-stu-id="e4767-117">A list of such integration and Single-Sign-On scenarios with Azure Active Directory (AAD) and SAP entities is described and documented in the section "AAD SAP Identity Integration and Single-Sign-On."</span></span>


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-118">SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-118">SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-119">Panoramica e architettura di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="e4767-120">Titolo: Panoramica e architettura di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-120">Title: Overview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="e4767-121">Riepilogo: Questa guida sull'architettura e la distribuzione tecnica di SAP offre informazioni sulle modalità di distribuzione di SAP nella nuova piattaforma SAP HANA in Azure (istanze di grandi dimensioni).</span><span class="sxs-lookup"><span data-stu-id="e4767-121">Summary: This Architecture and Technical Deployment Guide provides information to help you deploy SAP on the new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="e4767-122">Non è stata concepita per essere una guida completa sull'installazione specifica di soluzioni SAP, ma per offrire utili informazioni sulla distribuzione iniziale e le operazioni successive.</span><span class="sxs-lookup"><span data-stu-id="e4767-122">It is not intended to be a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="e4767-123">Non deve essere usata in sostituzione della documentazione di SAP correlata all'installazione di SAP HANA o delle varie note di supporto SAP che riguardano l'argomento.</span><span class="sxs-lookup"><span data-stu-id="e4767-123">It should not replace SAP documentation related to the installation of SAP HANA (or the many SAP Support Notes that cover the topic).</span></span> <span data-ttu-id="e4767-124">Offre semplicemente una panoramica e informazioni specifiche sull'installazione di SAP HANA in Azure (istanze di grandi dimensioni).</span><span class="sxs-lookup"><span data-stu-id="e4767-124">It gives you an overview and provides the additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="e4767-125">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-125">Updated: July 2017</span></span>

[<span data-ttu-id="e4767-126">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-to-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-127">Infrastruttura e connettività a SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-127">Infrastructure and connectivity to SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="e4767-128">Titolo: Infrastruttura e connettività a SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-128">Title: Infrastructure and Connectivity to SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="e4767-129">Riepilogo: Dopo aver finalizzato l'acquisto di SAP HANA in Azure (istanze di grandi dimensioni) con il team Microsoft dedicato agli account aziendali, per garantire una connettività appropriata è necessario eseguire alcune configurazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="e4767-129">Summary: After the purchase of SAP HANA on Azure (Large Instances) is finalized between you and the Microsoft enterprise account team, various network configurations are required in order to ensure proper connectivity.</span></span>  <span data-ttu-id="e4767-130">Questo documento descrive le informazioni che devono essere condivise e le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="e4767-130">This document outlines the information that has to be shared with the following information is required.</span></span> <span data-ttu-id="e4767-131">In particolare, descrive quali informazioni devono essere raccolte e quali script di configurazione devono essere eseguiti.</span><span class="sxs-lookup"><span data-stu-id="e4767-131">This document outlines what information has to be collected and what configuration scripts have to be run.</span></span> 

<span data-ttu-id="e4767-132">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-132">Updated: July 2017</span></span>

[<span data-ttu-id="e4767-133">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-134">Installare SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-134">Install SAP HANA in SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="e4767-135">Titolo: Installare SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-135">Title: Install SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="e4767-136">Riepilogo: Questo documento descrive le procedure necessarie per l'installazione di SAP HANA nell'istanza di grandi dimensioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-136">Summary: This document outlines the setup procedures for installing SAP HANA on your Azure Large Instance.</span></span> 

<span data-ttu-id="e4767-137">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-137">Updated: July 2017</span></span>

[<span data-ttu-id="e4767-138">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-139">Disponibilità elevata e ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="e4767-140">Titolo: Disponibilità elevata e ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-140">Title: High Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="e4767-141">Riepilogo: La disponibilità elevata e il ripristino di emergenza sono aspetti importanti dell'esecuzione di sistemi SAP HANA cruciali nei server di Azure (istanze di grandi dimensioni).</span><span class="sxs-lookup"><span data-stu-id="e4767-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="e4767-142">La collaborazione con SAP, l'integratore di sistemi e/o Microsoft è fondamentale per progettare e implementare correttamente la strategia di disponibilità elevata e ripristino di emergenza adatta alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="e4767-142">It's import to work with SAP, your system integrator, and/or Microsoft to properly architect and implement the right HA/DR strategy for you.</span></span> <span data-ttu-id="e4767-143">È inoltre necessario prendere in considerazione alcuni fattori significativi, come l'RPO (Recovery Point Objective, obiettivo del punto di ripristino) e l'RTO (Recovery Time Objective, obiettivo del tempo di ripristino), specifici del proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="e4767-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific to your environment, must be considered.</span></span>  <span data-ttu-id="e4767-144">Questo documento illustra le opzioni disponibili per abilitare i livelli desiderati di disponibilità elevata e ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="e4767-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="e4767-145">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="e4767-145">Updated: December 2016</span></span>

[<span data-ttu-id="e4767-146">Questo documento è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="e4767-147">Risoluzione dei problemi e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="e4767-148">Titolo: Risoluzione dei problemi e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="e4767-148">Title: Troubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="e4767-149">Riepilogo: Questa guida offre informazioni utili per definire il monitoraggio di SAP HANA in ambiente Azure e informazioni aggiuntive sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e4767-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="e4767-150">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="e4767-150">Updated: December 2016</span></span>

[<span data-ttu-id="e4767-151">Questo documento è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a><span data-ttu-id="e4767-152">SAP HANA nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-152">SAP HANA on Azure Virtual Machines</span></span>

### <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="e4767-153">Introduzione a SAP HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-153">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="e4767-154">Titolo: Guida introduttiva per l'installazione manuale di SAP HANA nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-154">Title: Quickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="e4767-155">Riepilogo: Questa guida introduttiva consente di configurare un sistema SAP HANA a istanza singola nelle VM di Azure mediante un'installazione manuale di SAP NetWeaver 7.5 e SAP HANA SP12.</span><span class="sxs-lookup"><span data-stu-id="e4767-155">Summary: This quickstart guide helps to set up a single-instance SAP HANA system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="e4767-156">La guida presuppone che il lettore abbia familiarità con nozioni fondamentali di IaaS di Azure come la distribuzione di macchine virtuali o di reti virtuali tramite il portale di Azure o PowerShell/interfaccia della riga di comando, inclusa la possibilità di usare modelli JSON.</span><span class="sxs-lookup"><span data-stu-id="e4767-156">The guide presumes that the reader is familiar with Azure IaaS basics like how to deploy virtual machines or virtual networks either via the Azure portal or Powershell/CLI including the option to use json templates.</span></span> <span data-ttu-id="e4767-157">Si presuppone anche che il lettore abbia familiarità con SAP HANA, SAP NetWeaver e la relativa installazione locale.</span><span class="sxs-lookup"><span data-stu-id="e4767-157">Furthermore it's expected that the reader is familiar with SAP HANA, SAP NetWeaver and how to install it on-premises.</span></span>

<span data-ttu-id="e4767-158">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-158">Updated: June 2017</span></span>

[<span data-ttu-id="e4767-159">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-159">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a><span data-ttu-id="e4767-160">Distribuzione di S/4HANA SAP CAL in Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-160">S/4HANA SAP CAL deployment on Azure</span></span>
<span data-ttu-id="e4767-161">Titolo: Distribuire SAP S/4HANA o BW/4HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-161">Title: Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>

<span data-ttu-id="e4767-162">Riepilogo: Questa Guida consente di dimostrare la distribuzione di SAP S/4HANA in Azure mediante SAP Cloud Appliance Library.</span><span class="sxs-lookup"><span data-stu-id="e4767-162">Summary: This guide helps to demonstrate the deployment of SAP S/4HANA on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="e4767-163">SAP Cloud Appliance Library è un servizio di SAP che consente di distribuire applicazioni SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-163">SAP Cloud Appliance Library is a service by SAP that allows to deploy SAP applications on Azure.</span></span> <span data-ttu-id="e4767-164">La guida descrive dettagliatamente la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e4767-164">The guide describes step by step the deployment.</span></span>

<span data-ttu-id="e4767-165">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-165">Updated: June 2017</span></span>

[<span data-ttu-id="e4767-166">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-166">This guide can be found here</span></span>](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a><span data-ttu-id="e4767-167">Disponibilità elevata di SAP HANA in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-167">High Availability of SAP HANA in Azure Virtual Machines</span></span>
<span data-ttu-id="e4767-168">Titolo: Disponibilità elevata di SAP HANA in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-168">Title: High Availability of SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="e4767-169">Riepilogo: Questa guida presenta la procedura passo per passo per la configurazione della disponibilità elevata del sistema operativo SUSE 12 e di SAP HANA per il supporto della replica del sistema HANA con failover automatico.</span><span class="sxs-lookup"><span data-stu-id="e4767-169">Summary: This guide leads you through the high availability configuration of the SUSE 12 OS and SAP HANA to accommodate HANA System replication with automatic failover.</span></span> <span data-ttu-id="e4767-170">La guida è specifica per SUSE e Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-170">The guide is specific for SUSE and Azure Virtual Machines.</span></span> <span data-ttu-id="e4767-171">La guida non si applica tuttavia a Red Hat, bare metal, cloud privato o altre distribuzioni di cloud pubblici non Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-171">The guide does not apply yet for Red Hat or bare-metal or private cloud or other non-Azure public cloud deployments.</span></span>

<span data-ttu-id="e4767-172">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-172">Updated: June 2017</span></span>

[<span data-ttu-id="e4767-173">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-173">This guide can be found here</span></span>](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a><span data-ttu-id="e4767-174">Panoramica del backup di SAP HANA nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-174">SAP HANA backup overview on Azure VMs</span></span>
<span data-ttu-id="e4767-175">Titolo: Guida del backup di SAP HANA in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-175">Title: Backup guide for SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="e4767-176">Riepilogo: Questa guida fornisce informazioni di base sulle possibilità di backup quando si esegue SAP HANA in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-176">Summary: This guide provides basic information about backup possibilities running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="e4767-177">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-177">Updated: March 2017</span></span>

[<span data-ttu-id="e4767-178">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-178">This guide can be found here</span></span>](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a><span data-ttu-id="e4767-179">Backup di SAP HANA a livello di file in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-179">SAP HANA file level backup on Azure VMs</span></span>
<span data-ttu-id="e4767-180">Titolo: Backup di SAP HANA basato su snapshot di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e4767-180">Title: SAP HANA backup based on storage snapshots</span></span>

<span data-ttu-id="e4767-181">Riepilogo: Questa guida fornisce informazioni sull'uso di backup basati su snapshot in VM di Azure durante l'esecuzione di SAP HANA su Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-181">Summary: This guide provides information about using snapshot-based backups on Azure VMs when running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="e4767-182">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-182">Updated: March 2017</span></span>

[<span data-ttu-id="e4767-183">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-183">This guide can be found here</span></span>](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a><span data-ttu-id="e4767-184">Backup di SAP HANA basati su snapshot in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-184">SAP HANA snapshot based backups on Azure VMs</span></span>
<span data-ttu-id="e4767-185">Titolo: Backup di SAP HANA di Azure a livello di file</span><span class="sxs-lookup"><span data-stu-id="e4767-185">Title: SAP HANA Azure Backup on file level</span></span>

<span data-ttu-id="e4767-186">Riepilogo: Questa guida fornisce informazioni sull'uso di backup di SAP HANA a livello di file durante l'esecuzione di SAP HANA su macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-186">Summary: This guide provides information about using SAP HANA file level backup running SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="e4767-187">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-187">Updated: March 2017</span></span>

[<span data-ttu-id="e4767-188">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-188">This guide can be found here</span></span>](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a><span data-ttu-id="e4767-189">SAP NetWeaver distribuito in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-189">SAP NetWeaver deployed on Azure Virtual Machines</span></span>

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a><span data-ttu-id="e4767-190">Distribuire il sistema SAP IDES in Windows e SQL Server mediante SAP CAL in Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-190">Deploy SAP IDES system on Windows and SQL Server through SAP CAL on Azure</span></span>
<span data-ttu-id="e4767-191">Titolo: Test di SAP NetWeaver nelle macchine virtuali SUSE Linux di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-191">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="e4767-192">Riepilogo: Questo documento descrive la distribuzione di un sistema SAP IDES basato su Windows e SQL Server in Azure mediante SAP Cloud Appliance Library.</span><span class="sxs-lookup"><span data-stu-id="e4767-192">Summary: This document describes the deployment of an SAP IDES system based on Windows and SQL Server on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="e4767-193">SAP Cloud appliance Library è un servizio SAP che consente la distribuzione di prodotti SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-193">SAP Cloud appliance Library is an SAP service that allows the deployment of SAP products on Azure.</span></span> <span data-ttu-id="e4767-194">Questo documento descrive passo per passo la distribuzione di un sistema SAP IDES.</span><span class="sxs-lookup"><span data-stu-id="e4767-194">This document goes step by step through the deployment of an SAP IDES system.</span></span> <span data-ttu-id="e4767-195">Il sistema IDES è solo un esempio di molte altre decine di applicazioni che possono essere distribuite attraverso appliance cloud SAP in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-195">The IDES system is just an example for several other dozen applications that can be deployed through SAP Cloud appliance on Microsoft Azure.</span></span>

<span data-ttu-id="e4767-196">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-196">Updated: June 2017</span></span>

[<span data-ttu-id="e4767-197">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-197">This guide can be found here</span></span>](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="e4767-198">Guida rapida per NetWeaver su SUSE Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-198">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="e4767-199">Titolo: Test di SAP NetWeaver nelle macchine virtuali SUSE Linux di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-199">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="e4767-200">Riepilogo: Questo articolo descrive vari aspetti da considerare quando si esegue SAP NetWeaver in macchine virtuali (VM) SUSE Linux di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-200">Summary: This article describes various things to consider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="e4767-201">SAP NetWeaver è ufficialmente supportato nelle macchine virtuali SUSE Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-201">SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="e4767-202">Tutti i dettagli riguardanti le versioni di Linux, le versioni del kernel SAP e altre informazioni sono reperibili nella nota 1928533 di SAP "SAP Applications on Azure: Supported Products and Azure VM types" (Applicazioni SAP in Azure: prodotti supportati e i tipi di VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="e4767-202">All details regarding Linux versions, SAP kernel versions, and other details can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="e4767-203">Ultimo aggiornamento: settembre 2016</span><span class="sxs-lookup"><span data-stu-id="e4767-203">Updated: September 2016</span></span>

[<span data-ttu-id="e4767-204">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-204">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="e4767-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Pianificazione e implementazione</span><span class="sxs-lookup"><span data-stu-id="e4767-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and implementation</span></span>
<span data-ttu-id="e4767-206">Titolo: Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e4767-206">Title: Azure Virtual Machines planning and implementation for SAP NetWeaver</span></span>

<span data-ttu-id="e4767-207">Riepilogo: Questo documento è una guida introduttiva utile se si sta valutando la possibilità di eseguire SAP NetWeaver in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-207">Summary: This document is the guide to start with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="e4767-208">Questa Guida alla pianificazione e implementazione permette di valutare se è possibile distribuire un sistema basato su SAP NetWeaver esistente o pianificato in un ambiente di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-208">This planning and implementation guide helps you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed to an Azure Virtual Machines environment.</span></span> <span data-ttu-id="e4767-209">Illustra vari scenari di distribuzione di SAP NetWeaver e include configurazioni SAP specifiche per Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-209">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific to Azure.</span></span> <span data-ttu-id="e4767-210">Il documento elenca e descrive tutte le informazioni di configurazione necessarie relative a SAP/Azure per eseguire un landscape SAP ibrido.</span><span class="sxs-lookup"><span data-stu-id="e4767-210">The paper lists and describes all the necessary configuration information you’ll need on the SAP/Azure side to run a hybrid SAP landscape.</span></span> <span data-ttu-id="e4767-211">Vengono anche descritte le misure che è possibile adottare per garantire la disponibilità elevata dei sistemi basati su SAP NetWeaver nella soluzione IaaS.</span><span class="sxs-lookup"><span data-stu-id="e4767-211">Measures you can take to ensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="e4767-212">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-212">Updated: June 2017</span></span>

<span data-ttu-id="e4767-213">[Questa guida è disponibile qui][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e4767-213">[This guide can be found here][planning-guide]</span></span>

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="e4767-214">Configurazioni a disponibilità elevata di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-214">High Availability configurations of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="e4767-215">Titolo: Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e4767-215">Title: Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="e4767-216">Riepilogo: Questo documento illustra la procedura che è possibile eseguire per distribuire sistemi SAP a disponibilità elevata in Azure, usando il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e4767-216">Summary: In this document, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e4767-217">Le attività principali che verranno illustrate sono le seguenti.</span><span class="sxs-lookup"><span data-stu-id="e4767-217">We walk you through these major tasks.</span></span> <span data-ttu-id="e4767-218">Il documento descrive come proteggere i componenti con un singolo punto di guasto in Azure, ad esempio Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) e i sistemi di gestione di database (DBMS), oltre ai componenti ridondanti, ad esempio i server applicazioni SAP, eseguiti nelle VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-218">In the document, we describe how single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server are going to be protected when running in Azure VMs.</span></span> <span data-ttu-id="e4767-219">Questo documento riporta la dimostrazione passo per passo di un esempio di installazione e configurazione di un sistema SAP a disponibilità elevata in un cluster Windows Server Failover Clustering in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-219">A step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure is demonstrated and shown in this document.</span></span>

<span data-ttu-id="e4767-220">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-220">Updated: June 2017</span></span>

[<span data-ttu-id="e4767-221">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-221">This guide can be found here</span></span>](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="e4767-222">Realizzazione di distribuzioni a più SID di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-222">Realizing Multi-SID deployments of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="e4767-223">Titolo: Creare una configurazione di SAP NetWeaver a più SID</span><span class="sxs-lookup"><span data-stu-id="e4767-223">Title: Create an SAP NetWeaver multi-SID configuration</span></span> 

<span data-ttu-id="e4767-224">Riepilogo: Questo documento costituisce un'aggiunta al documento sulla disponibilità elevata per SAP NetWeaver in VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-224">Summary: This document is an addition to the document High availability for SAP NetWeaver on Azure VMs.</span></span> <span data-ttu-id="e4767-225">A causa di nuove funzionalità di Azure introdotte nel settembre 2016, è possibile distribuire più istanze di SAP NetWeaver ASCS/SCS in una coppia di VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-225">Due to new functionality in Azure that got introduced in September 2016, it is possible to deploy multiple SAP NetWeaver ASCS/SCS instances in a pair of Azure VMs.</span></span> <span data-ttu-id="e4767-226">Con questa configurazione è possibile ridurre il numero di VM distribuite per realizzare configurazioni a disponibilità elevata di SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="e4767-226">With such a configuration, you can reduce the number of VMs necessary to deploy to realize highly available SAP NetWeaver configurations.</span></span> <span data-ttu-id="e4767-227">La guida descrive l'impostazione di tali configurazioni a più SID.</span><span class="sxs-lookup"><span data-stu-id="e4767-227">The guide describes the setup of such multi-SID configurations.</span></span>

<span data-ttu-id="e4767-228">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="e4767-228">Updated: December 2016</span></span>

[<span data-ttu-id="e4767-229">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-229">This guide can be found here</span></span>](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="e4767-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Distribuzione di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="e4767-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="e4767-231">Titolo: Distribuzione di Macchine virtuali di Azure per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e4767-231">Title: Azure Virtual Machines deployment for SAP NetWeaver</span></span>

<span data-ttu-id="e4767-232">Riepilogo: In questo documento vengono fornite indicazioni generali sulle procedure per la distribuzione del software SAP NetWeaver nelle macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-232">Summary: This document provides procedural guidance for deploying SAP NetWeaver software to virtual machines in Azure.</span></span> <span data-ttu-id="e4767-233">Questo documento descrive tre scenari di distribuzione specifici, con particolare attenzione all'abilitazione delle estensioni di monitoraggio di Azure per SAP, inclusi alcuni suggerimenti per la risoluzione dei problemi delle estensioni di monitoraggio di Azure per SAP.</span><span class="sxs-lookup"><span data-stu-id="e4767-233">This paper focuses on three specific deployment scenarios, with an emphasis on enabling the Azure Monitoring Extensions for SAP, including troubleshooting recommendations for the Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="e4767-234">Prima di passare a questo documento, è necessario aver letto la Guida alla pianificazione e all'implementazione.</span><span class="sxs-lookup"><span data-stu-id="e4767-234">This paper assumes that you’ve read the planning and implementation guide.</span></span>

<span data-ttu-id="e4767-235">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-235">Updated: June 2017</span></span>

<span data-ttu-id="e4767-236">[Questa guida è disponibile qui][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e4767-236">[This guide can be found here][deployment-guide]</span></span>

### <span data-ttu-id="e4767-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guida alla distribuzione DBMS</span><span class="sxs-lookup"><span data-stu-id="e4767-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS deployment guide</span></span>
<span data-ttu-id="e4767-238">Titolo: Distribuzione DBMS di Macchine virtuali di Azure per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e4767-238">Title: Azure Virtual Machines DBMS deployment for SAP NetWeaver</span></span>

<span data-ttu-id="e4767-239">Riepilogo: Questo documento presenta le considerazioni sulla pianificazione e l'implementazione per i sistemi DBMS che dovranno essere eseguiti con SAP.</span><span class="sxs-lookup"><span data-stu-id="e4767-239">Summary: This paper covers planning and implementation considerations for the DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="e4767-240">Nella prima parte vengono elencate e presentate alcune considerazioni di carattere generale.</span><span class="sxs-lookup"><span data-stu-id="e4767-240">In the first part, general considerations are listed and presented.</span></span> <span data-ttu-id="e4767-241">Le parti successive descrivono invece le distribuzioni supportate da SAP di diversi sistemi DBMS in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-241">The following parts of the paper relate to deployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="e4767-242">I sistemi DBMS presentati sono SQL Server, SAP ASE e Oracle.</span><span class="sxs-lookup"><span data-stu-id="e4767-242">Different DBMS presented are SQL Server, SAP ASE, and Oracle.</span></span> <span data-ttu-id="e4767-243">In queste sezioni più specifiche vengono illustrate le considerazioni di cui è necessario tenere conto quando si eseguono sistemi SAP con tali sistemi DBMS in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4767-243">In those specific parts, considerations you have to account for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="e4767-244">Vengono presentati argomenti quali i metodi di backup e disponibilità elevata supportati dai diversi sistemi DBMS in Azure per l'utilizzo con applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="e4767-244">Subjects like backup and high availability methods that are supported by the different DBMS on Azure are presented for the usage with SAP applications.</span></span>

<span data-ttu-id="e4767-245">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-245">Updated: June 2017</span></span>

<span data-ttu-id="e4767-246">[Questa guida è disponibile qui][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e4767-246">[This guide can be found here][dbms-guide]</span></span>

### <a name="using-azure-site-recovery-for-sap-workload"></a><span data-ttu-id="e4767-247">Utilizzo di Azure Site Recovery per un carico di lavoro SAP</span><span class="sxs-lookup"><span data-stu-id="e4767-247">Using Azure Site Recovery for SAP workload</span></span>
<span data-ttu-id="e4767-248">Titolo: SAP NetWeaver - Creazione di una soluzione di ripristino di emergenza con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e4767-248">Title: SAP NetWeaver: Building a Disaster Recovery Solution with Azure Site Recovery</span></span> 

<span data-ttu-id="e4767-249">Riepilogo: Questo documento descrive come è possibile usare i servizi Azure Site Recovery per gestire scenari di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="e4767-249">Summary: This document describes the way how Azure Site Recovery services can be used for the purpose of handling disaster recovery scenarios.</span></span> <span data-ttu-id="e4767-250">Casi in cui è possibile usare Azure come posizione di ripristino di emergenza per un landscape SAP locale mediante i servizi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e4767-250">Cases where Azure is used as disaster recovery location for an on-premise SAP landscape using Azure Site Recovery Services.</span></span> <span data-ttu-id="e4767-251">In questo documento è descritta anche la procedura per gestire un caso di ripristino di emergenza A2A (da Azure ad Azure) con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e4767-251">Another scenario described in the document is the Aure-to-Azure (A2A) disaster recovery case and how it is managed with Azure Site Recovery.</span></span>  

<span data-ttu-id="e4767-252">Ultimo aggiornamento: agosto 2017</span><span class="sxs-lookup"><span data-stu-id="e4767-252">Updated: August 2017</span></span>

[<span data-ttu-id="e4767-253">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="e4767-253">This guide can be found here</span></span>](http://aka.ms/asr-sap)

