---
title: "disponibilità elevata di macchine virtuali per SAP NetWeaver aaaAzure | Documenti Microsoft"
description: "Guida alle funzionalità di disponibilità elevata per SAP NetWeaver in macchine virtuali di Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="19b51-103">Disponibilità elevata per SAP NetWeaver in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

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

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="19b51-109">Macchine virtuali di Azure è una soluzione di hello per le organizzazioni che necessitano di calcolo, archiviazione e risorse di rete, in tempi minimi senza lunghi cicli di approvvigionamento.</span><span class="sxs-lookup"><span data-stu-id="19b51-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="19b51-110">È possibile utilizzare applicazioni classiche toodeploy di macchine virtuali di Azure come ABAP basate su SAP NetWeaver, Java e uno stack ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="19b51-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="19b51-111">È possibile estendere l'affidabilità e la disponibilità senza risorse locali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="19b51-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="19b51-112">Macchine virtuali di Azure supporta la connettività cross-premise e quindi è possibile integrare Macchine virtuali di Azure nei domini locali, nei cloud privati e nel panorama applicativo del sistema SAP dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="19b51-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="19b51-113">In questo articolo si descrivono i passaggi di hello che è possibile trarre toodeploy sistemi SAP a disponibilità elevata in Azure con modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="19b51-114">Le attività principali che verranno illustrate sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="19b51-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="19b51-115">Trovare hello destra guide di note su SAP e l'installazione, elencate in hello [risorse] [ sap-ha-guide-2] sezione.</span><span class="sxs-lookup"><span data-stu-id="19b51-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="19b51-116">In questo articolo integra la documentazione di installazione di SAP e note su SAP, che sono le risorse primarie hello che consentono di installare e distribuire il software SAP in piattaforme specifiche.</span><span class="sxs-lookup"><span data-stu-id="19b51-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="19b51-117">Differenze di hello tra modello di distribuzione Azure Resource Manager hello e il modello di distribuzione classica Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="19b51-118">Informazioni sulle modalità quorum di Windows Server Failover Clustering, è possibile scegliere modello hello appropriato per la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="19b51-119">Comprendere l'archiviazione condivisa di Windows Server Failover Clustering nei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="19b51-120">Informazioni su come proteggere i componenti singolo punto di errore come avanzate Business dell'applicazione di programmazione (ABAP) SAP Central Services (ASCS) toohelp / SAP Central Services (SCS) e sistemi di gestione di database (DBMS) e i componenti ridondanti quali SAP Server applicazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="19b51-121">Seguire un esempio dettagliato di installazione e configurazione di un sistema SAP a disponibilità elevata in un cluster Windows Server Failover Clustering in Azure usando Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19b51-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="19b51-122">Informazioni su Windows Server Failover Clustering in Azure la toouse necessari passaggi aggiuntivi, ma che non sono necessari in una distribuzione locale.</span><span class="sxs-lookup"><span data-stu-id="19b51-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="19b51-123">toosimplify distribuzione e la configurazione, in questo articolo, utilizziamo hello modelli di gestione risorse SAP a tre livelli a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="19b51-124">modelli di Hello automatizzare la distribuzione di hello tutta l'infrastruttura necessaria per un sistema SAP a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="19b51-125">infrastruttura Hello supporta anche il ridimensionamento di SAP applicazione prestazioni Standard (SAP) del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="19b51-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="19b51-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="19b51-127">Prima di iniziare, assicurarsi che siano soddisfatti i prerequisiti di hello descritti in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="19b51-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="19b51-128">Inoltre, essere toocheck che tutte le risorse elencate in hello [risorse] [ sap-ha-guide-2] sezione.</span><span class="sxs-lookup"><span data-stu-id="19b51-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="19b51-129">In questo articolo vengono usati i modelli di Azure Resource Manager per [SAP NetWeaver a tre livelli](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="19b51-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="19b51-130">Per una panoramica dei modelli, vedere i [modelli di Azure Resource Manager per SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="19b51-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="19b51-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Risorse</span><span class="sxs-lookup"><span data-stu-id="19b51-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="19b51-132">Questi articoli descrivono le distribuzioni SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="19b51-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="19b51-133">[Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="19b51-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="19b51-134">[Distribuzione di Macchine virtuali di Azure per SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="19b51-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="19b51-135">[Distribuzione DBMS di Macchine virtuali di Azure per SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="19b51-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="19b51-136">[Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver (questa guida)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="19b51-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-137">Quando possibile, fornita è toohello un collegamento che fa riferimento la Guida all'installazione SAP (vedere hello [Guide all'installazione di SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="19b51-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="19b51-138">Per i prerequisiti e informazioni sul processo di installazione, hello è un'installazione di SAP NetWeaver hello tooread buona guide con attenzione.</span><span class="sxs-lookup"><span data-stu-id="19b51-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="19b51-139">Questo articolo illustra solo attività specifiche per i sistemi basati su SAP NetWeaver che è possibile usare con Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="19b51-140">Queste note SAP sono correlati toohello argomento SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="19b51-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="19b51-141">Numero della nota</span><span class="sxs-lookup"><span data-stu-id="19b51-141">Note number</span></span> | <span data-ttu-id="19b51-142">Titolo</span><span class="sxs-lookup"><span data-stu-id="19b51-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="19b51-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="19b51-143">[1928533]</span></span> |<span data-ttu-id="19b51-144">Applicazioni SAP in Azure: dimensioni e prodotti supportati</span><span class="sxs-lookup"><span data-stu-id="19b51-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="19b51-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="19b51-145">[2015553]</span></span> |<span data-ttu-id="19b51-146">SAP in Microsoft Azure: prerequisiti per il supporto</span><span class="sxs-lookup"><span data-stu-id="19b51-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="19b51-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="19b51-147">[1999351]</span></span> |<span data-ttu-id="19b51-148">Monitoraggio avanzato di Azure per SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="19b51-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="19b51-149">[2178632]</span></span> |<span data-ttu-id="19b51-150">Metriche chiave del monitoraggio per SAP in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="19b51-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="19b51-151">[1999351]</span></span> |<span data-ttu-id="19b51-152">Virtualizzazione in Windows: monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="19b51-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="19b51-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="19b51-153">[2243692]</span></span> |<span data-ttu-id="19b51-154">Use of Azure Premium SSD Storage for SAP DBMS Instance (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP)</span><span class="sxs-lookup"><span data-stu-id="19b51-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="19b51-155">Altre informazioni su hello [limitazioni delle sottoscrizioni di Azure][azure-subscription-service-limits-subscription], inclusi i limiti predefiniti generali e limitazioni massime.</span><span class="sxs-lookup"><span data-stu-id="19b51-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="19b51-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP a disponibilità elevata con Azure Resource Manager e il modello di distribuzione classica Azure hello</span><span class="sxs-lookup"><span data-stu-id="19b51-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="19b51-157">Hello Azure Resource Manager e i modelli di distribuzione classico di Azure sono diversi in hello seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="19b51-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="19b51-158">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="19b51-158">Resource groups</span></span>
- <span data-ttu-id="19b51-159">Azure interno caricare la dipendenza del servizio di bilanciamento nel gruppo di risorse di Azure hello</span><span class="sxs-lookup"><span data-stu-id="19b51-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="19b51-160">Supporto per scenari di SAP con più SID</span><span class="sxs-lookup"><span data-stu-id="19b51-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="19b51-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="19b51-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="19b51-162">Gestione risorse di Microsoft Azure, è possibile utilizzare risorse gruppi toomanage tutte le risorse dell'applicazione hello nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="19b51-163">Un approccio integrato, in un gruppo di risorse, tutte le risorse sono hello stesso ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="19b51-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="19b51-164">Ad esempio, per cui tutte le risorse vengono create in hello stesso volta e vengono eliminate alla hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="19b51-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="19b51-165">Altre informazioni sui [gruppi di risorse](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="19b51-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="19b51-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno caricare la dipendenza del servizio di bilanciamento nel gruppo di risorse di Azure hello</span><span class="sxs-lookup"><span data-stu-id="19b51-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="19b51-167">Nel modello di distribuzione classica Azure hello, vi è una dipendenza tra il gruppo di servizio cloud hello e di servizio di bilanciamento del carico interno di Azure hello (servizio di bilanciamento del carico di Azure).</span><span class="sxs-lookup"><span data-stu-id="19b51-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="19b51-168">Ogni bilanciamento del carico interno necessita di un gruppo di servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="19b51-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="19b51-169">Gestione risorse di Microsoft Azure, non è necessario un toouse gruppo di risorse di Azure bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="19b51-170">ambiente Hello è più semplice e più flessibile.</span><span class="sxs-lookup"><span data-stu-id="19b51-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="19b51-171">Supporto per scenari di SAP con più SID</span><span class="sxs-lookup"><span data-stu-id="19b51-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="19b51-172">In Azure Resource Manager è possibile installare istanze di ASCS/SCS con più SAP ID (SID).</span><span class="sxs-lookup"><span data-stu-id="19b51-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="19b51-173">Le istanze con più SID sono consentite grazie al supporto di più indirizzi IP per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="19b51-174">toouse hello modello di distribuzione classico di Azure, seguire procedure hello descritte in [SAP NetWeaver in Azure: le istanze di Clustering SAP ASCS/SCS tramite Windows Server Failover Clustering in Azure con SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="19b51-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19b51-175">È consigliabile utilizzare un modello di distribuzione Azure Resource Manager hello per le installazioni di SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="19b51-176">Offre numerosi vantaggi che non sono disponibili nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="19b51-177">Sono disponibili altre informazioni sui [modelli di distribuzione][virtual-machines-azure-resource-manager-architecture-benefits-arm] di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="19b51-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span><span class="sxs-lookup"><span data-stu-id="19b51-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="19b51-179">Windows Server Failover Clustering è foundation hello di un'installazione di SAP ASCS/SCS a disponibilità elevata e di un sistema DBMS in Windows.</span><span class="sxs-lookup"><span data-stu-id="19b51-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="19b51-180">Un cluster di failover è un gruppo di 1 + n server indipendenti (nodi) che interagiscono tra di loro disponibilità hello tooincrease di applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="19b51-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="19b51-181">Se si verifica un errore di nodo, Windows Server Failover Clustering calcola il numero di hello di errori che possono verificarsi durante la gestione di un cluster tooprovide applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="19b51-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="19b51-182">È possibile scegliere da clustering di failover tooachieve modalità quorum diversi.</span><span class="sxs-lookup"><span data-stu-id="19b51-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="19b51-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modalità quorum</span><span class="sxs-lookup"><span data-stu-id="19b51-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="19b51-184">È possibile scegliere tra quattro modalità quorum quando si usa Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="19b51-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="19b51-185">**Maggioranza dei nodi**.</span><span class="sxs-lookup"><span data-stu-id="19b51-185">**Node Majority**.</span></span> <span data-ttu-id="19b51-186">Ogni nodo del cluster hello può votare.</span><span class="sxs-lookup"><span data-stu-id="19b51-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="19b51-187">Hello cluster funziona solo con la maggior parte dei voti, vale a dire con voti hello più della metà.</span><span class="sxs-lookup"><span data-stu-id="19b51-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="19b51-188">È consigliabile scegliere questa opzione per i cluster con un numero dispari di nodi.</span><span class="sxs-lookup"><span data-stu-id="19b51-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="19b51-189">Ad esempio, tre nodi in un cluster di sette nodi possono non riuscire e hello cluster continua non otterrà una maggioranza e continua toorun.</span><span class="sxs-lookup"><span data-stu-id="19b51-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="19b51-190">**Maggioranza dei nodi e dei dischi**.</span><span class="sxs-lookup"><span data-stu-id="19b51-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="19b51-191">Ogni nodo e un disco designato (un disco di controllo) nell'archiviazione cluster hello può votare quando sono disponibili e in comunicazione.</span><span class="sxs-lookup"><span data-stu-id="19b51-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="19b51-192">funzioni di cluster Hello solo con la maggior parte di hello voti, vale a dire con voti hello più della metà.</span><span class="sxs-lookup"><span data-stu-id="19b51-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="19b51-193">Questa modalità ha senso in un ambiente cluster con un numero pari di nodi.</span><span class="sxs-lookup"><span data-stu-id="19b51-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="19b51-194">Se i nodi di metà hello e disco hello sono online, il cluster di hello rimane in uno stato integro.</span><span class="sxs-lookup"><span data-stu-id="19b51-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="19b51-195">**Maggioranza dei nodi e delle condivisioni file**.</span><span class="sxs-lookup"><span data-stu-id="19b51-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="19b51-196">Ogni nodo e crea una condivisione di file designati (una condivisione file di controllo) hello amministratore può votare, indipendentemente dal fatto che siano disponibili nodi hello e condivisione file e in comunicazione.</span><span class="sxs-lookup"><span data-stu-id="19b51-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="19b51-197">funzioni di cluster Hello solo con la maggior parte di hello voti, vale a dire con voti hello più della metà.</span><span class="sxs-lookup"><span data-stu-id="19b51-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="19b51-198">Questa modalità ha senso in un ambiente cluster con un numero pari di nodi.</span><span class="sxs-lookup"><span data-stu-id="19b51-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="19b51-199">È simile toohello nodo e modalità maggioranza dei dischi, ma utilizza una condivisione di file di controllo anziché un disco di controllo.</span><span class="sxs-lookup"><span data-stu-id="19b51-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="19b51-200">Questa modalità è facile tooimplement, ma se condivide file hello stesso non è a disponibilità elevata, potrebbe risultare un singolo punto di errore.</span><span class="sxs-lookup"><span data-stu-id="19b51-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="19b51-201">**Non di maggioranza - solo disco**.</span><span class="sxs-lookup"><span data-stu-id="19b51-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="19b51-202">cluster Hello dispone di un quorum se un nodo è disponibile e in comunicazione con un disco specifico nell'archiviazione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="19b51-203">Solo i nodi di hello inoltre sono in comunicazione con il disco è possono aggiungere cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="19b51-204">Si consiglia di non usare questa modalità.</span><span class="sxs-lookup"><span data-stu-id="19b51-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="19b51-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering locale</span><span class="sxs-lookup"><span data-stu-id="19b51-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="19b51-206">La figura 1 illustra un cluster con due nodi.</span><span class="sxs-lookup"><span data-stu-id="19b51-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="19b51-207">Se hello si verifica un errore di connessione di rete tra i nodi di hello e rimangono entrambi i nodi e in esecuzione, una condivisione di file o disco quorum determina quale nodo continuerà applicazioni e servizi del cluster di tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="19b51-208">nodo Hello con disco quorum toohello di accesso o una condivisione file è nodo hello che assicura che i servizi di continuino.</span><span class="sxs-lookup"><span data-stu-id="19b51-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="19b51-209">Poiché in questo esempio utilizza un cluster a due nodi, utilizziamo hello nodo e modalità quorum maggioranza dei condivisione File.</span><span class="sxs-lookup"><span data-stu-id="19b51-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="19b51-210">Inoltre, Hello nodo e la maggior parte del disco è un'opzione valida.</span><span class="sxs-lookup"><span data-stu-id="19b51-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="19b51-211">In un ambiente di produzione è consigliabile usare un disco quorum.</span><span class="sxs-lookup"><span data-stu-id="19b51-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="19b51-212">È possibile utilizzare l'archiviazione e rete toomake tecnologia di sistema è a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-212">You can use network and storage system technology toomake it highly available.</span></span>

![Figura 1: Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="19b51-214">_**Figura 1:** Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="19b51-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="19b51-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Spazio di archiviazione condiviso</span><span class="sxs-lookup"><span data-stu-id="19b51-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="19b51-216">La figura 1 illustra anche un cluster di archiviazione condiviso a due nodi.</span><span class="sxs-lookup"><span data-stu-id="19b51-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="19b51-217">In un cluster di archiviazione condivisa locale, tutti i nodi cluster hello rilevare archiviazione condivisa.</span><span class="sxs-lookup"><span data-stu-id="19b51-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="19b51-218">Un meccanismo di blocco protegge i dati di hello da eventuali danni.</span><span class="sxs-lookup"><span data-stu-id="19b51-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="19b51-219">Tutti i nodi possono rilevare se si verifica un errore in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="19b51-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="19b51-220">Se un nodo, nodo rimanente hello acquisisce la proprietà delle risorse di archiviazione hello e garantisce la disponibilità dei servizi hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-221">Non sono necessari dischi condivisi per la disponibilità elevata con alcune applicazioni DBMS, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19b51-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="19b51-222">SQL Server Always On consente di replicare i file di dati e di log DBMS da disco locale di hello del disco locale toohello nodo di un cluster di un altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="19b51-223">Configurazione del cluster di Windows hello in tal caso, non è necessario un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="19b51-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="19b51-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Rete e risoluzione dei nomi</span><span class="sxs-lookup"><span data-stu-id="19b51-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="19b51-225">I computer client raggiungono cluster hello su un indirizzo IP virtuale e un nome host virtuale che hello fornisce server DNS.</span><span class="sxs-lookup"><span data-stu-id="19b51-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="19b51-226">Hello nodi in locale e server DNS hello può gestire più indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="19b51-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="19b51-227">In un'installazione tipica si usano due o più connessioni di rete:</span><span class="sxs-lookup"><span data-stu-id="19b51-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="19b51-228">Archiviazione di toohello una connessione dedicata</span><span class="sxs-lookup"><span data-stu-id="19b51-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="19b51-229">Una connessione di rete interne al cluster per heartbeat hello</span><span class="sxs-lookup"><span data-stu-id="19b51-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="19b51-230">Una rete pubblica che i client utilizzino tooconnect toohello cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="19b51-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="19b51-232">Confrontare le distribuzioni di cloud privato o metal toobare, macchine virtuali di Azure richiede passaggi aggiuntivi tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="19b51-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="19b51-233">Quando si crea un disco cluster condiviso, è necessario tooset nomi diversi indirizzi IP e l'host virtuale per l'istanza di SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="19b51-234">In questo articolo è illustrare i concetti chiave e hello toobuild necessari passaggi aggiuntivi un cluster a disponibilità elevata centrale servizi SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="19b51-235">Viene illustrata la modalità tooset dello strumento di terze parti hello SIOS DataKeeper di e come tooconfigure hello Azure interno il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="19b51-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="19b51-236">È possibile utilizzare questi toocreate strumenti un cluster di failover di Windows con una condivisione file di controllo in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso][sap-ha-guide-figure-1001]

<span data-ttu-id="19b51-238">_**Figura 2:** Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso_</span><span class="sxs-lookup"><span data-stu-id="19b51-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="19b51-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco condiviso in Azure con SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="19b51-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="19b51-240">È necessario spazio di archiviazione condiviso del cluster per un'istanza di SAP ASCS/SCS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="19b51-241">Come di settembre 2016, Azure non offre spazio di archiviazione condiviso che è possibile utilizzare toocreate un cluster di archiviazione condivisa.</span><span class="sxs-lookup"><span data-stu-id="19b51-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="19b51-242">È possibile utilizzare il software di terze parti SIOS DataKeeper Cluster Edition toocreate un'archiviazione con mirroring che simula l'archiviazione condivisa cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="19b51-243">Hello soluzione SIOS fornisce la replica di dati sincroni in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="19b51-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="19b51-244">Per creare una risorsa disco condiviso per un cluster, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="19b51-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="19b51-245">Collegare un tooeach aggiuntive Azure disco rigido virtuale (VHD) di hello le macchine virtuali (VM) in una configurazione cluster di Windows.</span><span class="sxs-lookup"><span data-stu-id="19b51-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="19b51-246">Eseguire SIOS DataKeeper Cluster Edition in entrambi i nodi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="19b51-247">Configurare SIOS DataKeeper Cluster Edition in modo speculare contenuto hello del volume di disco rigido virtuale collegato aggiuntivo di hello da hello macchina virtuale toohello aggiuntive disco rigido virtuale collegato volume di origine della macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="19b51-248">SIOS DataKeeper estrae i volumi locali di origine e destinazione hello e quindi li presenta tooWindows Clustering di Failover di Server come un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="19b51-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="19b51-249">Altre informazioni su [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="19b51-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="19b51-251">_**Figura 3:** Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="19b51-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-252">Non sono necessari dischi condivisi per la disponibilità elevata con alcuni prodotti DBMS, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19b51-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="19b51-253">SQL Server Always On consente di replicare i file di dati e di log DBMS da disco locale di hello del disco locale toohello nodo di un cluster di un altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="19b51-254">Configurazione del cluster di Windows hello in questo caso, non è necessario un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="19b51-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="19b51-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Risoluzione dei nomi in Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="19b51-256">piattaforma di cloud di Azure Hello non offre hello opzione tooconfigure indirizzi IP virtuali, ad esempio indirizzi IP mobili.</span><span class="sxs-lookup"><span data-stu-id="19b51-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="19b51-257">È necessario un tooset soluzione alternativa di una virtuale risorsa indirizzo IP tooreach hello cluster nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="19b51-258">Azure offre un servizio di bilanciamento del carico interno nel servizio di bilanciamento del carico di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="19b51-259">Con servizio di bilanciamento del carico interno hello client raggiungono cluster hello tramite indirizzo IP virtuale del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="19b51-260">È necessario bilanciamento del carico interno di hello toodeploy nel gruppo di risorse hello che contiene i nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="19b51-261">Quindi, configurare tutte le necessarie regole di port forwarding con probe hello porte di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="19b51-262">Hello client possono connettersi utilizzando il nome host virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="19b51-263">server DNS Hello risolve l'indirizzo IP del cluster hello e porta handle del bilanciamento del carico interno hello toohello nodo attivo del cluster hello di inoltro.</span><span class="sxs-lookup"><span data-stu-id="19b51-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="19b51-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Disponibilità elevata di SAP NetWeaver nell'infrastruttura distribuita come servizio (IaaS) di Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="19b51-265">tooachieve SAP a disponibilità elevata dell'applicazione, ad esempio per i componenti software SAP, è necessario hello tooprotect seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="19b51-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="19b51-266">Istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-266">SAP Application Server instance</span></span>
* <span data-ttu-id="19b51-267">Istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="19b51-268">Server DBMS</span><span class="sxs-lookup"><span data-stu-id="19b51-268">DBMS server</span></span>

<span data-ttu-id="19b51-269">Per altre informazioni sulla protezione dei componenti SAP in scenari a disponibilità elevata, vedere [Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="19b51-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="19b51-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Server applicazioni SAP a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="19b51-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="19b51-271">In genere non è necessaria una soluzione a disponibilità elevata specifica per le istanze di Server applicazioni SAP e finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="19b51-272">La disponibilità elevata si ottiene tramite la ridondanza e si dovranno configurare più istanze delle finestre di dialogo in istanze diverse di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="19b51-273">È necessario avere almeno due istanze dell'applicazione SAP installate in due istanze di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Server applicazioni SAP a disponibilità elevata][sap-ha-guide-figure-2000]

<span data-ttu-id="19b51-275">_**Figura 4:** Server applicazioni SAP a disponibilità elevata_</span><span class="sxs-lookup"><span data-stu-id="19b51-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="19b51-276">È necessario inserire tutte le macchine virtuali che istanze dell'host Server applicazioni SAP in hello stesso set di disponibilità di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="19b51-277">Un set di disponibilità di Azure assicura che:</span><span class="sxs-lookup"><span data-stu-id="19b51-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="19b51-278">Tutte le macchine virtuali fanno parte di hello nello stesso dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="19b51-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="19b51-279">Un dominio di aggiornamento, ad esempio, assicura che le macchine virtuali hello non sono aggiornate in hello contemporaneamente durante i tempi di inattività di manutenzione pianificata.</span><span class="sxs-lookup"><span data-stu-id="19b51-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="19b51-280">Tutte le macchine virtuali fanno parte di hello stesso dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="19b51-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="19b51-281">Un dominio di errore, ad esempio, rende assicurarsi che le macchine virtuali sono distribuite in modo che nessun singolo punto di errore influisce sulla disponibilità di hello di tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="19b51-282">Per ulteriori informazioni su troppo[gestione hello disponibilità delle macchine virtuali][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="19b51-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="19b51-283">Poiché hello account di archiviazione di Azure è un potenziale singolo punto di errore, è importante toohave almeno due account di archiviazione di Azure, in cui vengono distribuite almeno due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="19b51-284">In un'installazione ideale, i dischi di hello di ogni macchina virtuale che esegue un'istanza della finestra di dialogo SAP sarà distribuiti in un altro account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="19b51-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="19b51-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Istanza di SAP ASCS/SCS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="19b51-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="19b51-286">La figura 5 è un esempio di istanza di SAP ASCS/SCS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-2001]

<span data-ttu-id="19b51-288">_**Figura 5:** Istanza di SAP ASCS/SCS a disponibilità elevata_</span><span class="sxs-lookup"><span data-stu-id="19b51-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="19b51-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Disponibilità elevata dell'istanza di SAP ASCS/SCS con Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="19b51-290">Confrontare le distribuzioni di cloud privato o metal toobare, macchine virtuali di Azure richiede passaggi aggiuntivi tooconfigure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="19b51-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="19b51-291">toobuild un cluster di failover di Windows, è necessario un disco cluster condiviso, più indirizzi IP, diversi nomi host virtuale e un servizio di bilanciamento del carico interno di Azure per il clustering di un'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="19b51-292">Esaminati in dettaglio più avanti in articolo hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-292">We discuss this in more detail later in hello article.</span></span>

![Figura 6: Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="19b51-294">_**Figura 6:** Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="19b51-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="19b51-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Istanza di DBMS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="19b51-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="19b51-296">Hello DBMS è anche un singolo punto di contatto in un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="19b51-297">È necessario tooprotect usando una soluzione a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="19b51-298">Figura 7 illustra una soluzione a disponibilità elevata SQL Server Always On in Azure, con Windows Server Failover Clustering e hello Azure interno il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="19b51-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="19b51-299">SQL Server AlwaysOn replica i file di dati e di log DBMS usando la replica DBMS.</span><span class="sxs-lookup"><span data-stu-id="19b51-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="19b51-300">In questo caso, non necessario dischi condivisi cluster, che semplifica l'installazione intera hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Figura 7: Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn][sap-ha-guide-figure-2003]

<span data-ttu-id="19b51-302">_**Figura 7:** Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn_</span><span class="sxs-lookup"><span data-stu-id="19b51-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="19b51-303">Per ulteriori informazioni sul clustering di SQL Server in Azure utilizzando il modello di distribuzione del hello Azure Resource Manager, vedere gli articoli:</span><span class="sxs-lookup"><span data-stu-id="19b51-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="19b51-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual] (Configurare manualmente un gruppo di disponibilità Always On in macchine virtuali di Azure tramite Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="19b51-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="19b51-305">[Configurare un servizio di bilanciamento del carico interno di Azure per un gruppo di disponibilità AlwaysOn in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="19b51-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="19b51-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Scenari di distribuzione a disponibilità elevata end-to-end</span><span class="sxs-lookup"><span data-stu-id="19b51-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="19b51-307">Scenario di distribuzione usando il modello architetturale 1</span><span class="sxs-lookup"><span data-stu-id="19b51-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="19b51-308">La figura 8 illustra un esempio di architettura a disponibilità elevata SAP NetWeaver in Azure per **un** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="19b51-309">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="19b51-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="19b51-310">Un cluster dedicato viene utilizzato per l'istanza di SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="19b51-311">Un cluster dedicato viene utilizzato per l'istanza DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="19b51-312">Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="19b51-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Modello architetturale 1 a disponibilità elevata di SAP, con cluster dedicato per ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="19b51-314">_**Figura 8:** Modello architetturale 1 a disponibilità elevata di SAP, cluster dedicati per ASCS/SCS e DBMS_</span><span class="sxs-lookup"><span data-stu-id="19b51-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="19b51-315">Scenario di distribuzione usando il modello architetturale 2</span><span class="sxs-lookup"><span data-stu-id="19b51-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="19b51-316">La figura 9 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **un** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="19b51-317">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="19b51-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="19b51-318">Viene utilizzato un cluster dedicato per **entrambi** hello SAP ASCS/SCS di istanza e hello DBMS.</span><span class="sxs-lookup"><span data-stu-id="19b51-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="19b51-319">Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="19b51-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="19b51-321">_**Figura 9:** Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS_</span><span class="sxs-lookup"><span data-stu-id="19b51-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="19b51-322">Scenario di distribuzione usando il modello architetturale 3</span><span class="sxs-lookup"><span data-stu-id="19b51-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="19b51-323">La figura 10 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **due** sistemi SAP, con &lt;SID1&gt; e &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="19b51-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="19b51-324">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="19b51-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="19b51-325">Viene utilizzato un cluster dedicato per **entrambi** istanza hello SAP ASCS/SCS SID1 *e* istanza hello SAP ASCS/SCS SID2 (cluster).</span><span class="sxs-lookup"><span data-stu-id="19b51-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="19b51-326">Un cluster dedicato viene usato per DBMS SID1 e un altro cluster dedicato viene usato per DBMS SID2 (due cluster).</span><span class="sxs-lookup"><span data-stu-id="19b51-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="19b51-327">Le istanze di Server applicazioni SAP per il sistema SAP SID1 hello hanno le proprie macchine virtuali di dedicato.</span><span class="sxs-lookup"><span data-stu-id="19b51-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="19b51-328">Le istanze di Server applicazioni SAP per il sistema SAP SID2 hello hanno le proprie macchine virtuali di dedicato.</span><span class="sxs-lookup"><span data-stu-id="19b51-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="19b51-330">_**Figura 10:** Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="19b51-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="19b51-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparare l'infrastruttura di hello</span><span class="sxs-lookup"><span data-stu-id="19b51-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="19b51-332">Preparare l'infrastruttura di hello per 1 modello dell'architettura</span><span class="sxs-lookup"><span data-stu-id="19b51-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="19b51-333">I modelli di Azure Resource Manager per SAP consentono di semplificare la distribuzione delle risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="19b51-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="19b51-334">modelli a tre livelli di Hello in Gestione risorse di Azure supportano inoltre scenari a disponibilità elevata, ad esempio nel architetturale 1 di modello, che dispone di due cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="19b51-335">Ogni cluster è un singolo punto di guasto SAP per SAP ASCS/SCS e DBMS.</span><span class="sxs-lookup"><span data-stu-id="19b51-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="19b51-336">Ecco dove ottenere i modelli di gestione risorse di Azure per uno scenario di esempio hello che descritti in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="19b51-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="19b51-337">Immagine di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="19b51-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="19b51-338">Immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="19b51-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="19b51-339">infrastruttura di hello tooprepare per architettura modello 1:</span><span class="sxs-lookup"><span data-stu-id="19b51-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="19b51-340">Nel portale di Azure su hello hello **parametri** pannello in hello **SYSTEMAVAILABILITY** , quindi selezionare **a disponibilità elevata**.</span><span class="sxs-lookup"><span data-stu-id="19b51-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="19b51-342">_**Figura 11:** Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP_</span><span class="sxs-lookup"><span data-stu-id="19b51-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="19b51-343">creano modelli di Hello:</span><span class="sxs-lookup"><span data-stu-id="19b51-343">hello templates create:</span></span>

  * <span data-ttu-id="19b51-344">**Macchine virtuali**:</span><span class="sxs-lookup"><span data-stu-id="19b51-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="19b51-345">Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-di-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="19b51-346">Macchine virtuali del cluster ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="19b51-347">Cluster DBMS: <*SIDSistemaSAP*>-db-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="19b51-348">**Schede di rete per tutte le macchine virtuali, con gli indirizzi IP associati**:</span><span class="sxs-lookup"><span data-stu-id="19b51-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="19b51-349"><*SIDSistemaSAP*&gt;-nic-di-&lt;*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="19b51-350"><*SIDSistemaSAP*>-nic-ascs-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="19b51-351"><*SIDSistemaSAP*&gt;-nic-db-&lt;*Numero*></span><span class="sxs-lookup"><span data-stu-id="19b51-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="19b51-352">**Account di archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="19b51-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="19b51-353">**Gruppi di disponibilità** per:</span><span class="sxs-lookup"><span data-stu-id="19b51-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="19b51-354">Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="19b51-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="19b51-355">Macchine virtuali del cluster SAP ASCS/SCS: <*SIDSistemaSAP*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="19b51-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="19b51-356">Macchine virtuali del cluster DBMS: <*SIDSistemaSAP*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="19b51-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="19b51-357">**Servizio di bilanciamento del carico interno di Azure**:</span><span class="sxs-lookup"><span data-stu-id="19b51-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="19b51-358">Con tutte le porte per l'istanza di ASCS/SCS hello e l'indirizzo IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="19b51-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="19b51-359">Con tutte le porte per hello DBMS di SQL Server e l'indirizzo IP <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="19b51-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="19b51-360">**Gruppo di sicurezza di rete**: <*SIDSistemaSAP*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="19b51-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="19b51-361">Con un toohello di porte Remote Desktop Protocol (RDP) esterno aprire <*SAPSystemSID*> macchina virtuale - ascs - 0</span><span class="sxs-lookup"><span data-stu-id="19b51-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-362">Tutti gli indirizzi IP delle schede di rete hello e servizi di bilanciamento del carico interno di Azure sono **dinamica** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="19b51-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="19b51-363">Modificarle troppo**statico** gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="19b51-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="19b51-364">Viene descritto come toodo questo più avanti in articolo hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="19b51-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Distribuire le macchine virtuali con toouse (cross-premise) di connettività di rete aziendale nell'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="19b51-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="19b51-366">Per i sistemi SAP di produzione, distribuire le macchine virtuali di Azure con la [connettività di rete aziendale (cross-premise)][planning-guide-2.2] usando la rete VPN da sito a sito di Azure o Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="19b51-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-367">È possibile usare l'istanza di Rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="19b51-368">subnet e la rete virtuale hello già creati e preparati.</span><span class="sxs-lookup"><span data-stu-id="19b51-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="19b51-369">Nel portale di Azure su hello hello **parametri** pannello in hello **NEWOREXISTINGSUBNET** , quindi selezionare **esistente**.</span><span class="sxs-lookup"><span data-stu-id="19b51-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="19b51-370">In hello **struttura** , aggiungere una stringa completa di hello della rete Azure preparata struttura in cui si prevede toodeploy macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="19b51-371">tooget un elenco di tutte le subnet di rete di Azure, eseguire questo comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="19b51-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="19b51-372">Hello **ID** campo Mostra hello **struttura**.</span><span class="sxs-lookup"><span data-stu-id="19b51-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="19b51-373">un elenco di tutti tooget **struttura** valori, eseguire questo comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="19b51-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="19b51-374">Hello **struttura** simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="19b51-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="19b51-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Distribuire delle istanze di SAP solo cloud a scopo di test e dimostrazione</span><span class="sxs-lookup"><span data-stu-id="19b51-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="19b51-376">È possibile distribuire il sistema SAP a disponibilità elevata in un modello di distribuzione solo cloud.</span><span class="sxs-lookup"><span data-stu-id="19b51-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="19b51-377">Questo tipo di distribuzione è utile soprattutto per i casi d'uso di demo e test.</span><span class="sxs-lookup"><span data-stu-id="19b51-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="19b51-378">Non è adatto per i casi d'uso in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="19b51-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="19b51-379">Nel portale di Azure su hello hello **parametri** pannello in hello **NEWOREXISTINGSUBNET** , quindi selezionare **nuova**.</span><span class="sxs-lookup"><span data-stu-id="19b51-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="19b51-380">Lasciare hello **struttura** campo vuoto.</span><span class="sxs-lookup"><span data-stu-id="19b51-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="19b51-381">Hello SAP Azure Resource Manager modello crea automaticamente hello subnet e rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-382">È inoltre necessario toodeploy almeno uno dedicato macchina virtuale per Active Directory e DNS in hello stessa istanza di rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="19b51-383">modello di Hello non è possibile creare queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="19b51-384">Preparare l'infrastruttura di hello per 2 modello dell'architettura</span><span class="sxs-lookup"><span data-stu-id="19b51-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="19b51-385">È possibile utilizzare questo modello di gestione risorse di Azure per SAP toohelp semplificare la distribuzione delle risorse di infrastruttura necessaria per 2 modello architetturale SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="19b51-386">Ecco dove è possibile ottenere i modelli di Azure Resource Manager per questo scenario di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="19b51-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="19b51-387">Immagine di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="19b51-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="19b51-388">Immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="19b51-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="19b51-389">Preparare l'infrastruttura di hello per 3 dell'architettura di modello</span><span class="sxs-lookup"><span data-stu-id="19b51-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="19b51-390">È possibile preparare l'infrastruttura di hello e configurare SAP per **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="19b51-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="19b51-391">Ad esempio, è possibile aggiungere un'istanza di SAP ASCS/SCS aggiuntiva in una configurazione di cluster *esistente*.</span><span class="sxs-lookup"><span data-stu-id="19b51-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="19b51-392">Per ulteriori informazioni, vedere [configurare un'altra istanza di SAP ASCS/SCS in un toocreate di configurazione di cluster una configurazione di multi-SID di SAP esistente in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="19b51-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="19b51-393">Se si desidera toocreate un nuovo cluster con più SID, è possibile utilizzare multi-SID hello [modelli delle Guide rapide su GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="19b51-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="19b51-394">toocreate un nuovo cluster con più SID, è necessario hello toodeploy tre modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="19b51-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="19b51-395">Modello di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="19b51-396">Modello di database</span><span class="sxs-lookup"><span data-stu-id="19b51-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="19b51-397">Modello dei server applicazioni</span><span class="sxs-lookup"><span data-stu-id="19b51-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="19b51-398">Hello nelle sezioni seguenti sono riportati ulteriori dettagli sui modelli di hello e parametri hello è necessario tooprovide nei modelli di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="19b51-399"><a name="ASCS-SCS-template"></a> Modello di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="19b51-400">modello ASCS/SCS Hello distribuisce due macchine virtuali che è possibile utilizzare un cluster di failover di Windows Server che ospita più istanze ASCS/SCS toocreate.</span><span class="sxs-lookup"><span data-stu-id="19b51-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="19b51-401">tooset un modello multi-SID ASCS/SCS hello, in hello [modello multi-SID ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image], immettere i valori per hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="19b51-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="19b51-402">**Resource Prefix**.</span><span class="sxs-lookup"><span data-stu-id="19b51-402">**Resource Prefix**.</span></span>  <span data-ttu-id="19b51-403">Impostare hello risorse prefisso, tooprefix utilizzate tutte le risorse che vengono create durante la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="19b51-404">Perché le risorse di hello non appartengono a un sistema SAP di tooonly, prefisso hello della risorsa hello non hello SID di un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="19b51-405">prefisso Hello deve essere compreso tra **tre a sei caratteri**.</span><span class="sxs-lookup"><span data-stu-id="19b51-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="19b51-406">**Stack Type**.</span><span class="sxs-lookup"><span data-stu-id="19b51-406">**Stack Type**.</span></span> <span data-ttu-id="19b51-407">Selezionare il tipo di stack hello di hello sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="19b51-408">In base al tipo di stack hello, bilanciamento del carico di Azure con uno (ABAP o Java solo) o due (ABAP + Java) indirizzi IP per ogni sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="19b51-409">**OS Type**.</span><span class="sxs-lookup"><span data-stu-id="19b51-409">**OS Type**.</span></span> <span data-ttu-id="19b51-410">Selezionare il sistema operativo hello delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="19b51-411">**SAP System Count**.</span><span class="sxs-lookup"><span data-stu-id="19b51-411">**SAP System Count**.</span></span> <span data-ttu-id="19b51-412">Selezionare il numero di hello dei sistemi SAP si desidera tooinstall in questo cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="19b51-413">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="19b51-413">**System Availability**.</span></span> <span data-ttu-id="19b51-414">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="19b51-414">Select **HA**.</span></span>
  -  <span data-ttu-id="19b51-415">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="19b51-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="19b51-416">Creare un nuovo utente che può essere utilizzati toosign toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="19b51-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="19b51-417">**New Or Existing Subnet**.</span><span class="sxs-lookup"><span data-stu-id="19b51-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="19b51-418">Impostare se devono essere create una nuova rete virtuale e una nuova subnet o se deve essere usata una subnet esistente.</span><span class="sxs-lookup"><span data-stu-id="19b51-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="19b51-419">Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare **esistente**.</span><span class="sxs-lookup"><span data-stu-id="19b51-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="19b51-420">**Subnet Id**. Impostare ID hello di hello toowhich di subnet hello devono essere connesse le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="19b51-421">Selezionare hello subnet della rete locale ExpressRoute rete virtuale tooconnect hello macchina virtuale tooyour o rete privata virtuale (VPN).</span><span class="sxs-lookup"><span data-stu-id="19b51-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="19b51-422">ID Hello in genere è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="19b51-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="19b51-423">/subscriptions/<*ID sottoscrizione*>/resourceGroups/<*nomegruppo risorse*>/providers/Microsoft.Network/VirtualNetwork/<*nome rete virtuale*>>/subnets/<*nome subnet*></span><span class="sxs-lookup"><span data-stu-id="19b51-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="19b51-424">modello Hello consente di distribuire un'istanza di bilanciamento del carico di Azure, che supporta più sistemi SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="19b51-425">Hello ASCS vengono configurate per numero di istanza 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="19b51-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="19b51-426">Hello SCS vengono configurate per numero di istanza 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="19b51-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="19b51-427">Hello ASCS Enqueue replica Server (Hiamanti) (solo Linux) vengono configurate per numero di istanza 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="19b51-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="19b51-428">Hello SCS Hiamanti (solo Linux) vengono configurate per numero di istanza 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="19b51-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="19b51-429">servizio di bilanciamento del carico Hello contiene 1 (2 per Linux) VIP(s), 1 x VIP per ASCS/SCS e 1 x VIP per Hiamanti (solo Linux).</span><span class="sxs-lookup"><span data-stu-id="19b51-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="19b51-430">Hello elenco seguente sono contenuti tutti bilanciamento del carico (dove x è il numero di hello di hello sistema SAP, ad esempio, 1, 2, 3 e così via) di regole:</span><span class="sxs-lookup"><span data-stu-id="19b51-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="19b51-431">Porte specifiche di Windows per ogni sistema SAP 445, 5985</span><span class="sxs-lookup"><span data-stu-id="19b51-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="19b51-432">Porte ASCS (numero di istanza x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="19b51-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="19b51-433">Porte SCS (numero di istanza x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="19b51-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="19b51-434">Porte ASCS ERS in Linux (numero di istanza x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="19b51-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="19b51-435">Porte SCS ERS in Linux (numero di istanza x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="19b51-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="19b51-436">servizio di bilanciamento del carico Hello è hello toouse configurato porte probe (dove x è il numero di hello di hello sistema SAP, ad esempio, 1, 2, 3 e così via) di seguito:</span><span class="sxs-lookup"><span data-stu-id="19b51-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="19b51-437">Porta probe del servizio di bilanciamento del carico interno ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="19b51-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="19b51-438">Porta probe del servizio di bilanciamento del carico interno ERS (solo Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="19b51-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="19b51-439"><a name="database-template"></a> Modello di database</span><span class="sxs-lookup"><span data-stu-id="19b51-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="19b51-440">Consente di distribuire il modello di database Hello uno o due macchine virtuali che è possibile utilizzare tooinstall hello sistema di gestione di database relazionali (RDBMS) per un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="19b51-441">Ad esempio, se si distribuisce un modello ASCS/SCS per cinque sistemi SAP, è necessario toodeploy questo modello cinque volte.</span><span class="sxs-lookup"><span data-stu-id="19b51-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="19b51-442">tooset un modello multi-SID di hello database, in hello [modello di database multi-SID][sap-templates-3-tier-multisid-db-marketplace-image], immettere i valori per hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="19b51-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="19b51-443">**Sap System Id**. Immettere l'ID sistema SAP di hello del sistema SAP si desidera tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="19b51-444">ID Hello verrà considerato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="19b51-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="19b51-445">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="19b51-445">**Os Type**.</span></span> <span data-ttu-id="19b51-446">Selezionare il sistema operativo hello delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="19b51-447">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="19b51-447">**Dbtype**.</span></span> <span data-ttu-id="19b51-448">Selezionare il tipo di hello del database hello desiderato tooinstall nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="19b51-449">Selezionare **SQL** se si desidera tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19b51-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="19b51-450">Selezionare **HANA** se si prevede di macchine virtuali hello tooinstall SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="19b51-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="19b51-451">Verificare che tipo di sistema operativo corretto di hello tooselect: selezionare **Windows** per SQL, selezionare una distribuzione di Linux per HANA.</span><span class="sxs-lookup"><span data-stu-id="19b51-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="19b51-452">Hello bilanciamento del carico di Azure che toohello connessa le macchine virtuali siano configurati toosupport il tipo di database hello selezionato:</span><span class="sxs-lookup"><span data-stu-id="19b51-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="19b51-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="19b51-453">**SQL**.</span></span> <span data-ttu-id="19b51-454">servizio di bilanciamento del carico Hello sarà la porta 1433 il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="19b51-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="19b51-455">Verificare che toouse questa porta per l'installazione di SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="19b51-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="19b51-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="19b51-456">**HANA**.</span></span> <span data-ttu-id="19b51-457">servizio di bilanciamento del carico Hello sarà il bilanciamento del carico porte 35015 e 35017.</span><span class="sxs-lookup"><span data-stu-id="19b51-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="19b51-458">Verificare che tooinstall SAP HANA con numero di istanza **50**.</span><span class="sxs-lookup"><span data-stu-id="19b51-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="19b51-459">servizio di bilanciamento del carico Hello utilizzerà la porta probe 62550.</span><span class="sxs-lookup"><span data-stu-id="19b51-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="19b51-460">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="19b51-460">**Sap System Size**.</span></span> <span data-ttu-id="19b51-461">Numero di set hello del nuovo sistema SAP hello fornirà.</span><span class="sxs-lookup"><span data-stu-id="19b51-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="19b51-462">Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere al SAP tecnologia Partner o l'integratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="19b51-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="19b51-463">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="19b51-463">**System Availability**.</span></span> <span data-ttu-id="19b51-464">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="19b51-464">Select **HA**.</span></span>
  -  <span data-ttu-id="19b51-465">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="19b51-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="19b51-466">Creare un nuovo utente che può essere utilizzati toosign toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="19b51-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="19b51-467">**Subnet Id**. Immettere hello ID di subnet hello utilizzati durante la distribuzione di hello del modello ASCS/SCS hello, o hello della subnet hello che è stato creato come parte della distribuzione del modello ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="19b51-468"><a name="application-servers-template"></a> Modello dei server applicazioni</span><span class="sxs-lookup"><span data-stu-id="19b51-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="19b51-469">modello di server dell'applicazione Hello distribuisce due o più macchine virtuali che può essere usate come istanze del Server applicazioni SAP per un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="19b51-470">Ad esempio, se si distribuisce un modello ASCS/SCS per cinque sistemi SAP, è necessario toodeploy questo modello cinque volte.</span><span class="sxs-lookup"><span data-stu-id="19b51-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="19b51-471">tooset backup hello server multi-SID modello di applicazione, in hello [modello di applicazione server multi-SID][sap-templates-3-tier-multisid-apps-marketplace-image], immettere i valori per hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="19b51-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="19b51-472">**Sap System Id**. Immettere l'ID sistema SAP di hello del sistema SAP si desidera tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="19b51-473">ID Hello verrà considerato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="19b51-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="19b51-474">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="19b51-474">**Os Type**.</span></span> <span data-ttu-id="19b51-475">Selezionare il sistema operativo hello delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="19b51-476">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="19b51-476">**Sap System Size**.</span></span> <span data-ttu-id="19b51-477">numero di Hello del nuovo sistema SAP hello fornirà.</span><span class="sxs-lookup"><span data-stu-id="19b51-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="19b51-478">Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere al SAP tecnologia Partner o l'integratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="19b51-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="19b51-479">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="19b51-479">**System Availability**.</span></span> <span data-ttu-id="19b51-480">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="19b51-480">Select **HA**.</span></span>
  -  <span data-ttu-id="19b51-481">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="19b51-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="19b51-482">Creare un nuovo utente che può essere utilizzati toosign toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="19b51-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="19b51-483">**Subnet Id**. Immettere hello ID di subnet hello utilizzati durante la distribuzione di hello del modello ASCS/SCS hello, o hello della subnet hello che è stato creato come parte della distribuzione del modello ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="19b51-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="19b51-485">In questo esempio, spazio degli indirizzi di hello di hello rete virtuale di Azure è 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="19b51-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="19b51-486">Esiste una subnet denominata **Subnet**, con un intervallo di indirizzi di 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="19b51-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="19b51-487">Tutte le macchine virtuali e i servizi di bilanciamento del carico interni vengono distribuiti in questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="19b51-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19b51-488">Non apportare alcuna modifica le impostazioni di rete toohello all'interno del sistema operativo guest di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="19b51-489">inclusi indirizzi IP, server DNS e la subnet.</span><span class="sxs-lookup"><span data-stu-id="19b51-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="19b51-490">Configurare tutte le impostazioni di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="19b51-491">il servizio Dynamic Host Configuration Protocol (DHCP) Hello propaga le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="19b51-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="19b51-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Indirizzi IP DNS</span><span class="sxs-lookup"><span data-stu-id="19b51-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="19b51-493">hello tooset necessarie che agli indirizzi IP di DNS, hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="19b51-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="19b51-494">Nel portale di Azure su hello hello **server DNS** pannello, assicurarsi che la rete virtuale **server DNS** impostazione troppo**DNS personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="19b51-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="19b51-495">Selezionare le impostazioni in base al tipo di hello della rete che si dispone.</span><span class="sxs-lookup"><span data-stu-id="19b51-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="19b51-496">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="19b51-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="19b51-497">[Connettività di rete aziendale (cross-premise)][planning-guide-2.2]: aggiungere gli indirizzi IP hello del server DNS locali di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="19b51-498">È possibile estendere locale DNS server toohello macchine virtuali che sono in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="19b51-499">In questo scenario, è possibile aggiungere gli indirizzi IP hello di hello Azure le macchine virtuali in cui viene eseguito il servizio DNS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="19b51-500">[Distribuzione solo cloud][planning-guide-2.1]: distribuire una macchina virtuale supplementare in hello stessa istanza di rete virtuale che funge da un server DNS.</span><span class="sxs-lookup"><span data-stu-id="19b51-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="19b51-501">Aggiungere gli indirizzi IP hello di hello Azure le macchine virtuali che hai configurato il servizio DNS toorun.</span><span class="sxs-lookup"><span data-stu-id="19b51-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Figura 12: Configurare i server DNS per Rete virtuale di Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="19b51-503">_**Figura 12:** Configurare i server DNS per Rete virtuale di Azure_</span><span class="sxs-lookup"><span data-stu-id="19b51-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="19b51-504">Se si modificano gli indirizzi IP hello del server DNS hello, è necessario toorestart hello macchine virtuali di Azure tooapply hello modifica e propagare hello nuovi server.</span><span class="sxs-lookup"><span data-stu-id="19b51-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="19b51-505">In questo esempio, hello servizio DNS viene installato e configurato in tali macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="19b51-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="19b51-506">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-506">Virtual machine role</span></span> | <span data-ttu-id="19b51-507">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-507">Virtual machine host name</span></span> | <span data-ttu-id="19b51-508">Nome scheda di rete</span><span class="sxs-lookup"><span data-stu-id="19b51-508">Network card name</span></span> | <span data-ttu-id="19b51-509">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="19b51-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="19b51-510">Primo server DNS</span><span class="sxs-lookup"><span data-stu-id="19b51-510">First DNS server</span></span> |<span data-ttu-id="19b51-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="19b51-511">domcontr-0</span></span> |<span data-ttu-id="19b51-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="19b51-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="19b51-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="19b51-513">10.0.0.10</span></span> |
| <span data-ttu-id="19b51-514">Secondo server DNS</span><span class="sxs-lookup"><span data-stu-id="19b51-514">Second DNS server</span></span> |<span data-ttu-id="19b51-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="19b51-515">domcontr-1</span></span> |<span data-ttu-id="19b51-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="19b51-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="19b51-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="19b51-517">10.0.0.11</span></span> |

### <span data-ttu-id="19b51-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>I nomi host e indirizzi IP statici per l'istanza cluster di SAP ASCS/SCS hello e istanza in cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="19b51-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="19b51-519">Per una distribuzione locale, sono necessari questi nomi host e indirizzi IP riservati:</span><span class="sxs-lookup"><span data-stu-id="19b51-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="19b51-520">Ruolo nome host virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-520">Virtual host name role</span></span> | <span data-ttu-id="19b51-521">Nome host virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-521">Virtual host name</span></span> | <span data-ttu-id="19b51-522">Indirizzo IP statico virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b51-523">Primo nome host virtuale del cluster SAP ASCS/SCS (per la gestione del cluster)</span><span class="sxs-lookup"><span data-stu-id="19b51-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="19b51-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="19b51-524">pr1-ascs-vir</span></span> |<span data-ttu-id="19b51-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="19b51-525">10.0.0.42</span></span> |
| <span data-ttu-id="19b51-526">Nome host virtuale dell'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="19b51-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="19b51-527">pr1-ascs-sap</span></span> |<span data-ttu-id="19b51-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="19b51-528">10.0.0.43</span></span> |
| <span data-ttu-id="19b51-529">Secondo nome host virtuale del cluster SAP DBMS (gestione del cluster)</span><span class="sxs-lookup"><span data-stu-id="19b51-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="19b51-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="19b51-530">pr1-dbms-vir</span></span> |<span data-ttu-id="19b51-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="19b51-531">10.0.0.32</span></span> |

<span data-ttu-id="19b51-532">Quando si crea il cluster di hello, creare hello nomi host virtuali **pr1-ascs-vir** e **pr1-dbms-vir** e hello associati gli indirizzi IP per la gestione di cluster hello stesso.</span><span class="sxs-lookup"><span data-stu-id="19b51-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="19b51-533">Per informazioni su come toodo questa operazione, vedere [raccogliere i nodi del cluster in una configurazione cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="19b51-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="19b51-534">È possibile creare manualmente hello altri due nomi host virtuale, **pr1-sap ascs** e **pr1-dbms-sap**, e hello associati gli indirizzi IP, sul server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="19b51-535">Hello istanza SAP ASCS/SCS cluster e l'istanza DBMS hello cluster utilizza queste risorse.</span><span class="sxs-lookup"><span data-stu-id="19b51-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="19b51-536">Per informazioni su come toodo questa operazione, vedere [creare un nome host virtuale per un'istanza di SAP ASCS/SCS cluster][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="19b51-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="19b51-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Impostare gli indirizzi IP statici per le macchine virtuali SAP hello</span><span class="sxs-lookup"><span data-stu-id="19b51-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="19b51-538">Dopo aver distribuito hello toouse di macchine virtuali del cluster, è necessario indirizzi IP statici tooset per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="19b51-539">Eseguire questa operazione nella configurazione di rete virtuale di Azure hello e non nel sistema operativo guest di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="19b51-540">Nel portale di Azure hello, selezionare **gruppo di risorse** > **scheda di rete** > **impostazioni** > **indirizzo IP** .</span><span class="sxs-lookup"><span data-stu-id="19b51-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="19b51-541">In hello **gli indirizzi IP** pannello, in **assegnazione**selezionare **statico**.</span><span class="sxs-lookup"><span data-stu-id="19b51-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="19b51-542">In hello **indirizzo IP** , immettere l'indirizzo IP hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="19b51-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="19b51-543">Se si modifica l'indirizzo IP hello hello della scheda di rete, è necessario toorestart hello macchine virtuali di Azure tooapply hello modifica.</span><span class="sxs-lookup"><span data-stu-id="19b51-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Figura 13: Impostare gli indirizzi IP statici per la scheda di rete hello di ogni macchina virtuale][sap-ha-guide-figure-3002]

  <span data-ttu-id="19b51-545">_**Figura 13:** impostare gli indirizzi IP statici per la scheda di rete hello di ogni macchina virtuale_</span><span class="sxs-lookup"><span data-stu-id="19b51-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="19b51-546">Ripetere questo passaggio per tutte le interfacce di rete, ovvero per tutte le macchine virtuali, incluse le macchine virtuali che si desidera toouse per il servizio Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="19b51-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="19b51-547">In questo esempio vengono usate le macchine virtuali e gli indirizzi IP statici seguenti:</span><span class="sxs-lookup"><span data-stu-id="19b51-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="19b51-548">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-548">Virtual machine role</span></span> | <span data-ttu-id="19b51-549">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19b51-549">Virtual machine host name</span></span> | <span data-ttu-id="19b51-550">Nome scheda di rete</span><span class="sxs-lookup"><span data-stu-id="19b51-550">Network card name</span></span> | <span data-ttu-id="19b51-551">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="19b51-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="19b51-552">Prima istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-552">First SAP Application Server instance</span></span> |<span data-ttu-id="19b51-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="19b51-553">pr1-di-0</span></span> |<span data-ttu-id="19b51-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="19b51-554">pr1-nic-di-0</span></span> |<span data-ttu-id="19b51-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="19b51-555">10.0.0.50</span></span> |
| <span data-ttu-id="19b51-556">Seconda istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="19b51-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="19b51-557">pr1-di-1</span></span> |<span data-ttu-id="19b51-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="19b51-558">pr1-nic-di-1</span></span> |<span data-ttu-id="19b51-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="19b51-559">10.0.0.51</span></span> |
| <span data-ttu-id="19b51-560">...</span><span class="sxs-lookup"><span data-stu-id="19b51-560">...</span></span> |<span data-ttu-id="19b51-561">...</span><span class="sxs-lookup"><span data-stu-id="19b51-561">...</span></span> |<span data-ttu-id="19b51-562">...</span><span class="sxs-lookup"><span data-stu-id="19b51-562">...</span></span> |<span data-ttu-id="19b51-563">...</span><span class="sxs-lookup"><span data-stu-id="19b51-563">...</span></span> |
| <span data-ttu-id="19b51-564">Ultima istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="19b51-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="19b51-565">pr1-di-5</span></span> |<span data-ttu-id="19b51-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="19b51-566">pr1-nic-di-5</span></span> |<span data-ttu-id="19b51-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="19b51-567">10.0.0.55</span></span> |
| <span data-ttu-id="19b51-568">Primo nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="19b51-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="19b51-569">pr1-ascs-0</span></span> |<span data-ttu-id="19b51-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="19b51-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="19b51-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="19b51-571">10.0.0.40</span></span> |
| <span data-ttu-id="19b51-572">Secondo nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="19b51-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="19b51-573">pr1-ascs-1</span></span> |<span data-ttu-id="19b51-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="19b51-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="19b51-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="19b51-575">10.0.0.41</span></span> |
| <span data-ttu-id="19b51-576">Primo nodo del cluster per l'istanza di DBMS</span><span class="sxs-lookup"><span data-stu-id="19b51-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="19b51-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="19b51-577">pr1-db-0</span></span> |<span data-ttu-id="19b51-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="19b51-578">pr1-nic-db-0</span></span> |<span data-ttu-id="19b51-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="19b51-579">10.0.0.30</span></span> |
| <span data-ttu-id="19b51-580">Secondo nodo del cluster per l'istanza di DBMS</span><span class="sxs-lookup"><span data-stu-id="19b51-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="19b51-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="19b51-581">pr1-db-1</span></span> |<span data-ttu-id="19b51-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="19b51-582">pr1-nic-db-1</span></span> |<span data-ttu-id="19b51-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="19b51-583">10.0.0.31</span></span> |

### <span data-ttu-id="19b51-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Impostare un indirizzo IP statico per servizio di bilanciamento del carico interno di Azure hello</span><span class="sxs-lookup"><span data-stu-id="19b51-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="19b51-585">modello di gestione risorse di Azure SAP Hello crea un servizio di bilanciamento del carico interno di Azure che viene utilizzato per cluster di istanze di SAP ASCS/SCS hello e cluster DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19b51-586">Hello l'indirizzo IP del nome host virtuale hello hello SAP ASCS/SCS è hello stesso come indirizzo IP hello di bilanciamento del carico interno di SAP ASCS/SCS hello: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="19b51-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="19b51-587">Hello l'indirizzo IP del nome del DBMS è hello virtuale hello hello stesso come indirizzo IP hello di bilanciamento del carico interno DBMS hello: **pr1 lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="19b51-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="19b51-588">un indirizzo IP statico per hello Azure interno tooset bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="19b51-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="19b51-589">Hello distribuzione iniziale Imposta indirizzo IP di bilanciamento del carico interno di hello troppo**dinamica**.</span><span class="sxs-lookup"><span data-stu-id="19b51-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="19b51-590">Nel portale di Azure su hello hello **gli indirizzi IP** pannello, in **assegnazione**selezionare **statico**.</span><span class="sxs-lookup"><span data-stu-id="19b51-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="19b51-591">Impostare l'indirizzo IP hello del bilanciamento del carico interno hello **pr1-lb-ascs** toohello l'indirizzo IP del nome host virtuale hello dell'istanza di SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="19b51-592">Impostare l'indirizzo IP hello del bilanciamento del carico interno hello **pr1 lb-dbms** toohello l'indirizzo IP del nome host virtuale hello dell'istanza DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Nella figura 14: Impostare gli indirizzi IP statici per servizio di bilanciamento del carico interno hello per istanza di SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  <span data-ttu-id="19b51-594">_**Nella figura 14:** impostare gli indirizzi IP statici per servizio di bilanciamento del carico interno hello per istanza di SAP ASCS/SCS hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="19b51-595">Nell'esempio sono presenti due servizi di bilanciamento del carico interno di Azure con questi indirizzi IP statici:</span><span class="sxs-lookup"><span data-stu-id="19b51-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="19b51-596">Ruolo del servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-596">Azure internal load balancer role</span></span> | <span data-ttu-id="19b51-597">Nome del servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-597">Azure internal load balancer name</span></span> | <span data-ttu-id="19b51-598">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="19b51-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b51-599">Servizio di bilanciamento del carico interno dell'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="19b51-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="19b51-600">pr1-lb-ascs</span></span> |<span data-ttu-id="19b51-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="19b51-601">10.0.0.43</span></span> |
| <span data-ttu-id="19b51-602">Servizio di bilanciamento del carico interno di SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="19b51-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="19b51-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="19b51-603">pr1-lb-dbms</span></span> |<span data-ttu-id="19b51-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="19b51-604">10.0.0.33</span></span> |


### <span data-ttu-id="19b51-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico ASCS/SCS predefinito</span><span class="sxs-lookup"><span data-stu-id="19b51-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="19b51-606">modello di gestione risorse di Azure SAP Hello Crea porte hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="19b51-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="19b51-607">Un'istanza di ABAP ASCS, con numero di istanza predefinito hello **00**</span><span class="sxs-lookup"><span data-stu-id="19b51-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="19b51-608">Un'istanza di Java SCS, con numero di istanza predefinito hello **01**</span><span class="sxs-lookup"><span data-stu-id="19b51-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="19b51-609">Quando si installa l'istanza di SAP ASCS/SCS, è necessario utilizzare un numero di istanza predefinito hello **00** per il numero ABAP ASCS hello e di istanza predefinito istanza **01** per l'istanza di Java SCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="19b51-610">Creare quindi richiesto di endpoint per le porte di SAP NetWeaver hello di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="19b51-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="19b51-611">toocreate richiesto endpoint di bilanciamento del carico interno, creare in primo luogo, questi endpoint per le porte di SAP NetWeaver ABAP ASCS hello di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="19b51-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="19b51-612">Servizio/nome regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="19b51-612">Service/load balancing rule name</span></span> | <span data-ttu-id="19b51-613">Numeri porte predefinite</span><span class="sxs-lookup"><span data-stu-id="19b51-613">Default port numbers</span></span> | <span data-ttu-id="19b51-614">Porte concrete per (istanza ASCS con l'istanza numero 00) (ERS con 10)</span><span class="sxs-lookup"><span data-stu-id="19b51-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b51-615">Server di accodamento/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="19b51-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="19b51-616">32<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-617">3200</span><span class="sxs-lookup"><span data-stu-id="19b51-617">3200</span></span> |
| <span data-ttu-id="19b51-618">Server messaggi ABAP/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="19b51-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="19b51-619">36<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-620">3600</span><span class="sxs-lookup"><span data-stu-id="19b51-620">3600</span></span> |
| <span data-ttu-id="19b51-621">Messaggio ABAP interno/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="19b51-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="19b51-622">39<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-623">3900</span><span class="sxs-lookup"><span data-stu-id="19b51-623">3900</span></span> |
| <span data-ttu-id="19b51-624">HTTP server messaggi/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="19b51-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="19b51-625">81<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-626">8100</span><span class="sxs-lookup"><span data-stu-id="19b51-626">8100</span></span> |
| <span data-ttu-id="19b51-627">SAP Start Service ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="19b51-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="19b51-628">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="19b51-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="19b51-629">50013</span><span class="sxs-lookup"><span data-stu-id="19b51-629">50013</span></span> |
| <span data-ttu-id="19b51-630">SAP Start Service ASCS HTTPS/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="19b51-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="19b51-631">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="19b51-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="19b51-632">50014</span><span class="sxs-lookup"><span data-stu-id="19b51-632">50014</span></span> |
| <span data-ttu-id="19b51-633">Replica di accodamento/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="19b51-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="19b51-634">5<*NumeroIstanza*>16</span><span class="sxs-lookup"><span data-stu-id="19b51-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="19b51-635">50016</span><span class="sxs-lookup"><span data-stu-id="19b51-635">50016</span></span> |
| <span data-ttu-id="19b51-636">SAP Start Service ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="19b51-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="19b51-637">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="19b51-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="19b51-638">51013</span><span class="sxs-lookup"><span data-stu-id="19b51-638">51013</span></span> |
| <span data-ttu-id="19b51-639">SAP Start Service ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="19b51-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="19b51-640">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="19b51-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="19b51-641">51014</span><span class="sxs-lookup"><span data-stu-id="19b51-641">51014</span></span> |
| <span data-ttu-id="19b51-642">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="19b51-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="19b51-643">5985</span><span class="sxs-lookup"><span data-stu-id="19b51-643">5985</span></span> |
| <span data-ttu-id="19b51-644">Condivisione file *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="19b51-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="19b51-645">445</span><span class="sxs-lookup"><span data-stu-id="19b51-645">445</span></span> |

<span data-ttu-id="19b51-646">_**Tabella 1:** porta un numero di istanze di SAP NetWeaver ABAP ASCS hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="19b51-647">Quindi, creare questi endpoint per le porte di SAP NetWeaver Java SCS hello di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="19b51-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="19b51-648">Servizio/nome regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="19b51-648">Service/load balancing rule name</span></span> | <span data-ttu-id="19b51-649">Numeri porte predefinite</span><span class="sxs-lookup"><span data-stu-id="19b51-649">Default port numbers</span></span> | <span data-ttu-id="19b51-650">Porte concrete per (istanza SCS con numero di istanza 01) (ERS con 11)</span><span class="sxs-lookup"><span data-stu-id="19b51-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b51-651">Server di accodamento/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="19b51-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="19b51-652">32<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-653">3201</span><span class="sxs-lookup"><span data-stu-id="19b51-653">3201</span></span> |
| <span data-ttu-id="19b51-654">Server gateway/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="19b51-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="19b51-655">33<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-656">3301</span><span class="sxs-lookup"><span data-stu-id="19b51-656">3301</span></span> |
| <span data-ttu-id="19b51-657">Server messaggi Java/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="19b51-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="19b51-658">39<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-659">3901</span><span class="sxs-lookup"><span data-stu-id="19b51-659">3901</span></span> |
| <span data-ttu-id="19b51-660">HTTP server messaggi/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="19b51-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="19b51-661">81<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="19b51-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="19b51-662">8101</span><span class="sxs-lookup"><span data-stu-id="19b51-662">8101</span></span> |
| <span data-ttu-id="19b51-663">SAP Start Service SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="19b51-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="19b51-664">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="19b51-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="19b51-665">50113</span><span class="sxs-lookup"><span data-stu-id="19b51-665">50113</span></span> |
| <span data-ttu-id="19b51-666">SAP Start Service SCS HTTPS/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="19b51-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="19b51-667">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="19b51-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="19b51-668">50114</span><span class="sxs-lookup"><span data-stu-id="19b51-668">50114</span></span> |
| <span data-ttu-id="19b51-669">Replica di accodamento/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="19b51-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="19b51-670">5<*NumeroIstanza*>16</span><span class="sxs-lookup"><span data-stu-id="19b51-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="19b51-671">50116</span><span class="sxs-lookup"><span data-stu-id="19b51-671">50116</span></span> |
| <span data-ttu-id="19b51-672">SAP Start Service ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="19b51-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="19b51-673">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="19b51-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="19b51-674">51113</span><span class="sxs-lookup"><span data-stu-id="19b51-674">51113</span></span> |
| <span data-ttu-id="19b51-675">SAP Start Service ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="19b51-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="19b51-676">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="19b51-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="19b51-677">51114</span><span class="sxs-lookup"><span data-stu-id="19b51-677">51114</span></span> |
| <span data-ttu-id="19b51-678">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="19b51-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="19b51-679">5985</span><span class="sxs-lookup"><span data-stu-id="19b51-679">5985</span></span> |
| <span data-ttu-id="19b51-680">Condivisione file *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="19b51-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="19b51-681">445</span><span class="sxs-lookup"><span data-stu-id="19b51-681">445</span></span> |

<span data-ttu-id="19b51-682">_**Tabella 2:** porta un numero di istanze di SAP NetWeaver Java SCS hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Predefinito ASCS/SCS bilanciamento del carico regole di bilanciamento del carico interno di Azure hello][sap-ha-guide-figure-3004]

<span data-ttu-id="19b51-684">_**Figura 15:** regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico ASCS/SCS predefinito_</span><span class="sxs-lookup"><span data-stu-id="19b51-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="19b51-685">Impostare l'indirizzo IP hello di bilanciamento del carico hello **pr1 lb-dbms** toohello l'indirizzo IP del nome host virtuale hello dell'istanza DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="19b51-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Modificare le regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico di predefinito di hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="19b51-687">Se si desidera numeri diversi toouse per hello SAP ASCS o istanze SCS, è necessario modificare hello nomi e valori delle relative porte dai valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="19b51-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="19b51-688">Nel portale di Azure hello, selezionare  **<* SID*> - lb - ascs caricare bilanciamento * * > **regole di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="19b51-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="19b51-689">Per le regole che appartengono a toohello SAP ASCS o istanza SCS di bilanciamento del carico tutti, è possibile modificare questi valori:</span><span class="sxs-lookup"><span data-stu-id="19b51-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="19b51-690">Nome</span><span class="sxs-lookup"><span data-stu-id="19b51-690">Name</span></span>
  * <span data-ttu-id="19b51-691">Porta</span><span class="sxs-lookup"><span data-stu-id="19b51-691">Port</span></span>
  * <span data-ttu-id="19b51-692">Porta back-end</span><span class="sxs-lookup"><span data-stu-id="19b51-692">Back-end port</span></span>

  <span data-ttu-id="19b51-693">Ad esempio, se si desidera toochange hello predefinito ASCS del numero di istanza da too31 00, è necessario modifiche hello toomake per tutte le porte elencate nella tabella 1.</span><span class="sxs-lookup"><span data-stu-id="19b51-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="19b51-694">Ecco un esempio di aggiornamento per la porta *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="19b51-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Modificare le regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico di predefinito di hello ASCS/SCS][sap-ha-guide-figure-3005]

  <span data-ttu-id="19b51-696">_**Figura 16:** modifica hello ASCS/SCS predefinito bilanciamento carico di regole di bilanciamento del carico interno di Azure hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="19b51-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Aggiungi dominio toohello macchine virtuali di Windows</span><span class="sxs-lookup"><span data-stu-id="19b51-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="19b51-698">Dopo aver assegnato una macchina virtuale toohello di indirizzo IP statico, aggiungere dominio toohello di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19b51-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Figura 17: Aggiungere un dominio tooa macchina virtuale][sap-ha-guide-figure-3006]

<span data-ttu-id="19b51-700">_**Figura 17:** aggiungere un dominio tooa macchina virtuale_</span><span class="sxs-lookup"><span data-stu-id="19b51-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="19b51-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Aggiungere le voci del Registro di sistema in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="19b51-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="19b51-702">Bilanciamento del carico di Azure è un servizio di bilanciamento del carico interno che si chiude le connessioni quando le connessioni hello sono inattive per un determinato periodo di tempo (un timeout di inattività).</span><span class="sxs-lookup"><span data-stu-id="19b51-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="19b51-703">Processi di lavoro SAP nella finestra di dialogo istanze connessioni aperte toohello SAP enqueue elaborare appena hello prima enqueue o dequeue richiesta toobe esigenze inviato.</span><span class="sxs-lookup"><span data-stu-id="19b51-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="19b51-704">Queste connessioni rimangono in genere stabilite finché il processo di lavoro hello o hello enqueue processo viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="19b51-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="19b51-705">Tuttavia, se la connessione hello è inattiva per un determinato periodo di tempo, hello connessioni hello chiude bilanciamento di carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="19b51-706">Ciò non rappresenta un problema perché il processo di lavoro SAP hello ristabilita processo enqueue toohello di hello connessione se non esiste più.</span><span class="sxs-lookup"><span data-stu-id="19b51-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="19b51-707">Queste attività sono documentate nelle tracce di sviluppatore hello dei processi SAP, ma creano una grande quantità di contenuto aggiuntivo in tali tracce.</span><span class="sxs-lookup"><span data-stu-id="19b51-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="19b51-708">È un hello toochange buona TCP/IP `KeepAliveTime` e `KeepAliveInterval` in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="19b51-709">Combinare le modifiche nei parametri TCP/IP hello con parametri di profilo SAP, descritti più avanti nell'articolo di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="19b51-710">le voci del Registro di sistema tooadd in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello, aggiungono innanzitutto queste voci del Registro di sistema di Windows in entrambi i nodi del cluster di Windows per SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="19b51-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="19b51-711">Path</span><span class="sxs-lookup"><span data-stu-id="19b51-711">Path</span></span> | <span data-ttu-id="19b51-712">HKLM\System\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="19b51-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="19b51-713">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="19b51-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="19b51-714">Tipo di variabile</span><span class="sxs-lookup"><span data-stu-id="19b51-714">Variable type</span></span> |<span data-ttu-id="19b51-715">REG_DWORD (decimale)</span><span class="sxs-lookup"><span data-stu-id="19b51-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="19b51-716">Valore</span><span class="sxs-lookup"><span data-stu-id="19b51-716">Value</span></span> |<span data-ttu-id="19b51-717">120000</span><span class="sxs-lookup"><span data-stu-id="19b51-717">120000</span></span> |
| <span data-ttu-id="19b51-718">Collegamento toodocumentation</span><span class="sxs-lookup"><span data-stu-id="19b51-718">Link toodocumentation</span></span> |[<span data-ttu-id="19b51-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="19b51-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="19b51-720">_**Tabella 3:** parametro TCP/IP prima della modifica hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="19b51-721">Aggiungere quindi le voci del Registro di sistema Windows in entrambi i nodi del cluster Windows per SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="19b51-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="19b51-722">Path</span><span class="sxs-lookup"><span data-stu-id="19b51-722">Path</span></span> | <span data-ttu-id="19b51-723">HKLM\System\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="19b51-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="19b51-724">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="19b51-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="19b51-725">Tipo di variabile</span><span class="sxs-lookup"><span data-stu-id="19b51-725">Variable type</span></span> |<span data-ttu-id="19b51-726">REG_DWORD (decimale)</span><span class="sxs-lookup"><span data-stu-id="19b51-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="19b51-727">Valore</span><span class="sxs-lookup"><span data-stu-id="19b51-727">Value</span></span> |<span data-ttu-id="19b51-728">120000</span><span class="sxs-lookup"><span data-stu-id="19b51-728">120000</span></span> |
| <span data-ttu-id="19b51-729">Collegamento toodocumentation</span><span class="sxs-lookup"><span data-stu-id="19b51-729">Link toodocumentation</span></span> |[<span data-ttu-id="19b51-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="19b51-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="19b51-731">_**Tabella 4:** modifica hello secondo TCP/IP parametro_</span><span class="sxs-lookup"><span data-stu-id="19b51-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="19b51-732">**modifiche di hello tooapply, riavviare entrambi i nodi del cluster**.</span><span class="sxs-lookup"><span data-stu-id="19b51-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="19b51-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurare un cluster di Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="19b51-734">La configurazione di un cluster Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="19b51-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="19b51-735">La raccolta di nodi del cluster hello in una configurazione cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="19b51-736">Configurazione di un controllo di condivisione file del cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="19b51-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Raccogliere i nodi del cluster hello in una configurazione cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="19b51-738">Hello Add Role guidata e funzionalità, aggiungere i nodi del cluster tooboth di clustering di failover.</span><span class="sxs-lookup"><span data-stu-id="19b51-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="19b51-739">Configurare il cluster di failover di hello utilizzando Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="19b51-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="19b51-740">In Gestione Cluster di Failover, selezionare **crea Cluster**e quindi aggiungere solo hello nome del cluster prima di hello, il nodo A. Non aggiungere hello secondo nodo. secondo nodo hello verrà aggiunto in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="19b51-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Figura 18: Aggiungere server hello o un nome macchina virtuale del primo nodo del cluster hello][sap-ha-guide-figure-3007]

  <span data-ttu-id="19b51-742">_**Figura 18:** Aggiungi hello server o macchina virtuale il nome del primo nodo del cluster hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="19b51-743">Immettere il nome di rete hello (nome host virtuale) del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Figura 19: Immettere il nome del cluster hello][sap-ha-guide-figure-3008]

  <span data-ttu-id="19b51-745">_**Figura 19:** immettere il nome del cluster hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="19b51-746">Dopo aver creato il cluster hello, eseguire un test di convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Figura 20: Esecuzione del controllo di convalida cluster hello][sap-ha-guide-figure-3009]

  <span data-ttu-id="19b51-748">_**Figura 20:** esecuzione del controllo di convalida cluster hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="19b51-749">È possibile ignorare eventuali avvisi relativi a questo punto i dischi nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="19b51-750">Si aggiungerà che una condivisione file di controllo e hello SIOS dischi condivisi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="19b51-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="19b51-751">In questa fase, non è necessario tooworry sulla presenza di un quorum.</span><span class="sxs-lookup"><span data-stu-id="19b51-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Figura 21: Nessun disco quorum trovato][sap-ha-guide-figure-3010]

  <span data-ttu-id="19b51-753">_**Figura 21:** Nessun disco quorum trovato_</span><span class="sxs-lookup"><span data-stu-id="19b51-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: La risorsa del cluster principale richiede un nuovo indirizzo IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="19b51-755">_**Figura 22:** La risorsa del cluster principale richiede un nuovo indirizzo IP_</span><span class="sxs-lookup"><span data-stu-id="19b51-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="19b51-756">Modificare l'indirizzo IP di hello del servizio cluster di hello core.</span><span class="sxs-lookup"><span data-stu-id="19b51-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="19b51-757">cluster Hello Impossibile avviare finché non si modifica l'indirizzo IP di hello del servizio cluster di hello core, indirizzo IP di hello del server hello punta tooone dei nodi di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="19b51-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="19b51-758">Effettuare questa operazione su hello **proprietà** pagina della risorsa IP del servizio di hello core del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="19b51-759">Ad esempio, è necessario un indirizzo IP tooassign (in questo esempio, **10.0.0.42**) per nome host virtuale del cluster hello **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="19b51-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Nella figura 23: Nella finestra di dialogo Proprietà hello, modificare l'indirizzo IP hello][sap-ha-guide-figure-3012]

  <span data-ttu-id="19b51-761">_**Nella figura 23:** In hello **proprietà** della finestra di dialogo Modifica indirizzo IP di hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Figura 24: Assegnare l'indirizzo IP hello è riservato per il cluster hello][sap-ha-guide-figure-3013]

  <span data-ttu-id="19b51-763">_**Figura 24:** Assegnazione indirizzo IP hello riservata per il cluster hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="19b51-764">Portare hello host virtuale nome del cluster online.</span><span class="sxs-lookup"><span data-stu-id="19b51-764">Bring hello cluster virtual host name online.</span></span>

  ![Figura 25: Servizio di base del Cluster sia attivo e in esecuzione e hello correggere l'indirizzo IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="19b51-766">_**Figura 25:** servizio principale del Cluster sia attivo e in esecuzione e con hello correggere l'indirizzo IP_</span><span class="sxs-lookup"><span data-stu-id="19b51-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="19b51-767">Aggiungere hello secondo nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="19b51-768">Ora che il servizio cluster core hello sia in esecuzione, è possibile aggiungere secondo nodo del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Figura 26: Aggiungere hello secondo nodo del cluster][sap-ha-guide-figure-3015]

  <span data-ttu-id="19b51-770">_**Figura 26:** Aggiungi hello secondo nodo del cluster_</span><span class="sxs-lookup"><span data-stu-id="19b51-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="19b51-771">Immettere un nome per il secondo host di nodo del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-771">Enter a name for hello second cluster node host.</span></span>

  ![Figura 27: Immettere nome host nodo hello secondo cluster][sap-ha-guide-figure-3016]

  <span data-ttu-id="19b51-773">_**Figura 27:** invio hello secondo host nome del nodo cluster_</span><span class="sxs-lookup"><span data-stu-id="19b51-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19b51-774">Assicurarsi che hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster** casella di controllo è **non** selezionato.</span><span class="sxs-lookup"><span data-stu-id="19b51-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: Non selezionare la casella di controllo hello][sap-ha-guide-figure-3017]

  <span data-ttu-id="19b51-776">_**Figura 28:** si **non** selezionare hello casella di controllo_</span><span class="sxs-lookup"><span data-stu-id="19b51-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="19b51-777">È possibile ignorare gli avvisi relativi al quorum e ai dischi.</span><span class="sxs-lookup"><span data-stu-id="19b51-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="19b51-778">Si imposteranno hello quorum e condivisione hello disco in un secondo momento, come descritto in [installazione SIOS DataKeeper Cluster Edition per la condivisione del disco del cluster di SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="19b51-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorare gli avvisi sul quorum disco hello][sap-ha-guide-figure-3018]

  <span data-ttu-id="19b51-780">_**Figura 29:** ignorare gli avvisi sul quorum disco hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="19b51-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurare il controllo di condivisione file del cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="19b51-782">La configurazione di un controllo di condivisione file del cluster prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="19b51-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="19b51-783">Creazione di una condivisione file</span><span class="sxs-lookup"><span data-stu-id="19b51-783">Creating a file share</span></span>
- <span data-ttu-id="19b51-784">L'impostazione di quorum di controllo condivisione file hello in Gestione Cluster di Failover</span><span class="sxs-lookup"><span data-stu-id="19b51-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="19b51-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="19b51-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="19b51-786">Selezionare un controllo di condivisione file invece di un disco quorum.</span><span class="sxs-lookup"><span data-stu-id="19b51-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="19b51-787">SIOS DataKeeper supporta questa opzione.</span><span class="sxs-lookup"><span data-stu-id="19b51-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="19b51-788">Negli esempi di hello in questo articolo, hello witness di condivisione file è nel server di Active Directory/DNS hello è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="19b51-789">Hello condivisione file di controllo viene chiamato **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="19b51-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="19b51-790">Poiché potrebbe aver configurato un tooAzure di connessione VPN (tramite VPN Site-to-Site o ExpressRoute di Azure), il/DNS di Active Directory service è locale e non è adatto toorun un file di condividere controllo del mirroring.</span><span class="sxs-lookup"><span data-stu-id="19b51-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="19b51-791">Se il servizio Active Directory/DNS viene eseguito solo in locale, non si configura la condivisione file di controllo nel sistema operativo di Active Directory/DNS Windows hello che è in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="19b51-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="19b51-792">La latenza di rete tra i nodi del cluster in esecuzione in Azure e Active Directory/DNS in locale potrebbe essere eccessiva e causare problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="19b51-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="19b51-793">Impossibile verificare tooconfigure hello witness di condivisione file in una macchina virtuale di Azure che esegue toohello Chiudi nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="19b51-794">unità quorum Hello richiede almeno 1024 MB di spazio libero.</span><span class="sxs-lookup"><span data-stu-id="19b51-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="19b51-795">È consigliabile 2048 MB di spazio disponibile per l'unità quorum hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="19b51-796">Aggiungere l'oggetto nome cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-796">Add hello cluster name object.</span></span>

  ![Figura 30: Assegnare le autorizzazioni hello hello condivisione per l'oggetto nome cluster di hello][sap-ha-guide-figure-3019]

  <span data-ttu-id="19b51-798">_**Figura 30:** assegnare autorizzazioni hello nella condivisione di hello per l'oggetto nome cluster di hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="19b51-799">Assicurarsi che le autorizzazioni di hello includano dati di hello autorità toochange nella condivisione di hello per l'oggetto nome cluster di hello (in questo esempio, **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="19b51-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="19b51-800">tooadd hello cluster nome oggetto toohello elenco, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="19b51-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="19b51-801">Modificare hello toocheck di filtro per gli oggetti computer, in aggiunta toothose illustrato nella figura 31.</span><span class="sxs-lookup"><span data-stu-id="19b51-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Figura 31: Modificare i computer tooinclude di tipi di oggetto hello][sap-ha-guide-figure-3020]

  <span data-ttu-id="19b51-803">_**Figura 31:** cambia hello tipi di oggetto tooinclude computer_</span><span class="sxs-lookup"><span data-stu-id="19b51-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![32 figura: Casella di controllo di computer selezionare hello][sap-ha-guide-figure-3021]

  <span data-ttu-id="19b51-805">_**Nella figura 32:** hello seleziona **computer** casella di controllo_</span><span class="sxs-lookup"><span data-stu-id="19b51-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="19b51-806">Immettere il oggetto nome cluster hello come illustrato nella figura 31.</span><span class="sxs-lookup"><span data-stu-id="19b51-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="19b51-807">Poiché è già stato creato il record di hello, è possibile modificare le autorizzazioni di hello, come illustrato nella figura 30.</span><span class="sxs-lookup"><span data-stu-id="19b51-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="19b51-808">Seleziona hello **sicurezza** scheda della condivisione hello e quindi impostare più dettagliato le autorizzazioni per l'oggetto nome cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Figura 33: Impostare gli attributi di sicurezza di hello per l'oggetto nome cluster di hello in quorum di condivisione file hello][sap-ha-guide-figure-3022]

  <span data-ttu-id="19b51-810">_**Nella figura 33:** impostare gli attributi di sicurezza hello per l'oggetto nome cluster di hello in quorum di condivisione file hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="19b51-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Impostare quorum di controllo condivisione file hello in Gestione Cluster di Failover</span><span class="sxs-lookup"><span data-stu-id="19b51-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="19b51-812">Aprire configurazione Quorum impostazione guidata hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Avviare hello guidata Configura impostazioni Quorum del Cluster][sap-ha-guide-figure-3023]

  <span data-ttu-id="19b51-814">_**Figura 34:** inizio hello configurazione guidata impostazioni Quorum del Cluster_</span><span class="sxs-lookup"><span data-stu-id="19b51-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="19b51-815">In hello **selezionare configurazione Quorum** selezionare **selezione quorum di controllo hello**.</span><span class="sxs-lookup"><span data-stu-id="19b51-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Figura 35: Configurazioni del quorum tra cui è possibile scegliere][sap-ha-guide-figure-3024]

  <span data-ttu-id="19b51-817">_**Figura 35:** Configurazioni del quorum tra cui è possibile scegliere_</span><span class="sxs-lookup"><span data-stu-id="19b51-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="19b51-818">In hello **selezione Quorum di controllo** selezionare **configurare una condivisione file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="19b51-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![36 figura: Controllo di condivisione file hello selezionare][sap-ha-guide-figure-3025]

  <span data-ttu-id="19b51-820">_**Nella figura 36:** selezionare hello witness di condivisione file_</span><span class="sxs-lookup"><span data-stu-id="19b51-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="19b51-821">Immettere una condivisione di file toohello percorso UNC hello (in questo esempio, \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="19b51-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="19b51-822">un elenco di hello le modifiche apportate, selezionare toosee **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="19b51-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Figura 37: Definire percorso della condivisione file hello per la condivisione di controllo hello][sap-ha-guide-figure-3026]

  <span data-ttu-id="19b51-824">_**Figura 37:** definire percorso della condivisione file hello per la condivisione di controllo hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="19b51-825">Selezionare le modifiche di hello desiderato e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="19b51-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="19b51-826">È necessario toosuccessfully riconfigurare configurazione cluster hello, come illustrato nella figura 38.</span><span class="sxs-lookup"><span data-stu-id="19b51-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Nella figura 38: Conferma che è stato riconfigurato cluster hello][sap-ha-guide-figure-3027]

  <span data-ttu-id="19b51-828">_**Nella figura 38:** conferma che è stato riconfigurato cluster hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="19b51-829">Dopo l'installazione di un Cluster di Failover di Windows hello correttamente, è necessario modifiche toobe apportate toosome soglie tooadapt failover rilevamento tooconditions in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="19b51-830">Hello toobe parametri modificati sono documentati in questo blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="19b51-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="19b51-831">Presupponendo che le due macchine virtuali che compila hello configurazione di Cluster di Windows per ASCS/SCS sono hello stessa SubNet, i seguenti parametri hello necessari valori toothese toobe modificato:</span><span class="sxs-lookup"><span data-stu-id="19b51-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="19b51-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="19b51-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="19b51-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="19b51-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="19b51-834">Queste impostazioni sono state testate con clienti e fornite toobe un buon compromesso sufficientemente flessibili nel lato "uno" hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="19b51-835">In hello invece tali impostazioni sono state fornendo fast sufficiente failover nelle condizioni di errore in caso di errore SAP software o nodo/macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="19b51-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="19b51-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Installare l'edizione Cluster di SIOS DataKeeper per disco condivisione del cluster di SAP ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="19b51-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="19b51-837">Ora è disponibile una configurazione funzionante di Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="19b51-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="19b51-838">Ma, tooinstall un'istanza di SAP ASCS/SCS, è necessario utilizzare una risorsa disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="19b51-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="19b51-839">È possibile creare le risorse disco condivise hello che è necessario in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="19b51-840">SIOS DataKeeper Cluster Edition è una soluzione di terze parti è possibile utilizzare le risorse disco condivise toocreate.</span><span class="sxs-lookup"><span data-stu-id="19b51-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="19b51-841">Installazione di SIOS DataKeeper Cluster Edition per SAP ASCS/SCS hello disco del cluster di condivisione include le attività:</span><span class="sxs-lookup"><span data-stu-id="19b51-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="19b51-842">Aggiunta di hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="19b51-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="19b51-843">Installazione di SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="19b51-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="19b51-844">Configurazione di SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="19b51-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="19b51-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Aggiungere hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="19b51-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="19b51-846">Hello Microsoft .NET Framework 3.5 non viene automaticamente attivato o installato in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="19b51-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="19b51-847">Poiché SIOS DataKeeper richiede hello toobe di .NET Framework in tutti i nodi che si installa DataKeeper in, è necessario installare .NET Framework 3.5 hello nel sistema operativo guest di hello di tutte le macchine virtuali in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="19b51-848">Esistono due hello di tooadd metodi .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="19b51-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="19b51-849">Utilizzare hello Aggiunta guidata ruoli e funzionalità in Windows, come illustrato nella figura 39.</span><span class="sxs-lookup"><span data-stu-id="19b51-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Installare .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3028]

  <span data-ttu-id="19b51-851">_**Nella figura 39:** hello installare .NET Framework 3.5 utilizzando hello Aggiunta guidata ruoli e funzionalità_</span><span class="sxs-lookup"><span data-stu-id="19b51-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Figura 40: Installazione indicatore di stato quando si installa .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3029]

  <span data-ttu-id="19b51-853">_**Figura 40:** indicatore quando si installa .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità di installazione_</span><span class="sxs-lookup"><span data-stu-id="19b51-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="19b51-854">Utilizzare hello strumento da riga di comando dism.exe.</span><span class="sxs-lookup"><span data-stu-id="19b51-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="19b51-855">Per questo tipo di installazione, è necessario tooaccess hello SxS directory hello supporti di installazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="19b51-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="19b51-856">A un prompt dei comandi con privilegi elevati digitare:</span><span class="sxs-lookup"><span data-stu-id="19b51-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="19b51-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Installare SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="19b51-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="19b51-858">Installare l'edizione Cluster di SIOS DataKeeper su ogni nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="19b51-859">archiviazione condivisa virtuale toocreate con SIOS DataKeeper, creare un mirror sincronizzato e simulare archiviazione condivisa cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="19b51-860">Prima di installare il software SIOS hello, creare l'utente di dominio di hello **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="19b51-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-861">Aggiungere hello **DataKeeperSvc** utente toohello **amministratore locale** gruppo in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="19b51-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="19b51-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="19b51-863">Installare il software SIOS hello in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![Programma di installazione SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Prima pagina di installazione di SIOS DataKeeper hello][sap-ha-guide-figure-3031]

  <span data-ttu-id="19b51-866">_**Figura 41:** prima pagina di installazione di SIOS DataKeeper hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="19b51-867">Selezionare la finestra di dialogo hello illustrata nella figura 42, **Sì**.</span><span class="sxs-lookup"><span data-stu-id="19b51-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: DataKeeper segnala che un servizio verrà disabilitato][sap-ha-guide-figure-3032]

  <span data-ttu-id="19b51-869">_**Figura 42:** DataKeeper segnala che un servizio verrà disabilitato_</span><span class="sxs-lookup"><span data-stu-id="19b51-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="19b51-870">Nella finestra di dialogo hello illustrata nella figura 43, è consigliabile selezionare **account di dominio o Server**.</span><span class="sxs-lookup"><span data-stu-id="19b51-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Selezione dell'utente per SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="19b51-872">_**Figura 43:** Selezione dell'utente per SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="19b51-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="19b51-873">Immettere nome utente dell'account di dominio hello e la password creata per SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="19b51-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Immettere nome utente di dominio hello e una password per hello installazione SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="19b51-875">_**Figura 44:** immettere nome utente di dominio hello e la password per l'installazione di SIOS DataKeeper hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="19b51-876">Installare hello chiave di licenza per l'istanza di SIOS DataKeeper, come illustrato nella Figura 45.</span><span class="sxs-lookup"><span data-stu-id="19b51-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: Specificare la chiave di licenza di SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="19b51-878">_**Figura 45:** Specificare la chiave di licenza di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="19b51-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="19b51-879">Quando richiesto, riavviare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="19b51-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurare SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="19b51-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="19b51-881">Dopo aver installato SIOS DataKeeper in entrambi i nodi, è necessario configurazione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="19b51-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="19b51-882">obiettivo di Hello della configurazione di hello è la replica di dati sincroni toohave tra hello ulteriori dischi rigidi virtuali collegati tooeach delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="19b51-883">Avviare Gestione DataKeeper hello e strumento di configurazione e quindi selezionare **Connetti Server**.</span><span class="sxs-lookup"><span data-stu-id="19b51-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="19b51-884">Nella figura 46, questa opzione è racchiusa in un cerchio rosso.</span><span class="sxs-lookup"><span data-stu-id="19b51-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Strumento di configurazione e gestione di SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="19b51-886">_**Figura 46:** Strumento di configurazione e gestione di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="19b51-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="19b51-887">Immettere il nome di hello o indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve connettersi a e, in un secondo passaggio, secondo nodo hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Figura 47: Nome hello inserimento o l'indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve collegarsi a e, in un secondo passaggio, secondo nodo hello][sap-ha-guide-figure-3037]

  <span data-ttu-id="19b51-889">_**Figura 47:** nome hello inserimento o l'indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve collegarsi a e, in un secondo passaggio, secondo nodo hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="19b51-890">Creare il processo di replica hello tra due nodi hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-890">Create hello replication job between hello two nodes.</span></span>

  ![Figura 48: Creare un processo di replica][sap-ha-guide-figure-3038]

  <span data-ttu-id="19b51-892">_**Figura 48:** Creare un processo di replica_</span><span class="sxs-lookup"><span data-stu-id="19b51-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="19b51-893">Una procedura guidata semplificato il processo di hello di creazione di un processo di replica.</span><span class="sxs-lookup"><span data-stu-id="19b51-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="19b51-894">Definire nome hello indirizzo TCP/IP e il volume del disco del nodo di origine hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Figura 49: Definire il nome di hello del processo di replica hello][sap-ha-guide-figure-3039]

  <span data-ttu-id="19b51-896">_**Figura 49:** nome hello di definizione del processo di replica hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Figura 50: Definire i dati di base per il nodo hello, che deve essere il nodo di origine corrente hello hello][sap-ha-guide-figure-3040]

  <span data-ttu-id="19b51-898">_**Figura 50:** definire dati di base per il nodo hello, che deve essere il nodo di origine corrente hello hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="19b51-899">Definire nome hello indirizzo TCP/IP e il volume del disco del nodo di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Figura 51: Definire i dati di base per il nodo hello, che deve essere il nodo di destinazione corrente hello hello][sap-ha-guide-figure-3041]

  <span data-ttu-id="19b51-901">_**Figura 51:** definire dati di base per il nodo hello, che deve essere il nodo di destinazione corrente hello hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="19b51-902">Definire gli algoritmi di compressione hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-902">Define hello compression algorithms.</span></span> <span data-ttu-id="19b51-903">In questo esempio, è consigliabile comprimere il flusso di replica hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="19b51-904">Specialmente in situazioni di risincronizzazione, la compressione di hello del flusso di replica hello riduce notevolmente il tempo di risincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="19b51-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="19b51-905">Si noti che la compressione utilizza risorse di CPU e RAM hello di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="19b51-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="19b51-906">Man mano che aumenta la velocità di compressione hello, pertanto hello volume delle risorse della CPU utilizzato.</span><span class="sxs-lookup"><span data-stu-id="19b51-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="19b51-907">È possibile anche modificare questa impostazione in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="19b51-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="19b51-908">Un'altra impostazione necessaria toocheck è se hello replica sincrona o asincrona.</span><span class="sxs-lookup"><span data-stu-id="19b51-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="19b51-909">*Per proteggere le configurazioni di SAP ASCS/SCS, è necessario usare la replica sincrona*.</span><span class="sxs-lookup"><span data-stu-id="19b51-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definire i dettagli della replica][sap-ha-guide-figure-3042]

  <span data-ttu-id="19b51-911">_**Figura 52:** Definire i dettagli della replica_</span><span class="sxs-lookup"><span data-stu-id="19b51-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="19b51-912">Definire se volume hello replicato dal processo di replica hello deve essere di configurazione del cluster Windows Server Failover Clustering tooa rappresentato come un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="19b51-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="19b51-913">Per la configurazione di SAP ASCS/SCS hello, selezionare **Sì** in modo che Windows hello cluster vede hello volume replicati come un disco condiviso che è possibile utilizzare come un volume del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Hello tooset selezionare Sì replicate volume come volume del cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="19b51-915">_**Figura 53:** selezionare **Sì** tooset hello volume come volume di cluster di replicate_</span><span class="sxs-lookup"><span data-stu-id="19b51-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="19b51-916">Dopo aver creato il volume di hello, lo strumento di configurazione e gestione DataKeeper hello viene illustrato che tale processo di replica hello è attivo.</span><span class="sxs-lookup"><span data-stu-id="19b51-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Figura 54: Mirroring sincrono DataKeeper per SAP ASCS/SCS condivisione disco hello è attivo][sap-ha-guide-figure-3044]

  <span data-ttu-id="19b51-918">_**Figura 54:** mirroring sincrono DataKeeper per SAP ASCS/SCS hello condividere disco è attivo_</span><span class="sxs-lookup"><span data-stu-id="19b51-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="19b51-919">Gestione Cluster di failover viene ora disco hello come disco DataKeeper, come illustrato nella Figura 55.</span><span class="sxs-lookup"><span data-stu-id="19b51-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: In Gestione Cluster di Failover viene visualizzato disco hello replicati DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="19b51-921">_**Figura 55:** gestione Cluster di Failover viene disco hello che DataKeeper replicati_</span><span class="sxs-lookup"><span data-stu-id="19b51-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="19b51-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Installare il sistema di SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="19b51-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="19b51-923">È non descrivono il programma di installazione di hello DBMS perché le impostazioni variano a seconda di hello sistema DBMS in uso.</span><span class="sxs-lookup"><span data-stu-id="19b51-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="19b51-924">Tuttavia, si presuppone che i problemi di disponibilità elevata hello DBMS vengono indirizzati con funzionalità hello diversi fornitori di sistemi DBMS hello il supporto per Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="19b51-925">ad esempio AlwaysOn o mirroring del database per SQL Server e Oracle Data Guard per database Oracle.</span><span class="sxs-lookup"><span data-stu-id="19b51-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="19b51-926">Nello scenario di hello che viene usato in questo articolo, ci non sono state aggiunte altre protezione toohello DBMS.</span><span class="sxs-lookup"><span data-stu-id="19b51-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="19b51-927">Non esistono particolari considerazioni per il caso in cui servizi DBMS differenti interagiscono con questa configurazione di SAP ASCS/SCS in cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-928">procedure di installazione Hello di sistemi SAP NetWeaver ABAP, Java e sistemi ABAP + Java sono quasi identiche.</span><span class="sxs-lookup"><span data-stu-id="19b51-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="19b51-929">la differenza più significativa di Hello è un sistema SAP ABAP con un'istanza ASCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="19b51-930">Hello sistema Java di SAP include un'istanza SCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="19b51-931">Hello sistema ABAP + Java di SAP include un'istanza ASCS e in esecuzione in un'istanza SCS hello nello stesso gruppo di cluster di failover di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19b51-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="19b51-932">Eventuali differenze di installazione per ogni stack di installazione di SAP NetWeaver verranno indicate in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="19b51-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="19b51-933">Si può presupporre che tutte le altre parti sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="19b51-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="19b51-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Installare SAP con un'istanza di ASCS/SCS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="19b51-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19b51-935">Verificare che i volumi con mirroring di non tooplace in DataKeeper di file della pagina.</span><span class="sxs-lookup"><span data-stu-id="19b51-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="19b51-936">DataKeeper non supporta i volumi con mirroring.</span><span class="sxs-lookup"><span data-stu-id="19b51-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="19b51-937">È possibile lasciare il file di pagina nell'unità temporanea hello D di una macchina virtuale di Azure, ovvero impostazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="19b51-938">Se non è già presente, è possibile spostare hello Windows pagina file toodrive D della macchina virtuale Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="19b51-939">L'installazione di SAP con un'istanza di ASCS/SCS a disponibilità elevata prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="19b51-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="19b51-940">Creazione di un nome host virtuale per l'istanza di SAP ASCS/SCS hello in cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="19b51-941">L'installazione di hello SAP primo nodo del cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="19b51-942">Modifica profilo SAP hello dell'istanza di hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="19b51-943">Aggiunta di un porta probe</span><span class="sxs-lookup"><span data-stu-id="19b51-943">Adding a probe port</span></span>
- <span data-ttu-id="19b51-944">Aprire la porta probe di hello Windows firewall</span><span class="sxs-lookup"><span data-stu-id="19b51-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="19b51-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Creare un nome host virtuale per l'istanza di SAP ASCS/SCS hello in cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="19b51-946">Nella console di gestione DNS di Windows hello, creare una voce DNS per il nome host virtuale hello dell'istanza di hello ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19b51-947">Hello indirizzo IP che è assegnato il nome host virtuale toohello di hello ASCS/SCS istanza deve essere hello stesso come indirizzo IP hello assegnato tooAzure bilanciamento del carico (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="19b51-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="19b51-948">l'indirizzo IP del nome host di SAP ASCS/SCS virtuale hello Hello (**pr1-sap ascs**) hello stesso come indirizzo IP hello di bilanciamento del carico di Azure (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="19b51-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definire voce DNS hello per il nome virtuale del cluster di SAP ASCS/SCS hello e l'indirizzo TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="19b51-950">_**Figura 56:** definire una voce DNS hello per il nome virtuale del cluster di SAP ASCS/SCS hello e l'indirizzo TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="19b51-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="19b51-951">toodefine hello nome indirizzo IP assegnato toohello host virtuale, selezionare **gestore DNS** > **dominio**.</span><span class="sxs-lookup"><span data-stu-id="19b51-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="19b51-953">_**Figura 57:** Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="19b51-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="19b51-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Installare hello SAP primo nodo del cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="19b51-955">Eseguire hello primo nodo opzione cluster sul nodo del cluster A. Ad esempio, in hello **pr1-ascs-0** host.</span><span class="sxs-lookup"><span data-stu-id="19b51-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="19b51-956">porte predefinite di hello tookeep per hello Azure interno il bilanciamento del carico, selezionare:</span><span class="sxs-lookup"><span data-stu-id="19b51-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="19b51-957">Per il **sistema ABAP**: **ASCS** numero di istanza **00**</span><span class="sxs-lookup"><span data-stu-id="19b51-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="19b51-958">Per il **sistema Java**: **SCS** numero di istanza **01**</span><span class="sxs-lookup"><span data-stu-id="19b51-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="19b51-959">Per il **sistema ABAP + Java**: **ASCS** numero di istanza **00** e **SCS** numero di istanza **01**</span><span class="sxs-lookup"><span data-stu-id="19b51-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="19b51-960">istanza toouse numeri diverso da 00 per hello ABAP ASCS 01 per l'istanza di Java SCS hello e istanza, è necessario innanzitutto toochange hello Azure carico interno del servizio di bilanciamento predefinito di bilanciamento del carico le regole, descritte in [carico predefinito ASCS/SCS hello di modifica bilanciamento del carico delle regole di bilanciamento del carico interno di Azure hello][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="19b51-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="19b51-961">alcune attività successiva Hello non sono descritti nella documentazione di installazione SAP standard hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-962">documentazione di installazione di SAP Hello viene descritto come tooinstall hello primo nodo del cluster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="19b51-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="19b51-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificare il profilo di SAP hello dell'istanza di hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="19b51-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="19b51-964">È necessario tooadd un nuovo parametro del profilo.</span><span class="sxs-lookup"><span data-stu-id="19b51-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="19b51-965">parametro del profilo Hello impedisce le connessioni tra i processi di lavoro SAP e il server di Accodamento hello di chiusura quando sono inattivi per troppo tempo.</span><span class="sxs-lookup"><span data-stu-id="19b51-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="19b51-966">Accennato scenario problema hello in [aggiungere le voci del Registro di sistema in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="19b51-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="19b51-967">In questa sezione è stata introdotta anche due modifiche toosome base TCP/IP parametri di connessione.</span><span class="sxs-lookup"><span data-stu-id="19b51-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="19b51-968">In un secondo passaggio, è necessario tooset hello enqueue server toosend un `keep_alive` indicano in modo che le connessioni di hello non raggiunto una soglia di inattività del hello Azure interna di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="19b51-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="19b51-969">hello toomodify profilo SAP dell'istanza ASCS/SCS hello:</span><span class="sxs-lookup"><span data-stu-id="19b51-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="19b51-970">Aggiungere questo toohello di parametro del profilo di istanza di SAP ASCS/SCS di profilo:</span><span class="sxs-lookup"><span data-stu-id="19b51-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="19b51-971">In questo esempio, il percorso di hello è:</span><span class="sxs-lookup"><span data-stu-id="19b51-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="19b51-972">Ad esempio, profilo di istanza SAP SCS toohello e il percorso corrispondente:</span><span class="sxs-lookup"><span data-stu-id="19b51-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="19b51-973">modifiche hello tooapply, riavviare l'istanza di SAP ASCS /SCS hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="19b51-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Aggiungere una porta probe</span><span class="sxs-lookup"><span data-stu-id="19b51-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="19b51-975">Utilizzare operazioni di configurazione del hello interna di bilanciamento del carico probe funzionalità toomake hello intero cluster con bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="19b51-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="19b51-976">servizio di bilanciamento del carico interno di Azure Hello distribuisce in genere hello in arrivo del carico di lavoro in modo uniforme tra le macchine virtuali partecipante.</span><span class="sxs-lookup"><span data-stu-id="19b51-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="19b51-977">Questa operazione non funziona tuttavia in alcune configurazioni di cluster perché è attiva una sola istanza.</span><span class="sxs-lookup"><span data-stu-id="19b51-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="19b51-978">Hello altra istanza è passiva e non può accettare qualsiasi carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="19b51-979">Una funzionalità di probe è utile quando si assegna bilanciamento di carico interno di Azure hello istanze attive tooan solo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19b51-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="19b51-980">Con la funzionalità di probe hello, bilanciamento del carico interno hello può rilevare le istanze che sono attive e quindi puntare solo hello istanza con carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="19b51-981">una porta probe tooadd:</span><span class="sxs-lookup"><span data-stu-id="19b51-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="19b51-982">Controllare hello corrente **ProbePort** impostazione eseguendo il comando PowerShell seguente hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="19b51-983">Eseguirlo all'interno di una delle macchine virtuali hello nella configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="19b51-984">Definire una porta probe.</span><span class="sxs-lookup"><span data-stu-id="19b51-984">Define a probe port.</span></span> <span data-ttu-id="19b51-985">numero di porta probe predefinito Hello è **0**.</span><span class="sxs-lookup"><span data-stu-id="19b51-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="19b51-986">In questo esempio viene usata la porta probe **62000**.</span><span class="sxs-lookup"><span data-stu-id="19b51-986">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: porta probe configurazione del cluster hello è 0 per impostazione predefinita][sap-ha-guide-figure-3048]

  <span data-ttu-id="19b51-988">_**Figura 58:** la porta probe hello predefinita cluster configurazione è 0_</span><span class="sxs-lookup"><span data-stu-id="19b51-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="19b51-989">numero di porta Hello è definito nei modelli di SAP Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19b51-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="19b51-990">È possibile assegnare il numero di porta hello in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19b51-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="19b51-991">un nuovo valore ProbePort per hello tooset  **SAP <*SID*> IP * * risorsa cluster, eseguire lo script di PowerShell seguente hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="19b51-992">Aggiornare le variabili di PowerShell hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="19b51-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="19b51-993">Dopo l'esecuzione dello script hello, sarà richiesta toorestart hello SAP cluster tooactivate hello modifiche apportate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="19b51-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="19b51-994">Dopo aver portato hello  **SAP <*SID*> * * ruolo del cluster, verificare che **ProbePort** è impostato un valore nuovo toohello.</span><span class="sxs-lookup"><span data-stu-id="19b51-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Probe porta hello del cluster dopo aver impostato il nuovo valore di hello][sap-ha-guide-figure-3049]

  <span data-ttu-id="19b51-996">_**Figura 59:** Probe porta hello del cluster dopo aver impostato il nuovo valore di hello_</span><span class="sxs-lookup"><span data-stu-id="19b51-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="19b51-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Aprire la porta probe di hello Windows firewall</span><span class="sxs-lookup"><span data-stu-id="19b51-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="19b51-998">È necessario tooopen una porta di probe di Windows firewall su entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="19b51-999">Utilizzare i seguenti script tooopen una porta probe del firewall Windows hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="19b51-1000">Aggiornare le variabili di PowerShell hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="19b51-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="19b51-1001">Hello **ProbePort** è troppo**62000**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="19b51-1002">Ora è possibile accedere a una condivisione di hello  **\\\ascsha-clsap\sapmnt** da altri host, ad esempio di **ascsha DBA**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="19b51-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Installare l'istanza del database hello</span><span class="sxs-lookup"><span data-stu-id="19b51-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="19b51-1004">database hello tooinstall dell'istanza, seguire il processo di hello descritto nella documentazione di installazione di SAP hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="19b51-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Installare secondo nodo del cluster hello</span><span class="sxs-lookup"><span data-stu-id="19b51-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="19b51-1006">tooinstall hello secondo cluster, eseguire i passaggi nella Guida all'installazione di SAP hello hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="19b51-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Modificare il tipo di avvio dell'istanza di servizio SAP Hiamanti Windows hello hello</span><span class="sxs-lookup"><span data-stu-id="19b51-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="19b51-1008">Modificare il tipo di avvio del servizio SAP Hiamanti Windows hello hello troppo**automatico (avvio ritardato)** in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="19b51-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Modificare il tipo di servizio hello per hello SAP Hiamanti istanza toodelayed automatico][sap-ha-guide-figure-3050]

<span data-ttu-id="19b51-1010">_**Figura 60:** modificare il tipo di servizio hello per hello SAP Hiamanti istanza toodelayed automatico_</span><span class="sxs-lookup"><span data-stu-id="19b51-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="19b51-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Installare hello Server primario di applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="19b51-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="19b51-1012">Installare l'istanza primaria applicazione Server (PAS) hello <*SID*> - di - 0 nella macchina virtuale hello specificate toohost hello indirizzi PA.</span><span class="sxs-lookup"><span data-stu-id="19b51-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="19b51-1013">Non sono presenti dipendenze da specifiche impostazioni di Azure o DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="19b51-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="19b51-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Installare ulteriori Server di applicazioni SAP hello</span><span class="sxs-lookup"><span data-stu-id="19b51-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="19b51-1015">Installare un Server applicazioni aggiuntivi SAP (AAS) in tutte le macchine virtuali hello che è stato designato toohost un'istanza del Server SAP.</span><span class="sxs-lookup"><span data-stu-id="19b51-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="19b51-1016">Ad esempio, in <*SID*> - di - 1 troppo <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="19b51-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="19b51-1017">Questo completa l'installazione di hello di un sistema SAP NetWeaver a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="19b51-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="19b51-1018">Procedere quindi con il test del failover.</span><span class="sxs-lookup"><span data-stu-id="19b51-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="19b51-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Test di failover di istanza di SAP ASCS/SCS hello e la replica di SIOS</span><span class="sxs-lookup"><span data-stu-id="19b51-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="19b51-1020">È facile tootest e monitorare un failover di istanza di SAP ASCS/SCS e la replica dei dischi SIOS usando Gestione Cluster di Failover e lo strumento di configurazione e gestione di SIOS DataKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="19b51-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="19b51-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> Istanza di SAP ASCS/SCS in esecuzione nel nodo A del cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="19b51-1022">Hello **PR1 SAP** gruppo di cluster è in esecuzione sul nodo del cluster A. Ad esempio, in **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="19b51-1023">Assegnare l'unità disco condivisa hello S, che fa parte di hello **PR1 SAP** gruppo e viene utilizzata l'istanza ASCS/SCS hello, toocluster nodo a cluster</span><span class="sxs-lookup"><span data-stu-id="19b51-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Figura 61: Gestione Cluster di Failover: gruppo di cluster SAP < SID > hello è in esecuzione in un nodo del cluster][sap-ha-guide-figure-5000]

<span data-ttu-id="19b51-1025">_**Figura 61:** gestione Cluster di Failover: hello SAP <*SID*> gruppo di cluster è in esecuzione in un nodo del cluster_</span><span class="sxs-lookup"><span data-stu-id="19b51-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="19b51-1026">In hello SIOS DataKeeper gestione e lo strumento di configurazione, è possibile visualizzare tale disco condiviso hello i dati vengono replicati in modo sincrono da hello volume unità di origine S sul nodo del cluster di un'unità di volume di destinazione S toohello nel nodo B. Ad esempio, viene replicata dal **pr1-ascs-0 [10.0.0.40]** troppo**pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: In SIOS DataKeeper, replicare volume locale hello dal nodo del cluster un nodo toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="19b51-1028">_**Figura 62:** In SIOS DataKeeper, replicare volume locale hello dal nodo del cluster un nodo toocluster B_</span><span class="sxs-lookup"><span data-stu-id="19b51-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="19b51-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover dal nodo toonode B</span><span class="sxs-lookup"><span data-stu-id="19b51-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="19b51-1030">Scegliere una di queste opzioni tooinitiate un failover di hello SAP <*SID*> gruppo di cluster dal nodo toocluster del nodo cluster b:</span><span class="sxs-lookup"><span data-stu-id="19b51-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="19b51-1031">Usare Gestione cluster di failover</span><span class="sxs-lookup"><span data-stu-id="19b51-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="19b51-1032">Usare PowerShell per Clustering di failover</span><span class="sxs-lookup"><span data-stu-id="19b51-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="19b51-1033">Riavviare un nodo di cluster all'interno del sistema operativo guest di Windows hello (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).</span><span class="sxs-lookup"><span data-stu-id="19b51-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="19b51-1034">Riavviare un nodo del cluster da hello portale di Azure (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).</span><span class="sxs-lookup"><span data-stu-id="19b51-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="19b51-1035">Riavviare un nodo del cluster tramite Azure PowerShell (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).</span><span class="sxs-lookup"><span data-stu-id="19b51-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="19b51-1036">Dopo il failover, hello SAP <*SID*> gruppo di cluster è in esecuzione nel nodo B. Ad esempio, è in esecuzione **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: In Gestione Cluster di Failover, gruppo di cluster SAP < SID > hello è in esecuzione sul nodo del cluster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="19b51-1038">_**Figura 63**: In Gestione Cluster di Failover, hello SAP <*SID*> gruppo di cluster è in esecuzione sul nodo del cluster B_</span><span class="sxs-lookup"><span data-stu-id="19b51-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="19b51-1039">Hello disco condiviso è ora installato nel cluster nodo B. SIOS DataKeeper è la replica dei dati dall'unità di volume di origine S nel cluster del nodo B tootarget volume unità S nel nodo del cluster A. Ad esempio, è la replica da **pr1-ascs-1 [10.0.0.41]** troppo**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="19b51-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica volume locale hello dal cluster nodo B toocluster nodo][sap-ha-guide-figure-5003]

  <span data-ttu-id="19b51-1041">_**Figura 64:** SIOS DataKeeper replica volume locale hello dal nodo del cluster del nodo B toocluster A_</span><span class="sxs-lookup"><span data-stu-id="19b51-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
