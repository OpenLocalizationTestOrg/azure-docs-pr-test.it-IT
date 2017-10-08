---
title: "aaaSAP NetWeaver in macchine virtuali di Azure – Guida alla distribuzione di DBMS | Documenti Microsoft"
description: SAP NetWeaver in macchine virtuali (VM) di Azure - Guida alla distribuzione DBMS
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver in macchine virtuali (VM) Windows di Azure - Guida alla distribuzione DBMS
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md 
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
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
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
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

Questa guida fa parte della documentazione di hello all'implementazione e distribuzione del software SAP hello in Microsoft Azure. Prima di leggere questa Guida, leggere hello [Guida alla pianificazione e implementazione][planning-guide]. Questo documento descrive la distribuzione di hello di diversi sistemi di gestione dei Database relazionali (RDBMS) e i prodotti correlati in combinazione con SAP in Microsoft macchine virtuali di Azure (VM) utilizzando hello infrastruttura di Azure come una funzionalità del servizio (IaaS).

Hello carta integra hello documentazione di installazione di SAP e note su SAP che rappresentano le risorse primarie hello per le distribuzioni del software SAP e le installazioni dato piattaforme

## <a name="general-considerations"></a>Considerazioni generali
Questo capitolo introduce alcune considerazioni relative all'esecuzione di sistemi DBMS correlati a SAP in macchine virtuali di Azure. Sono presenti alcuni riferimenti sistemi DBMS toospecific in questo capitolo. Sistemi DBMS specifici hello vengono invece gestiti all'interno di questo documento, dopo questo capitolo.

### <a name="definitions-upfront"></a>Definizioni
In tutto il documento hello utilizzeremo hello seguenti termini:

* IaaS (Infrastructure as a Service): infrastruttura distribuita come servizio.
* PaaS (Platform as a Service): piattaforma distribuita come servizio.
* SaaS (Software as a Service): software come un servizio.
* Componente SAP: singola applicazione SAP, ad esempio ECC, BW, Solution Manager o EP.  I componenti SAP possono essere basati su tecnologie ABAP o Java tradizionali o su un'applicazione non basata su NetWeaver, ad esempio Business Objects.
* Ambiente SAP: uno o più componenti SAP raggruppati logicamente tooperform una funzione di business, ad esempio Development, QAS, Training, ripristino di emergenza o di produzione.
* Landscape SAP: Si riferisce toohello intera asset SAP in un cliente landscape IT. Hello landscape SAP include tutti di produzione e ambienti non di produzione.
* Sistema SAP: combinazione hello del livello DBMS e applicazione di, ad esempio un sistema di sviluppo ERP SAP, sistema di test BW SAP, sistema di produzione CRM SAP e così via. In Azure le distribuzioni che non è supportato toodivide questi due livelli tra sedi locali e Azure. Un sistema SAP deve quindi essere distribuito o in locale o in Azure. Tuttavia, è possibile distribuire i sistemi diversi di hello di un landscape SAP in Azure o in locale. Ad esempio, è possibile distribuire i sistemi hello CRM SAP sviluppo e test in Azure ma hello CRM SAP produzione sistema locale.
* Distribuzione solo cloud: una distribuzione in cui hello sottoscrizione di Azure non è connesso tramite un sito a sito o ExpressRoute connessione toohello on-premise infrastruttura di rete. Nella documentazione comune su Azure questi tipi di distribuzioni vengono definiti anche distribuzioni "solo cloud". Macchine virtuali distribuite con questo metodo si accede tramite Internet hello e gli endpoint Internet pubblici assegnati toohello macchine virtuali in Azure. Hello locale Active Directory (AD) e DNS non viene esteso tooAzure in questi tipi di distribuzione. Pertanto le macchine virtuali hello non fanno parte di hello Active Directory locale. Nota: le distribuzioni solo cloud in questo documento vengono definite come panorama applicativo SAP completi in esecuzione esclusivamente in Azure, senza estensione di Active Directory o risoluzione dei nomi dall'istanza locale al cloud pubblico. Le configurazioni solo cloud non sono supportate per i sistemi SAP di produzione o configurazioni in cui STMS SAP o altre risorse locali devono toobe utilizzato tra i sistemi SAP ospitati in Azure e risorse che risiedono in locale.
* Cross-premise: Viene descritto uno scenario in cui le macchine virtuali sono distribuite tooan sottoscrizione di Azure con site-to-site, multisita o ExpressRoute connettività tra Data Center locale hello e Azure. Nella documentazione comune su Azure questi tipi di distribuzioni vengono definiti anche scenari cross-premise. motivo Hello connessione hello è tooextend domini locali, Active Directory locale e DNS in locale in Azure. Hello locale orizzontale è estesa toohello asset Azure della sottoscrizione hello. Grazie a questa estensione, hello macchine virtuali può far parte del dominio locale hello. Gli utenti di dominio del dominio locale hello possono accedere ai server hello ed eseguire servizi su tali macchine virtuali (ad esempio servizi DBMS). La comunicazione e la risoluzione dei nomi tra VM distribuite in locale e VM distribuite in Azure sono consentite. È probabile che questo scenario più comune di hello toobe per la distribuzione di risorse SAP in Azure. Per altre informazioni, vedere [questo][vpn-gateway-cross-premises-options] articolo e [questa pagina][vpn-gateway-site-to-site-create].

> [!NOTE]
> Le distribuzioni cross-premise di sistemi SAP in cui le macchine virtuali di Azure che eseguono sistemi SAP sono membri di un dominio locale sono supportate per i sistemi SAP di produzione. Le configurazioni cross-premise sono supportate per la distribuzione parziale o completa di panorami applicativi SAP in Azure. Anche landscape SAP completo hello in esecuzione in Azure, è necessario che tali macchine virtuali da parte del dominio locale e annunci. Nelle versioni precedenti della documentazione di hello abbiamo parlato scenari IT ibridi, in cui il termine hello "Ibrido" nella radice di fatto hello che vi sia una connettività cross-premise tra sedi locali e Azure. In questo caso "Ibrido" inoltre significa che le macchine virtuali hello in Azure fanno parte di hello in Active Directory locale.
>
>

Alcuni documenti Microsoft descrivono scenari cross-premise in modo leggermente diverso, in particolare per configurazioni DBMS a disponibilità elevata. In hello case di hello SAP documenti correlati, uno scenario di hello Cross-premise solo riduce toohaving site-to-site o privato (ExpressRoute) per la connettività e toohello fact che landscape SAP hello viene distribuito tra sedi locali e Azure.

### <a name="resources"></a>Risorse
Hello guide seguenti sono disponibili per l'argomento hello distribuzioni SAP in Azure:

* [SAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide][planning-guide] (SAP NetWeaver in macchine virtuali di Azure: guida alla pianificazione e all'implementazione)
* [SAP NetWeaver on Azure Virtual Machines (VMs) – Deployment Guide][deployment-guide] (SAP NetWeaver in macchine virtuali di Azure: guida alla distribuzione)
* [SAP NetWeaver in macchine virtuali di Azure (VM) - Guida alla distribuzione DBMS (questo documento)][dbms-guide]
* [SAP NetWeaver in macchine virtuali di Azure - Guida alla distribuzione di funzionalità di disponibilità elevata][ha-guide]

Hello note su SAP seguenti è correlati toohello argomento SAP in Azure:

| Numero della nota | Titolo |
| --- | --- |
| [1928533] |Applicazioni SAP in Azure: prodotti supportati e tipi di macchine virtuali di Azure |
| [2015553] |SAP in Microsoft Azure: prerequisiti per il supporto |
| [1999351] |Risoluzione dei problemi del monitoraggio avanzato di Azure per SAP |
| [2178632] |Metriche chiave del monitoraggio per SAP in Microsoft Azure |
| [1409604] |Virtualizzazione in Windows: monitoraggio avanzato |
| [2191498] |SAP in Linux con Azure: monitoraggio avanzato |
| [2039619] |Applicazioni SAP in Microsoft Azure mediante hello Database Oracle: prodotti supportati e delle versioni |
| [2233094] |DB6: Informazioni aggiuntive sulle applicazioni SAP in Azure che usano IBM DB2 per Linux, UNIX e Windows |
| [2243692] |Linux in una macchina virtuale di Microsoft Azure (IaaS): problemi delle licenze SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: note di installazione |
| [2002167] |Red Hat Enterprise Linux 7. x: installazione e aggiornamento |

Leggere inoltre hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) che contiene tutte le note SAP per Linux.

È necessario una conoscenza approfondita sull'architettura di Microsoft Azure hello e come macchine virtuali di Microsoft Azure vengono distribuiti e gestiti. Altre informazioni sono disponibili qui: <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Siamo **non** discussione relativa piattaforma Microsoft Azure come un offerte di servizio (PaaS) di hello piattaforma Microsoft Azure. In questo documento riguarda in esecuzione un sistema di gestione di database (DBMS) in Microsoft macchine virtuali di Azure (IaaS), come eseguire hello DBMS nell'ambiente locale. Le funzionalità di database di queste due offerte sono molto diverse e non devono essere confuse tra loro. Vedere anche: <https://azure.microsoft.com/services/sql-database/>
>
>

Poiché si stanno esaminando IaaS, in genere hello Windows, Linux e DBMS installazione e configurazione vengono essenzialmente hello uguale a qualsiasi macchina virtuale o un computer bare metal sarà necessario installare on-premise. Quando si usa la tecnologia IaaS, ci sono tuttavia alcune differenze nelle decisioni relative all'architettura e all'implementazione della gestione del sistema. scopo di Hello di questo documento è tooexplain hello dell'architettura e sistema di gestione le differenze specifiche che è necessario essere pronti per quando si utilizza IaaS.

In generale, hello complessive aree di differenza che in questo documento verrà illustrate sono:

* Pianificazione hello macchine virtuali/dischi un layout appropriato di tooensure sistemi SAP si dispone di layout dei file di dati corretto hello e può ottenere sufficiente di IOPS per il carico di lavoro.
* Considerazioni sulla rete per l'uso della tecnologia IaaS.
* Toouse funzionalità di database specifico in layout database hello toooptimize dell'ordine.
* Considerazioni sul backup e il ripristino nella tecnologia IaaS.
* Utilizzo di diversi tipi di immagini per la distribuzione.
* Disponibilità elevata nella tecnologia IaaS di Azure.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Struttura di una distribuzione RDBMS
In ordine, seguire questo capitolo, è necessario toounderstand cosa presentata [questo] [ deployment-guide-3] capitolo di hello [Guida alla distribuzione][deployment-guide]. Conoscenza hello diverso di serie di macchine Virtuali e le differenze e le differenze di Azure Standard e Premium archiviazione devono essere comprese e note prima di leggere questo capitolo.

Fino a marzo 2015, dischi rigidi virtuali di Azure che contiene un sistema operativo sono dimensioni limitate too127 GB. Questa limitazione è stata sollevata nel marzo 2015 (per altre informazioni, vedere <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> ). Da qui in dischi rigidi virtuali contenitore hello del sistema operativo può avere hello stessa dimensione come qualsiasi altro disco rigido virtuale. Tuttavia, si preferisce comunque una struttura di distribuzione in cui hello del sistema operativo, DBMS e l'eventuale file binari SAP sono separati dai file di database hello. Pertanto, è probabile che i sistemi SAP in esecuzione in macchine virtuali di Azure avrà hello base VM (o VHD) installata con sistema operativo hello, database management system eseguibili e file eseguibili SAP. Hello dati DBMS e file di log verranno archiviati in archiviazione di Azure (Standard o Premium archiviazione) nel file VHD separati e collegati come dischi logici toohello originale Azure immagine del sistema operativo VM.

Sfruttando Azure Standard o Premium archiviazione (ad esempio usando hello serie DS o GS-series VM) sono dipendenti dai sono altre quote di Azure sono illustrati [qui][virtual-machines-sizes]. Quando si pianificano i dischi rigidi virtuali di Azure, è necessario migliore bilanciamento hello toofind di quote hello per seguenti hello:

* numero di Hello dei file di dati.
* numero di Hello di dischi rigidi virtuali contenenti file hello.
* quote di Hello IOPS di un singolo disco rigido virtuale.
* Hello velocità di trasmissione dati per ogni disco rigido virtuale.
* numero di Hello di ulteriori possibile di dischi rigidi virtuali per ogni dimensione della macchina virtuale.
* Hello complessivo della velocità effettiva di archiviazione una macchina virtuale può fornire.

Azure impone una quota di IOPS per ogni unità disco rigido virtuale. I dischi rigidi virtuali ospitati in Archiviazione Standard di Azure e quelli ospitati in Archiviazione Premium hanno quote diverse. Anche le latenze dei / o sarà molto diverse tra due tipi archiviazione hello con archiviazione Premium recapito fattori latenze dei / o migliori. Ognuno dei diversi tipi di macchine Virtuali hello dispongono di un numero limitato di dischi rigidi virtuali che si è in grado di tooattach. Un'altra restrizione è data dal fatto che solo determinati tipi di macchine virtuali possono usare Archiviazione Premium di Azure. Ciò significa che la decisione di hello per un determinato tipo di macchina virtuale potrebbe non solo dipendere dalla hello CPU e i requisiti di memoria, ma anche da hello IOPS, requisiti di velocità effettiva di latenza e il disco che in genere vengono ridimensionati con il numero di hello di dischi rigidi virtuali o hello tipo dei dischi di archiviazione Premium. Soprattutto con archiviazione Premium dimensioni hello di un disco rigido virtuale anche potrebbero dipende dal numero di hello di IOPS e la velocità effettiva che deve toobe scopo ogni disco rigido virtuale.

fatto Hello che IOPS velocità, il numero di hello di dischi rigidi virtuali montati, hello e dimensioni di macchina virtuale siano collegati, hello hello potrebbe causare una configurazione di un sistema SAP per toobe diverso da quello della distribuzione locale di Azure. limiti di Hello IOPS per LUN sono in genere configurabili nelle distribuzioni locali. Mentre con archiviazione di Azure tali limiti sono fisse o come archiviazione Premium che dipendono dal tipo di disco hello. È pertanto vedere configurazioni del cliente di server di database che usano molti volumi diversi per eseguibili speciali come SAP e hello DBMS o volumi speciali per i database temporanei o spazi di tabella con distribuzioni locali. Quando un sistema locale è tooAzure spostata, è possibile che tooa spreco della larghezza di banda IOPS potenziale utilizzo di un disco rigido virtuale per eseguibili o i database che non eseguono uno o molti non di IOPS. Pertanto, in macchine virtuali di Azure è consigliabile che hello DBMS e gli eseguibili SAP installata nel disco del sistema operativo hello se possibile.

Hello posizionamento dei file di database hello e file di log e tipo hello di archiviazione di Azure usata, deve essere definito da requisiti di velocità effettiva, latenza e IOPS. In ordine toohave sufficiente di IOPS per i log delle transazioni hello, potrebbe essere forzato tooleverage più dischi rigidi virtuali per i log delle transazioni hello file oppure usare un disco di archiviazione Premium più grande. In tal caso, è necessario creare un software RAID con dischi rigidi virtuali che conterrà i log delle transazioni hello hello (ad esempio Windows Pool di archiviazione per Windows o MDADM e LVM (gestione Volume logico) per Linux).

- - -
> ![Windows][Logo_Windows] Windows
>
> Unità D:\ in una macchina virtuale di Azure è un'unità non persistente supportato da alcuni dischi locali nel nodo di calcolo di Azure hello. Poiché non persistenti, ciò significa che qualsiasi contenuto toohello le modifiche apportate in hello unità D:\ venga persa quando hello VM è stato riavviato. Per "tutte le modifiche" si intende il salvataggio di file, la creazione di directory, l'installazione di applicazioni e così via.
>
> ![Linux][Logo_Linux] Linux
>
> Macchine virtuali di Azure Linux montare automaticamente un'unità in /mnt/resource che è un'unità non persistente supportata da dischi locali nel nodo di calcolo di Azure hello. Poiché non persistenti, ciò significa che qualsiasi toocontent le modifiche apportate in /mnt/resource viene persa quando hello VM è stato riavviato. Per "tutte le modifiche" si intende il salvataggio di file, la creazione di directory, l'installazione di applicazioni e così via.
>
>

- - -
Dipende hello Azure della serie di macchine Virtuali, dischi locali hello hello calcolano Mostra diverse le prestazioni del nodo che possono essere suddivisi in categorie come:

* A0-A7: prestazioni molto limitate. L'unico uso possibile è il file di paging di Windows.
* A8-A11: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva > 1 GB/sec.
* Serie D: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva > 1 GB/sec.
* Serie DS: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva > 1 GB/sec.
* Serie G: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva > 1 GB/sec.
* Serie GS: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva > 1 GB/sec.

Istruzioni precedenti si applicano toohello i tipi di macchine Virtuali che sono certificati con SAP. Hello serie di macchine Virtuali con eccellente IOPS e la velocità effettiva idonei per l'utilizzo da alcune funzionalità DBMS, ad esempio tempdb o uno spazio di tabella temporanea.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Caching per VM e dischi rigidi virtuali
Quando si creano tali dischi/dischi rigidi virtuali tramite il portale di hello o quando si monta caricato tooVMs dischi rigidi virtuali, è possibile scegliere se il traffico dei / o hello tra hello VM e i dischi rigidi virtuali presenti nell'archiviazione di Azure vengono memorizzati nella cache. Archiviazione Premium e Archiviazione Standard di Azure usano due tecnologie diverse per questo tipo di cache. In entrambi i casi hello della cache stessa verrà disco eseguito su hello stessa unità usata da hello disco temporaneo (D:\ in Windows) o /mnt/resource su Linux di hello macchina virtuale.

Archiviazione di Azure Standard hello cache possibili sono:

* Nessuna memorizzazione nella cache
* Memorizzazione nella cache di lettura
* Memorizzazione nella cache di lettura e scrittura

Ordine tooget coerenti e deterministiche delle prestazioni, è necessario impostare hello la memorizzazione nella cache nell'archiviazione di Azure Standard per tutti i dischi rigidi virtuali contenenti **DBMS relativi file di dati, i file di log e tabella spazio too'NONE'**. la memorizzazione nella cache di Hello di hello VM possono rimanere predefinito hello.

Archiviazione Premium di Azure esiste hello memorizzazione nella cache le opzioni seguenti:

* Nessuna memorizzazione nella cache
* Memorizzazione nella cache di lettura

Archiviazione Premium di Azure, si consiglia tooleverage **leggere la memorizzazione nella cache per file di dati** del database SAP hello e scelto **nessuna memorizzazione nella cache di hello VHD(s) dei file di log**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>RAID software
Come già indicato in precedenza, sarà necessario numero hello toobalance di IOPS necessarie per i file di database hello in serie hello di dischi rigidi virtuali è possibile configurare e hello numero massimo di IOPS fornirà una macchina virtuale di Azure per ogni disco rigido virtuale o di archiviazione Premium disco tipo. Il modo più semplice toodeal con carico di IOPS sui dischi rigidi virtuali hello è un software RAID toobuild su hello diversi dischi rigidi virtuali. Quindi, inserire un numero di file di dati di hello DBMS SAP su hello che LUN separate dalla RAID software hello. Dipende da requisiti hello che è tooconsider hello sull'utilizzo di archiviazione Premium anche poiché due dei hello tre diversi dischi di archiviazione Premium forniscono quota di IOPS maggiore di dischi rigidi virtuali in base a Standard di archiviazione. Oltre a hello significativo meglio la latenza dei / o fornite da archiviazione Premium di Azure.

Ciò vale anche il log delle transazioni toohello dei sistemi DBMS diversi hello. Con molti appena aggiunta di più file del log delle transazioni non è utile poiché sistemi DBMS hello scrivere in uno dei file hello in una sola volta. Se è necessarie la velocità di IOPS di un unico Standard di archiviazione basato su disco rigido virtuale è in grado di offrire, è possibile eseguire lo striping sui dischi rigidi virtuali archiviazione Standard più o è possibile utilizzare un tipo di disco più grande di archiviazione Premium che oltre la velocità di IOPS offre una latenza più bassa fattori per la scrittura di hello è / Sistema operativo nel log delle transazioni hello.

Ecco alcuni esempi di situazioni che si sono verificate nelle distribuzioni di Azure e per le quali sarebbe preferibile usare un RAID software:

* Log delle transazioni o log di rollforward che richiedono un numero di IOPS maggiore di quanto sia possibile ottenere con un singolo disco rigido virtuale di Azure. Come indicato in precedenza, questo problema può essere risolto con la compilazione di un LUN in più dischi rigidi virtuali tramite un RAID software.
* Distribuzione non uniforme i/o del carico di lavoro su hello vari file di dati del database SAP hello. In questi casi uno può subire un file di dati raggiunge la quota hello piuttosto spesso. Mentre altri file di dati non ricevono anche quota di IOPS toohello chiusura di un singolo disco rigido virtuale. In tali hello casi soluzione più semplice è toobuild uno LUN su più dischi rigidi virtuali con un software RAID.
* Non si conosce quali hello esatto i/o il carico di lavoro per ogni file di dati e solo approssimativamente conosce quali hello complessiva carico di lavoro IOPS hello DBMS è. Toodo più semplice è toobuild un unico LUN con hello Guida in linea di un software RAID. somma Hello delle quote di più dischi rigidi virtuali dietro il LUN debba quindi soddisfare hello noto IOPS frequenza.

- - -
> ![Windows][Logo_Windows] Windows
>
> L'uso di Windows Server 2012 o di spazi di archiviazione superiori è preferibile perché risulta più efficiente rispetto allo striping in Windows di versioni precedenti di Windows. Tenere presente che potrebbe essere necessario toocreate hello pool di archiviazione di Windows e spazi di archiviazione per i comandi di PowerShell quando si utilizza Windows Server 2012 come sistema operativo. i comandi di PowerShell Hello è reperibile qui <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Solo MDADM e LVM (gestione dei volumi logici) sono supportati toobuild un software RAID su Linux. Per ulteriori informazioni, leggere hello seguenti articoli:
>
> * [Configurare RAID software su Linux][virtual-machines-linux-configure-raid] (per MDADM)
> * [Configurare LVM in una macchina virtuale Linux in Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Considerazioni per l'utilizzo di serie per la macchina virtuale che in genere sono in grado di toowork con archiviazione Premium di Azure sono:

* Le richieste di latenze dei / o chiudere toowhat SAN/NAS dispositivi recapito.
* Richiesta di una latenza di I/O molto superiore alle possibilità di Archiviazione Standard di Azure.
* IOPS per macchina virtuale superiore al numero che è possibile raggiungere con più dischi rigidi virtuali di Archiviazione Standard rispetto a un determinato tipo di macchina virtuale.

Poiché hello archiviazione di Azure sottostante replica nodi di archiviazione tooat almeno tre ogni disco rigido virtuale, RAID 0 può essere utilizzato lo striping semplice. Non vi è alcuna necessità tooimplement RAID5 o RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Archiviazione di Microsoft Azure
Archiviazione di Azure archivierà Microsoft hello base VM (con sistema operativo) e i nodi di archiviazione distinti tooat almeno 3 dischi rigidi virtuali o BLOB. Quando si crea un account di archiviazione, è possibile scegliere il livello di protezione come illustrato di seguito:

![Replica geografica abilitata per l'account di archiviazione di Azure][dbms-guide-figure-100]

Replica archiviazione di Azure locale (ridondanza locale) fornisce i livelli di protezione contro la perdita di dati a causa di un errore tooinfrastructure che alcuni clienti potrebbero permettersi toodeploy. Come illustrato in precedenza sono disponibili opzioni diverse 4 con un quinto una variante di uno di hello innanzitutto tre. Esaminando tali opzioni più da vicino è possibile distinguere:

* **Archiviazione con ridondanza locale Premium**: l'archiviazione Premium di Azure offre prestazioni elevate e supporto di dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con I/O intensivo. Sono disponibili 3 repliche dei dati hello hello stesso Data Center di Azure di un'area di Azure. Hello copie sarà in diversi domini di errore e l'aggiornamento (per i concetti, vedere [questo] [ planning-guide-3.2] capitolo hello [Guida alla pianificazione][planning-guide]). In caso di una replica dei dati di hello uscita da servizio a causa di errore del nodo archiviazione tooa o errore del disco, viene generata automaticamente una nuova replica.
* **Archiviazione con ridondanza locale (LRS)**: In questo caso sono presenti 3 repliche dei dati di hello in hello stesso Data Center di Azure di un'area di Azure. Hello copie sarà in diversi domini di errore e l'aggiornamento (per i concetti, vedere [questo] [ planning-guide-3.2] capitolo hello [Guida alla pianificazione][planning-guide]). In caso di una replica dei dati di hello uscita da servizio a causa di errore del nodo archiviazione tooa o errore del disco, viene generata automaticamente una nuova replica.
* **Archiviazione con ridondanza geografica (GRS)**: In questo caso è presente una replica asincrona che inserirà un ulteriore hello di 3 repliche dei dati di hello in un'altra area di Azure, ovvero nella maggior parte dei casi hello nella stessa area geografica (ad esempio, Europa settentrionale e occidentale Europa). In questo modo si ottengono tre repliche aggiuntive, per un totale di sei repliche. Una variante di questo è un componente aggiuntivo in cui i dati di hello nell'area di Azure replicati geografica hello possono essere utilizzati per la lettura (accesso in lettura con ridondanza geografica).
* **Zona di archiviazione ridondanti (ZRS)**: In questo caso le repliche di hello 3 di hello dati rimangono in hello stessa regione di Azure. Come spiegato in [questo] [ planning-guide-3.1] capitolo di hello [Guida alla pianificazione] [ planning-guide] un'area di Azure può essere un numero di Data Center in stretta vicinanza. Nel caso di hello di archiviazione con ridondanza locale repliche hello vengono distribuite nel Data Center diversi hello che costituiscono un'area di Azure.

Ulteriori informazioni sono disponibili [qui][storage-redundancy].

> [!NOTE]
> Per le distribuzioni DBMS, utilizzo di hello di archiviazione con ridondanza geografica non è consigliato
>
> La replica geografica di Archiviazione di Azure è asincrona. Replica di singoli dischi rigidi virtuali montati tooa singola macchina virtuale non sono sincronizzate nel passaggio di blocco. Pertanto, non è adatto tooreplicate i file DBMS che vengono distribuiti su diversi dischi rigidi virtuali o distribuiti da un software RAID basato su più dischi rigidi virtuali. Il software DBMS richiede che archiviazione hello dei dischi persistente sia sincronizzata con precisione in LUN diversi e dischi/dischi rigidi virtuali/spindle sottostanti. Il software DBMS Usa vari meccanismi toosequence, i/o scrivere attività e un DBMS segnalerà che l'archiviazione su disco hello destinata di replica hello è danneggiato se queste si scostano anche pochi millisecondi. Pertanto se assolutamente necessario implementare una configurazione del database con un database esteso su più dischi rigidi virtuali con replica geografica, è necessario toobe eseguita con strumenti di database e funzionalità di tale replica. Non è sufficiente in Azure replica geografica dell'archiviazione tooperform questo processo.
>
> problema di Hello è più semplice tooexplain con un sistema di esempio. Si supponga che si dispone di un sistema SAP caricato in Azure è 8 dischi rigidi virtuali che contengono file di dati di hello DBMS e un disco rigido virtuale contenente hello log delle transazioni. I dati scritti toothem in un metodo coerenza in base toohello DBMS se hello i dati vengono scritti i file di log delle transazioni o di dati toohello disporrà di ognuno di questi 9 dischi rigidi virtuali.
>
> In ordine tooproperly abilitare la replica geografica hello dati e mantenere un'immagine del database coerente, contenuto hello di tutti i dischi rigidi nove virtuali potrebbe avere toobe replicato geograficamente nelle operazioni dei / o hello hello ordine esatto sono state eseguite nei hello nove diversi dischi rigidi virtuali. Replica geografica dell'archiviazione di Azure non consente tuttavia toodeclare dipendenze tra i dischi rigidi virtuali. Ciò significa che l'archiviazione di Microsoft Azure-replica geografica non è conoscenza dei fatti hello contenuto hello in questi nove dischi rigidi virtuali vengono correlati tooeach altri che si è verificato che le modifiche ai dati hello siano coerenti solo quando la replica in operazioni dei / o di hello ordine hello tra tutti i dischi rigidi virtuali hello 9.
>
> Oltre alla possibilità di essere elevato che le immagini di replica geografica di hello in uno scenario di hello non forniscono un'immagine di database coerente, è anche una riduzione delle prestazioni che viene visualizzato con l'archiviazione con ridondanza geografica che può essere gravemente sulle prestazioni. In breve, non è consigliabile usare questo tipo di ridondanza di archiviazione per carichi di lavoro di tipo DBMS.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Mapping di dischi rigidi virtuali in account di archiviazione del servizio Macchina virtuale di Azure
Un account di archiviazione di Azure non è soltanto un costrutto amministrativo, ma è anche soggetto a limitazioni. Mentre le limitazioni di hello variano se si parla di un Account di archiviazione di Azure Standard o un Account di archiviazione Premium di Azure. sono elencate Hello esatta funzionalità e limitazioni [qui][storage-scalability-targets]

Pertanto è importante toonote Standard di archiviazione di Azure è previsto un limite in hello IOPS per ogni account di archiviazione (riga che contiene 'Frequenza di richiesta totale' [articolo hello][storage-scalability-targets]). Esiste poi un limite iniziale di 100 account di archiviazione per ogni sottoscrizione di Azure (a partire da luglio 2015). Pertanto, è consigliabile toobalance IOPS di macchine virtuali tra più account di archiviazione quando si utilizza l'archiviazione di Azure Standard. Teoricamente, una singola macchina virtuale dovrebbe usare un solo account di archiviazione, se possibile. Se si parla quindi di distribuzioni DBMS in cui ogni disco rigido virtuale ospitato in Archiviazione Standard di Azure potrebbe raggiungere il relativo limite di quota, è necessario distribuire solo 30-40 dischi rigidi virtuali per ogni account di archiviazione di Azure che usa Archiviazione Standard di Azure. In hello altra parte, se si utilizzano l'archiviazione Premium di Azure e si desidera toostore volumi di database di grandi dimensioni, potrebbe essere appropriato in termini di IOPS. Un account di archiviazione Premium di Azure, però, è molto più restrittivo in termini di volume di dati rispetto a un account di archiviazione Standard di Azure. Di conseguenza, è possibile distribuire solo un numero limitato di dischi rigidi virtuali all'interno di un Account di archiviazione Premium di Azure prima di premere hello limite volume dei dati. All'interazione utente finale di hello di un Account di archiviazione di Azure come una "SAN virtuale" che dispone di funzionalità limitate in IOPS e/o capacità. Di conseguenza, hello attività rimane nelle distribuzioni locali, layout di hello toodefine di hello dischi rigidi virtuali di sistemi SAP diversi hello su hello diverso 'dispositivi SAN immaginari' o gli account di archiviazione di Azure.

Per archiviazione di Azure Standard non è consigliato archiviazione toopresent da tooa gli account di archiviazione diversi singola macchina virtuale se possibile.

Mentre l'utilizzo di hello DS o GS-series di macchine virtuali di Azure è possibile toomount i dischi rigidi virtuali da account di archiviazione di Azure Standard e account di archiviazione Premium. Casi di utilizzo come scrivere i backup nel servizio di archiviazione Standard supportato dischi rigidi virtuali mentre i dati di DBMS e file di log in archiviazione Premium sono toomind in cui è stato sfruttato tale archiviazione eterogenee.

Basata su distribuzioni dei clienti e too40 circa 30 test possono eseguire il provisioning di dischi rigidi virtuali contenenti file di dati di database e i file di log in un Account di archiviazione Standard Azure singolo con prestazioni accettabili. Come accennato in precedenza, limitazione di hello di un Account di archiviazione Premium di Azure è probabilmente toobe hello dati capacità che può contenere e non gli IOPS.

Come con SAN dispositivi in locale, condivisione richiede alcune attività di monitoraggio in ordine tooeventually rilevare i colli di bottiglia in un Account di archiviazione di Azure. Hello Azure Monitoring Extension per SAP e hello portale di Azure sono disponibili strumenti che possono essere utilizzati toodetect occupato gli account di archiviazione di Azure che possono fornire prestazioni dei / o non ottimali.  Se viene rilevata questa situazione che è consigliabile toomove tooanother di macchine virtuali occupato Account di archiviazione Azure. Consultare toohello [Guida alla distribuzione] [ deployment-guide] per informazioni dettagliate su come tooactivate hello SAP ospitare le funzionalità di monitoraggio.

Un altro articolo che riepiloga le procedure consigliate per Archiviazione Standard di Azure e gli account di Archiviazione Standard di Azure è disponibile qui <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Lo spostamento distribuito le macchine virtuali DBMS da archiviazione di Azure Standard tooAzure archiviazione Premium
Si verificano molto scenari in cui è cliente toomove una macchina virtuale distribuita da archiviazione Standard di Azure in archiviazione Premium di Azure. Ciò non fosse possibile senza spostare fisicamente i dati di hello. Vi sono l'obiettivo di hello tooachieve modi diversi:

* È possibile copiare semplicemente tutti i dischi rigidi virtuali, il VHD di base, nonché i VHD di dati in un nuovo account di archiviazione Premium di Azure. Molto spesso si è scelto il numero di hello di dischi rigidi virtuali in archiviazione di Azure Standard non a causa delle tabelle dei fatti hello che è necessario che il volume di dati di hello. Ma è necessario un numero così elevato di dischi rigidi virtuali a causa di hello IOPS. Ora che si sposta tooAzure archiviazione Premium è possibile passare in modo meno tooachieve dischi rigidi virtuali hello alcuni della velocità effettiva IOPS. Dato delle tabelle dei fatti hello in archiviazione di Azure Standard si paga per hello utilizzato dati e non hello nominale disco, il numero di hello di dischi rigidi virtuali non davvero importanti in termini di costi. Con l'archiviazione Premium di Azure, tuttavia, si paga la dimensione del disco nominale hello. Pertanto, la maggior parte dei clienti hello prova con numero di hello tookeep di dischi rigidi virtuali di Azure in archiviazione Premium a hello numero tooachieve necessari hello IOPS una velocità effettiva necessaria. In tal caso, la maggior parte dei clienti decidono modo hello 1:1 una semplice copia.
* Se non è già stato fatto, è possibile montare un singolo disco rigido virtuale che può contenere un backup del database SAP. Dopo il backup di hello, disinstallare tutti i dischi rigidi virtuali incluso hello disco rigido virtuale contenente hello backup e hello copia VHD di base e hello VHD con backup hello in un account di archiviazione Premium di Azure. È quindi sarebbe distribuire macchine Virtuali in base a hello base VHD e montaggio hello VHD con backup hello hello. Ora è creare ulteriori vuoto dischi di archiviazione Premium per VM hello sono database hello toorestore utilizzati in. Si presuppone che tale hello DBMS consente toochange percorsi toohello log file di dati e come parte del processo di ripristino hello.
* Un'altra possibilità è una variante del processo precedente hello, in cui appena copiare il backup di hello VHD nell'archiviazione Premium di Azure e collegarlo da una macchina virtuale che è appena distribuito e installato.
* possibilità di quarto Hello scegliere quando si è in hanno l'esigenza di numero hello toochange dei file di dati del database. In tal caso si esegue una copia di sistema omogeneo SAP usando le funzionalità di importazione ed esportazione. PUT quelli esportare i file in un disco rigido virtuale che viene copiato in un Account di archiviazione Premium di Azure e collegarlo tooa VM utilizzare processi di importazione toorun hello. I clienti utilizzare questa possibilità principalmente quando si desidera che il numero di hello toodecrease dei file di dati.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Distribuzione di macchine virtuali per SAP in Azure
Microsoft Azure offre diversi modi di macchine virtuali toodeploy e associati i dischi. In tal modo è molto importante toounderstand differenze di hello poiché preparazioni delle macchine virtuali di hello potrebbero variare a seconda modalità hello di distribuzione. In generale, vengono esaminati gli scenari di hello descritti nella seguente capitoli hello.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Distribuzione di una macchina virtuale da hello Azure Marketplace
Si desidera che Microsoft tootake o 3rd party fornite immagine da hello Azure Marketplace toodeploy la macchina virtuale. Dopo aver distribuito la macchina virtuale in Azure, seguire hello stesse linee guida e gli strumenti tooinstall hello software SAP nella macchina virtuale come si farebbe in un ambiente locale. Per l'installazione di software SAP hello hello macchina virtuale di Azure, SAP e Microsoft consiglia tooupload e archiviare supporti di installazione di SAP hello in dischi rigidi virtuali di Azure o toocreate una macchina virtuale di Azure funziona come "File server' che contiene tutti hello necessarie SAP supporti di installazione.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Distribuzione di una macchina virtuale con un'immagine generalizzata specifica del cliente
A causa di requisiti di patch toospecific in tooyour relativamente del sistema operativo o la versione DBMS, le immagini fornita hello in hello Azure Marketplace potrebbero non soddisfare le proprie esigenze. Di conseguenza, potrebbe essere necessario toocreate una macchina virtuale tramite la propria immagine di macchina virtuale del sistema operativo/DBMS 'private', che può essere distribuito più volte in seguito. tooprepare questa immagine 'privata' per la duplicazione, sistema operativo deve essere generalizzato su hello hello locale macchina virtuale. Consultare toohello [Guida alla distribuzione] [ deployment-guide] per informazioni dettagliate su come toogeneralize una macchina virtuale.

Se è già stato installato contenuto SAP nella macchina virtuale locale (in particolare per i sistemi di livello 2), è possibile adattare le impostazioni di sistema SAP hello dopo la distribuzione di hello di hello macchina virtuale di Azure tramite istanza hello rinominare procedure supportate da SAP Software Provisioning hello Manager (nota SAP [1619720]). In caso contrario è possibile installare il software SAP hello in un secondo momento dopo la distribuzione di hello di hello macchina virtuale di Azure.

A partire da hello del contenuto del database utilizzato da hello applicazione SAP, è possibile generare hello contenuto da zero tramite un'installazione SAP o è possibile importare il contenuto in Azure utilizzando un disco rigido virtuale con un backup del database DBMS o tramite le funzionalità di hello DBMS toodirectly backup in archiviazione di Microsoft Azure. In questo caso, si potrebbe inoltre di preparare i dischi rigidi virtuali con i dati DBMS hello log file locale e quindi importarli come dischi in Azure. Ma trasferimento hello dei dati DBMS che vengono caricati da on-premise tooAzure funziona solo su dischi VHD che devono toobe preparati in locale.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Lo spostamento di una macchina virtuale da tooAzure locale con un disco non generalizzato
Si prevede di toomove un sistema SAP specifico da on-premise tooAzure (accuratezza e MAIUSC). Questa operazione può essere eseguita caricando hello disco rigido virtuale contenente hello del sistema operativo, hello binari SAP e gli eventuali binari DBMS più hello dischi rigidi virtuali con file di dati e log hello di hello DBMS tooAzure. In opposto tooscenario #2 precedente, mantenere hello hostname, SID di SAP e account utente SAP nella macchina virtuale di Azure hello come sono stati configurati nell'ambiente locale hello. Pertanto, generalizzare l'immagine di hello non è necessario. In questo caso verrà applicato principalmente per gli scenari di più sedi locali in cui una parte di hello landscape SAP viene eseguita in locale e le parti in Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Disponibilità elevata e ripristino di emergenza con VM di Azure
Azure offre hello seguendo le funzionalità di disponibilità elevata e ripristino di emergenza che si applicano toodifferent componenti usati per le distribuzioni SAP e DBMS

### <a name="vms-deployed-on-azure-nodes"></a>Macchine virtuali distribuite in nodi di Azure
Hello piattaforma Azure offre funzionalità quali la migrazione in tempo reale per le macchine virtuali distribuite. Pertanto, se in un cluster di server in cui è distribuita una macchina virtuale è necessaria la manutenzione, hello VM tooget arrestato e riavviato. In Azure la manutenzione viene eseguita usando i domini di aggiornamento all'interno dei cluster di server. È possibile eseguire la manutenzione di un solo dominio di aggiornamento alla volta. Durante tale riavvio verrà un'interruzione del servizio mentre hello che arresto della macchina virtuale, viene eseguita la manutenzione e riavviato VM. Tuttavia, la maggior parte dei fornitori di sistemi DBMS forniscono funzionalità di disponibilità elevata e ripristino di emergenza che consentono di riavviare rapidamente servizi DBMS hello in un altro nodo se non è disponibile nel nodo primario hello. Hello piattaforma Azure offre funzionalità toodistribute macchine virtuali, archiviazione e altri servizi di Azure tra domini di aggiornamento tooensure che gli errori di infrastruttura o di manutenzione pianificato influirebbe solo un piccolo subset delle macchine virtuali o servizi.  Con un'attenta pianificazione è infrastrutture confrontabili tooon locale livelli di disponibilità tooachieve possibili.

Set di disponibilità di Microsoft Azure sono un raggruppamento logico di macchine virtuali o servizi che garantisce le macchine virtuali e altri servizi sono distribuiti toodifferent errore e domini di aggiornamento all'interno di un cluster in modo che potrebbe essere presente solo l'arresto di un nodo da un punto nel tempo (lettura [questo] [ virtual-machines-manage-availability] per ulteriori dettagli).

È necessario toobe configurati appositamente durante il rollout delle macchine virtuali, come illustrato di seguito:

![Definizione di un set di disponibilità per le configurazioni a disponibilità DBMS][dbms-guide-figure-200]

Se si desidera che le configurazioni a disponibilità elevata toocreate di distribuzioni DBMS (indipendente di hello singoli DBMS con disponibilità elevata funzionalità utilizzata), le macchine virtuali DBMS hello necessario:

* Aggiungere hello macchine virtuali toohello stessa rete virtuale di Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* le macchine virtuali di configurazione a disponibilità elevata hello Hello deve inoltre essere in hello stessa subnet. Risoluzione dei nomi tra subnet diverse hello non è possibile nelle distribuzioni solo Cloud, funzionerà solo la risoluzione IP. Se si usa la connettività da sito a sito o ExpressRoute per le distribuzioni cross-premise, è già presente una rete con almeno una subnet. Verrà eseguita la risoluzione dei nomi in base toohello locale criteri di Active Directory e infrastruttura di rete.

[comment]: <> (MSSedusch TODO Test if still true in ARM)

#### <a name="ip-addresses"></a>Indirizzi IP
È consigliabile toosetup hello macchine virtuali per le configurazioni a disponibilità elevata in modo resiliente. Basarsi su IP indirizzi tooaddress hello partner di disponibilità elevata all'interno di configurazione a disponibilità elevata hello non è affidabile in Azure a meno che non vengono utilizzati indirizzi IP statici. Azure prevede due tipi di "arresto":

* Arresto tramite il portale di Azure o Azure PowerShell il cmdlet Stop-AzureRmVM: In questo caso hello macchina virtuale viene arrestata e deallocata. L'account di Azure non verrà addebitato per questa macchina virtuale non è più in modo hello unici costi che comporteranno sono per l'archiviazione di hello utilizzato. Tuttavia, se l'indirizzo IP privato hello hello dell'interfaccia di rete non è statico, indirizzo IP hello viene rilasciato e non è garantito il che interfaccia di rete hello Ottiene hello vecchio indirizzo IP assegnato dopo il riavvio di hello macchina virtuale. Esecuzione di hello arresto tramite il portale di Azure hello o chiamando Stop AzureRmVM verranno automaticamente deallocazione. Se non si desidera macchina hello toodeallocat utilizzare Stop-AzureRmVM - StayProvisioned
* Se si arresta hello macchina virtuale da un livello del sistema operativo, hello VM Ottiene chiuso e non viene deallocata. Tuttavia, in questo caso, l'account di Azure ancora verrà addebitato hello VM, nonostante hello se è arrestata. In tal caso, hello assegnazione di hello IP indirizzo tooa macchina virtuale arrestata rimarrà invariata. Arresto hello macchina non forza automaticamente la deallocazione.

Anche per scenari con più sedi locali, per impostazione predefinita un arresto e la deallocazione implica annullamento dell'assegnazione di hello indirizzi IP da hello macchina virtuale, anche se i criteri locali nelle impostazioni DHCP sono diversi.

* Hello eccezione se uno assegna un' statico IP indirizzo tooa interfaccia di rete come descritto [qui][virtual-networks-reserved-private-ip].
* In questo caso l'indirizzo IP hello rimane fisso come interfaccia di rete hello non viene eliminato.

> [!IMPORTANT]
> In ordine tookeep hello intera distribuzione semplice e gestibile, hello chiaro raccomandazione è toosetup hello macchine virtuali associate in una configurazione DBMS con disponibilità elevata o ripristino di emergenza in Azure in modo che vi sia una risoluzione dei nomi funzionante tra hello diverse macchine virtuali coinvolte.
>
>

## <a name="deployment-of-host-monitoring"></a>Distribuzione del monitoraggio host
Per l'utilizzo produttivo di applicazioni SAP in macchine virtuali di Azure, SAP richiede hello possibilità dell'host tooget dati di monitoraggio dall'host fisico di hello in esecuzione hello macchine virtuali di Azure. È necessario un livello di patch SAP Host Agent specifico che abilita questa funzionalità in SAPOSCOL e SAP Host Agent. livello di patch esatto Hello è documentato nella nota SAP [1409604].

Per informazioni dettagliate hello sulla distribuzione di componenti che forniscono host dati tooSAPOSCOL e SAPHostAgent e hello gestione del ciclo di vita di questi componenti, consultare toohello [Guida alla distribuzione][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Le specifiche tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>SQL Server in IaaS
A partire da Microsoft Azure, è possibile eseguire facilmente la migrazione delle applicazioni di SQL Server esistenti compilate nella piattaforma di Windows Server tooAzure macchine virtuali. SQL Server in una macchina virtuale consente di tooreduce hello costo totale di proprietà di distribuzione, gestione e manutenzione di applicazioni breadth aziendali eseguendo facilmente la migrazione di questi tooMicrosoft applicazioni Azure. Con SQL Server in una macchina virtuale di Azure, gli amministratori e sviluppatori possono ancora usare hello stessi strumenti di sviluppo e amministrazione disponibili in locale.

> [!IMPORTANT]
> Nota: non si tratta di una Database di SQL Azure Microsoft che è una piattaforma come un'offerta di servizio di hello piattaforma Microsoft Azure. discussione Hello in questo documento viene descritta l'esecuzione del prodotto SQL Server hello quanto è noto per le distribuzioni locali in macchine virtuali di Azure, sfruttando hello infrastruttura come funzionalità del servizio di Azure. Le funzionalità di database di queste due offerte sono diverse e non devono essere confuse tra loro. Vedere anche: <https://azure.microsoft.com/services/sql-database/>
>
>

È consigliabile tooreview [questo] [ virtual-machines-sql-server-infrastructure-services] documentazione prima di continuare.

In hello parti nelle sezioni seguenti di parti della documentazione di hello in collegamento hello precedente verranno aggregati e indicati. Vengono anche riportate le specifiche relative a SAP e alcuni concetti vengono descritti in modo più dettagliato. Tuttavia, è consigliabile toowork tramite documentazione hello indicata sopra prima prima di leggere la documentazione specifica di SQL Server hello.

Di seguito sono indicate alcune informazioni specifiche su SQL Server in IaaS che è necessario conoscere per poter continuare:

* **Contratto di servizio per macchine virtuali**: il contratto di servizio per le macchine virtuali in esecuzione in Azure è disponibile qui: <https://azure.microsoft.com/support/legal/sla/>  
* **Supporto della versione SQL**: per i clienti SAP, le macchine virtuali di Microsoft Azure supportano SQL Server 2008 R2 e versioni successive. Le versioni precedenti non sono supportate. Per altre informazioni, vedere questa [informativa sul supporto](https://support.microsoft.com/kb/956893) di carattere generale. Si noti che in genere SQL Server 2008 è supportato anche da Microsoft. Tuttavia, a causa di funzionalità toosignificant per SAP che è stata introdotta con SQL Server 2008 R2, SQL Server 2008 R2 è una versione minima di hello per SAP. Tenere presente che SQL Server 2012 e 2014 è stato ulteriormente esteso con un'integrazione più approfondita in uno scenario IaaS hello (ad esempio, il backup direttamente nel servizio di archiviazione Azure). Pertanto, è limitare questa tooSQL carta Server 2012 e 2014 con il livello di patch più recente per Azure.
* **Supporto di funzionalità SQL**: le macchine virtuali di Microsoft Azure supportano la maggior parte delle funzionalità di SQL Server, con alcune eccezioni. **Il clustering di failover di SQL Server tramite dischi condivisi non è supportato**.  Le tecnologie distribuite quali il mirroring del database, i gruppi di disponibilità AlwaysOn, la replica, il log shipping e Service Broker sono supportate in un'unica area di Azure. SQL Server AlwaysOn inoltre è supportato tra diverse aree di Azure come indicato qui:  <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Hello revisione [istruzione di supporto](https://support.microsoft.com/kb/956893) per altri dettagli. Un esempio di come toodeploy una configurazione di AlwaysOn verrà visualizzata nei [questo] [ virtual-machines-workload-template-sql-alwayson] articolo. Inoltre, estrarre hello consigliate documentate [qui][virtual-machines-sql-server-infrastructure-services]
* **Prestazioni SQL**: si è certi di Microsoft Azure verrà prestazioni molto elevate macchine virtuali ospitate nelle offerte di virtualizzazione di confronto tooother cloud pubblico, ma i singoli risultati possono variare. Per informazioni, consultare [questo articolo][virtual-machines-sql-server-performance-best-practices].
* **Utilizzo di immagini da Azure Marketplace**: hello più veloce modo toodeploy una nuova macchina virtuale di Microsoft Azure è toouse un'immagine da hello Azure Marketplace. Vi sono immagini in hello Azure Marketplace che contengono SQL Server. le immagini di Hello in SQL Server è già installato non possono essere utilizzati immediatamente per le applicazioni SAP NetWeaver. Hello, infatti, regole di confronto SQL Server predefinite hello viene installata all'interno di tali immagini e non hello regole di confronto richieste dai sistemi SAP NetWeaver. In ordine toouse tali immagini, verificare i passaggi di hello descritti nei capitoli [a un Server SQL immagini fuori hello Microsoft Azure Marketplace][dbms-guide-5.6].
* Per altre informazioni, consultare i [dettagli sui prezzi](https://azure.microsoft.com/pricing/) . Hello [Guida alla gestione delle licenze di SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) e [Guida di gestione delle licenze di SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) sono anche una risorsa importante.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Linee guida per la configurazione di SQL Server per le installazioni di SQL Server correlate a SAP nelle VM di Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Consigli sulla struttura di VM/dischi rigidi virtuali per distribuzioni di SQL Server correlate a SAP
In conformità con descrizione generale di hello, file eseguibili di SQL Server devono essere disponibile oppure installati nell'unità di sistema hello di hello della macchina virtuale VHD di base (unità c:\).  In genere, la maggior parte dei database di sistema di SQL Server hello non vengono utilizzata un livello elevato dal carico di lavoro di SAP NetWeaver. Di conseguenza il database di sistema hello di SQL Server (master, msdb e modello) possono rimanere su hello anche l'unità C:\. Un'eccezione può essere tempdb, che nel caso di hello di alcuni ERP SAP e tutti i carichi di lavoro BW, potrebbe richiedere il volume di dati maggiore o volume di operazioni dei / o che non si adattata hello macchina virtuale originale. Per questi sistemi, è opportuno eseguire hello alla procedura seguente:

* Spostare hello tempdb primari dati file toohello stessa unità logica come file di dati primari hello del database SAP hello.
* Aggiungere qualsiasi tooeach i file di dati tempdb aggiuntivi di hello altre unità logiche contenenti un file di dati di database utente SAP di hello.
* Aggiungere hello tempdb logfile toohello unità logica che contiene i file di log del database utente hello.
* **Esclusivamente per i tipi di macchine Virtuali che utilizzano unità SSD locale** dati tempdb del nodo di calcolo hello e di log file potrebbero essere posizionati in unità D:\ hello. Tuttavia, potrebbe essere consigliabile toouse più file di dati di tempdb. Tenere presente i volumi di unità D:\ sono diversi in base a hello tipo di macchina virtuale.

Queste configurazioni abilitano tempdb tooconsume più spazio rispetto a unità di sistema di hello è in grado di tooprovide. In dimensioni di tempdb appropriate hello toodetermine ordine, è possibile verificare le dimensioni di tempdb hello nei sistemi esistenti in cui vengono eseguiti in locale. Inoltre, tale configurazione consentirebbe di operazioni IOPS eseguite in tempdb, che è possibile eseguire con unità di sistema hello. Nuovamente, i sistemi che eseguono in locale possono essere utilizzato toomonitor i/o il carico di lavoro nel database tempdb in modo che sia possibile trarre hello IOPS previste toosee tempdb.

Una configurazione della macchina virtuale che esegue SQL Server con un database SAP e in cui vengono memorizzati i dati di tempdb e file di log tempdb nell'unità D:\ hello sarebbe simile:

![Configurazione di riferimento di una VM IaaS di Azure per SAP][dbms-guide-figure-300]

Tenere presente che hello unità D:\ è dipende dal tipo di macchina virtuale hello di dimensioni diverse. Dipende dal requisito di hello dimensioni di tempdb potrebbe essere forzato toopair di dati tempdb e i file di log con hello SAP dati del database e i file di log nei casi in cui l'unità D:\ è troppo piccolo.

#### <a name="formatting-hello-vhds"></a>Formattazione di dischi rigidi virtuali hello
Per messaggi hello del Server SQL dimensione del blocco NTFS per i dischi rigidi virtuali contenenti dati di SQL Server e di log file devono essere di 64 KB. Non è hello di tooformat unità D:\ non necessario. perché viene fornita preformattata.

In ordine toomake certi che hello ripristino o la creazione di database non inizializzazione dei file di dati hello azzerando il contenuto di hello del file hello, è opportuno accertarsi che il servizio SQL Server hello di hello utente contesto è in esecuzione in disponga di determinate autorizzazioni. In genere gli utenti al gruppo degli amministratori di Windows hello dispongono di tali autorizzazioni. Se hello servizio SQL Server viene eseguito nel contesto utente hello dell'utente Administrator non Windows, è necessario tooassign tale hello utente il diritto utente 'Eseguire le operazioni di manutenzione volume'.  Visualizzare i dettagli di hello in questo articolo della Microsoft Knowledge Base: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Impatto della compressione del database
Nelle configurazioni in cui la larghezza di banda dei / o può diventare un fattore limitante, ogni misura riducendo il numero di IOPS può contribuire a carico di lavoro di hello toostretch può eseguire in uno scenario IaaS come Azure. Pertanto, se non è ancora fatto, applicare la compressione di pagina di SQL Server è consigliabile da SAP e Microsoft prima di caricare un SAP esistente database tooAzure.

Hello raccomandazione tooperform la compressione del Database prima di caricare tooAzure ha due motivi:

* quantità di Hello di dati toobe caricate è inferiore.
* durata Hello dell'esecuzione di compressione di hello è più breve, supponendo che sia possibile usare hardware più potente con più CPU o della larghezza di banda dei / o maggiore o minore latenza i/o in locale.
* Database di dimensioni più piccolo potrebbe causare costi tooless per l'allocazione dei dischi

Il funzionamento della compressione del database nelle macchine virtuali di Azure è analogo a quello in locale. Per ulteriori informazioni su come toocompress un database di SQL Server SAP esistente, fare clic qui: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014: archiviazione dei file di database direttamente nell'archivio BLOB di Azure
SQL Server 2014 consente di aprire file di database toostore possibilità hello direttamente sull'archivio Blob di Azure senza hello 'wrapper' di un disco rigido virtuale attorno a esse. In particolare all'utilizzo di archiviazione di Azure Standard o tipi di macchine Virtuali più piccoli in questo modo gli scenari in cui è possibile ovviare a limiti di hello di IOPS che verrà applicata a un numero limitato di dischi rigidi virtuali che possono essere tipi di macchine Virtuali montati toosome più piccoli. Si tratta però di una funzionalità valida per i database utente e non per i database di sistema di SQL Server, che funziona anche per i file di log e di dati di SQL Server. Se si desidera toodeploy SAP SQL Server di database in questo modo, invece di 'wrapping' in dischi rigidi virtuali, tenere presente i seguenti hello:

* toobe esigenze di Account di archiviazione usato Hello in hello stessa regione di Azure come hello ovvero hello toodeploy utilizzati VM SQL Server è in esecuzione in una.
* Elencate in precedenza in toodistribute per quanto riguarda i dischi rigidi virtuali tramite gli account di archiviazione di Azure diverse considerazioni per questo metodo anche le distribuzioni di. Mezzo hello numero di operazioni dei / o rispetto ai limiti di hello di hello Account di archiviazione Azure.

[comment]: <> (MSSedusch TODO But this will use network bandwith and not storage bandwith, doesn't it?)

Informazioni dettagliate su questo tipo di distribuzione sono riportate qui: <https://msdn.microsoft.com/library/dn385720.aspx>

In ordine toostore dati file di SQL Server direttamente in archiviazione Premium di Azure, è necessario un minimo di SQL Server 2014 toohave versione di patch documentato qui: <https://support.microsoft.com/kb/3063054>. L'archiviazione dei file di dati SQL Server nell'archivio Standard di Azure funziona con la versione rilasciata di hello di SQL Server 2014. Tuttavia, hello molto stesse patch contenere un'altra serie di correzioni rendere più affidabile l'utilizzo diretto hello dell'archiviazione Blob di Azure per i backup e il file di dati di SQL Server. È pertanto consigliabile toouse queste patch in generale.

### <a name="sql-server-2014-buffer-pool-extension"></a>Estensione del pool di buffer di SQL Server 2014
In SQL Server 2014 è stata introdotta una nuova funzionalità denominata estensione del pool di buffer. Questa funzionalità estende il pool di buffer hello di SQL Server, che viene mantenuto in memoria con una cache di livello secondo supportata da unità SSD locale di un server o macchina virtuale. In questo modo tookeep un working set superiore di dati 'in memoria'. Tooaccessing confrontati accesso hello di archiviazione di Azure Standard nell'estensione hello del pool di buffer hello memorizzato su unità SSD locale di una macchina virtuale di Azure è più veloce molti fattori.  Pertanto, sfruttando unità D:\ locale hello di tipi VM hello che hanno eccellente IOPS e la velocità effettiva potrebbe essere un hello tooreduce soluzione ragionevole molto IOPS caricare nel servizio di archiviazione Azure e di migliorare notevolmente i tempi di risposta delle query. Questo vale soprattutto quando non si usa Archiviazione Premium. In caso di archiviazione Premium e l'utilizzo di hello di hello Cache di lettura di Azure Premium sul nodo di calcolo hello, come consigliato per i file di dati, non sono previste notevoli differenze. Motivo è che entrambi cache (estensione Pool di Buffer di SQL Server e Cache di lettura di archiviazione Premium) con i dischi locali hello hello di nodi di calcolo.
Per altri dettagli su questa funzionalità, vedere <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>Considerazioni sul backup/ripristino per SQL Server
Quando si distribuisce SQL Server in Azure, è necessario rivedere la metodologia di backup. Anche se il sistema di hello non è un sistema di produzione, hello SAP ospitato da SQL Server deve essere eseguito il backup database periodicamente. Poiché l'archiviazione di Azure vengono conservate tre immagini, una copia di backup è meno importante riguardo toocompensating un arresto anomalo del sistema di archiviazione. Hello priorità per la gestione di un piano di backup e ripristino corretta, infatti, più che è possibile compensare errori logici o manuali grazie alle funzionalità di ripristino ora. Obiettivo di hello è tooeither utilizzare backup toorestore hello database back-tooa determinato punto nel tempo o toouse backup hello in Azure tooseed un altro sistema mediante la copia di database esistente di hello. Ad esempio, è possibile eseguire il trasferimento da un'installazione di sistema a 3 livelli a 2 livelli SAP configurazione tooa di hello stesso sistema ripristinando un backup.

Esistono tre modi diversi toobackup SQL Server tooAzure archiviazione:

1. SQL Server 2012 CU4 e l'URL di tooa in modo nativo i backup di database può essere superiore. Questo è descritta in dettaglio nel blog di hello [nuove funzionalità di miglioramenti di Backup e ripristino di SQL Server 2014 – parte 5 –](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Vedere il capitolo [SQL Server 2012 SP1 CU4 and later][dbms-guide-5.5.1] (SQL Server 2012 SP1 CU4 e versioni successive).
2. TooSQL precedenti versioni di SQL Server 2012 CU4 possono usare un tooa toobackup funzionalità di reindirizzamento disco rigido virtuale e spostare il flusso di scrittura hello verso un percorso di archiviazione di Azure che è stato configurato. Vedere il capitolo [SQL Server 2012 SP1 CU3 and earlier releases][dbms-guide-5.5.2] (SQL Server 2012 SP1 CU3 e versioni precedenti).
3. metodo finale Hello è tooperform un comando di toodisk backup convenzionale di SQL Server in un dispositivo disco VHD.  Questo è identica toohello modello di distribuzione locale e non viene illustrato in dettaglio in questo documento.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 e versioni successive
Questa funzionalità consente toodirectly tooAzure backup nell'archiviazione BLOB. Senza questo metodo, è necessario eseguire il backup tooother dischi rigidi virtuali Azure consumando la capacità del disco rigido virtuale e IOPS. Hello idea è sostanzialmente questa:

 ![Utilizzo di Backup di SQL Server 2012 tooMicrosoft BLOB di archiviazione di Azure][dbms-guide-figure-400]

in questo caso, il vantaggio di Hello è che non è necessario backup di SQL Server toostore toospend dischi rigidi virtuali in. Pertanto, si dispone di meno i dischi rigidi virtuali allocati e hello tutta la larghezza di banda di IOPS VHD può essere utilizzato per i file di dati e di log. Si noti che hello massima di un backup sia limitato tooa massimo di 1 TB come descritto nella sezione hello 'Limitazioni' in questo articolo: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Se le dimensioni, dimensioni del backup hello, nonostante l'utilizzo di SQL Server Backup compression dovesse superare 1 TB, hello funzionalità descritta nel capitolo [SQL Server 2012 SP1 CU3 e versioni precedenti] [ dbms-guide-5.5.2] di questo documento toobe utilizzato.

[La documentazione pertinente](https://msdn.microsoft.com/library/dn449492.aspx) che descrive il ripristino di hello del database dal backup su archivio Blob di Azure è consigliabile non toorestore direttamente dall'archivio BLOB di Azure se i backup hello > 25 GB. indicazione Hello in questo articolo è semplicemente basata su considerazioni sulle prestazioni e non a causa di restrizioni toofunctional. Le condizioni applicabili possono quindi variare caso per caso.

La documentazione relativa alla configurazione e all'uso di questo tipo di backup è disponibile in [questa](https://msdn.microsoft.com/library/dn466438.aspx) esercitazione

Un esempio di hello sequenza di passaggi può essere letti [qui](https://msdn.microsoft.com/library/dn435916.aspx).

L'automatizzazione di backup, è della massima importanza toomake, assicurarsi che i BLOB hello per ogni backup sono denominati in modo diverso. In caso contrario, verranno sovrascritti e hello ripristino catena è stata interrotta.

In ordine non toomix tra tipi diversi di hello 3 di backup, è consigliabile toocreate contenitori diversi sotto l'account di archiviazione hello usato per i backup. contenitori di Hello potrebbe essere solo dalla macchina virtuale o al tipo di macchina virtuale e di Backup. come potrebbe apparire schema Hello:

 ![Con Backup di SQL Server 2012 tooMicrosoft BLOB di archiviazione di Azure-contenitori diversi account di archiviazione separato][dbms-guide-figure-500]

Nell'esempio hello in precedenza, hello i backup non verrà eseguiti nella stessa risorsa di archiviazione di account in cui hello hello vengono distribuite le macchine virtuali. Non vi sarà un nuovo account di archiviazione in modo specifico per i backup hello. All'interno gli account di archiviazione hello, non vi sarà diversi contenitori creati con una matrice di tipo hello di backup e hello nome della macchina virtuale. Questa segmentazione renderà più facile tooadministrate hello i backup di hello diverse macchine virtuali.

BLOB Hello direttamente scritti i backup di hello, non viene aggiunto il conteggio toohello di hello dischi rigidi virtuali di una macchina virtuale. Pertanto possibile aumentare al massimo hello dischi rigidi virtuali montati di hello specifico VM SKU per i dati di hello e file di log di transazione ed eseguire comunque un backup in un contenitore di archiviazione.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 e versioni precedenti
primo passaggio Hello in ordine tooachieve è necessario eseguire un backup direttamente nel servizio di archiviazione Azure sarebbe toodownload hello msi collegato troppo[questo](https://www.microsoft.com/download/details.aspx?id=40740) articolo della Knowledge Base.

Scaricare il file di installazione x64 hello e la documentazione di hello. file Hello installerà un programma denominato: 'TooMicrosoft di Backup di Microsoft SQL Server dello strumento di Azure'. Leggere attentamente la documentazione di hello del prodotto hello.  strumento di Hello funziona nel seguente modo hello:

* Dal lato Server SQL hello, viene definito un percorso su disco per il backup di SQL Server hello (non utilizzare unità D:\ hello per questo).
* strumento Hello consente regole toodefine che possono essere utilizzato toodirect diversi tipi di contenitori di archiviazione di Azure toodifferent di backup.
* Una volta regole hello, strumento hello reindirizzerà il flusso di scrittura hello di hello tooone backup di dischi rigidi virtuali e dischi di hello toohello percorso di archiviazione di Azure definito in precedenza.
* Hello strumento lascerà un file di piccole dimensioni stub delle dimensioni di pochi KB nel disco rigido virtuale o disco che è stato definito per SQL Server hello hello backup. **Questo file deve essere lasciato nel percorso di archiviazione hello perché è necessario toorestore nuovamente da archiviazione di Azure.**
  * Se si hanno più file stub hello (ad esempio, in seguito alla perdita hello dei supporti di archiviazione contenente file stub hello) e si è scelto l'opzione hello di backup tooa account di archiviazione di Microsoft Azure, è possibile recuperare il file stub hello tramite l'archiviazione di Microsoft Azure da scaricarlo dal contenitore di archiviazione hello in cui è stato inserito. È quindi consigliabile inserire il file di stub hello in una cartella nel computer locale hello in hello strumento configurato toohello toodetect e il caricamento dello stesso contenitore con hello stessa password di crittografia, se è stata utilizzata la crittografia con la regola originale hello.

Ciò significa schema hello come descritto in precedenza per le versioni più recenti di SQL Server può essere inserito in anche per le versioni di SQL Server che non consentono l'indirizzamento diretto un percorso di archiviazione di Azure.

È consigliabile non usare questo metodo con versioni più recenti di SQL Server che supportano il backup in modalità nativa in Archiviazione di Azure. Le eccezioni sono limitazioni del backup nativo di hello in Azure bloccano in esecuzione del backup nativo in Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Altri database di SQL Server toobackup possibilità
Altri database toobackup possibilità è tooattach tooa di dischi rigidi virtuali aggiuntivo macchina virtuale che si utilizzano backup toostore in. In questo caso è necessario assicurarsi che toomake tale hello dischi rigidi virtuali non sono in esecuzione completa. Se è questo caso di hello, sarebbe necessario toounmount hello disco rigido virtuale e pertanto toospeak "archiviarlo" e sostituirlo con un nuovo disco rigido virtuale vuoto. Se si passa il percorso verso il basso, si desidera tookeep questi dischi rigidi virtuali negli account di archiviazione di Azure separate da quelle che hello dischi rigidi virtuali con file di database hello hello.

Una seconda possibilità è toouse una macchina virtuale di grandi dimensioni che può avere molti dischi rigidi virtuali collegati. Ad esempio, D14 con 32 dischi rigidi virtuali. Utilizzare un ambiente flessibile in cui è possibile creare condivisioni utilizzate quindi come destinazioni di backup per server DBMS diversi hello toobuild di spazi di archiviazione.

Per la documentazione su alcune procedure consigliate, vedere anche [qui](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) .

#### <a name="performance-considerations-for-backupsrestores"></a>Considerazioni sulle prestazioni per backup/ripristini
Come nelle distribuzioni bare metal, le prestazioni di backup/ripristino dipende del numero di volumi può essere letti in parallelo e velocità effettiva quali hello di tali volumi potrebbe essere. Inoltre, hello CPU usata dalla compressione dei backup potrebbe svolgono un ruolo significativo in macchine virtuali con solo i thread di CPU too8. Si può quindi presumere quanto segue:

* Hello meno hello numero di dischi rigidi virtuali utilizzati file di dati toostore hello, hello hello minore velocità effettiva complessiva in lettura.
* numero inferiore di hello di thread CPU nella macchina virtuale hello Hello, hello più grave impatto hello della compressione di backup.
* Hello toowrite destinazioni (BLOB o VHD) meno hello backup per, hello minore velocità effettiva di hello.
* prova prova più piccola dimensioni delle macchine Virtuali, hello più piccoli hello velocità effettiva quota di archiviazione scrittura e lettura da archiviazione di Azure. Indipendentemente dal fatto che se i backup hello sono archiviati direttamente nel Blob di Azure o se vengono archiviati nei dischi rigidi virtuali nuovamente archiviati nel BLOB di Azure.

Quando si utilizza un BLOB di archiviazione di Microsoft Azure come destinazione di backup hello nelle versioni più recenti, si è limitati toodesignating solo uno di URL di destinazione per ogni backup specifico.

Ma quando si utilizza hello "Backup di Microsoft SQL Server tooMicrosoft strumento di Azure' nelle versioni precedenti, è possibile definire più di una destinazione file. Con più destinazioni, possono essere ridimensionati backup hello e hello velocità effettiva del backup hello è superiore. Questo porterebbe quindi in più file nonché hello account di archiviazione di Azure. Durante il test utilizzando più destinazioni file è possibile ottenere la velocità effettiva hello che si otterrebbe con estensioni backup hello implementate a partire da SQL Server 2012 SP1 CU4. Inoltre non vengono bloccate dal limite di 1TB hello come backup nativo di hello in Azure.

Tuttavia, tenere presente, la velocità effettiva hello anche dipendente nel percorso di hello dell'Account di archiviazione di Azure utilizzare per il backup di hello hello. Un'idea potrebbe essere l'account di archiviazione toolocate hello in macchine virtuali in esecuzione in un'area diversa di hello. Ad esempio, eseguire configurazione della macchina virtuale hello in Europa, ma si deve inserire hello Account di archiviazione utilizzare tooback fronteggiare in Europa settentrionale. Che certamente avrà un impatto sulla velocità effettiva del backup hello ed è probabilmente non toogenerate una velocità effettiva di 150MB/sec come sembra toobe nei casi in cui hello archiviazione di destinazione e hello macchine virtuali sono in esecuzione in hello stesso Data Center regionale.

#### <a name="managing-backup-blobs"></a>Gestione dei BLOB di backup
È un backup di hello toomanage requisito per conto proprio. Poiché si prevede di hello che verranno creati molti BLOB tramite l'esecuzione di backup del log delle transazioni frequenti, amministrazione di questi BLOB può facilmente sovraccaricare hello portale di Azure. È pertanto consigliabile tooleverage di esplorazione dell'archiviazione Azure. Sono disponibili alcuni ottimi strumenti che consentono di toomanage un account di archiviazione di Azure

* Microsoft Visual Studio con Azure SDK installato (<https://azure.microsoft.com/downloads/>)
* Esplora archivi di Microsoft Azure (<https://azure.microsoft.com/downloads/>)
* Strumenti di terze parti

[comment]: <> (Not yet supported on ARM)
[comment]: <> (#### Azure VM backup)
[comment]: <> (Macchine virtuali nel sistema SAP hello possono essere eseguite utilizzando la funzionalità di Backup di macchine virtuali di Azure. Backup della macchina virtuale Azure introdotto nelle prime fasi anno hello 2015 e nel frattempo è toobackup un metodo standard per una macchina virtuale completezza in Azure. Backup di Azure consente di archiviare i backup hello in Azure e consente un ripristino di una macchina virtuale.)
[comment]: <> (Le macchine virtuali che l'esecuzione possono essere backup dei database in modo coerente se supporta sistemi DBMS di hello hello servizio Copia Shadow del Volume Windows VSS < https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> come SQL Server. In modo tramite VM Azure backup può essere un tooa tooget modo possibile ripristinare backup di un database SAP. However, be aware that based on Azure VM backups point-in-time restores of databases is not possible. Pertanto, indicazione hello è tooperform backup dei database con funzionalità DBMS invece di basarsi sui Backup di VM di Azure.)
[comment]: <> (tooget familiarità con Backup di macchine virtuali di Azure, iniziare da qui < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Utilizzo di un'immagine di SQL Server insufficiente hello Microsoft Azure Marketplace
Microsoft offre le macchine virtuali in hello Azure Marketplace che già contengono le versioni di SQL Server. Per i clienti SAP che necessitano di licenze per SQL Server e Windows, potrebbe trattarsi di una necessità di opportunità toobasically copertura hello per le licenze adottando macchine virtuali con SQL Server già installato. Ordine toouse tali immagini per SAP, hello considerazioni seguenti devono essere apportate toobe:

* le versioni non di valutazione di SQL Server Hello presentano costi più elevati rispetto a solo un 'Solo Windows' macchina virtuale distribuita da Azure Marketplace. Vedere i prezzi toocompare questi articoli: <https://azure.microsoft.com/pricing/details/virtual-machines/> e <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* È possibile usare solo versioni di SQL Server supportate da SAP, come SQL Server 2012.
* regole di confronto di Hello dell'istanza di SQL Server hello che viene installato nelle macchine virtuali hello presenti hello Azure Marketplace non è toorun istanza di SQL Server hello richiede che le regole di confronto hello SAP NetWeaver. È possibile modificare le regole di confronto di hello nonostante con istruzioni hello nella seguente sezione hello.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Hello la modifica delle regole di confronto di SQL Server di una macchina virtuale di Microsoft Windows/SQL Server
Poiché le immagini di SQL Server hello in hello Azure Marketplace non sono configurate regole di confronto hello toouse richiesto dalle applicazioni SAP NetWeaver, deve toobe modificato immediatamente dopo la distribuzione di hello. Per SQL Server 2012, questa operazione può essere eseguita con hello i passaggi seguenti appena hello macchina virtuale è stata distribuita e un amministratore è in grado di toolog in hello distribuito macchina virtuale:

* Aprire una finestra di comando di Windows come amministratore.
* Modificare hello directory tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Eseguire il comando hello: Setup.exe /QUIET /ACTION = REBUILDDATABASE /INSTANCENAME = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`> /SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> hello account è stato definito come account di amministratore di hello quando si distribuisce hello VM per hello prima volta attraverso il gallery hello.

processo Hello operazione può richiedere alcuni minuti. In ordine toomake che, se il passaggio di hello finisce con risultato corretto hello, eseguire hello alla procedura seguente:

* Aprire SQL Server Management Studio.
* Aprire una finestra di query.
* Eseguire hello comando sp_helpsort nel database master di SQL Server hello.

il risultato desiderato Hello dovrebbe essere simile:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Se questo non è risultato hello, interrompere la distribuzione di SAP e analizzare i motivi per cui il comando di installazione di hello non ha funzionato come previsto. Distribuzione di applicazioni SAP NetWeaver in istanza di SQL Server con tabelle codici diverse di SQL Server rispetto a quello indicato in precedenza hello è **non** supportato.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Disponibilità elevata di SQL Server per SAP in Azure
Come accennato in precedenza in questo documento, non possibilità toocreate condivise di archiviazione è necessaria per l'utilizzo di hello di funzionalità a disponibilità elevata SQL Server meno recente hello. Questa funzionalità potrebbe installare due o più istanze di SQL Server in un Server Failover Cluster WSFC (Windows) con un disco condiviso per i database utente hello (e tempdb). Questo metodo di elevata disponibilità standard molto tempo hello, che è anche supportato da SAP è. Azure però non supporta l'archiviazione condivisa, di conseguenza non è possibile realizzare configurazioni a disponibilità elevata di SQL Server con cluster di tipo disco condiviso. Tuttavia, molti altri metodi di disponibilità elevata sono comunque possibili e vengono descritti in hello le sezioni seguenti.

[comment]: <> (Articolo è ancora tooASM fa riferimento)
[comment]: <> (Prima di leggere le tecnologie di disponibilità elevata specifico diverso hello utilizzabile per SQL Server in Azure, è un ottimo documento che fornisce ulteriori dettagli e i puntatori [[qui] Virtual-Machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Log shipping SQL Server
Uno dei metodi di hello della disponibilità elevata (HA) è la distribuzione dei Log di SQL Server. Se le macchine virtuali hello partecipa alla configurazione a disponibilità elevata hello utilizza la risoluzione dei nomi, non si è verificato alcun problema e l'installazione di hello in Azure non sarà diversa da qualsiasi programma di installazione viene eseguita in locale. Non è consigliabile toorely solo alla risoluzione IP. Per quanto riguarda toosetting di Log Shipping e principi hello relativi Log Shipping, vedere la documentazione:

<https://technet.microsoft.com/library/ms187103.aspx>

In ordine tooreally ottenere una disponibilità elevata, è necessario che uno toodeploy hello macchine virtuali che sono all'interno di tali toobe di una configurazione Log Shipping all'interno di hello stesso Set di disponibilità.

#### <a name="database-mirroring"></a>Mirroring del database
Mirroring del database come supportato da SAP (vedere la nota SAP [965908]) si basa sulla definizione di un partner di failover nella stringa di connessione SAP hello. Per i casi di hello Cross-premise, si presuppone che hello due macchine virtuali sono in hello nello stesso dominio e che eseguono istanze di SQL Server hello due contesto utente hello in sono utenti di dominio e disporre di privilegi sufficienti in istanze di SQL Server hello due coinvolte. Pertanto, il programma di installazione di hello del mirroring del Database in Azure non differiscono tra una configurazione tipica locale.

Come le distribuzioni solo Cloud, di metodo più semplice di hello è toohave un altro dominio del programma di installazione in Azure toohave tali macchine virtuali DBMS (e macchine virtuali SAP dedicate) all'interno di un dominio.

Se un dominio non è possibile, anche possibile usare i certificati per il database di hello gli endpoint del mirroring, come descritto qui: <https://technet.microsoft.com/library/ms191477.aspx>

Un'esercitazione tooset-up del mirroring del Database in Azure sono disponibili qui: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
Come AlwaysOn è supportato per SAP in locale (vedere la nota SAP [1772688]), è supportato toobe utilizzato in combinazione con SAP in Azure. fatti Hello che non si è in grado di toocreate condiviso dischi in Azure non significa che uno non è possibile creare una configurazione di AlwaysOn Windows Server Failover Cluster (WSFC) tra diverse macchine virtuali. Significa solo che non si dispone hello possibilità toouse un disco condiviso come quorum nella configurazione del cluster hello. Di conseguenza è possibile compilare una configurazione di WSFC AlwaysOn in Azure e non semplicemente la Seleziona tipo di quorum hello che usa il disco condiviso. Hello ambiente Azure tali macchine virtuali distribuite in viene risolto hello macchine virtuali in base al nome e deve essere hello hello macchine virtuali nello stesso dominio. Queste indicazioni sono valide solo per distribuzioni solo Azure e cross-premise. Esistono alcune considerazioni sulla distribuzione hello listener del gruppo di disponibilità di SQL Server (non toobe confusa con il Set di disponibilità di Azure hello) poiché in questo momento Azure non consente toosimply creare un oggetto AD/DNS come è possibile on-premise. Di conseguenza, alcuni passaggi di installazione diversa sono necessarie tooovercome comportamento specifico di hello di Azure.

Di seguito sono elencate alcune considerazioni relative all'uso di un listener del gruppo di disponibilità.

* Tramite un listener del gruppo di disponibilità è possibile solo con Windows Server 2012 o Windows Server 2012 R2 come sistema operativo guest della macchina virtuale hello. Per Windows Server 2012 è necessario assicurarsi che si applica la patch toomake: <https://support.microsoft.com/kb/2854082>
* Per Windows Server 2008 R2 questa patch non esiste e sarebbe necessario AlwaysOn toobe utilizzato in hello stesso modo del Mirroring del Database specificando un partner di failover nella stringa di connessione hello (tramite hello SAP default.pfl dbs parametro/mss/server – vedere la nota SAP [965908]).
* Quando tramite un listener del gruppo di disponibilità, le macchine virtuali Database hello necessario toobe connesso tooa dedicato bilanciamento del carico. La risoluzione dei nomi nelle distribuzioni solo Cloud richiederebbe una tutte le macchine virtuali di un sistema SAP (server applicazioni, server DBMS e server (A) SCS) siano in hello stessa rete virtuale o richiederebbe da una manutenzione di hello livello applicazione SAP del file etc hello in ordine tooget hello nomi di macchina virtuale di hello risolto macchine virtuali SQL Server. In ordine tooavoid che Azure assegni nuovi indirizzi IP nei casi in cui entrambe le macchine virtuali tra l'altro arresto, è necessario assegnare indirizzi IP statici toohello interfacce di rete di tali macchine virtuali nella configurazione AlwaysOn hello (definizione di un indirizzo IP statico è descritta in [questo] [ virtual-networks-reserved-private-ip] articolo)

[comment]: <> (Blog precedente)
[comment]: <> (<https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, <https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>)
* Esistono passaggi speciali necessari per la compilazione di configurazione del cluster WSFC hello in cui è necessario un indirizzo IP specifico cluster hello assegnato, poiché Azure con le funzionalità correnti è necessario assegnare il nome del cluster hello hello nello stesso indirizzo IP del cluster di hello nodo hello viene creato. Ciò significa che un passaggio manuale deve essere eseguita tooassign un cluster di toohello di indirizzo IP diverso.
* Hello listener del gruppo di disponibilità è in corso toobe creato in Azure con gli endpoint TCP/IP che vengono assegnati le macchine virtuali toohello in esecuzione le repliche primarie e secondarie hello hello del gruppo di disponibilità.
* Potrebbe esserci un toosecure necessità questi endpoint con gli ACL.

[comment]: <> (TODO old blog)
[comment]: <> (i passaggi dettagliati Hello e qualsiasi cosa per il dell'installazione di una configurazione di AlwaysOn in Azure, è consigliabile fare riferimento hello esercitazione disponibile [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Configurazione AlwaysOn tramite hello Azure raccolta preconfigurato < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Creating an Availability Group Listener is best described in [this][virtual-machines-windows-classic-ps-sql-int-listener] tutorial)
[comment]: <> (Securing network endpoints with ACLs are explained best here:)
[comment]: <> (*    <https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx&gt; )
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx&gt;)

È possibile toodeploy un gruppo di disponibilità AlwaysOn di SQL Server su nonché diverse regioni di Azure. Questa funzionalità sfrutta la connettività hello Azure a rete virtuale a ([ulteriori dettagli][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (TODO old blog)
[comment]: <> (l'installazione di Hello di gruppi di disponibilità AlwaysOn di SQL Server in tale scenario è descritto di seguito: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Riepilogo sulla disponibilità elevata di SQL Server in Azure
Dato delle tabelle dei fatti hello che di archiviazione di Azure protegge il contenuto di hello, sussiste una minore tooinsist motivo su un'immagine hot standby. Questo significa che lo scenario di disponibilità elevata deve tooonly proteggersi da hello seguenti casi:

* Indisponibilità di hello VM nel suo complesso a causa di toomaintenance nel cluster di server hello in Azure o per altri motivi
* Problemi software nell'istanza di SQL Server hello
* Protezione da errori manuali nel caso in cui i dati vengono eliminati ed è necessario il ripristino temporizzato

Osservando le tecnologie corrispondenti una possibile sostengono che i primi due casi hello possono essere gestiti mediante il mirroring del Database o AlwaysOn, mentre il terzo caso hello solo possibile coperto dal Log Shipping.

Sarà necessario toobalance hello installazione più complessa di AlwaysOn, confrontati tooDatabase Mirroring, i vantaggi di hello di AlwaysOn. I vantaggi includono:

* Repliche secondarie leggibili.
* Backup da repliche secondarie.
* Migliore scalabilità.
* Possibilità di creare più repliche secondarie.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Riepilogo generale su SQL Server per SAP in Azure
Questa guida contiene numerosi consigli che è preferibile leggere più volte prima di pianificare la distribuzione di Azure. In generale, tuttavia, essere certi toofollow hello primi dieci sistemi DBMS in punti specifici di Azure:

[comment]: <> (2.3 higher throughput than what? Than one VHD?)
1. Utilizzare hello ultima versione del sistema DBMS, ad esempio SQL Server 2014, con la maggior parte dei vantaggi di hello in Azure. Per SQL Server, si tratta di SQL Server 2012 SP1 CU4 che include funzionalità di hello di backup diretto di archiviazione di Azure. Tuttavia, in combinazione con SAP, la raccomandazione almeno aggiornamento Cumulativo più recente di SQL Server 2014 SP1 CU1 o SQL Server 2012 SP2 e hello.
2. Pianificare attentamente il landscape del sistema SAP in Azure toobalance layout dei file di dati hello e le limitazioni di Azure:
   * Non è un numero eccessivo di dischi rigidi virtuali, ma dispone di sufficiente tooensure può raggiungere le operazioni di IOPS necessarie.
   * Tenere presente che il numero di operazioni di I/O al secondo varia a seconda dell'account di archiviazione di Azure e che tali account di archiviazione sono limitati nelle singole sottoscrizioni di Azure ([maggiori dettagli][azure-subscription-service-limits]).
   * Solo striping tra dischi rigidi virtuali se è necessario tooachieve una velocità effettiva superiore.
3. Non installare software o inserire i file che richiedono la persistenza in hello unità D:\ quelle non permanente e qualsiasi elemento in questa unità andranno persi al riavvio di Windows.
4. Non usare il caching dei dischi rigidi virtuali di Azure per l'archiviazione Standard di Azure.
5. Non usare account di archiviazione con replica geografica di Azure.  Usare l'opzione Con ridondanza locale per i carichi di lavoro DBMS.
6. Utilizzare i dati del fornitore del sistema DBMS HA/DR soluzione tooreplicate database.
7. Usare sempre la risoluzione dei nomi e non fare affidamento sugli indirizzi IP.
8. Utilizzare hello compressione di database massima possibile. Per SQL Server si tratta della compressione di pagina.
9. Assicurarsi che l'utilizzo di immagini di SQL Server da hello Azure Marketplace. Se si utilizza hello di SQL Server, è necessario modificare le regole di confronto di hello istanza prima di installare qualsiasi sistema SAP NetWeaver su di esso.
10. Installare e configurare SAP Host Monitoring per Azure hello, come descritto in [Guida alla distribuzione][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Le specifiche tooSAP ASE in Windows
A partire da Microsoft Azure, è possibile migrare i tooAzure di applicazioni SAP ASE macchine virtuali esistenti. SAP ASE in una macchina virtuale consente di tooreduce hello costo totale di proprietà di distribuzione, gestione e manutenzione di applicazioni breadth aziendali eseguendo facilmente la migrazione di questi tooMicrosoft applicazioni Azure. Con SAP ASE in una macchina virtuale di Azure, gli amministratori e sviluppatori possono ancora usare hello stessi strumenti di sviluppo e amministrazione disponibili in locale.

È un contratto di servizio per hello macchine virtuali di Azure che sono disponibili qui: <https://azure.microsoft.com/support/legal/sla>

Si è certi di Microsoft Azure verrà prestazioni molto elevate macchine virtuali ospitate nelle offerte di virtualizzazione di confronto tooother cloud pubblico, ma i singoli risultati possono variare. SAP ridimensionamento numeri SAP di hello SAP diversi certificati SKU di macchina virtuale verrà fornito in una nota SAP separato [1928533].

Istruzioni e indicazioni nell'utilizzo toohello considerare di archiviazione di Azure, la distribuzione di macchine virtuali SAP o SAP Monitoring si applicano toodeployments di SAP ASE in combinazione con le applicazioni SAP, come indicato in tutto hello primi quattro capitoli di questo documento.

### <a name="sap-ase-version-support"></a>Supporto della versione di SAP ASE
SAP supporta attualmente SAP ASE versione 16.0 per l'uso con i prodotti SAP Business Suite. Tutti gli aggiornamenti per il server SAP ASE o toobe di driver ODBC e JDBC utilizzato con i prodotti vengono forniti esclusivamente tramite SAP Business Suite hello SAP Service Marketplace in: <https://support.sap.com/swdc>.

Come per le installazioni locali, non scaricare gli aggiornamenti per il server SAP ASE hello o per hello JDBC e i driver ODBC direttamente da siti Web di Sybase. Per informazioni dettagliate sulle patch che sono supportati per l'utilizzo con i prodotti SAP Business Suite in locale e nelle macchine virtuali di Azure vedere hello note su SAP seguenti:

* [1590719]
* [1973241]

Informazioni generali sull'esecuzione di SAP Business Suite in SAP ASE sono reperibile in hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Linee guida per la configurazione di SAP ASE per le installazioni di SAP ASE correlate a SAP nelle VM di Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Struttura di distribuzione di SAP ASE hello
In conformità con descrizione generale di hello, gli eseguibili SAP ASE devono essere disponibile oppure installati nell'unità di sistema hello di hello della macchina virtuale VHD di base (unità c:\). In genere, la maggior parte dei database di sistema e gli strumenti di SAP ASE hello non sono realmente utilizzata rigido dal carico di lavoro di SAP NetWeaver. Pertanto hello sistema e i database di strumenti (master, model, saptools, sybmgmtdb, sybsystemdb) possono rimanere su hello C:\drive.

Un'eccezione può essere il database temporaneo di hello che contiene tutte le tabelle di lavoro e le tabelle temporanee create da SAP ASE, che in caso di alcune ERP SAP e tutti i carichi di lavoro BW potrebbe richiedere il volume di dati maggiore o volume di operazioni dei / o che non si adattata hello originale VHD di base della macchina virtuale (l'unità c:\).

A seconda di hello versione SAPInst/SWPM utilizzato system hello tooinstall, hello database potrebbe contenere:

* Un solo tempdb SAP ASE creato durante l'installazione di SAP ASE
* Un tempdb SAP ASE creato mediante l'installazione di SAP ASE e un saptempdb aggiuntivi creati da hello routine di installazione di SAP
* Un tempdb SAP ASE creato mediante l'installazione di SAP ASE e un tempdb aggiuntivi che è stato creato manualmente (ad esempio, dopo la nota SAP [1752266]) ai requisiti di tempdb specifico di toomeet ERP/BW

In caso di ERP specifico o tutti i carichi di lavoro BW ha senso, in tooperformance conto, i dispositivi di tempdb hello tookeep di hello inoltre creata tempdb (tramite SWPM o manualmente) in un'unità diversa da C:\. Se nessun tempdb aggiuntivi esistente, è consigliabile toocreate uno (nota SAP [1752266]).

Per hello tali sistemi è necessario eseguire i passaggi seguenti per hello inoltre creata tempdb:

* Spostare hello prima tempdb dispositivo toohello primo dispositivo del database SAP hello
* Aggiungere tooeach dispositivi tempdb di dischi rigidi virtuali contenenti un dispositivi del database SAP hello hello

Questo tooeither tempdb di configurazione consente di utilizzare più spazio rispetto a unità di sistema di hello è in grado di tooprovide. Come riferimento una possibile controllare le dimensioni di dispositivo tempdb hello nei sistemi esistenti in cui vengono eseguiti in locale. O una configurazione di questo tipo verrebbe IOPS eseguite tempdb che non può essere fornito con unità di sistema hello. Nuovamente sistemi che eseguono in locale possono essere utilizzati toomonitor i/o il carico di lavoro nel database tempdb.

Non inserire tutti i dispositivi SAP ASE in hello unità D:\ della macchina virtuale hello. Questo vale anche toohello tempdb, anche se gli oggetti di hello mantenuti in tempdb hello sono solo temporanei.

#### <a name="impact-of-database-compression"></a>Impatto della compressione del database
Nelle configurazioni in cui la larghezza di banda dei / o può diventare un fattore limitante, ogni misura riducendo il numero di IOPS può contribuire a carico di lavoro di hello toostretch può eseguire in uno scenario IaaS come Azure. Pertanto, è consigliabile assicurarsi che la compressione di SAP ASE viene utilizzata prima di caricare un tooAzure di database SAP esistente toomake.

la compressione di Hello raccomandazione tooperform prima del caricamento tooAzure se non è già stato implementato è dato da diversi motivi:

* quantità di Hello di dati caricato toobe tooAzure è inferiore
* durata Hello dell'esecuzione di compressione di hello è più breve, supponendo che sia possibile usare hardware più potente con più CPU o della larghezza di banda dei / o maggiore o minore latenza i/o in locale
* Database di dimensioni più piccolo potrebbe causare costi tooless per l'allocazione dei dischi

Il funzionamento della compressione dati e LOB in una VM ospitata in macchine virtuali di Azure è uguale a quello in locale. Per ulteriori informazioni sulla modalità toocheck se la compressione è già in uso in una versione esistente di SAP ASE database verificare la nota SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Utilizzo di istanze di Database toomonitor DBACockpit
Per i sistemi SAP che usano SAP ASE come piattaforma di database, è accessibile come le finestre del browser incorporato nella transazione DBACockpit o Webdynpro hello DBACockpit. Tuttavia hello funzionalità complete per il monitoraggio e amministrazione database hello è disponibile nell'implementazione di Webdynpro hello di hello DBACockpit.

Come con locale sistemi che diversi passaggi sono necessari tooenable utilizzata dall'implementazione di Webdynpro hello di hello DBACockpit tutte le funzionalità di SAP NetWeaver. Seguire la nota SAP [1245200] tooenable hello sull'utilizzo di webdynpros e generare hello necessari quelle. Quando istruzioni hello seguenti in hello sopra si configurerà hello Gestione comunicazioni Internet (icm) insieme a note hello toobe porte utilizzate per le connessioni http e https. impostazione predefinita Hello per http è simile al seguente:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

e collegamenti hello generati in transazione DBACockpit avrà un aspetto simile toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

A seconda se e come hello host macchina virtuale di Azure di hello sistema SAP è connesso tramite site-to-site, multi-site o ExpressRoute (distribuzione Cross-premise) toomake è necessario che tale ICM utilizza un nome host completo che può essere risolto in hello computer in cui si sta provando tooopen hello DBACockpit da. Vedere la nota SAP [773830] toounderstand come ICM determina hello in modo esplicito il nome host completo in base a parametri del profilo e set parametro icm/host_name_full se necessario.

Se è stato distribuito hello macchina virtuale in uno scenario solo Cloud senza connettività tra più sedi locali e Azure, è necessario toodefine un indirizzo IP pubblico e un domainlabel. formato di Hello del nome DNS pubblico hello di hello VM sarà quindi simile al seguente:

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Ulteriori dettagli correlato è disponibile il nome DNS toohello [qui][virtual-machines-azurerm-versus-azuresm].

Impostazione hello SAP profilo parametro icm/host_name_full toohello nome DNS del collegamento di hello hello Azure VM potrebbe essere simile a:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

In questo caso è necessario toomake assicurarsi di:

* Aggiungere le regole in entrata toohello, il gruppo di sicurezza di rete nel portale di Azure di hello per le porte TCP/IP hello utilizzato toocommunicate con ICM
* Aggiungere una configurazione di Windows Firewall toohello le regole in entrata per hello TCP/IP porte usate toocommunicate con hello ICM

Per importata un processo automatico di tutte le correzioni disponibili, è consigliabile tooperiodically applicare hello correzione raccolta SAP nota tooyour applicabile SAP versione:

* [1558958]
* [1619967]
* [1882376]

Ulteriori informazioni sul pannello di controllo amministratore di database per SAP ASE sono reperibile in hello note su SAP seguenti:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considerazioni sul backup/ripristino per SAP ASE
Quando si distribuisce SAP ASE in Azure, è necessario rivedere la metodologia di backup. Anche se il sistema di hello non è un sistema di produzione, il database SAP hello ospitato da SAP ASE deve essere periodicamente il backup. Poiché l'archiviazione di Azure vengono conservate tre immagini, una copia di backup è meno importante riguardo toocompensating un arresto anomalo del sistema di archiviazione. Hello motivo principale per la gestione di un piano di backup e ripristino corretto è più che è possibile compensare errori logici o manuali grazie alle funzionalità di ripristino ora. Obiettivo di hello è tooeither utilizzare backup toorestore hello database back-tooa determinato punto nel tempo o toouse backup hello in Azure tooseed un altro sistema mediante la copia di database esistente di hello. Ad esempio, è possibile eseguire il trasferimento da un'installazione di sistema a 3 livelli a 2 livelli SAP configurazione tooa di hello stesso sistema ripristinando un backup.

Backup e ripristino di un database in Azure funziona hello stesso Analogamente a quanto accade in locale. Vedere le note SAP:

* [1588316]
* [1585981]

per i dettagli sulla creazione di configurazioni di dump e sulla pianificazione dei backup. A seconda dei strategia ed esigenze è possibile configurare database e log dump toodisk su uno dei dischi rigidi virtuali esistenti hello o aggiungere un disco rigido virtuale aggiuntivo per il backup di hello.  rischio hello tooreduce perdita di dati in caso di errore è consigliabile toouse un disco rigido virtuale in cui si trova alcuna periferica di database.

Oltre alla compressione dati e LOB, SAP ASE offre anche la compressione del backup. esegue il dump toooccupy meno spazio con database hello e di log, è consigliabile la compressione dei backup toouse. Per altre informazioni, vedere la nota SAP [1588316] . La compressione dei backup hello è anche fondamentale tooreduce hello toobe dati trasferiti se si intende backup toodownload o dischi rigidi virtuali contenenti i dump di backup da hello locale tooon macchina virtuale di Azure.

Non usare l'unità D:\ come destinazione dei dump di database o di log.

#### <a name="performance-considerations-for-backupsrestores"></a>Considerazioni sulle prestazioni per backup/ripristini
Come nelle distribuzioni bare metal, le prestazioni di backup/ripristino dipende del numero di volumi può essere letti in parallelo e velocità effettiva quali hello di tali volumi potrebbe essere. Inoltre, hello CPU usata dalla compressione dei backup potrebbe svolgono un ruolo significativo in macchine virtuali con solo i thread di CPU too8. Si può quindi presumere quanto segue:

* Hello numero hello un minor numero di dischi rigidi virtuali toostore hello database i dispositivi di uso, hello hello minore velocità effettiva complessiva in lettura
* numero inferiore di hello di thread CPU nella macchina virtuale hello Hello, hello più grave impatto hello di compressione dei backup
* salve backup per Hello meno toowrite destinazioni (directory di striping, dischi rigidi virtuali), hello minore velocità effettiva di hello

numero di hello tooincrease di destinazioni toowrite toothere sono disponibili due opzioni che possono essere utilizzato/combinati in base alle esigenze:

* Lo striping del volume di destinazione di backup hello su più dischi rigidi virtuali montati della velocità effettiva di IOPS hello tooimprove ordine sul volume con striping
* Creazione di una configurazione di dump livello SAP ASE che utilizza più di una destinazione directory toowrite hello dump per

Lo striping di un volume su più dischi rigidi virtuali montati è stato illustrato prima in questa guida. Per ulteriori informazioni sull'utilizzo di più directory di configurazione di dump SAP ASE hello consultare la documentazione di toohello su sp_config_dump Stored Procedure che è la configurazione dei dump hello toocreate utilizzati in hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Ripristino di emergenza con VM di Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replica dei dati con SAP Sybase Replication Server
Con hello SAP Sybase Server di replica SAP ASE fornisce un soluzione di riserva warm tootransfer transazioni tooa distante percorso del database in modo asincrono.

installazione di Hello e il funzionamento di SRS funziona anche livello funzionale in una macchina virtuale ospitata in servizi macchine virtuali di Azure a quanto accade in locale.

ASE HADR tramite SAP Replication Server è previsto per una versione futura. Verrà testato e rilasciato per le piattaforme Microsoft Azure non appena sarà disponibile.

## <a name="specifics-toosap-ase-on-linux"></a>Le specifiche tooSAP ASE su Linux
A partire da Microsoft Azure, è possibile migrare i tooAzure di applicazioni SAP ASE macchine virtuali esistenti. SAP ASE in una macchina virtuale consente di tooreduce hello costo totale di proprietà di distribuzione, gestione e manutenzione di applicazioni breadth aziendali eseguendo facilmente la migrazione di questi tooMicrosoft applicazioni Azure. Con SAP ASE in una macchina virtuale di Azure, gli amministratori e sviluppatori possono ancora usare hello stessi strumenti di sviluppo e amministrazione disponibili in locale.

Per la distribuzione di macchine virtuali di Azure, è importante tooknow hello ufficiale contratti di servizio che sono disponibili qui: <https://azure.microsoft.com/support/legal/sla>

Le informazioni sul ridimensionamento di SAP e un elenco di SKU di VM con certificazione SAP saranno disponibili nella nota SAP [1928533]. Altri documenti di ridimensionamento SAP per le macchine virtuali di Azure sono disponibili qui <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> e qui <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Istruzioni e indicazioni nell'utilizzo toohello considerare di archiviazione di Azure, la distribuzione di macchine virtuali SAP o SAP Monitoring si applicano toodeployments di SAP ASE in combinazione con le applicazioni SAP, come indicato in tutto hello primi quattro capitoli di questo documento.

Hello due note su SAP seguenti includono informazioni generali su ASE su Linux e ASE in hello Cloud:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Supporto della versione di SAP ASE
SAP supporta attualmente SAP ASE versione 16.0 per l'uso con i prodotti SAP Business Suite. Tutti gli aggiornamenti per il server SAP ASE o toobe di driver ODBC e JDBC utilizzato con i prodotti vengono forniti esclusivamente tramite SAP Business Suite hello SAP Service Marketplace in: <https://support.sap.com/swdc>.

Come per le installazioni locali, non scaricare gli aggiornamenti per il server SAP ASE hello o per hello JDBC e i driver ODBC direttamente da siti Web di Sybase. Per informazioni dettagliate sulle patch che sono supportati per l'utilizzo con i prodotti SAP Business Suite in locale e nelle macchine virtuali di Azure vedere hello note su SAP seguenti:

* [1590719]
* [1973241]

Informazioni generali sull'esecuzione di SAP Business Suite in SAP ASE sono reperibile in hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Linee guida per la configurazione di SAP ASE per le installazioni di SAP ASE correlate a SAP nelle VM di Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Struttura di distribuzione di SAP ASE hello
In conformità con descrizione generale di hello, gli eseguibili SAP ASE devono essere disponibile oppure installati nel sistema di file radice hello di hello VM (/sybase). In genere, la maggior parte dei database di sistema e gli strumenti di SAP ASE hello non sono realmente utilizzata rigido dal carico di lavoro di SAP NetWeaver. Pertanto hello sistema e i database di strumenti (master, model, saptools, sybmgmtdb, sybsystemdb) possono rimanere su hello radice file system nonché.

Un'eccezione può essere il database temporaneo di hello che contiene tutte le tabelle di lavoro e le tabelle temporanee create da SAP ASE, che in caso di alcune ERP SAP e tutti i carichi di lavoro BW potrebbe richiedere il volume di dati maggiore o volume di operazioni dei / o che non si adattata hello originale Disco del sistema operativo della macchina virtuale.

A seconda di hello versione SAPInst/SWPM utilizzato system hello tooinstall, hello database potrebbe contenere:

* Un solo tempdb SAP ASE creato durante l'installazione di SAP ASE
* Un tempdb SAP ASE creato mediante l'installazione di SAP ASE e un saptempdb aggiuntivi creati da hello routine di installazione di SAP
* Un tempdb SAP ASE creato mediante l'installazione di SAP ASE e un tempdb aggiuntivi che è stato creato manualmente (ad esempio, dopo la nota SAP [1752266]) ai requisiti di tempdb specifico di toomeet ERP/BW

In caso di ERP specifico o tutti i carichi di lavoro BW l'aderenza, considerare tooperformance, i dispositivi di tempdb hello tookeep di hello inoltre creata tempdb (tramite SWPM o manualmente) in un sistema file separato che può essere rappresentato da un disco dati di Azure singolo o un sistema RAID Linux che si estende su più dischi dati di Azure. Se nessun tempdb aggiuntivi esistente, è consigliabile toocreate uno (nota SAP [1752266]).

Per hello tali sistemi è necessario eseguire i passaggi seguenti per hello inoltre creata tempdb:

* Spostare hello prima tempdb directory toohello primo file system del database SAP hello
* Aggiungere tooeach directory tempdb di dischi rigidi virtuali contenenti un file System del database SAP hello hello

Questo tooeither tempdb di configurazione consente di utilizzare più spazio rispetto a unità di sistema di hello è in grado di tooprovide. Come riferimento una possibile controllare le dimensioni di directory tempdb hello nei sistemi esistenti in cui vengono eseguiti in locale. O una configurazione di questo tipo verrebbe IOPS eseguite tempdb che non può essere fornito con unità di sistema hello. Nuovamente sistemi che eseguono in locale possono essere utilizzati toomonitor i/o il carico di lavoro nel database tempdb.

Non inserire mai le directory SAP ASE in /mnt o /mnt/resource di hello macchina virtuale. Questo vale anche toohello tempdb, anche se gli oggetti hello mantenuti in tempdb hello sono temporanei solo perché /mnt o /mnt/resource è uno spazio temporaneo di macchina virtuale di Azure predefinito che non è persistente. Ulteriori dettagli su hello spazio temporaneo di macchina virtuale di Azure sono reperibile [in questo articolo][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Impatto della compressione del database
Nelle configurazioni in cui la larghezza di banda dei / o può diventare un fattore limitante, ogni misura riducendo il numero di IOPS può contribuire a carico di lavoro di hello toostretch può eseguire in uno scenario IaaS come Azure. Pertanto, è consigliabile assicurarsi che la compressione di SAP ASE viene utilizzata prima di caricare un tooAzure di database SAP esistente toomake.

la compressione di Hello raccomandazione tooperform prima del caricamento tooAzure se non è già stato implementato è dato da diversi motivi:

* quantità di Hello di dati caricato toobe tooAzure è inferiore
* durata Hello dell'esecuzione di compressione di hello è più breve, supponendo che sia possibile usare hardware più potente con più CPU o della larghezza di banda dei / o maggiore o minore latenza i/o in locale
* Database di dimensioni più piccolo potrebbe causare costi tooless per l'allocazione dei dischi

Il funzionamento della compressione dati e LOB in una VM ospitata in macchine virtuali di Azure è uguale a quello in locale. Per ulteriori informazioni sulla modalità toocheck se la compressione è già in uso in una versione esistente di SAP ASE database verificare la nota SAP [1750510]. Per altre informazioni sulla compressione del database, vedere anche la nota SAP [2121797] .

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Utilizzo di istanze di Database toomonitor DBACockpit
Per i sistemi SAP che usano SAP ASE come piattaforma di database, è accessibile come le finestre del browser incorporato nella transazione DBACockpit o Webdynpro hello DBACockpit. Tuttavia hello funzionalità complete per il monitoraggio e amministrazione database hello è disponibile nell'implementazione di Webdynpro hello di hello DBACockpit.

Come con locale sistemi che diversi passaggi sono necessari tooenable utilizzata dall'implementazione di Webdynpro hello di hello DBACockpit tutte le funzionalità di SAP NetWeaver. Seguire la nota SAP [1245200] tooenable hello sull'utilizzo di webdynpros e generare hello necessari quelle. Quando istruzioni hello seguenti in hello sopra si configurerà hello Gestione comunicazioni Internet (icm) insieme a note hello toobe porte utilizzate per le connessioni http e https. impostazione predefinita Hello per http è simile al seguente:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

e collegamenti hello generati in transazione DBACockpit avrà un aspetto simile toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

A seconda se e come hello host macchina virtuale di Azure di hello sistema SAP è connesso tramite site-to-site, multi-site o ExpressRoute (distribuzione Cross-premise) toomake è necessario che tale ICM utilizza un nome host completo che può essere risolto in hello computer in cui si sta provando tooopen hello DBACockpit da. Vedere la nota SAP [773830] toounderstand come ICM determina hello in modo esplicito il nome host completo in base a parametri del profilo e set parametro icm/host_name_full se necessario.

Se è stato distribuito hello macchina virtuale in uno scenario solo Cloud senza connettività tra più sedi locali e Azure, è necessario toodefine un indirizzo IP pubblico e un domainlabel. formato di Hello del nome DNS pubblico hello di hello VM sarà quindi simile al seguente:

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Ulteriori dettagli correlato è disponibile il nome DNS toohello [qui][virtual-machines-azurerm-versus-azuresm].

Impostazione hello SAP profilo parametro icm/host_name_full toohello nome DNS del collegamento di hello hello Azure VM potrebbe essere simile a:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

In questo caso è necessario toomake assicurarsi di:

* Aggiungere le regole in entrata toohello, il gruppo di sicurezza di rete nel portale di Azure di hello per le porte TCP/IP hello utilizzato toocommunicate con ICM
* Aggiungere una configurazione di Windows Firewall toohello le regole in entrata per hello TCP/IP porte usate toocommunicate con hello ICM

Per importata un processo automatico di tutte le correzioni disponibili, è consigliabile tooperiodically applicare hello correzione raccolta SAP nota tooyour applicabile SAP versione:

* [1558958]
* [1619967]
* [1882376]

Ulteriori informazioni sul pannello di controllo amministratore di database per SAP ASE sono reperibile in hello note su SAP seguenti:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considerazioni sul backup/ripristino per SAP ASE
Quando si distribuisce SAP ASE in Azure, è necessario rivedere la metodologia di backup. Anche se il sistema di hello non è un sistema di produzione, il database SAP hello ospitato da SAP ASE deve essere periodicamente il backup. Poiché l'archiviazione di Azure vengono conservate tre immagini, una copia di backup è meno importante riguardo toocompensating un arresto anomalo del sistema di archiviazione. Hello motivo principale per la gestione di un piano di backup e ripristino corretto è più che è possibile compensare errori logici o manuali grazie alle funzionalità di ripristino ora. Obiettivo di hello è tooeither utilizzare backup toorestore hello database back-tooa determinato punto nel tempo o toouse backup hello in Azure tooseed un altro sistema mediante la copia di database esistente di hello. Ad esempio, è possibile eseguire il trasferimento da un'installazione di sistema a 3 livelli a 2 livelli SAP configurazione tooa di hello stesso sistema ripristinando un backup.

Backup e ripristino di un database in Azure funziona hello stesso Analogamente a quanto accade in locale. Vedere le note SAP:

* [1588316]
* [1585981]

per i dettagli sulla creazione di configurazioni di dump e sulla pianificazione dei backup. A seconda dei strategia ed esigenze è possibile configurare database e log dump toodisk su uno dei dischi rigidi virtuali esistenti hello o aggiungere un disco rigido virtuale aggiuntivo per il backup di hello.  rischio hello tooreduce perdita di dati in caso di errore è consigliabile toouse un disco rigido virtuale in cui si trova alcuna directory o file di database.

Oltre alla compressione dati e LOB, SAP ASE offre anche la compressione del backup. esegue il dump toooccupy meno spazio con database hello e di log, è consigliabile la compressione dei backup toouse. Per altre informazioni, vedere la nota SAP [1588316] . La compressione dei backup hello è anche fondamentale tooreduce hello toobe dati trasferiti se si intende backup toodownload o dischi rigidi virtuali contenenti i dump di backup da hello locale tooon macchina virtuale di Azure.

Non utilizzare hello Azure VM spazio temporaneo /mnt o /mnt/resource come destinazione di dump di database o log.

#### <a name="performance-considerations-for-backupsrestores"></a>Considerazioni sulle prestazioni per backup/ripristini
Come nelle distribuzioni bare metal, le prestazioni di backup/ripristino dipende del numero di volumi può essere letti in parallelo e velocità effettiva quali hello di tali volumi potrebbe essere. Inoltre, hello CPU usata dalla compressione dei backup potrebbe svolgono un ruolo significativo in macchine virtuali con solo i thread di CPU too8. Si può quindi presumere quanto segue:

* Hello numero hello un minor numero di dischi rigidi virtuali toostore hello database i dispositivi di uso, hello hello minore velocità effettiva complessiva in lettura
* numero inferiore di hello di thread CPU nella macchina virtuale hello Hello, hello più grave impatto hello di compressione dei backup
* salve backup per Hello meno toowrite destinazioni (Linux RAID software, i dischi rigidi virtuali), hello minore velocità effettiva di hello

numero di hello tooincrease di destinazioni toowrite toothere sono disponibili due opzioni che possono essere utilizzato/combinati in base alle esigenze:

* Lo striping del volume di destinazione di backup hello su più dischi rigidi virtuali montati della velocità effettiva di IOPS hello tooimprove ordine sul volume con striping
* Creazione di una configurazione di dump livello SAP ASE che utilizza più di una destinazione directory toowrite hello dump per

Lo striping di un volume su più dischi rigidi virtuali montati è stato illustrato prima in questa guida. Per ulteriori informazioni sull'utilizzo di più directory di configurazione di dump SAP ASE hello consultare la documentazione di toohello su sp_config_dump Stored Procedure che è la configurazione dei dump hello toocreate utilizzati in hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Ripristino di emergenza con VM di Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replica dei dati con SAP Sybase Replication Server
Con hello SAP Sybase Server di replica SAP ASE fornisce un soluzione di riserva warm tootransfer transazioni tooa distante percorso del database in modo asincrono.

installazione di Hello e il funzionamento di SRS funziona anche livello funzionale in una macchina virtuale ospitata in servizi macchine virtuali di Azure a quanto accade in locale.

ASE HADR tramite SAP Replication Server NON è attualmente supportato. Potrebbe essere testato con e rilasciato per le piattaforme Microsoft Azure hello future.

## <a name="specifics-toooracle-database-on-windows"></a>Le specifiche tooOracle Database in Windows
Poiché a metà anno 2013, il software Oracle è supportato da Oracle toorun in Microsoft Windows Hyper-V e Azure. Leggere informazioni dettagliate sul supporto generale di hello di Windows Hyper-V e Azure da Oracle tooget questo articolo: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Seguenti supporto generale hello, è supportato anche uno specifico scenario hello di applicazioni SAP sfruttando il database Oracle. I dettagli sono denominati in questa parte del documento hello.

### <a name="oracle-version-support"></a>Supporto della versione di Oracle
Tutti i dettagli sulle versioni di Oracle e le versioni del sistema operativo corrispondenti che sono supportate per l'esecuzione di SAP su Oracle in macchine virtuali Azure sono disponibili nella nota SAP seguente hello [2039619]

Informazioni generali sull'esecuzione di SAP Business Suite in Oracle sono disponibili in SCN: <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Linee guida per la configurazione di Oracle per le installazioni di SAP nelle VM di Azure
#### <a name="storage-configuration"></a>Configurazione dell'archiviazione
È supportata una sola istanza di Oracle che usa dischi formattati NTFS. Tutti i file di database devono essere archiviati in file system di hello NTFS in base a dischi rigidi Virtuali. Questi dischi VHD sono montato toohello macchina virtuale di Azure e si basano sull'archiviazione BLOB di Azure pagina (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Le unità di rete o le condivisioni remote, ad esempio i servizi file di Azure:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**NON** sono supportate per i file di database Oracle.

Utilizzando dischi rigidi virtuali di Azure in archiviazione BLOB di Azure pagina base, hello istruzioni eseguite in questo documento nel capitolo [la memorizzazione nella cache per le macchine virtuali e dischi rigidi virtuali] [ dbms-guide-2.1] e [archiviazione di Microsoft Azure] [ dbms-guide-2.3] applicare toodeployments con hello Database Oracle.

Come illustrato in precedenza in hello generale parte hello documento, esistono quote alla velocità effettiva IOPS per i dischi rigidi virtuali di Azure. Hello esatta le quote in base al tipo di macchina virtuale hello servono. Un elenco di tipi di macchine virtuali con le rispettive quote è disponibile [qui][virtual-machines-sizes]

hello tooidentify supportati tipi di macchine Virtuali di Azure, vedere la nota tooSAP [1928533]

Purché quota di IOPS per ogni disco corrente hello soddisfa i requisiti di hello, è possibile toostore tutti i file hello DB in un unico montato disco rigido virtuale di Azure.

Se più IOPS sono necessari, è consigliabile pool di archiviazione finestra toouse (solo disponibili in Windows Server 2012 e versioni successive) o con striping per Windows 2008 R2 toocreate un dispositivo logico big su più dischi rigidi Virtuali montati di Windows. Vedere anche il capitolo [Software RAID][dbms-guide-2.2] di questo documento. Questo approccio semplifica lo spazio su disco hello hello amministrazione toomanage overhead ed evita sforzo hello toomanually distribuire file tra più dischi rigidi virtuali montati.

#### <a name="backup--restore"></a>Backup/Ripristino
Per il backup / ripristino delle funzionalità, hello BR SAP * strumenti per Oracle sono supportati in hello stesso modo come in standard i sistemi operativi Windows Server e Hyper-V. Gestione del ripristino (RMAN) di Oracle è supportata anche per toodisk di backup e il ripristino dal disco.

#### <a name="high-availability"></a>Disponibilità elevata
[comment]: <> (collegamento fa riferimento tooASM)
Oracle Data Guard è supportato per motivi di disponibilità elevata e ripristino di emergenza. I dettagli sono disponibili in [questa][virtual-machines-windows-classic-configure-oracle-data-guard] documentazione.

#### <a name="other"></a>Altre
Tutti gli altri argomenti generali come set di disponibilità di Azure o SAP monitoring si applicano come descritto in hello primi tre capitoli di questo documento per le distribuzioni di macchine virtuali con hello Database Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Specifiche per hello MaxDB Database SAP in Windows
### <a name="sap-maxdb-version-support"></a>Supporto della versione di SAP MaxDB
SAP supporta attualmente SAP MaxDB versione 7.9 per l'uso con prodotti basati su SAP NetWeaver in Azure. Tutti gli aggiornamenti per il server SAP MaxDB o toobe di driver ODBC e JDBC utilizzata con prodotti basate su SAP NetWeaver vengono forniti esclusivamente tramite hello SAP Service Marketplace in <https://support.sap.com/swdc>.
Le informazioni generali sull'esecuzione di SAP NetWeaver in SAP MaxDB sono disponibili su <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Versioni di Microsoft Windows e tipi di VM di Azure supportati per SAP MaxDB DBMS
versione di Microsoft Windows toofind hello è supportato per SAP MaxDB DBMS in Azure, vedere:

* [Product Availability Matrix (PAM) SAP][sap-pam]
* Nota SAP [1928533]

Versione più recente di hello toouse di hello del sistema operativo Microsoft Windows, ovvero Microsoft Windows 2012 R2, è consigliabile.

### <a name="available-sap-maxdb-documentation"></a>Documentazione disponibile su SAP MaxDB
È possibile trovare l'elenco di hello aggiornata della documentazione di SAP MaxDB nella nota SAP seguente hello [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Linee guida per la configurazione di SAP MaxDB per le installazioni di SAP nelle VM di Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Configurazione dell'archiviazione
Procedure consigliate di archiviazione di Azure per SAP MaxDB seguono le raccomandazioni generali hello indicate nel capitolo [struttura di una distribuzione RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Come altri database, anche SAP MaxDB include file di dati e di log. Tuttavia, la terminologia di SAP MaxDB termine corretto hello è "volume" (non "file"). Esistono, ad esempio, volumi di dati e volumi di log di SAP MaxDB. Non confonderli con i volumi dei dischi del sistema operativo.
>
>

In breve, è necessario:

* Impostare l'account di archiviazione di Azure hello contenente hello SAP MaxDB dati e log volumi (ad esempio file) troppo**archiviazione con ridondanza locale (LRS)** come specificato nel capitolo [archiviazione di Microsoft Azure] [ dbms-guide-2.3].
* Percorso dei / o hello separati per i volumi di dati SAP MaxDB (ad esempio file) dal percorso dei / o hello per volumi di log (ad esempio file). Ciò significa che i volumi di dati (ad esempio file) SAP MaxDB toobe installato in un'unità logica e log MaxDB SAP nei volumi (ad esempio file) è toobe installato in un'altra unità logica.
* Impostare hello file appropriate memorizzazione nella cache per ogni blob di Azure, a seconda se si usano per SAP MaxDB volumi di dati o di log (ad esempio file) e che si utilizzi Standard di Azure o di archiviazione Premium di Azure, come descritto nel capitolo [la memorizzazione nella cache per le macchine virtuali] [ dbms-guide-2.1].
* Purché quota di IOPS per ogni disco corrente hello soddisfa i requisiti di hello, è possibile toostore tutti i volumi di dati hello in un disco rigido virtuale Azure singolo montata e anche archiviare tutti i volumi di log del database in un altro singolo Azure disco rigido virtuale montato.
* Se sono necessarie altre operazioni IOPS e/o spazi, è consigliabile toouse Microsoft finestra pool di archiviazione (solo disponibili in Microsoft Windows Server 2012 e versioni successive) o Microsoft Windows per Microsoft Windows 2008 R2 toocreate con striping un dispositivo logico elevato su più dischi di disco rigido virtuale montati. Vedere anche il capitolo [Software RAID][dbms-guide-2.2] di questo documento. Questo approccio semplifica lo spazio su disco hello hello amministrazione toomanage overhead e si evita di dover distribuire manualmente i file tra più dischi rigidi virtuali montati hello.
* Per i requisiti di IOPS massimi hello, è possibile utilizzare l'archiviazione Premium di Azure, che è disponibile in serie DS e GS-series VM.

![Configurazione di riferimento di una VM IaaS di Azure per SAP MaxDB DBMS][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Backup e ripristino
Quando si distribuisce SAP MaxDB in Azure, è necessario rivedere la metodologia di backup. Anche se il sistema di hello non è un sistema di produzione, hello SAP ospitato da SAP MaxDB deve essere eseguito il backup database periodicamente. Poiché Archiviazione di Azure conserva tre immagini, il backup è ora meno importante dal punto di vista della protezione del sistema da errori di archiviazione e da errori operativi o amministrativi più gravi. Hello motivo principale per la gestione di un backup corretto e un piano di ripristino è in modo che è possibile compensare errori logici o manuali fornendo funzionalità di ripristino in un momento. Hello obiettivo è tooeither utilizzare backup toorestore hello database tooa determinati punto nel tempo o toouse backup hello in Azure tooseed un altro sistema mediante la copia di database esistente di hello. Ad esempio, è possibile eseguire il trasferimento da un'installazione di sistema a 3 livelli a 2 livelli SAP configurazione tooa di hello stesso sistema ripristinando un backup.

Backup e ripristino di un database in Azure funziona hello come avviene per i sistemi locali, è possibile utilizzare MaxDB SAP standard strumenti, che sono descritte in uno dei documenti di documentazione di SAP MaxDB hello backup/ripristino riportato nella nota SAP [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Considerazioni sulle prestazioni per il backup e il ripristino
Come nelle distribuzioni bare metal, le prestazioni di backup e ripristino dipende del numero di volumi può essere letti in parallelo e hello velocità effettiva di tali volumi. Inoltre, hello CPU usata dalla compressione dei backup può riprodurre un ruolo significativo in macchine virtuali con i thread CPU too8. Si può quindi presumere quanto segue:

* numero di hello un minor numero di dischi rigidi virtuali usati toostore hello database dispositivi Hello, hello inferiore hello complessivo della velocità effettiva di lettura
* numero inferiore di hello di thread CPU nella macchina virtuale hello Hello, hello più grave impatto hello di compressione dei backup
* Hello meno destinazioni (directory di striping, dischi rigidi virtuali) toowrite hello backup, alta hello hello

numero hello tooincrease di destinata toowrite per, sono disponibili due opzioni che è possibile utilizzare, eventualmente in combinazione, in base alle esigenze:

* Volumi separati dedicati al backup
* Lo striping del volume di destinazione di backup hello su più dischi rigidi virtuali montati in ordine tooimprove hello IOPS velocità effettiva in tale volume con striping del disco
* Dispositivi dischi logici separati dedicati per:
  * Volumi (ovvero file) di backup di SAP MaxDB
  * Volumi (ovvero file) di dati di SAP MaxDB
  * Volumi (ovvero file) di log di SAP MaxDB

Lo striping di un volume su più dischi rigidi virtuali montati è stato illustrato in precedenza nel capitolo [Software RAID][dbms-guide-2.2] di questo documento.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Altro
Tutte le altri argomenti generali, ad esempio il set di disponibilità di Azure o SAP monitoring si applicano anche come descritto in hello primi tre capitoli di questo documento per le distribuzioni di macchine virtuali con database SAP MaxDB hello.
Altre impostazioni specifiche SAP MaxDB sono macchine virtuali tooAzure trasparente e sono descritte in diversi documenti riportati nella nota SAP [767598 ] e nelle note SAP:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Specifiche per SAP liveCache in Windows
### <a name="sap-livecache-version-support"></a>Supporto della versione di SAP liveCache
La versione minima di SAP liveCache supportata nelle macchine virtuali di Azure è **SAP LC/LCAPPS 10.0 SP 25**, incluse **liveCache 7.9.08.31** e **LCA-Build 25**, rilasciate per **EhP 2 for SAP SCM 7.0** e versioni successive.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Versioni di Microsoft Windows e tipi di VM di Azure supportati per SAP liveCache DBMS
versione di Microsoft Windows toofind hello è supportato per liveCache SAP in Azure, vedere:

* [Product Availability Matrix (PAM) SAP][sap-pam]
* Nota SAP [1928533]

Versione più recente di hello toouse di hello del sistema operativo Microsoft Windows, ovvero Microsoft Windows 2012 R2, è consigliabile.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Linee guida per la configurazione di SAP liveCache per le installazioni di SAP nelle VM di Azure
#### <a name="recommended-azure-vm-types"></a>Tipi di VM di Azure consigliati
SAP liveCache è un'applicazione che esegue i calcoli di grandi dimensioni, hello quantità e la velocità di RAM e CPU ha un forte impatto sulle prestazioni liveCache SAP.

Per i tipi di macchina virtuale di Azure hello supportati da SAP (nota SAP [1928533]), tutte le risorse di CPU virtuali allocate toohello dedicato alle risorse della CPU fisica dell'hypervisor hello vengono sottoposti a macchina virtuale. Non si verifica nessun provisioning eccessivo (e quindi nessuna competizione per le risorse della CPU).

Analogamente, per tutti i tipi di istanza VM di Azure supportati da SAP, memoria della macchina virtuale hello è stato eseguito il mapping di 100% memoria fisica di toohello – overprovisioning (overcommit), ad esempio, non viene utilizzata.

Da questa prospettiva è consigliabile toouse hello nuova serie D o macchina virtuale di Azure della serie DS (in combinazione con l'archiviazione di Azure Premium) tipo, in cui il 60% processori più veloci rispetto a hello serie. Per hello RAM e CPU carico massimo, è possibile utilizzare G-series e GS-series (in combinazione con l'archiviazione di Azure Premium) di macchine virtuali con processore Intel® Xeon® più recente di hello E5 v3 famiglia, che contengono due volte la memoria hello e quattro volte hello a tinta unita archiviazione dello stato unità (SSD Solid) di hello D / Serie DS.

#### <a name="storage-configuration"></a>Configurazione dell'archiviazione
Come liveCache SAP è basato sulla tecnologia MaxDB SAP, tutti hello di archiviazione di Azure le procedure consigliate indicate per SAP MaxDB nel capitolo [configurazione dell'archiviazione] [ dbms-guide-8.4.1] sono validi anche per liveCache SAP.

#### <a name="dedicated-azure-vm-for-livecache"></a>VM di Azure dedicata per liveCache
Come SAP liveCache usa intensamente la potenza di calcolo, per l'utilizzo produttivo è consigliabile toodeploy in una macchina virtuale dedicato Azure.

![VM di Azure dedicata per liveCache per un caso d'uso produttivo][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Backup e ripristino
Backup e ripristino, incluse le considerazioni sulle prestazioni, sono già stati descritti nei capitoli SAP MaxDB rilevanti hello [di Backup e ripristino] [ dbms-guide-8.4.2] e [considerazioni sulle prestazioni per il Backup e il ripristino][dbms-guide-8.4.3].

#### <a name="other"></a>Altre
Tutti gli altri argomenti generali sono già stati descritti in hello rilevanti SAP MaxDB [questo] [ dbms-guide-8.4.4] capitolo.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Specifiche per i Server di contenuti di SAP in Windows hello
Hello Server contenuto SAP è un contenuto toostore componente separato, basato su server, ad esempio documenti elettronici in formati diversi. Hello Server contenuto SAP è fornito dall'ambiente di sviluppo della tecnologia ed è toobe utilizzato tra le applicazioni per tutte le applicazioni SAP. Viene installato in un sistema distinto. Il contenuto tipico è training materiale e la documentazione di Warehouse Knowledge o disegni tecnici provenienti da mySAP hello del ciclo di sistema di gestione di documenti.

### <a name="sap-content-server-version-support"></a>Supporto della versione di SAP Content Server
SAP attualmente supporta:

* **SAP Content Server** con la versione **6.50 (e successive)**
* **SAP MaxDB versione 7.9**
* **Microsoft IIS (Internet Information Server) versione 8.0 (e successive)**

Si consiglia di versione più recente di toouse hello del Server contenuti SAP, che in fase di hello di scrittura di questo documento è **6.50 SP4**e la versione più recente di hello del **Microsoft IIS 8.5**.

Controllo delle versioni di hello supportata più recente del Server di contenuti di SAP e Microsoft IIS in hello [SAP prodotto disponibilità matrice (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Tipi di VM di Azure e di Microsoft Windows supportati per SAP Content Server
toofind versione supportata di Windows per Server di contenuti di SAP in Azure, vedere:

* [Product Availability Matrix (PAM) SAP][sap-pam]
* Nota SAP [1928533]

Si consiglia di versione più recente di hello toouse di Microsoft Windows, che in fase di hello di scrittura di questo documento è **Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Linee guida per la configurazione di SAP Content Server per le installazioni di SAP nelle VM di Azure
#### <a name="storage-configuration"></a>Configurazione dell'archiviazione
Se si configurano i file Server di contenuti di SAP toostore nel database SAP MaxDB hello, archiviazione di Azure tutte le procedura consigliate raccomandazione indicato per SAP MaxDB nel capitolo [configurazione dell'archiviazione] [ dbms-guide-8.4.1] sono anche valido per uno scenario Server di contenuti di SAP hello.

Se si configurano i file Server di contenuti di SAP toostore nel file system di hello, è consigliabile toouse un'unità logica dedicata. Usa spazi di archiviazione consente di dimensioni del disco logico tooalso aumento e la velocità effettiva IOPS, come descritto nel capitolo [RAID Software][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>Posizione di SAP Content Server
Server contenuto SAP è distribuito in hello toobe stessa regione di Azure e rete virtuale di Azure in cui è distribuito hello sistema SAP. Si è toodecide disponibile se si desidera che i componenti Server di contenuti di SAP toodeploy in una macchina virtuale di Azure dedicata o nel database hello stessa macchina virtuale in cui è in esecuzione hello sistema SAP.

![VM di Azure dedicata per SAP Content Server][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Posizione di SAP Cache Server
Hello SAP Cache Server è un componente aggiuntivo basato su server tooprovide accesso too(cached) documenti in locale. Hello SAP Cache Server memorizza nella cache di documenti hello di un Server di contenuti di SAP. Si tratta di toooptimize il traffico di rete se i documenti hanno toobe più di una volta recuperato da diverse posizioni. In generale Hello è che il Server di Cache SAP hello ha toobe toohello fisicamente Chiudi client che accede ai Server di Cache SAP hello.

Sono disponibili due opzioni:

1. **Il client è un sistema SAP back-end** se un sistema SAP back-end è configurato tooaccess Server contenuto SAP, tale sistema SAP è un client. Come sistema SAP sia Server di contenuti di SAP vengono distribuiti in hello stessa regione di Azure – in hello stesso Data Center di Azure – sono fisicamente Chiudi tooeach altri. Pertanto, non è toohave necessario un Server di Cache dedicato di SAP. Interfaccia utente di SAP (SAP GUI o un browser web) client accesso hello sistema SAP direttamente e hello SAP sistema recupera documenti da hello Content Server SAP.
2. **Il client è un browser web locale** hello Server contenuto SAP può essere configurato toobe accedere direttamente dal browser web hello. In questo caso, un web browser in esecuzione in locale è un client di hello Content Server SAP. Data Center locale e Data Center di Azure vengono inseriti in diverse ubicazioni fisiche (idealmente Chiudi tooeach altri). Il data center locale è connesso tooAzure tramite Azure VPN Site-to-Site o ExpressRoute. Anche se entrambe le opzioni offrono protezione tooAzure di connessione di rete VPN, connessione di rete da sito a sito non offre un contratto di servizio rete larghezza di banda e latenza tra Data Center locale hello e hello Data Center di Azure. toospeed backup toodocuments di accesso, è possibile eseguire una delle seguenti hello:
   1. Installare il Server di Cache SAP in locale, chiudere toohello on premise web browser (opzione [questo] [ dbms-guide-900-sap-cache-server-on-premises] figura)
   2. Configurare Azure ExpressRoute, che offre una connessione di rete dedicata a velocità elevata e a bassa latenza tra il data center locale e il data center di Azure.

![Opzione tooinstall SAP Cache Server locale][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Backup/Ripristino
Se si configurano toostore i file Server di contenuti di SAP di hello nel database SAP MaxDB hello, hello backup/ripristino procedure e considerazioni sulle prestazioni sono già stati descritti nei capitoli da SAP MaxDB [di Backup e ripristino] [ dbms-guide-8.4.2] e capitolo [considerazioni sulle prestazioni per il Backup e ripristino][dbms-guide-8.4.3].

Se si configurano toostore i file Server di contenuti di SAP di hello nel file system di hello, un'opzione è tooexecute backup/ripristino manuale della struttura di hello intero file in cui si trovano i documenti hello. TooSAP simile MaxDB backup/ripristino, è consigliabile toohave un volume dedicato a scopo di backup.

#### <a name="other"></a>Altre
Altre impostazioni specifiche del Server di contenuti di SAP sono macchine virtuali tooAzure trasparente e sono descritte in diversi documenti e note su SAP:

* <https://service.sap.com/contentserver>
* Nota SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Le specifiche tooIBM DB2 per LUW in Windows
Con Microsoft Azure, è possibile eseguire facilmente la migrazione dell'applicazione SAP esistente in esecuzione in IBM DB2 per Linux, UNIX e Windows (LUW) le macchine virtuali tooAzure. Con SAP in IBM DB2 per LUW, amministratori e sviluppatori possono ancora usare hello stessi strumenti di sviluppo e amministrazione disponibili in locale.
Informazioni generali sull'esecuzione di SAP Business Suite in IBM DB2 per LUW è reperibile hello SAP Community rete (SCN) in <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Per altre informazioni e aggiornamenti su SAP in DB2 per LUW in Azure, vedere la nota SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Supporto della versione di IBM DB2 per Linux, UNIX e Windows
SAP in IBM DB2 per LUW nei servizi Macchine virtuali di Microsoft Azure è supportato a partire da DB2 versione 10.5.

Per informazioni su prodotti SAP supportati e i tipi di macchine Virtuali di Azure, consultare tooSAP nota [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Linee guida per la configurazione di IBM DB2 per Linux, UNIX e Windows per le installazioni di SAP nelle VM di Azure
#### <a name="storage-configuration"></a>Configurazione dell'archiviazione
Tutti i file di database devono essere archiviati in file system di hello NTFS in base a dischi rigidi Virtuali. Questi dischi VHD sono montato toohello macchina virtuale di Azure e si basano nell'archiviazione BLOB di Azure pagina (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Qualsiasi tipo di unità di rete o condivisioni remote come hello seguenti servizi di file di Azure è **non** supportato per i file di database:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Se si usano dischi rigidi virtuali di Azure in archiviazione BLOB di Azure pagina base, hello istruzioni eseguite in questo documento nel capitolo [struttura di una distribuzione RDBMS] [ dbms-guide-2] si applicano anche toodeployments con hello IBM DB2 per LUW Database.

Come illustrato in precedenza in hello generale parte hello documento, esistono quote alla velocità effettiva IOPS per i dischi rigidi virtuali di Azure. le quote esatta Hello dipendono dal tipo di macchina virtuale hello utilizzato. Un elenco di tipi di macchine virtuali con le rispettive quote è disponibile [qui][virtual-machines-sizes]

Purché hello corrente quota IOPS per ogni disco è sufficiente, che è possibile toostore in che tutti hello i file di database un unico montati disco rigido virtuale di Azure.

Per ottenere prestazioni considerazioni anche fare riferimento toochapter "sicurezza e prestazioni considerazioni per Database"directory dati nelle guide di installazione di SAP.

In alternativa, è possibile utilizzare pool di archiviazione di Windows (solo disponibili in Windows Server 2012 e versioni successive) o lo striping di Windows per Windows 2008 R2, come descritto nel capitolo [RAID Software] [ dbms-guide-2.2] di questo documento toocreate una grande dispositivo logico su più dischi rigidi Virtuali montati.
Per i dischi hello contenente i percorsi di archiviazione DB2 hello per le directory sapdata e saptmp, è necessario specificare una dimensione di settore del disco fisico di 512 KB. Quando si utilizza il pool di archiviazione di Windows, è necessario creare hello pool di archiviazione manualmente tramite l'interfaccia della riga di comando utilizzando il parametro hello "-LogicalSectorSizeDefault". Per altre informazioni, vedere <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Backup/Ripristino
funzionalità di backup/ripristino Hello per IBM DB2 per LUW è supportato in hello stesso modo come in standard i sistemi operativi Windows Server e Hyper-V.

È necessario verificare di avere adottato una valida strategia di backup di database.

Come nelle distribuzioni bare metal, le prestazioni di backup/ripristino varia a seconda del numero di volumi può essere letti in parallelo e velocità effettiva quali hello di tali volumi potrebbe essere. Inoltre, hello CPU usata dalla compressione dei backup potrebbe svolgono un ruolo significativo in macchine virtuali con solo i thread di CPU too8. Si può quindi presumere quanto segue:

* Hello numero hello un minor numero di dischi rigidi virtuali toostore hello database i dispositivi di uso, hello hello minore velocità effettiva complessiva in lettura
* numero inferiore di hello di thread CPU nella macchina virtuale hello Hello, hello più grave impatto hello di compressione dei backup
* Hello meno destinazioni (directory di striping, dischi rigidi virtuali) toowrite hello backup, alta hello hello

numero di hello tooincrease di destinazioni toowrite a, due opzioni possono essere utilizzato/combinati in base alle esigenze:

* Lo striping del volume di destinazione di backup hello su più dischi rigidi virtuali montati della velocità effettiva di IOPS hello tooimprove ordine sul volume con striping
* Utilizzo di più di una destinazione directory toowrite hello backup per

#### <a name="high-availability-and-disaster-recovery"></a>Disponibilità elevata e ripristino di emergenza
Il server di cluster Microsoft non è supportato.

Il ripristino di emergenza a disponibilità DB2 è supportato. Se dispone di macchine virtuali hello di configurazione a disponibilità elevata hello utilizza la risoluzione dei nomi, il programma di installazione di hello in Azure non sarà diversa da qualsiasi programma di installazione viene eseguita in locale. Non è consigliabile toorely solo alla risoluzione IP.

Non usare la replica geografica di Azure Store. Per ulteriori informazioni, vedere toochapter [archiviazione di Microsoft Azure] [ dbms-guide-2.3] e capitolo [disponibilità elevata e ripristino di emergenza con macchine virtuali di Azure] [ dbms-guide-3].

#### <a name="other"></a>Altre
Tutti gli altri argomenti generali come set di disponibilità di Azure o SAP monitoring si applicano come descritto in hello primi tre capitoli di questo documento per le distribuzioni di macchine virtuali con IBM DB2 per LUW anche.

Fare riferimento anche toochapter [generali di SQL Server per SAP in Azure riepilogo][dbms-guide-5.8].
