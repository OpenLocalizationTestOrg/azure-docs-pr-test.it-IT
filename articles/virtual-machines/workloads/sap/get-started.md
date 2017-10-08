---
title: aaaGetting avviato con SAP in macchine virtuali di Azure | Documenti Microsoft
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
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a><span data-ttu-id="c16b1-103">Utilizzo di Azure per l'hosting e l'esecuzione di scenari con carichi di lavoro SAP</span><span class="sxs-lookup"><span data-stu-id="c16b1-103">Using Azure for hosting and running SAP workload scenarios</span></span>
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

<span data-ttu-id="c16b1-104">Se si sceglie Microsoft Azure come partner di cloud pronto SAP, sono tooreliably in grado di eseguire i carichi di lavoro di importanza critiche SAP e scenari su una piattaforma scalabile, conformo e rivelati enterprise.</span><span class="sxs-lookup"><span data-stu-id="c16b1-104">By choosing Microsoft Azure as your SAP ready cloud partner, you are able tooreliably run your mission critical SAP workloads and scenarios on a scalable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="c16b1-105">Ottenere la scalabilità hello, flessibilità e risparmi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-105">Get hello scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="c16b1-106">Con hello espanso collaborazione tra Microsoft e SAP, è possibile eseguire applicazioni SAP in scenari di sviluppo e test e di produzione in Azure - e sia completamente supportato.</span><span class="sxs-lookup"><span data-stu-id="c16b1-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in Azure - and be fully supported.</span></span> <span data-ttu-id="c16b1-107">Da SAP NetWeaver tooSAP S4/HANA, SAP BI, tooWindows Linux, tooSQL SAP HANA, sono disponibili per te.</span><span class="sxs-lookup"><span data-stu-id="c16b1-107">From SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="c16b1-108">Oltre a scenari SAP NetWeaver con host hello diversi DBMS in Azure, è possibile ospitare diversi altri scenari di carico di lavoro SAP, come SAP BI in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-108">Besides hosting SAP NetWeaver scenarios with hello different DBMS on Azure, you can host different other SAP workload scenarios, like SAP BI on Azure.</span></span> <span data-ttu-id="c16b1-109">La documentazione relativa a distribuzioni di SAP NetWeaver in macchine virtuali di Azure nativo è reperibile nella sezione hello "SAP NetWeaver in macchine virtuali di Azure".</span><span class="sxs-lookup"><span data-stu-id="c16b1-109">Documentation regarding SAP NetWeaver deployments on Azure native Virtual Machines can be found in hello section "SAP NetWeaver on Azure Virtual Machines."</span></span> 

<span data-ttu-id="c16b1-110">Azure offre native offerte di macchina virtuale di Azure che sono in continua crescita dimensioni di CPU e memoria risorse toocover SAP carico di lavoro che si avvale di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c16b1-110">Azure has native Azure Virtual Machine offers that are ever growing in size of CPU and memory resources toocover SAP workload that leverages SAP HANA.</span></span> <span data-ttu-id="c16b1-111">Per ulteriori informazioni su questo argomento, cercare documenti hello nella sezione hello SAP HANA in macchine virtuali di Azure."</span><span class="sxs-lookup"><span data-stu-id="c16b1-111">For more information on this topic, look up hello documents under hello section SAP HANA on Azure Virtual Machines."</span></span>

<span data-ttu-id="c16b1-112">l'univocità Hello di Azure per SAP HANA è un'offerta univoca che differenzia la concorrenza di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-112">hello uniqueness of Azure for SAP HANA is a unique offer that sets Azure apart from competition.</span></span> <span data-ttu-id="c16b1-113">In ordine tooenable hosting di più memoria e risorse della CPU SAP complesse scenari che implicano SAP HANA, Azure offre utilizzo hello del cliente dedicato hardware bare metal scopo hello di distribuzioni di SAP HANA che richiedono backup too20 TB (scalabilità 60 TB) di in esecuzione memoria per S/4HANA o altro carico di lavoro di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c16b1-113">In order tooenable hosting more memory and CPU resource demanding SAP scenarios involving SAP HANA, Azure offers hello usage of customer dedicated bare-metal hardware for hello purpose of running SAP HANA deployments that require up too20 TB (60 TB scale-out) of memory for S/4HANA or other SAP HANA workload.</span></span> <span data-ttu-id="c16b1-114">Questa soluzione Azure di SAP HANA in Azure (istanze di grandi dimensioni) consente toorun SAP HANA hardware bare metal hello dedicato con livello di applicazione SAP hello o un livello di middleware del carico di lavoro ospitato in macchine virtuali di Azure di tipo nativo.</span><span class="sxs-lookup"><span data-stu-id="c16b1-114">This unique Azure solution of SAP HANA on Azure (Large Instances) allows you toorun SAP HANA on hello dedicated bare-metal hardware with hello SAP application layer or workload middle-ware layer hosted in native Azure Virtual Machines.</span></span> <span data-ttu-id="c16b1-115">Questa soluzione è documentata in diversi documenti nella sezione hello "SAP HANA in Azure (istanze di grandi dimensioni)".</span><span class="sxs-lookup"><span data-stu-id="c16b1-115">This solution is documented in several documents in hello section "SAP HANA on Azure (Large Instances)."</span></span>   

<span data-ttu-id="c16b1-116">Scenari di carico di lavoro SAP in Azure di hosting anche creare i requisiti di integrazione delle identità e Single Sign-On utilizzando componenti di Azure Directory attività toodifferent SAP e SAP SaaS offre PaaS.</span><span class="sxs-lookup"><span data-stu-id="c16b1-116">Hosting SAP workload scenarios in Azure also can create requirements of Identity integration and Single-Sign-On using Azure Activity Directory toodifferent SAP components and SAP SaaS or PaaS offers.</span></span> <span data-ttu-id="c16b1-117">Un elenco di tale integrazione e scenari di Single Sign-On con Azure Active Directory (AAD) e SAP entità è descritti e illustrato nella sezione hello "SAP AAD dell'integrazione delle identità e Single Sign-On."</span><span class="sxs-lookup"><span data-stu-id="c16b1-117">A list of such integration and Single-Sign-On scenarios with Azure Active Directory (AAD) and SAP entities is described and documented in hello section "AAD SAP Identity Integration and Single-Sign-On."</span></span>


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-118">SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-118">SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-119">Panoramica e architettura di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="c16b1-120">titolo: aaaOverview e architettura di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-120">title: aaaOverview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c16b1-121">Riepilogo: Questa architettura tecnica Guida alla distribuzione e fornisce informazioni toohelp la distribuzione di SAP in hello nuovo SAP HANA in Azure (istanze di grandi dimensioni) in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-121">Summary: This Architecture and Technical Deployment Guide provides information toohelp you deploy SAP on hello new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="c16b1-122">Non è una guida completa copertura specifico il programma di installazione di soluzioni SAP, ma piuttosto utile informazioni in corso operazioni di distribuzione iniziale e di toobe desiderato.</span><span class="sxs-lookup"><span data-stu-id="c16b1-122">It is not intended toobe a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="c16b1-123">Non è necessario sostituire la documentazione SAP correlati toohello installazione di SAP HANA (o hello molti note sul supporto di SAP che coprono argomento hello).</span><span class="sxs-lookup"><span data-stu-id="c16b1-123">It should not replace SAP documentation related toohello installation of SAP HANA (or hello many SAP Support Notes that cover hello topic).</span></span> <span data-ttu-id="c16b1-124">Viene fornita una panoramica e vengono forniti dettagli aggiuntivi di hello dell'installazione di SAP HANA in Azure (istanze di grandi dimensioni).</span><span class="sxs-lookup"><span data-stu-id="c16b1-124">It gives you an overview and provides hello additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="c16b1-125">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-125">Updated: July 2017</span></span>

[<span data-ttu-id="c16b1-126">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-127">Infrastruttura e la connettività tooSAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-127">Infrastructure and connectivity tooSAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="c16b1-128">titolo: aaaInfrastructure e connettività tooSAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-128">title: aaaInfrastructure and Connectivity tooSAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c16b1-129">Riepilogo: Dopo l'acquisto di hello di SAP HANA in Azure (istanze di grandi dimensioni) è stato finalizzato tra i team dell'account aziendale Microsoft hello, sono necessarie diverse configurazioni di rete nella connettività corretta tooensure di ordine.</span><span class="sxs-lookup"><span data-stu-id="c16b1-129">Summary: After hello purchase of SAP HANA on Azure (Large Instances) is finalized between you and hello Microsoft enterprise account team, various network configurations are required in order tooensure proper connectivity.</span></span>  <span data-ttu-id="c16b1-130">Questo documento vengono illustrati hello informazioni toobe condivisa con le seguenti informazioni hello sono obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="c16b1-130">This document outlines hello information that has toobe shared with hello following information is required.</span></span> <span data-ttu-id="c16b1-131">Questo documento descrive quali informazioni sono toobe raccolti in modo che gli script di configurazione toobe eseguire.</span><span class="sxs-lookup"><span data-stu-id="c16b1-131">This document outlines what information has toobe collected and what configuration scripts have toobe run.</span></span> 

<span data-ttu-id="c16b1-132">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-132">Updated: July 2017</span></span>

[<span data-ttu-id="c16b1-133">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-134">Installare SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-134">Install SAP HANA in SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="c16b1-135">titolo: aaaInstall SAP HANA in SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-135">title: aaaInstall SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c16b1-136">Riepilogo: Questo documento sono descritte le procedure di installazione di hello per l'installazione di SAP HANA nell'istanza di grandi dimensioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-136">Summary: This document outlines hello setup procedures for installing SAP HANA on your Azure Large Instance.</span></span> 

<span data-ttu-id="c16b1-137">Ultimo aggiornamento: luglio 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-137">Updated: July 2017</span></span>

[<span data-ttu-id="c16b1-138">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-139">Disponibilità elevata e ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="c16b1-140">titolo: aaaHigh disponibilità e ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-140">title: aaaHigh Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c16b1-141">Riepilogo: La disponibilità elevata e il ripristino di emergenza sono aspetti importanti dell'esecuzione di sistemi SAP HANA cruciali nei server di Azure (istanze di grandi dimensioni).</span><span class="sxs-lookup"><span data-stu-id="c16b1-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="c16b1-142">Di importazione toowork con SAP, l'integratore e/o tooproperly Microsoft progettare e implementare destra hello HA/DR strategia per l'utente.</span><span class="sxs-lookup"><span data-stu-id="c16b1-142">It's import toowork with SAP, your system integrator, and/or Microsoft tooproperly architect and implement hello right HA/DR strategy for you.</span></span> <span data-ttu-id="c16b1-143">Considerazioni importanti come obiettivo del punto di ripristino (RPO) e l'obiettivo del tempo ripristino (RTO), tooyour specifico ambiente, è necessario considerare.</span><span class="sxs-lookup"><span data-stu-id="c16b1-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific tooyour environment, must be considered.</span></span>  <span data-ttu-id="c16b1-144">Questo documento illustra le opzioni disponibili per abilitare i livelli desiderati di disponibilità elevata e ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="c16b1-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="c16b1-145">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="c16b1-145">Updated: December 2016</span></span>

[<span data-ttu-id="c16b1-146">Questo documento è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c16b1-147">Risoluzione dei problemi e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="c16b1-148">titolo: aaaTroubleshooting e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni)</span><span class="sxs-lookup"><span data-stu-id="c16b1-148">title: aaaTroubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c16b1-149">Riepilogo: Questa guida offre informazioni utili per definire il monitoraggio di SAP HANA in ambiente Azure e informazioni aggiuntive sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c16b1-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="c16b1-150">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="c16b1-150">Updated: December 2016</span></span>

[<span data-ttu-id="c16b1-151">Questo documento è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a><span data-ttu-id="c16b1-152">SAP HANA nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-152">SAP HANA on Azure Virtual Machines</span></span>

### <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="c16b1-153">Introduzione a SAP HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-153">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="c16b1-154">titolo: aaaQuickstart Guida all'installazione manuale di SAP HANA in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-154">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="c16b1-155">Riepilogo: Consente di questa Guida rapida tooset sistema in un singola istanza SAP HANA in macchine virtuali di Azure da un'installazione manuale di 7.5 di SAP NetWeaver e SAP HANA SP12.</span><span class="sxs-lookup"><span data-stu-id="c16b1-155">Summary: This quickstart guide helps tooset up a single-instance SAP HANA system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="c16b1-156">Guida di Hello presuppone che il lettore hello sia familiarità con Azure IaaS nozioni di base come come toodeploy le macchine virtuali o reti virtuali tramite hello portale di Azure o Powershell/CLI inclusi hello modelli json toouse delle opzioni.</span><span class="sxs-lookup"><span data-stu-id="c16b1-156">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="c16b1-157">Inoltre è previsto che il lettore hello è familiarità con SAP HANA, SAP NetWeaver e come tooinstall locale.</span><span class="sxs-lookup"><span data-stu-id="c16b1-157">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="c16b1-158">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-158">Updated: June 2017</span></span>

[<span data-ttu-id="c16b1-159">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-159">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a><span data-ttu-id="c16b1-160">Distribuzione di S/4HANA SAP CAL in Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-160">S/4HANA SAP CAL deployment on Azure</span></span>
<span data-ttu-id="c16b1-161">titolo: aaaDeploy SAP S/4HANA o BW/4HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-161">title: aaaDeploy SAP S/4HANA or BW/4HANA on Azure</span></span>

<span data-ttu-id="c16b1-162">Riepilogo: In questa guida semplifica la distribuzione di hello toodemonstrate di S/4HANA SAP in Azure con SAP Cloud accessorio libreria.</span><span class="sxs-lookup"><span data-stu-id="c16b1-162">Summary: This guide helps toodemonstrate hello deployment of SAP S/4HANA on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="c16b1-163">Libreria di Appliance di SAP Cloud è un servizio da SAP che consente alle applicazioni di SAP toodeploy in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-163">SAP Cloud Appliance Library is a service by SAP that allows toodeploy SAP applications on Azure.</span></span> <span data-ttu-id="c16b1-164">Guida di Hello descrive hello dettagliate di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c16b1-164">hello guide describes step by step hello deployment.</span></span>

<span data-ttu-id="c16b1-165">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-165">Updated: June 2017</span></span>

[<span data-ttu-id="c16b1-166">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-166">This guide can be found here</span></span>](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a><span data-ttu-id="c16b1-167">Disponibilità elevata di SAP HANA in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-167">High Availability of SAP HANA in Azure Virtual Machines</span></span>
<span data-ttu-id="c16b1-168">titolo: aaaHigh disponibilità di SAP HANA in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-168">title: aaaHigh Availability of SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="c16b1-169">Riepilogo: La presente guida descrive tramite configurazione a disponibilità elevata di hello del sistema operativo 12 SUSE hello e SAP HANA tooaccommodate HANA replica con failover automatico.</span><span class="sxs-lookup"><span data-stu-id="c16b1-169">Summary: This guide leads you through hello high availability configuration of hello SUSE 12 OS and SAP HANA tooaccommodate HANA System replication with automatic failover.</span></span> <span data-ttu-id="c16b1-170">Guida di Hello è specifico per SUSE e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-170">hello guide is specific for SUSE and Azure Virtual Machines.</span></span> <span data-ttu-id="c16b1-171">Guida di Hello non si applica ancora per Red Hat o bare metal o private cloud o altre distribuzioni di cloud pubblici non Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-171">hello guide does not apply yet for Red Hat or bare-metal or private cloud or other non-Azure public cloud deployments.</span></span>

<span data-ttu-id="c16b1-172">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-172">Updated: June 2017</span></span>

[<span data-ttu-id="c16b1-173">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-173">This guide can be found here</span></span>](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a><span data-ttu-id="c16b1-174">Panoramica del backup di SAP HANA nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-174">SAP HANA backup overview on Azure VMs</span></span>
<span data-ttu-id="c16b1-175">titolo: Guida aaaBackup per SAP HANA in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-175">title: aaaBackup guide for SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="c16b1-176">Riepilogo: Questa guida fornisce informazioni di base sulle possibilità di backup quando si esegue SAP HANA in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-176">Summary: This guide provides basic information about backup possibilities running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="c16b1-177">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-177">Updated: March 2017</span></span>

[<span data-ttu-id="c16b1-178">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-178">This guide can be found here</span></span>](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a><span data-ttu-id="c16b1-179">Backup di SAP HANA a livello di file in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-179">SAP HANA file level backup on Azure VMs</span></span>
<span data-ttu-id="c16b1-180">titolo: backup HANA aaaSAP basato su snapshot di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c16b1-180">title: aaaSAP HANA backup based on storage snapshots</span></span>

<span data-ttu-id="c16b1-181">Riepilogo: Questa guida fornisce informazioni sull'uso di backup basati su snapshot in VM di Azure durante l'esecuzione di SAP HANA su Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-181">Summary: This guide provides information about using snapshot-based backups on Azure VMs when running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="c16b1-182">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-182">Updated: March 2017</span></span>

[<span data-ttu-id="c16b1-183">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-183">This guide can be found here</span></span>](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a><span data-ttu-id="c16b1-184">Backup di SAP HANA basati su snapshot in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-184">SAP HANA snapshot based backups on Azure VMs</span></span>
<span data-ttu-id="c16b1-185">titolo: aaaSAP HANA Azure Backup a livello di file</span><span class="sxs-lookup"><span data-stu-id="c16b1-185">title: aaaSAP HANA Azure Backup on file level</span></span>

<span data-ttu-id="c16b1-186">Riepilogo: Questa guida fornisce informazioni sull'uso di backup di SAP HANA a livello di file durante l'esecuzione di SAP HANA su macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-186">Summary: This guide provides information about using SAP HANA file level backup running SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="c16b1-187">Ultimo aggiornamento: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-187">Updated: March 2017</span></span>

[<span data-ttu-id="c16b1-188">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-188">This guide can be found here</span></span>](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a><span data-ttu-id="c16b1-189">SAP NetWeaver distribuito in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-189">SAP NetWeaver deployed on Azure Virtual Machines</span></span>

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a><span data-ttu-id="c16b1-190">Distribuire il sistema SAP IDES in Windows e SQL Server mediante SAP CAL in Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-190">Deploy SAP IDES system on Windows and SQL Server through SAP CAL on Azure</span></span>
<span data-ttu-id="c16b1-191">titolo: aaaTesting SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="c16b1-191">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="c16b1-192">Riepilogo: Questo documento descrive hello di distribuzione di un sistema SAP IDE basato su Windows e SQL Server in Azure con SAP Cloud accessorio libreria.</span><span class="sxs-lookup"><span data-stu-id="c16b1-192">Summary: This document describes hello deployment of an SAP IDES system based on Windows and SQL Server on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="c16b1-193">Dispositivo Cloud SAP libreria è un servizio SAP che consente la distribuzione di hello dei prodotti SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-193">SAP Cloud appliance Library is an SAP service that allows hello deployment of SAP products on Azure.</span></span> <span data-ttu-id="c16b1-194">Questo documento dettagliate attraversa distribuzione hello di un sistema SAP IDE.</span><span class="sxs-lookup"><span data-stu-id="c16b1-194">This document goes step by step through hello deployment of an SAP IDES system.</span></span> <span data-ttu-id="c16b1-195">Hello sistema IDE è solo un esempio per diverse decine applicazioni che possono essere distribuiti attraverso appliance di Cloud di SAP in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-195">hello IDES system is just an example for several other dozen applications that can be deployed through SAP Cloud appliance on Microsoft Azure.</span></span>

<span data-ttu-id="c16b1-196">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-196">Updated: June 2017</span></span>

[<span data-ttu-id="c16b1-197">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-197">This guide can be found here</span></span>](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="c16b1-198">Guida rapida per NetWeaver su SUSE Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-198">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="c16b1-199">titolo: aaaTesting SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="c16b1-199">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="c16b1-200">Riepilogo: Questo articolo descrive i vari aspetti tooconsider quando si esegue SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="c16b1-200">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="c16b1-201">SAP NetWeaver è ufficialmente supportato nelle macchine virtuali SUSE Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-201">SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="c16b1-202">Tutti i dettagli riguardanti le versioni di Linux, le versioni del kernel SAP e altre informazioni sono reperibili nella nota 1928533 di SAP "SAP Applications on Azure: Supported Products and Azure VM types" (Applicazioni SAP in Azure: prodotti supportati e i tipi di VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="c16b1-202">All details regarding Linux versions, SAP kernel versions, and other details can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="c16b1-203">Ultimo aggiornamento: settembre 2016</span><span class="sxs-lookup"><span data-stu-id="c16b1-203">Updated: September 2016</span></span>

[<span data-ttu-id="c16b1-204">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-204">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="c16b1-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Pianificazione e implementazione</span><span class="sxs-lookup"><span data-stu-id="c16b1-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and implementation</span></span>
<span data-ttu-id="c16b1-206">titolo: aaaAzure macchine virtuali di pianificazione e implementazione di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c16b1-206">title: aaaAzure Virtual Machines planning and implementation for SAP NetWeaver</span></span>

<span data-ttu-id="c16b1-207">Riepilogo: Questo documento è hello Guida toostart con se si sta pensando di eseguire SAP NetWeaver in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-207">Summary: This document is hello guide toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="c16b1-208">Questa Guida alla pianificazione e implementazione permette di valutare se un sistema esistente o pianificato basato su SAP NetWeaver può essere distribuito tooan ambiente di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-208">This planning and implementation guide helps you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="c16b1-209">Illustra più scenari di distribuzione di SAP NetWeaver e include configurazioni SAP tooAzure specifico.</span><span class="sxs-lookup"><span data-stu-id="c16b1-209">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="c16b1-210">carta Hello Elenca e descrive tutti hello informazioni di configurazione necessarie, occorre su hello toorun lato SAP/Azure un panorama SAP ibrido.</span><span class="sxs-lookup"><span data-stu-id="c16b1-210">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="c16b1-211">Sono incluse anche procedure che possono essere eseguite tooensure un'elevata disponibilità dei sistemi basati su SAP NetWeaver in IaaS.</span><span class="sxs-lookup"><span data-stu-id="c16b1-211">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="c16b1-212">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-212">Updated: June 2017</span></span>

<span data-ttu-id="c16b1-213">[Questa guida è disponibile qui][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="c16b1-213">[This guide can be found here][planning-guide]</span></span>

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="c16b1-214">Configurazioni a disponibilità elevata di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-214">High Availability configurations of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="c16b1-215">titolo: aaaAzure disponibilità elevata di macchine virtuali per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c16b1-215">title: aaaAzure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="c16b1-216">Riepilogo: In questo documento, si illustrano i passaggi di hello che è possibile trarre toodeploy sistemi SAP a disponibilità elevata in Azure con modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="c16b1-216">Summary: In this document, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c16b1-217">Le attività principali che verranno illustrate sono le seguenti.</span><span class="sxs-lookup"><span data-stu-id="c16b1-217">We walk you through these major tasks.</span></span> <span data-ttu-id="c16b1-218">Nel documento hello, viene descritto come singolo-punto-di-errore componenti, ad esempio Advanced Business dell'applicazione di programmazione (ABAP) SAP Central Services (ASCS) / SAP Central Services (SCS) e sistemi di gestione di database (DBMS) e i componenti ridondanti quali SAP Server applicazioni sta toobe protetto durante l'esecuzione in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-218">In hello document, we describe how single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server are going toobe protected when running in Azure VMs.</span></span> <span data-ttu-id="c16b1-219">Questo documento riporta la dimostrazione passo per passo di un esempio di installazione e configurazione di un sistema SAP a disponibilità elevata in un cluster Windows Server Failover Clustering in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-219">A step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure is demonstrated and shown in this document.</span></span>

<span data-ttu-id="c16b1-220">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-220">Updated: June 2017</span></span>

[<span data-ttu-id="c16b1-221">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-221">This guide can be found here</span></span>](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="c16b1-222">Realizzazione di distribuzioni a più SID di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-222">Realizing Multi-SID deployments of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="c16b1-223">titolo: aaaCreate una configurazione di multi-SID di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c16b1-223">title: aaaCreate an SAP NetWeaver multi-SID configuration</span></span> 

<span data-ttu-id="c16b1-224">Riepilogo: Questo documento è un documento di inoltre toohello la disponibilità elevata per SAP NetWeaver in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-224">Summary: This document is an addition toohello document High availability for SAP NetWeaver on Azure VMs.</span></span> <span data-ttu-id="c16b1-225">A causa di funzionalità toonew in Azure che è stata introdotta in settembre 2016, è possibile toodeploy più SAP NetWeaver ASCS/SCS istanze in una coppia di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-225">Due toonew functionality in Azure that got introduced in September 2016, it is possible toodeploy multiple SAP NetWeaver ASCS/SCS instances in a pair of Azure VMs.</span></span> <span data-ttu-id="c16b1-226">Con questa configurazione, è possibile ridurre il numero di hello delle configurazioni SAP NetWeaver a disponibilità elevata di macchine virtuali necessarie toodeploy toorealize.</span><span class="sxs-lookup"><span data-stu-id="c16b1-226">With such a configuration, you can reduce hello number of VMs necessary toodeploy toorealize highly available SAP NetWeaver configurations.</span></span> <span data-ttu-id="c16b1-227">Guida di Hello descrive l'installazione di hello di tali configurazioni multi-SID.</span><span class="sxs-lookup"><span data-stu-id="c16b1-227">hello guide describes hello setup of such multi-SID configurations.</span></span>

<span data-ttu-id="c16b1-228">Ultimo aggiornamento: dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="c16b1-228">Updated: December 2016</span></span>

[<span data-ttu-id="c16b1-229">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-229">This guide can be found here</span></span>](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="c16b1-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Distribuzione di SAP NetWeaver in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="c16b1-231">titolo: distribuzione di macchine virtuali per SAP NetWeaver aaaAzure</span><span class="sxs-lookup"><span data-stu-id="c16b1-231">title: aaaAzure Virtual Machines deployment for SAP NetWeaver</span></span>

<span data-ttu-id="c16b1-232">Riepilogo: Questo documento include indicazioni dettagliate sulle procedure per la distribuzione di macchine di toovirtual software SAP NetWeaver in Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-232">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="c16b1-233">Questo documento è incentrato sui tre scenari di distribuzione specifico, con particolare attenzione sull'abilitazione delle estensioni hello di Azure Monitoring per SAP, incluse indicazioni per le estensioni di monitoraggio di Azure per SAP hello la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="c16b1-233">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="c16b1-234">Questo documento si presuppone che sia stata letta hello pianificazione e implementazione della Guida.</span><span class="sxs-lookup"><span data-stu-id="c16b1-234">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="c16b1-235">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-235">Updated: June 2017</span></span>

<span data-ttu-id="c16b1-236">[Questa guida è disponibile qui][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="c16b1-236">[This guide can be found here][deployment-guide]</span></span>

### <span data-ttu-id="c16b1-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guida alla distribuzione DBMS</span><span class="sxs-lookup"><span data-stu-id="c16b1-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS deployment guide</span></span>
<span data-ttu-id="c16b1-238">titolo: distribuzione di macchine virtuali DBMS per SAP NetWeaver aaaAzure</span><span class="sxs-lookup"><span data-stu-id="c16b1-238">title: aaaAzure Virtual Machines DBMS deployment for SAP NetWeaver</span></span>

<span data-ttu-id="c16b1-239">Riepilogo: Questo documento include considerazioni sulla pianificazione e implementazione per sistemi DBMS hello che deve essere eseguito insieme a SAP.</span><span class="sxs-lookup"><span data-stu-id="c16b1-239">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="c16b1-240">Nella prima parte hello, considerazioni generali sono elencate e presentate.</span><span class="sxs-lookup"><span data-stu-id="c16b1-240">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="c16b1-241">Hello parti seguenti di carta hello correlare toodeployments di vari DBMS in Azure supportati da SAP.</span><span class="sxs-lookup"><span data-stu-id="c16b1-241">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="c16b1-242">I sistemi DBMS presentati sono SQL Server, SAP ASE e Oracle.</span><span class="sxs-lookup"><span data-stu-id="c16b1-242">Different DBMS presented are SQL Server, SAP ASE, and Oracle.</span></span> <span data-ttu-id="c16b1-243">In tali parti specifiche, vengono illustrate considerazioni è tooaccount per quando si eseguono i sistemi SAP in Azure in combinazione con tali DBMS.</span><span class="sxs-lookup"><span data-stu-id="c16b1-243">In those specific parts, considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="c16b1-244">Gli argomenti come metodi di backup e disponibilità elevata supportate da hello che diversi DBMS in Azure sono disponibili per l'utilizzo di hello con le applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="c16b1-244">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="c16b1-245">Ultimo aggiornamento: giugno 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-245">Updated: June 2017</span></span>

<span data-ttu-id="c16b1-246">[Questa guida è disponibile qui][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="c16b1-246">[This guide can be found here][dbms-guide]</span></span>

### <a name="using-azure-site-recovery-for-sap-workload"></a><span data-ttu-id="c16b1-247">Utilizzo di Azure Site Recovery per un carico di lavoro SAP</span><span class="sxs-lookup"><span data-stu-id="c16b1-247">Using Azure Site Recovery for SAP workload</span></span>
<span data-ttu-id="c16b1-248">titolo: aaaSAP NetWeaver: creazione di una soluzione di ripristino di emergenza con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c16b1-248">title: aaaSAP NetWeaver: Building a Disaster Recovery Solution with Azure Site Recovery</span></span> 

<span data-ttu-id="c16b1-249">Riepilogo: Questo documento descrive il modo di hello come servizi di Azure Site Recovery possono essere usati a scopo di hello di gestione degli scenari di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="c16b1-249">Summary: This document describes hello way how Azure Site Recovery services can be used for hello purpose of handling disaster recovery scenarios.</span></span> <span data-ttu-id="c16b1-250">Casi in cui è possibile usare Azure come posizione di ripristino di emergenza per un landscape SAP locale mediante i servizi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c16b1-250">Cases where Azure is used as disaster recovery location for an on-premise SAP landscape using Azure Site Recovery Services.</span></span> <span data-ttu-id="c16b1-251">Un altro scenario descritto nel documento hello è case di ripristino di emergenza di hello Azure in Azure (A2A) e come viene gestito con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c16b1-251">Another scenario described in hello document is hello Aure-to-Azure (A2A) disaster recovery case and how it is managed with Azure Site Recovery.</span></span>  

<span data-ttu-id="c16b1-252">Ultimo aggiornamento: agosto 2017</span><span class="sxs-lookup"><span data-stu-id="c16b1-252">Updated: August 2017</span></span>

[<span data-ttu-id="c16b1-253">Questa guida è disponibile qui</span><span class="sxs-lookup"><span data-stu-id="c16b1-253">This guide can be found here</span></span>](http://aka.ms/asr-sap)

