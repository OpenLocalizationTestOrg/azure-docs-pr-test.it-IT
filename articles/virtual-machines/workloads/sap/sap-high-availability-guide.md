---
title: "Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver | Documentazione Microsoft"
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
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="867f7-103">Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="867f7-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="867f7-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="867f7-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="867f7-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="867f7-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="867f7-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="867f7-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="867f7-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="867f7-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="867f7-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="867f7-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="867f7-109">Macchine virtuali di Azure è la soluzione ideale per le organizzazioni che necessitano di risorse di calcolo, di archiviazione e di rete in tempi minimi e con cicli di approvvigionamento brevi.</span><span class="sxs-lookup"><span data-stu-id="867f7-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="867f7-110">È possibile usare Macchine virtuali di Azure per distribuire applicazioni classiche, ad esempio ABAP basato su SAP NetWeaver, Java e uno stack ABAP+Java.</span><span class="sxs-lookup"><span data-stu-id="867f7-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="867f7-111">È possibile estendere l'affidabilità e la disponibilità senza risorse locali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="867f7-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="867f7-112">Macchine virtuali di Azure supporta la connettività cross-premise e quindi è possibile integrare Macchine virtuali di Azure nei domini locali, nei cloud privati e nel panorama applicativo del sistema SAP dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="867f7-113">Questo articolo illustra la procedura che è possibile eseguire per distribuire sistemi SAP a disponibilità elevata in Azure, usando il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="867f7-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="867f7-114">Le attività principali che verranno illustrate sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="867f7-115">Trovare le guide all'installazione e le note di SAP appropriate elencate nella sezione [Risorse][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="867f7-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="867f7-116">Questo articolo integra la documentazione sull'installazione di SAP e le note su SAP, che sono le risorse principali per l'installazione e la distribuzione del software SAP in piattaforme specifiche.</span><span class="sxs-lookup"><span data-stu-id="867f7-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="867f7-117">Informazioni sulle differenze tra il modello di distribuzione classica di Azure e il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="867f7-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="867f7-118">Informazioni sulle modalità quorum di Windows Server Failover Clustering per consentire la selezione del modello più adatto per la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="867f7-119">Comprendere l'archiviazione condivisa di Windows Server Failover Clustering nei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="867f7-120">Leggere le informazioni su come proteggere in Azure i componenti con un singolo punto di guasto, ad esempio Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) e i sistemi di gestione di database (DBMS), oltre ai componenti ridondanti, ad esempio i server applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="867f7-121">Seguire un esempio dettagliato di installazione e configurazione di un sistema SAP a disponibilità elevata in un cluster Windows Server Failover Clustering in Azure usando Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="867f7-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="867f7-122">Apprendere gli altri passaggi obbligatori per usare Windows Server Failover Clustering in Azure, ma non necessari in una distribuzione locale.</span><span class="sxs-lookup"><span data-stu-id="867f7-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="867f7-123">Per semplificare la distribuzione e la configurazione, in questo articolo verranno usati modelli di Resource Manager a disponibilità elevata a tre livelli per SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="867f7-124">Il modelli automatizzano la distribuzione dell'intera infrastruttura necessaria per un sistema SAP a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="867f7-125">L'infrastruttura supporta anche il ridimensionamento SAP Application Performance Standard (SAPS) del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="867f7-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="867f7-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="867f7-127">Prima di iniziare, verificare che siano soddisfatti i prerequisiti descritti nei capitoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="867f7-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="867f7-128">Assicurarsi anche di controllare tutte le risorse elencate nella sezione [Risorse][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="867f7-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="867f7-129">In questo articolo vengono usati i modelli di Azure Resource Manager per [SAP NetWeaver a tre livelli con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="867f7-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="867f7-130">Per una panoramica dei modelli, vedere i [modelli di Azure Resource Manager per SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="867f7-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="867f7-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Risorse</span><span class="sxs-lookup"><span data-stu-id="867f7-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="867f7-132">Questi articoli descrivono le distribuzioni SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="867f7-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="867f7-133">[Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="867f7-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="867f7-134">[Distribuzione di Macchine virtuali di Azure per SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="867f7-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="867f7-135">[Distribuzione DBMS di Macchine virtuali di Azure per SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="867f7-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="867f7-136">[Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver (questa guida)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="867f7-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-137">Quando è possibile, viene fornito un collegamento alla guida di riferimento per l'installazione di SAP. Vedere le [guide all'installazione di SAP][sap-installation-guides].</span><span class="sxs-lookup"><span data-stu-id="867f7-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="867f7-138">Per i prerequisiti e per informazioni sul processo di installazione, è consigliabile leggere attentamente le guide all'installazione di SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="867f7-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="867f7-139">Questo articolo illustra solo attività specifiche per i sistemi basati su SAP NetWeaver che è possibile usare con Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="867f7-140">Queste note su SAP sono correlate all'argomento relativo a SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="867f7-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="867f7-141">Numero della nota</span><span class="sxs-lookup"><span data-stu-id="867f7-141">Note number</span></span> | <span data-ttu-id="867f7-142">Titolo</span><span class="sxs-lookup"><span data-stu-id="867f7-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="867f7-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="867f7-143">[1928533]</span></span> |<span data-ttu-id="867f7-144">Applicazioni SAP in Azure: dimensioni e prodotti supportati</span><span class="sxs-lookup"><span data-stu-id="867f7-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="867f7-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="867f7-145">[2015553]</span></span> |<span data-ttu-id="867f7-146">SAP in Microsoft Azure: prerequisiti per il supporto</span><span class="sxs-lookup"><span data-stu-id="867f7-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="867f7-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="867f7-147">[1999351]</span></span> |<span data-ttu-id="867f7-148">Monitoraggio avanzato di Azure per SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="867f7-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="867f7-149">[2178632]</span></span> |<span data-ttu-id="867f7-150">Metriche chiave del monitoraggio per SAP in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="867f7-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="867f7-151">[1999351]</span></span> |<span data-ttu-id="867f7-152">Virtualizzazione in Windows: monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="867f7-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="867f7-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="867f7-153">[2243692]</span></span> |<span data-ttu-id="867f7-154">Use of Azure Premium SSD Storage for SAP DBMS Instance (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP)</span><span class="sxs-lookup"><span data-stu-id="867f7-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="867f7-155">Sono disponibili altre informazioni sulle [limitazioni delle sottoscrizioni di Azure][azure-subscription-service-limits-subscription], incluse le limitazioni massime e quelle predefinite generali.</span><span class="sxs-lookup"><span data-stu-id="867f7-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="867f7-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP a disponibilità elevata con il modello di distribuzione classica di Azure e il modello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="867f7-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="867f7-157">I modelli di distribuzione di Azure Resource Manager e di distribuzione classica presentano le differenze seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="867f7-158">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="867f7-158">Resource groups</span></span>
- <span data-ttu-id="867f7-159">Dipendenza del servizio di bilanciamento del carico interno di Azure nel gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="867f7-160">Supporto per scenari di SAP con più SID</span><span class="sxs-lookup"><span data-stu-id="867f7-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="867f7-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="867f7-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="867f7-162">In Azure Resource Manager è possibile usare i gruppi di risorse per gestire tutte le risorse dell'applicazione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="867f7-163">In un approccio integrato tutte le risorse di un gruppo di risorse hanno lo stesso ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="867f7-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="867f7-164">Ad esempio, tutte le risorse vengono create ed eliminate contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="867f7-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="867f7-165">Altre informazioni sui [gruppi di risorse](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="867f7-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="867f7-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Dipendenza del servizio di bilanciamento del carico interno di Azure nel gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="867f7-167">Nel modello di distribuzione classica di Azure esiste una dipendenza tra il servizio di bilanciamento del carico interno di Azure (servizio Azure Load Balancer) e il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="867f7-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="867f7-168">Ogni servizio di bilanciamento del carico interno necessita di un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="867f7-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="867f7-169">In Azure Resource Manager ogni risorsa di Azure deve essere inserita in un gruppo di risorse di Azure, come anche Azure Load Balancer,</span><span class="sxs-lookup"><span data-stu-id="867f7-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="867f7-170">ma non è necessario avere un gruppo di risorse di Azure per ogni istanza di Azure Load Balancer. Un gruppo di risorse di Azure, ad esempio, può contenere più istanze di Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="867f7-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="867f7-171">L'ambiente è più semplice e flessibile.</span><span class="sxs-lookup"><span data-stu-id="867f7-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="867f7-172">Supporto per scenari di SAP con più SID</span><span class="sxs-lookup"><span data-stu-id="867f7-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="867f7-173">In Azure Resource Manager è possibile installare istanze di ASCS/SCS con più SAP ID (SID).</span><span class="sxs-lookup"><span data-stu-id="867f7-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="867f7-174">Le istanze con più SID sono consentite grazie al supporto di più indirizzi IP per ogni servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="867f7-175">Per usare il modello di distribuzione classica di Azure, seguire le procedure descritte in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056) (SAP NetWeaver in Azure: clustering di istanze di SAP ASCS/SCS tramite Windows Server Failover Clustering in Azure con SIOS DataKeeper).</span><span class="sxs-lookup"><span data-stu-id="867f7-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867f7-176">Per le installazioni SAP, è consigliabile usare il modello di distribuzione Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="867f7-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="867f7-177">perché offre molti vantaggi non disponibili nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="867f7-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="867f7-178">Sono disponibili altre informazioni sui [modelli di distribuzione][virtual-machines-azure-resource-manager-architecture-benefits-arm] di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="867f7-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span><span class="sxs-lookup"><span data-stu-id="867f7-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="867f7-180">Windows Server Failover Clustering è alla base di un'installazione SAP ASCS/SCS e di DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="867f7-181">Un cluster di failover è un gruppo di 1 + n server (nodi) indipendenti che funzionano insieme per aumentare la disponibilità di applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="867f7-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="867f7-182">Se si verifica un errore in un nodo, Windows Server Failover Clustering calcola il numero di errori che possono verificarsi e mantiene un cluster integro per fornire le applicazioni e i servizi.</span><span class="sxs-lookup"><span data-stu-id="867f7-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="867f7-183">A questo scopo è possibile scegliere tra diverse modalità quorum per ottenere il clustering di failover.</span><span class="sxs-lookup"><span data-stu-id="867f7-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="867f7-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modalità quorum</span><span class="sxs-lookup"><span data-stu-id="867f7-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="867f7-185">È possibile scegliere tra quattro modalità quorum quando si usa Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="867f7-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="867f7-186">**Maggioranza dei nodi**.</span><span class="sxs-lookup"><span data-stu-id="867f7-186">**Node Majority**.</span></span> <span data-ttu-id="867f7-187">Ogni nodo del cluster può votare.</span><span class="sxs-lookup"><span data-stu-id="867f7-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="867f7-188">Il cluster funziona solo con la maggioranza dei voti, vale a dire con più della metà dei voti.</span><span class="sxs-lookup"><span data-stu-id="867f7-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="867f7-189">È consigliabile scegliere questa opzione per i cluster con un numero dispari di nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="867f7-190">Ad esempio, anche se si verificano errori in tre nodi di un cluster con sette nodi, il cluster ottiene comunque la maggioranza e continua l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="867f7-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="867f7-191">**Maggioranza dei nodi e dei dischi**.</span><span class="sxs-lookup"><span data-stu-id="867f7-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="867f7-192">Ogni nodo e un disco designato (un disco di controllo) nello spazio di archiviazione del cluster possono votare quando sono disponibili e in comunicazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="867f7-193">Il cluster funziona solo con la maggioranza dei voti, vale a dire con più della metà dei voti.</span><span class="sxs-lookup"><span data-stu-id="867f7-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="867f7-194">Questa modalità ha senso in un ambiente cluster con un numero pari di nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="867f7-195">Se metà dei nodi e il disco sono online, il cluster rimane in uno stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="867f7-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="867f7-196">**Maggioranza dei nodi e delle condivisioni file**.</span><span class="sxs-lookup"><span data-stu-id="867f7-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="867f7-197">Ogni nodo e una condivisione file designata (controllo di condivisione file) creata dall'amministratore possono votare, indipendentemente dal fatto che i nodi e la condivisione file siano disponibili e in comunicazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="867f7-198">Il cluster funziona solo con la maggioranza dei voti, vale a dire con più della metà dei voti.</span><span class="sxs-lookup"><span data-stu-id="867f7-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="867f7-199">Questa modalità ha senso in un ambiente cluster con un numero pari di nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="867f7-200">È simile alla modalità Maggioranza dei nodi e dei dischi, ma usa una condivisione file di controllo invece di un disco di controllo.</span><span class="sxs-lookup"><span data-stu-id="867f7-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="867f7-201">Questa modalità è facile da implementare, ma la condivisione file potrebbe diventare un singolo punto di guasto, se non è a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="867f7-202">**Non di maggioranza - solo disco**.</span><span class="sxs-lookup"><span data-stu-id="867f7-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="867f7-203">Il cluster ha un quorum se un nodo è disponibile e in comunicazione con un disco specifico nello spazio di archiviazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="867f7-204">Solo i nodi che sono anche in comunicazione con questo disco possono aggiungersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="867f7-205">Si consiglia di non usare questa modalità.</span><span class="sxs-lookup"><span data-stu-id="867f7-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="867f7-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering locale</span><span class="sxs-lookup"><span data-stu-id="867f7-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="867f7-207">La figura 1 illustra un cluster con due nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="867f7-208">Se la connessione di rete tra i nodi viene interrotta ed entrambi i nodi rimangono operativi, un disco quorum o una condivisione file determina quale nodo continuerà a fornire le applicazioni e i servizi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="867f7-209">Il nodo che ha accesso alla condivisione file o al disco quorum è il nodo che garantisce la continuità dei servizi.</span><span class="sxs-lookup"><span data-stu-id="867f7-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="867f7-210">Poiché questo esempio usa un cluster con due nodi, viene usata la modalità quorum Maggioranza dei nodi e delle condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="867f7-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="867f7-211">Anche l'opzione Maggioranza dei nodi e dei dischi è valida.</span><span class="sxs-lookup"><span data-stu-id="867f7-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="867f7-212">In un ambiente di produzione è consigliabile usare un disco quorum.</span><span class="sxs-lookup"><span data-stu-id="867f7-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="867f7-213">Per fare in modo che sia a disponibilità elevata, è possibile usare una tecnologia basata su un sistema di archiviazione e sulla rete.</span><span class="sxs-lookup"><span data-stu-id="867f7-213">You can use network and storage system technology to make it highly available.</span></span>

![Figura 1: Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="867f7-215">_**Figura 1:** Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="867f7-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="867f7-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Spazio di archiviazione condiviso</span><span class="sxs-lookup"><span data-stu-id="867f7-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="867f7-217">La figura 1 illustra anche un cluster di archiviazione condiviso a due nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="867f7-218">In un cluster di archiviazione condiviso locale tutti i nodi del cluster rilevano lo spazio di archiviazione condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="867f7-219">Un meccanismo di blocco protegge i dati da danneggiamenti.</span><span class="sxs-lookup"><span data-stu-id="867f7-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="867f7-220">Tutti i nodi possono rilevare se si verifica un errore in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="867f7-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="867f7-221">Se si verifica un errore in un nodo, il nodo rimanente assume la proprietà delle risorse di archiviazione e assicura la disponibilità dei servizi.</span><span class="sxs-lookup"><span data-stu-id="867f7-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-222">Non sono necessari dischi condivisi per la disponibilità elevata con alcune applicazioni DBMS, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="867f7-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="867f7-223">La funzionalità AlwaysOn di SQL Server replica i file di dati e di log del sistema DBMS dal disco locale di un nodo del cluster nel disco locale di un altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="867f7-224">In tal caso, la configurazione del cluster Windows non richiede un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="867f7-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Rete e risoluzione dei nomi</span><span class="sxs-lookup"><span data-stu-id="867f7-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="867f7-226">I computer client raggiungono il cluster tramite un indirizzo IP virtuale e un nome host virtuale forniti dal server DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="867f7-227">I nodi locali e il server DNS possono gestire più indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="867f7-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="867f7-228">In un'installazione tipica si usano due o più connessioni di rete:</span><span class="sxs-lookup"><span data-stu-id="867f7-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="867f7-229">Una connessione dedicata all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="867f7-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="867f7-230">Una connessione di rete interna al cluster per l'heartbeat</span><span class="sxs-lookup"><span data-stu-id="867f7-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="867f7-231">Una rete pubblica usata dai client per la connessione al cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="867f7-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="867f7-233">Rispetto alle distribuzioni bare metal o cloud privato, sono necessari passaggi aggiuntivi per configurare un Windows Server Failover Clustering in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="867f7-234">Quando si crea un disco cluster condiviso, è necessario impostare diversi indirizzi IP e nomi host virtuali per l'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="867f7-235">Questo articolo illustra i concetti chiave e i passaggi aggiuntivi necessari per creare un cluster SAP Central Services a disponibilità elevata in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="867f7-236">Viene illustrato come configurare lo strumento SIOS DataKeeper di terze parti e come configurare il servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="867f7-237">È possibile usare questi strumenti per creare un cluster di failover Windows con un controllo di condivisione file in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso][sap-ha-guide-figure-1001]

<span data-ttu-id="867f7-239">_**Figura 2:** Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso_</span><span class="sxs-lookup"><span data-stu-id="867f7-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="867f7-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco condiviso in Azure con SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="867f7-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="867f7-241">È necessario spazio di archiviazione condiviso del cluster per un'istanza di SAP ASCS/SCS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="867f7-242">A partire da settembre 2016, Azure non offre spazio di archiviazione condiviso da usare per creare un cluster di archiviazione condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="867f7-243">È possibile usare il software SIOS DataKeeper Cluster Edition di terze parti per creare una risorsa di archiviazione con mirroring che simula la risorsa di archiviazione condivisa del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="867f7-244">La soluzione SIOS fornisce la replica di dati sincrona in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="867f7-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="867f7-245">Per creare una risorsa disco condiviso per un cluster, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="867f7-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="867f7-246">Collegare un disco aggiuntivo a ogni macchina virtuale (VM) in una configurazione cluster Windows.</span><span class="sxs-lookup"><span data-stu-id="867f7-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="867f7-247">Eseguire SIOS DataKeeper Cluster Edition in entrambi i nodi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="867f7-248">Configurare SIOS DataKeeper Cluster Edition per eseguire il mirroring del contenuto del volume collegato del disco aggiuntivo dalla macchina virtuale di origine al volume collegato del disco aggiuntivo della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="867f7-249">SIOS DataKeeper astrae i volumi locali di origine e di destinazione e quindi li presenta a Windows Server Failover Clustering come un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="867f7-250">Altre informazioni su [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="867f7-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="867f7-252">_**Figura 3:** Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-253">Non sono necessari dischi condivisi per la disponibilità elevata con alcuni prodotti DBMS, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="867f7-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="867f7-254">La funzionalità AlwaysOn di SQL Server replica i file di dati e di log del sistema DBMS dal disco locale di un nodo del cluster nel disco locale di un altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="867f7-255">In questo caso, la configurazione del cluster Windows non richiede un disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="867f7-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Risoluzione dei nomi in Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="867f7-257">La piattaforma cloud di Azure non consente di configurare indirizzi IP virtuali, ad esempio indirizzi IP mobili.</span><span class="sxs-lookup"><span data-stu-id="867f7-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="867f7-258">È necessaria una soluzione alternativa per configurare un indirizzo IP virtuale per poter raggiungere la risorsa cluster nel cloud.</span><span class="sxs-lookup"><span data-stu-id="867f7-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="867f7-259">Azure include un servizio di bilanciamento del carico interno nel servizio Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="867f7-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="867f7-260">Con il servizio di bilanciamento del carico interno, i client raggiungono il cluster tramite l'indirizzo IP virtuale del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="867f7-261">È necessario distribuire il servizio di bilanciamento del carico interni nel gruppo di risorse che contiene i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="867f7-262">Configurare quindi tutte le necessarie regole di port forwarding con le porte probe del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="867f7-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="867f7-263">I client possono connettersi tramite il nome host virtuale.</span><span class="sxs-lookup"><span data-stu-id="867f7-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="867f7-264">Il server DNS risolve l'indirizzo IP del cluster e il servizio di bilanciamento del carico interno gestisce il port forwarding al nodo attivo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="867f7-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Disponibilità elevata di SAP NetWeaver nell'infrastruttura distribuita come servizio (IaaS) di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="867f7-266">Per ottenere la disponibilità elevata per le applicazioni SAP, ad esempio per i componenti software SAP, è necessario proteggere i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="867f7-267">Istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-267">SAP Application Server instance</span></span>
* <span data-ttu-id="867f7-268">Istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="867f7-269">Server DBMS</span><span class="sxs-lookup"><span data-stu-id="867f7-269">DBMS server</span></span>

<span data-ttu-id="867f7-270">Per altre informazioni sulla protezione dei componenti SAP in scenari a disponibilità elevata, vedere [Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="867f7-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="867f7-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Server applicazioni SAP a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="867f7-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="867f7-272">In genere non è necessaria una specifica soluzione a disponibilità elevata per le istanze e del server applicazioni SAP e di dialogo.</span><span class="sxs-lookup"><span data-stu-id="867f7-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="867f7-273">La disponibilità elevata si ottiene tramite la ridondanza e si dovranno configurare più istanze delle finestre di dialogo in istanze diverse di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="867f7-274">È necessario avere almeno due istanze dell'applicazione SAP installate in due istanze di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Server applicazioni SAP a disponibilità elevata][sap-ha-guide-figure-2000]

<span data-ttu-id="867f7-276">_**Figura 4:** Server applicazioni SAP a disponibilità elevata_</span><span class="sxs-lookup"><span data-stu-id="867f7-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="867f7-277">È necessario inserire tutte le macchine virtuali che ospitano le istanze del server applicazioni SAP nello stesso set di disponibilità di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="867f7-278">Un set di disponibilità di Azure assicura che:</span><span class="sxs-lookup"><span data-stu-id="867f7-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="867f7-279">Tutte le macchine virtuali facciano parte dello stesso dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="867f7-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="867f7-280">Un dominio di aggiornamento, ad esempio, verifica che le macchine virtuali non vengano aggiornate contemporaneamente durante i tempi di inattività per la manutenzione pianificati.</span><span class="sxs-lookup"><span data-stu-id="867f7-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="867f7-281">Tutte le macchine virtuali facciano parte dello stesso dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="867f7-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="867f7-282">Un dominio di errore, ad esempio, verifica che le macchine virtuali vengano distribuite in modo che nessun singolo punto di guasto influisca sulla disponibilità di tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="867f7-283">Altre informazioni su come [gestire la disponibilità delle macchine virtuali][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="867f7-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="867f7-284">Solo dischi non gestiti: poiché l'account di archiviazione di Azure è un potenziale singolo punto di guasto, è importante avere almeno due account di archiviazione di Azure, in cui verranno distribuite almeno due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="867f7-285">In una configurazione ideale, il disco di ogni macchina virtuale che esegue l'istanza di una finestra di dialogo SAP verrà distribuito in un account di archiviazione diverso.</span><span class="sxs-lookup"><span data-stu-id="867f7-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="867f7-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Istanza di SAP ASCS/SCS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="867f7-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="867f7-287">La figura 5 è un esempio di istanza di SAP ASCS/SCS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-2001]

<span data-ttu-id="867f7-289">_**Figura 5:** Istanza di SAP ASCS/SCS a disponibilità elevata_</span><span class="sxs-lookup"><span data-stu-id="867f7-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="867f7-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Disponibilità elevata dell'istanza di SAP ASCS/SCS con Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="867f7-291">Rispetto alle distribuzioni bare metal o cloud privato, sono necessari passaggi aggiuntivi per configurare un Windows Server Failover Clustering in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="867f7-292">Per creare un cluster di failover Windows, sono necessari un disco cluster condiviso, più indirizzi IP, più nomi host virtuali e un servizio di bilanciamento del carico interno di Azure per il clustering di un'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="867f7-293">Questo argomento viene illustrato più dettagliatamente più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="867f7-293">We discuss this in more detail later in the article.</span></span>

![Figura 6: Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="867f7-295">_**Figura 6:** Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="867f7-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Istanza di DBMS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="867f7-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="867f7-297">Anche DBMS è un singolo punto di contatto in un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="867f7-298">È necessario proteggerlo usando una soluzione a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="867f7-299">La figura 7 illustra una soluzione a disponibilità elevata SQL Server AlwaysOn in Azure con Windows Server Failover Clustering e il bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="867f7-300">SQL Server AlwaysOn replica i file di dati e di log DBMS usando la replica DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="867f7-301">In questo caso, non sono necessari dischi condivisi di cluster, semplificando così l'intera configurazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Figura 7: Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn][sap-ha-guide-figure-2003]

<span data-ttu-id="867f7-303">_**Figura 7:** Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn_</span><span class="sxs-lookup"><span data-stu-id="867f7-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="867f7-304">Per altre informazioni sul clustering di SQL Server in Azure con il modello di distribuzione Azure Resource Manager, vedere questi articoli:</span><span class="sxs-lookup"><span data-stu-id="867f7-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="867f7-305">[Configurare manualmente il gruppo di disponibilità AlwaysOn in Macchine virtuali di Azure con Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="867f7-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="867f7-306">[Configurare un servizio di bilanciamento del carico interno di Azure per un gruppo di disponibilità AlwaysOn in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="867f7-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="867f7-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Scenari di distribuzione a disponibilità elevata end-to-end</span><span class="sxs-lookup"><span data-stu-id="867f7-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="867f7-308">Scenario di distribuzione usando il modello architetturale 1</span><span class="sxs-lookup"><span data-stu-id="867f7-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="867f7-309">La figura 8 illustra un esempio di architettura a disponibilità elevata SAP NetWeaver in Azure per **un** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="867f7-310">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="867f7-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="867f7-311">Un cluster dedicato viene usato per l'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="867f7-312">Un cluster dedicato viene usato per l'istanza di DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="867f7-313">Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="867f7-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Modello architetturale 1 a disponibilità elevata di SAP, con cluster dedicato per ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="867f7-315">_**Figura 8:** Modello architetturale 1 a disponibilità elevata di SAP, cluster dedicati per ASCS/SCS e DBMS_</span><span class="sxs-lookup"><span data-stu-id="867f7-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="867f7-316">Scenario di distribuzione usando il modello architetturale 2</span><span class="sxs-lookup"><span data-stu-id="867f7-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="867f7-317">La figura 9 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **un** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="867f7-318">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="867f7-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="867f7-319">Un cluster dedicato viene usato **sia** per l'istanza di SAP ASCS/SCS che per l'istanza di DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="867f7-320">Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="867f7-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="867f7-322">_**Figura 9:** Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS_</span><span class="sxs-lookup"><span data-stu-id="867f7-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="867f7-323">Scenario di distribuzione usando il modello architetturale 3</span><span class="sxs-lookup"><span data-stu-id="867f7-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="867f7-324">La figura 10 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **due** sistemi SAP, con &lt;SID1&gt; e &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="867f7-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="867f7-325">Questo scenario viene configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="867f7-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="867f7-326">Un cluster dedicato viene usato **sia** per l'istanza di SAP ASCS/SCS SID1 *che* per l'istanza di SAP ASCS/SCS SID2 (un cluster).</span><span class="sxs-lookup"><span data-stu-id="867f7-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="867f7-327">Un cluster dedicato viene usato per DBMS SID1 e un altro cluster dedicato viene usato per DBMS SID2 (due cluster).</span><span class="sxs-lookup"><span data-stu-id="867f7-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="867f7-328">Le istanze del server applicazioni SAP per il SID1 del sistema SAP hanno proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="867f7-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="867f7-329">Le istanze del server applicazioni SAP per il SID2 del sistema SAP hanno proprie VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="867f7-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="867f7-331">_**Figura 10:** Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="867f7-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Preparare l'infrastruttura</span><span class="sxs-lookup"><span data-stu-id="867f7-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="867f7-333">Preparare l'infrastruttura per il modello architetturale 1</span><span class="sxs-lookup"><span data-stu-id="867f7-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="867f7-334">I modelli di Azure Resource Manager per SAP consentono di semplificare la distribuzione delle risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="867f7-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="867f7-335">I modelli a tre livelli in Azure Resource Manager supportano anche scenari a disponibilità elevata, ad esempio il modello architetturale 1 con due cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="867f7-336">Ogni cluster è un singolo punto di guasto SAP per SAP ASCS/SCS e DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="867f7-337">Ecco dove è possibile ottenere i modelli di Azure Resource Manager per questo scenario di esempio descritto in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="867f7-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="867f7-338">Immagine di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="867f7-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="867f7-339">Immagine di Azure Marketplace che usa Managed Disks</span><span class="sxs-lookup"><span data-stu-id="867f7-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="867f7-340">Immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="867f7-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="867f7-341">Immagine personalizzata che usa Managed Disks</span><span class="sxs-lookup"><span data-stu-id="867f7-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="867f7-342">Per preparare l'infrastruttura per il modello architetturale 1:</span><span class="sxs-lookup"><span data-stu-id="867f7-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="867f7-343">Nella casella **SYSTEMAVAILABILITY** nel pannello **Parametri** del portale di Azure selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="867f7-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="867f7-345">_**Figura 11:** Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP_</span><span class="sxs-lookup"><span data-stu-id="867f7-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="867f7-346">I modelli creano:</span><span class="sxs-lookup"><span data-stu-id="867f7-346">The templates create:</span></span>

  * <span data-ttu-id="867f7-347">**Macchine virtuali**:</span><span class="sxs-lookup"><span data-stu-id="867f7-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="867f7-348">Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-di-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="867f7-349">Macchine virtuali del cluster ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="867f7-350">Cluster DBMS: <*SIDSistemaSAP*>-db-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="867f7-351">**Schede di rete per tutte le macchine virtuali, con gli indirizzi IP associati**:</span><span class="sxs-lookup"><span data-stu-id="867f7-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="867f7-352"><*SIDSistemaSAP*>-nic-di-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="867f7-353"><*SIDSistemaSAP*>-nic-ascs-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="867f7-354"><*SIDSistemaSAP*>-nic-db-<*Numero*></span><span class="sxs-lookup"><span data-stu-id="867f7-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="867f7-355">**Account di archiviazione di Azure (solo dischi non gestiti)**</span><span class="sxs-lookup"><span data-stu-id="867f7-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="867f7-356">**Gruppi di disponibilità** per:</span><span class="sxs-lookup"><span data-stu-id="867f7-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="867f7-357">Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="867f7-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="867f7-358">Macchine virtuali del cluster SAP ASCS/SCS: <*SIDSistemaSAP*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="867f7-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="867f7-359">Macchine virtuali del cluster DBMS: <*SIDSistemaSAP*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="867f7-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="867f7-360">**Servizio di bilanciamento del carico interno di Azure**:</span><span class="sxs-lookup"><span data-stu-id="867f7-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="867f7-361">Con tutte le porte per l'istanza di ASCS/SCS e l'indirizzo IP <*SIDSistemaSAP*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="867f7-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="867f7-362">Con tutte le porte per l'istanza di SQL Server DBMS e l'indirizzo IP <*SIDSistemaSAP*>-lb-db</span><span class="sxs-lookup"><span data-stu-id="867f7-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="867f7-363">**Gruppo di sicurezza di rete**: <*SIDSistemaSAP*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="867f7-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="867f7-364">Con una porta Remote Desktop Protocol (RDP) esterna aperta alla macchina virtuale <*SIDSistemaSAP*>-ascs-0</span><span class="sxs-lookup"><span data-stu-id="867f7-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-365">Tutti gli indirizzi IP delle schede di rete e i servizi di bilanciamento del carico interno di Azure sono **dinamici** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="867f7-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="867f7-366">Impostarli come indirizzi IP **statici**,</span><span class="sxs-lookup"><span data-stu-id="867f7-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="867f7-367">Questo argomento verrà illustrato più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="867f7-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="867f7-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Distribuire macchine virtuali con connettività di rete aziendale (cross-premise) da usare in fase di produzione</span><span class="sxs-lookup"><span data-stu-id="867f7-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="867f7-369">Per i sistemi SAP di produzione, distribuire le macchine virtuali di Azure con la [connettività di rete aziendale (cross-premise)][planning-guide-2.2] usando la rete VPN da sito a sito di Azure o Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="867f7-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-370">È possibile usare l'istanza di Rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="867f7-371">La rete virtuale e la subnet sono già state create e preparate.</span><span class="sxs-lookup"><span data-stu-id="867f7-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="867f7-372">Nella casella **NEWOREXISTINGSUBNET** nel pannello **Parametri** del portale di Azure selezionare **existing**.</span><span class="sxs-lookup"><span data-stu-id="867f7-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="867f7-373">Nella casella**SUBNETID** aggiungere la stringa completa del campo SubnetID relativo alla rete di Azure preparata, in cui si prevede di distribuire le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="867f7-374">Per ottenere un elenco di tutte le subnet di rete di Azure, eseguire questo comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="867f7-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="867f7-375">Il campo **ID** contiene il valore di **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="867f7-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="867f7-376">Per ottenere un elenco di tutti i valori **SUBNETID**, eseguire questo comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="867f7-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="867f7-377">Il valore di **SUBNETID** è il seguente:</span><span class="sxs-lookup"><span data-stu-id="867f7-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="867f7-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Distribuire delle istanze di SAP solo cloud a scopo di test e dimostrazione</span><span class="sxs-lookup"><span data-stu-id="867f7-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="867f7-379">È possibile distribuire il sistema SAP a disponibilità elevata in un modello di distribuzione solo cloud.</span><span class="sxs-lookup"><span data-stu-id="867f7-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="867f7-380">Questo tipo di distribuzione è utile soprattutto per i casi d'uso di demo e test.</span><span class="sxs-lookup"><span data-stu-id="867f7-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="867f7-381">Non è adatto per i casi d'uso in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="867f7-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="867f7-382">Nella casella **NEWOREXISTINGSUBNET** nel pannello **Parametri** del portale di Azure selezionare **new**.</span><span class="sxs-lookup"><span data-stu-id="867f7-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="867f7-383">Lasciare vuoto il campo **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="867f7-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="867f7-384">Il modello di Azure Resource Manager per SAP crea automaticamente la rete virtuale di Azure e la subnet.</span><span class="sxs-lookup"><span data-stu-id="867f7-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-385">È anche necessario distribuire almeno una macchina virtuale dedicata per Active Directory e DNS nella stessa istanza di Rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="867f7-386">Il modello non crea queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="867f7-387">Preparare l'infrastruttura per il modello architetturale 2</span><span class="sxs-lookup"><span data-stu-id="867f7-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="867f7-388">È possibile usare questo modello di Azure Resource Manager in modo che SAP semplifichi la distribuzione delle risorse di infrastruttura necessarie per il modello di SAP 2.</span><span class="sxs-lookup"><span data-stu-id="867f7-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="867f7-389">Ecco dove è possibile ottenere i modelli di Azure Resource Manager per questo scenario di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="867f7-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="867f7-390">Immagine di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="867f7-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="867f7-391">Immagine di Azure Marketplace che usa Managed Disks</span><span class="sxs-lookup"><span data-stu-id="867f7-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="867f7-392">Immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="867f7-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="867f7-393">Immagine personalizzata che usa Managed Disks</span><span class="sxs-lookup"><span data-stu-id="867f7-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="867f7-394">Preparare l'infrastruttura per il modello architetturale 3</span><span class="sxs-lookup"><span data-stu-id="867f7-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="867f7-395">È possibile preparare l'infrastruttura e configurare SAP per **più SID**.</span><span class="sxs-lookup"><span data-stu-id="867f7-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="867f7-396">Ad esempio, è possibile aggiungere un'istanza di SAP ASCS/SCS aggiuntiva in una configurazione di cluster *esistente*.</span><span class="sxs-lookup"><span data-stu-id="867f7-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="867f7-397">Per altre informazioni, vedere [Configurare un'istanza di SAP ASCS/SCS aggiuntiva in una configurazione di cluster esistente per creare una configurazione di SAP a più SID in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="867f7-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="867f7-398">Per creare un nuovo cluster con più SID, è possibile usare i [modelli di avvio rapido su GitHub](https://github.com/Azure/azure-quickstart-templates) relativi a più SID.</span><span class="sxs-lookup"><span data-stu-id="867f7-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="867f7-399">Per creare un nuovo cluster a più SID, è necessario distribuire i tre modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="867f7-400">Modello di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="867f7-401">Modello di database</span><span class="sxs-lookup"><span data-stu-id="867f7-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="867f7-402">Modello dei server applicazioni</span><span class="sxs-lookup"><span data-stu-id="867f7-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="867f7-403">Le sezioni seguenti includono informazioni dettagliate sui modelli e parametri che è necessario fornire nei modelli.</span><span class="sxs-lookup"><span data-stu-id="867f7-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="867f7-404"><a name="ASCS-SCS-template"></a> Modello di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="867f7-405">Il modello di ASCS/SCS distribuisce due macchine virtuali che possono essere usate per creare un cluster di failover di Windows che ospita più istanze di ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="867f7-406">Per configurare il modello a più SID di ASCS/SCS nel [modello a più SID di ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image] o il [modello a più SID di ASCS/SCS con Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], immettere i valori per i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="867f7-407">**Resource Prefix**.</span><span class="sxs-lookup"><span data-stu-id="867f7-407">**Resource Prefix**.</span></span>  <span data-ttu-id="867f7-408">Impostare il prefisso della risorsa, che viene usato per assegnare un prefisso a tutte le risorse create durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="867f7-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="867f7-409">Poiché le risorse non appartengono a un solo sistema SAP, il prefisso della risorsa non è il SID di un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="867f7-410">Il prefisso deve essere compreso fra **tre e sei caratteri**.</span><span class="sxs-lookup"><span data-stu-id="867f7-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="867f7-411">**Stack Type**.</span><span class="sxs-lookup"><span data-stu-id="867f7-411">**Stack Type**.</span></span> <span data-ttu-id="867f7-412">Selezionare il tipo di stack del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="867f7-413">A seconda del tipo di stack, Azure Load Balancer dispone di un indirizzo IP (solo ABAP o Java) o due indirizzi IP (ABAP+Java) privati per ogni sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="867f7-414">**OS Type**.</span><span class="sxs-lookup"><span data-stu-id="867f7-414">**OS Type**.</span></span> <span data-ttu-id="867f7-415">Selezionare il sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="867f7-416">**SAP System Count**.</span><span class="sxs-lookup"><span data-stu-id="867f7-416">**SAP System Count**.</span></span> <span data-ttu-id="867f7-417">Selezionare il numero di sistemi SAP da installare in questo cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="867f7-418">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="867f7-418">**System Availability**.</span></span> <span data-ttu-id="867f7-419">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="867f7-419">Select **HA**.</span></span>
  -  <span data-ttu-id="867f7-420">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="867f7-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="867f7-421">Creare un nuovo utente che può essere usato per accedere alla macchina.</span><span class="sxs-lookup"><span data-stu-id="867f7-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="867f7-422">**New Or Existing Subnet**.</span><span class="sxs-lookup"><span data-stu-id="867f7-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="867f7-423">Impostare se devono essere create una nuova rete virtuale e una nuova subnet o se deve essere usata una subnet esistente.</span><span class="sxs-lookup"><span data-stu-id="867f7-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="867f7-424">Se è già presente una rete virtuale connessa alla rete locale, selezionare **existing**.</span><span class="sxs-lookup"><span data-stu-id="867f7-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="867f7-425">**Subnet Id**.</span><span class="sxs-lookup"><span data-stu-id="867f7-425">**Subnet Id**.</span></span> <span data-ttu-id="867f7-426">Impostare l'ID della subnet a cui devono essere connesse le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="867f7-427">Selezionare la subnet della rete virtuale ExpressRoute o VPN per connettere la macchina virtuale alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="867f7-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="867f7-428">L'ID in genere è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="867f7-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="867f7-429">/subscriptions/<*ID sottoscrizione*>/resourceGroups/<*nomegruppo risorse*>/providers/Microsoft.Network/VirtualNetwork/<*nome rete virtuale*>>/subnets/<*nome subnet*></span><span class="sxs-lookup"><span data-stu-id="867f7-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="867f7-430">Il modello consente di distribuire un'istanza di Azure Load Balancer che supporta più sistemi SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="867f7-431">Le istanze ASCS sono configurate per i numeri di istanza 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="867f7-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="867f7-432">Le istanze SCS sono configurate per i numeri di istanza 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="867f7-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="867f7-433">Le istanze di ASCS Enqueue Replication Server (ERS) (Linux) sono configurate per i numeri di istanza 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="867f7-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="867f7-434">Le istanze SCS ERS (solo Linux) sono configurate per i numeri di istanza 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="867f7-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="867f7-435">Il bilanciamento del carico contiene 1 (2 per Linux) indirizzo VIP, 1 indirizzo VIP per ASCS/SCS e 1 indirizzo VIP per ERS (solo Linux).</span><span class="sxs-lookup"><span data-stu-id="867f7-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="867f7-436">L'elenco seguente contiene tutte le regole di bilanciamento del carico (dove x è il numero del sistema SAP, ad esempio, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="867f7-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="867f7-437">Porte specifiche di Windows per ogni sistema SAP 445, 5985</span><span class="sxs-lookup"><span data-stu-id="867f7-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="867f7-438">Porte ASCS (numero di istanza x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="867f7-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="867f7-439">Porte SCS (numero di istanza x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="867f7-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="867f7-440">Porte ASCS ERS in Linux (numero di istanza x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="867f7-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="867f7-441">Porte SCS ERS in Linux (numero di istanza x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="867f7-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="867f7-442">Il servizio di bilanciamento del carico viene configurato per l'uso delle porte probe seguenti (dove x è il numero del sistema SAP, ad esempio 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="867f7-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="867f7-443">Porta probe del servizio di bilanciamento del carico interno ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="867f7-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="867f7-444">Porta probe del servizio di bilanciamento del carico interno ERS (solo Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="867f7-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="867f7-445"><a name="database-template"></a> Modello di database</span><span class="sxs-lookup"><span data-stu-id="867f7-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="867f7-446">Il modello di database distribuisce una o due macchine virtuali che è possibile usare per installare il sistema di gestione di database relazionali (RDBMS) per un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="867f7-447">Se, ad esempio, si distribuisce un modello ASCS/SCS per 5 sistemi SAP, è necessario distribuire questo modello cinque volte.</span><span class="sxs-lookup"><span data-stu-id="867f7-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="867f7-448">Per configurare il modello a più SID di database nel [modello a più SID di database][sap-templates-3-tier-multisid-db-marketplace-image] o il [modello a più SID di database con Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], immettere i valori per i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="867f7-449">**Sap System Id**.</span><span class="sxs-lookup"><span data-stu-id="867f7-449">**Sap System Id**.</span></span> <span data-ttu-id="867f7-450">Immettere l'ID del sistema SAP che si vuole installare.</span><span class="sxs-lookup"><span data-stu-id="867f7-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="867f7-451">L'ID verrà usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="867f7-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="867f7-452">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="867f7-452">**Os Type**.</span></span> <span data-ttu-id="867f7-453">Selezionare il sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="867f7-454">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="867f7-454">**Dbtype**.</span></span> <span data-ttu-id="867f7-455">Selezionare il tipo di database che si vuole installare nel cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="867f7-456">Selezionare **SQL** se si vuole installare Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="867f7-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="867f7-457">Selezionare **HANA** se si prevede di installare SAP HANA nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="867f7-458">Assicurarsi di selezionare il tipo di sistema operativo corretto: selezionare **Windows** per SQL e selezionare una distribuzione Linux per HANA.</span><span class="sxs-lookup"><span data-stu-id="867f7-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="867f7-459">L'istanza di Azure Load Balancer connessa alle macchine virtuali verrà configurata per supportare il tipo di database selezionato:</span><span class="sxs-lookup"><span data-stu-id="867f7-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="867f7-460">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="867f7-460">**SQL**.</span></span> <span data-ttu-id="867f7-461">Il servizio di bilanciamento del carico caricherà la porta di bilanciamento 1433.</span><span class="sxs-lookup"><span data-stu-id="867f7-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="867f7-462">Assicurarsi di usare questa porta per l'installazione di SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="867f7-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="867f7-463">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="867f7-463">**HANA**.</span></span> <span data-ttu-id="867f7-464">Il servizio di bilanciamento del carico caricherà le porta di bilanciamento 35015 e 35017.</span><span class="sxs-lookup"><span data-stu-id="867f7-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="867f7-465">Assicurarsi di installare SAP HANA con il numero di istanza **50**.</span><span class="sxs-lookup"><span data-stu-id="867f7-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="867f7-466">Il servizio bilanciamento del carico userà la porta probe 62550.</span><span class="sxs-lookup"><span data-stu-id="867f7-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="867f7-467">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="867f7-467">**Sap System Size**.</span></span> <span data-ttu-id="867f7-468">Impostare il numero di SAPS forniti dal nuovo sistema.</span><span class="sxs-lookup"><span data-stu-id="867f7-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="867f7-469">Se non si è certi del numero di SAPS necessari per il sistema, chiedere all'integratore di sistemi o al partner tecnologico SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="867f7-470">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="867f7-470">**System Availability**.</span></span> <span data-ttu-id="867f7-471">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="867f7-471">Select **HA**.</span></span>
  -  <span data-ttu-id="867f7-472">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="867f7-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="867f7-473">Creare un nuovo utente che può essere usato per accedere alla macchina.</span><span class="sxs-lookup"><span data-stu-id="867f7-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="867f7-474">**Subnet Id**.</span><span class="sxs-lookup"><span data-stu-id="867f7-474">**Subnet Id**.</span></span> <span data-ttu-id="867f7-475">Immettere l'ID della subnet usata durante la distribuzione del modello di ASCS/SCS o l'ID della subnet creata come parte della distribuzione del modello di ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="867f7-476"><a name="application-servers-template"></a> Modello dei server applicazioni</span><span class="sxs-lookup"><span data-stu-id="867f7-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="867f7-477">Il modello dei server applicazioni consente di distribuire due o più macchine virtuali che possono essere usate come istanze del server applicazioni SAP per un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="867f7-478">Se, ad esempio, si distribuisce un modello ASCS/SCS per 5 sistemi SAP, è necessario distribuire questo modello cinque volte.</span><span class="sxs-lookup"><span data-stu-id="867f7-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="867f7-479">Per configurare il modello a più SID dei server applicazioni nel [modello a più SID dei server applicazioni][sap-templates-3-tier-multisid-apps-marketplace-image] o il [modello a più SID dei server applicazioni con Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], immettere i valori per i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="867f7-480">**Sap System Id**.</span><span class="sxs-lookup"><span data-stu-id="867f7-480">**Sap System Id**.</span></span> <span data-ttu-id="867f7-481">Immettere l'ID del sistema SAP che si vuole installare.</span><span class="sxs-lookup"><span data-stu-id="867f7-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="867f7-482">L'ID verrà usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="867f7-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="867f7-483">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="867f7-483">**Os Type**.</span></span> <span data-ttu-id="867f7-484">Selezionare il sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="867f7-485">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="867f7-485">**Sap System Size**.</span></span> <span data-ttu-id="867f7-486">Numero di SAPS forniti dal nuovo sistema.</span><span class="sxs-lookup"><span data-stu-id="867f7-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="867f7-487">Se non si è certi del numero di SAPS necessari per il sistema, chiedere all'integratore di sistemi o al partner tecnologico SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="867f7-488">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="867f7-488">**System Availability**.</span></span> <span data-ttu-id="867f7-489">Selezionare **HA**.</span><span class="sxs-lookup"><span data-stu-id="867f7-489">Select **HA**.</span></span>
  -  <span data-ttu-id="867f7-490">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="867f7-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="867f7-491">Creare un nuovo utente che può essere usato per accedere alla macchina.</span><span class="sxs-lookup"><span data-stu-id="867f7-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="867f7-492">**Subnet Id**.</span><span class="sxs-lookup"><span data-stu-id="867f7-492">**Subnet Id**.</span></span> <span data-ttu-id="867f7-493">Immettere l'ID della subnet usata durante la distribuzione del modello di ASCS/SCS o l'ID della subnet creata come parte della distribuzione del modello di ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="867f7-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="867f7-495">In questo esempio lo spazio degli indirizzi della rete virtuale di Azure è 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="867f7-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="867f7-496">Esiste una subnet denominata **Subnet**, con un intervallo di indirizzi di 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="867f7-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="867f7-497">Tutte le macchine virtuali e i servizi di bilanciamento del carico interni vengono distribuiti in questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="867f7-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867f7-498">Non apportare modifiche alle impostazioni di rete nel sistema operativo guest,</span><span class="sxs-lookup"><span data-stu-id="867f7-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="867f7-499">inclusi indirizzi IP, server DNS e la subnet.</span><span class="sxs-lookup"><span data-stu-id="867f7-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="867f7-500">Configurare tutte le impostazioni di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="867f7-501">Il servizio Dynamic Host Configuration Protocol (DHCP) propaga le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="867f7-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="867f7-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Indirizzi IP DNS</span><span class="sxs-lookup"><span data-stu-id="867f7-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="867f7-503">Per impostare gli indirizzi IP DNS necessari, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="867f7-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="867f7-504">Nel pannello **Server DSN** del portale di Azure verificare che l'opzione **Server DNS** della rete virtuale sia impostata su **DNS personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="867f7-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="867f7-505">Selezionare le impostazioni in base al tipo di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="867f7-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="867f7-506">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="867f7-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="867f7-507">[Connettività di rete aziendale (cross-premise)][planning-guide-2.2]: aggiungere gli indirizzi IP dei server DNS locali.</span><span class="sxs-lookup"><span data-stu-id="867f7-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="867f7-508">È possibile estendere i server DNS locali alle macchine virtuali in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="867f7-509">In tale scenario è possibile aggiungere gli indirizzi IP delle macchine virtuali di Azure in cui si esegue il servizio DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="867f7-510">[Distribuzione solo cloud][planning-guide-2.1]: distribuire una macchina virtuale aggiuntiva nella stessa istanza di Rete virtuale che funge da server DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="867f7-511">Aggiungere gli indirizzi IP delle macchine virtuali di Azure configurate per l'esecuzione del servizio DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Figura 12: Configurare i server DNS per Rete virtuale di Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="867f7-513">_**Figura 12:** Configurare i server DNS per Rete virtuale di Azure_</span><span class="sxs-lookup"><span data-stu-id="867f7-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="867f7-514">Se si modificano gli indirizzi IP dei server DNS, è necessario riavviare le macchine virtuali di Azure per applicare la modifica e propagare i nuovi server DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="867f7-515">Nell'esempio il servizio DNS viene installato e configurato in queste macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="867f7-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="867f7-516">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-516">Virtual machine role</span></span> | <span data-ttu-id="867f7-517">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-517">Virtual machine host name</span></span> | <span data-ttu-id="867f7-518">Nome scheda di rete</span><span class="sxs-lookup"><span data-stu-id="867f7-518">Network card name</span></span> | <span data-ttu-id="867f7-519">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="867f7-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="867f7-520">Primo server DNS</span><span class="sxs-lookup"><span data-stu-id="867f7-520">First DNS server</span></span> |<span data-ttu-id="867f7-521">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="867f7-521">domcontr-0</span></span> |<span data-ttu-id="867f7-522">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="867f7-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="867f7-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="867f7-523">10.0.0.10</span></span> |
| <span data-ttu-id="867f7-524">Secondo server DNS</span><span class="sxs-lookup"><span data-stu-id="867f7-524">Second DNS server</span></span> |<span data-ttu-id="867f7-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="867f7-525">domcontr-1</span></span> |<span data-ttu-id="867f7-526">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="867f7-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="867f7-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="867f7-527">10.0.0.11</span></span> |

### <span data-ttu-id="867f7-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Nomi host e indirizzi IP statici per l'istanza in cluster di SAP ASCS/SCS e l'istanza in cluster di DBMS</span><span class="sxs-lookup"><span data-stu-id="867f7-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="867f7-529">Per una distribuzione locale, sono necessari questi nomi host e indirizzi IP riservati:</span><span class="sxs-lookup"><span data-stu-id="867f7-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="867f7-530">Ruolo nome host virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-530">Virtual host name role</span></span> | <span data-ttu-id="867f7-531">Nome host virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-531">Virtual host name</span></span> | <span data-ttu-id="867f7-532">Indirizzo IP statico virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="867f7-533">Primo nome host virtuale del cluster SAP ASCS/SCS (per la gestione del cluster)</span><span class="sxs-lookup"><span data-stu-id="867f7-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="867f7-534">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="867f7-534">pr1-ascs-vir</span></span> |<span data-ttu-id="867f7-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="867f7-535">10.0.0.42</span></span> |
| <span data-ttu-id="867f7-536">Nome host virtuale dell'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="867f7-537">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="867f7-537">pr1-ascs-sap</span></span> |<span data-ttu-id="867f7-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="867f7-538">10.0.0.43</span></span> |
| <span data-ttu-id="867f7-539">Secondo nome host virtuale del cluster SAP DBMS (gestione del cluster)</span><span class="sxs-lookup"><span data-stu-id="867f7-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="867f7-540">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="867f7-540">pr1-dbms-vir</span></span> |<span data-ttu-id="867f7-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="867f7-541">10.0.0.32</span></span> |

<span data-ttu-id="867f7-542">Quando si crea il cluster, creare i nomi host virtuale **pr1-ascs-vir** e **pr1-dbms-vir** e gli indirizzi IP associati che gestiscono il cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="867f7-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="867f7-543">Per informazioni su come eseguire questa operazione, vedere [Raccogliere i nodi del cluster in una configurazione cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="867f7-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="867f7-544">È possibile creare manualmente gli altri due nomi host virtuale, **pr1-ascs-sap** e **pr1-dbms-sap** e gli indirizzi IP associati, nel server DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="867f7-545">L'istanza di SAP ASCS/SCS in cluster e l'istanza di DBMS in cluster usano queste risorse,</span><span class="sxs-lookup"><span data-stu-id="867f7-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="867f7-546">Per informazioni su come eseguire questa operazione, vedere [Creare un nome host virtuale per un'istanza di SAP ASCS/SCS in cluster][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="867f7-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="867f7-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Impostare gli indirizzi IP statici per le macchine virtuali SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="867f7-548">Dopo avere distribuito le macchine virtuali da usare nel cluster, è necessario impostare gli indirizzi IP statici per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="867f7-549">Eseguire questa operazione nella configurazione di Rete virtuale di Azure e non nel sistema operativo guest.</span><span class="sxs-lookup"><span data-stu-id="867f7-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="867f7-550">Nel portale di Azure selezionare **Gruppo di risorse** > **Scheda di rete** > **Impostazioni** > **Indirizzo IP**.</span><span class="sxs-lookup"><span data-stu-id="867f7-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="867f7-551">Nel pannello **Indirizzi IP** in **Assegnazione** selezionare **Statica**.</span><span class="sxs-lookup"><span data-stu-id="867f7-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="867f7-552">Nella casella **Indirizzo IP** immettere l'indirizzo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="867f7-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="867f7-553">Se si modifica l'indirizzo IP della scheda di rete, è necessario riavviare le macchine virtuali di Azure per applicare la modifica.</span><span class="sxs-lookup"><span data-stu-id="867f7-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Figura 13: Impostare gli indirizzi IP statici per la scheda di rete di ogni macchina virtuale][sap-ha-guide-figure-3002]

  <span data-ttu-id="867f7-555">_**Figura 13:** Impostare gli indirizzi IP statici per la scheda di rete di ogni macchina virtuale_</span><span class="sxs-lookup"><span data-stu-id="867f7-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="867f7-556">Ripetere questo passaggio per tutte le interfacce di rete, ovvero per tutte le macchine virtuali, incluse le macchine virtuali che si vuole usare per il servizio Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="867f7-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="867f7-557">In questo esempio vengono usate le macchine virtuali e gli indirizzi IP statici seguenti:</span><span class="sxs-lookup"><span data-stu-id="867f7-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="867f7-558">Ruolo macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-558">Virtual machine role</span></span> | <span data-ttu-id="867f7-559">Nome host macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="867f7-559">Virtual machine host name</span></span> | <span data-ttu-id="867f7-560">Nome scheda di rete</span><span class="sxs-lookup"><span data-stu-id="867f7-560">Network card name</span></span> | <span data-ttu-id="867f7-561">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="867f7-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="867f7-562">Prima istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-562">First SAP Application Server instance</span></span> |<span data-ttu-id="867f7-563">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="867f7-563">pr1-di-0</span></span> |<span data-ttu-id="867f7-564">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="867f7-564">pr1-nic-di-0</span></span> |<span data-ttu-id="867f7-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="867f7-565">10.0.0.50</span></span> |
| <span data-ttu-id="867f7-566">Seconda istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="867f7-567">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="867f7-567">pr1-di-1</span></span> |<span data-ttu-id="867f7-568">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="867f7-568">pr1-nic-di-1</span></span> |<span data-ttu-id="867f7-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="867f7-569">10.0.0.51</span></span> |
| <span data-ttu-id="867f7-570">...</span><span class="sxs-lookup"><span data-stu-id="867f7-570">...</span></span> |<span data-ttu-id="867f7-571">...</span><span class="sxs-lookup"><span data-stu-id="867f7-571">...</span></span> |<span data-ttu-id="867f7-572">...</span><span class="sxs-lookup"><span data-stu-id="867f7-572">...</span></span> |<span data-ttu-id="867f7-573">...</span><span class="sxs-lookup"><span data-stu-id="867f7-573">...</span></span> |
| <span data-ttu-id="867f7-574">Ultima istanza del server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="867f7-575">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="867f7-575">pr1-di-5</span></span> |<span data-ttu-id="867f7-576">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="867f7-576">pr1-nic-di-5</span></span> |<span data-ttu-id="867f7-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="867f7-577">10.0.0.55</span></span> |
| <span data-ttu-id="867f7-578">Primo nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="867f7-579">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="867f7-579">pr1-ascs-0</span></span> |<span data-ttu-id="867f7-580">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="867f7-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="867f7-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="867f7-581">10.0.0.40</span></span> |
| <span data-ttu-id="867f7-582">Secondo nodo del cluster per l'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="867f7-583">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="867f7-583">pr1-ascs-1</span></span> |<span data-ttu-id="867f7-584">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="867f7-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="867f7-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="867f7-585">10.0.0.41</span></span> |
| <span data-ttu-id="867f7-586">Primo nodo del cluster per l'istanza di DBMS</span><span class="sxs-lookup"><span data-stu-id="867f7-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="867f7-587">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="867f7-587">pr1-db-0</span></span> |<span data-ttu-id="867f7-588">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="867f7-588">pr1-nic-db-0</span></span> |<span data-ttu-id="867f7-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="867f7-589">10.0.0.30</span></span> |
| <span data-ttu-id="867f7-590">Secondo nodo del cluster per l'istanza di DBMS</span><span class="sxs-lookup"><span data-stu-id="867f7-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="867f7-591">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="867f7-591">pr1-db-1</span></span> |<span data-ttu-id="867f7-592">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="867f7-592">pr1-nic-db-1</span></span> |<span data-ttu-id="867f7-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="867f7-593">10.0.0.31</span></span> |

### <span data-ttu-id="867f7-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Impostare un indirizzo IP statico per il servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="867f7-595">Il modello di Azure Resource Manager per SAP crea un servizio di bilanciamento del carico interno di Azure usato per il cluster dell'istanza di SAP ASCS/SCS e per il cluster DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867f7-596">L'indirizzo IP del nome host virtuale di SAP ASCS/SCS è lo stesso del servizio di bilanciamento del carico interno di SAP ASCS/SCS: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="867f7-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="867f7-597">L'indirizzo IP del nome virtuale di DBMS è lo stesso del servizio di bilanciamento del carico interno di DBMS: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="867f7-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="867f7-598">Per impostare un indirizzo IP statico per il servizio di bilanciamento del carico interno di Azure:</span><span class="sxs-lookup"><span data-stu-id="867f7-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="867f7-599">La distribuzione iniziale imposta l'indirizzo IP del servizio di bilanciamento del carico interno come **dinamico**.</span><span class="sxs-lookup"><span data-stu-id="867f7-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="867f7-600">Nel pannello **Indirizzi IP** del portale di Azure selezionare **Statica** in **Assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="867f7-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="867f7-601">Impostare l'indirizzo IP del bilanciamento del carico interno **pr1-lb-ascs** sull'indirizzo IP del nome host virtuale dell'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="867f7-602">Impostare l'indirizzo IP del bilanciamento del carico interno **pr1-lb-dbms** sull'indirizzo IP del nome host virtuale dell'istanza di DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Figura 14: Impostare indirizzi IP statici per il servizio di bilanciamento del carico interno per l'istanza di SAP ASCS/SCS][sap-ha-guide-figure-3003]

  <span data-ttu-id="867f7-604">_**Figura 14:** Impostare indirizzi IP statici per il servizio di bilanciamento del carico interno per l'istanza di SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="867f7-605">Nell'esempio sono presenti due servizi di bilanciamento del carico interno di Azure con questi indirizzi IP statici:</span><span class="sxs-lookup"><span data-stu-id="867f7-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="867f7-606">Ruolo del servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-606">Azure internal load balancer role</span></span> | <span data-ttu-id="867f7-607">Nome del servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-607">Azure internal load balancer name</span></span> | <span data-ttu-id="867f7-608">Indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="867f7-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="867f7-609">Servizio di bilanciamento del carico interno dell'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="867f7-610">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="867f7-610">pr1-lb-ascs</span></span> |<span data-ttu-id="867f7-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="867f7-611">10.0.0.43</span></span> |
| <span data-ttu-id="867f7-612">Servizio di bilanciamento del carico interno di SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="867f7-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="867f7-613">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="867f7-613">pr1-lb-dbms</span></span> |<span data-ttu-id="867f7-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="867f7-614">10.0.0.33</span></span> |


### <span data-ttu-id="867f7-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="867f7-616">Il modello di Azure Resource Manager per SAP crea le porte necessarie:</span><span class="sxs-lookup"><span data-stu-id="867f7-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="867f7-617">Un'istanza di ABAP ASCS, con il numero di istanza predefinito **00**</span><span class="sxs-lookup"><span data-stu-id="867f7-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="867f7-618">Un'istanza di Java SCS, con il numero di istanza predefinito **01**</span><span class="sxs-lookup"><span data-stu-id="867f7-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="867f7-619">Quando si installa l'istanza di SAP ASCS/SCS, è necessario usare il numero di istanza predefinito **00** per l'istanza di ABAP ASCS e il numero di istanza predefinito **01** per l'istanza di Java SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="867f7-620">Creare quindi gli endpoint di bilanciamento del carico interno obbligatori per le porte di SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="867f7-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="867f7-621">Per creare gli endpoint di bilanciamento del carico interno obbligatori, creare prima questi endpoint per le porte di SAP NetWeaver ABAP ASCS:</span><span class="sxs-lookup"><span data-stu-id="867f7-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="867f7-622">Servizio/nome regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="867f7-622">Service/load balancing rule name</span></span> | <span data-ttu-id="867f7-623">Numeri porte predefinite</span><span class="sxs-lookup"><span data-stu-id="867f7-623">Default port numbers</span></span> | <span data-ttu-id="867f7-624">Porte concrete per (istanza ASCS con l'istanza numero 00) (ERS con 10)</span><span class="sxs-lookup"><span data-stu-id="867f7-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="867f7-625">Server di accodamento/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="867f7-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="867f7-626">32<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-627">3200</span><span class="sxs-lookup"><span data-stu-id="867f7-627">3200</span></span> |
| <span data-ttu-id="867f7-628">Server messaggi ABAP/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="867f7-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="867f7-629">36<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-630">3600</span><span class="sxs-lookup"><span data-stu-id="867f7-630">3600</span></span> |
| <span data-ttu-id="867f7-631">Messaggio ABAP interno/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="867f7-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="867f7-632">39<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-633">3900</span><span class="sxs-lookup"><span data-stu-id="867f7-633">3900</span></span> |
| <span data-ttu-id="867f7-634">HTTP server messaggi/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="867f7-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="867f7-635">81<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-636">8100</span><span class="sxs-lookup"><span data-stu-id="867f7-636">8100</span></span> |
| <span data-ttu-id="867f7-637">SAP Start Service ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="867f7-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="867f7-638">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="867f7-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="867f7-639">50013</span><span class="sxs-lookup"><span data-stu-id="867f7-639">50013</span></span> |
| <span data-ttu-id="867f7-640">SAP Start Service ASCS HTTPS/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="867f7-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="867f7-641">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="867f7-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="867f7-642">50014</span><span class="sxs-lookup"><span data-stu-id="867f7-642">50014</span></span> |
| <span data-ttu-id="867f7-643">Replica di accodamento/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="867f7-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="867f7-644">5<*NumeroIstanza*>16</span><span class="sxs-lookup"><span data-stu-id="867f7-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="867f7-645">50016</span><span class="sxs-lookup"><span data-stu-id="867f7-645">50016</span></span> |
| <span data-ttu-id="867f7-646">SAP Start Service ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="867f7-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="867f7-647">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="867f7-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="867f7-648">51013</span><span class="sxs-lookup"><span data-stu-id="867f7-648">51013</span></span> |
| <span data-ttu-id="867f7-649">SAP Start Service ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="867f7-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="867f7-650">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="867f7-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="867f7-651">51014</span><span class="sxs-lookup"><span data-stu-id="867f7-651">51014</span></span> |
| <span data-ttu-id="867f7-652">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="867f7-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="867f7-653">5985</span><span class="sxs-lookup"><span data-stu-id="867f7-653">5985</span></span> |
| <span data-ttu-id="867f7-654">Condivisione file *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="867f7-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="867f7-655">445</span><span class="sxs-lookup"><span data-stu-id="867f7-655">445</span></span> |

<span data-ttu-id="867f7-656">_**Tabella 1:** Numeri di porta delle istanze di SAP NetWeaver ABAP ASCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="867f7-657">Creare quindi questi endpoint di bilanciamento del carico per le porte SCS di SAP NetWeaver Java:</span><span class="sxs-lookup"><span data-stu-id="867f7-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="867f7-658">Servizio/nome regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="867f7-658">Service/load balancing rule name</span></span> | <span data-ttu-id="867f7-659">Numeri porte predefinite</span><span class="sxs-lookup"><span data-stu-id="867f7-659">Default port numbers</span></span> | <span data-ttu-id="867f7-660">Porte concrete per (istanza SCS con numero di istanza 01) (ERS con 11)</span><span class="sxs-lookup"><span data-stu-id="867f7-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="867f7-661">Server di accodamento/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="867f7-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="867f7-662">32<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-663">3201</span><span class="sxs-lookup"><span data-stu-id="867f7-663">3201</span></span> |
| <span data-ttu-id="867f7-664">Server gateway/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="867f7-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="867f7-665">33<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-666">3301</span><span class="sxs-lookup"><span data-stu-id="867f7-666">3301</span></span> |
| <span data-ttu-id="867f7-667">Server messaggi Java/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="867f7-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="867f7-668">39<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-669">3901</span><span class="sxs-lookup"><span data-stu-id="867f7-669">3901</span></span> |
| <span data-ttu-id="867f7-670">HTTP server messaggi/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="867f7-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="867f7-671">81<*NumeroIstanza*></span><span class="sxs-lookup"><span data-stu-id="867f7-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="867f7-672">8101</span><span class="sxs-lookup"><span data-stu-id="867f7-672">8101</span></span> |
| <span data-ttu-id="867f7-673">SAP Start Service SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="867f7-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="867f7-674">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="867f7-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="867f7-675">50113</span><span class="sxs-lookup"><span data-stu-id="867f7-675">50113</span></span> |
| <span data-ttu-id="867f7-676">SAP Start Service SCS HTTPS/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="867f7-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="867f7-677">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="867f7-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="867f7-678">50114</span><span class="sxs-lookup"><span data-stu-id="867f7-678">50114</span></span> |
| <span data-ttu-id="867f7-679">Replica di accodamento/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="867f7-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="867f7-680">5<*NumeroIstanza*>16</span><span class="sxs-lookup"><span data-stu-id="867f7-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="867f7-681">50116</span><span class="sxs-lookup"><span data-stu-id="867f7-681">50116</span></span> |
| <span data-ttu-id="867f7-682">SAP Start Service ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="867f7-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="867f7-683">5<*NumeroIstanza*>13</span><span class="sxs-lookup"><span data-stu-id="867f7-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="867f7-684">51113</span><span class="sxs-lookup"><span data-stu-id="867f7-684">51113</span></span> |
| <span data-ttu-id="867f7-685">SAP Start Service ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="867f7-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="867f7-686">5<*NumeroIstanza*>14</span><span class="sxs-lookup"><span data-stu-id="867f7-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="867f7-687">51114</span><span class="sxs-lookup"><span data-stu-id="867f7-687">51114</span></span> |
| <span data-ttu-id="867f7-688">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="867f7-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="867f7-689">5985</span><span class="sxs-lookup"><span data-stu-id="867f7-689">5985</span></span> |
| <span data-ttu-id="867f7-690">Condivisione file *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="867f7-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="867f7-691">445</span><span class="sxs-lookup"><span data-stu-id="867f7-691">445</span></span> |

<span data-ttu-id="867f7-692">_**Tabella 2:** Numeri di porta delle istanze di SAP NetWeaver Java SCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure][sap-ha-guide-figure-3004]

<span data-ttu-id="867f7-694">_**Figura 15:** Regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure_</span><span class="sxs-lookup"><span data-stu-id="867f7-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="867f7-695">Impostare l'indirizzo IP del servizio di bilanciamento del carico **pr1-lb-dbms** sull'indirizzo IP del nome host virtuale dell'istanza di DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="867f7-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Modificare le regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="867f7-697">Per usare numeri diversi per le istanze di SAP ASCS o SCS, è necessario cambiare i nomi e i valori di queste porte rispetto ai valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="867f7-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="867f7-698">Nel portale di Azure selezionare **<*SID*>-lb-ascs load balancer** > **Regole di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="867f7-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="867f7-699">Per tutte le regole di bilanciamento del carico appartenenti all'istanza di SAP ASCS o SCS, modificare questi valori:</span><span class="sxs-lookup"><span data-stu-id="867f7-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="867f7-700">Nome</span><span class="sxs-lookup"><span data-stu-id="867f7-700">Name</span></span>
  * <span data-ttu-id="867f7-701">Porta</span><span class="sxs-lookup"><span data-stu-id="867f7-701">Port</span></span>
  * <span data-ttu-id="867f7-702">Porta back-end</span><span class="sxs-lookup"><span data-stu-id="867f7-702">Back-end port</span></span>

  <span data-ttu-id="867f7-703">Ad esempio, per sostituire il numero di istanza di ASCS predefinito 00 con 31, è necessario apportare le modifiche per tutte le porte elencate nella tabella 1.</span><span class="sxs-lookup"><span data-stu-id="867f7-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="867f7-704">Ecco un esempio di aggiornamento per la porta *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="867f7-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Modificare le regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure][sap-ha-guide-figure-3005]

  <span data-ttu-id="867f7-706">_**Figura 16:** Modificare le regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure_</span><span class="sxs-lookup"><span data-stu-id="867f7-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="867f7-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Aggiungere macchine virtuali Windows al dominio</span><span class="sxs-lookup"><span data-stu-id="867f7-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="867f7-708">Dopo avere assegnato un indirizzo IP statico alle macchine virtuali, aggiungere le macchine virtuali al dominio.</span><span class="sxs-lookup"><span data-stu-id="867f7-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Figura 17: Aggiungere una macchina virtuale a un dominio][sap-ha-guide-figure-3006]

<span data-ttu-id="867f7-710">_**Figura 17:** Aggiungere una macchina virtuale a un dominio_</span><span class="sxs-lookup"><span data-stu-id="867f7-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="867f7-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Aggiungere le voci del Registro di sistema in entrambi i nodi del cluster per l'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="867f7-712">Azure Load Balancer ha un servizio di bilanciamento del carico interno che chiude le connessioni quando rimangono inattive per un periodo di tempo impostato (timeout di inattività).</span><span class="sxs-lookup"><span data-stu-id="867f7-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="867f7-713">I processi di lavoro SAP nelle istanze delle finestre di dialogo aprono le connessioni al processo di accodamento SAP non appena deve essere inviata la prima richiesta di accodamento/rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="867f7-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="867f7-714">Queste connessioni restano in genere stabilite fino al riavvio del processo di lavoro o del processo di accodamento.</span><span class="sxs-lookup"><span data-stu-id="867f7-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="867f7-715">Se tuttavia la connessione rimane inattiva per un determinato periodo di tempo, il servizio di bilanciamento del carico interno di Azure chiude le connessioni.</span><span class="sxs-lookup"><span data-stu-id="867f7-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="867f7-716">Questo non è un problema perché il processo di lavoro SAP ristabilisce la connessione al processo di accodamento se non esiste più.</span><span class="sxs-lookup"><span data-stu-id="867f7-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="867f7-717">Queste attività sono documentate nelle tracce degli sviluppatori dei processi SAP, ma creano una grande quantità di contenuti aggiuntivi in tali tracce.</span><span class="sxs-lookup"><span data-stu-id="867f7-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="867f7-718">È consigliabile modificare i parametri `KeepAliveTime` e `KeepAliveInterval` TCP/IP in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="867f7-719">Combinare queste modifiche nei parametri TCP/IP con i parametri del profilo SAP, illustrati più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="867f7-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="867f7-720">Per aggiungere le voci del Registro di sistema in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS, aggiungere prima queste voci del Registro di sistema di Windows in entrambi i nodi del cluster Windows per SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="867f7-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="867f7-721">Path</span><span class="sxs-lookup"><span data-stu-id="867f7-721">Path</span></span> | <span data-ttu-id="867f7-722">HKLM\System\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="867f7-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="867f7-723">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="867f7-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="867f7-724">Tipo di variabile</span><span class="sxs-lookup"><span data-stu-id="867f7-724">Variable type</span></span> |<span data-ttu-id="867f7-725">REG_DWORD (decimale)</span><span class="sxs-lookup"><span data-stu-id="867f7-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="867f7-726">Valore</span><span class="sxs-lookup"><span data-stu-id="867f7-726">Value</span></span> |<span data-ttu-id="867f7-727">120000</span><span class="sxs-lookup"><span data-stu-id="867f7-727">120000</span></span> |
| <span data-ttu-id="867f7-728">Collegamento alla documentazione</span><span class="sxs-lookup"><span data-stu-id="867f7-728">Link to documentation</span></span> |[<span data-ttu-id="867f7-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="867f7-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="867f7-730">_**Tabella 3:** Modificare il primo parametro TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="867f7-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="867f7-731">Aggiungere quindi le voci del Registro di sistema Windows in entrambi i nodi del cluster Windows per SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="867f7-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="867f7-732">Path</span><span class="sxs-lookup"><span data-stu-id="867f7-732">Path</span></span> | <span data-ttu-id="867f7-733">HKLM\System\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="867f7-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="867f7-734">Nome variabile</span><span class="sxs-lookup"><span data-stu-id="867f7-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="867f7-735">Tipo di variabile</span><span class="sxs-lookup"><span data-stu-id="867f7-735">Variable type</span></span> |<span data-ttu-id="867f7-736">REG_DWORD (decimale)</span><span class="sxs-lookup"><span data-stu-id="867f7-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="867f7-737">Valore</span><span class="sxs-lookup"><span data-stu-id="867f7-737">Value</span></span> |<span data-ttu-id="867f7-738">120000</span><span class="sxs-lookup"><span data-stu-id="867f7-738">120000</span></span> |
| <span data-ttu-id="867f7-739">Collegamento alla documentazione</span><span class="sxs-lookup"><span data-stu-id="867f7-739">Link to documentation</span></span> |[<span data-ttu-id="867f7-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="867f7-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="867f7-741">_**Tabella 4:** Modificare il secondo parametro TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="867f7-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="867f7-742">**Per applicare le modifiche, riavviare entrambi i nodi del cluster**.</span><span class="sxs-lookup"><span data-stu-id="867f7-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="867f7-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurare un cluster di Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="867f7-744">La configurazione di un cluster Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="867f7-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="867f7-745">Raccolta dei nodi del cluster in una configurazione di cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="867f7-746">Configurazione di un controllo di condivisione file del cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="867f7-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Raccogliere i nodi del cluster in una configurazione cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="867f7-748">Nella procedura guidata Aggiungi ruoli e funzionalità aggiungere il clustering di failover a entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="867f7-749">Configurare il cluster di failover usando Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="867f7-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="867f7-750">In Gestione Cluster di Failover selezionare **Crea cluster**, quindi aggiungere solo il nome del primo cluster, il nodo A. Non aggiungere il secondo nodo; aggiungere il secondo nodo in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="867f7-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Figura 18: Aggiungere il nome del server o della macchina virtuale del primo nodo del cluster][sap-ha-guide-figure-3007]

  <span data-ttu-id="867f7-752">_**Figura 18:** Aggiungere il nome del server o della macchina virtuale del primo nodo del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="867f7-753">Immettere il nome della rete (nome host virtuale) del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Figura 19: Definire il nome del cluster][sap-ha-guide-figure-3008]

  <span data-ttu-id="867f7-755">_**Figura 19:** Definire il nome del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="867f7-756">Dopo avere creato il cluster, eseguire un test di convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![Figura 20: Eseguire il controllo di convalida del cluster][sap-ha-guide-figure-3009]

  <span data-ttu-id="867f7-758">_**Figura 20:** Eseguire il controllo di convalida del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="867f7-759">A questo punto del processo è possibile ignorare gli avvisi sui dischi.</span><span class="sxs-lookup"><span data-stu-id="867f7-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="867f7-760">Più avanti si aggiungeranno un controllo di condivisione file e i dischi condivisi SIOS.</span><span class="sxs-lookup"><span data-stu-id="867f7-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="867f7-761">In questa fase, non è necessario un quorum.</span><span class="sxs-lookup"><span data-stu-id="867f7-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Figura 21: Nessun disco quorum trovato][sap-ha-guide-figure-3010]

  <span data-ttu-id="867f7-763">_**Figura 21:** Nessun disco quorum trovato_</span><span class="sxs-lookup"><span data-stu-id="867f7-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: La risorsa del cluster principale richiede un nuovo indirizzo IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="867f7-765">_**Figura 22:** La risorsa del cluster principale richiede un nuovo indirizzo IP_</span><span class="sxs-lookup"><span data-stu-id="867f7-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="867f7-766">Modificare l'indirizzo IP del servizio cluster principale.</span><span class="sxs-lookup"><span data-stu-id="867f7-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="867f7-767">Il cluster non può essere avviato finché non si cambia l'indirizzo IP del servizio cluster principale perché l'indirizzo IP del server punta a uno dei nodi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="867f7-768">Eseguire questa operazione nella pagina **Proprietà** della risorsa IP del servizio cluster principale.</span><span class="sxs-lookup"><span data-stu-id="867f7-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="867f7-769">Ad esempio, è necessario assegnare un indirizzo IP (in questo esempio **10.0.0.42**) per il nome host virtuale del cluster **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="867f7-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: Nella finestra di dialogo Proprietà modificare l'indirizzo IP][sap-ha-guide-figure-3012]

  <span data-ttu-id="867f7-771">_**Figura 23:** Nella finestra di dialogo **Proprietà** modificare l'indirizzo IP_</span><span class="sxs-lookup"><span data-stu-id="867f7-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Figura 24: Assegnare l'indirizzo IP riservato per il cluster][sap-ha-guide-figure-3013]

  <span data-ttu-id="867f7-773">_**Figura 24:** Assegnare l'indirizzo IP riservato per il cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="867f7-774">Portare online il nome host virtuale del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-774">Bring the cluster virtual host name online.</span></span>

  ![Figura 25: Il servizio principale del cluster è in esecuzione con l'indirizzo IP corretto][sap-ha-guide-figure-3014]

  <span data-ttu-id="867f7-776">_**Figura 25:** Il servizio principale del cluster è in esecuzione con l'indirizzo IP corretto_</span><span class="sxs-lookup"><span data-stu-id="867f7-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="867f7-777">Aggiungere il secondo nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-777">Add the second cluster node.</span></span>

  <span data-ttu-id="867f7-778">Ora che il servizio principale del cluster è attivo e in esecuzione, è possibile aggiungere il secondo nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Figura 26: Aggiungere il secondo nodo del cluster][sap-ha-guide-figure-3015]

  <span data-ttu-id="867f7-780">_**Figura 26:** Aggiungere il secondo nodo del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="867f7-781">Immettere un nome host del secondo nodo cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-781">Enter a name for the second cluster node host.</span></span>

  ![Figura 27: Immettere il nome host del secondo nodo cluster][sap-ha-guide-figure-3016]

  <span data-ttu-id="867f7-783">_**Figura 27:** Immettere il nome host del secondo nodo cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="867f7-784">Assicurarsi che la casella di controllo **Aggiungi tutte le risorse di archiviazione idonee al cluster** **NON** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="867f7-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: Non selezionare la casella di controllo][sap-ha-guide-figure-3017]

  <span data-ttu-id="867f7-786">_**Figura 28:** **NON** selezionare la casella di controllo_</span><span class="sxs-lookup"><span data-stu-id="867f7-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="867f7-787">È possibile ignorare gli avvisi relativi al quorum e ai dischi.</span><span class="sxs-lookup"><span data-stu-id="867f7-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="867f7-788">Si imposterà il quorum e si condividerà il disco in un secondo momento, come descritto in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3] (Installazione di SIOS DataKeeper Cluster Edition per il disco di condivisione del cluster SAP ASCS/SCS).</span><span class="sxs-lookup"><span data-stu-id="867f7-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorare gli avvisi sul quorum del disco][sap-ha-guide-figure-3018]

  <span data-ttu-id="867f7-790">_**Figura 29:** Ignorare gli avvisi sul quorum del disco_</span><span class="sxs-lookup"><span data-stu-id="867f7-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="867f7-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurare il controllo di condivisione file del cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="867f7-792">La configurazione di un controllo di condivisione file del cluster prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="867f7-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="867f7-793">Creazione di una condivisione file</span><span class="sxs-lookup"><span data-stu-id="867f7-793">Creating a file share</span></span>
- <span data-ttu-id="867f7-794">Impostazione del quorum del controllo di condivisione file in Gestione cluster di failover</span><span class="sxs-lookup"><span data-stu-id="867f7-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="867f7-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="867f7-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="867f7-796">Selezionare un controllo di condivisione file invece di un disco quorum.</span><span class="sxs-lookup"><span data-stu-id="867f7-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="867f7-797">SIOS DataKeeper supporta questa opzione.</span><span class="sxs-lookup"><span data-stu-id="867f7-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="867f7-798">Negli esempi di questo articolo, il controllo di condivisione file è nel server Active Directory/DNS in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="867f7-799">Il controllo di condivisione file è denominato **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="867f7-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="867f7-800">Poiché sarà stata configurata una connessione VPN ad Azure (tramite la VPN da sito a sito o Azure ExpressRoute), il servizio Active Directory/DNS è locale e non è adatto all'esecuzione di un controllo di condivisione file.</span><span class="sxs-lookup"><span data-stu-id="867f7-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="867f7-801">Se il servizio Active Directory/DNS viene eseguito solo in locale, non configurare il controllo di condivisione file nel sistema operativo Windows con Active Directory/DNS eseguito in locale.</span><span class="sxs-lookup"><span data-stu-id="867f7-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="867f7-802">La latenza di rete tra i nodi del cluster in esecuzione in Azure e Active Directory/DNS in locale potrebbe essere eccessiva e causare problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="867f7-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="867f7-803">Assicurarsi di configurare il controllo di condivisione file in una macchina virtuale di Azure in esecuzione vicino al nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="867f7-804">L'unità del quorum richiede almeno 1.024 MB di spazio disponibile.</span><span class="sxs-lookup"><span data-stu-id="867f7-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="867f7-805">Si consiglia un valore di 2.048 MB di spazio disponibile per l'unità quorum.</span><span class="sxs-lookup"><span data-stu-id="867f7-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="867f7-806">Aggiungere l'oggetto del nome cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-806">Add the cluster name object.</span></span>

  ![Figura 30: Assegnare le autorizzazioni nella condivisione per l'oggetto nome cluster][sap-ha-guide-figure-3019]

  <span data-ttu-id="867f7-808">_**Figura 30:** Assegnare le autorizzazioni nella condivisione per l'oggetto nome cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="867f7-809">Assicurarsi che le autorizzazioni includano l'autorità di modificare i dati nella condivisione per l'oggetto nome cluster (in questo esempio **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="867f7-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="867f7-810">Per aggiungere l'oggetto nome cluster all'elenco, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="867f7-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="867f7-811">Modificare il filtro per cercare gli oggetti computer, oltre a quelli illustrati nella figura 31.</span><span class="sxs-lookup"><span data-stu-id="867f7-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Figura 31: Modificare i tipi di oggetto per includere i computer][sap-ha-guide-figure-3020]

  <span data-ttu-id="867f7-813">_**Figura 31:** Modificare i tipi di oggetto per includere i computer_</span><span class="sxs-lookup"><span data-stu-id="867f7-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Figura 32: Selezionare la casella di controllo Computer][sap-ha-guide-figure-3021]

  <span data-ttu-id="867f7-815">_**Figura 32:** Selezionare la casella di controllo **Computer**_</span><span class="sxs-lookup"><span data-stu-id="867f7-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="867f7-816">Immettere l'oggetto nome del cluster, come illustrato nella figura 31.</span><span class="sxs-lookup"><span data-stu-id="867f7-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="867f7-817">Poiché il record è già stato creato, è possibile modificare le autorizzazioni, come illustrato nella figura 30.</span><span class="sxs-lookup"><span data-stu-id="867f7-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="867f7-818">Selezionare la scheda **Sicurezza** della condivisione e quindi impostare autorizzazioni più dettagliate per l'oggetto del nome cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Figura 33: Impostare gli attributi di sicurezza per l'oggetto nome cluster sul quorum della condivisione file][sap-ha-guide-figure-3022]

  <span data-ttu-id="867f7-820">_**Figura 33:** Impostare gli attributi di sicurezza per l'oggetto nome cluster sul quorum della condivisione file_</span><span class="sxs-lookup"><span data-stu-id="867f7-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="867f7-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Impostare il quorum del controllo di condivisione file in Gestione cluster di failover</span><span class="sxs-lookup"><span data-stu-id="867f7-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="867f7-822">Aprire Configurazione guidata quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Avviare la procedura guidata Configura impostazioni quorum del cluster][sap-ha-guide-figure-3023]

  <span data-ttu-id="867f7-824">_**Figura 34:** Avviare la procedura guidata Configura impostazioni quorum del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="867f7-825">Nella pagina **Selezione configurazione quorum** selezionare **Seleziona il quorum di controllo**.</span><span class="sxs-lookup"><span data-stu-id="867f7-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Figura 35: Configurazioni del quorum tra cui è possibile scegliere][sap-ha-guide-figure-3024]

  <span data-ttu-id="867f7-827">_**Figura 35:** Configurazioni del quorum tra cui è possibile scegliere_</span><span class="sxs-lookup"><span data-stu-id="867f7-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="867f7-828">Nella pagina **Seleziona il quorum di controllo** selezionare **Configura condivisione file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="867f7-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figura 36: Selezionare il controllo di condivisione file][sap-ha-guide-figure-3025]

  <span data-ttu-id="867f7-830">_**Figura 36:** Selezionare il controllo di condivisione file_</span><span class="sxs-lookup"><span data-stu-id="867f7-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="867f7-831">Immettere il percorso UNC della condivisione file (in questo esempio \\domcontr-0\FSW) .</span><span class="sxs-lookup"><span data-stu-id="867f7-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="867f7-832">Selezionare **Avanti** per visualizzare un elenco delle modifiche che è possibile apportare.</span><span class="sxs-lookup"><span data-stu-id="867f7-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![Figura 37: Definire il percorso della condivisione file per la condivisione di controllo][sap-ha-guide-figure-3026]

  <span data-ttu-id="867f7-834">_**Figura 37:** Definire il percorso della condivisione file per la condivisione di controllo_</span><span class="sxs-lookup"><span data-stu-id="867f7-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="867f7-835">Selezionare le modifiche desiderate e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="867f7-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="867f7-836">È necessario riconfigurare correttamente il cluster, come illustrato nella figura 38.</span><span class="sxs-lookup"><span data-stu-id="867f7-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![Figura 38: Conferma della riconfigurazione del cluster][sap-ha-guide-figure-3027]

  <span data-ttu-id="867f7-838">_**Figura 38:** Conferma della riconfigurazione del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="867f7-839">Dopo aver installato correttamente il Cluster di failover Windows, è necessario modificare alcune soglie per adattare il rilevamento del failover alle condizioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="867f7-840">I parametri da modificare sono documentati in questo blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span><span class="sxs-lookup"><span data-stu-id="867f7-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="867f7-841">Supponendo che le due VM che compongono la configurazione del cluster Windows per ASCS/SCS siano nella stessa SubNet, è necessario modificare i parametri seguenti impostando i valori indicati:</span><span class="sxs-lookup"><span data-stu-id="867f7-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="867f7-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="867f7-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="867f7-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="867f7-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="867f7-844">Queste impostazioni sono state testate con i clienti e hanno fornito un buon compromesso in quanto da un lato sono sufficientemente resilienti</span><span class="sxs-lookup"><span data-stu-id="867f7-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="867f7-845">e dall'altro offrono un failover sufficientemente rapido in condizioni di errore reale del software SAP o del nodo/VM.</span><span class="sxs-lookup"><span data-stu-id="867f7-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="867f7-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Installare SIOS DataKeeper Cluster Edition per il disco di condivisione del cluster SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="867f7-847">Ora è disponibile una configurazione funzionante di Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="867f7-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="867f7-848">ma, per installare un'istanza di SAP ASCS/SCS, è necessaria una risorsa disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="867f7-849">Non è possibile creare le risorse del disco condiviso necessarie in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="867f7-850">SIOS DataKeeper Cluster Edition è una soluzione di terze parti che è possibile usare per creare le risorse disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="867f7-851">L'installazione di SIOS DataKeeper Cluster Edition per il disco di condivisione del cluster SAP ASCS/SCS prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="867f7-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="867f7-852">Aggiunta di .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="867f7-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="867f7-853">Installazione di SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="867f7-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="867f7-854">Configurazione di SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="867f7-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="867f7-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Aggiungere .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="867f7-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="867f7-856">Microsoft .NET Framework 3.5 non viene attivato né installato automaticamente in Windows Server 2012 R2,</span><span class="sxs-lookup"><span data-stu-id="867f7-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="867f7-857">Poiché SIOS DataKeeper richiede l'installazione di .NET Framework in tutti i nodi in cui si installa DataKeeper, è necessario installare .NET Framework 3.5 nel sistema operativo guest di tutte le macchine virtuali nel cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="867f7-858">È possibile aggiungere .NET Framework 3.5 in due modi:</span><span class="sxs-lookup"><span data-stu-id="867f7-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="867f7-859">Usare l'Aggiunta guidata ruoli e funzionalità in Windows come illustrato nella figura 39.</span><span class="sxs-lookup"><span data-stu-id="867f7-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Installare .NET Framework 3.5 usando l'Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3028]

  <span data-ttu-id="867f7-861">_**Figura 39:** Installare .NET Framework 3.5 usando l'Aggiunta guidata ruoli e funzionalità_</span><span class="sxs-lookup"><span data-stu-id="867f7-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Figura 40: Indicatore di stato dell'installazione quando si installa .NET Framework 3.5 usando l'Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3029]

  <span data-ttu-id="867f7-863">_**Figura 40:** Indicatore di stato dell'installazione quando si installa .NET Framework 3.5 usando l'Aggiunta guidata ruoli e funzionalità_</span><span class="sxs-lookup"><span data-stu-id="867f7-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="867f7-864">Usare lo strumento da riga di comando dism.exe.</span><span class="sxs-lookup"><span data-stu-id="867f7-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="867f7-865">Per questo tipo di installazione è necessario accedere alla directory SxS nei supporti di installazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="867f7-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="867f7-866">A un prompt dei comandi con privilegi elevati digitare:</span><span class="sxs-lookup"><span data-stu-id="867f7-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="867f7-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Installare SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="867f7-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="867f7-868">Installare SIOS DataKeeper Cluster Edition in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="867f7-869">Per creare una risorsa di archiviazione condivisa virtuale con SIOS DataKeeper, creare un mirror sincronizzato e quindi simulare la risorsa di archiviazione condivisa del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="867f7-870">Prima di installare il software SIOS, creare l'utente di dominio **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="867f7-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-871">Aggiungere l'utente **DataKeeperSvc** al gruppo **Administrators locale** in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="867f7-872">Per installare SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="867f7-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="867f7-873">Installare il software SIOS in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-873">Install the SIOS software on both cluster nodes.</span></span>

  ![Programma di installazione SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Prima schermata dell'installazione di SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="867f7-876">_**Figura 41:** Prima schermata dell'installazione di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="867f7-877">Nella finestra di dialogo illustrata nella figura 42 selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="867f7-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: DataKeeper segnala che un servizio verrà disabilitato][sap-ha-guide-figure-3032]

  <span data-ttu-id="867f7-879">_**Figura 42:** DataKeeper segnala che un servizio verrà disabilitato_</span><span class="sxs-lookup"><span data-stu-id="867f7-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="867f7-880">Nella finestra di dialogo illustrata nella figura 43, si consiglia di selezionare **Domain or Server account** (Account di dominio o server).</span><span class="sxs-lookup"><span data-stu-id="867f7-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Selezione dell'utente per SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="867f7-882">_**Figura 43:** Selezione dell'utente per SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="867f7-883">Specificare il nome utente dell'account di dominio e le password creati per SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="867f7-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Specificare il nome utente di dominio e la password per l'installazione di SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="867f7-885">_**Figura 44:** Specificare il nome utente di dominio e la password per l'installazione di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="867f7-886">Installare la chiave di licenza per l'istanza di SIOS DataKeeper, come illustrato nella figura 45.</span><span class="sxs-lookup"><span data-stu-id="867f7-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: Specificare la chiave di licenza di SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="867f7-888">_**Figura 45:** Specificare la chiave di licenza di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="867f7-889">Quando richiesto, riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="867f7-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="867f7-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurare SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="867f7-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="867f7-891">Dopo l'installazione di SIOS DataKeeper su entrambi i nodi è necessario avviare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="867f7-892">L'obiettivo della configurazione è eseguire la replica di dati sincrona tra i dischi aggiuntivi collegati a ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="867f7-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="867f7-893">Avviare lo strumento di configurazione e gestione di DataKeeper e selezionare il collegamento **Connect Server** (Connetti server).</span><span class="sxs-lookup"><span data-stu-id="867f7-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="867f7-894">Nella figura 46, questa opzione è racchiusa in un cerchio rosso.</span><span class="sxs-lookup"><span data-stu-id="867f7-894">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Strumento di configurazione e gestione di SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="867f7-896">_**Figura 46:** Strumento di configurazione e gestione di SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="867f7-897">Inserire il nome o l'indirizzo TCP/IP del primo nodo cui deve connettersi lo strumento di configurazione e gestione; eseguire l'operazione in un altro passaggio per il secondo nodo.</span><span class="sxs-lookup"><span data-stu-id="867f7-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Figura 47: Inserire il nome o l'indirizzo TCP/IP del primo nodo cui deve connettersi lo strumento di configurazione e gestione; eseguire l'operazione in un altro passaggio per il secondo nodo][sap-ha-guide-figure-3037]

  <span data-ttu-id="867f7-899">_**Figura 47:** Inserire il nome o l'indirizzo TCP/IP del primo nodo cui deve connettersi lo strumento di configurazione e gestione; eseguire l'operazione in un altro passaggio per il secondo nodo_</span><span class="sxs-lookup"><span data-stu-id="867f7-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="867f7-900">Creare il processo di replica tra i due nodi.</span><span class="sxs-lookup"><span data-stu-id="867f7-900">Create the replication job between the two nodes.</span></span>

  ![Figura 48: Creare un processo di replica][sap-ha-guide-figure-3038]

  <span data-ttu-id="867f7-902">_**Figura 48:** Creare un processo di replica_</span><span class="sxs-lookup"><span data-stu-id="867f7-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="867f7-903">Per la creazione di un processo di replica è disponibile una procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="867f7-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="867f7-904">Definire il nome, l'indirizzo TCP/IP e un volume del disco del nodo di origine.</span><span class="sxs-lookup"><span data-stu-id="867f7-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Figura 49: Definire il nome del processo di replica][sap-ha-guide-figure-3039]

  <span data-ttu-id="867f7-906">_**Figura 49:** Definire il nome del processo di replica_</span><span class="sxs-lookup"><span data-stu-id="867f7-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Figura 50: Definire i dati di base per il nodo che deve essere il nodo di origine corrente][sap-ha-guide-figure-3040]

  <span data-ttu-id="867f7-908">_**Figura 50:** Definire i dati di base per il nodo che deve essere il nodo di origine corrente_</span><span class="sxs-lookup"><span data-stu-id="867f7-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="867f7-909">Definire il nome, l'indirizzo TCP/IP e un volume del disco del nodo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Figura 51: Definire i dati di base per il nodo che deve essere il nodo di destinazione corrente][sap-ha-guide-figure-3041]

  <span data-ttu-id="867f7-911">_**Figura 51:** Definire i dati di base per il nodo che deve essere il nodo di destinazione corrente_</span><span class="sxs-lookup"><span data-stu-id="867f7-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="867f7-912">Definire gli algoritmi di compressione.</span><span class="sxs-lookup"><span data-stu-id="867f7-912">Define the compression algorithms.</span></span> <span data-ttu-id="867f7-913">Nell'esempio è consigliabile comprimere il flusso di replica.</span><span class="sxs-lookup"><span data-stu-id="867f7-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="867f7-914">Soprattutto in caso di risincronizzazione, la compressione del flusso di replica riduce notevolmente il tempo necessario per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="867f7-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="867f7-915">Si noti che la compressione usa le risorse di CPU e RAM di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="867f7-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="867f7-916">Con l'aumentare del tasso di compressione aumenta anche il volume delle risorse di CPU usate.</span><span class="sxs-lookup"><span data-stu-id="867f7-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="867f7-917">È possibile anche modificare questa impostazione in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="867f7-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="867f7-918">Un'altra impostazione da verificare è se la replica viene eseguita in modalità sincrona o asincrona.</span><span class="sxs-lookup"><span data-stu-id="867f7-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="867f7-919">*Per proteggere le configurazioni di SAP ASCS/SCS, è necessario usare la replica sincrona*.</span><span class="sxs-lookup"><span data-stu-id="867f7-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definire i dettagli della replica][sap-ha-guide-figure-3042]

  <span data-ttu-id="867f7-921">_**Figura 52:** Definire i dettagli della replica_</span><span class="sxs-lookup"><span data-stu-id="867f7-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="867f7-922">Definire se il volume replicato dal processo di replica deve essere rappresentato in una configurazione di cluster WSFC (Windows Server Failover Clustering) come disco condiviso.</span><span class="sxs-lookup"><span data-stu-id="867f7-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="867f7-923">Per la configurazione di SAP ASCS/SCS è necessario scegliere **Yes** in modo che il cluster di Windows rilevi il volume replicato come disco condiviso che può essere usato come volume del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Selezionare Yes (Sì) per impostare il volume replicato come volume del cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="867f7-925">_**Figura 53:** Selezionare **Yes** (Sì) per impostare il volume replicato come volume del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="867f7-926">Dopo aver creato il volume, lo strumento di configurazione e gestione di DataKeeper mostra che il processo di replica è attivo.</span><span class="sxs-lookup"><span data-stu-id="867f7-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Figura 54: Il mirroring sincrono di DataKeeper per il disco condiviso di SAP ASCS/SCS è attivo][sap-ha-guide-figure-3044]

  <span data-ttu-id="867f7-928">_**Figura 54:** Il mirroring sincrono di DataKeeper per il disco condiviso di SAP ASCS/SCS è attivo_</span><span class="sxs-lookup"><span data-stu-id="867f7-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="867f7-929">Gestione cluster di failover visualizza ora il disco come disco di DataKeeper, come illustrato nella figura 55.</span><span class="sxs-lookup"><span data-stu-id="867f7-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: Gestione cluster di failover visualizza il disco replicato da DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="867f7-931">_**Figura 55:** Gestione cluster di failover visualizza il disco replicato da DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="867f7-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="867f7-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Installare il sistema SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="867f7-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="867f7-933">La configurazione del sistema DBMS non viene descritta perché varia a seconda del sistema DBMS usato.</span><span class="sxs-lookup"><span data-stu-id="867f7-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="867f7-934">Si presuppone tuttavia che i problemi di disponibilità elevata del sistema DBMS vengano risolti con le funzionalità supportate dai diversi fornitori di sistemi DBMS per Azure,</span><span class="sxs-lookup"><span data-stu-id="867f7-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="867f7-935">ad esempio AlwaysOn o mirroring del database per SQL Server e Oracle Data Guard per database Oracle.</span><span class="sxs-lookup"><span data-stu-id="867f7-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="867f7-936">Nello scenario usato in questo articolo, non sono state aggiunte altre funzionalità di protezione per il sistema DBMS.</span><span class="sxs-lookup"><span data-stu-id="867f7-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="867f7-937">Non esistono particolari considerazioni per il caso in cui servizi DBMS differenti interagiscono con questa configurazione di SAP ASCS/SCS in cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-938">La procedura di installazione dei sistemi SAP NetWeaver ABAP, Java e ABAP + Java è praticamente identica.</span><span class="sxs-lookup"><span data-stu-id="867f7-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="867f7-939">La differenza principale è che un sistema SAP ABAP ha un'istanza di ASCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="867f7-940">Il sistema SAP Java ha un'istanza di SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="867f7-941">Il sistema SAP ABAP + Java ha un'istanza ASCS e un'istanza SCS in esecuzione nello stesso gruppo di cluster di failover Microsoft.</span><span class="sxs-lookup"><span data-stu-id="867f7-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="867f7-942">Eventuali differenze di installazione per ogni stack di installazione di SAP NetWeaver verranno indicate in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="867f7-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="867f7-943">Si presume che tutte le altre parti siano uguali.</span><span class="sxs-lookup"><span data-stu-id="867f7-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="867f7-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Installare SAP con un'istanza di ASCS/SCS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="867f7-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867f7-945">Non inserire il file di paging nei volumi con mirroring di DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="867f7-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="867f7-946">DataKeeper non supporta i volumi con mirroring.</span><span class="sxs-lookup"><span data-stu-id="867f7-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="867f7-947">È possibile lasciare il file di paging nell'unità temporanea D di una macchina virtuale di Azure, ovvero l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="867f7-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="867f7-948">Se non è già presente, spostare il file di paging di Windows nell'unità D: della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="867f7-949">L'installazione di SAP con un'istanza di ASCS/SCS a disponibilità elevata prevede queste attività:</span><span class="sxs-lookup"><span data-stu-id="867f7-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="867f7-950">Creazione di un nome host virtuale per l'istanza di SAP ASCS/SCS in cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="867f7-951">Installazione del primo nodo del cluster SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="867f7-952">Modifica del profilo SAP dell'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="867f7-953">Aggiunta di un porta probe</span><span class="sxs-lookup"><span data-stu-id="867f7-953">Adding a probe port</span></span>
- <span data-ttu-id="867f7-954">Apertura della porta probe di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="867f7-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="867f7-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Creare un nome host virtuale per l'istanza di SAP ASCS/SCS in cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="867f7-956">In Gestore DNS di Windows creare una voce DNS per il nome host virtuale dell'istanza di ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="867f7-957">L'indirizzo IP assegnato al nome host virtuale dell'istanza di ASCS/SCS deve essere lo stesso indirizzo IP assegnato ad Azure Load Balancer (**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="867f7-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="867f7-958">L'indirizzo IP del nome host virtuale di SAP ASCS/SCS (**pr1-ascs-sap**) è lo stesso indirizzo IP di Azure Load Balancer (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="867f7-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definire la voce DNS per il nome virtuale e l'indirizzo TCP/IP del cluster SAP ASCS/SCS][sap-ha-guide-figure-3046]

  <span data-ttu-id="867f7-960">_**Figura 56:** Definire la voce DNS per il nome virtuale e l'indirizzo TCP/IP del cluster SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="867f7-961">Per definire l'indirizzo IP assegnato al nome host virtuale, selezionare **Gestore DNS** > **Dominio**.</span><span class="sxs-lookup"><span data-stu-id="867f7-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="867f7-963">_**Figura 57:** Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="867f7-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="867f7-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Installare il primo nodo del cluster SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="867f7-965">Eseguire l'opzione del primo nodo del cluster nel nodo A, ad esempio nell'host **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="867f7-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="867f7-966">Per mantenere le porte predefinite per il bilanciamento del carico interno di Azure, selezionare:</span><span class="sxs-lookup"><span data-stu-id="867f7-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="867f7-967">Per il **sistema ABAP**: **ASCS** numero di istanza **00**</span><span class="sxs-lookup"><span data-stu-id="867f7-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="867f7-968">Per il **sistema Java**: **SCS** numero di istanza **01**</span><span class="sxs-lookup"><span data-stu-id="867f7-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="867f7-969">Per il **sistema ABAP + Java**: **ASCS** numero di istanza **00** e **SCS** numero di istanza **01**</span><span class="sxs-lookup"><span data-stu-id="867f7-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="867f7-970">Per usare altri numeri di istanza rispetto a 00 per l'istanza di ABAP ASCS e rispetto a 01 per l'istanza di Java SCS, è prima necessario modificare le regole predefinite del servizio di bilanciamento del carico interno di Azure, come descritto in [Modificare le regole di bilanciamento del carico predefinite di ASCS/SCS per il servizio di bilanciamento del carico interno di Azure][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="867f7-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="867f7-971">Le attività successive non sono descritte nella documentazione di installazione generale di SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-972">La documentazione di installazione di SAP descrive come installare il primo nodo del cluster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="867f7-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modificare il profilo SAP dell'istanza di ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="867f7-974">È necessario aggiungere un nuovo parametro del profilo.</span><span class="sxs-lookup"><span data-stu-id="867f7-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="867f7-975">Questo parametro impedisce la chiusura delle connessioni tra i processi di lavoro SAP e il server di accodamento quando sono inattivi per un tempo eccessivo.</span><span class="sxs-lookup"><span data-stu-id="867f7-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="867f7-976">Lo scenario del problema è stato descritto nella sezione [Aggiungere le voci del Registro di sistema in entrambi i nodi del cluster per l'istanza di SAP ASCS/SCS][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="867f7-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="867f7-977">In quella sezione sono anche illustrate due modifiche ad alcuni parametri della connessione TCP/IP di base.</span><span class="sxs-lookup"><span data-stu-id="867f7-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="867f7-978">Nel secondo passaggio è necessario impostare il server di accodamento per l'invio di un segnale `keep_alive` per impedire alle connessioni di raggiungere la soglia di inattività del servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="867f7-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="867f7-979">Per modificare il profilo SAP dell'istanza di ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="867f7-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="867f7-980">Aggiungere questo parametro al profilo dell'istanza di SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="867f7-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="867f7-981">Nell'esempio il percorso è:</span><span class="sxs-lookup"><span data-stu-id="867f7-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="867f7-982">Ad esempio, al profilo dell'istanza di SAP SCS e al percorso corrispondente:</span><span class="sxs-lookup"><span data-stu-id="867f7-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="867f7-983">Per applicare le modifiche, riavviare l'istanza di SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="867f7-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Aggiungere una porta probe</span><span class="sxs-lookup"><span data-stu-id="867f7-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="867f7-985">Usare la funzionalità probe del servizio di bilanciamento del carico interno per il corretto funzionamento della configurazione del cluster con Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="867f7-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="867f7-986">Il servizio di bilanciamento del carico interno di Azure distribuisce in genere il carico di lavoro in ingresso in modo uniforme tra le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="867f7-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="867f7-987">Questa operazione non funziona tuttavia in alcune configurazioni di cluster perché è attiva una sola istanza.</span><span class="sxs-lookup"><span data-stu-id="867f7-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="867f7-988">L'altra istanza è passiva e non può accettare carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="867f7-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="867f7-989">La funzionalità probe è utile quando il servizio di bilanciamento del carico interno di Azure assegna il carico di lavoro solo a un'istanza attiva.</span><span class="sxs-lookup"><span data-stu-id="867f7-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="867f7-990">Con la funzionalità probe, il servizio di bilanciamento del carico interno può rilevare l'istanza attiva e usare solo questa istanza come destinazione del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="867f7-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="867f7-991">Per aggiungere una porta probe:</span><span class="sxs-lookup"><span data-stu-id="867f7-991">To add a probe port:</span></span>

1.  <span data-ttu-id="867f7-992">Verificare l'impostazione di **ProbePort** corrente eseguendo il comando di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="867f7-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="867f7-993">Eseguire il comando all'interno di una delle macchine virtuali della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="867f7-994">Definire una porta probe.</span><span class="sxs-lookup"><span data-stu-id="867f7-994">Define a probe port.</span></span> <span data-ttu-id="867f7-995">Il numero della porta probe predefinita è **0**.</span><span class="sxs-lookup"><span data-stu-id="867f7-995">The default probe port number is **0**.</span></span> <span data-ttu-id="867f7-996">In questo esempio viene usata la porta probe **62000**.</span><span class="sxs-lookup"><span data-stu-id="867f7-996">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: La porta probe della configurazione del cluster è 0 per impostazione predefinita][sap-ha-guide-figure-3048]

  <span data-ttu-id="867f7-998">_**Figura 58:** La porta probe predefinita della configurazione del cluster è 0_</span><span class="sxs-lookup"><span data-stu-id="867f7-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="867f7-999">Il numero della porta è definito nei modelli di Azure Resource Manager per SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="867f7-1000">È possibile assegnare il numero della porta in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="867f7-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="867f7-1001">Per impostare un nuovo valore di ProbePort per la risorsa cluster **SAP <*SID*> IP**, eseguire il seguente script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="867f7-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="867f7-1002">Aggiornare le variabili PowerShell per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="867f7-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="867f7-1003">Dopo l'esecuzione dello script, verrà richiesto di riavviare il gruppo di cluster SAP per attivare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="867f7-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="867f7-1004">Dopo avere portato online il ruolo cluster **SAP <*SID*>**, verificare che **ProbePort** sia impostato sul nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="867f7-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Eseguire il probe della porta del cluster dopo aver impostato il nuovo valore][sap-ha-guide-figure-3049]

  <span data-ttu-id="867f7-1006">_**Figura 59:** Eseguire il probe della porta del cluster dopo aver impostato il nuovo valore_</span><span class="sxs-lookup"><span data-stu-id="867f7-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="867f7-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Aprire la porta probe di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="867f7-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="867f7-1008">È necessario aprire una porta probe di Windows Firewall in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="867f7-1009">Usare lo script seguente per aprire una porta probe di Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="867f7-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="867f7-1010">Aggiornare le variabili PowerShell per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="867f7-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="867f7-1011">**ProbePort** è impostato su **62000**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="867f7-1012">Ora è possibile accedere alla condivisione file **\\\ascsha-clsap\sapmnt** da altri host come **ascsha-dbas**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="867f7-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Installare l'istanza di database</span><span class="sxs-lookup"><span data-stu-id="867f7-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="867f7-1014">Per installare l'istanza di database, seguire la procedura descritta nella documentazione sull'installazione di SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="867f7-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Installare il secondo nodo del cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="867f7-1016">Per installare il secondo nodo del cluster, seguire i passaggi descritti nella guida all'installazione di SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="867f7-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Cambiare il tipo di avvio dell'istanza del servizio Windows SAP ERS</span><span class="sxs-lookup"><span data-stu-id="867f7-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="867f7-1018">Cambiare il tipo di avvio del servizio Windows SAP ERS su **(avvio ritardato) automatico** in entrambi i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="867f7-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Cambiare il tipo di servizio per l'istanza di SAP ERS su ritardo automatico][sap-ha-guide-figure-3050]

<span data-ttu-id="867f7-1020">_**Figura 60:** Cambiare il tipo di servizio per l'istanza di SAP ERS su ritardo automatico_</span><span class="sxs-lookup"><span data-stu-id="867f7-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="867f7-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Installare Primary Application Server (PAS) SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="867f7-1022">Installare l'istanza di Primary Application Server (PAS) <*SID*>-di-0 nella macchina virtuale designata per ospitare PAS.</span><span class="sxs-lookup"><span data-stu-id="867f7-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="867f7-1023">Non sono presenti dipendenze da specifiche impostazioni di Azure o DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="867f7-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="867f7-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Installare Additional Application Server (AAS) SAP</span><span class="sxs-lookup"><span data-stu-id="867f7-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="867f7-1025">Installare un'istanza di Additional Application Server (AAS) SAP in tutte le macchine virtuali designate per ospitare un'istanza del server applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="867f7-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="867f7-1026">Ad esempio, in <*SID*>-di-1 per <*SID*>-di-&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="867f7-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="867f7-1027">Questa operazione completa l'installazione di un sistema SAP NetWeaver a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="867f7-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="867f7-1028">Procedere quindi con il test del failover.</span><span class="sxs-lookup"><span data-stu-id="867f7-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="867f7-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Testare il failover e la replica SIOS dell'istanza di SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="867f7-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="867f7-1030">È possibile testare e monitorare con facilità un failover dell'istanza di SAP ASCS/SCS e una replica del disco SIOS usando Gestione cluster di failover e lo strumento di configurazione e gestione di SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="867f7-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="867f7-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> Istanza di SAP ASCS/SCS in esecuzione nel nodo A del cluster</span><span class="sxs-lookup"><span data-stu-id="867f7-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="867f7-1032">Il gruppo di cluster **SAP PR1** è in esecuzione nel nodo A del cluster, ad esempio in **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="867f7-1033">Assegnare al nodo A del cluster l'unità disco condivisa S, appartenente al gruppo di cluster **SAP PR1** e usata dall'istanza di ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="867f7-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Figura 61: Gestione cluster di failover: il gruppo di cluster <SID> SAP è in esecuzione nel nodo A del cluster][sap-ha-guide-figure-5000]

<span data-ttu-id="867f7-1035">_**Figura 61:** Gestione cluster di failover: il gruppo di cluster SAP <*SID*> è in esecuzione nel nodo A del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="867f7-1036">Nello strumento di configurazione e gestione di SIOS DataKeeper è possibile verificare che i dati di dischi condivisi vengano replicati in modo sincrono dall'unità S del volume di origine nel nodo A del cluster all'unità S del volume di destinazione nel nodo B del cluster, ad esempio da **pr1-ascs-0 [10.0.0.40]** a **pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: In SIOS DataKeeper, replicare il volume locale dal nodo A al nodo B del cluster][sap-ha-guide-figure-5001]

<span data-ttu-id="867f7-1038">_**Figura 62:** In SIOS DataKeeper, replicare il volume locale dal nodo A al nodo B del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="867f7-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover dal nodo A al nodo B</span><span class="sxs-lookup"><span data-stu-id="867f7-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="867f7-1040">Scegliere una di queste opzioni per avviare un failover del gruppo di cluster <*SID*> SAP dal nodo A al nodo B del cluster:</span><span class="sxs-lookup"><span data-stu-id="867f7-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="867f7-1041">Usare Gestione cluster di failover</span><span class="sxs-lookup"><span data-stu-id="867f7-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="867f7-1042">Usare PowerShell per Clustering di failover</span><span class="sxs-lookup"><span data-stu-id="867f7-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="867f7-1043">Riavviare il nodo A del cluster nel sistema operativo guest di Windows. Verrà avviato un failover automatico del gruppo di cluster <*SID*> SAP dal nodo A al nodo B.</span><span class="sxs-lookup"><span data-stu-id="867f7-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="867f7-1044">Riavviare il nodo A del cluster nel portale di Azure. Verrà avviato un failover automatico del gruppo di cluster <*SID*> SAP dal nodo A al nodo B.</span><span class="sxs-lookup"><span data-stu-id="867f7-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="867f7-1045">Riavviare il nodo A del cluster usando Azure PowerShell. Verrà avviato un failover automatico del gruppo di cluster <*SID*> SAP dal nodo A al nodo B.</span><span class="sxs-lookup"><span data-stu-id="867f7-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="867f7-1046">Il gruppo di cluster SAP <*SID*> è in esecuzione nel nodo B del cluster, ad esempio in **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: In Gestione cluster di failover, il gruppo di cluster <SID> SAP è in esecuzione nel nodo B del cluster][sap-ha-guide-figure-5002]

  <span data-ttu-id="867f7-1048">_**Figura 63**: In Gestione cluster di failover, il gruppo di cluster SAP <*SID*> è in esecuzione nel nodo B del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="867f7-1049">Il disco condiviso è ora montato nel nodo B del cluster. SIOS DataKeeper replica i dati dall'unità S del volume di origine nel nodo B del cluster all'unità S del volume di destinazione nel nodo A del cluster, ad esempio da **pr1-ascs-1 [10.0.0.41]** a **pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="867f7-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica il volume locale dal nodo B al nodo A del cluster][sap-ha-guide-figure-5003]

  <span data-ttu-id="867f7-1051">_**Figura 64:** SIOS DataKeeper replica il volume locale dal nodo B al nodo A del cluster_</span><span class="sxs-lookup"><span data-stu-id="867f7-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
