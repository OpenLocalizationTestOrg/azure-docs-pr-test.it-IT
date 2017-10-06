---
title: Macchine virtuali aaaAzure pianificazione e implementazione di SAP NetWeaver | Documenti Microsoft
description: Guida alla pianificazione e all'implementazione di macchine virtuali di Azure per SAP NetWeaver
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>Guida alla pianificazione e all'implementazione di macchine virtuali di Azure per SAP NetWeaver
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
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
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

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

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
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
[sap-pam]:https://support.sap.com/pam
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
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
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
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
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
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure consente di risorse di calcolo e archiviazione tooacquire società in poco tempo, senza lunghi cicli di approvvigionamento. Macchine virtuali di Azure consentire alle aziende toodeploy applicazioni classiche, come le applicazioni in Azure basate su SAP NetWeaver ed estendere l'affidabilità e disponibilità senza la necessità di ulteriori risorse disponibili in locale. Servizi macchine virtuali di Azure supporta inoltre la connettività tra più sedi locali, macchine virtuali di Azure quali tooactively società consente di integrare i domini locali, nei cloud privati e i relativi Landscape del sistema SAP.
Questo white paper descrive i principi fondamentali di hello macchina virtuale di Microsoft Azure e fornisce una panoramica delle considerazioni sulla pianificazione e implementazione per le installazioni di SAP NetWeaver in Azure e di conseguenza devono essere hello documento tooread prima di iniziare distribuzioni effettive di SAP NetWeaver in Azure.
Hello carta integra hello documentazione di installazione di SAP e note su SAP, che rappresentano le risorse primarie hello per le distribuzioni del software SAP e le installazioni dato piattaforme.

## <a name="summary"></a>Riepilogo
Il cloud Computing è un termine ampiamente usato, che sta per essere importanza sempre maggiore di hello settore IT, dalle piccole imprese di società toolarge e implementazione.

Microsoft Azure è una piattaforma di servizi Cloud Microsoft, che offre un'ampia gamma di nuove possibilità hello. I clienti sono ora toorapidly in grado di effettuare il provisioning e la prestazione applicazioni come un servizio cloud hello, in modo che non siano tootechnical limitato o restrizioni budget. Invece di investire tempo e denaro nell'infrastruttura hardware, le organizzazioni possono dedicarsi applicazione hello, i processi di business e i vantaggi per clienti e utenti.

Grazie ai servizi inclusi in Macchine virtuali di Microsoft Azure, Microsoft offre una piattaforma di infrastruttura distribuita come servizio (IaaS) completa. Le applicazioni basate su SAP NetWeaver sono supportate in Macchine virtuali di Azure (IaaS). Questo white paper viene descritto come tooplan e SAP NetWeaver di implementare applicazioni basate su all'interno di Microsoft Azure come piattaforma di hello di scelta.

Hello stesso esaminati due aspetti principali:

* prima parte Hello descrive due modelli di distribuzione supportati per le applicazioni basate su SAP NetWeaver in Azure. Descrive anche la gestione generale di Azure, con particolare attenzione alle distribuzioni SAP.
* Hello seconda parte dettagli implementazione hello due diversi scenari descritti nella prima parte hello.

Per altre risorse, vedere il capitolo [Risorse][planning-guide-1.2] in questo documento.

### <a name="definitions-upfront"></a>Definizioni
In tutto il documento di hello, utilizziamo hello seguenti termini:

* IaaS (Infrastructure as a Service): infrastruttura distribuita come servizio
* PaaS (Platform as a Service): piattaforma distribuita come servizio
* SaaS (Software as a Service): software come un servizio
* ARM: Azure Resource Manager
* Componente SAP: singola applicazione SAP, ad esempio ECC, BW, Solution Manager o EP.  I componenti SAP possono essere basati su tecnologie ABAP o Java tradizionali o su un'applicazione non basata su NetWeaver, ad esempio Business Objects.
* Ambiente SAP: uno o più componenti SAP raggruppati logicamente tooperform una funzione di business, ad esempio Development, QAS, Training, ripristino di emergenza o di produzione.
* Landscape SAP: Si riferisce toohello intera asset SAP in un cliente landscape IT. Hello landscape SAP include tutti di produzione e ambienti non di produzione.
* Sistema SAP: combinazione hello del livello DBMS e applicazione di, ad esempio, un sistema di sviluppo ERP SAP, sistema di test BW SAP, sistema di produzione CRM SAP e così via... In distribuzioni di Azure, non è supportato toodivide questi due livelli tra sedi locali e Azure. Un sistema SAP deve quindi essere distribuito o in locale o in Azure. Tuttavia, è possibile distribuire i sistemi diversi di hello di un landscape SAP in Azure o in locale. Ad esempio, è possibile distribuire i sistemi hello CRM SAP sviluppo e test in Azure ma hello CRM SAP produzione sistema locale.
* Distribuzione solo cloud: una distribuzione in cui hello sottoscrizione di Azure non è connesso tramite un sito a sito o ExpressRoute connessione toohello on-premise infrastruttura di rete. Nella documentazione comune su Azure questi tipi di distribuzioni vengono definiti anche distribuzioni "solo cloud". Macchine virtuali distribuite con questo metodo si accede tramite internet hello e un indirizzo IP pubblico e/o un DNS pubblico nome assegnato toohello macchine virtuali in Azure. Per Microsoft Windows hello locale di Active Directory (AD) e DNS non viene esteso tooAzure in questi tipi di distribuzione. Pertanto le macchine virtuali hello non fanno parte di hello Active Directory locale. Queste considerazioni sono applicabili anche alle implementazioni Linux che usano, ad esempio, OpenLDAP + Kerberos.

> [!NOTE]
> La distribuzione solo cloud in questo documento viene definita come panorama applicativo SAP completo e viene eseguita esclusivamente in Azure senza estensione di Active Directory/OpenLDAP o risoluzione dei nomi da locale a cloud pubblico. Le configurazioni solo cloud non sono supportate per i sistemi SAP di produzione o configurazioni in cui STMS SAP o altre risorse locali devono toobe utilizzato tra i sistemi SAP ospitati in Azure e risorse che risiedono in locale.
>
>

* Cross-premise: Viene descritto uno scenario in cui le macchine virtuali sono distribuite tooan sottoscrizione di Azure con site-to-site, multi-sito o ExpressRoute connettività tra Data Center locale hello e Azure. Nella documentazione comune su Azure, questi tipi di distribuzioni vengono definiti anche scenari cross-premise. motivo Hello connessione hello è tooextend domini locali, Active Directory/OpenLDAP on-premise e DNS in locale in Azure. Hello locale orizzontale è estesa toohello asset Azure della sottoscrizione hello. Grazie a questa estensione, hello macchine virtuali può far parte del dominio locale hello. Gli utenti di dominio del dominio locale hello possono accedere ai server hello ed eseguire servizi su tali macchine virtuali (ad esempio servizi DBMS). La comunicazione e la risoluzione dei nomi tra VM distribuite in locale e VM distribuite in Azure sono consentite. Si tratta di uno scenario di hello è probabile che la maggior parte delle toobe asset SAP distribuiti in. Per ulteriori informazioni, vedere [questo][vpn-gateway-cross-premises-options] articolo e [questo][vpn-gateway-site-to-site-create].

> [!NOTE]
> Le distribuzioni cross-premise di sistemi SAP in cui le macchine virtuali di Azure che eseguono sistemi SAP sono membri di un dominio locale sono supportate per i sistemi SAP di produzione. Le configurazioni cross-premise sono supportate per la distribuzione parziale o completa di panorami applicativi SAP in Azure. Anche landscape SAP completo hello in esecuzione in Azure, è necessario che tali macchine virtuali da parte del dominio locale e annunci/OpenLDAP. Nelle versioni precedenti della documentazione di hello, abbiamo parlato scenari IT ibridi, in cui il termine hello "Ibrido" nella radice di fatto hello che vi sia una connettività cross-premise tra sedi locali e Azure. Inoltre, fatti hello che hello macchine virtuali in Azure fanno parte di hello in Active Directory locale / OpenLDAP.
>
>

Alcuni documenti Microsoft descrivono scenari cross-premise in modo leggermente diverso, in particolare per configurazioni DBMS a disponibilità elevata. Nel caso di hello di documenti correlati a SAP hello, scenario cross-premise hello solo riduce toohaving site-to-site o privato (ExpressRoute) per la connettività e hello fact che landscape SAP hello viene distribuito tra sedi locali e Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Risorse
Hello Guide aggiuntive seguenti sono disponibili per l'argomento hello distribuzioni SAP in Azure:

* [Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver (il presente documento)][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP NetWeaver][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP NetWeaver][dbms-guide]

> [!IMPORTANT]
> Utilizzato ovunque possibile toohello un collegamento che fa riferimento la Guida all'installazione SAP (riferimento InstGuide-01, vedere <http://service.sap.com/instguides>). Quando si tratta di prerequisiti toohello e processo di installazione, guide all'installazione di hello SAP NetWeaver deve essere sempre leggere con attenzione, perché in questo documento tratta solo specifiche attività per i sistemi SAP NetWeaver installati in una macchina virtuale di Microsoft Azure.
>
>

Hello note su SAP seguenti è correlati toohello argomento SAP in Azure:

| Numero della nota | Titolo |
| --- | --- |
| [1928533] |Applicazioni SAP in Azure: dimensioni e prodotti supportati |
| [2015553] |SAP in Microsoft Azure: prerequisiti per il supporto |
| [1999351] |Risoluzione dei problemi del monitoraggio avanzato di Azure per SAP |
| [2178632] |Metriche chiave del monitoraggio per SAP in Microsoft Azure |
| [1409604] |Virtualizzazione in Windows: monitoraggio avanzato |
| [2191498] |SAP in Linux con Azure: monitoraggio avanzato |
| [2243692] |Linux in una macchina virtuale di Microsoft Azure (IaaS): problemi delle licenze SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: note di installazione |
| [2002167] |Red Hat Enterprise Linux 7. x: installazione e aggiornamento |
| [2069760] |Installazione e aggiornamento di Oracle Linux 7.x SAP |
| [1597355] |Raccomandazione sullo spazio di scambio per Linux |

Leggere inoltre hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) che contiene tutte le note SAP per Linux.

Le limitazioni predefinite generali e le limitazioni massime delle sottoscrizioni di Azure sono disponibili in [questo articolo][azure-subscription-service-limits-subscription].

## <a name="possible-scenarios"></a>Scenari possibili
SAP viene spesso considerata come una delle applicazioni mission-critical di hello all'interno delle organizzazioni. architettura di Hello e le operazioni di queste applicazioni sono in genere molto complesso ed è importante assicurarsi che siano soddisfatti i requisiti di disponibilità e prestazioni.

È quindi necessario toothink con attenzione quali applicazioni possono essere eseguite in un ambiente cloud pubblico, indipendentemente dal provider di cloud hello scelto.

Ecco un elenco dei possibili tipi di sistema per la distribuzione di applicazioni basate su SAP NetWeaver in ambienti cloud pubblico:

1. Sistemi di produzione di medie dimensioni
2. Sistemi di sviluppo
3. Sistemi di test
4. Sistemi prototipo
5. Sistemi di apprendimento/dimostrativi

In ordine toosuccessfully distribuire i sistemi SAP in Azure IaaS o IaaS in generale, è importante toounderstand hello differenze significative hello offerte di tradizionali Outsourcer o di hosting e le offerte IaaS. Mentre hoster tradizionale hello o outsourcer adatta il carico di lavoro di infrastruttura (tipo di rete, archiviazione e server) toohello toohost desidera che un cliente, è invece responsabilità toochoose hello giusto carico di lavoro del cliente hello per le distribuzioni IaaS.

Come primo passaggio, i clienti devono hello tooverify seguenti elementi:

* Hello SAP supportati i tipi di macchine Virtuali di Azure
* prodotti/versioni di supportate Hello SAP in Azure
* Hello supportate le versioni del sistema operativo e DBMS per hello che rilascia specifico SAP in Azure
* La velocità effettiva di SAPS fornita da diversi SKU di Azure

Hello risposte toothese domande possono essere letti nella nota SAP [1928533].

Come secondo passaggio, limiti di larghezza di banda e risorse Azure necessario consumo di risorse tooactual toobe rispetto dei sistemi locali. Di conseguenza, i clienti necessità toobe familiarità con funzionalità diverse di hello del hello Azure supportati con SAP nell'area di hello del:

* Risorse di CPU e di memoria per diversi tipi di macchine virtuali
* Larghezza di banda IOPS per diversi tipi di macchine virtuali
* Funzionalità di rete dei diversi tipi di macchine virtuali

La maggior parte di quei dati si trova [qui (Linux)][virtual-machines-sizes-linux] e [qui (Windows)][virtual-machines-sizes-windows].

Tenere presente che hello limiti elencati nel collegamento hello precedente sono i limiti superiori. Questo non significa che i limiti di hello per le risorse di hello, ad esempio IOPS può essere forniti in tutte le circostanze. eccezioni di Hello sono tuttavia le risorse di CPU e memoria hello di un tipo di macchina virtuale selezionata. Per i tipi VM hello supportati da SAP, le risorse di CPU e memoria hello sono riservate e di conseguenza disponibili in qualsiasi punto nel tempo per l'utilizzo all'interno di hello macchina virtuale.

piattaforma Microsoft Azure Hello come altre piattaforme IaaS è multi-tenant. Le risorse di archiviazione, di rete e di altro tipo sono quindi condivise tra i tenant. Logica intelligente di limitazioni e quote è influenzando le prestazioni di hello di un altro tenant (vicino) in modo drastico tenant tooprevent usato uno. Anche se logica di Azure tenta tookeep varianze nella larghezza di banda riscontrata piattaforme di piccole dimensioni, ampiamente condivise tendono a toointroduce maggiori le varianze nella disponibilità di risorse/larghezza di banda di molti clienti sono utilizzati tooin le distribuzioni locali. Di conseguenza, è possibile riscontrare livelli diversi di larghezza di banda sulla rete o dei / o (volume hello nonché latenza) di archiviazione da toominute minuti. probabilità Hello che un sistema SAP in Azure registri varianze maggiori rispetto a un sistema locale deve toobe presi in considerazione.

L'ultimo passaggio consiste tooevaluate requisiti di disponibilità. Può verificarsi, tale hello sottostante l'infrastruttura di Azure deve tooget aggiornato e host di hello che eseguono le macchine virtuali toobe riavviato. In questi casi vengono arrestate e riavviate anche le macchine virtuali in esecuzione in questi host. Intervallo Hello di questi interventi di manutenzione viene eseguita durante l'orario non di base per una determinata area, ma è relativamente ampia potenziale finestra hello di poche ore durante il quale si verificherà un riavvio. Esistono varie tecnologie hello piattaforma Azure che può essere configurato toomitigate alcune o tutte hello impatto di tali aggiornamenti. Futuri miglioramenti della piattaforma Azure, DBMS, hello e applicazione SAP sono progettati impatto hello toominimize di questi riavvii.

In ordine toosuccessfully distribuire un sistema SAP in Azure, hello locale i sistemi SAP del sistema operativo, Database e applicazioni SAP devono essere visualizzati in hello Azure SAP può fornire una matrice di supporto, rientra hello hello di risorse dell'infrastruttura di Azure e che lavorare con hello che offre disponibilità contratti di servizio Microsoft Azure. Quando vengono identificati tali sistemi, è necessario toodecide in uno dei seguenti due scenari di distribuzione hello.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Solo cloud - distribuzioni di macchine virtuali in Azure senza dipendenze da hello locale rete cliente
![Singola macchina virtuale con scenario dimostrativo o di formazione SAP distribuito in Azure][planning-guide-figure-100]

Questo scenario è tipico di formazione o sistemi dimostrativi, in cui sono installati tutti i componenti di hello di SAP e non SAP software all'interno di una singola macchina virtuale. I sistemi SAP di produzione non sono supportati in questo scenario di distribuzione. In generale, questo scenario soddisfa hello seguenti requisiti:

* macchine virtuali di Hello sono accessibili attraverso la rete pubblica hello. Connettività di rete diretto per applicazioni di hello in esecuzione all'interno di hello macchine virtuali toohello locale della rete di una società di hello proprietaria contenuto demo o di formazione di hello o cliente di hello non necessario.
* In caso di più macchine virtuali che rappresenta lo scenario demo o formazione di hello, risoluzione dei nomi e di comunicazioni di rete deve toowork tra le macchine virtuali hello. Ma le comunicazioni tra il set di hello di macchine virtuali devono toobe isolato in modo che più set di macchine virtuali possono essere distribuiti side-by-side senza interferenze.  
* Connettività Internet è necessaria per account di accesso tooremote hello utente finale in toohello che macchine virtuali ospitate in Azure. A seconda del sistema operativo guest, hello viene usato servizi Terminal/RDS o VNC/ssh tooaccess hello VM tooeither completare le attività di formazione hello o eseguire demo di hello. Porte di SAP, ad esempio 3200, 3300 & 3600 può anche essere esposti istanza dell'applicazione SAP hello è possibile accedere da qualsiasi desktop connesso a Internet.
* i sistemi SAP di Hello (e VM(s)) rappresentano uno scenario autonomo in Azure, che solo richiede la connettività internet pubblica per l'accesso dell'utente finale e non richiede un tooother connessione macchine virtuali in Azure.
* Installazione ed eseguiti direttamente sulle hello VM SAPGUI e un browser.
* È necessario un ripristino rapido dello stato originale di toohello macchina virtuale e nuovo la distribuzione di tale stato originale.
* Nel caso di hello di scenari di formazione e dimostrazione, che vengono realizzati in più macchine virtuali, un server Active Directory service OpenLDAP e/o DNS è richiesto per ogni set di macchine virtuali.

![Gruppo di VM che rappresenta un scenario dimostrativo o di formazione in un servizio cloud di Azure][planning-guide-figure-200]

È importante tookeep presente che hello nelle macchine virtuali in ogni hello imposta toobe necessità distribuito in parallelo, in cui i nomi di macchina virtuale hello in ognuno dei set di hello sono hello stesso.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Cross-premise - distribuzione di una o più macchine virtuali SAP in Azure con il requisito di hello di siano pienamente integrate nella rete locale hello
![VPN con connettività da sito a sito (cross-premise)][planning-guide-figure-300]

Questo scenario è uno scenario cross-premise con molti modelli di distribuzione possibili. Può essere semplicemente come descritto per l'esecuzione di alcune parti di hello SAP landscape locale e altre parti di hello landscape SAP in Azure. Tutti gli aspetti delle tabelle dei fatti hello che parte dei componenti SAP hello sono in esecuzione in Azure dovrebbero essere trasparenti per gli utenti finali. Di conseguenza hello SAP trasporto correzione sistema (STMS), comunicazione RFC, stampa, sicurezza (come SSO) e così via. funziona perfettamente per i sistemi SAP di hello in esecuzione in Azure. Ma scenario cross-premise hello viene inoltre descritto uno scenario in cui landscape SAP completo hello in esecuzione in Azure con il dominio del cliente hello e DNS estesa in Azure.

> [!NOTE]
> Si tratta di scenario di distribuzione hello è supportato per l'esecuzione di sistemi SAP di produzione.
>
>

Lettura [questo articolo] [ vpn-gateway-create-site-to-site-rm-powershell] per ulteriori informazioni su come tooconnect tooMicrosoft Azure di rete locale

> [!IMPORTANT]
> Quando per quanto riguarda gli scenari di cross-premise tra Azure e locali distribuzioni dei clienti, si sta esaminando la granularità hello dell'insieme dei sistemi SAP. Ecco gli scenari *non supportati* per gli scenari cross-premise:
>
> * Esecuzione di livelli diversi di applicazioni SAP in diversi metodi di distribuzione, In esecuzione, ad esempio hello DBMS livello locale, ma a livello dell'applicazione hello SAP in macchine virtuali distribuite come macchine virtuali di Azure e viceversa.
> * Alcuni componenti di un livello SAP in Azure e altri in locale, Ad esempio la suddivisione di istanze di livello dell'applicazione SAP hello tra sedi locali e macchine virtuali di Azure.
> * La distribuzione di macchine virtuali che eseguono istanze SAP di un sistema in più aree di Azure non è supportata.
>
> motivo di Hello di queste restrizioni è il requisito di hello per una rete ad alte prestazioni di latenza molto bassa all'interno di un sistema SAP, soprattutto tra le istanze dell'applicazione hello e il livello DBMS hello di un sistema SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Sistemi operativi e versioni di database supportati
* Il software server Microsoft supportato per i servizi Macchine virtuali di Azure è elencato in questo articolo: <http://support.microsoft.com/kb/2721672>.
* Le versioni supportate del sistema operativo e le versioni dei sistemi database supportate nei servizi di macchine virtuali di Azure insieme al software SAP sono indicate nella nota SAP [1928533].
* Le applicazioni e le versioni SAP supportate nei servizi di macchine virtuali di Azure sono indicate nella nota SAP [1928533].
* Solo immagini a 64 Bit sono toorun supportati come Guest di macchine virtuali in Azure per gli scenari SAP. Sono quindi supportati solo database e applicazioni SAP a 64 bit.

## <a name="microsoft-azure-virtual-machine-services"></a>Servizi Macchine virtuali di Microsoft Azure
piattaforma Microsoft Azure Hello è un cloud su scala internet piattaforma di servizi ospitati e gestiti in Microsoft data center. piattaforma di Hello include servizi macchine virtuali di hello Microsoft Azure (infrastruttura come servizio o IaaS) e un set di funzionalità di piattaforma come una funzionalità del servizio (PaaS).

Hello piattaforma Azure riduce la necessità di hello di iniziali in tecnologie e infrastrutture degli acquisti. Semplifica la manutenzione e gestione di applicazioni fornendo toohost di calcolo e archiviazione su richiesta, scalare e gestire applicazioni web e applicazioni connesse. Gestione dell'infrastruttura è automatizzata con una piattaforma progettata per la disponibilità elevata e scalabilità toomatch esigenze per l'utilizzo con l'opzione hello di un modello di determinazione dei prezzi prepagato dinamica.

![Posizionamento di Servizi Macchine virtuali di Microsoft Azure][planning-guide-figure-400]

Con servizi di macchine virtuali di Azure, Microsoft consente toodeploy server personalizzato immagini tooAzure come istanze di IaaS (vedere la figura 4). Hello macchine virtuali in Azure si basano sulle unità disco rigido virtuale (VHD) Hyper-V e sono in grado di toorun diversi sistemi operativi come sistema operativo Guest.

Dal punto di vista operativo, hello che servizio macchina virtuale di Azure offre simile si verifica come macchine virtuali distribuite in locale. Tuttavia, dispone di vantaggio significativo hello che non è necessario tooprocure, amministrare e gestire l'infrastruttura di hello. Gli sviluppatori e gli amministratori hanno controllo completo dell'immagine del sistema operativo hello all'interno di queste macchine virtuali. Gli amministratori possono accedere in modalità remota in toothose macchine virtuali tooperform manutenzione e risoluzione dei problemi di attività, nonché le attività di distribuzione software. In considerazione toodeployment, uniche restrizioni hello sono dimensioni hello e le funzionalità di macchine virtuali di Azure. È possibile che la configurazione non sia dettagliata quanto la configurazione locale. È possibile scegliere tipi di VM basati su una combinazione degli elementi seguenti:

* Numero di vCPU
* Memoria
* Numero di dischi rigidi virtuali che è possibile collegare
* Larghezza di banda di rete e di archiviazione

dimensioni Hello e le limitazioni di varie dimensioni diverse macchine virtuali offerte sono consultabili in una tabella in [(Linux) in questo articolo] [ virtual-machines-sizes-linux] e [(Windows) in questo articolo] [ virtual-machines-sizes-windows].

Come si può notare, sono disponibili diverse famiglie o serie di macchine virtuali. È possibile distinguere hello famiglie di macchine virtuali seguenti:

* Tipi di VM A0-A7: non tutti questi tipi sono certificati per SAP. Si tratta della prima serie di VM in cui è stata introdotta la soluzione IaaS per Azure.
* Tipi di VM A8-A11: istanze HPC (High-Performance Computing). In esecuzione in host di calcolo diversi, con prestazioni migliori rispetto alle altre VM della serie A.
* Tipi di VM serie D/Dv2: prestazioni migliori rispetto ad A0-A7. Non tutti i tipi di VM hello sono certificati con SAP.
* Tipi di macchine Virtuali di dominio Active Directory/DSv2-Series: tooD/Dv2-series simili, ma che sono in grado di tooconnect tooAzure archiviazione Premium (vedere il capitolo [archiviazione Premium di Azure] [ planning-guide-3.3.2] di questo documento). Anche in questo caso, non tutti i tipi di VM sono certificati per SAP.
* Tipi di VM di serie G: tipi di macchine virtuali con memoria elevata.
* Tipi di macchine Virtuali GS-Series: come serie G ma inclusi hello opzione toouse archiviazione Premium di Azure (vedere il capitolo [archiviazione Premium di Azure] [ planning-guide-3.3.2] di questo documento). Quando si utilizzano le macchine virtuali GS-Series come server di database, è obbligatorio toouse archiviazione Premium per file di registro e dati di database

È possibile hello stesse configurazioni di CPU e memoria in diverse serie di macchine Virtuali. Tuttavia, quando si cercano le prestazioni di velocità effettiva di hello di queste macchine virtuali da una serie diversa di hello che potrebbero essere diverse in modo significativo. Nonostante entrambe abbiano hello stessa configurazione di memoria e CPU. Motivo è che hello host server hardware sottostante all'introduzione di hello di diversi tipi di macchine Virtuali hello ha caratteristiche diverse velocità effettiva.  In genere differenza hello illustrato nelle prestazioni di velocità effettiva viene riflessa anche nella prezzo hello di hello diverse macchine virtuali.

Non tutte le serie diverse di macchina virtuale potrebbero essere disponibile in ognuno di essi di hello aree di Azure (per le aree di Azure vedere il capitolo successivo). Occorre anche notare che non tutte le VM o le serie di VM sono certificate per SAP.

> [!IMPORTANT]
> Per l'utilizzo di hello delle applicazioni basate su SAP NetWeaver, solo i subset di hello di configurazioni e i tipi di macchine Virtuali riportato nella nota SAP [1928533] sono supportati.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Aree di Azure
Microsoft consente toodeploy macchine virtuali in Azure aree' denominati'. Un'area di Azure può essere costituita da uno o più data center che si trovano in posizioni molto vicine. Per la maggior parte delle hello geopolitiche aree in HelloWorld Microsoft dispone di almeno due aree di Azure. ad esempio, in Europa sono disponibili le aree di Azure "Europa settentrionale" ed "Europa occidentale". Queste due aree di Azure in un'area di natura geopolitica sono separati da distanza sufficientemente elevato in modo che non interessano entrambe le aree di Azure in hello calamità naturali o tecniche stessa regione di natura geopolitica. Poiché Microsoft è costantemente nello sviluppo nuove aree di Azure in diverse aree di natura geopolitiche a livello globale, il numero di hello di queste aree aumentano in modo costante e a partire da dicembre 2015 raggiunto il numero di hello di 20 aree di Azure con aree aggiuntive già annunciate. È un cliente può distribuire i sistemi SAP in tutte queste aree, tra cui hello due aree di Azure in Cina. Per informazioni aggiornate sulle aree di Azure, vedere il sito Web <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Hello concetto di macchina virtuale di Microsoft Azure
Microsoft Azure offre un'infrastruttura come un toohost di soluzioni di servizio (IaaS) delle macchine virtuali con funzionalità simili come una soluzione di virtualizzazione locale. Si è in grado di toocreate macchine virtuali da all'interno di hello portale di Azure PowerShell o CLI, che offrono inoltre funzionalità di gestione e distribuzione.

Gestione risorse di Azure consente tooprovision delle applicazioni utilizzando un modello dichiarativo. In un unico modello, è possibile distribuire più servizi con le relative dipendenze. Utilizzare hello stesso modello toorepeatedly distribuire l'applicazione durante ogni fase del ciclo di vita dell'applicazione hello.

Altre informazioni sull'uso dei modelli di Resource Manager sono disponibili qui:

* [Distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello CLI di Azure] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Gestire macchine virtuali con Azure Resource Manager e PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

Un'altra funzionalità interessante è immagini toocreate possibilità di hello dalle macchine virtuali, che consente di tooprepare determinati archivi da cui si sta tooquickly in grado di distribuiscono le istanze di macchina virtuale, che soddisfano i requisiti.

Altre informazioni sulla creazione di immagini da Macchine virtuali sono disponibili in [questo articolo (Linux)][virtual-machines-linux-capture-image-resource-manager] e in [questo articolo (Windows)][virtual-machines-windows-capture-image-resource-manager].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domini di errore
Domini di errore rappresentano un'unità fisica di errore, strettamente correlati toohello infrastruttura fisica contenuta nei data center, mentre un pannello fisico o un rack può essere considerato un dominio di errore, non esiste alcun mapping diretto uno a uno tra due hello.

Quando si distribuiscono più macchine virtuali come parte di un sistema SAP in servizi macchine virtuali di Microsoft Azure, è possibile influenzare hello toodeploy di Controller di infrastruttura di Azure dell'applicazione in diversi domini di errore, così da soddisfare i requisiti di hello di hello Contratto di servizio di Microsoft Azure. Hello, tuttavia, la distribuzione di domini di errore su un'unità di scala di Azure (raccolta di centinaia di nodi di calcolo o nodi di archiviazione e rete) o assegnazione hello di macchine virtuali tooa specifico di dominio di errore è un elemento su cui non è indirizzare il controllo. In ordine toodirect hello infrastruttura di Azure controller toodeploy un set di macchine virtuali tra diversi domini di errore, è necessario tooassign un toohello Set di disponibilità di Azure le macchine virtuali in fase di distribuzione. Per altre informazioni sui set di disponibilità di Azure, vedere il capitolo [Set di disponibilità di Azure][planning-guide-3.2.3] in questo documento.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Domini di aggiornamento
Domini di aggiornamento rappresentano un'unità logica che guida la modalità di aggiornamento di una macchina virtuale all'interno di un sistema SAP, costituito da istanze SAP in esecuzione in più macchine virtuali, toodetermine. Quando si verifica un aggiornamento, Microsoft Azure passa attraverso il processo di hello di Aggiorna questi domini uno alla volta. Suddividendo le macchine virtuali in diversi domini di aggiornamento durante la fase di distribuzione, è possibile proteggere parzialmente il sistema SAP da potenziali tempi di inattività. In ordine tooforce toodeploy Azure hello macchine virtuali di un sistema SAP suddivise tra diversi domini di aggiornamento, è necessario un attributo specifico tooset al momento della distribuzione di ogni macchina virtuale. Domini tooFault analoghi, un'unità di scala di Azure è diviso in più domini di aggiornamento. In ordine toodirect hello infrastruttura di Azure controller toodeploy un set di macchine virtuali tra diversi domini di aggiornamento, è necessario tooassign un toohello Set di disponibilità di Azure le macchine virtuali in fase di distribuzione. Per altre informazioni sui set di disponibilità di Azure, vedere il capitolo [Set di disponibilità di Azure][planning-guide-3.2.3] più avanti.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Set di disponibilità di Azure
Macchine virtuali di Azure all'interno di un Set di disponibilità vengono distribuite dal Controller di infrastruttura di Azure hello in diversi domini di errore e l'aggiornamento. scopo di Hello della distribuzione hello in diversi domini di errore e l'aggiornamento è tooprevent che tutte le macchine virtuali di un sistema SAP venga arrestate in caso di hello di manutenzione dell'infrastruttura o un errore all'interno di un dominio di errore. Per impostazione predefinita, le VM non fanno parte di un set di disponibilità. la partecipazione di Hello di una macchina virtuale in un Set di disponibilità viene definita in fase di distribuzione o in un secondo momento da una riconfigurazione e la ridistribuzione di una macchina virtuale.

concetto di hello toounderstand di set di disponibilità di Azure e hello modo correlazione con tooFault e domini di aggiornamento, leggere [in questo articolo][virtual-machines-manage-availability]

set di disponibilità toodefine per ARM tramite un modello json vedere [hello specifiche api rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) e cercare "disponibilità".

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Archiviazione: Archiviazione di Microsoft Azure e dischi dati
Le macchine virtuali di Microsoft Azure utilizzano diversi tipi di archiviazione. Quando si implementa SAP in servizi macchine virtuali di Azure, è importante toounderstand differenze di hello tra questi due tipi principali di archiviazione:

* Archiviazione volatile, non permanente.
* Archiviazione permanente.

archiviazione non permanente Hello è collegato direttamente toohello macchine virtuali in esecuzione e risiede nei nodi di calcolo hello, ossia hello istanza locale (archiviazione temporanea). dimensioni Hello dipendono dalle dimensioni hello di macchina virtuale scelta all'avvio di distribuzione hello hello. Questo tipo di archiviazione è volatile e pertanto disco hello viene inizializzato al riavvio di un'istanza di macchina virtuale. File di paging hello per sistema operativo hello in genere, si trova su questo disco temporaneo.

- - -
> ![Windows][Logo_Windows] Windows
>
> Nelle macchine virtuali di Windows hello temp è montata come unità D:\ in una macchina virtuale distribuita.
>
> ![Linux][Logo_Linux] Linux
>
> Nelle macchine virtuali Linux viene montata come /mnt/resource o /mnt. Per informazioni dettagliate, vedere:
>
> * [Come tooAttach tooa un disco dati macchina virtuale Linux][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux#temporary-disk>
>
>

- - -
unità effettiva Hello è volatile perché viene archiviata nel server host di hello stesso. Se hello VM spostata durante una ridistribuzione (ad esempio scadenza toomaintenance sull'host di hello o arresto e riavvio) contenuto hello dell'unità hello viene perso. Pertanto, non è un'opzione toostore tutti i dati importanti su questa unità. tipo Hello di supporto utilizzato per questo tipo di archiviazione differisce tra serie diverse di VM con caratteristiche di prestazioni molto diversi che, a partire da giugno 2015, questo aspetto:

* A5-A7: prestazioni estremamente limitate. Consigliato solo per i file di paging.
* A8-A11: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva >1 GB/sec.
* Serie D: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva >1 GB/sec.
* Serie DS: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva >1 GB/sec.
* Serie G: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva >1 GB/sec.
* Serie GS: caratteristiche di prestazioni molto valide con circa diecimila IOPS e velocità effettiva >1 GB/sec.

Istruzioni precedenti si applicano toohello i tipi di macchine Virtuali che sono certificati con SAP. Hello serie di macchine Virtuali con eccellente IOPS e la velocità effettiva idonei per l'utilizzo per alcune funzionalità di DBMS. Per ulteriori informazioni, vedere hello [Guida alla distribuzione di DBMS][dbms-guide].

Archiviazione di Microsoft Azure fornisce persistente hello e archiviazione tipici livelli di protezione e ridondanza disponibili nell'archiviazione SAN. Dischi basati su archiviazione di Azure sono di tipo disco rigido virtuale (VHD) presente in servizi di archiviazione di Azure hello. Hello disco del sistema operativo locale (c: di Windows\, Linux/sviluppo/sda1) è archiviato in archiviazione di Azure, hello e volumi e dischi aggiuntivi montato toohello VM ottenere archiviate, troppo.

È possibile tooupload un disco rigido virtuale esistente da on-premise o crearne di vuoti all'interno di Azure e collegare tali macchine virtuali toodeployed.

Dopo la creazione o il caricamento di un disco rigido virtuale nell'archiviazione di Azure, è possibile toomount e collegare tali tooan macchina virtuale e toocopy esistente VHD (non montati) esistenti.

Poiché questi dischi rigidi virtuali sono permanenti, i dati e le modifiche apportate al loro interno rimangono al sicuro dopo il riavvio e la ricreazione di un'istanza di macchina virtuale. Anche se viene eliminata un'istanza, questi dischi rigidi virtuali rimangono inalterati e possono essere ridistribuiti oppure in caso di dischi non del sistema operativo possono essere macchine virtuali montati tooother.

All'interno di hello è possibile configurare una rete di livelli diversi di ridondanza di archiviazione di Azure:

* Livello minimo che può essere selezionato è 'ridondanza locale', che è equivalente toothree-replica dei dati hello hello nello stesso data center di un'area di Azure (vedere il capitolo [aree di Azure][planning-guide-3.1]).
* Archiviazione di ridondanza di zona, quali immagini hello tre pagine su data center diversi all'interno di hello stessa regione di Azure.
* Livello di ridondanza predefinito è la ridondanza geografica, che consente di replicare in modo asincrono il contenuto di hello in un altro tre immagini di dati hello in un'altra area di Azure, che è ospitato in hello stessa regione di natura geopolitica.

Vedere anche la tabella hello all'inizio di questo articolo relativa hello ridondanza diverse opzioni: <https://azure.microsoft.com/pricing/details/storage/>

Altre informazioni su Archiviazione di Azure sono disponibili qui:

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Archiviazione Standard di Azure
Standard di archiviazione Azure è il tipo di hello spazio di archiviazione disponibile al momento del rilascio IaaS di Azure. Prevedeva l'applicazione di quote di IOPS per ogni disco. Latenza che si è verificata non hello stessa classe di dispositivi SAN/NAS per i sistemi SAP di fascia alta in genere distribuiti ospitato in locale. Tuttavia, hello archiviazione di Azure Standard dimostrato sufficiente per molte centinaia sistemi SAP nel frattempo distribuiti in Azure.

Dischi in cui sono archiviati in account di archiviazione di Azure Standard vengono addebitati in base a hello dati effettivi archiviati, volume hello di transazioni di archiviazione, trasferimenti di dati in uscita e opzione di ridondanza scelto. Numero di dischi può essere creati in hello massimo 1 TB di dimensione, ma, purché tali rimanere vuote non è previsto alcun addebito. Se si compila quindi un disco rigido virtuale con 100GB, viene addebitato per archiviare 100GB e non per hello dimensioni nominali hello creato con disco rigido virtuale.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Archiviazione Premium di Azure
Nel mese di aprile 2015 Microsoft ha introdotto l'Archiviazione Premium di Azure, Archiviazione Premium introdotto con tooprovide obiettivo hello:

* Migliore latenza di I/O.
* Migliore velocità effettiva.
* Minore variabilità della latenza di I/O.

A tale scopo, numero di modifiche sono state introdotte di quali hello due principali sono:

* Utilizzo di dischi SSD in nodi di archiviazione di Azure hello
* Una nuova cache di lettura supportato da hello SSD locale di un nodo di calcolo di Azure

Nel servizio di archiviazione tooStandard opposto in cui le funzionalità non è stata modificata dipende dalle dimensioni hello del disco hello (o VHD), archiviazione Premium attualmente dispone di tre categorie di un disco diverso, che vengono visualizzate in questo articolo: <https://azure.microsoft.com/ piano tariffario/dettagli / / non gestiti non-i dischi di archiviazione />

Vedrai che IOPS o disco e velocità effettiva/disco dipendono dalla categoria di dimensione hello di dischi hello

Base di costo nel caso di hello di archiviazione Premium non è il volume di dati effettivi hello archiviato in tali dischi, ma la categoria di dimensione hello di questo tipo un disco, indipendentemente dalla quantità di hello di hello i dati archiviati all'interno del disco hello.

È inoltre possibile creare dischi nell'archiviazione Premium che non esegue il mapping direttamente in categorie di dimensioni hello illustrate. Può trattarsi di case hello, soprattutto quando la copia dei dischi da archiviazione Standard in archiviazione Premium. In tali casi viene eseguita mapping toohello successivo più grande Premium opzione di archiviazione su disco.

Tenere presente che solo determinate serie di macchine Virtuali possono trarre vantaggio dall'archiviazione di Azure Premium hello. A partire da dicembre 2015, si tratta di hello e GS-serie DS. Hello serie DS è fondamentalmente hello stesso come serie D con eccezione hello che serie DS è hello possibilità toomount archiviazione Premium basati su macchine virtuali inoltre toodisks che sono ospitati in archiviazione di Azure Standard. Stessa operazione è valida per serie tooGS serie G confrontata.

Se si sta estraendo parte hello di macchine virtuali serie DS hello in [(Linux) in questo articolo] [ virtual-machines-sizes-linux] e [(Windows) in questo articolo][virtual-machines-sizes-windows], ci si accorge che sono presenti dati volume limitazioni tooPremium dischi di archiviazione in granularità hello di hello livello macchina virtuale. Diversa serie DS o GS-series VM sono anche diverse limitazioni relativamente toohello numero di dischi dati che può essere montato. Questi limiti sono documentati nell'articolo hello indicato in precedenza anche. Ma in pratica significa che se è, ad esempio, montare 32 x P30 dischi tooa singola macchina virtuale DS14 è possibile non ottenere 32 x velocità effettiva massima hello di un disco P30. Hello invece la velocità effettiva massima nel livello di macchina virtuale, come illustrato nella velocità effettiva dei dati hello articolo limiti.

Altre informazioni sull'archiviazione Premium sono disponibili qui: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>Managed Disks
I Managed Disks sono un nuovo tipo di risorsa in Azure Resource Manager, utilizzabile al posto dei dischi rigidi virtuali archiviati negli account di archiviazione di Azure. Dischi gestiti allineano automaticamente con il Set di disponibilità della macchina virtuale hello che sono collegati tooand pertanto aumento hello disponibilità delle macchine virtuali e dei servizi di hello che sono in esecuzione nella macchina virtuale hello hello. Per altre informazioni, vedere hello [articolo introduttivo](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

È consigliabile utilizzare tooyou disco gestito, perché semplificano hello distribuzione e gestione delle macchine virtuali.
SAP attualmente supporta solo Managed Disks Premium. Per altre informazioni, vedere la nota SAP [1928533].

#### <a name="azure-storage-accounts"></a>Account di archiviazione di Azure
Quando si distribuiscono servizi o macchine virtuali in Azure, la distribuzione di dischi rigidi virtuali e immagini di VM può essere organizzata in unità definite account di archiviazione di Azure. Quando si pianifica una distribuzione di Azure, è necessario toocarefully prendere in considerazione hello restrizioni di Azure. Sul lato "uno" hello, è un numero limitato di account di archiviazione per ogni sottoscrizione di Azure. Anche se ogni Account di archiviazione di Azure può contenere un numero elevato di file di disco rigido virtuale, è previsto un limite fisso sul hello totale di IOPS per Account di archiviazione. Quando si distribuiscono centinaia di macchine virtuali SAP con sistemi DBMS che creano chiamate dei / o significative, è consigliabile toodistribute elevata le macchine virtuali DBMS IOPS tra più account di archiviazione di Azure. Prestare attenzione non tooexceed hello limite corrente di account di archiviazione di Azure per ogni sottoscrizione. Perché l'archiviazione è una parte essenziale della distribuzione di database hello per un sistema SAP, questo concetto viene discusso in dettaglio in hello già fatto riferimento [Guida alla distribuzione di DBMS][dbms-guide].

Altre informazioni sugli account di archiviazione di Azure sono disponibili in [questo articolo][storage-scalability-targets]. Leggendo questo articolo, si rende conto che non esistono differenze tra account di archiviazione di Azure Standard e account di archiviazione Premium limitazioni hello. Differenze principali sono volume hello di dati che possono essere archiviati all'interno di un Account di archiviazione. Nel servizio di archiviazione Standard volume hello è una grandezza maggiore con archiviazione Premium. In hello è limitato gravi altro lato, Account di archiviazione Standard hello IOPS (vedere la colonna 'Frequenza di richiesta totale'), mentre questa limitazione non dispone di Account di archiviazione di Azure Premium hello. Quando si parla di distribuzioni hello dei sistemi SAP, in particolare hello DBMS i server verranno illustrati i dettagli e i risultati di queste differenze.

All'interno di un Account di archiviazione sono contenitori diversi hello possibilità toocreate scopo hello di organizzare e classificare i diversi dischi rigidi virtuali. Questi contenitori vengono in genere usati ad esempio per separare dischi rigidi virtuali di diverse macchine virtuali. L'uso di un solo contenitore o di più contenitori in un singolo account di archiviazione di Azure non comporta alcuna implicazione a livello di prestazioni.

In Azure un nome del disco rigido virtuale seguente hello seguente connessione di denominazione che richiede un nome univoco per hello VHD in Azure tooprovide:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Come stringa hello menzionate sopra toouniquely deve identificare hello disco rigido virtuale che viene archiviato nell'archiviazione di Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Rete di Microsoft Azure
Microsoft Azure offre un'infrastruttura di rete, che consente il mapping di hello di tutti gli scenari, che si desidera toorealize con il software SAP. funzionalità di Hello sono:

* Accesso da hello esterno, direttamente toohello macchine virtuali tramite servizi Terminal di Windows oppure ssh/VNC
* Accesso tooservices e specifiche porte usate dalle applicazioni all'interno di hello macchine virtuali
* Comunicazioni interne e risoluzione dei nomi tra un gruppo di macchine virtuali distribuite come macchine virtuali di Azure
* Connettività cross-premise tra la rete locale del cliente e hello rete di Azure
* Connettività tra aree o data center di Azure tra i siti di Azure

Altre informazioni sono disponibili qui: <https://azure.microsoft.com/documentation/services/virtual-network/>

Esistono molti nome tooconfigure diverse possibilità e la risoluzione IP in Azure. In questo documento, gli scenari solo Cloud si basano su predefinito hello con DNS di Azure (in contrasto toodefining un servizio DNS personalizzato). È anche disponibile un nuovo servizio DNS di Azure, che può essere usato invece di configurare un server DNS personalizzato. Altre informazioni sono disponibili in [questo articolo][virtual-networks-manage-dns-in-vnet] e in [questa pagina](https://azure.microsoft.com/services/dns/).

Per gli scenari di cross-premise, siamo affidati fatto hello che hello locale OpenLDAP/AD/DNS è stato esteso tramite VPN o connessione privata tooAzure. Per determinati scenari illustrati di seguito, potrebbe essere necessario toohave una replica di Active Directory/OpenLDAP installata in Azure.

La rete e la risoluzione dei nomi è una parte essenziale della distribuzione di database hello per un sistema SAP, questo concetto viene discusso in dettaglio in hello [Guida alla distribuzione di DBMS][dbms-guide].

##### <a name="azure-virtual-networks"></a>Reti virtuali di Azure
Tramite la compilazione di una rete virtuale di Azure, è possibile definire l'intervallo di indirizzi hello di hello gli indirizzi IP privati allocati dalla funzionalità DHCP di Azure. In scenari di cross-premise, intervallo di indirizzi IP hello definito viene comunque allocato utilizzando DHCP da Azure. Tuttavia, la risoluzione dei nomi di dominio viene eseguita in locale (presupponendo che le macchine virtuali hello fanno parte di un dominio locale) e pertanto può risolvere gli indirizzi oltre diversi servizi Cloud di Azure.

Ogni macchina virtuale in Azure esigenze toobe connessa tooa rete virtuale.

Per informazioni dettagliate, vedere [questo articolo][resource-groups-networking] e [questa pagina](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd TODO Impossibile trovare un articolo che include l'argomento OpenLDAP hello + ARM;)
[comment]: <> (MSSedusch &lt;https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL&gt;)

> [!NOTE]
> Per impostazione predefinita, dopo aver distribuita una macchina virtuale è possibile modificare la configurazione della rete virtuale hello. impostazioni TCP/IP Hello devono essere server DHCP di Azure toohello a sinistra. Il comportamento predefinito prevede l'assegnazione di IP dinamici.
>
>

indirizzo MAC della scheda di rete virtuale hello Hello può cambiare, ad esempio dopo il ridimensionamento e di Windows hello o sistema operativo guest Linux preleva nuova scheda di rete hello e utilizza automaticamente DHCP tooassign hello indirizzi IP e DNS in questo caso.

##### <a name="static-ip-assignment"></a>Assegnazione di indirizzi IP statici
È possibile tooassign fissata o indirizzi IP riservati tooVMs all'interno di una rete virtuale di Azure. Macchine virtuali di hello in esecuzione in una rete virtuale di Azure, viene aperto un tooleverage ampie possibilità questa funzionalità, se necessario o richiesto per alcuni scenari. assegnazione di indirizzi IP Hello rimane valida per l'esistenza di hello di hello macchina virtuale, indipendentemente se hello macchina virtuale è in fase di esecuzione o arrestato. Di conseguenza, è necessario tootake hello numero complessivo di macchine virtuali (VM in esecuzione e arrestate) in considerazione quando si definiscono hello intervallo di indirizzi IP per rete virtuale hello. indirizzo IP Hello rimane assegnato finché non viene eliminato hello macchina virtuale e la relativa interfaccia di rete o fino a quando l'indirizzo IP hello Ottiene nuovo annullata l'assegnazione. Per altre informazioni, leggere [questo articolo][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Più schede di interfaccia di rete per ogni VM
È possibile definire più schede di interfaccia di rete virtuali (vNIC, Virtual Network Interface Card) per una macchina virtuale di Azure. Hello possibilità toohave più vNICs è possibile avviare tooset di separazione del traffico di rete in cui, ad esempio, client traffico viene instradato tramite una scheda di rete virtuale e back-end traffico viene instradato tramite una seconda scheda di rete virtuale. L'attributo che dipendono dal tipo di hello della macchina virtuale sono disponibili diverse limitazioni in numero toohello di vNICs. Per informazioni dettagliate precise, funzionalità e limitazioni, vedere questi articoli:

* [Creare una VM Windows con più schede di interfaccia di rete][virtual-networks-multiple-nics-windows]
* [Creare una VM Linux con più schede di interfaccia di rete][virtual-networks-multiple-nics-linux]
* [Distribuire macchine virtuali con più NIC tramite un modello][virtual-network-deploy-multinic-arm-template]
* [Distribuire macchine virtuali con più NIC tramite PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Distribuire le macchine virtuali NIC multi utilizzando hello CLI di Azure][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Connettività da sito a sito
La soluzione cross-premise è costituita da macchine virtuali di Azure e locali collegate tramite una connessione VPN trasparente e permanente. È previsto toobecome hello più comune modello di distribuzione SAP in Azure. il presupposto di Hello è che i processi con le istanze di SAP in Azure e procedure operative dovrebbero funzionare in modo trasparente. Ciò significa che è necessario essere in grado di tooprint da questi sistemi, nonché utilizzare hello tootransport di sistema di gestione trasporto (TMS) SAP viene modificato da un sistema di sviluppo in Azure tooa sistema, che viene distribuita in locale. Per altre informazioni sulla modalità da sito a sito, vedere [questo articolo][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Dispositivo tunnel VPN
In ordine toocreate una connessione site-to-site (nel data center tooAzure data center locale), è necessario tooeither ottenere e configurare un dispositivo VPN oppure utilizzare il servizio Routing e accesso remoto (RRAS) che è stato introdotto come un componente software con Windows Server 2012.

* [Creare una rete virtuale con una connessione VPN da sito a sito mediante PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [Informazioni sui dispositivi VPN per le connessioni di gateway VPN da sito a sito][vpn-gateway-about-vpn-devices]
* [Domande frequenti sul gateway VPN][vpn-gateway-vpn-faq]

![Connessione da sito a sito tra rete locale e Azure][planning-guide-figure-600]

Hello nella figura precedente mostra due sottoscrizioni Azure dispongono di intervalli secondari di indirizzi IP riservati per l'uso in reti virtuali in Azure. connettività Hello da hello locale tooAzure di rete viene stabilita via VPN.

#### <a name="point-to-site-vpn"></a>VPN da punto a sito
VPN Point-to-site richiede ogni tooconnect di computer client con il proprio VPN in Azure. Per gli scenari SAP hello in esame, la connettività point-to-site non è pratica. Di conseguenza, nessun ulteriore riferimento viene fornito la connettività VPN da sito a toopoint.

Ulteriori informazioni sono disponibili qui
* [Configurare un tooa connessione Point-to-Site rete virtuale utilizzando hello portale di Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [Configurare un tooa connessione Point-to-Site rete virtuale con PowerShell](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>VPN multisito
Azure offre inoltre oggi hello possibilità toocreate multisito connettività VPN per una sottoscrizione di Azure. Una singola sottoscrizione in precedenza era limitato tooone connessione di VPN site-to-site. Questa limitazione è stata rimossa grazie alle connessioni VPN multisito per una singola sottoscrizione. Questo rende possibile tooleverage più di una regione di Azure per una sottoscrizione specifica tramite le configurazioni cross-premise.

Per altre informazioni, vedere [questo articolo][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO found no ARM docu link)

#### <a name="vnet-toovnet-connection"></a>Rete virtuale tooVNet connessione
Tramite una VPN multisito, è necessario tooconfigure una rete virtuale di Azure distinta in ognuna delle aree di hello. Tuttavia molto spesso è il requisito hello che i componenti software hello in aree diverse hello devono comunicare tra loro. Idealmente questa comunicazione non dovrebbe essere indirizzata da una regione di Azure tooon-locale e da toohello esistono altre aree di Azure. tooshortcut, Azure offre hello possibilità tooconfigure una connessione da una rete virtuale di Azure in un'area tooanother, che rete virtuale di Azure ospitati in un'altra area. Questa funzionalità viene definita connessione da rete virtuale a rete virtuale. Altri dettagli su questa funzionalità sono disponibili qui: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>Privato connessione tooAzure-ExpressRoute
Microsoft Azure ExpressRoute consente hello creare connessioni private tra data center di Azure e l'infrastruttura locale del cliente entrambi hello o in un ambiente di condivisione percorso. ExpressRoute viene offerto da diversi provider di VPN MPLS (con scambio di pacchetto) o da altri provider di servizi di rete. Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. Le connessioni ExpressRoute offrono una maggiore sicurezza, maggiore affidabilità più circuiti paralleli, velocità più elevate e minori latenze rispetto alle connessioni tramite hello Internet.

Altri dettagli su Azure ExpressRoute e sulle offerte sono disponibili qui:

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

ExpressRoute abilita più sottoscrizioni di Azure tramite un circuito ExpressRoute, come illustrato qui

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Tunneling forzato in caso di scenari cross-premise
Per le macchine virtuali di accesso ai domini locali tramite site-to-site, point-to-site o ExpressRoute, è necessario assicurarsi che le impostazioni proxy di Internet hello vengano distribuite per tutti gli utenti di hello in queste macchine virtuali anche toomake. Per impostazione predefinita, il software in esecuzione in queste macchine virtuali o gli utenti che usano un hello tooaccess browser internet non attraverseranno proxy aziendale hello, ma si connetteranno direttamente tramite Azure toohello internet. Ma l'impostazione proxy hello anche non è un traffico di hello toodirect soluzione 100% tramite proxy aziendale hello perché è responsabilità del software e servizi toocheck per proxy hello. Se il software in esecuzione nella macchina virtuale hello non esegue questa operazione o l'amministratore modifica le impostazioni di hello, toohello il traffico Internet può essere reindirizzato direttamente tramite Azure toohello Internet.

In ordine tooavoid questo, è possibile configurare il Tunneling forzato con connettività da sito a sito tra sedi locali e Azure. Hello descrizione dettagliata della funzionalità di Tunneling forzato hello viene pubblicato qui <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Tunneling forzato con ExpressRoute è abilitato per i clienti annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering.

#### <a name="summary-of-azure-networking"></a>Riepilogo dei servizi di rete di Azure
Questo capitolo include molti aspetti importanti relativi ai servizi di rete di Azure. Di seguito è riportato un riepilogo dei punti principali hello:

* Reti virtuali di Azure consente tooset rete hello eseguito in base alle proprie esigenze tooyour
* Reti virtuali di Azure possono essere sfruttate tooassign IP indirizzo intervalli tooVMs o assegnare tooVMs di indirizzi IP fissi
* tooset un Site-To-Site o di una connessione Point-To-Site, è necessario innanzitutto toocreate una rete virtuale di Azure
* Dopo la distribuzione di una macchina virtuale, non è più possibile toochange hello che toohello VM assegnare rete virtuale

### <a name="quotas-in-azure-virtual-machine-services"></a>Quote nei servizi Macchine virtuali di Azure
È necessario toobe cancellare sulle tabelle dei fatti hello che l'archiviazione hello e infrastruttura di rete è condivisa tra le macchine virtuali in esecuzione una varietà di servizi in hello dell'infrastruttura di Azure. E come nei data center di hello del cliente, l'overprovisioning di alcune delle risorse dell'infrastruttura hello grado tooa sul posto. Hello piattaforma Microsoft Azure Usa disco, CPU, rete e altri consumo di risorse di quote toolimit hello e prestazioni coerenti e deterministiche toopreserve.  Hello diversi tipi di macchine Virtuali (A5, A6 e così via) hanno quote diverse per il numero di dischi, CPU, RAM, hello e di rete.

> [!NOTE]
> Risorse della CPU e memoria dei tipi VM hello supportati da SAP sono preallocate nei nodi host hello. Ciò significa che una volta distribuito, hello VM hello risorse nell'host di hello disponibili come definito dal tipo di macchina virtuale hello.
>
>

Quando la pianificazione e dimensionamento di SAP in soluzioni Azure hello le quote per ogni dimensione di macchina virtuale deve essere considerata. vengono descritte le quote VM Hello [qui (Linux)] [ virtual-machines-sizes-linux] e [qui (Windows)][virtual-machines-sizes-windows].

quote di Hello descritte rappresentano valori massimi teorici hello.  limite Hello di IOPS per ogni disco può essere ottenuto ridotti (8kb), ma potrebbe non essere realizzate con IOs di grandi dimensioni (1Mb).  limite di IOPS Hello è applicato sulla granularità hello del disco singolo.

In un toodecide di albero delle decisioni approssimativa se si inserisce un sistema SAP in servizi macchine virtuali di Azure e alle relative funzionalità o se un sistema esistente deve toobe configurato in modo diverso nel sistema di ordini toodeploy hello in Azure, è possibile utilizzare un albero delle decisioni hello seguente:

![Toodecide di albero delle decisioni, toodeploy possibilità SAP in Azure][planning-guide-figure-700]

**Passaggio 1**: hello più importanti informazioni toostart con è requisiti SAPS hello per uno specifico sistema SAP. Hello SAPS requisiti necessità toobe ripartiti in parte DBMS hello e ambito di applicazione hello SAP, anche se hello sistema SAP è già distribuito in locale in una configurazione a 2 livelli. Per i sistemi esistenti, hello SAPS correlati toohello hardware in uso spesso può essere determinati o stimati in base attuali benchmark SAP. risultati Hello è reperibile qui: <http://global.sap.com/campaigns/benchmark/index.epx>.
Per i nuovi sistemi SAP distribuiti, è necessario calcolare le dimensioni e ottenere, che deve determinare i requisiti SAPS hello del sistema hello.
Per informazioni sul ridimensionamento di SAP in Azure, vedere anche questo post di blog e il documento allegato: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Passaggio 2**: per i sistemi esistenti, hello volume dei / o e operazioni dei / o al secondo nel server DBMS hello devono essere misurate. Per i nuovi sistemi pianificati, prestare hello ridimensionamento esercizio per il nuovo sistema di hello anche idee approssimative dei requisiti dei / o hello sul lato DBMS hello. In caso di dubbi, è necessario infine tooconduct un modello di prova.

**Passaggio 3**: requisiti SAPS hello di confronto per hello server DBMS con hello SAPS hello diversi tipi di macchine Virtuali di Azure può offrire. informazioni di Hello sui valori SAPS dei diversi tipi di macchina virtuale di Azure hello sono documentate nella nota SAP [1928533]. lo stato attivo Hello deve trovarsi in hello VM DBMS prima poiché il livello di database hello è hello in un sistema SAP NetWeaver che non scala orizzontalmente nella maggior parte di hello delle distribuzioni. Al contrario, è possibile scalare orizzontalmente livello dell'applicazione SAP hello. Se nessuno dei hello SAP supportati tipi di macchine Virtuali di Azure è in grado di offrire SAPS hello necessario, carico di lavoro di hello del sistema SAP hello pianificato non può essere eseguito in Azure. È necessario toodeploy hello sistema locale o al volume del carico di lavoro di hello toochange per sistema hello.

**Passaggio 4**: come documentato [qui (Linux)][virtual-machines-sizes-linux] e [qui (Windows)][virtual-machines-sizes-windows], Azure applica una quota di operazioni di I/O al secondo a ogni disco a prescindere dall'uso dell'archiviazione Standard o dell'archiviazione Premium. Dipende dal tipo di macchina virtuale hello, numero di hello di dischi dati, che è possibile montare varia. Di conseguenza, è possibile calcolare un numero massimo di IOPS che può essere ottenuto con ognuno dei diversi tipi di macchine Virtuali hello. Dipende dal layout del file hello database, è possibile eseguire lo striping dischi toobecome un volume del sistema operativo guest hello. Tuttavia, se hello volume corrente di IOPS di un sistema SAP distribuito supera i limiti di hello calcolato del tipo di macchina virtuale di Azure e se non vi è alcun toocompensate possibilità con più memoria più grande hello, carico di lavoro hello di hello sistema SAP può essere ragguardevoli. In questi casi, è possibile raggiungere un punto in cui non è necessario distribuire il sistema hello in Azure.

**Passaggio 5**: particolare nei sistemi SAP, che vengono distribuiti in locale in configurazioni a 2 livelli, il possibilità hello è che il sistema hello potrebbe essere necessario toobe configurato in Azure in una configurazione a 3 livelli. In questo passaggio, è necessario toocheck se c'è un componente nel livello applicazione hello SAP, alla quale non può essere scalato orizzontalmente e che non entra hello CPU e memoria risorse hello offerta di tipi di macchina virtuale di Azure differente. Se in realtà è un componente di questo tipo, sistema SAP hello e il carico di lavoro non può essere distribuiti in Azure. Ma se è possibile scalare orizzontalmente i componenti dell'applicazione SAP hello in più macchine virtuali di Azure, il sistema hello può essere distribuito in Azure.

**Passaggio 6**: se hello DBMS e componenti di livello applicazione SAP possono essere eseguiti in macchine virtuali di Azure, la configurazione di hello deve toobe definito quanto riguarda:

* Numero di macchine virtuali di Azure
* Tipi di macchine Virtuali per i singoli componenti hello
* Numero di dischi rigidi virtuali in VM DBMS tooprovide sufficiente di IOPS

## <a name="managing-azure-assets"></a>Gestione degli asset di Azure
### <a name="azure-portal"></a>Portale di Azure
Hello portale di Azure è una delle distribuzioni di tre interfacce toomanage macchina virtuale di Azure. attività di gestione di base Hello, come la distribuzione di macchine virtuali da immagini, possono essere eseguite tramite hello portale di Azure. Hello, inoltre, la creazione di account di archiviazione, reti virtuali, e altri componenti di Azure sono anche attività hello portale di Azure è possibile gestire molto bene. Tuttavia, funzionalità quali il caricamento di dischi rigidi virtuali da tooAzure locale o la copia di un disco rigido virtuale in Azure sono attività che richiedono strumenti di terze parti o amministrazione tramite PowerShell o CLI.

![Portale di Microsoft Azure: panoramica delle macchine virtuali][planning-guide-figure-800]

[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * &lt;https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/&gt;)

Attività di amministrazione e configurazione per l'istanza di macchina virtuale hello sono possibili all'interno di hello portale di Azure.

Oltre a riavviare e arrestare una macchina virtuale è possibile anche allegare, disconnettere e creare dischi dati hello macchina virtuale istanza toocapture hello per la preparazione dell'immagine e configurare dimensioni hello dell'istanza di macchina virtuale hello.

Hello portale di Azure fornisce funzionalità di base toodeploy e configurare macchine virtuali e molti altri servizi di Azure. Tuttavia non tutte le funzionalità disponibili sono coperto da hello portale di Azure. Nel portale di Azure hello, non è possibile tooperform attività, ad esempio:

* Caricamento di dischi rigidi virtuali tooAzure
* Copiare macchine virtuali

[comment]: <> (MShermannd TODO what about automation service for SAP VMs ? )
[comment]: <> (MSSedusch deployment of multiple VMs os meanwhile possible)
[comment]: <> (MSSedusch anche qualsiasi tipo di automazione per la distribuzione non è possibile con hello portale di Azure. Attività quali la distribuzione tramite script di più macchine virtuali non è possibile tramite hello portale di Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Gestione con i cmdlet di Microsoft Azure PowerShell
Windows PowerShell è un framework potente ed estensibile che è stato ampiamente adottato dai clienti che distribuiscono grandi quantità di sistemi in Azure. Dopo l'installazione dei cmdlet di PowerShell in un desktop, portatile o workstation di gestione dedicata hello hello i cmdlet di PowerShell può essere eseguito in modalità remota.

Hello tooenable processo un desktop/portatile locale per l'utilizzo di hello dei cmdlet PowerShell di Azure e come quelli per hello utilizzo con tooconfigure hello Azure delle sottoscrizioni sono descritta nell'argomento [questo articolo][powershell-install-configure].

Procedure più dettagliate su come tooinstall, aggiornare e configurare i cmdlet di Azure PowerShell hello possono essere rilevate anche in [in questo capitolo della Guida alla distribuzione hello][deployment-guide-4.1].

Analisi utilizzo software finora è stato PowerShell (PS) è certamente hello più potente strumento toodeploy macchine virtuali e toocreate personalizzato di passaggi di distribuzione hello di macchine virtuali. Tutti i clienti di hello in esecuzione le istanze di SAP in Azure utilizza PS cmdlet toosupplement attività di gestione che nel portale di Azure hello o anche i cmdlet di PS toomanage esclusivamente le distribuzioni in Azure. Condivisione di cmdlet specifici di Azure hello hello stessa convenzione di denominazione come hello oltre 2000 cmdlet correlati a Windows, ed è una semplice attività per Windows amministratori tooleverage questi cmdlet.

Per esempi, vedere qui: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO describe new CLI command when tested )
Distribuzione di hello Azure Monitoring Extension per SAP (vedere il capitolo [soluzione di monitoraggio di Azure per SAP] [ planning-guide-9.1] in questo documento) è possibile solo tramite PowerShell o CLI. Pertanto è obbligatorio tooset backup e configurare PowerShell o CLI quando si distribuisce o amministrazione di un sistema SAP NetWeaver in Azure.  

Quando Azure offrirà più funzionalità, i nuovi cmdlet di PS sta toobe aggiunto che richiede un aggiornamento di hello cmdlet. Pertanto hello toocheck senso sito di Download di Azure ad almeno una volta il mese hello <https://azure.microsoft.com/downloads/> per una nuova versione di hello cmdlet. nuova versione di Hello è installato in versione di hello.

Per un elenco generale dei comandi di PowerShell correlati ad Azure, vedere <https://docs.microsoft.com/powershell/azure/overview>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Gestione con i comandi dell'interfaccia della riga di comando di Microsoft Azure
Per i clienti che utilizzano Linux e desidera toomanage Azure Powershell risorse potrebbero non essere un'opzione. Microsoft offre l'interfaccia della riga di comando di Azure come alternativa.
Hello CLI di Azure fornisce un set di open source, multipiattaforma comandi per l'utilizzo con hello piattaforma Azure. Hello CLI di Azure fornisce gran parte delle stesse funzionalità trovata nel portale di Azure hello hello.

Per informazioni sull'installazione, configurazione e funzionamento dei comandi tooaccomplish toouse CLI di attività di Azure, vedere

* [Installare hello CLI di Azure][xplat-cli]
* [Distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello CLI di Azure] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Utilizzare hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure][xplat-cli-azure-resource-manager]

Leggere inoltre capitolo [CLI di Azure per le macchine virtuali Linux] [ deployment-guide-4.5.2] in hello [Guida alla distribuzione] [ planning-guide] in modo toouse CLI di Azure toodeploy hello Azure Monitoring Extension per SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Toodeploy diverse macchine virtuali per SAP in Azure
In questo capitolo viene illustrato hello modi toodeploy una macchina virtuale in Azure. Gli argomenti trattati includono le varie procedure di preparazione e la gestione dei dischi rigidi virtuali e delle macchine virtuali in Azure.

### <a name="deployment-of-vms-for-sap"></a>Distribuzione di VM per SAP
Microsoft Azure offre diversi modi di macchine virtuali toodeploy e associati i dischi. È pertanto differenze hello toounderstand molto importante perché preparazioni delle macchine virtuali hello potrebbero variare a seconda di metodo hello di distribuzione. In generale, è un quadro hello seguenti scenari:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Lo spostamento di una macchina virtuale da tooAzure locale con un disco non generalizzato
Si prevede un sistema SAP specifico da on-premise tooAzure toomove. Questo può essere eseguito caricando hello disco rigido virtuale, che contiene hello del sistema operativo, hello binari SAP e binari DBMS più hello dischi rigidi virtuali con file di dati e log hello di hello DBMS tooAzure. Al contrario troppo[scenario 2 di # seguito][planning-guide-5.1.2], mantenere hello hostname, il SID di SAP e gli account utente SAP in Azure VM hello come sono stati configurati nell'ambiente locale hello. Pertanto, generalizzare l'immagine di hello non è necessario. Vedere capitoli [preparazione per lo spostamento di una macchina virtuale da tooAzure locale con un disco non generalizzato] [ planning-guide-5.2.1] di questo documento per operazioni di preparazione in locale e il caricamento di tooAzure macchine virtuali o i dischi rigidi virtuali non generalizzate. Capitolo lettura [Scenario 3: spostare una macchina virtuale locale con un VHD di Azure non generalizzato con SAP] [ deployment-guide-3.4] in hello [Guida alla distribuzione] [ deployment-guide] Per informazioni dettagliate su come distribuire tale immagine in Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Distribuzione di una VM con un'immagine specifica del cliente
A causa di requisiti di patch toospecific della versione del sistema operativo o DBMS, le immagini fornita hello in hello Azure Marketplace potrebbero non soddisfare le proprie esigenze. Di conseguenza, potrebbe essere necessario toocreate una macchina virtuale tramite la propria immagine di macchina virtuale del sistema operativo/DBMS 'private', che può essere distribuito più volte in un secondo momento. tooprepare questa immagine 'privata' per la duplicazione, hello seguenti elementi è considerati toobe:

- - -
> ![Windows][Logo_Windows] Windows
>
> Visualizzare ulteriori dettagli qui: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> le impostazioni di Windows hello (ad esempio SID e il nome host) è necessario estrarre/generalizzare hello locale Macchina virtuale tramite il comando di sysprep hello.
>
>
> ![Linux][Logo_Linux] Linux
>
> Seguire i passaggi di hello descritti negli articoli seguenti per [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], o [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooprepare toobe un disco rigido virtuale caricato tooAzure.
>
>

- - -
Se è già stato installato contenuto SAP nella macchina virtuale locale (in particolare per i sistemi di livello 2), è possibile adattare le impostazioni di sistema SAP hello dopo la distribuzione di hello di hello macchina virtuale di Azure tramite istanza hello rinominare procedure supportate da SAP Software Provisioning hello Manager (nota SAP [1619720]). Vedere capitoli [preparazione per la distribuzione di una macchina virtuale con un'immagine di specifiche del cliente per SAP] [ planning-guide-5.2.2] e [il caricamento di un disco rigido virtuale da on-premise tooAzure] [ planning-guide-5.3.2]di questo documento per operazioni di preparazione in locale e il caricamento di un tooAzure macchina virtuale generalizzata. Capitolo lettura [nello Scenario 2: distribuzione di una macchina virtuale con un'immagine personalizzata per SAP] [ deployment-guide-3.3] in hello [Guida alla distribuzione] [ deployment-guide] per informazioni dettagliate di distribuzione tale immagine in Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Distribuzione di una macchina virtuale dalla hello Azure Marketplace
Desidera toouse Microsoft o terze parti forniti da hello Azure Marketplace toodeploy immagine di macchina virtuale di una macchina virtuale. Dopo aver distribuito la macchina virtuale in Azure, seguire hello stesse linee guida e gli strumenti tooinstall hello software SAP e/o DBMS nella macchina virtuale come si farebbe in un ambiente locale. Per informazioni dettagliate descrizione della distribuzione, vedere il capitolo [lo Scenario 1: distribuzione di una macchina virtuale dalla hello Azure Marketplace per SAP] [ deployment-guide-3.2] in hello [Guida alla distribuzione] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Preparazione di VM con SAP per Azure
Prima di caricare macchine virtuali in Azure è necessario che le macchine virtuali hello e dischi rigidi virtuali soddisfano determinati requisiti toomake. Esistono piccole differenze in base al metodo di distribuzione hello utilizzato.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Preparazione per lo spostamento di una macchina virtuale da tooAzure locale con un disco non generalizzato
Un metodo di distribuzione comune è toomove una macchina virtuale esistente che esegue un sistema SAP da tooAzure locale. Che macchina virtuale e il sistema SAP in VM devono essere eseguiti in Azure tramite hello hello hello stesso nome host e molto probabilmente hello stesso SID di SAP. In questo caso hello del sistema operativo della macchina virtuale guest non deve essere generalizzato per più distribuzioni. Se rete locale hello venga estesa in Azure (vedere il capitolo [cross-premise - distribuzione di una o più macchine virtuali SAP in Azure con il requisito di hello di siano pienamente integrate nella rete locale hello] [ planning-guide-2.2] in questo documento), quindi anche hello stessi account di dominio consente all'interno di hello VM come quelli usati in precedenza in locale.

I requisiti per la preparazione del disco della VM di Azure sono:

* Originariamente hello disco rigido virtuale contenente hello del sistema operativo potrebbe avere solo una dimensione massima di 127GB. Questa limitazione è stata eliminata alla fine di hello di marzo 2015. Ora hello disco rigido virtuale contenente hello del sistema operativo può essere backup too1TB dimensioni come qualsiasi altro dispositivo di archiviazione Azure ospitata nonché di disco rigido virtuale.
* È necessario che toobe in hello in formato VHD fisso. Il disco o i dischi rigidi virtuali dinamici in formato VHDx non sono ancora supportati in Azure. Dischi rigidi virtuali dinamici sarà toostatic convertire i dischi rigidi virtuali quando si carica hello disco rigido virtuale con i cmdlet di PowerShell o CLI
* Dischi rigidi virtuali montato toohello VM e devono essere montati di nuovo in Azure toohello VM necessario toobe in un formato di disco rigido virtuale fisso anche. Leggere [questo articolo (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) e [questo articolo (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) per i limiti dimensionali dei dischi dati. Dischi rigidi virtuali dinamici sarà toostatic convertire i dischi rigidi virtuali quando si carica hello disco rigido virtuale con i cmdlet di PowerShell o CLI
* Aggiungere un altro account locale con privilegi di amministratore che può essere utilizzato dal supporto tecnico Microsoft o che può essere assegnato come contesto per i servizi e applicazioni toorun in finché hello che macchina virtuale viene distribuita e utenti più appropriati può essere utilizzato.
* Per caso hello di uno scenario di distribuzione solo Cloud (vedere il capitolo [solo Cloud - distribuzioni di macchine virtuali in Azure senza dipendenze da hello locale rete cliente] [ planning-guide-2.1] di questo oggetto il documento) in combinazione con questo metodo di distribuzione, dominio account potrebbero non funzionare dopo hello disco di Azure viene distribuito in Azure. Ciò vale soprattutto per gli account che sono servizi toorun usato come hello DBMS o applicazioni SAP. Pertanto necessario tooreplace questi account di dominio con account locali di macchina virtuale ed eliminare gli account di dominio locale hello in hello macchina virtuale. Mantenere gli utenti del dominio locale nell'immagine di macchina virtuale hello non costituisce un problema quando hello macchina virtuale viene distribuita in hello scenario cross-premise descritta nel capitolo [Cross-premise - distribuzione di una o più macchine virtuali SAP in Azure con obbligo di hello di completamente integrato in una rete locale hello] [ planning-guide-2.2] in questo documento.
* Se sono stati usati account di dominio come account di accesso DBMS o gli utenti durante l'esecuzione hello sistema locale e tali macchine virtuali devono toobe distribuiti negli scenari di solo Cloud, gli utenti di dominio hello devono toobe eliminato. È necessario assicurarsi che messaggio per l'amministratore locale e un altro utente locale di macchina virtuale viene aggiunto come un account di accesso/utente in DBMS come amministratori hello toomake.
* Aggiungere altri account locali, come quelli potrebbe essere necessaria per hello specifico scenario di distribuzione.

- - -
> ![Windows][Logo_Windows] Windows
>
> In questo scenario Nessuna generalizzazione (sysprep) di hello VM è necessario tooupload e distribuire hello macchina virtuale in Azure.
> Accertarsi che non venga utilizzata l’unità D:\.
> Impostare il montaggio automatico dei dischi collegati come descritto nel capitolo [Impostazione del montaggio automatico per dischi collegati][planning-guide-5.5.3] di questo documento.
>
> ![Linux][Logo_Linux] Linux
>
> In questo scenario Nessuna generalizzazione (comando waagent-deprovision) di hello VM, è necessario tooupload e distribuire hello macchina virtuale in Azure.
> Assicurarsi che /mnt/resource non sia usato e che TUTTI i dischi siano montati con UUID. Per il disco di hello del sistema operativo, verificare che voce del caricatore di avvio hello anche montaggio basato su uuid hello.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Preparazione per la distribuzione di una VM con un'immagine specifica del cliente per SAP
I file dei dischi rigidi virtuali che contengono un sistema operativo generalizzato vengono archiviati in contenitori negli account di archiviazione di Azure o come immagini di dischi gestiti. È possibile distribuire una nuova macchina virtuale da un'immagine facendo riferimento immagine di disco rigido virtuale o del disco gestito hello come origine nei file di modello di distribuzione descritta nel capitolo [nello Scenario 2: distribuzione di una macchina virtuale con un'immagine personalizzata per SAP] [ deployment-guide-3.3]di hello [Guida alla distribuzione][deployment-guide].

I requisiti per la preparazione dell'immagine di VM di Azure sono:

* Originariamente hello disco rigido virtuale contenente hello del sistema operativo potrebbe avere solo una dimensione massima di 127GB. Questa limitazione è stata eliminata alla fine di hello di marzo 2015. Ora hello disco rigido virtuale contenente hello del sistema operativo può essere backup too1TB dimensioni come qualsiasi altro dispositivo di archiviazione Azure ospitata nonché di disco rigido virtuale.
* È necessario che toobe in hello in formato VHD fisso. Il disco o i dischi rigidi virtuali dinamici in formato VHDx non sono ancora supportati in Azure. Dischi rigidi virtuali dinamici sarà toostatic convertire i dischi rigidi virtuali quando si carica hello disco rigido virtuale con i cmdlet di PowerShell o CLI
* Dischi rigidi virtuali montato toohello VM e devono essere montati di nuovo in Azure toohello VM necessario toobe in un formato di disco rigido virtuale fisso anche. Leggere [questo articolo (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) e [questo articolo (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) per i limiti dimensionali dei dischi dati. Dischi rigidi virtuali dinamici sarà toostatic convertire i dischi rigidi virtuali quando si carica hello disco rigido virtuale con i cmdlet di PowerShell o CLI
* Poiché tutti gli utenti di dominio registrati come utenti in hello VM non esiste in uno scenario solo Cloud di hello (vedere il capitolo [solo Cloud - distribuzioni di macchine virtuali in Azure senza dipendenze da hello locale rete cliente] [ planning-guide-2.1] di questo documento), i servizi che usano il dominio di questo account potrebbero non funzionare dopo la distribuzione di hello immagine in Azure. Ciò vale soprattutto per gli account sono utilizzati toorun servizi come DBMS o applicazioni SAP. Pertanto necessario tooreplace questi account di dominio con account locali di macchina virtuale ed eliminare gli account di dominio locale hello in hello macchina virtuale. Mantenere gli utenti del dominio locale nell'immagine di macchina virtuale hello non sia un problema quando una macchina virtuale viene distribuita in hello hello scenario cross-premise descritta nel capitolo [Cross-premise - distribuzione di una o più macchine virtuali SAP in Azure con il requisito di hello di siano pienamente integrate nella rete locale hello] [ planning-guide-2.2] in questo documento.
* Aggiungere un altro account locale con privilegi di amministratore che può essere utilizzato dagli utenti più appropriati e supporto tecnico Microsoft nell'analisi dei problemi o che può essere assegnato come contesto per i servizi e applicazioni toorun in finché hello che macchina virtuale viene distribuita può essere utilizzato.
* Nelle distribuzioni solo Cloud e in cui sono stati usati account di dominio come account di accesso DBMS o gli utenti durante l'esecuzione di hello sistema locale, gli utenti del dominio hello devono essere eliminati. È necessario accertarsi che l'amministratore locale hello oltre a un altro utente locale di macchina virtuale è aggiunto come account di accesso/utente di hello DBMS come amministratori toomake.
* Aggiungere altri account locali, come quelli potrebbe essere necessaria per hello specifico scenario di distribuzione.
* Se è probabile che la ridenominazione del nome host hello dal nome originale del hello presso i punti di hello hello Azure distribuzione immagine hello contiene un'installazione di SAP NetWeaver, è consigliato toocopy versioni più recenti di hello hello SAP Software Provisioning Manager DVD in modello di Hello. Ciò consentirà tooeasily utilizzare hello SAP fornito Rinomina funzionalità tooadapt hello modificato il nome host e/o modifica hello SID del sistema SAP con hello hello distribuito l'immagine di macchina virtuale non appena viene avviata una nuova copia.

- - -
> ![Windows][Logo_Windows] Windows
>
> Verificare che l'unità D:\ non sia usata. Impostare il montaggio automatico dei dischi collegati come descritto nel capitolo [Impostazione del montaggio automatico per dischi collegati][planning-guide-5.5.3] di questo documento.
>
> ![Linux][Logo_Linux] Linux
>
> Assicurarsi che /mnt/resource non sia usato e che TUTTI i dischi siano montati con UUID. Per il disco del sistema operativo hello, assicurarsi di voce del caricatore di avvio hello riflette anche montaggio basato su uuid hello.
>
>

- - -
* L'interfaccia utente grafica (GUI) SAP può essere preinstallata in questo modello per scopi di amministrazione e installazione.
* Altro software necessario toorun hello correttamente in scenari di cross-premise le macchine virtuali possono essere installate, purché sia compatibile con hello rinominare di hello VM.

Se hello macchina virtuale viene preparata sufficientemente toobe generica ed eventualmente indipendente da account/utenti non è disponibili in hello destinazione uno scenario di distribuzione di Azure, viene effettuata hello ultimo passaggio di preparazione della generalizzazione di tale immagine.

##### <a name="generalizing-a-vm"></a>Generalizzazione di una macchina virtuale
- - -
> ![Windows][Logo_Windows] Windows
>
> ultimo passaggio Hello è toolog in tooa macchina virtuale con un account amministratore. Aprire una finestra di comando di Windows come "amministratore". Passare too%windir%\windows\system32\sysprep ed eseguire sysprep.exe.
> Viene visualizzata una finestra di piccole dimensioni. È importante toocheck hello 'Generalize' opzione (impostazione predefinita di hello è deselezionata) e modificare l'opzione di arresto hello da quello predefinito di 'Riavvia' too'Shutdown'. Questa procedura si presuppone che il processo di sysprep hello eseguita in locale in hello del sistema operativo Guest di una macchina virtuale.
> Se si desidera tooperform hello con una macchina virtuale già in esecuzione in Azure, seguire i passaggi di hello descritti in [questo articolo](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource).
>
> ![Linux][Logo_Linux] Linux
>
> [Come toocapture un toouse di macchina virtuale Linux come modello di gestione delle risorse][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Trasferimento di macchine virtuali e dischi rigidi virtuali tra tooAzure locale
Poiché il caricamento tooAzure immagini e dischi di macchina virtuale non è possibile tramite hello portale di Azure, è necessario toouse cmdlet di Azure PowerShell o CLI. Un'altra possibilità è utilizzare hello dello strumento hello 'AzCopy'. strumento Hello è possibile copiare i dischi rigidi virtuali tra sedi locali e Azure (in entrambe le direzioni). Può anche copiare i dischi rigidi virtuali tra le diverse aree di Azure. Per il download e l'uso di AzCopy, vedere [questa documentazione][storage-use-azcopy].

Una terza alternativa sarebbe toouse vari strumenti orientati alla GUI di terze parti. Tuttavia, assicurarsi che questi strumenti supportino i BLOB di pagine di Azure. Per questo scopo è necessario toouse Blob di pagine di Azure store (hello differenze sono illustrate qui: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). Anche gli strumenti di hello forniti da Azure sono molto efficienti nella compressione di macchine virtuali hello e dischi rigidi virtuali toobe caricato. Questo è importante perché questa efficienza nella compressione riduce il tempo di caricamento hello (che varia comunque a seconda di hello caricamento collegamento toohello internet dalla struttura di on-premise hello e area di distribuzione di Azure hello destinazione). È ragionevole supporre che il caricamento di una macchina virtuale o un disco rigido virtuale da una località europea toohello dati di Azure basata negli Stati Uniti Center richiederà più tempo rispetto al caricamento hello stesso data center di macchine virtuali/dischi rigidi virtuali toohello Azure europei.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Caricamento di un disco rigido virtuale da tooAzure locale
macchina virtuale esistente o un disco rigido virtuale da hello locale questa macchina virtuale di rete o un disco rigido virtuale deve requisiti hello toomeet come indicato nel capitolo tooupload [preparazione per lo spostamento di una macchina virtuale da tooAzure locale con un disco non generalizzato] [ planning-guide-5.2.1] di questo documento.

Questa macchina virtuale non è necessario toobe generalizzato e può essere caricata in stato hello e la forma che ha dopo l'arresto hello locale lato. Hello stesso vale per dischi rigidi virtuali aggiuntivi che non possono contenere qualsiasi sistema operativo.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Caricamento di un disco rigido virtuale e conversione in un disco di Azure
In questo caso si desidera tooupload un disco rigido virtuale, con o senza un sistema operativo e montarlo tooa macchina virtuale come disco dati o utilizzarlo come disco del sistema operativo. Il processo si articola in più passaggi

**PowerShell**

* Accedi a sottoscrizione tooyour con *AzureRmAccount di account di accesso*
* Impostare la sottoscrizione hello del contesto con *Set AzureRmContext* e parametro SubscriptionId o SubscriptionName - vedere <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Caricare hello VHD con *Aggiungi AzureRmVhd* tooan Account di archiviazione di Azure - vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Facoltativo) Creare un disco gestito da hello VHD con *New AzureRmDisk* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* Impostare il disco di hello del sistema operativo di un nuovo toohello di configurazione macchina virtuale VHD o gestiti con *Set AzureRmVMOSDisk* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* Creare una nuova macchina virtuale dalla configurazione di macchina virtuale hello con *New AzureRmVM* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* Aggiungere un tooa disco dati nuova macchina virtuale con *Aggiungi AzureRmVMDataDisk* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Interfaccia della riga di comando di Azure 2.0**

* Accedi a sottoscrizione tooyour con *accesso az*
* Selezionare la propria sottoscrizione con *az account set --subscription `<subscription name or id`>*
* Caricare hello VHD con *caricamento blob di archiviazione az* -vedere [Using hello CLI di Azure con l'archiviazione di Azure][storage-azure-cli]
* (Facoltativo) Creare un disco gestito da hello VHD con *disco az creare* -vedere https://docs.microsoft.com/cli/azure/disk#create
* Creare una nuova macchina virtuale specifica hello caricato disco rigido virtuale o del disco gestito come disco del sistema operativo con *creare vm az* e parametro *-collega disco di sistema operativo*
* Aggiungere un tooa disco dati nuova macchina virtuale con *collegare il disco di macchina virtuale az* e parametro *-nuovo*

**Modello**

* Caricare hello disco rigido virtuale con Powershell o CLI di Azure
* (Facoltativo) Creare un disco gestito da hello disco rigido virtuale con Powershell, CLI di Azure o hello portale di Azure
* Distribuire hello macchina virtuale con un modello JSON facendo riferimento hello disco rigido virtuale, come illustrato [questo modello JSON di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) o utilizzando dischi gestiti, come illustrato nel [questo modello JSON di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Distribuzione di un'immagine di VM
macchina virtuale esistente o un disco rigido virtuale da hello locale di rete in ordine toouse, come un'immagine di macchina virtuale di Azure, questa macchina virtuale o un disco rigido virtuale necessari requisiti di hello toomeet elencati nel capitolo tooupload [preparazione per la distribuzione di una macchina virtuale con un'immagine di specifiche del cliente per SAP] [ planning-guide-5.2.2] di questo documento.

* Utilizzare *sysprep* in Windows o *waagent-deprovision* su Linux toogeneralize la macchina virtuale - vedere [documentazione tecnica su Sysprep](https://technet.microsoft.com/library/cc766049.aspx) per Windows o [come toocapture un Toouse macchina virtuale Linux come un modello di gestione risorse] [ capture-image-linux-step-2-create-vm-image] per Linux
* Accedi a sottoscrizione tooyour con *AzureRmAccount di account di accesso*
* Impostare la sottoscrizione hello del contesto con *Set AzureRmContext* e parametro SubscriptionId o SubscriptionName - vedere <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Caricare hello VHD con *Aggiungi AzureRmVhd* tooan Account di archiviazione di Azure - vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Facoltativo) Creare un'immagine del disco gestito da hello VHD con *New AzureRmImage* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* Impostare il disco del sistema operativo hello di un nuovo toothe configurazione macchina virtuale
  * disco rigido virtuale con *Set-AzureRmVMOSDisk -SourceImageUri -CreateOption fromImage*; vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
  * Immagine del disco gestito *Set-AzureRmVMSourceImage*; vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>
* Creare una nuova macchina virtuale dalla configurazione di macchina virtuale hello con *New AzureRmVM* -vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Interfaccia della riga di comando di Azure 2.0**

* Utilizzare *sysprep* in Windows o *waagent-deprovision* su Linux toogeneralize la macchina virtuale - vedere [documentazione tecnica su Sysprep](https://technet.microsoft.com/library/cc766049.aspx) per Windows o [come toocapture un Toouse macchina virtuale Linux come un modello di gestione risorse] [ capture-image-linux-step-2-create-vm-image] per Linux
* Accedi a sottoscrizione tooyour con *accesso az*
* Selezionare la propria sottoscrizione con *az account set --subscription `<subscription name or id`>*
* Caricare hello VHD con *caricamento blob di archiviazione az* -vedere [Using hello CLI di Azure con l'archiviazione di Azure][storage-azure-cli]
* (Facoltativo) Creare un'immagine del disco gestito da hello VHD con *immagine az creare* -vedere https://docs.microsoft.com/cli/azure/image#create
* Creare una nuova macchina virtuale specifica hello caricato gestiti immagine di disco o VHD come disco del sistema operativo con *creare vm az* e parametro *-immagine*

**Modello**

* Utilizzare *sysprep* in Windows o *waagent-deprovision* su Linux toogeneralize la macchina virtuale - vedere [documentazione tecnica su Sysprep](https://technet.microsoft.com/library/cc766049.aspx) per Windows o [come toocapture un Toouse macchina virtuale Linux come un modello di gestione risorse] [ capture-image-linux-step-2-create-vm-image] per Linux
* Caricare hello disco rigido virtuale con Powershell o CLI di Azure
* (Facoltativo) Creare un'immagine del disco gestito da hello disco rigido virtuale con Powershell, CLI di Azure o hello portale di Azure
* Distribuire hello macchina virtuale con un modello JSON che fanno riferimento a come illustrato nell'immagine del disco rigido virtuale hello [questo modello JSON di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) o utilizzando hello gestiti immagine del disco, come illustrato nella [questo modello JSON di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>Download di dischi rigidi virtuali o dischi gestiti tooon locale
Infrastruttura di Azure come un servizio non è una strada unidirezionale di solo essere in grado di tooupload dischi rigidi virtuali e i sistemi SAP. È possibile spostare SAP locale HelloWorld nonché nuovamente sistemi da Azure.

Durante la fase di hello di hello download hello dischi rigidi virtuali o dischi gestiti non può essere attivo. Anche quando vengono scaricati dischi montati tooVMs, hello VM esigenze toobe chiuso e deallocato. Se si desidera solo toodownload hello contenuto del database che deve essere quindi utilizzato tooset imposta un nuovo sistema locale e se è accettabile che durante la fase di hello di hello scaricare e hello il programma di installazione del sistema hello nuovo hello sistema in Azure può essere comunque operativo , è possibile evitare un lungo periodo di inattività effettuando un backup compresso del database in un disco e scaricare solo tale disco anziché anche hello macchina virtuale di base del sistema operativo.

#### <a name="powershell"></a>PowerShell

  * Download di un disco gestito  
  È necessario innanzitutto tooget accesso toohello blob di hello disco gestito sottostante. È quindi possibile copiare hello sottostante tooa nuovo account di archiviazione blob e scaricare hello blob da questo account di archiviazione.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * Download di un disco rigido virtuale  
  Una volta hello sistema SAP viene arrestato e hello arresto della macchina virtuale, è possibile usare il cmdlet di PowerShell hello Salva AzureRmVhd nel hello locale ripristino dei dischi VHD di destinazione toodownload hello world locale toohello. In ordine toodo, è necessario URL hello del disco rigido virtuale che trova nella 'sezione archiviazione' hello hello di hello del portale di Azure (necessità toonavigate toohello Account di archiviazione e hello contenitore di archiviazione in cui hello disco rigido virtuale è stato creato) ed è necessario tooknow in cui hello disco rigido virtuale deve essere copiato.

  Quindi è possibile utilizzare il comando hello definendo semplicemente il parametro hello SourceUri come URL hello toodownload VHD hello e hello LocalFilePath come percorso fisico di hello di hello disco rigido virtuale (incluso il relativo nome). come potrebbe apparire comando Hello:

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Per informazioni dettagliate di hello Salva AzureRmVhd cmdlet, vedere <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>.

#### <a name="cli-20"></a>Interfaccia della riga di comando 2.0
  * Download di un disco gestito  
  È necessario innanzitutto tooget accesso toohello blob di hello disco gestito sottostante. È quindi possibile copiare hello sottostante tooa nuovo account di archiviazione blob e scaricare hello blob da questo account di archiviazione.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * Download di un disco rigido virtuale   
  Una volta hello sistema SAP viene arrestato e hello arresto della macchina virtuale, è possibile utilizzare un comando CLI di Azure hello _download di blob di archiviazione di azure_ nella destinazione locale hello hello toodownload VHD dischi world locale toohello indietro. In ordine toodo, è necessario il nome di hello e contenitore hello del disco rigido virtuale che trova nella 'sezione archiviazione' hello hello di hello del portale di Azure (necessità toonavigate toohello Account di archiviazione e hello contenitore di archiviazione in cui hello disco rigido virtuale è stato creato) ed è necessario tooknow in Hello disco rigido virtuale deve essere copiato.

  Quindi è possibile utilizzare il comando hello definendo semplicemente hello parametri blob e contenitori di toodownload VHD hello e di destinazione hello come percorso di destinazione fisico hello di hello disco rigido virtuale (incluso il relativo nome). come potrebbe apparire comando Hello:

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>Trasferimento di VM e dischi in Azure
#### <a name="copying-sap-systems-within-azure"></a>Copia di sistemi SAP in Azure
Un sistema SAP o anche un server DBMS dedicato che supporta un livello dell'applicazione SAP sarà probabilmente sono costituiti da più dischi che contengono entrambi hello del sistema operativo con i file binari hello o hello dati e i file registro del database SAP hello. Hello funzionalità di copia dei dischi di Azure né di salvataggio su disco locale di dischi tooa hello sono un meccanismo di sincronizzazione, che verrebbe snapshot più dischi in modo sincrono. Pertanto, lo stato di hello di hello copiati o salvato i dischi, anche se vengono montati su hello sarebbe diverso stessa macchina virtuale. Ciò significa che in caso di concreta hello di disporre di dati diversi e log contenuti in dischi diversi hello, database hello fine hello non sarà coerenti.

**Conclusione: Ordine toocopy o salvare dischi che fanno parte della configurazione di un sistema SAP è necessario sistema SAP di hello toostop ed è anche necessario tooshut verso il basso hello distribuito macchina virtuale. Solo a questo punto è possibile copiare o scaricare hello set di dischi tooeither creare una copia di hello sistema SAP in Azure o in locale.**

Dischi dati possono essere archiviati come file VHD nell'Account di archiviazione di Azure e possono essere una macchina virtuale tooa collegata direttamente o essere utilizzati come immagine. In questo caso, hello VHD è copiato tooanother percorso prima della macchina virtuale toohello associata. nome completo di Hello del file VHD hello in Azure deve essere univoco in Azure. Come accennato in precedenza è già, il nome di hello è un tipo di nome in tre parti simile:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

I dischi dati possono essere anche Managed Disks. In questo caso, hello gestito disco è utilizzato toocreate Managed nuovo disco prima della macchina virtuale toohello associata. nome Hello di hello disco gestito deve essere univoco all'interno di un gruppo di risorse.

##### <a name="powershell"></a>PowerShell
È possibile utilizzare i cmdlet di Azure PowerShell toocopy un disco rigido virtuale, come illustrato nella [questo articolo][storage-powershell-guide-full-copy-vhd]. toocreate un nuovo disco gestito, utilizzare New-AzureRmDiskConfig e New-AzureRmDisk come illustrato nell'esempio seguente hello.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>Interfaccia della riga di comando 2.0
È possibile utilizzare Azure CLI toocopy un disco rigido virtuale, come illustrato nella [questo articolo][storage-azure-cli-copy-blobs]. toocreate un nuovo disco gestito, utilizzare *disco az creare* come illustrato nell'esempio seguente hello.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Strumenti di archiviazione di Azure
* <http://storageexplorer.com/>

Edizioni professionali degli strumenti di esplorazione di archiviazione di Azure sono disponibili qui:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

copia di Hello di un disco rigido virtuale all'interno di un account di archiviazione è un processo che richiede solo pochi secondi (simile tooSAN hardware la creazione di snapshot con copia lazy e copia in scrittura). Dopo aver creato una copia del file di disco rigido virtuale hello è possibile collegare la macchina virtuale tooa o utilizzare come un'immagine tooattach copia macchine toovirtual del disco rigido virtuale hello.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>Interfaccia della riga di comando 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Copia di dischi tra account di archiviazione di Azure
Questa attività non può essere eseguita nel portale di Azure hello. È possibile usare i cmdlet di Azure PowerShell, l'interfaccia della riga di comando di Azure o un browser di archiviazione terze parti. Hello i cmdlet di PowerShell o i comandi CLI è possono creare e gestire BLOB, che includono BLOB di copia di hello possibilità tooasynchronously tra gli account di archiviazione e tra aree all'interno di hello sottoscrizione di Azure.

##### <a name="powershell"></a>PowerShell
È inoltre possibile copiare i dischi rigidi virtuali tra le sottoscrizioni. Per altre informazioni, leggere [questo articolo][storage-powershell-guide-full-copy-vhd].

flusso di base della logica di cmdlet di PS hello Hello è simile al seguente:

* Creare un contesto di account di archiviazione per hello **origine** account di archiviazione con *New AzureStorageContext* -vedere <https://msdn.microsoft.com/library/dn806380.aspx>
* Creare un contesto di account di archiviazione per hello **destinazione** account di archiviazione con *New AzureStorageContext* -vedere <https://msdn.microsoft.com/library/dn806380.aspx>
* Avviare la copia hello con

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Controllare lo stato di hello della copia hello in un ciclo con

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Collegare hello nuova VHD tooa macchina virtuale, come descritto in precedenza.

Per alcuni esempi, vedere [questo articolo][storage-powershell-guide-full-copy-vhd].

##### <a name="cli-20"></a>Interfaccia della riga di comando 2.0
* Avviare la copia hello con

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* Controllare lo stato di hello se hello copia in un ciclo con

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Collegare hello nuova VHD tooa macchina virtuale, come descritto in precedenza.

Per alcuni esempi, vedere [questo articolo][storage-azure-cli-copy-blobs].

### <a name="disk-handling"></a>Gestione del disco
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Struttura di macchina virtuale/disco per le distribuzioni SAP
Idealmente hello la gestione della struttura di hello di una macchina virtuale e i dischi associato hello dovrebbero essere molto semplici. Nelle installazioni locali, i clienti hanno sviluppato diverse procedure per strutturare un'installazione server.

* Un disco di base che contiene hello del sistema operativo e tutti i file binari hello di hello DBMS e/o SAP. Poiché marzo 2015, questo disco può essere di dimensioni anziché precedenti restrizioni che è limitato too1TB too127GB.
* Uno o più dischi hello DBMS contenente file di log del database SAP hello ed i file di log hello di hello area di archiviazione temporanea di DBMS (se hello DBMS è supportata). Se i requisiti di IOPS hello database log sono elevati, è necessario toostripe più dischi nel volume di ordine tooreach hello IOPS richiesto.
* Un numero di dischi che contengono uno o due file di database del database SAP hello e anche file di dati temporanei DBMS hello (se hello DBMS è supportata).

![Configurazione di riferimento di una VM IaaS di Azure per SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd  TODO describe Linux structure  )

- - -
> ![Windows][Logo_Windows] Windows
>
> Con molti clienti adottano configurazioni in cui, ad esempio, i file binari SAP e DBMS non sono stati installati nell'unità c:\ hello in hello sistema operativo è stato installato. Si sono verificati diversi fattori, ma c' toohello radice, in genere è che hello unità avevano una capacità ridotta e aggiornamenti del sistema operativo richiedevano spazio aggiuntivo 10-15 anni fa. Oggi queste condizioni non si verificano quasi più, Oggi è possibile eseguire il mapping unità c:\ hello in macchine virtuali o i dischi dei volumi di grandi dimensioni. Nelle distribuzioni tookeep ordine semplice nella relativa struttura, è consigliabile toofollow il modello di distribuzione seguenti per i sistemi SAP NetWeaver in Azure
>
> file di paging del sistema operativo Windows Hello devono trovarsi in hello unità d: (disco non persistente)
>
> ![Linux][Logo_Linux] Linux
>
> Inserire il file di scambio di hello Linux in /mnt /mnt/Retention/ risorse su Linux, come descritto in [questo articolo][virtual-machines-linux-agent-user-guide]. file di swapping Hello possa essere configurato nel file di configurazione hello di hello /etc/waagent.conf agente Linux. Aggiungere o modificare hello seguenti impostazioni:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

modifiche di hello tooactivate, è necessario toorestart hello agente Linux con

```
sudo service waagent restart
```

Leggere la nota SAP [1597355] per ulteriori dettagli su hello consigliabile dimensioni file di scambio

- - -
il numero di Hello di dischi utilizzato per i file di dati DBMS hello e tipo di hello di questi dischi sono ospitati in archiviazione di Azure deve essere determinato dai requisiti di IOPS hello e latenza hello richiesta. Le quote esatte sono descritte in [questo articolo (Linux)][virtual-machines-sizes-linux] e in [questo articolo (Windows)][virtual-machines-sizes-windows].

Le distribuzioni di SAP su hello ultimi 2 anni di esperienza di invece ci alcune lezioni che possono essere riepilogate come:

* File di dati IOPS traffico toodifferent non è sempre hello stesso poiché i sistemi di clienti esistenti potrebbero disporre in modo diverso dati di dimensioni di file che rappresenta i relativi database SAP. Di conseguenza si è scoperto toobe migliore se si utilizza una configurazione RAID su più file di dati di hello tooplace, dischi che LUN separate dalla quelli. Si sono verificati situazioni, soprattutto con archiviazione di Azure Standard in cui una frequenza IOPS raggiunto la quota hello di un singolo disco sul log delle transazioni DBMS hello. In questi scenari è consigliabile usare hello archiviazione Premium o in alternativa l'aggregazione di archiviazione Standard più dischi con un software RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Procedure consigliate per le prestazioni di SQL Server in Macchine virtuali di Azure][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Configurare RAID software in Linux][virtual-machines-linux-configure-raid]
> * [Configurare LVM in una macchina virtuale Linux in Azure][virtual-machines-linux-configure-lvm]
> * [Segreti dell'archiviazione di Azure e ottimizzazioni I/O di Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* L'archiviazione Premium mostra prestazioni notevolmente migliori, soprattutto per le scritture del log delle transazioni critiche. Per gli scenari SAP di produzione previsto toodeliver come le prestazioni, è consigliabile toouse serie per la macchina virtuale che consentono l'utilizzo di archiviazione Premium di Azure.

Tenere presente tale disco hello contenente hello del sistema operativo, e come si consiglia di hello file binari del database SAP e hello (base VM), non è più limitato too127GB. Ora possibile avere fino too1TB dimensioni. Questo deve essere sufficiente tookeep spazio che tutti hello inclusi i file necessari, ad esempio, i registri dei processi batch SAP.

Per ulteriori suggerimenti e dettagli, in particolare per le macchine virtuali DBMS, consultare hello [Guida alla distribuzione di DBMS][dbms-guide]

#### <a name="disk-handling"></a>Gestione del disco
Nella maggior parte degli scenari è necessario toocreate dischi aggiuntivi nel database di ordine toodeploy hello SAP in VM hello. Abbiamo parlato delle considerazioni hello sul numero di dischi nel capitolo [struttura disco della macchina virtuale o per le distribuzioni SAP] [ planning-guide-5.5.1] di questo documento. portale di Azure Hello consente tooattach e scollegare i dischi dopo aver distribuita una macchina virtuale di base. Hello dischi possono essere collegati e rimossi indipendentemente hello VM sia attivo e in esecuzione e quando è stato arrestato. Quando si collega un disco, hello portale di Azure offre tooattach un disco vuoto o un disco esistente che in questo momento non è collegato tooanother macchina virtuale.

**Nota**: dischi possono essere solo tooone collegato macchina virtuale in qualsiasi momento.

![Collegare e scollegare dischi con l'archiviazione standard di Azure][planning-guide-figure-1400]

Durante la distribuzione di hello di una nuova macchina virtuale, è possibile decidere se i dischi gestiti toouse oppure collocare i dischi in account di archiviazione Azure. Se si desidera toouse archiviazione Premium, è consigliabile utilizzare dischi gestiti.

Successivamente, è necessario toodecide se si desidera toocreate un disco nuovo e vuoto o se si desidera tooselect un disco esistente che è stato caricato in precedenza e deve essere associata a questo punto toohello macchina virtuale.

**IMPORTANTE**: si **non** desidera toouse memorizzazione nella cache Host con l'archiviazione di Azure Standard. È consigliabile lasciare preferenze Cache dell'Host hello hello valore predefinito NONE. Con archiviazione Premium di Azure è necessario abilitare la memorizzazione nella cache di lettura se caratteristiche dei / o hello è di lettura per lo più come tipico traffico dei / o sui file di dati di database. Nel caso dei file di log delle transazioni del database, la memorizzazione nella cache non è consigliata.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Funzionamento dei dischi nel portale di Azure hello tooattach un tipo di dati][virtual-machines-linux-attach-disk-portal]
>
> Se sono collegati dischi, è necessario toolog in hello tooopen VM toohello Gestione disco di Windows. Se il montaggio automatico non è abilitato come consigliato nel capitolo [impostazione del montaggio automatico per i dischi collegati][planning-guide-5.5.3], volume appena collegato hello deve toobe portato online e inizializzato.
>
> ![Linux][Logo_Linux] Linux
>
> Se sono collegati dischi, è necessario toolog in toohello VM e inizializzare i dischi di hello, come descritto in [in questo articolo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Se il nuovo disco hello è un disco vuoto, è necessario anche su disco hello tooformat. Per la formattazione, soprattutto per DBMS, file di dati e log hello stesse raccomandazioni fornite per le distribuzioni bare metal di hello a che DBMS si applicano.

Come già accennato nel capitolo [hello concetto di macchina virtuale di Microsoft Azure][planning-guide-3.2], un account di archiviazione di Azure non fornisce risorse infinite in termini di volume dei / o, IOPS e volume di dati. In genere le macchine virtuali DBMS sono quelle più interessate dal problema. Se si dispone di alcuni toodeploy macchine virtuali di volume elevato dei / o in ordine toostay entro il limite di hello di hello volume di Account di archiviazione di Azure potrebbe essere migliore toouse un Account di archiviazione separato per ogni macchina virtuale. In caso contrario, è necessario toosee come bilanciare queste macchine virtuali tra diversi account di archiviazione senza raggiungere il limite di hello di ogni singolo Account di archiviazione. Altri dettagli sono riportati in hello [Guida alla distribuzione di DBMS][dbms-guide]. Tenere presenti queste limitazioni anche per le macchine virtuali pure del server applicazioni SAP o per altre macchine virtuali che potrebbero richiedere altri dischi rigidi virtuali. Queste restrizioni non sono applicabili se si utilizza un disco gestito. Se si prevede di toouse archiviazione Premium, è consigliabile usare dischi gestiti.

Un altro argomento rilevante per gli account di archiviazione è se ottengono hello dischi rigidi virtuali in un Account di archiviazione replicata geograficamente. La replica geografica è abilitata o disabilitata su hello a livello di Account di archiviazione e non su hello livello macchina virtuale. Se è abilitata la replica geografica, dischi rigidi virtuali hello in Account di archiviazione verranno replicato in un altro data center di Azure all'interno di hello hello stessa area. Prima di decidere su questo, è necessario considerare hello restrizione seguente:

Replica geografica di Azure funziona a livello locale in ogni disco rigido virtuale in una macchina virtuale e non vengono replicate IOs hello in ordine cronologico tra più dischi rigidi virtuali in una macchina virtuale. Pertanto, hello disco rigido virtuale che rappresenta hello macchina virtuale di base, nonché qualsiasi toohello di dischi rigidi virtuali collegati VM aggiuntiva vengono replicate indipendenti tra loro. Ciò significa che non vi è alcuna sincronizzazione tra le modifiche hello hello diversi dischi rigidi virtuali. Hello fatto che hello IOs vengono replicate in modo indipendente da ordine hello in cui vengono scritti significa che la replica geografica non è valida per i server di database i cui database distribuiti su più dischi rigidi virtuali. In aggiunta toohello DBMS, potrebbero esserci altre applicazioni in cui i processi scrivono o modificare i dati in diversi dischi rigidi virtuali e in cui l'ordine di hello tookeep importante delle modifiche. Se questo è un requisito, la replica geografica in Azure non dovrebbe essere abilitata. Se si deve o si vuole usare la replica geografica solo in determinati set di macchine virtuali, è possibile suddividere le macchine virtuali e i dischi rigidi virtuali correlati in account di archiviazione diversi con replica geografica abilitata o disabilitata.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Impostazione del montaggio automatico per dischi collegati
- - -
> ![Windows][Logo_Windows] Windows
>
> Per le macchine virtuali che vengono create da immagini o dischi personali, è necessario toocheck e possibilmente impostare il parametro di montaggio automatico hello. Impostazione di questo parametro consente hello VM dopo un riavvio o una ridistribuzione in Azure toomount hello collegate/montate unità automaticamente.
> il parametro Hello è impostato per le immagini di hello fornite da Microsoft in hello Azure Marketplace.
>
> In ordine tooset hello automount, controllare la documentazione di hello di hello della riga di comando eseguibile diskpart.exe in questo articolo:
>
> * [Opzioni della riga di comando di DiskPart](https://technet.microsoft.com/library/bb490893.aspx)
> * [Montaggio automatico](http://technet.microsoft.com/library/cc753703.aspx)
>
> finestra della riga di comando di Windows Hello deve essere aperta come amministratore.
>
> Se sono collegati dischi, è necessario toolog in hello tooopen VM toohello Gestione disco di Windows. Se il montaggio automatico non è abilitato come consigliato nel capitolo [impostazione del montaggio automatico per i dischi collegati][planning-guide-5.5.3], hello appena collegati volume > deve toobe portato online e inizializzato.
>
> ![Linux][Logo_Linux] Linux
>
> Come descritto in, è necessario un disco vuoto appena collegato tooinitialize [questo articolo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> È inoltre necessario tooadd nuovi dischi toohello /etc/fstab..
>
>

- - -
### <a name="final-deployment"></a>Distribuzione finale
Per hello distribuzione finale e i passaggi effettivi, soprattutto con relativamente toohello distribuzione di SAP Extended Monitoring, vedere toohello [Guida alla distribuzione][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Accesso ai sistemi SAP in esecuzione in macchine virtuali di Azure
Per gli scenari solo Cloud, si potrebbero volere i sistemi SAP toothose tooconnect tra hello usando SAPGUI rete internet pubblica. In questi casi, hello seguenti procedure devono toobe applicato.

Più avanti nel documento hello che si parlerà hello altri scenario principale, la connessione di sistemi tooSAP nelle distribuzioni di più sedi locali che hanno una connessione da sito a sito (tunnel VPN) o connessione Azure ExpressRoute tra sistemi di hello in locale e Azure.

### <a name="remote-access-toosap-systems"></a>Sistemi tooSAP di accesso remoti
Con Gestione risorse di Azure non sono presenti endpoint di predefinito più simile nel modello classico precedente hello. Tutte le porte di una macchina virtuale ARM di Azure sono aperte, purché:

1. Nessun gruppo di sicurezza di rete è definito per la subnet hello o l'interfaccia di rete hello. Il traffico di rete tooAzure macchine virtuali può essere protette tramite i cosiddetti "gruppi di sicurezza rete". Per altre informazioni, vedere [Che cos'è un gruppo di sicurezza di rete][virtual-networks-nsg]
2. Nessun servizio di bilanciamento del carico di Azure viene definito per l'interfaccia di rete hello   

Vedere hello architettura differenza modello classico e ARM, come descritto in [questo articolo][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configurazione di hello connettività sistema SAP e interfaccia utente grafica SAP per scenario solo Cloud
Vedere questo articolo che descrive i dettagli toothis argomento: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Modifica delle impostazioni del firewall all'interno di una macchina virtuale
Potrebbe essere necessario tooconfigure firewall hello tooallow le macchine virtuali sistema SAP tooyour di traffico in ingresso.

- - -
> ![Windows][Logo_Windows] Windows
>
> Per impostazione predefinita, Windows Firewall all'interno di una macchina virtuale distribuita Azure hello è attivata. È ora necessario tooallow hello porta SAP toobe aperto, in caso contrario hello SAPGUI non sarà in grado di tooconnect.
> toodo questo:
>
> * Aprire Pannello di controllo\sistema e sicurezza\windows Firewall too'Advanced impostazioni.
> * Fare clic con il pulsante destro del mouse su Regole connessioni in entrata e scegliere "Nuova regola".
> * In hello guidata seguente scelta toocreate una nuova regola 'Porta'.
> * In hello passaggio successivo della procedura guidata hello lasciare hello impostazione su TCP e digitare il numero di porta hello da tooopen. L'ID dell'istanza SAP è 00, quindi verrà usato 3200. Se l'istanza è un numero diverso di istanza, porta hello è definito in precedenza in base al numero di istanza hello deve essere aperto.
> * Nella parte successiva di hello della procedura guidata hello, è necessario elemento hello tooleave 'Consenti la connessione' selezionata.
> * Nel passaggio successivo di hello della procedura guidata hello toodefine è necessario se si applica la regola hello per rete di dominio, privato e pubblico. Modificarlo se è necessario tooyour necessarie. Tuttavia, la connessione con SAPGUI da hello esterno tramite la rete pubblica hello, è necessario rete pubblica toohello toohave hello regola applicata.
> * In hello ultimo passaggio della procedura guidata hello Nome regola hello e salvare premendo 'Fine'
>
> regola di Hello diventa effettiva immediatamente.
>
> ![Definizione delle regole delle porte][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> le immagini Linux Hello in hello Azure Marketplace non attivano hello iptables firewall per impostazione predefinita e sistema SAP di hello connessione tooyour dovrebbe funzionare. Se è abilitata iptables o un altro firewall, consultare la documentazione di toohello di iptables o tooallow firewall hello utilizzato traffico tcp in ingresso troppo porta 32xx (dove xx rappresenta il numero sistema hello del sistema SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Suggerimenti per la sicurezza
Hello SAPGUI non effettua immediatamente la connessione tooany hello di istanze di SAP (porta 32xx) che sono in esecuzione, ma si connette innanzitutto tramite hello porta aperta toohello SAP messaggio processo server (porta 36xx). In hello oltre hello stessa porta utilizzato dal server messaggi hello per le istanze dell'applicazione toohello hello comunicazioni interne. tooprevent applicazione server locali comunichino accidentalmente con un server in Azure hello interno le porte di comunicazione possono essere modificate. Si consiglia di toochange hello le comunicazioni interne tra il server di messaggistica SAP hello e il relativo numero di porta diverso applicazione tooa istanze nei sistemi clonati da sistemi locali, ad esempio un clone di sviluppo per il progetto di test e così via. Questa operazione può essere eseguita con parametro hello del profilo predefinito:

> rdisp/msserv_internal
>
>

come descritto in [impostazioni di sicurezza per Server di messaggistica SAP hello](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Concetti della distribuzione solo cloud di istanze di SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Scenario di formazione/dimostrativo di una singola VM con SAP NetWeaver
![Sistemi singola macchina virtuale SAP demo con hello stessi nomi di macchina virtuale, isolato in servizi Cloud di Azure][planning-guide-figure-1700]

In questo scenario (vedere il capitolo [solo Cloud] [ planning-guide-2.1] di questo documento) si implementa uno scenario di sistema tipico di formazione/dimostrazione in cui è contenuto uno scenario di formazione/dimostrazione completa di hello in una singola macchina virtuale. Si presuppone che la distribuzione di hello viene eseguita tramite modelli immagine di macchina virtuale. Si presuppone inoltre che più di questi toobe necessità di macchine virtuali di dimostrazione/formazione distribuito con le macchine virtuali con hello hello stesso nome.

il presupposto di Hello è che è stata creata un'immagine di macchina virtuale come descritto nelle sezioni del capitolo [preparazione di macchine virtuali con SAP per Azure] [ planning-guide-5.2] in questo documento.

sequenza di Hello dello scenario di eventi tooimplement hello è simile al seguente:

##### <a name="powershell"></a>PowerShell
* Creare un nuovo gruppo di risorse per ogni scenario di formazione/dimostrativo

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Creare un nuovo account di archiviazione, se non si desidera dischi gestiti toouse

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Creare una nuova rete virtuale per ogni utilizzo di formazione/dimostrazione orizzontale tooenable hello di hello stesso nome host e indirizzi IP. rete virtuale Hello è protetto da un gruppo di sicurezza di rete che consente solo l'accesso traffico tooport 3389 tooenable Desktop remoto e porta 22 per SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Creare un nuovo indirizzo IP pubblico che può essere utilizzato tooaccess hello macchina virtuale hello internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Creare una nuova interfaccia di rete per la macchina virtuale hello

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Creare una macchina virtuale. Per uno scenario solo Cloud hello ogni macchina virtuale avrà hello stesso nome. SID di SAP delle istanze di tali macchine virtuali saranno di SAP NetWeaver hello Hello hello nonché stesso. All'interno di hello il gruppo di risorse di Azure, il nome di hello di hello VM deve toobe univoco, ma in diversi gruppi di risorse di Azure è possibile eseguire le macchine virtuali con hello stesso nome. account 'Administrator' predefinito di Windows Hello o 'root' per Linux non sono validi. Pertanto, un nuovo nome utente amministratore deve toobe definito con una password. dimensioni Hello di hello VM devono inoltre toobe definito.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Facoltativamente, aggiungere altri dischi e ripristinare il contenuto necessario. Tenere presente che tutti i nomi di blob (URL toohello BLOB) devono essere univoci in Azure.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Hello seguente esempio di codice utilizzabile in Linux. Per Windows, uno utilizzare PowerShell come descritto in precedenza o adattare hello esempio toouse % rgName % anziché $rgName e impostare hello variabile di ambiente utilizzando il comando di Windows hello *impostare*.

* Creare un nuovo gruppo di risorse per ogni scenario di formazione/dimostrativo

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* Creare un nuovo account di archiviazione.

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* Creare una nuova rete virtuale per ogni utilizzo di formazione/dimostrazione orizzontale tooenable hello di hello stesso nome host e indirizzi IP. rete virtuale Hello è protetto da un gruppo di sicurezza di rete che consente solo l'accesso traffico tooport 3389 tooenable Desktop remoto e porta 22 per SSH.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Creare un nuovo indirizzo IP pubblico che può essere utilizzato tooaccess hello macchina virtuale hello internet

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Creare una nuova interfaccia di rete per la macchina virtuale hello

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* Creare una macchina virtuale. Per uno scenario solo Cloud hello ogni macchina virtuale avrà hello stesso nome. SID di SAP delle istanze di tali macchine virtuali saranno di SAP NetWeaver hello Hello hello nonché stesso. All'interno di hello il gruppo di risorse di Azure, il nome di hello di hello VM deve toobe univoco, ma in diversi gruppi di risorse di Azure è possibile eseguire le macchine virtuali con hello stesso nome. account 'Administrator' predefinito di Windows Hello o 'root' per Linux non sono validi. Pertanto, un nuovo nome utente amministratore deve toobe definito con una password. dimensioni Hello di hello VM devono inoltre toobe definito.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* Facoltativamente, aggiungere altri dischi e ripristinare il contenuto necessario. Tenere presente che tutti i nomi di blob (URL toohello BLOB) devono essere univoci in Azure.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>Modello
È possibile utilizzare i modelli di esempio hello nel repository di azure-Guida introduttiva: modelli hello su github.

* [Macchina virtuale semplice di Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Macchina virtuale semplice di Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Macchina virtuale dall'immagine](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementare un set di macchine virtuali che devono toocommunicate all'interno di Azure
Questo scenario solo Cloud è uno scenario tipico per fini di formazione e dimostrazione in cui hello software che rappresenta uno scenario di dimostrazione/formazione hello suddivisa su più macchine virtuali. Hello diversi componenti installati in hello diverse macchine virtuali è necessario toocommunicate tra loro. Anche in questo scenario non è necessaria alcuna comunicazione di rete locale o scenario cross-premise.

Questo scenario è un'estensione dell'installazione di hello descritta nei capitoli [singola macchina virtuale con SAP NetWeaver scenario di dimostrazione/formazione] [ planning-guide-7.1] di questo documento. In questo caso più macchine virtuali verrà aggiunto il gruppo di risorse esistente tooan. In hello seguente orizzontale training hello di esempio è costituito da un SAP ASCS/SCS VM, una macchina virtuale in esecuzione un sistema DBMS e un'istanza del Server SAP macchina virtuale.

Prima di creare questo scenario è necessario toothink le impostazioni di base come illustrato nello scenario di hello prima.

#### <a name="resource-group-and-virtual-machine-naming"></a>Denominazione dei gruppi di risorse e delle macchine virtuali
Tutti i nomi dei gruppi di risorse devono essere univoci. Sviluppare il proprio schema di denominazione delle risorse, ad esempio `<rg-name`>-suffisso.

nome della macchina virtuale Hello è univoco nel gruppo di risorse hello toobe.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>Impostare la rete per la comunicazione tra hello diverse macchine virtuali
![Set di VM all'interno di una rete virtuale di Azure][planning-guide-figure-1900]

tooprevent conflitti con i cloni di hello stesso scenario di formazione/dimostrazione, è necessario toocreate una rete virtuale di Azure per ogni orizzontale. Risoluzione dei nomi DNS sarà fornita da Azure oppure è possibile configurare il server DNS all'esterno di Azure (non toobe ulteriormente descritte di seguito). In questo scenario non viene configurato alcun DNS personalizzato. Per tutte le macchine virtuali all'interno di una rete virtuale di Azure viene abilitata la comunicazione usando nomi host.

Hello motivi scenari di formazione o demo tooseparate reti virtuali e non solo risorsa gruppi potrebbero essere:

* Hello SAP orizzontale come impostato esigenze proprio AD/OpenLDAP e una parte di toobe Server di dominio alle esigenze di ogni scenario hello.  
* Hello landscape SAP come set di backup include componenti che toowork necessità con indirizzi IP fissi.

Altre informazioni sulle reti virtuali di Azure e come toodefine li è reperibile [questo articolo][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Distribuzione di VM SAP con connettività di rete aziendale (cross-premise)
Si esegue un landscape SAP e si desidera distribuzione hello toodivide tra bare metal per i server DBMS di fascia alta, ambienti locali virtualizzati per livelli dell'applicazione e inferiore a 2 livelli configurato sistemi SAP e IaaS di Azure. presupposto di base Hello è che i sistemi SAP in un landscape SAP necessitano toocommunicate tra loro e con molti altri componenti software distribuiti in hello, indipendenti dalla società modalità di distribuzione. Inoltre dovrebbe esserci differenze introdotte dalla forma distribuzione hello per hello la connessione con SAPGUI o altre interfacce. Queste condizioni possono solo essere soddisfatti quando abbiamo hello locali Active Directory/OpenLDAP ed estesa dei servizi DNS toohello sistemi Azure tramite connettività site-a-sito/più di un sito o connessioni private come Azure ExpressRoute.

In ordine tooget più in background sui dettagli di implementazione hello SAP in Azure, si consiglia di capitolo tooread [distribuzione concetti di rete di istanze di SAP] [ planning-guide-7] di questo documento che spiega alcuni dei concetti di base hello costrutti di Azure e come questi devono essere utilizzati con le applicazioni SAP in Azure.

### <a name="scenario-of-an-sap-landscape"></a>Scenario di un panorama applicativo SAP
Hello scenario tra sedi locali può essere descritto approssimativamente come nei grafici hello seguenti:

![Connettività da sito a sito tra asset locali e di Azure][planning-guide-figure-2100]

scenario di Hello illustrato in precedenza descrive uno scenario in cui hello locale/OpenLDAP di Active Directory e DNS vengono estesi tooAzure. Sul lato locale di hello, un determinato intervallo di indirizzi IP è riservato per ogni sottoscrizione di Azure. verrà assegnato un intervallo di indirizzi IP Hello tooan rete virtuale di Azure su hello lato Azure.

#### <a name="security-considerations"></a>Considerazioni relative alla sicurezza
Hello requisito minimo è hello utilizzo di protocolli di comunicazione protetta, ad esempio SSL/TLS per l'accesso al browser o connessioni basate su VPN per il sistema accedere toohello Azure servizi. il presupposto di Hello è che le società gestiscano connessione VPN hello tra la rete aziendale e Azure in modo molto diverso. Alcune società possono semplicemente aprire tutte le porte hello. Alcune altre società potrebbe essere necessario toobe molto preciso le porte necessarie tooopen e così via.

Nella tabella hello seguito tipiche di SAP sono elencate le porte di comunicazione. Sostanzialmente, è sufficiente tooopen hello porta gateway SAP.

| Service | Nome della porta | Esempio `<nn`> = 01 | Intervallo predefinito (min-max) | Commento |
| --- | --- | --- | --- | --- |
| Dispatcher |sapdp`<nn>` vedere * |3201 |3200 – 3299 |Dispatcher di SAP, usato dall'interfaccia utente grafica di SAP per Windows e Java |
| Server messaggi |sapms`<sid`> vedere ** |3600 |sapms libero`<anySID`> |sid = SAP-System-ID |
| Gateway |sapgw`<nn`> vedere * |3301 |libero |Gateway SAP, usato per le comunicazioni CPIC e RFC |
| Router SAP |sapdp99 |3299 |libero |Solo i nomi di servizio IC (istanza centrale) possono essere riassegnati in /etc/Services specificando tooan arbitrario valore dopo l'installazione. |

*) nn = numero istanza SAP

**) sid = SAP-System-ID

Informazioni più dettagliate sulle porte necessarie per i diversi prodotti o servizi SAP in base ai prodotti SAP sono disponibili qui: <http://scn.sap.com/docs/DOC-17124>.
Con questo documento dovrebbe essere in grado di tooopen dedicato porte in un dispositivo VPN hello necessaria per gli scenari e i prodotti SAP specifici.

Misure di altri protezione quando la distribuzione di macchine virtuali in tale scenario potrebbe essere toocreate un [Network Security Group] [ virtual-networks-nsg] toodefine le regole di accesso.

### <a name="dealing-with-different-virtual-machine-series"></a>Gestione di serie di macchine virtuali diverse
Nel corso di hello di dodici mesi Microsoft aggiungere molti altri tipi di macchina virtuale che si differenziano in numero di Vcpu, memoria o più importante su hardware in cui viene eseguito. Non tutte queste VM sono supportate con SAP (vedere i tipi di VM supportati nella nota SAP [1928533]). Alcune di queste VM vengono eseguite su generazioni di hardware host diverse, Queste generazioni di hardware host sono distribuite in granularità hello di una Azure unità di scala. Possono verificarsi casi indica dove hello diverse dimensioni di macchina virtuale selezionata non è possibile eseguire su hello stessa unità di scala. Un Set di disponibilità è limitato in hello possibilità toospan che unità di scala basata su hardware diverso.  Per esempio, se si desidera toorun hello DBMS in macchine virtuali A5 A11 e hello livello dell'applicazione SAP nelle macchine virtuali serie G, sarebbe forzato toodeploy un unico sistema SAP o sistemi SAP diversi all'interno di diversi set di disponibilità.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Stampa su una stampante di rete locale dall'istanza SAP in Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Stampa su TCP/IP in uno scenario cross-premise
Configurazione delle stampanti di rete TCP/IP basato su locale in una macchina virtuale di Azure è globale hello uguale a quello della rete aziendale, presupponendo che si dispone di un tunnel VPN Site-To-Site o ExpressRoute connessione stabilita.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo questo:
>
> * Alcune stampanti di rete vengono forniti con una procedura guidata di configurazione che rende facile tooset installazione della stampante in una macchina virtuale di Azure. Se nessun software della procedura guidata è stata distribuita con la modalità "manuale" hello stampante tooset stampante hello è toocreate una nuova porta stampante TCP/IP.
> * Aprire Pannello di controllo -> Dispositivi e stampanti -> Aggiungi stampante
> * Scegliere Aggiungi una stampante usando un nome host o un indirizzo TCP/IP
> * Tipo di indirizzo IP della stampante hello in hello
> * Porta stampante standard 9100
> * Se è necessario installare driver della stampante appropriato hello manualmente.
>
> ![Linux][Logo_Linux] Linux
>
> * ad esempio di Windows appena seguire hello procedura standard tooinstall una stampante di rete
> * è sufficiente seguire hello pubblica Linux le guide per [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) o [Red Hat e Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) sulla tooadd una stampante.
>
>

- - -
![Stampa di rete][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Stampante basata su host su SMB (stampante condivisa) in uno scenario cross-premise
Per impostazione predefinita le stampanti basate su host non sono compatibili con la rete. Ma una stampante basata su host può essere condivise tra i computer in una rete, purché la stampante hello sia connesso tooa computer acceso. Connettere la rete aziendale da sito a sito o con ExpressRoute e condividere la stampante locale. Hello protocollo SMB Usa NetBIOS anziché DNS come nome del servizio. il nome host NetBIOS Hello può essere diverso dal nome host DNS di hello. caso standard Hello è che il nome host NetBIOS hello e il nome host DNS hello siano identici. dominio DNS Hello è inutile nello spazio dei nomi NetBIOS di hello. Di conseguenza, hello costituita da nome host DNS di hello un nome di host DNS completo e il dominio DNS non deve essere utilizzato lo spazio dei nomi NetBIOS hello.

condivisione di stampa Hello è identificata da un nome univoco nella rete hello:

* Nome dell'host SMB hello (sempre necessita).
* Nome della condivisione hello (sempre necessita).
* Nome del dominio hello se la condivisione della stampante non è presente in hello stesso dominio del sistema SAP.
* Inoltre, un nome utente e una password potrebbe essere necessario tooaccess hello stampante condivisa.

Procedura:

- - -
> ![Windows][Logo_Windows] Windows
>
> Condividere la stampante locale.
> In hello macchina virtuale di Azure, aprire Esplora risorse di Windows hello e digitare il nome di condivisione hello della stampante hello.
> Un'installazione guidata stampante verrà semplificato il processo di installazione di hello.
>
> ![Linux][Logo_Linux] Linux
>
> Di seguito sono riportati alcuni esempi di documentazione sulla configurazione delle stampanti di rete in Linux o sull'inclusione di un capitolo relativo alla stampa in Linux. Hello funzionerà esattamente come in una macchina virtuale Linux Azure purché hello macchina virtuale fa parte di una connessione VPN:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL o Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Stampante USB (inoltro stampante)
Capacità di hello Azure di hello Servizi Desktop remoto tooprovide hello accesso dispositivi stampante locale tootheir in una sessione remota non è disponibile.

- - -
> ![Windows][Logo_Windows] Windows
>
> Altri dettagli sulla stampa con Windows sono disponibili qui: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integrazione dei sistemi SAP in Azure in Correction and Transport System (TMS) cross-premise
Modifica SAP e il sistema di trasporto (TMS) tooexport toobe configurato esigenze Hello e importare richieste di trasporto tra i sistemi nel landscape hello. Si presuppone che le istanze di sviluppo hello di un sistema SAP (DEV) si trovano in Azure mentre hello qualità (QA) e i sistemi di produzione (PRD) sono locali. Inoltre, si presuppone che sia presente una directory di trasporto centrale.

##### <a name="configuring-hello-transport-domain"></a>Configurazione di dominio di trasporto hello
Configurare il dominio di trasporto nel sistema di hello è designato come hello Controller di dominio di trasporto, come descritto in [hello configurazione Controller di dominio di trasporto](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Un utente di sistema che TMSADM verrà creato e hello necessario destinazione RFC verrà generato. È possibile verificare queste connessioni RFC utilizzando hello transazione SM59. La risoluzione dei nomi host deve essere abilitata nel dominio di trasporto.

Procedura:

* In questo scenario si è deciso di hello locale sistema QAS sarà controller di dominio di CTS hello. Chiamare la transazione STMS. verrà visualizzata la finestra di dialogo TMS di Hello. Viene visualizzata la finestra di dialogo Configure Transport Domain (questa finestra di dialogo viene visualizzata solo se non è stato ancora configurato un dominio di trasporto).
* Assicurarsi che l'utente creato automaticamente hello TMSADM è autorizzato (SM59 -> ABAP Connection -> TMSADM@E61.DOMAIN_E61 -> dettagli -> Utilities (m) -> Authorization Test). schermata iniziale di Hello della transazione STMS dovrebbe essere indicato che il sistema SAP ora sta funzionando come controller di hello del dominio di trasporto hello come illustrato di seguito:

![Schermata iniziale della transazione STMS sul controller di dominio hello][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Inclusione di sistemi SAP nel dominio di trasporto hello
sequenza di Hello di inclusione di un sistema SAP in un dominio di trasporto è simile al seguente:

* Nel sistema DEV in Azure hello, passare il sistema di trasporto toohello (Client 000) e chiamare la transazione STMS. Scegliere Other Configuration nella finestra di dialogo hello e procedere con Include System in Domain. Specificare hello Controller di dominio come host di destinazione ([tra i sistemi SAP nel dominio di trasporto hello](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). sistema Hello è ora incluso nel dominio di trasporto hello toobe di attesa.
* Per motivi di sicurezza, quindi è toogo toohello indietro domain controller tooconfirm la richiesta. Scegliere System Overview e Approve del sistema in attesa di hello. Confermare quindi hello prompt dei comandi e hello la configurazione verrà distribuita.

Nel sistema SAP ora informazioni hello necessarie hello tutti i sistemi SAP nel dominio di trasporto hello. In hello stesso tempo indirizzi hello dati di sistema SAP di nuovo hello viene inviati tooall hello altri sistemi SAP e hello sistema SAP viene immesso nel profilo di trasporto hello del programma di controllo di trasporto hello. Controllare se RFC e la directory di trasporto toohello accesso del dominio hello di lavoro.

Continuare con la configurazione di hello del sistema di trasporto come al solito come descritto nella documentazione di hello [modifica e sistema di trasporto](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Procedura:

* Assicurarsi che il sistema STMS locale sia configurato correttamente.
* Verificare che nome host hello del Controller di dominio di trasporto hello può essere risolto dalla macchina virtuale in Azure e viceversa.
* Chiamare la transazione STMS -> Other Configuration -> Include System in Domain.
* Verificare la connessione hello in hello sistema TMS locale.
* Configurare le route, i gruppi e i livelli di trasporto, come di consueto.

Nel sito a sito connessi cross-premise scenari, latenza hello tra sedi locali e Azure può essere ancora significativa. Se si seguire hello sequenza di oggetti tramite tooproduction di sistemi di sviluppo e test di trasporto o si pensa di applicare i trasporti o supporto pacchetti toohello diversi sistemi, si tenere presente che, dipende dal percorso di hello di trasporto centrale hello Directory, alcuni dei sistemi di hello verificheranno elevata latenza di lettura o scrittura dei dati nella directory di trasporto centrale hello. situazione Hello è configurazioni del landscape tooSAP simili in cui sono distribuiti i sistemi diversi di hello tramite diversi data center significativamente distanti da hello data center.

In ordine toowork intorno a latenza e sono i sistemi di hello lavoro rapidamente in lettura o scrittura tooor dalla directory di trasporto hello, è possibile configurare due domini di trasporto STMS (uno per on-premise. e uno con i sistemi di hello in domini di trasporto hello Azure e collegamento Verificare la documentazione che descrive i principi di hello alla base di questo concetto nel TMS di SAP hello: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Procedura:

* Configurare un dominio di trasporto in ogni posizione (in locale e in Azure) usando la transazione STMS <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Collegare domini hello con un collegamento di dominio e verificare hello collegamento tra due domini hello.
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* Distribuire hello configurazione toohello collegato sistema.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Traffico RFC tra le istanze SAP in Azure e locali (cross-premise)
Traffico RFC tra i sistemi locali e in Azure deve toowork. tooset la connessione di chiamare la transazione SM59 in un sistema di origine in cui è necessario toodefine una connessione RFC verso il sistema di destinazione hello. configurazione di Hello è simile toohello standard il programma di installazione di una connessione RFC.

Si presuppone che in uno scenario cross-premise hello, quali esecuzione sistemi SAP che devono toocommunicate tra loro presenti macchine virtuali di hello hello nello stesso dominio. Pertanto hello il programma di installazione di una connessione RFC tra sistemi SAP non differiscono dai passaggi di installazione hello e gli input in scenari locali.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Accesso a condivisioni file "locali" da istanze SAP che si trovano in Azure e viceversa
Le istanze SAP residenti in Azure devono tooaccess condivisioni di file disponibili nell'ambiente aziendale hello. Inoltre, le istanze di SAP locale necessario tooaccess condivisioni di file che si trovano in Azure. condivisioni di file hello tooenable è necessario configurare autorizzazioni hello e le opzioni di condivisione nel sistema locale hello. Verificare che tooopen hello le porte su hello VPN o connessione ExpressRoute tra Azure e il Data Center.

## <a name="supportability"></a>Supporto
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Soluzione di monitoraggio di Azure per SAP
Strumenti di monitoraggio, SAPOSCOL, o l'agente Host SAP Ottiene i dati host del servizio di macchina virtuale di Azure hello tramite Azure Monitoring Extension per SAP in ordine tooenable hello monitoraggio dei sistemi SAP cruciali in Azure hello SAP. Poiché hello esigenze di SAP erano tooSAP molto specifiche applicazioni, Microsoft ha deciso di non toogenerically implementano hello necessaria la funzionalità in Azure, ma lasciare il campo per i clienti toodeploy hello necessarie monitoraggio componenti e le configurazioni tootheir Macchine virtuali in esecuzione in Azure. Tuttavia, Gestione distribuzione e del ciclo di vita di monitoraggio dei componenti di hello sarà automatizzata principalmente da Azure.

#### <a name="solution-design"></a>Progettazione della soluzione
soluzione Hello sviluppato tooenable che SAP Monitoring si basa sull'architettura di hello del framework di estensioni e agente VM di Azure. il concetto di Hello di framework agente VM di Azure e l'estensione di hello è tooallow installazione delle applicazioni software disponibili nella raccolta di Azure VM Extension hello all'interno di una macchina virtuale. salve principio idea alla base di questo concetto è tooallow (in casi come Azure Monitoring Extension per SAP hello), hello distribuzione di funzionalità speciali in una configurazione macchina virtuale e hello di tale software in fase di distribuzione.

Hello 'Agente VM di Azure' che consente la gestione di specifiche estensioni di macchina virtuale di Azure all'interno di hello che VM, viene inserito nelle macchine virtuali di Windows per impostazione predefinita di creazione della macchina virtuale nel portale di Azure hello. In caso di SUSE, Red Hat o Oracle Linux, l'agente VM hello fa già parte dell'immagine di Azure Marketplace. Nel caso in cui uno potrebbe caricare una VM Linux da agente della macchina virtuale locale tooAzure hello è toobe installato manualmente.

Hello blocchi predefiniti di base della soluzione di monitoraggio hello in Azure per SAP è simile al seguente:

![Componenti dell'estensione di Microsoft Azure][planning-guide-figure-2400]

Come illustrato nel diagramma a blocchi hello precedente, una parte della soluzione di monitoraggio per SAP hello è ospitata in hello immagine di macchina virtuale di Azure e raccolta di estensioni di Azure che è un archivio replicato globalmente è gestito da operazioni di Azure. È responsabilità di hello del team SAP/MS comune hello lavorando hello Azure implementazione di SAP toowork con le nuove versioni toopublish operazioni di Azure di hello Azure Monitoring Extension per SAP.

Quando si distribuisce una nuova macchina virtuale di Windows, hello 'Agente di macchine Virtuali di Azure' viene automaticamente aggiunta in hello macchina virtuale. funzione Hello dell'agente è hello toocoordinate durante il caricamento e la configurazione di hello Azure estensioni per il monitoraggio dei sistemi SAP NetWeaver. Per le macchine virtuali Linux hello agente VM di Azure fa già parte dell'immagine del sistema operativo di Azure Marketplace hello.

Tuttavia, è un passaggio che deve comunque eseguite dal cliente hello toobe. Questo è l'abilitazione di hello e la configurazione di raccolta prestazioni hello. il processo di Hello correlato toohello 'configuration' è automatizzato mediante uno script di PowerShell o un comando CLI. Hello script di PowerShell può essere scaricato in Microsoft Azure Script Center hello come descritto in hello [Guida alla distribuzione][deployment-guide].

Hello architettura complessiva di hello soluzione Azure monitoring per SAP è simile a:

![Soluzione di monitoraggio di Azure per SAP NetWeaver][planning-guide-figure-2500]

**Per hello esatta procedura-tooand per i passaggi dettagliati dell'utilizzo di questi cmdlet di PowerShell o il comando CLI durante le distribuzioni, seguire le istruzioni di hello all'hello [Guida alla distribuzione][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integrazione di un'istanza SAP ubicata in Azure in SAProuter
Le istanze di SAP in esecuzione in Azure necessario toobe accessibili da SAProuter anche.

![Connessione di rete SAP-router][planning-guide-figure-2600]

SAProuter abilita la comunicazione TCP/IP hello tra i sistemi partecipanti se non c'è alcuna connessione IP diretta. Questo offre il vantaggio di hello che nessuna connessione end-to-end tra i partner di comunicazione hello è necessaria il livello di rete. Hello SAProuter è in ascolto sulla porta 3299 per impostazione predefinita.
istanze tooconnect SAP tramite SAProuter è necessario toogive hello stringa SAProuter e il nome host con qualsiasi tooconnect tentativo.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Fino a questo punto lo stato attivo hello del documento hello è stata SAP NetWeaver in generale o hello stack ABAP di SAP NetWeaver. In questa piccola sezione sono elencate le considerazioni specifiche per lo stack Java di SAP hello. Uno dei più importante applicazioni basate esclusivamente su Java di SAP NetWeaver hello è hello SAP Enterprise Portal. Applicazioni basate su altri SAP NetWeaver come SAP PI e SAP Solution Manager utilizzare hello ABAP di SAP NetWeaver e stack Java. Di conseguenza, sono certamente è una necessità tooconsider aspetti specifici toohello correlati Java di SAP NetWeaver stack anche.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
configurazione di Hello di un portale di SAP in una macchina virtuale di Azure è diversa da un'installazione locale in se si distribuisce in scenari di cross-premise. Poiché hello che DNS viene effettuata in locale, impostazioni della porta hello di singole istanze hello possono essere eseguite come locale configurato. suggerimenti di Hello e le restrizioni descritte in questo documento fino a questo punto si applicano per un'applicazione come SAP Enterprise Portal o stack Java di SAP NetWeaver hello in generale.

![SAP Portal esposto][planning-guide-figure-2700]

Uno scenario di distribuzione speciale da alcuni clienti è l'esposizione diretta di hello di hello SAP Enterprise Portal toohello Internet mentre host macchina virtuale hello è rete aziendale toohello connesso tramite il tunnel VPN site-to-site o ExpressRoute. Per tale scenario, è necessario toomake verificare che determinate porte siano aperte e non sia bloccato da firewall o gruppo di sicurezza. Hello stesso meccanismo sarebbe necessario toobe applicate quando si desidera tooconnect tooan Java di SAP istanza locale in uno scenario solo Cloud.

Hello URI iniziale del portale è http (s):`<Portalserver`>: 5XX00/irj in cui la porta hello è formata da 50000 più (Systemnumber × 100). Hello predefinito portale URI del sistema SAP 00 è `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Per altri dettagli, vedere <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Configurazione dell'endpoint][planning-guide-figure-2800]

Se si desidera toocustomize hello URL e/o porte di SAP Enterprise Portal, verificare la documentazione:

* [Modificare l'URL del portale](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Modificare i numeri di porta predefiniti e i numeri di porta del portale](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Disponibilità elevata e ripristino di emergenza per SAP NetWeaver in esecuzione in macchine virtuali di Azure
### <a name="definition-of-terminologies"></a>Definizione dei termini
il termine Hello **disponibilità elevata (HA)** è in genere correlato tooa set di tecnologie che riduce al minimo le interruzioni IT fornendo la continuità aziendale dei servizi IT tramite ridondanti e a tolleranza di errore o failover protetti i componenti all'interno di hello **stesso** centro dati. Nel caso di questo documento, all'interno di un'unica area di Azure.

Anche il **ripristino di emergenza** ha la funzione di ridurre al minimo le interruzioni dei servizi IT e il relativo ripristino, ma tra data center **diversi**, in genere ubicati a centinaia di chilometri di distanza. In questo caso, in genere tra diverse aree di Azure all'interno di hello stessa regione di natura geopolitica o definito dall'utente come un cliente.

### <a name="overview-of-high-availability"></a>Panoramica della disponibilità elevata
È possibile separare discussione hello su disponibilità elevata SAP in Azure in due parti:

* **Disponibilità elevata dell'infrastruttura di Azure**, relativa, ad esempio, al calcolo (VM), alla rete, all'archiviazione e così via e i relativi vantaggi associati all'aumento della disponibilità delle applicazioni SAP.
* **Disponibilità elevata delle applicazioni SAP**, relativa, ad esempio, ai componenti software SAP:
  * Server applicazioni SAP
  * Istanza di SAP ASCS/SCS
  * Server di database

e al modo in cui è possibile combinarli con la disponibilità elevata dell'infrastruttura di Azure.

Disponibilità elevata di SAP in Azure è tooSAP alcune differenze rispetto ad alta disponibilità in un ambiente locale, fisico o virtuale. il documento seguente di SAP Hello descrive standard configurazioni a disponibilità elevata di SAP in ambienti virtualizzati in Windows: <http://scn.sap.com/docs/DOC-44415>. In Linux non è disponibile alcuna configurazione a disponibilità elevata di SAP integrata in SAPinst come quella disponibile per Windows. Altre informazioni sulla disponibilità elevata di SAP in locale per Linux sono disponibili qui: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Disponibilità elevata dell'infrastruttura di Azure
Al momento è previsto un contratto di servizio a singola VM del 99,9%. tooget un'idea, come disponibilità hello di una singola macchina virtuale potrebbe essere ad esempio, è possibile semplicemente compilare prodotto hello di hello diversi contratti di servizio Azure disponibile: <https://azure.microsoft.com/support/legal/sla/>.

base Hello hello calcolo è 30 giorni al mese o 43200 minuti. Di conseguenza, i tempi di inattività dello 0,05% corrisponde too21.6 minuti. Come al solito, la disponibilità di hello dei diversi servizi hello verrà multiply nel seguente modo hello:

(Disponibilità servizio n. 1/100) * (Disponibilità servizio n. 2/100) + (Disponibilità servizio n. 3/100) *…

Ad esempio:

(99,95/100) + (99,9/100) + (99,9/100) = 0,9975 o una disponibilità complessiva del 99,75%.

#### <a name="virtual-machine-vm-high-availability"></a>Disponibilità elevata delle macchine virtuali
Esistono due tipi di eventi della piattaforma Azure che possono influire sulla disponibilità hello delle macchine virtuali: pianificate di manutenzione non pianificata e manutenzione.

* Gli eventi di manutenzione pianificata sono gli aggiornamenti periodici eseguiti dalle toohello Microsoft sottostante tooimprove piattaforma Azure l'affidabilità complessive, prestazioni e protezione dell'infrastruttura della piattaforma hello le macchine virtuali eseguite in.
* Quando si è verificato un errore hardware hello o infrastruttura fisica sottostante la macchina virtuale in qualche modo, si verificano eventi di manutenzione non pianificata. Può trattarsi, ad esempio, di errori della rete locale, guasti di un disco locale o altri errori a livello di rack. Quando viene rilevato un errore di questo tipo, hello piattaforma Azure eseguirà automaticamente la migrazione della macchina virtuale dal server fisico con hello danneggiato che ospita il server fisico integro macchina virtuale tooa. Tali eventi sono rari, ma potrebbero anche essere tooreboot la macchina virtuale.

Per altri dettagli, vedere questo documento: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Ridondanza di Archiviazione di Azure
dati Hello nell'Account di archiviazione di Microsoft Azure sono sempre replicati tooensure durabilità e disponibilità elevata, riunione hello contratto di servizio di archiviazione Azure, anche in faccia hello di errori hardware temporanei.

Poiché l'archiviazione di Azure è mantenendo tre immagini dei dati di hello per impostazione predefinita, RAID5 o RAID1 tra più dischi di Azure non sono necessari.

Per altri dettagli, vedere questo articolo: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Utilizzo di riavvio della macchina virtuale dell'infrastruttura Azure tooAchieve "Disponibilità" di applicazioni SAP
Se si decide di non toouse funzionalità, ad esempio Windows Server Failover Clustering (WSFC) o Pacemaker in Linux (attualmente supportata solo per SLES 12 e successive), il riavvio di macchina virtuale di Azure è tooprotect utilizzato un sistema SAP tempi di inattività pianificati e di hello Infrastruttura di Azure server fisico e complessiva della piattaforma Azure sottostante.

> [!NOTE]
> È importante toomention che principalmente riavvio della macchina virtuale Azure protegge le macchine virtuali e non applicazioni. Il riavvio delle VM non offre una disponibilità elevata per le applicazioni SAP, ma offre un certo livello di disponibilità dell'infrastruttura e quindi, indirettamente, una "disponibilità più elevata" dei sistemi SAP. Non è inoltre disponibile alcun contratto di servizio per volta hello che richiederà toorestart una macchina virtuale dopo un'interruzione dell'alimentazione pianificato o host. Questo metodo di "disponibilità elevata", quindi, non è adatto per i componenti fondamentali di un sistema SAP come (A)SCS o DBMS.
>
>

Un altro elemento importante dell'infrastruttura per la disponibilità elevata è l'archiviazione. Ad esempio, il contratto di servizio di archiviazione di Azure prevede una disponibilità del 99,9%. Se si effettua la distribuzione di tutte le VM con i relativi dischi in un singolo account di archiviazione di Azure, la potenziale indisponibilità di Archiviazione di Azure causerà l'indisponibilità di tutte le VM presenti in tale account di archiviazione di Azure e anche di tutti i componenti SAP in esecuzione all'interno di tali VM.  

Anziché inserire tutte le VM virtuali in un singolo account di archiviazione di Azure, è possibile anche usare account di archiviazione dedicati per ogni VM e, in questo modo, aumentare la disponibilità complessiva delle VM e delle applicazioni SAP usando più account di archiviazione di Azure indipendenti.

I dischi di Azure gestiti vengono inseriti automaticamente nella hello dominio di errore della macchina virtuale hello che sono collegati. Se si inseriscono due macchine virtuali in un disponibilità impostare e utilizzare dischi gestiti, piattaforma hello si occuperà di distribuzione di dischi gestiti hello in diversi domini di errore anche. Se si prevede di toouse archiviazione Premium, è consigliabile anche mediante gestione di dischi.

Un'architettura di esempio di un sistema SAP NetWeaver che usa la disponibilità elevata dell'infrastruttura di Azure e gli account di archiviazione potrebbe avere un aspetto simile al seguente:

![Utilizzo dell'infrastruttura di Azure a disponibilità elevata tooachieve SAP "higher" della disponibilità dell'applicazione][planning-guide-figure-2900]

Un'architettura di esempio di un sistema SAP NetWeaver che usa la disponibilità elevata dell'infrastruttura di Azure e i Managed Disks potrebbe avere un aspetto simile al seguente:

![Utilizzo dell'infrastruttura di Azure a disponibilità elevata tooachieve SAP "higher" della disponibilità dell'applicazione][planning-guide-figure-2901]

Per i componenti SAP critici ottenuta hello seguendo finora:

* Disponibilità elevata di server applicazioni SAP

  Le istanze dei server applicazioni SAP sono componenti ridondanti. Ogni istanza dei server applicazioni SAP viene distribuita nella relativa macchina virtuale, che è in esecuzione in un dominio di errore e di aggiornamento di Azure diverso (vedere i capitoli [Domini di errore][planning-guide-3.2.1] e [Domini di aggiornamento][planning-guide-3.2.2]). Ciò è garantito dall'uso dei set di disponibilità di Azure (vedere il capitolo [Set di disponibilità di Azure][planning-guide-3.2.3]). La potenziale indisponibilità pianificata o non pianificata di un dominio di errore o di aggiornamento di Azure causerà l'indisponibilità di un numero limitato di VM con le relative istanze dei server applicazioni SAP.

  Ogni istanza dei server applicazioni SAP è posizionata nel relativo account di archiviazione di Azure; la potenziale indisponibilità di un account di archiviazione di Azure causerà l'indisponibilità di una sola VM con la relativa istanza dei server applicazioni SAP. Tenere presente, tuttavia, che esiste un limite al numero di account di archiviazione di Azure che è possibile avere all'interno di una sottoscrizione di Azure. avvio automatico di tooensure dell'istanza (A) SCS dopo hello VM riavvio, assicurarsi tooset hello Autostart-parametro nell'istanza (A) SCS avviare profilo descritto nei capitoli [con avvio automatico per le istanze di SAP] [ planning-guide-11.5].
  Leggere anche il capitolo [Disponibilità elevata per i server applicazioni SAP][planning-guide-11.4.1] per maggiori informazioni.

  Anche se si utilizzano i Managed Disks, i dischi vengono archiviati anche sull’account di archiviazione di Azure e possono essere non disponibili in caso di disservizio della risorsa di archiviazione.

* *più elevata* dell'istanza di SAP (A)SCS

  Qui è utilizzare riavvio della macchina virtuale Azure tooprotect hello VM con l'istanza di SAP (A) SCS installata. In server hello maiuscole/minuscole del tempo di inattività pianificato o di Azure, le macchine virtuali verranno riavviate in un altro server disponibile. Come accennato in precedenza, principalmente riavvio della macchina virtuale Azure protegge le macchine virtuali e non le applicazioni, in questo caso hello istanza (A) SCS. Tramite hello riavvio della macchina virtuale ti contatteremo ai recapiti indirettamente "disponibilità" dell'istanza di SAP (A) SCS. avvio automatico di tooinsure dell'istanza (A) SCS dopo hello VM riavvio, assicurarsi tooset Autostart-parametro nell'istanza (A) SCS avviare profilo descritto nei capitoli da [con avvio automatico per le istanze di SAP][planning-guide-11.5]. Ciò significa hello (A) SCS istanza come un singolo punto di errore (SPOF) in esecuzione in una singola macchina virtuale sarà fattore determinante di hello per la disponibilità dell'intero landscape SAP di hello hello.

* *più elevata* del server DBMS

  In questo caso, istanza di SAP (A) SCS toohello simile caso d'uso, è utilizzare riavvio della macchina virtuale Azure tooprotect hello VM con software installato di DBMS e otteniamo "disponibilità" del software DBMS tramite riavvio della macchina virtuale.
  DBMS in esecuzione in una singola macchina virtuale è anche un SPOF, ed è il fattore determinante di hello per la disponibilità dell'intero landscape SAP di hello hello.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Disponibilità elevata delle applicazioni SAP su IaaS di Azure
tooachieve completo SAP sistema la disponibilità elevata, è necessario tooprotect componenti di sistema SAP di importanza critica, per esempio ridondanti i server applicazioni SAP e componenti univoci (ad esempio singolo punto di errore) come istanza di SAP (A) SCS e DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Disponibilità elevata per i server applicazioni SAP
Per le istanze server/finestra di dialogo dell'applicazione hello SAP non è necessario toothink su una soluzione di disponibilità specifico. La disponibilità elevata si ottiene semplicemente con la ridondanza che deve quindi essere presente in livelli sufficienti nelle varie macchine virtuali. Deve tutte inserite in hello tooavoid stesso Set di disponibilità di Azure che hello macchine virtuali potrebbero essere aggiornati in hello contemporaneamente durante i tempi di inattività di manutenzione pianificata. funzionalità di base Hello che si basa su diversi aggiornamento e domini di errore all'interno di un'unità di scala di Azure già è stato introdotto nel capitolo [domini di aggiornamento][planning-guide-3.2.2]. I set di disponibilità di Azure sono stati presentati nel capitolo [Set di disponibilità di Azure][planning-guide-3.2.3] di questo documento.

Non esiste alcun numero infinito di domini di errore e di aggiornamento che può essere usato da un set di disponibilità di Azure all'interno di un'unità di scala di Azure. Ciò significa che inserisce un numero di macchine virtuali in un Set di disponibilità, prima o poi più di una macchina virtuale finisce in hello errore stesso o al dominio di aggiornamento.

Distribuzione di alcuni server di applicazioni SAP istanze nelle macchine virtuali di loro dedicati e presupponendo che si è arrivati cinque domini di aggiornamento, hello immagine sintetizzata, alla fine di hello. Numero max Hello effettivo dei domini di errore e di aggiornamento all'interno di un set di disponibilità potrebbe cambiare in futuro hello:

![Disponibilità elevata dei i server applicazioni SAP in Azure][planning-guide-figure-3000]

Per altri dettagli, vedere questo documento: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Disponibilità elevata per l'istanza di SAP (A) SCS hello in Windows
Windows Server Failover Cluster (WSFC) è un'istanza di SAP (A) SCS hello tooprotect soluzione usati di frequente. È anche integrato in SAPinst in forma di un'installazione a "disponibilità elevata". In questo momento hello dell'infrastruttura di Azure non è in grado di tooprovide hello funzionalità tooset backup hello necessario hello di Cluster di Failover di Windows Server come operazione viene eseguita in locale.

A partire da gennaio 2016 piattaforma cloud di Azure hello sistema operativo di Windows hello non fornisce il possibilità hello dell'uso di un volume condiviso cluster in un disco condiviso tra due macchine virtuali di Azure.

Una soluzione valida è tuttavia l'utilizzo di hello del software di terze parti 3rd che fornisce un volume condiviso dalla replica sincrona e trasparente disco che può essere integrata in WSFC. Questo approccio implica che solo nodo cluster attivo hello è in grado di tooaccess uno dei dischi hello copia in un punto nel tempo. A partire da gennaio 2016, questo HA la configurazione è l'istanza di SAP (A) SCS hello tooprotect supportati in Windows del sistema operativo guest nelle macchine virtuali di Azure in combinazione con il software di terze parti 3rd SIOS DataKeeper.

Hello SIOS DataKeeper soluzione garantisce un tooWindows di risorse cluster disco condiviso cluster di Failover mediante l'impiego:

* Un disco rigido virtuale di Azure aggiuntivi collegato tooeach di hello macchine virtuali (VM) in una configurazione Cluster di Windows
* SIOS DataKeeper Cluster Edition in esecuzione in entrambi i nodi delle VM
* Con SIOS DataKeeper Cluster Edition configurato in modo che riflette in modo sincrono contenuto hello di hello aggiuntiva disco rigido virtuale collegato volume dal volume di disco rigido virtuale collegato tooadditional macchine virtuali di origine della macchina virtuale di destinazione.
* SIOS DataKeeper astraendo i volumi locali di origine e destinazione hello e presentazione di tooWindows Cluster di Failover come un singolo disco condiviso.

È possibile trovare tutti i dettagli su come tooinstall un Cluster di Failover di Windows con SIOS DataKeeper e SAP in hello [Clustering istanza di SAP ASCS tramite Windows Server Failover Clustering in Azure con SIOS DataKeeper] [ ha-guide-classic]white paper relativo alle.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Disponibilità elevata per l'istanza di SAP (A) SCS hello in Linux
A partire da dicembre 2015 non è inoltre disponibile alcun disco equivalente tooshared WSFC per le macchine virtuali Linux in Azure. Le soluzioni alternative che usano software di terze parti come SIOS per Windows non sono ancora convalidate per l'esecuzione di SAP su Linux in Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Disponibilità elevata per l'istanza del database SAP hello
Hello SAP DBMS con disponibilità elevata installazione tipica è basato su due macchine virtuali DBMS in cui viene utilizzata la funzionalità a disponibilità elevata DBMS dati tooreplicate hello active DBMS istanza toohello seconda macchina virtuale in un'istanza DBMS passiva.

Funzionalità elevata di ripristino di emergenza e disponibilità per DBMS in generale, nonché specifico DBMS sono descritti in hello [Guida alla distribuzione di DBMS][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>La disponibilità elevata end-to-End per hello completa del sistema SAP
Di seguito sono riportati due esempi di architettura SAP NetWeaver a disponibilità elevata in Azure, uno per Windows e l'altro per Linux.

Non gestiti non solo i dischi: concetti hello, come illustrato di seguito potrebbe essere necessario toobe compromesso un bit quando si distribuiscono molti sistemi SAP e il numero di hello di macchine virtuali distribuite è superiori a limite massimo hello di account di archiviazione per ogni sottoscrizione. In questi casi, i dischi rigidi virtuali delle macchine virtuali è necessario toobe combinati all'interno di un Account di archiviazione. In genere questa operazione viene effettuata combinando i dischi rigidi virtuali delle VM del livello dell'applicazione SAP con sistemi SAP diversi.  Sono stati anche combinati diversi dischi rigidi virtuali delle VM DBMS diverse su sistemi SAP diversi in un account di archiviazione di Azure. In tal modo tenendo presente i limiti IOPS hello di account di archiviazione di Azure (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Disponibilità elevata in Windows
![Architettura a disponibilità elevata dell'applicazione SAP NetWeaver con SQL Server in IaaS di Azure][planning-guide-figure-3200]

Hello seguenti costrutti di Azure viene utilizzato per sistema SAP NetWeaver hello, impatto toominimize da problemi di infrastruttura e l'applicazione di patch host:

* sistema completo Hello viene distribuito in Azure (obbligatorio - livello DBMS (A) SCS istanza e il toorun necessità di livello applicazione completa in hello nello stesso percorso).
* sistema completo di Hello viene eseguito all'interno di una sottoscrizione di Azure (obbligatoria).
* sistema completo di Hello viene eseguito all'interno di una rete virtuale di Azure (obbligatorio).
* separazione di Hello di hello macchine virtuali di un sistema SAP in tre set di disponibilità è possibile anche con tutte le macchine virtuali hello appartenenti toohello stessa rete virtuale.
* Tutte le VM che eseguono istanze di DBMS di un sistema SAP sono incluse in un unico set di disponibilità. Si suppone che siano presenti più VM che eseguono istanze di DBMS per ciascun sistema perché vengono usate le funzionalità di disponibilità elevata dei DBMS nativi, come SQL Server AlwaysOn oppure Oracle Data Guard.
* Tutte le VM che eseguono istanze di DBMS usano il proprio account di archiviazione. File di dati e di log DBMS vengono replicati da un account di archiviazione di tooanother account, archiviazione utilizzando funzioni di disponibilità elevata di DBMS che sincronizza i dati di hello. Mancata disponibilità di un account di archiviazione comporta l'indisponibilità di un nodo del cluster di Windows di SQL, ma non hello intero servizio SQL Server.
* Tutte le VM che eseguono istanze di (A)SCS di un sistema SAP sono incluse in un unico set di disponibilità. Un Cluster di Failover Windows Server (WSFC) è configurato all'interno di tali istanza di macchine virtuali tooprotect hello (A) SCS.
* Tutte le VM che eseguono istanze di (A)SCS usano il proprio account di archiviazione. (A) File di istanza SCS e cartella globale SAP vengono replicati da un account di archiviazione di tooanother account, archiviazione SIOS DataKeeper di replica. Mancata disponibilità di un account di archiviazione verrà causare la non disponibilità di uno (A) SCS Windows nodo del cluster, ma non hello intero servizio (A) SCS.
* TUTTE le macchine virtuali hello, che rappresenta il livello di server delle applicazioni di hello SAP sono in un terzo Set di disponibilità.
* TUTTE le macchine virtuali hello server applicazioni SAP in esecuzione usare il proprio account di archiviazione. Mancata disponibilità di un account di archiviazione comporta l'indisponibilità di un server applicazioni SAP, in cui altri AS SAP continuare toorun.

Figura Hello seguente è illustrato hello che stesso landscape utilizzando dischi gestiti.

![Architettura a disponibilità elevata dell'applicazione SAP NetWeaver con SQL Server in IaaS di Azure][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Disponibilità elevata in Linux
architettura di Hello per SAP a disponibilità elevata in Linux in Azure è fondamentalmente hello uguali a quelli di Windows come descritto in precedenza. Al mese di gennaio 2016, non è ancora disponibile alcuna soluzione SAP (A)SCS a disponibilità elevata in Linux su Azure

Di conseguenza di gennaio 2016 non è possibile ottenere un sistema SAP-Linux-Azure hello disponibilità stesso come un sistema SAP-Windows-Azure a causa di mancante a disponibilità elevata per l'istanza di hello (A) SCS e hello database SAP ASE a istanza singola.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Uso dell'avvio automatico per le istanze di SAP
SAP offerte funzionalità hello le istanze di SAP toostart immediatamente dopo l'avvio di hello di hello del sistema operativo all'interno di hello macchina virtuale. la procedura esatta Hello documentata nell'articolo della Knowledge Base SAP [1909114]. Tuttavia, SAP è non è consigliato toouse hello impostazione più perché è presente alcun controllo in ordine di hello di riavvii di istanza, supponendo che più di una macchina virtuale è stata interessata o più istanze eseguito per ogni macchina virtuale. Presupponendo un tipico scenario di Azure di un'istanza del server applicazioni SAP in caso di una singola macchina virtuale eventualmente recupero riavvio hello e macchina virtuale, hello avvio automatico non è realmente critico e può essere abilitata tramite l'aggiunta di questo parametro:

    Autostart = 1

In hello avviare profilo dell'istanza di hello ABAP SAP e/o Java.

> [!NOTE]
> parametro di avvio automatico di Hello può avere anche alcuni difetti. In modo più dettagliato, i trigger di parametro hello hello inizio di un'istanza di SAP ABAP o Java quando hello correlati viene avviato il servizio di Windows/Linux dell'istanza di hello. È certamente case hello all'avvio del sistema operativo hello. Tuttavia, i riavvii dei servizi SAP sono comuni anche per la funzionalità di gestione del ciclo di vita di SAP come SUM o altri aggiornamenti. Queste funzionalità non sono previsti un toobe istanza riavviato automaticamente in tutte. Di conseguenza, il parametro di avvio automatico hello deve essere disabilitato prima di eseguire tali attività. Hello Autostart parametro inoltre non deve essere utilizzato per le istanze di SAP in cluster, ad esempio ASCS/SCS/CI.
>
>

Maggiori informazioni sull'avvio automatico per le istanze di SAP sono disponibili qui:

* [Avviare/arrestare SAP con l'avvio/l'arresto del server Unix](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Avviare e arrestare gli agenti di gestione di SAP NetWeaver](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Come tooenable automaticamente l'avvio del Database HANA](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Sistemi SAP a 3 livelli di maggiori dimensioni
Gli aspetti di disponibilità elevata delle configurazioni SAP a 3 livelli sono già stati esaminati nelle sezioni precedenti. Ma cosa sui sistemi in cui i requisiti del server DBMS hello sono troppo grandi toohave che si trovano in Azure, ma a livello dell'applicazione hello SAP può essere distribuito in Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Posizione delle configurazioni SAP a 3 livelli
Non è di livello di applicazione hello toosplit supportati stesso o un'applicazione hello e DBMS tra sedi locali e Azure. Un sistema SAP deve essere completamente distribuito in locale OPPURE in Azure. Non è inoltre supportato toohave alcuni dei server applicazioni hello eseguire in locale e altri in Azure. Ovvero hello punto iniziale di discussione hello. È inoltre non supportano i componenti DBMS hello toohave di un sistema SAP e hello a livello di server applicazioni SAP distribuito in due diverse aree di Azure. Ad esempio, DBMS negli Stati Uniti occidentali e il livello dell'applicazione negli Stati Uniti centrali. Motivo per non supportare tali configurazioni è sensibilità latenza hello di hello architettura SAP NetWeaver.

Tuttavia, durante hello data ultimo anno partner center sviluppato aree tooAzure percorsi di condivisione. Questi percorsi di condivisione sono in genere dati di Azure fisico toohello molto vicina Center all'interno di un'area di Azure. Hello breve distanza e connessione delle risorse nel percorso condivisione tramite ExpressRoute hello in Azure può generare una latenza che è minore di 2 ms. In questi casi, è possibile toolocate hello livello DBMS (inclusa l'archiviazione SAN/NAS) in tali una condivisione percorso e il livello dell'applicazione hello SAP in Azure. Al mese di dicembre 2015 non sono disponibili distribuzioni del genere. Tuttavia, diversi clienti con distribuzioni di applicazioni non SAP stanno già usando questi approcci.

### <a name="offline-backup-of-sap-systems"></a>Backup offline di sistemi SAP
Dipende hello configurazione SAP scelta (2 o 3 livelli), si potrebbe essere un tooback necessità backup. contenuto di Hello di macchina virtuale stessa hello più toohave un backup del database hello. Hello correlati DBMS i backup sono previste toobe eseguita con i metodi di database. Una descrizione dettagliata di database diversi hello, è reperibile [DBMS Guida][dbms-guide]. In hello invece, hello dati SAP può eseguire il backup in una modalità offline (includendo anche il contenuto del database hello) come descritto in questa sezione oppure online come descritto nella sezione successiva hello.

backup non in linea Hello fondamentalmente richiederebbe un arresto della macchina virtuale tramite il portale di Azure hello hello e una copia del disco di macchina virtuale di base hello e tutti i dischi collegati toohello macchina virtuale. Ciò consentirà di mantenere un punto di immagine in fase di hello macchina virtuale e dei dischi associati. Si consiglia di backup' toocopy hello' in un altro Account di archiviazione di Azure. Di conseguenza hello procedura descritta nel capitolo [la copia dei dischi tra account di archiviazione di Azure] [ planning-guide-5.4.2] di questo documento verrà applicata.
Oltre all'arresto di hello mediante hello Azure portal uno puoi anche eseguire questa operazione tramite Powershell o CLI come descritto qui: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Potrebbe essere costituiti da un ripristino dello stato dell'eliminazione hello macchina virtuale di base nonché come hello dischi originali di hello di base VM e i dischi montati, ricopiando hello dischi salvato toohello Account di archiviazione o la risorsa gruppo originale per i dischi gestiti e quindi ridistribuire il sistema hello.
In questo articolo viene illustrato un esempio di come tooscript viene eseguito Powershell: <http://www.westerndevs.com/azure-snapshots/>

Verificare che tooinstall una nuova licenza SAP poiché ripristina un backup della macchina virtuale come descritto in precedenza crea una nuova chiave di hardware.

### <a name="online-backup-of-an-sap-system"></a>Backup online di un sistema SAP
Backup di hello DBMS viene eseguito con metodi specifici del DBMS, come descritto in hello [DBMS Guida][dbms-guide].

Altre macchine virtuali all'interno di hello sistema SAP possono essere eseguiti utilizzando la funzionalità di Backup di macchine virtuali di Azure. Backup della macchina virtuale Azure introdotto nelle prime fasi 2015 e nel frattempo è tooback un metodo standard per una macchina virtuale completo in Azure. Backup di Azure consente di archiviare i backup hello in Azure e consente un ripristino di una macchina virtuale.

> [!NOTE]
> A partire da dicembre 2015 utilizzando Backup di VM non mantiene hello VM ID univoco viene utilizzato per SAP licenze. Ciò significa che il ripristino da un backup di macchina virtuale richiede l'installazione di una nuova chiave di licenza SAP come hello ripristinata VM viene considerato toobe una nuova macchina virtuale e non una sostituzione di quello precedente è stato salvato.
>
> ![Windows][Logo_Windows] Windows
>
> In teoria, le macchine virtuali che esecuzione possono essere backup dei database in modo coerente se hello sistema DBMS supporta hello Windows VSS (servizio Copia Shadow del Volume <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >) come, ad esempio, SQL Server esegue.
> Tenere presente, tuttavia, che in base ai backup di VM di Azure, i ripristini temporizzati dei database non sono possibili. Pertanto, si consiglia di tooperform backup dei database con funzionalità DBMS invece di basarsi sui Backup di VM di Azure.
>
> tooget familiarità con Backup di macchine virtuali di Azure, iniziare da qui: <https://docs.microsoft.com/azure/backup/backup-azure-vms>.
>
> Altri valori possibili sono toouse una combinazione di Microsoft Data Protection Manager è installato in una macchina virtuale di Azure e Azure Backup ai database di backup e ripristino. Ulteriori informazioni possono essere reperite qui: <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>.  
>
> ![Linux][Logo_Linux] Linux
>
> Non vi è alcun equivalente tooWindows VSS in Linux. Quindi, è possibile eseguire solo backup coerenti con i file, ma non con l'applicazione. Hello DBMS SAP necessario eseguire il backup utilizzando funzionalità DBMS. Hello file system che include i dati relativi a SAP hello possono essere salvati, ad esempio, utilizzando tar come descritto qui: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure come sito di ripristino di emergenza per panorami applicativi SAP di produzione
Poiché Mid 2014, componenti estensioni toovarious di Hyper-V, System Center e Azure consentono l'utilizzo di hello di Azure come sito di ripristino di emergenza per le macchine virtuali in esecuzione in locale in Hyper-V.

Un blog che riporta in dettaglio come toodeploy questa soluzione è documentato qui: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>.

## <a name="summary"></a>Riepilogo
punti chiave Hello della disponibilità elevata per i sistemi SAP in Azure sono:

* In questo momento, hello punto debole SAP non può essere protetto esattamente hello stesso come può essere eseguita nelle distribuzioni locali. motivo di Hello è che i cluster di dischi condivisi non sono ancora possibile compilare in Azure senza utilizzare software di terze parti 3rd hello.
* Per il livello DBMS hello è necessario toouse funzionalità del sistema DBMS che non si basa sulla tecnologia cluster disco condiviso. Dettagli sono documentati in hello [DBMS Guida][dbms-guide].
* impatto di hello toominimize dei problemi all'interno di domini di errore in hello Azure infrastruttura o host di manutenzione, è consigliabile utilizzare il set di disponibilità di Azure:
  * È consigliabile toohave un Set di disponibilità per livello dell'applicazione SAP hello.
  * È consigliabile toohave una disponibilità separato impostate per il livello di sistema DBMS di SAP hello.
  * Non è consigliabile hello tooapply che set di disponibilità stesso per le macchine virtuali di sistemi SAP diversi.
  * Si consiglia di dischi gestiti di toouse Premium.
* Per scopi di Backup del livello DBMS SAP hello, verificare hello [DBMS Guida][dbms-guide].
* Backup delle istanze di finestra di dialogo SAP non ha molto senso perché è in genere più veloci tooredeploy semplici istanze di dialogo.
* Backup hello macchina virtuale che contiene la directory globale di hello di hello sistema SAP e tutti i profili di hello di istanze diverse di hello, ha senso e deve essere eseguita con Windows Backup o, ad esempio, tar in Linux. Poiché esistono differenze tra Windows Server 2008 (R2) e Windows Server 2012 (R2), che rendono più semplice tooback utilizzando hello versioni più recenti di Windows Server, è consigliabile toorun Windows Server 2012 (R2) come sistema operativo Windows.
