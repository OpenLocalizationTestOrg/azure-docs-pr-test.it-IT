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
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

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



Macchine virtuali di Azure è una soluzione di hello per le organizzazioni che necessitano di calcolo, archiviazione e risorse di rete, in tempi minimi senza lunghi cicli di approvvigionamento. È possibile utilizzare applicazioni classiche toodeploy di macchine virtuali di Azure come ABAP basate su SAP NetWeaver, Java e uno stack ABAP + Java. È possibile estendere l'affidabilità e la disponibilità senza risorse locali aggiuntive. Macchine virtuali di Azure supporta la connettività cross-premise e quindi è possibile integrare Macchine virtuali di Azure nei domini locali, nei cloud privati e nel panorama applicativo del sistema SAP dell'organizzazione.

In questo articolo si descrivono i passaggi di hello che è possibile trarre toodeploy sistemi SAP a disponibilità elevata in Azure con modello di distribuzione Azure Resource Manager hello. Le attività principali che verranno illustrate sono le seguenti:

* Trovare hello destra guide di note su SAP e l'installazione, elencate in hello [risorse] [ sap-ha-guide-2] sezione. In questo articolo integra la documentazione di installazione di SAP e note su SAP, che sono le risorse primarie hello che consentono di installare e distribuire il software SAP in piattaforme specifiche.
* Differenze di hello tra modello di distribuzione Azure Resource Manager hello e il modello di distribuzione classica Azure hello.
* Informazioni sulle modalità quorum di Windows Server Failover Clustering, è possibile scegliere modello hello appropriato per la distribuzione di Azure.
* Comprendere l'archiviazione condivisa di Windows Server Failover Clustering nei servizi di Azure.
* Informazioni su come proteggere i componenti singolo punto di errore come avanzate Business dell'applicazione di programmazione (ABAP) SAP Central Services (ASCS) toohelp / SAP Central Services (SCS) e sistemi di gestione di database (DBMS) e i componenti ridondanti quali SAP Server applicazioni in Azure.
* Seguire un esempio dettagliato di installazione e configurazione di un sistema SAP a disponibilità elevata in un cluster Windows Server Failover Clustering in Azure usando Azure Resource Manager.
* Informazioni su Windows Server Failover Clustering in Azure la toouse necessari passaggi aggiuntivi, ma che non sono necessari in una distribuzione locale.

toosimplify distribuzione e la configurazione, in questo articolo, utilizziamo hello modelli di gestione risorse SAP a tre livelli a disponibilità elevata. modelli di Hello automatizzare la distribuzione di hello tutta l'infrastruttura necessaria per un sistema SAP a disponibilità elevata. infrastruttura Hello supporta anche il ridimensionamento di SAP applicazione prestazioni Standard (SAP) del sistema SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisiti
Prima di iniziare, assicurarsi che siano soddisfatti i prerequisiti di hello descritti in hello le sezioni seguenti. Inoltre, essere toocheck che tutte le risorse elencate in hello [risorse] [ sap-ha-guide-2] sezione.

In questo articolo vengono usati i modelli di Azure Resource Manager per [SAP NetWeaver a tre livelli con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Per una panoramica dei modelli, vedere i [modelli di Azure Resource Manager per SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Risorse
Questi articoli descrivono le distribuzioni SAP in Azure:

* [Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP NetWeaver][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP NetWeaver][dbms-guide]
* [Disponibilità elevata in Macchine virtuali di Azure per SAP NetWeaver (questa guida)][sap-ha-guide]

> [!NOTE]
> Quando possibile, fornita è toohello un collegamento che fa riferimento la Guida all'installazione SAP (vedere hello [Guide all'installazione di SAP][sap-installation-guides]). Per i prerequisiti e informazioni sul processo di installazione, hello è un'installazione di SAP NetWeaver hello tooread buona guide con attenzione. Questo articolo illustra solo attività specifiche per i sistemi basati su SAP NetWeaver che è possibile usare con Macchine virtuali di Azure.
>
>

Queste note SAP sono correlati toohello argomento SAP in Azure:

| Numero della nota | Titolo |
| --- | --- |
| [1928533] |Applicazioni SAP in Azure: dimensioni e prodotti supportati |
| [2015553] |SAP in Microsoft Azure: prerequisiti per il supporto |
| [1999351] |Monitoraggio avanzato di Azure per SAP |
| [2178632] |Metriche chiave del monitoraggio per SAP in Microsoft Azure |
| [1999351] |Virtualizzazione in Windows: monitoraggio avanzato |
| [2243692] |Use of Azure Premium SSD Storage for SAP DBMS Instance (Uso dell'archiviazione unità SSD di Azure Premium per l'istanza DBMS di SAP) |

Altre informazioni su hello [limitazioni delle sottoscrizioni di Azure][azure-subscription-service-limits-subscription], inclusi i limiti predefiniti generali e limitazioni massime.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP a disponibilità elevata con Azure Resource Manager e il modello di distribuzione classica Azure hello
Hello Azure Resource Manager e i modelli di distribuzione classico di Azure sono diversi in hello seguenti aree:

- Gruppi di risorse
- Azure interno caricare la dipendenza del servizio di bilanciamento nel gruppo di risorse di Azure hello
- Supporto per scenari di SAP con più SID

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Gruppi di risorse
Gestione risorse di Microsoft Azure, è possibile utilizzare risorse gruppi toomanage tutte le risorse dell'applicazione hello nella sottoscrizione di Azure. Un approccio integrato, in un gruppo di risorse, tutte le risorse sono hello stesso ciclo di vita. Ad esempio, per cui tutte le risorse vengono create in hello stesso volta e vengono eliminate alla hello contemporaneamente. Altre informazioni sui [gruppi di risorse](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno caricare la dipendenza del servizio di bilanciamento nel gruppo di risorse di Azure hello

Nel modello di distribuzione classica Azure hello, vi è una dipendenza tra servizio di bilanciamento del carico interno di Azure hello (servizio di bilanciamento del carico di Azure) e il servizio cloud hello. Ogni servizio di bilanciamento del carico interno necessita di un servizio cloud.

Gestione risorse di Microsoft Azure, tutte le risorse di Azure devono toobe inseriti in un gruppo di risorse di Azure, ed è valido per servizio di bilanciamento del carico di Azure anche. Tuttavia, è presente alcun gruppo di risorse di Azure una necessità toohave per ogni servizio di bilanciamento del carico di Azure, ad esempio, un gruppo di risorse di Azure può contenere più bilanciamenti del carico Azure. ambiente Hello è più semplice e più flessibile. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Supporto per scenari di SAP con più SID

In Azure Resource Manager è possibile installare istanze di ASCS/SCS con più SAP ID (SID). Le istanze con più SID sono consentite grazie al supporto di più indirizzi IP per ogni servizio di bilanciamento del carico interno di Azure.

toouse hello modello di distribuzione classico di Azure, seguire procedure hello descritte in [SAP NetWeaver in Azure: le istanze di Clustering SAP ASCS/SCS tramite Windows Server Failover Clustering in Azure con SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> È consigliabile utilizzare un modello di distribuzione Azure Resource Manager hello per le installazioni di SAP. Offre numerosi vantaggi che non sono disponibili nel modello di distribuzione classica hello. Sono disponibili altre informazioni sui [modelli di distribuzione][virtual-machines-azure-resource-manager-architecture-benefits-arm] di Azure.   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering
Windows Server Failover Clustering è foundation hello di un'installazione di SAP ASCS/SCS a disponibilità elevata e di un sistema DBMS in Windows.

Un cluster di failover è un gruppo di 1 + n server indipendenti (nodi) che interagiscono tra di loro disponibilità hello tooincrease di applicazioni e servizi. Se si verifica un errore di nodo, Windows Server Failover Clustering calcola il numero di hello di errori che possono verificarsi durante la gestione di un cluster tooprovide applicazioni e servizi. È possibile scegliere da clustering di failover tooachieve modalità quorum diversi.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modalità quorum
È possibile scegliere tra quattro modalità quorum quando si usa Windows Server Failover Clustering:

* **Maggioranza dei nodi**. Ogni nodo del cluster hello può votare. Hello cluster funziona solo con la maggior parte dei voti, vale a dire con voti hello più della metà. È consigliabile scegliere questa opzione per i cluster con un numero dispari di nodi. Ad esempio, tre nodi in un cluster di sette nodi possono non riuscire e hello cluster continua non otterrà una maggioranza e continua toorun.  
* **Maggioranza dei nodi e dei dischi**. Ogni nodo e un disco designato (un disco di controllo) nell'archiviazione cluster hello può votare quando sono disponibili e in comunicazione. funzioni di cluster Hello solo con la maggior parte di hello voti, vale a dire con voti hello più della metà. Questa modalità ha senso in un ambiente cluster con un numero pari di nodi. Se i nodi di metà hello e disco hello sono online, il cluster di hello rimane in uno stato integro.
* **Maggioranza dei nodi e delle condivisioni file**. Ogni nodo e crea una condivisione di file designati (una condivisione file di controllo) hello amministratore può votare, indipendentemente dal fatto che siano disponibili nodi hello e condivisione file e in comunicazione. funzioni di cluster Hello solo con la maggior parte di hello voti, vale a dire con voti hello più della metà. Questa modalità ha senso in un ambiente cluster con un numero pari di nodi. È simile toohello nodo e modalità maggioranza dei dischi, ma utilizza una condivisione di file di controllo anziché un disco di controllo. Questa modalità è facile tooimplement, ma se condivide file hello stesso non è a disponibilità elevata, potrebbe risultare un singolo punto di errore.
* **Non di maggioranza - solo disco**. cluster Hello dispone di un quorum se un nodo è disponibile e in comunicazione con un disco specifico nell'archiviazione cluster hello. Solo i nodi di hello inoltre sono in comunicazione con il disco è possono aggiungere cluster hello. Si consiglia di non usare questa modalità.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering locale
La figura 1 illustra un cluster con due nodi. Se hello si verifica un errore di connessione di rete tra i nodi di hello e rimangono entrambi i nodi e in esecuzione, una condivisione di file o disco quorum determina quale nodo continuerà applicazioni e servizi del cluster di tooprovide hello. nodo Hello con disco quorum toohello di accesso o una condivisione file è nodo hello che assicura che i servizi di continuino.

Poiché in questo esempio utilizza un cluster a due nodi, utilizziamo hello nodo e modalità quorum maggioranza dei condivisione File. Inoltre, Hello nodo e la maggior parte del disco è un'opzione valida. In un ambiente di produzione è consigliabile usare un disco quorum. È possibile utilizzare l'archiviazione e rete toomake tecnologia di sistema è a disponibilità elevata.

![Figura 1: Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure][sap-ha-guide-figure-1000]

_**Figura 1:** Esempio di configurazione di Windows Server Failover Clustering proposta per SAP ASCS/SCS in Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Spazio di archiviazione condiviso
La figura 1 illustra anche un cluster di archiviazione condiviso a due nodi. In un cluster di archiviazione condivisa locale, tutti i nodi cluster hello rilevare archiviazione condivisa. Un meccanismo di blocco protegge i dati di hello da eventuali danni. Tutti i nodi possono rilevare se si verifica un errore in un altro nodo. Se un nodo, nodo rimanente hello acquisisce la proprietà delle risorse di archiviazione hello e garantisce la disponibilità dei servizi hello.

> [!NOTE]
> Non sono necessari dischi condivisi per la disponibilità elevata con alcune applicazioni DBMS, ad esempio SQL Server. SQL Server Always On consente di replicare i file di dati e di log DBMS da disco locale di hello del disco locale toohello nodo di un cluster di un altro nodo del cluster. Configurazione del cluster di Windows hello in tal caso, non è necessario un disco condiviso.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Rete e risoluzione dei nomi
I computer client raggiungono cluster hello su un indirizzo IP virtuale e un nome host virtuale che hello fornisce server DNS. Hello nodi in locale e server DNS hello può gestire più indirizzi IP.

In un'installazione tipica si usano due o più connessioni di rete:

* Archiviazione di toohello una connessione dedicata
* Una connessione di rete interne al cluster per heartbeat hello
* Una rete pubblica che i client utilizzino tooconnect toohello cluster

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure
Confrontare le distribuzioni di cloud privato o metal toobare, macchine virtuali di Azure richiede passaggi aggiuntivi tooconfigure Windows Server Failover Clustering. Quando si crea un disco cluster condiviso, è necessario tooset nomi diversi indirizzi IP e l'host virtuale per l'istanza di SAP ASCS/SCS hello.

In questo articolo è illustrare i concetti chiave e hello toobuild necessari passaggi aggiuntivi un cluster a disponibilità elevata centrale servizi SAP in Azure. Viene illustrata la modalità tooset dello strumento di terze parti hello SIOS DataKeeper di e come tooconfigure hello Azure interno il bilanciamento del carico. È possibile utilizzare questi toocreate strumenti un cluster di failover di Windows con una condivisione file di controllo in Azure.

![Figura 2: Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso][sap-ha-guide-figure-1001]

_**Figura 2:** Configurazione di Windows Server Failover Clustering in Azure senza disco condiviso_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco condiviso in Azure con SIOS DataKeeper
È necessario spazio di archiviazione condiviso del cluster per un'istanza di SAP ASCS/SCS a disponibilità elevata. Come di settembre 2016, Azure non offre spazio di archiviazione condiviso che è possibile utilizzare toocreate un cluster di archiviazione condivisa. È possibile utilizzare il software di terze parti SIOS DataKeeper Cluster Edition toocreate un'archiviazione con mirroring che simula l'archiviazione condivisa cluster. Hello soluzione SIOS fornisce la replica di dati sincroni in tempo reale. Per creare una risorsa disco condiviso per un cluster, seguire questa procedura:

1. Collegare un disco aggiuntivo di tooeach di hello le macchine virtuali (VM) in una configurazione cluster di Windows.
2. Eseguire SIOS DataKeeper Cluster Edition in entrambi i nodi delle macchine virtuali.
3. Configurare SIOS DataKeeper Cluster Edition in modo speculare contenuto hello del volume di disco aggiuntivo collegato hello dal volume disco aggiuntivo collegato toohello hello origine macchina virtuale della macchina virtuale di destinazione hello. SIOS DataKeeper estrae i volumi locali di origine e destinazione hello e quindi li presenta tooWindows Clustering di Failover di Server come un disco condiviso.

Altre informazioni su [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Figura 3: Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 3:** Configurazione di Windows Server Failover Clustering in Azure con SIOS DataKeeper_

> [!NOTE]
> Non sono necessari dischi condivisi per la disponibilità elevata con alcuni prodotti DBMS, ad esempio SQL Server. SQL Server Always On consente di replicare i file di dati e di log DBMS da disco locale di hello del disco locale toohello nodo di un cluster di un altro nodo del cluster. Configurazione del cluster di Windows hello in questo caso, non è necessario un disco condiviso.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Risoluzione dei nomi in Azure
piattaforma di cloud di Azure Hello non offre hello opzione tooconfigure indirizzi IP virtuali, ad esempio indirizzi IP mobili. È necessario un tooset soluzione alternativa di una virtuale risorsa indirizzo IP tooreach hello cluster nel cloud hello.
Azure offre un servizio di bilanciamento del carico interno nel servizio di bilanciamento del carico di Azure hello. Con servizio di bilanciamento del carico interno hello client raggiungono cluster hello tramite indirizzo IP virtuale del cluster hello.
È necessario bilanciamento del carico interno di hello toodeploy nel gruppo di risorse hello che contiene i nodi del cluster hello. Quindi, configurare tutte le necessarie regole di port forwarding con probe hello porte di bilanciamento del carico interno hello.
Hello client possono connettersi utilizzando il nome host virtuale hello. server DNS Hello risolve l'indirizzo IP del cluster hello e porta handle del bilanciamento del carico interno hello toohello nodo attivo del cluster hello di inoltro.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Disponibilità elevata di SAP NetWeaver nell'infrastruttura distribuita come servizio (IaaS) di Azure
tooachieve SAP a disponibilità elevata dell'applicazione, ad esempio per i componenti software SAP, è necessario hello tooprotect seguenti componenti:

* Istanza del server applicazioni SAP
* Istanza di SAP ASCS/SCS
* Server DBMS

Per altre informazioni sulla protezione dei componenti SAP in scenari a disponibilità elevata, vedere [Guida alla pianificazione e all'implementazione di Macchine virtuali di Azure per SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Server applicazioni SAP a disponibilità elevata
In genere non è necessaria una soluzione a disponibilità elevata specifica per le istanze di Server applicazioni SAP e finestra di dialogo hello. La disponibilità elevata si ottiene tramite la ridondanza e si dovranno configurare più istanze delle finestre di dialogo in istanze diverse di Macchine virtuali di Azure. È necessario avere almeno due istanze dell'applicazione SAP installate in due istanze di Macchine virtuali di Azure.

![Figura 4: Server applicazioni SAP a disponibilità elevata][sap-ha-guide-figure-2000]

_**Figura 4:** Server applicazioni SAP a disponibilità elevata_

È necessario inserire tutte le macchine virtuali che istanze dell'host Server applicazioni SAP in hello stesso set di disponibilità di Azure. Un set di disponibilità di Azure assicura che:

* Tutte le macchine virtuali fanno parte di hello nello stesso dominio di aggiornamento. Un dominio di aggiornamento, ad esempio, assicura che le macchine virtuali hello non sono aggiornate in hello contemporaneamente durante i tempi di inattività di manutenzione pianificata.
* Tutte le macchine virtuali fanno parte di hello stesso dominio di errore. Un dominio di errore, ad esempio, rende assicurarsi che le macchine virtuali sono distribuite in modo che nessun singolo punto di errore influisce sulla disponibilità di hello di tutte le macchine virtuali.

Per ulteriori informazioni su troppo[gestione hello disponibilità delle macchine virtuali][virtual-machines-manage-availability].

Solo disco non gestita: poiché hello account di archiviazione di Azure è un potenziale singolo punto di errore, è importante toohave almeno due account di archiviazione di Azure, in cui vengono distribuite almeno due macchine virtuali. In un'installazione ideale, i dischi di hello di ogni macchina virtuale che esegue un'istanza della finestra di dialogo SAP sarà distribuiti in un altro account di archiviazione.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Istanza di SAP ASCS/SCS a disponibilità elevata
La figura 5 è un esempio di istanza di SAP ASCS/SCS a disponibilità elevata.

![Figura 5: Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-2001]

_**Figura 5:** Istanza di SAP ASCS/SCS a disponibilità elevata_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Disponibilità elevata dell'istanza di SAP ASCS/SCS con Windows Server Failover Clustering in Azure
Confrontare le distribuzioni di cloud privato o metal toobare, macchine virtuali di Azure richiede passaggi aggiuntivi tooconfigure Windows Server Failover Clustering. toobuild un cluster di failover di Windows, è necessario un disco cluster condiviso, più indirizzi IP, diversi nomi host virtuale e un servizio di bilanciamento del carico interno di Azure per il clustering di un'istanza di SAP ASCS/SCS. Esaminati in dettaglio più avanti in articolo hello.

![Figura 6: Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 6:** Windows Server Failover Clustering per una configurazione SAP ASCS/SCS in Azure con SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Istanza di DBMS a disponibilità elevata
Hello DBMS è anche un singolo punto di contatto in un sistema SAP. È necessario tooprotect usando una soluzione a disponibilità elevata. Figura 7 illustra una soluzione a disponibilità elevata SQL Server Always On in Azure, con Windows Server Failover Clustering e hello Azure interno il bilanciamento del carico. SQL Server AlwaysOn replica i file di dati e di log DBMS usando la replica DBMS. In questo caso, non necessario dischi condivisi cluster, che semplifica l'installazione intera hello.

![Figura 7: Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn][sap-ha-guide-figure-2003]

_**Figura 7:** Esempio di SAP DBMS a disponibilità elevata con SQL Server AlwaysOn_

Per ulteriori informazioni sul clustering di SQL Server in Azure utilizzando il modello di distribuzione del hello Azure Resource Manager, vedere gli articoli:

* [Configurare manualmente il gruppo di disponibilità AlwaysOn in Macchine virtuali di Azure con Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Configurare un servizio di bilanciamento del carico interno di Azure per un gruppo di disponibilità AlwaysOn in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Scenari di distribuzione a disponibilità elevata end-to-end

### <a name="deployment-scenario-using-architectural-template-1"></a>Scenario di distribuzione usando il modello architetturale 1

La figura 8 illustra un esempio di architettura a disponibilità elevata SAP NetWeaver in Azure per **un** sistema SAP. Questo scenario viene configurato come segue:

- Un cluster dedicato viene utilizzato per l'istanza di SAP ASCS/SCS hello.
- Un cluster dedicato viene utilizzato per l'istanza DBMS hello.
- Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.

![Figura 8: Modello architetturale 1 a disponibilità elevata di SAP, con cluster dedicato per ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

_**Figura 8:** Modello architetturale 1 a disponibilità elevata di SAP, cluster dedicati per ASCS/SCS e DBMS_

### <a name="deployment-scenario-using-architectural-template-2"></a>Scenario di distribuzione usando il modello architetturale 2

La figura 9 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **un** sistema SAP. Questo scenario viene configurato come segue:

- Viene utilizzato un cluster dedicato per **entrambi** hello SAP ASCS/SCS di istanza e hello DBMS.
- Le istanze del server applicazioni SAP vengono distribuite in proprie VM dedicate.

![Figura 9: Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS][sap-ha-guide-figure-2005]

_**Figura 9:** Modello architetturale 2 a disponibilità elevata di SAP, con un cluster dedicato per ASCS/SCS e un cluster dedicato per DBMS_

### <a name="deployment-scenario-using-architectural-template-3"></a>Scenario di distribuzione usando il modello architetturale 3

La figura 10 illustra un esempio di architettura a disponibilità elevata di SAP NetWeaver in Azure per **due** sistemi SAP, con &lt;SID1&gt; e &lt;SID2&gt;. Questo scenario viene configurato come segue:

- Viene utilizzato un cluster dedicato per **entrambi** istanza hello SAP ASCS/SCS SID1 *e* istanza hello SAP ASCS/SCS SID2 (cluster).
- Un cluster dedicato viene usato per DBMS SID1 e un altro cluster dedicato viene usato per DBMS SID2 (due cluster).
- Le istanze di Server applicazioni SAP per il sistema SAP SID1 hello hanno le proprie macchine virtuali di dedicato.
- Le istanze di Server applicazioni SAP per il sistema SAP SID2 hello hanno le proprie macchine virtuali di dedicato.

![Figura 10: Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS][sap-ha-guide-figure-6003]

_**Figura 10:** Modello architetturale 3 a disponibilità elevata per SAP, con un cluster dedicato per istanze diverse di ASCS/SCS_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparare l'infrastruttura di hello

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Preparare l'infrastruttura di hello per 1 modello dell'architettura
I modelli di Azure Resource Manager per SAP consentono di semplificare la distribuzione delle risorse necessarie.

modelli a tre livelli di Hello in Gestione risorse di Azure supportano inoltre scenari a disponibilità elevata, ad esempio nel architetturale 1 di modello, che dispone di due cluster. Ogni cluster è un singolo punto di guasto SAP per SAP ASCS/SCS e DBMS.

Ecco dove ottenere i modelli di gestione risorse di Azure per uno scenario di esempio hello che descritti in questo articolo:

* [Immagine di Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Immagine di Azure Marketplace che usa Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Immagine personalizzata che usa Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

infrastruttura di hello tooprepare per architettura modello 1:

- Nel portale di Azure su hello hello **parametri** pannello in hello **SYSTEMAVAILABILITY** , quindi selezionare **a disponibilità elevata**.

  ![Figura 11: Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP][sap-ha-guide-figure-3000]

_**Figura 11:** Impostare i parametri di Azure Resource Manager di disponibilità elevata per SAP_


  creano modelli di Hello:

  * **Macchine virtuali**:
    * Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-di-<*Numero*>
    * Macchine virtuali del cluster ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Numero*>
    * Cluster DBMS: <*SIDSistemaSAP*>-db-<*Numero*>

  * **Schede di rete per tutte le macchine virtuali, con gli indirizzi IP associati**:
    * <*SIDSistemaSAP*&gt;-nic-di-&lt;*Numero*>
    * <*SIDSistemaSAP*>-nic-ascs-<*Numero*>
    * <*SIDSistemaSAP*>-nic-db-<*Numero*>

  * **Account di archiviazione di Azure (solo dischi non gestiti)**

  * **Gruppi di disponibilità** per:
    * Macchine virtuali del server applicazioni SAP: <*SIDSistemaSAP*>-avset-di
    * Macchine virtuali del cluster SAP ASCS/SCS: <*SIDSistemaSAP*>-avset-ascs
    * Macchine virtuali del cluster DBMS: <*SIDSistemaSAP*>-avset-db

  * **Servizio di bilanciamento del carico interno di Azure**:
    * Con tutte le porte per l'istanza di ASCS/SCS hello e l'indirizzo IP <*SAPSystemSID*> - lb - ascs
    * Con tutte le porte per hello DBMS di SQL Server e l'indirizzo IP <*SAPSystemSID*> - lb - db

  * **Gruppo di sicurezza di rete**: <*SIDSistemaSAP*>-nsg-ascs-0  
    * Con un toohello di porte Remote Desktop Protocol (RDP) esterno aprire <*SAPSystemSID*> macchina virtuale - ascs - 0

> [!NOTE]
> Tutti gli indirizzi IP delle schede di rete hello e servizi di bilanciamento del carico interno di Azure sono **dinamica** per impostazione predefinita. Modificarle troppo**statico** gli indirizzi IP. Viene descritto come toodo questo più avanti in articolo hello.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Distribuire le macchine virtuali con toouse (cross-premise) di connettività di rete aziendale nell'ambiente di produzione
Per i sistemi SAP di produzione, distribuire le macchine virtuali di Azure con la [connettività di rete aziendale (cross-premise)][planning-guide-2.2] usando la rete VPN da sito a sito di Azure o Azure ExpressRoute.

> [!NOTE]
> È possibile usare l'istanza di Rete virtuale di Azure. subnet e la rete virtuale hello già creati e preparati.
>
>

1.  Nel portale di Azure su hello hello **parametri** pannello in hello **NEWOREXISTINGSUBNET** , quindi selezionare **esistente**.
2.  In hello **struttura** , aggiungere una stringa completa di hello della rete Azure preparata struttura in cui si prevede toodeploy macchine virtuali di Azure.
3.  tooget un elenco di tutte le subnet di rete di Azure, eseguire questo comando di PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Hello **ID** campo Mostra hello **struttura**.
4. un elenco di tutti tooget **struttura** valori, eseguire questo comando di PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Hello **struttura** simile al seguente:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Distribuire delle istanze di SAP solo cloud a scopo di test e dimostrazione
È possibile distribuire il sistema SAP a disponibilità elevata in un modello di distribuzione solo cloud. Questo tipo di distribuzione è utile soprattutto per i casi d'uso di demo e test. Non è adatto per i casi d'uso in un ambiente di produzione.

- Nel portale di Azure su hello hello **parametri** pannello in hello **NEWOREXISTINGSUBNET** , quindi selezionare **nuova**. Lasciare hello **struttura** campo vuoto.

  Hello SAP Azure Resource Manager modello crea automaticamente hello subnet e rete virtuale di Azure.

> [!NOTE]
> È inoltre necessario toodeploy almeno uno dedicato macchina virtuale per Active Directory e DNS in hello stessa istanza di rete virtuale di Azure. modello di Hello non è possibile creare queste macchine virtuali.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Preparare l'infrastruttura di hello per 2 modello dell'architettura

È possibile utilizzare questo modello di gestione risorse di Azure per SAP toohelp semplificare la distribuzione delle risorse di infrastruttura necessaria per 2 modello architetturale SAP.

Ecco dove è possibile ottenere i modelli di Azure Resource Manager per questo scenario di distribuzione:

* [Immagine di Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Immagine di Azure Marketplace che usa Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Immagine personalizzata che usa Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Preparare l'infrastruttura di hello per 3 dell'architettura di modello

È possibile preparare l'infrastruttura di hello e configurare SAP per **multi-SID**. Ad esempio, è possibile aggiungere un'istanza di SAP ASCS/SCS aggiuntiva in una configurazione di cluster *esistente*. Per ulteriori informazioni, vedere [configurare un'altra istanza di SAP ASCS/SCS in un toocreate di configurazione di cluster una configurazione di multi-SID di SAP esistente in Azure Resource Manager][sap-ha-multi-sid-guide].

Se si desidera toocreate un nuovo cluster con più SID, è possibile utilizzare multi-SID hello [modelli delle Guide rapide su GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate un nuovo cluster con più SID, è necessario hello toodeploy tre modelli seguenti:

* [Modello di ASCS/SCS](#ASCS-SCS-template)
* [Modello di database](#database-template)
* [Modello dei server applicazioni](#application-servers-template)

Hello nelle sezioni seguenti sono riportati ulteriori dettagli sui modelli di hello e parametri hello è necessario tooprovide nei modelli di hello.

#### <a name="ASCS-SCS-template"></a> Modello di ASCS/SCS

modello ASCS/SCS Hello distribuisce due macchine virtuali che è possibile utilizzare un cluster di failover di Windows Server che ospita più istanze ASCS/SCS toocreate.

tooset un modello multi-SID ASCS/SCS hello, in hello [modello multi-SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] o [modello multi-SID ASCS/SCS utilizzando dischi gestiti] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], immettere i valori per hello seguenti parametri:

  - **Resource Prefix**.  Impostare hello risorse prefisso, tooprefix utilizzate tutte le risorse che vengono create durante la distribuzione di hello. Perché le risorse di hello non appartengono a un sistema SAP di tooonly, prefisso hello della risorsa hello non hello SID di un sistema SAP.  prefisso Hello deve essere compreso tra **tre a sei caratteri**.
  - **Stack Type**. Selezionare il tipo di stack hello di hello sistema SAP. In base al tipo di stack hello, bilanciamento del carico di Azure con uno (ABAP o Java solo) o due (ABAP + Java) indirizzi IP per ogni sistema SAP.
  -  **OS Type**. Selezionare il sistema operativo hello delle macchine virtuali hello.
  -  **SAP System Count**. Selezionare il numero di hello dei sistemi SAP si desidera tooinstall in questo cluster.
  -  **System Availability**. Selezionare **HA**.
  -  **Admin Username and Admin Password**. Creare un nuovo utente che può essere utilizzati toosign toohello macchina.
  -  **New Or Existing Subnet**. Impostare se devono essere create una nuova rete virtuale e una nuova subnet o se deve essere usata una subnet esistente. Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare **esistente**.
  -  **Subnet Id**. Impostare ID hello di hello toowhich di subnet hello devono essere connesse le macchine virtuali. Selezionare hello subnet della rete locale ExpressRoute rete virtuale tooconnect hello macchina virtuale tooyour o rete privata virtuale (VPN). ID Hello in genere è simile al seguente:

   /subscriptions/<*ID sottoscrizione*>/resourceGroups/<*nomegruppo risorse*>/providers/Microsoft.Network/VirtualNetwork/<*nome rete virtuale*>>/subnets/<*nome subnet*>

modello Hello consente di distribuire un'istanza di bilanciamento del carico di Azure, che supporta più sistemi SAP.

- Hello ASCS vengono configurate per numero di istanza 00, 10, 20...
- Hello SCS vengono configurate per numero di istanza 01, 11, 21...
- Hello ASCS Enqueue replica Server (Hiamanti) (solo Linux) vengono configurate per numero di istanza 02, 12, 22...
- Hello SCS Hiamanti (solo Linux) vengono configurate per numero di istanza 03, 13, 23...

servizio di bilanciamento del carico Hello contiene 1 (2 per Linux) VIP(s), 1 x VIP per ASCS/SCS e 1 x VIP per Hiamanti (solo Linux).

Hello elenco seguente sono contenuti tutti bilanciamento del carico (dove x è il numero di hello di hello sistema SAP, ad esempio, 1, 2, 3 e così via) di regole:
- Porte specifiche di Windows per ogni sistema SAP 445, 5985
- Porte ASCS (numero di istanza x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016
- Porte SCS (numero di istanza x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116
- Porte ASCS ERS in Linux (numero di istanza x2): 33x2, 5x213, 5x214, 5x216
- Porte SCS ERS in Linux (numero di istanza x3): 33x3, 5x313, 5x314, 5x316

servizio di bilanciamento del carico Hello è hello toouse configurato porte probe (dove x è il numero di hello di hello sistema SAP, ad esempio, 1, 2, 3 e così via) di seguito:
- Porta probe del servizio di bilanciamento del carico interno ASCS/SCS: 620x0
- Porta probe del servizio di bilanciamento del carico interno ERS (solo Linux): 621x2

#### <a name="database-template"></a> Modello di database

Consente di distribuire il modello di database Hello uno o due macchine virtuali che è possibile utilizzare tooinstall hello sistema di gestione di database relazionali (RDBMS) per un sistema SAP. Ad esempio, se si distribuisce un modello ASCS/SCS per cinque sistemi SAP, è necessario toodeploy questo modello cinque volte.

tooset un modello multi-SID di hello database, in hello [modello di database multi-SID] [ sap-templates-3-tier-multisid-db-marketplace-image] o [modello SID di più database utilizzando i dischi gestiti] [ sap-templates-3-tier-multisid-db-marketplace-image-md], immettere i valori per hello seguenti parametri:

  -  **Sap System Id**. Immettere l'ID sistema SAP di hello del sistema SAP si desidera tooinstall hello. ID Hello verrà considerato come prefisso per le risorse di hello che vengono distribuite.
  -  **Os Type**. Selezionare il sistema operativo hello delle macchine virtuali hello.
  -  **Dbtype**. Selezionare il tipo di hello del database hello desiderato tooinstall nel cluster hello. Selezionare **SQL** se si desidera tooinstall Microsoft SQL Server. Selezionare **HANA** se si prevede di macchine virtuali hello tooinstall SAP HANA. Verificare che tipo di sistema operativo corretto di hello tooselect: selezionare **Windows** per SQL, selezionare una distribuzione di Linux per HANA. Hello bilanciamento del carico di Azure che toohello connessa le macchine virtuali siano configurati toosupport il tipo di database hello selezionato:
    * **SQL**. servizio di bilanciamento del carico Hello sarà la porta 1433 il bilanciamento del carico. Verificare che toouse questa porta per l'installazione di SQL Server Always On.
    * **HANA**. servizio di bilanciamento del carico Hello sarà il bilanciamento del carico porte 35015 e 35017. Verificare che tooinstall SAP HANA con numero di istanza **50**.
    servizio di bilanciamento del carico Hello utilizzerà la porta probe 62550.
  -  **Sap System Size**. Numero di set hello del nuovo sistema SAP hello fornirà. Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere al SAP tecnologia Partner o l'integratore di sistema.
  -  **System Availability**. Selezionare **HA**.
  -  **Admin Username and Admin Password**. Creare un nuovo utente che può essere utilizzati toosign toohello macchina.
  -  **Subnet Id**. Immettere hello ID di subnet hello utilizzati durante la distribuzione di hello del modello ASCS/SCS hello, o hello della subnet hello che è stato creato come parte della distribuzione del modello ASCS/SCS hello.

#### <a name="application-servers-template"></a> Modello dei server applicazioni

modello di server dell'applicazione Hello distribuisce due o più macchine virtuali che può essere usate come istanze del Server applicazioni SAP per un sistema SAP. Ad esempio, se si distribuisce un modello ASCS/SCS per cinque sistemi SAP, è necessario toodeploy questo modello cinque volte.

tooset backup hello server multi-SID modello di applicazione, in hello [modello di applicazione server multi-SID] [ sap-templates-3-tier-multisid-apps-marketplace-image] o [modello di applicazione multi-SID server utilizzando i dischi gestiti] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], immettere i valori per hello seguenti parametri:

  -  **Sap System Id**. Immettere l'ID sistema SAP di hello del sistema SAP si desidera tooinstall hello. ID Hello verrà considerato come prefisso per le risorse di hello che vengono distribuite.
  -  **Os Type**. Selezionare il sistema operativo hello delle macchine virtuali hello.
  -  **Sap System Size**. numero di Hello del nuovo sistema SAP hello fornirà. Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere al SAP tecnologia Partner o l'integratore di sistema.
  -  **System Availability**. Selezionare **HA**.
  -  **Admin Username and Admin Password**. Creare un nuovo utente che può essere utilizzati toosign toohello macchina.
  -  **Subnet Id**. Immettere hello ID di subnet hello utilizzati durante la distribuzione di hello del modello ASCS/SCS hello, o hello della subnet hello che è stato creato come parte della distribuzione del modello ASCS/SCS hello.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rete virtuale di Azure
In questo esempio, spazio degli indirizzi di hello di hello rete virtuale di Azure è 10.0.0.0/16. Esiste una subnet denominata **Subnet**, con un intervallo di indirizzi di 10.0.0.0/24. Tutte le macchine virtuali e i servizi di bilanciamento del carico interni vengono distribuiti in questa rete virtuale.

> [!IMPORTANT]
> Non apportare alcuna modifica le impostazioni di rete toohello all'interno del sistema operativo guest di hello. inclusi indirizzi IP, server DNS e la subnet. Configurare tutte le impostazioni di rete in Azure. il servizio Dynamic Host Configuration Protocol (DHCP) Hello propaga le impostazioni.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Indirizzi IP DNS

hello tooset necessarie che agli indirizzi IP di DNS, hello alla procedura seguente.

1.  Nel portale di Azure su hello hello **server DNS** pannello, assicurarsi che la rete virtuale **server DNS** impostazione troppo**DNS personalizzato**.
2.  Selezionare le impostazioni in base al tipo di hello della rete che si dispone. Per ulteriori informazioni, vedere hello seguenti risorse:
    * [Connettività di rete aziendale (cross-premise)][planning-guide-2.2]: aggiungere gli indirizzi IP hello del server DNS locali di hello.  
    È possibile estendere locale DNS server toohello macchine virtuali che sono in esecuzione in Azure. In questo scenario, è possibile aggiungere gli indirizzi IP hello di hello Azure le macchine virtuali in cui viene eseguito il servizio DNS hello.
    * [Distribuzione solo cloud][planning-guide-2.1]: distribuire una macchina virtuale supplementare in hello stessa istanza di rete virtuale che funge da un server DNS. Aggiungere gli indirizzi IP hello di hello Azure le macchine virtuali che hai configurato il servizio DNS toorun.

    ![Figura 12: Configurare i server DNS per Rete virtuale di Azure][sap-ha-guide-figure-3001]

    _**Figura 12:** Configurare i server DNS per Rete virtuale di Azure_

  > [!NOTE]
  > Se si modificano gli indirizzi IP hello del server DNS hello, è necessario toorestart hello macchine virtuali di Azure tooapply hello modifica e propagare hello nuovi server.
  >
  >

In questo esempio, hello servizio DNS viene installato e configurato in tali macchine virtuali Windows:

| Ruolo macchina virtuale | Nome host macchina virtuale | Nome scheda di rete | Indirizzo IP statico |
| --- | --- | --- | --- |
| Primo server DNS |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| Secondo server DNS |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>I nomi host e indirizzi IP statici per l'istanza cluster di SAP ASCS/SCS hello e istanza in cluster DBMS

Per una distribuzione locale, sono necessari questi nomi host e indirizzi IP riservati:

| Ruolo nome host virtuale | Nome host virtuale | Indirizzo IP statico virtuale |
| --- | --- | --- |
| Primo nome host virtuale del cluster SAP ASCS/SCS (per la gestione del cluster) |pr1-ascs-vir |10.0.0.42 |
| Nome host virtuale dell'istanza di SAP ASCS/SCS |pr1-ascs-sap |10.0.0.43 |
| Secondo nome host virtuale del cluster SAP DBMS (gestione del cluster) |pr1-dbms-vir |10.0.0.32 |

Quando si crea il cluster di hello, creare hello nomi host virtuali **pr1-ascs-vir** e **pr1-dbms-vir** e hello associati gli indirizzi IP per la gestione di cluster hello stesso. Per informazioni su come toodo questa operazione, vedere [raccogliere i nodi del cluster in una configurazione cluster][sap-ha-guide-8.12.1].

È possibile creare manualmente hello altri due nomi host virtuale, **pr1-sap ascs** e **pr1-dbms-sap**, e hello associati gli indirizzi IP, sul server DNS hello. Hello istanza SAP ASCS/SCS cluster e l'istanza DBMS hello cluster utilizza queste risorse. Per informazioni su come toodo questa operazione, vedere [creare un nome host virtuale per un'istanza di SAP ASCS/SCS cluster][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Impostare gli indirizzi IP statici per le macchine virtuali SAP hello
Dopo aver distribuito hello toouse di macchine virtuali del cluster, è necessario indirizzi IP statici tooset per tutte le macchine virtuali. Eseguire questa operazione nella configurazione di rete virtuale di Azure hello e non nel sistema operativo guest di hello.

1.  Nel portale di Azure hello, selezionare **gruppo di risorse** > **scheda di rete** > **impostazioni** > **indirizzo IP** .
2.  In hello **gli indirizzi IP** pannello, in **assegnazione**selezionare **statico**. In hello **indirizzo IP** , immettere l'indirizzo IP hello che si desidera toouse.

  > [!NOTE]
  > Se si modifica l'indirizzo IP hello hello della scheda di rete, è necessario toorestart hello macchine virtuali di Azure tooapply hello modifica.  
  >
  >

  ![Figura 13: Impostare gli indirizzi IP statici per la scheda di rete hello di ogni macchina virtuale][sap-ha-guide-figure-3002]

  _**Figura 13:** impostare gli indirizzi IP statici per la scheda di rete hello di ogni macchina virtuale_

  Ripetere questo passaggio per tutte le interfacce di rete, ovvero per tutte le macchine virtuali, incluse le macchine virtuali che si desidera toouse per il servizio Active Directory/DNS.

In questo esempio vengono usate le macchine virtuali e gli indirizzi IP statici seguenti:

| Ruolo macchina virtuale | Nome host macchina virtuale | Nome scheda di rete | Indirizzo IP statico |
| --- | --- | --- | --- |
| Prima istanza del server applicazioni SAP |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| Seconda istanza del server applicazioni SAP |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Ultima istanza del server applicazioni SAP |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| Primo nodo del cluster per l'istanza di ASCS/SCS |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| Secondo nodo del cluster per l'istanza di ASCS/SCS |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| Primo nodo del cluster per l'istanza di DBMS |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| Secondo nodo del cluster per l'istanza di DBMS |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Impostare un indirizzo IP statico per servizio di bilanciamento del carico interno di Azure hello

modello di gestione risorse di Azure SAP Hello crea un servizio di bilanciamento del carico interno di Azure che viene utilizzato per cluster di istanze di SAP ASCS/SCS hello e cluster DBMS hello.

> [!IMPORTANT]
> Hello l'indirizzo IP del nome host virtuale hello hello SAP ASCS/SCS è hello stesso come indirizzo IP hello di bilanciamento del carico interno di SAP ASCS/SCS hello: **pr1-lb-ascs**.
> Hello l'indirizzo IP del nome del DBMS è hello virtuale hello hello stesso come indirizzo IP hello di bilanciamento del carico interno DBMS hello: **pr1 lb-dbms**.
>
>

un indirizzo IP statico per hello Azure interno tooset bilanciamento del carico:

1.  Hello distribuzione iniziale Imposta indirizzo IP di bilanciamento del carico interno di hello troppo**dinamica**. Nel portale di Azure su hello hello **gli indirizzi IP** pannello, in **assegnazione**selezionare **statico**.
2.  Impostare l'indirizzo IP hello del bilanciamento del carico interno hello **pr1-lb-ascs** toohello l'indirizzo IP del nome host virtuale hello dell'istanza di SAP ASCS/SCS hello.
3.  Impostare l'indirizzo IP hello del bilanciamento del carico interno hello **pr1 lb-dbms** toohello l'indirizzo IP del nome host virtuale hello dell'istanza DBMS hello.

  ![Nella figura 14: Impostare gli indirizzi IP statici per servizio di bilanciamento del carico interno hello per istanza di SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  _**Nella figura 14:** impostare gli indirizzi IP statici per servizio di bilanciamento del carico interno hello per istanza di SAP ASCS/SCS hello_

Nell'esempio sono presenti due servizi di bilanciamento del carico interno di Azure con questi indirizzi IP statici:

| Ruolo del servizio di bilanciamento del carico interno di Azure | Nome del servizio di bilanciamento del carico interno di Azure | Indirizzo IP statico |
| --- | --- | --- |
| Servizio di bilanciamento del carico interno dell'istanza di SAP ASCS/SCS |pr1-lb-ascs |10.0.0.43 |
| Servizio di bilanciamento del carico interno di SAP DBMS |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico ASCS/SCS predefinito

modello di gestione risorse di Azure SAP Hello Crea porte hello che è necessario:
* Un'istanza di ABAP ASCS, con numero di istanza predefinito hello **00**
* Un'istanza di Java SCS, con numero di istanza predefinito hello **01**

Quando si installa l'istanza di SAP ASCS/SCS, è necessario utilizzare un numero di istanza predefinito hello **00** per il numero ABAP ASCS hello e di istanza predefinito istanza **01** per l'istanza di Java SCS.

Creare quindi richiesto di endpoint per le porte di SAP NetWeaver hello di bilanciamento del carico interno.

toocreate richiesto endpoint di bilanciamento del carico interno, creare in primo luogo, questi endpoint per le porte di SAP NetWeaver ABAP ASCS hello di bilanciamento del carico:

| Servizio/nome regola di bilanciamento del carico | Numeri porte predefinite | Porte concrete per (istanza ASCS con l'istanza numero 00) (ERS con 10) |
| --- | --- | --- |
| Server di accodamento/ *lbrule3200* |32<*NumeroIstanza*> |3200 |
| Server messaggi ABAP/ *lbrule3600* |36<*NumeroIstanza*> |3600 |
| Messaggio ABAP interno/ *lbrule3900* |39<*NumeroIstanza*> |3900 |
| HTTP server messaggi/ *Lbrule8100* |81<*NumeroIstanza*> |8100 |
| SAP Start Service ASCS HTTP/ *Lbrule50013* |5<*NumeroIstanza*>13 |50013 |
| SAP Start Service ASCS HTTPS/ *Lbrule50014* |5<*NumeroIstanza*>14 |50014 |
| Replica di accodamento/ *Lbrule50016* |5<*NumeroIstanza*>16 |50016 |
| SAP Start Service ERS HTTP *Lbrule51013* |5<*NumeroIstanza*>13 |51013 |
| SAP Start Service ERS HTTP *Lbrule51014* |5<*NumeroIstanza*>14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| Condivisione file *Lbrule445* | |445 |

_**Tabella 1:** porta un numero di istanze di SAP NetWeaver ABAP ASCS hello_

Quindi, creare questi endpoint per le porte di SAP NetWeaver Java SCS hello di bilanciamento del carico:

| Servizio/nome regola di bilanciamento del carico | Numeri porte predefinite | Porte concrete per (istanza SCS con numero di istanza 01) (ERS con 11) |
| --- | --- | --- |
| Server di accodamento/ *lbrule3201* |32<*NumeroIstanza*> |3201 |
| Server gateway/ *lbrule3301* |33<*NumeroIstanza*> |3301 |
| Server messaggi Java/ *lbrule3900* |39<*NumeroIstanza*> |3901 |
| HTTP server messaggi/ *Lbrule8101* |81<*NumeroIstanza*> |8101 |
| SAP Start Service SCS HTTP/ *Lbrule50113* |5<*NumeroIstanza*>13 |50113 |
| SAP Start Service SCS HTTPS/ *Lbrule50114* |5<*NumeroIstanza*>14 |50114 |
| Replica di accodamento/ *Lbrule50116* |5<*NumeroIstanza*>16 |50116 |
| SAP Start Service ERS HTTP *Lbrule51113* |5<*NumeroIstanza*>13 |51113 |
| SAP Start Service ERS HTTP *Lbrule51114* |5<*NumeroIstanza*>14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| Condivisione file *Lbrule445* | |445 |

_**Tabella 2:** porta un numero di istanze di SAP NetWeaver Java SCS hello_

![Figura 15: Predefinito ASCS/SCS bilanciamento del carico regole di bilanciamento del carico interno di Azure hello][sap-ha-guide-figure-3004]

_**Figura 15:** regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico ASCS/SCS predefinito_

Impostare l'indirizzo IP hello di bilanciamento del carico hello **pr1 lb-dbms** toohello l'indirizzo IP del nome host virtuale hello dell'istanza DBMS hello.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Modificare le regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico di predefinito di hello ASCS/SCS

Se si desidera numeri diversi toouse per hello SAP ASCS o istanze SCS, è necessario modificare hello nomi e valori delle relative porte dai valori predefiniti.

1.  Nel portale di Azure hello, selezionare  **<* SID*> - lb - ascs caricare bilanciamento * * > **regole di bilanciamento del carico**.
2.  Per le regole che appartengono a toohello SAP ASCS o istanza SCS di bilanciamento del carico tutti, è possibile modificare questi valori:

  * Nome
  * Porta
  * Porta back-end

  Ad esempio, se si desidera toochange hello predefinito ASCS del numero di istanza da too31 00, è necessario modifiche hello toomake per tutte le porte elencate nella tabella 1.

  Ecco un esempio di aggiornamento per la porta *lbrule3200*.

  ![Figura 16: Modificare le regole di bilanciamento del carico interno di Azure hello di bilanciamento del carico di predefinito di hello ASCS/SCS][sap-ha-guide-figure-3005]

  _**Figura 16:** modifica hello ASCS/SCS predefinito bilanciamento carico di regole di bilanciamento del carico interno di Azure hello_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Aggiungi dominio toohello macchine virtuali di Windows

Dopo aver assegnato una macchina virtuale toohello di indirizzo IP statico, aggiungere dominio toohello di hello macchine virtuali.

![Figura 17: Aggiungere un dominio tooa macchina virtuale][sap-ha-guide-figure-3006]

_**Figura 17:** aggiungere un dominio tooa macchina virtuale_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Aggiungere le voci del Registro di sistema in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello

Bilanciamento del carico di Azure è un servizio di bilanciamento del carico interno che si chiude le connessioni quando le connessioni hello sono inattive per un determinato periodo di tempo (un timeout di inattività). Processi di lavoro SAP nella finestra di dialogo istanze connessioni aperte toohello SAP enqueue elaborare appena hello prima enqueue o dequeue richiesta toobe esigenze inviato. Queste connessioni rimangono in genere stabilite finché il processo di lavoro hello o hello enqueue processo viene riavviato. Tuttavia, se la connessione hello è inattiva per un determinato periodo di tempo, hello connessioni hello chiude bilanciamento di carico interno di Azure. Ciò non rappresenta un problema perché il processo di lavoro SAP hello ristabilita processo enqueue toohello di hello connessione se non esiste più. Queste attività sono documentate nelle tracce di sviluppatore hello dei processi SAP, ma creano una grande quantità di contenuto aggiuntivo in tali tracce. È un hello toochange buona TCP/IP `KeepAliveTime` e `KeepAliveInterval` in entrambi i nodi del cluster. Combinare le modifiche nei parametri TCP/IP hello con parametri di profilo SAP, descritti più avanti nell'articolo di hello.

le voci del Registro di sistema tooadd in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello, aggiungono innanzitutto queste voci del Registro di sistema di Windows in entrambi i nodi del cluster di Windows per SAP ASCS/SCS:

| Path | HKLM\System\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome variabile |`KeepAliveTime` |
| Tipo di variabile |REG_DWORD (decimale) |
| Valore |120000 |
| Collegamento toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabella 3:** parametro TCP/IP prima della modifica hello_

Aggiungere quindi le voci del Registro di sistema Windows in entrambi i nodi del cluster Windows per SAP ASCS/SCS:

| Path | HKLM\System\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome variabile |`KeepAliveInterval` |
| Tipo di variabile |REG_DWORD (decimale) |
| Valore |120000 |
| Collegamento toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabella 4:** modifica hello secondo TCP/IP parametro_

**modifiche di hello tooapply, riavviare entrambi i nodi del cluster**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurare un cluster di Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS

La configurazione di un cluster Windows Server Failover Clustering per un'istanza di SAP ASCS/SCS prevede queste attività:

- La raccolta di nodi del cluster hello in una configurazione cluster
- Configurazione di un controllo di condivisione file del cluster

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Raccogliere i nodi del cluster hello in una configurazione cluster

1.  Hello Add Role guidata e funzionalità, aggiungere i nodi del cluster tooboth di clustering di failover.
2.  Configurare il cluster di failover di hello utilizzando Gestione Cluster di Failover. In Gestione Cluster di Failover, selezionare **crea Cluster**e quindi aggiungere solo hello nome del cluster prima di hello, il nodo A. Non aggiungere hello secondo nodo. secondo nodo hello verrà aggiunto in un passaggio successivo.

  ![Figura 18: Aggiungere server hello o un nome macchina virtuale del primo nodo del cluster hello][sap-ha-guide-figure-3007]

  _**Figura 18:** Aggiungi hello server o macchina virtuale il nome del primo nodo del cluster hello_

3.  Immettere il nome di rete hello (nome host virtuale) del cluster di hello.

  ![Figura 19: Immettere il nome del cluster hello][sap-ha-guide-figure-3008]

  _**Figura 19:** immettere il nome del cluster hello_

4.  Dopo aver creato il cluster hello, eseguire un test di convalida del cluster.

  ![Figura 20: Esecuzione del controllo di convalida cluster hello][sap-ha-guide-figure-3009]

  _**Figura 20:** esecuzione del controllo di convalida cluster hello_

  È possibile ignorare eventuali avvisi relativi a questo punto i dischi nel processo di hello. Si aggiungerà che una condivisione file di controllo e hello SIOS dischi condivisi in un secondo momento. In questa fase, non è necessario tooworry sulla presenza di un quorum.

  ![Figura 21: Nessun disco quorum trovato][sap-ha-guide-figure-3010]

  _**Figura 21:** Nessun disco quorum trovato_

  ![Figura 22: La risorsa del cluster principale richiede un nuovo indirizzo IP][sap-ha-guide-figure-3011]

  _**Figura 22:** La risorsa del cluster principale richiede un nuovo indirizzo IP_

5.  Modificare l'indirizzo IP di hello del servizio cluster di hello core. cluster Hello Impossibile avviare finché non si modifica l'indirizzo IP di hello del servizio cluster di hello core, indirizzo IP di hello del server hello punta tooone dei nodi di hello macchina virtuale. Effettuare questa operazione su hello **proprietà** pagina della risorsa IP del servizio di hello core del cluster.

  Ad esempio, è necessario un indirizzo IP tooassign (in questo esempio, **10.0.0.42**) per nome host virtuale del cluster hello **pr1-ascs-vir**.

  ![Nella figura 23: Nella finestra di dialogo Proprietà hello, modificare l'indirizzo IP hello][sap-ha-guide-figure-3012]

  _**Nella figura 23:** In hello **proprietà** della finestra di dialogo Modifica indirizzo IP di hello_

  ![Figura 24: Assegnare l'indirizzo IP hello è riservato per il cluster hello][sap-ha-guide-figure-3013]

  _**Figura 24:** Assegnazione indirizzo IP hello riservata per il cluster hello_

6.  Portare hello host virtuale nome del cluster online.

  ![Figura 25: Servizio di base del Cluster sia attivo e in esecuzione e hello correggere l'indirizzo IP][sap-ha-guide-figure-3014]

  _**Figura 25:** servizio principale del Cluster sia attivo e in esecuzione e con hello correggere l'indirizzo IP_

7.  Aggiungere hello secondo nodo del cluster.

  Ora che il servizio cluster core hello sia in esecuzione, è possibile aggiungere secondo nodo del cluster hello.

  ![Figura 26: Aggiungere hello secondo nodo del cluster][sap-ha-guide-figure-3015]

  _**Figura 26:** Aggiungi hello secondo nodo del cluster_

8.  Immettere un nome per il secondo host di nodo del cluster di hello.

  ![Figura 27: Immettere nome host nodo hello secondo cluster][sap-ha-guide-figure-3016]

  _**Figura 27:** invio hello secondo host nome del nodo cluster_

  > [!IMPORTANT]
  > Assicurarsi che hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster** casella di controllo è **non** selezionato.  
  >
  >

  ![Figura 28: Non selezionare la casella di controllo hello][sap-ha-guide-figure-3017]

  _**Figura 28:** si **non** selezionare hello casella di controllo_

  È possibile ignorare gli avvisi relativi al quorum e ai dischi. Si imposteranno hello quorum e condivisione hello disco in un secondo momento, come descritto in [installazione SIOS DataKeeper Cluster Edition per la condivisione del disco del cluster di SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Figura 29: Ignorare gli avvisi sul quorum disco hello][sap-ha-guide-figure-3018]

  _**Figura 29:** ignorare gli avvisi sul quorum disco hello_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurare il controllo di condivisione file del cluster

La configurazione di un controllo di condivisione file del cluster prevede queste attività:

- Creazione di una condivisione file
- L'impostazione di quorum di controllo condivisione file hello in Gestione Cluster di Failover

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creare una condivisione file

1.  Selezionare un controllo di condivisione file invece di un disco quorum. SIOS DataKeeper supporta questa opzione.

  Negli esempi di hello in questo articolo, hello witness di condivisione file è nel server di Active Directory/DNS hello è in esecuzione in Azure. Hello condivisione file di controllo viene chiamato **domcontr 0**. Poiché potrebbe aver configurato un tooAzure di connessione VPN (tramite VPN Site-to-Site o ExpressRoute di Azure), il/DNS di Active Directory service è locale e non è adatto toorun un file di condividere controllo del mirroring.

  > [!NOTE]
  > Se il servizio Active Directory/DNS viene eseguito solo in locale, non si configura la condivisione file di controllo nel sistema operativo di Active Directory/DNS Windows hello che è in esecuzione in locale. La latenza di rete tra i nodi del cluster in esecuzione in Azure e Active Directory/DNS in locale potrebbe essere eccessiva e causare problemi di connettività. Impossibile verificare tooconfigure hello witness di condivisione file in una macchina virtuale di Azure che esegue toohello Chiudi nodo del cluster.  
  >
  >

  unità quorum Hello richiede almeno 1024 MB di spazio libero. È consigliabile 2048 MB di spazio disponibile per l'unità quorum hello.

2.  Aggiungere l'oggetto nome cluster di hello.

  ![Figura 30: Assegnare le autorizzazioni hello hello condivisione per l'oggetto nome cluster di hello][sap-ha-guide-figure-3019]

  _**Figura 30:** assegnare autorizzazioni hello nella condivisione di hello per l'oggetto nome cluster di hello_

  Assicurarsi che le autorizzazioni di hello includano dati di hello autorità toochange nella condivisione di hello per l'oggetto nome cluster di hello (in questo esempio, **pr1-ascs-vir$**).

3.  tooadd hello cluster nome oggetto toohello elenco, selezionare **Aggiungi**. Modificare hello toocheck di filtro per gli oggetti computer, in aggiunta toothose illustrato nella figura 31.

  ![Figura 31: Modificare i computer tooinclude di tipi di oggetto hello][sap-ha-guide-figure-3020]

  _**Figura 31:** cambia hello tipi di oggetto tooinclude computer_

  ![32 figura: Casella di controllo di computer selezionare hello][sap-ha-guide-figure-3021]

  _**Nella figura 32:** hello seleziona **computer** casella di controllo_

4.  Immettere il oggetto nome cluster hello come illustrato nella figura 31. Poiché è già stato creato il record di hello, è possibile modificare le autorizzazioni di hello, come illustrato nella figura 30.

5.  Seleziona hello **sicurezza** scheda della condivisione hello e quindi impostare più dettagliato le autorizzazioni per l'oggetto nome cluster di hello.

  ![Figura 33: Impostare gli attributi di sicurezza di hello per l'oggetto nome cluster di hello in quorum di condivisione file hello][sap-ha-guide-figure-3022]

  _**Nella figura 33:** impostare gli attributi di sicurezza hello per l'oggetto nome cluster di hello in quorum di condivisione file hello_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Impostare quorum di controllo condivisione file hello in Gestione Cluster di Failover

1.  Aprire configurazione Quorum impostazione guidata hello.

  ![Figura 34: Avviare hello guidata Configura impostazioni Quorum del Cluster][sap-ha-guide-figure-3023]

  _**Figura 34:** inizio hello configurazione guidata impostazioni Quorum del Cluster_

2.  In hello **selezionare configurazione Quorum** selezionare **selezione quorum di controllo hello**.

  ![Figura 35: Configurazioni del quorum tra cui è possibile scegliere][sap-ha-guide-figure-3024]

  _**Figura 35:** Configurazioni del quorum tra cui è possibile scegliere_

3.  In hello **selezione Quorum di controllo** selezionare **configurare una condivisione file di controllo**.

  ![36 figura: Controllo di condivisione file hello selezionare][sap-ha-guide-figure-3025]

  _**Nella figura 36:** selezionare hello witness di condivisione file_

4.  Immettere una condivisione di file toohello percorso UNC hello (in questo esempio, \\domcontr 0\FSW). un elenco di hello le modifiche apportate, selezionare toosee **Avanti**.

  ![Figura 37: Definire percorso della condivisione file hello per la condivisione di controllo hello][sap-ha-guide-figure-3026]

  _**Figura 37:** definire percorso della condivisione file hello per la condivisione di controllo hello_

5.  Selezionare le modifiche di hello desiderato e quindi selezionare **Avanti**. È necessario toosuccessfully riconfigurare configurazione cluster hello, come illustrato nella figura 38.  

  ![Nella figura 38: Conferma che è stato riconfigurato cluster hello][sap-ha-guide-figure-3027]

  _**Nella figura 38:** conferma che è stato riconfigurato cluster hello_

Dopo l'installazione di un Cluster di Failover di Windows hello correttamente, è necessario modifiche toobe apportate toosome soglie tooadapt failover rilevamento tooconditions in Azure. Hello toobe parametri modificati sono documentati in questo blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Presupponendo che le due macchine virtuali che compila hello configurazione di Cluster di Windows per ASCS/SCS sono hello stessa SubNet, i seguenti parametri hello necessari valori toothese toobe modificato:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Queste impostazioni sono state testate con clienti e fornite toobe un buon compromesso sufficientemente flessibili nel lato "uno" hello. In hello invece tali impostazioni sono state fornendo fast sufficiente failover nelle condizioni di errore in caso di errore SAP software o nodo/macchina virtuale. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Installare l'edizione Cluster di SIOS DataKeeper per disco condivisione del cluster di SAP ASCS/SCS hello

Ora è disponibile una configurazione funzionante di Windows Server Failover Clustering in Azure Ma, tooinstall un'istanza di SAP ASCS/SCS, è necessario utilizzare una risorsa disco condiviso. È possibile creare le risorse disco condivise hello che è necessario in Azure. SIOS DataKeeper Cluster Edition è una soluzione di terze parti è possibile utilizzare le risorse disco condivise toocreate.

Installazione di SIOS DataKeeper Cluster Edition per SAP ASCS/SCS hello disco del cluster di condivisione include le attività:

- Aggiunta di hello .NET Framework 3.5
- Installazione di SIOS DataKeeper
- Configurazione di SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Aggiungere hello .NET Framework 3.5
Hello Microsoft .NET Framework 3.5 non viene automaticamente attivato o installato in Windows Server 2012 R2. Poiché SIOS DataKeeper richiede hello toobe di .NET Framework in tutti i nodi che si installa DataKeeper in, è necessario installare .NET Framework 3.5 hello nel sistema operativo guest di hello di tutte le macchine virtuali in cluster hello.

Esistono due hello di tooadd metodi .NET Framework 3.5:

- Utilizzare hello Aggiunta guidata ruoli e funzionalità in Windows, come illustrato nella figura 39.

  ![Figura 39: Installare .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3028]

  _**Nella figura 39:** hello installare .NET Framework 3.5 utilizzando hello Aggiunta guidata ruoli e funzionalità_

  ![Figura 40: Installazione indicatore di stato quando si installa .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità][sap-ha-guide-figure-3029]

  _**Figura 40:** indicatore quando si installa .NET Framework 3.5 hello utilizzando hello Aggiunta guidata ruoli e funzionalità di installazione_

- Utilizzare hello strumento da riga di comando dism.exe. Per questo tipo di installazione, è necessario tooaccess hello SxS directory hello supporti di installazione di Windows. A un prompt dei comandi con privilegi elevati digitare:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> Installare SIOS DataKeeper

Installare l'edizione Cluster di SIOS DataKeeper su ogni nodo nel cluster hello. archiviazione condivisa virtuale toocreate con SIOS DataKeeper, creare un mirror sincronizzato e simulare archiviazione condivisa cluster.

Prima di installare il software SIOS hello, creare l'utente di dominio di hello **DataKeeperSvc**.

> [!NOTE]
> Aggiungere hello **DataKeeperSvc** utente toohello **amministratore locale** gruppo in entrambi i nodi del cluster.
>
>

tooinstall SIOS DataKeeper:

1.  Installare il software SIOS hello in entrambi i nodi del cluster.

  ![Programma di installazione SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Prima pagina di installazione di SIOS DataKeeper hello][sap-ha-guide-figure-3031]

  _**Figura 41:** prima pagina di installazione di SIOS DataKeeper hello_

2.  Selezionare la finestra di dialogo hello illustrata nella figura 42, **Sì**.

  ![Figura 42: DataKeeper segnala che un servizio verrà disabilitato][sap-ha-guide-figure-3032]

  _**Figura 42:** DataKeeper segnala che un servizio verrà disabilitato_

3.  Nella finestra di dialogo hello illustrata nella figura 43, è consigliabile selezionare **account di dominio o Server**.

  ![Figura 43: Selezione dell'utente per SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Figura 43:** Selezione dell'utente per SIOS DataKeeper_

4.  Immettere nome utente dell'account di dominio hello e la password creata per SIOS DataKeeper.

  ![Figura 44: Immettere nome utente di dominio hello e una password per hello installazione SIOS DataKeeper][sap-ha-guide-figure-3034]

  _**Figura 44:** immettere nome utente di dominio hello e la password per l'installazione di SIOS DataKeeper hello_

5.  Installare hello chiave di licenza per l'istanza di SIOS DataKeeper, come illustrato nella Figura 45.

  ![Figura 45: Specificare la chiave di licenza di SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Figura 45:** Specificare la chiave di licenza di SIOS DataKeeper_

6.  Quando richiesto, riavviare la macchina virtuale hello.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurare SIOS DataKeeper

Dopo aver installato SIOS DataKeeper in entrambi i nodi, è necessario configurazione hello toostart. obiettivo di Hello della configurazione di hello è la replica di dati sincroni toohave tra dischi aggiuntivi hello collegato tooeach delle macchine virtuali hello.

1.  Avviare Gestione DataKeeper hello e strumento di configurazione e quindi selezionare **Connetti Server**. Nella figura 46, questa opzione è racchiusa in un cerchio rosso.

  ![Figura 46: Strumento di configurazione e gestione di SIOS DataKeeper][sap-ha-guide-figure-3036]

  _**Figura 46:** Strumento di configurazione e gestione di SIOS DataKeeper_

2.  Immettere il nome di hello o indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve connettersi a e, in un secondo passaggio, secondo nodo hello.

  ![Figura 47: Nome hello inserimento o l'indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve collegarsi a e, in un secondo passaggio, secondo nodo hello][sap-ha-guide-figure-3037]

  _**Figura 47:** nome hello inserimento o l'indirizzo TCP/IP hello primo nodo hello gestione e la configurazione dello strumento di deve collegarsi a e, in un secondo passaggio, secondo nodo hello_

3.  Creare il processo di replica hello tra due nodi hello.

  ![Figura 48: Creare un processo di replica][sap-ha-guide-figure-3038]

  _**Figura 48:** Creare un processo di replica_

  Una procedura guidata semplificato il processo di hello di creazione di un processo di replica.
4.  Definire nome hello indirizzo TCP/IP e il volume del disco del nodo di origine hello.

  ![Figura 49: Definire il nome di hello del processo di replica hello][sap-ha-guide-figure-3039]

  _**Figura 49:** nome hello di definizione del processo di replica hello_

  ![Figura 50: Definire i dati di base per il nodo hello, che deve essere il nodo di origine corrente hello hello][sap-ha-guide-figure-3040]

  _**Figura 50:** definire dati di base per il nodo hello, che deve essere il nodo di origine corrente hello hello_

5.  Definire nome hello indirizzo TCP/IP e il volume del disco del nodo di destinazione hello.

  ![Figura 51: Definire i dati di base per il nodo hello, che deve essere il nodo di destinazione corrente hello hello][sap-ha-guide-figure-3041]

  _**Figura 51:** definire dati di base per il nodo hello, che deve essere il nodo di destinazione corrente hello hello_

6.  Definire gli algoritmi di compressione hello. In questo esempio, è consigliabile comprimere il flusso di replica hello. Specialmente in situazioni di risincronizzazione, la compressione di hello del flusso di replica hello riduce notevolmente il tempo di risincronizzazione. Si noti che la compressione utilizza risorse di CPU e RAM hello di una macchina virtuale. Man mano che aumenta la velocità di compressione hello, pertanto hello volume delle risorse della CPU utilizzato. È possibile anche modificare questa impostazione in un secondo momento.

7.  Un'altra impostazione necessaria toocheck è se hello replica sincrona o asincrona. *Per proteggere le configurazioni di SAP ASCS/SCS, è necessario usare la replica sincrona*.  

  ![Figura 52: Definire i dettagli della replica][sap-ha-guide-figure-3042]

  _**Figura 52:** Definire i dettagli della replica_

8.  Definire se volume hello replicato dal processo di replica hello deve essere di configurazione del cluster Windows Server Failover Clustering tooa rappresentato come un disco condiviso. Per la configurazione di SAP ASCS/SCS hello, selezionare **Sì** in modo che Windows hello cluster vede hello volume replicati come un disco condiviso che è possibile utilizzare come un volume del cluster.

  ![Figura 53: Hello tooset selezionare Sì replicate volume come volume del cluster][sap-ha-guide-figure-3043]

  _**Figura 53:** selezionare **Sì** tooset hello volume come volume di cluster di replicate_

  Dopo aver creato il volume di hello, lo strumento di configurazione e gestione DataKeeper hello viene illustrato che tale processo di replica hello è attivo.

  ![Figura 54: Mirroring sincrono DataKeeper per SAP ASCS/SCS condivisione disco hello è attivo][sap-ha-guide-figure-3044]

  _**Figura 54:** mirroring sincrono DataKeeper per SAP ASCS/SCS hello condividere disco è attivo_

  Gestione Cluster di failover viene ora disco hello come disco DataKeeper, come illustrato nella Figura 55.

  ![Figura 55: In Gestione Cluster di Failover viene visualizzato disco hello replicati DataKeeper][sap-ha-guide-figure-3045]

  _**Figura 55:** gestione Cluster di Failover viene disco hello che DataKeeper replicati_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Installare il sistema di SAP NetWeaver hello

È non descrivono il programma di installazione di hello DBMS perché le impostazioni variano a seconda di hello sistema DBMS in uso. Tuttavia, si presuppone che i problemi di disponibilità elevata hello DBMS vengono indirizzati con funzionalità hello diversi fornitori di sistemi DBMS hello il supporto per Azure. ad esempio AlwaysOn o mirroring del database per SQL Server e Oracle Data Guard per database Oracle. Nello scenario di hello che viene usato in questo articolo, ci non sono state aggiunte altre protezione toohello DBMS.

Non esistono particolari considerazioni per il caso in cui servizi DBMS differenti interagiscono con questa configurazione di SAP ASCS/SCS in cluster in Azure.

> [!NOTE]
> procedure di installazione Hello di sistemi SAP NetWeaver ABAP, Java e sistemi ABAP + Java sono quasi identiche. la differenza più significativa di Hello è un sistema SAP ABAP con un'istanza ASCS. Hello sistema Java di SAP include un'istanza SCS. Hello sistema ABAP + Java di SAP include un'istanza ASCS e in esecuzione in un'istanza SCS hello nello stesso gruppo di cluster di failover di Microsoft. Eventuali differenze di installazione per ogni stack di installazione di SAP NetWeaver verranno indicate in modo esplicito. Si può presupporre che tutte le altre parti sono hello stesso.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Installare SAP con un'istanza di ASCS/SCS a disponibilità elevata

> [!IMPORTANT]
> Verificare che i volumi con mirroring di non tooplace in DataKeeper di file della pagina. DataKeeper non supporta i volumi con mirroring. È possibile lasciare il file di pagina nell'unità temporanea hello D di una macchina virtuale di Azure, ovvero impostazione predefinita di hello. Se non è già presente, è possibile spostare hello Windows pagina file toodrive d: di macchina virtuale di Azure.
>
>

L'installazione di SAP con un'istanza di ASCS/SCS a disponibilità elevata prevede queste attività:

- Creazione di un nome host virtuale per l'istanza di SAP ASCS/SCS hello in cluster
- L'installazione di hello SAP primo nodo del cluster
- Modifica profilo SAP hello dell'istanza di hello ASCS/SCS
- Aggiunta di un porta probe
- Aprire la porta probe di hello Windows firewall

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Creare un nome host virtuale per l'istanza di SAP ASCS/SCS hello in cluster

1.  Nella console di gestione DNS di Windows hello, creare una voce DNS per il nome host virtuale hello dell'istanza di hello ASCS/SCS.

  > [!IMPORTANT]
  > Hello indirizzo IP che è assegnato il nome host virtuale toohello di hello ASCS/SCS istanza deve essere hello stesso come indirizzo IP hello assegnato tooAzure bilanciamento del carico (**<*SID*> - lb - ascs **).  
  >
  >

  l'indirizzo IP del nome host di SAP ASCS/SCS virtuale hello Hello (**pr1-sap ascs**) hello stesso come indirizzo IP hello di bilanciamento del carico di Azure (**pr1-lb-ascs**).

  ![Figura 56: Definire voce DNS hello per il nome virtuale del cluster di SAP ASCS/SCS hello e l'indirizzo TCP/IP][sap-ha-guide-figure-3046]

  _**Figura 56:** definire una voce DNS hello per il nome virtuale del cluster di SAP ASCS/SCS hello e l'indirizzo TCP/IP_

2.  toodefine hello nome indirizzo IP assegnato toohello host virtuale, selezionare **gestore DNS** > **dominio**.

  ![Figura 57: Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Figura 57:** Nuovo nome virtuale e indirizzo TCP/IP per la configurazione del cluster di SAP ASCS/SCS_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Installare hello SAP primo nodo del cluster

1.  Eseguire hello primo nodo opzione cluster sul nodo del cluster A. Ad esempio, in hello **pr1-ascs-0** host.
2.  porte predefinite di hello tookeep per hello Azure interno il bilanciamento del carico, selezionare:

  * Per il **sistema ABAP**: **ASCS** numero di istanza **00**
  * Per il **sistema Java**: **SCS** numero di istanza **01**
  * Per il **sistema ABAP + Java**: **ASCS** numero di istanza **00** e **SCS** numero di istanza **01**

  istanza toouse numeri diverso da 00 per hello ABAP ASCS 01 per l'istanza di Java SCS hello e istanza, è necessario innanzitutto toochange hello Azure carico interno del servizio di bilanciamento predefinito di bilanciamento del carico le regole, descritte in [carico predefinito ASCS/SCS hello di modifica bilanciamento del carico delle regole di bilanciamento del carico interno di Azure hello][sap-ha-guide-8.9].

alcune attività successiva Hello non sono descritti nella documentazione di installazione SAP standard hello.

> [!NOTE]
> documentazione di installazione di SAP Hello viene descritto come tooinstall hello primo nodo del cluster ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificare il profilo di SAP hello dell'istanza di hello ASCS/SCS

È necessario tooadd un nuovo parametro del profilo. parametro del profilo Hello impedisce le connessioni tra i processi di lavoro SAP e il server di Accodamento hello di chiusura quando sono inattivi per troppo tempo. Accennato scenario problema hello in [aggiungere le voci del Registro di sistema in entrambi i nodi del cluster dell'istanza di SAP ASCS/SCS hello][sap-ha-guide-8.11]. In questa sezione è stata introdotta anche due modifiche toosome base TCP/IP parametri di connessione. In un secondo passaggio, è necessario tooset hello enqueue server toosend un `keep_alive` indicano in modo che le connessioni di hello non raggiunto una soglia di inattività del hello Azure interna di bilanciamento del carico.

hello toomodify profilo SAP dell'istanza ASCS/SCS hello:

1.  Aggiungere questo toohello di parametro del profilo di istanza di SAP ASCS/SCS di profilo:

  ```
  enque/encni/set_so_keepalive = true
  ```
  In questo esempio, il percorso di hello è:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Ad esempio, profilo di istanza SAP SCS toohello e il percorso corrispondente:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  modifiche hello tooapply, riavviare l'istanza di SAP ASCS /SCS hello.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Aggiungere una porta probe

Utilizzare operazioni di configurazione del hello interna di bilanciamento del carico probe funzionalità toomake hello intero cluster con bilanciamento del carico di Azure. servizio di bilanciamento del carico interno di Azure Hello distribuisce in genere hello in arrivo del carico di lavoro in modo uniforme tra le macchine virtuali partecipante. Questa operazione non funziona tuttavia in alcune configurazioni di cluster perché è attiva una sola istanza. Hello altra istanza è passiva e non può accettare qualsiasi carico di lavoro hello. Una funzionalità di probe è utile quando si assegna bilanciamento di carico interno di Azure hello istanze attive tooan solo di lavoro. Con la funzionalità di probe hello, bilanciamento del carico interno hello può rilevare le istanze che sono attive e quindi puntare solo hello istanza con carico di lavoro hello.

una porta probe tooadd:

1.  Controllare hello corrente **ProbePort** impostazione eseguendo il comando PowerShell seguente hello. Eseguirlo all'interno di una delle macchine virtuali hello nella configurazione del cluster hello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Definire una porta probe. numero di porta probe predefinito Hello è **0**. In questo esempio viene usata la porta probe **62000**.

  ![Figura 58: porta probe configurazione del cluster hello è 0 per impostazione predefinita][sap-ha-guide-figure-3048]

  _**Figura 58:** la porta probe hello predefinita cluster configurazione è 0_

  numero di porta Hello è definito nei modelli di SAP Azure Resource Manager. È possibile assegnare il numero di porta hello in PowerShell.

  un nuovo valore ProbePort per hello tooset  **SAP <*SID*> IP * * risorsa cluster, eseguire lo script di PowerShell seguente hello. Aggiornare le variabili di PowerShell hello per l'ambiente. Dopo l'esecuzione dello script hello, sarà richiesta toorestart hello SAP cluster tooactivate hello modifiche apportate al gruppo.

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

  Dopo aver portato hello  **SAP <*SID*> * * ruolo del cluster, verificare che **ProbePort** è impostato un valore nuovo toohello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Probe porta hello del cluster dopo aver impostato il nuovo valore di hello][sap-ha-guide-figure-3049]

  _**Figura 59:** Probe porta hello del cluster dopo aver impostato il nuovo valore di hello_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Aprire la porta probe di hello Windows firewall

È necessario tooopen una porta di probe di Windows firewall su entrambi i nodi del cluster. Utilizzare i seguenti script tooopen una porta probe del firewall Windows hello. Aggiornare le variabili di PowerShell hello per l'ambiente.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Hello **ProbePort** è troppo**62000**. Ora è possibile accedere a una condivisione di hello  **\\\ascsha-clsap\sapmnt** da altri host, ad esempio di **ascsha DBA**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Installare l'istanza del database hello

database hello tooinstall dell'istanza, seguire il processo di hello descritto nella documentazione di installazione di SAP hello.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Installare secondo nodo del cluster hello

tooinstall hello secondo cluster, eseguire i passaggi nella Guida all'installazione di SAP hello hello.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Modificare il tipo di avvio dell'istanza di servizio SAP Hiamanti Windows hello hello

Modificare il tipo di avvio del servizio SAP Hiamanti Windows hello hello troppo**automatico (avvio ritardato)** in entrambi i nodi del cluster.

![Figura 60: Modificare il tipo di servizio hello per hello SAP Hiamanti istanza toodelayed automatico][sap-ha-guide-figure-3050]

_**Figura 60:** modificare il tipo di servizio hello per hello SAP Hiamanti istanza toodelayed automatico_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Installare hello Server primario di applicazioni SAP

Installare l'istanza primaria applicazione Server (PAS) hello <*SID*> - di - 0 nella macchina virtuale hello specificate toohost hello indirizzi PA. Non sono presenti dipendenze da specifiche impostazioni di Azure o DataKeeper.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Installare ulteriori Server di applicazioni SAP hello

Installare un Server applicazioni aggiuntivi SAP (AAS) in tutte le macchine virtuali hello che è stato designato toohost un'istanza del Server SAP. Ad esempio, in <*SID*> - di - 1 troppo <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Questo completa l'installazione di hello di un sistema SAP NetWeaver a disponibilità elevata. Procedere quindi con il test del failover.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Test di failover di istanza di SAP ASCS/SCS hello e la replica di SIOS
È facile tootest e monitorare un failover di istanza di SAP ASCS/SCS e la replica dei dischi SIOS usando Gestione Cluster di Failover e lo strumento di configurazione e gestione di SIOS DataKeeper hello.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> Istanza di SAP ASCS/SCS in esecuzione nel nodo A del cluster

Hello **PR1 SAP** gruppo di cluster è in esecuzione sul nodo del cluster A. Ad esempio, in **pr1-ascs-0**. Assegnare l'unità disco condivisa hello S, che fa parte di hello **PR1 SAP** gruppo e viene utilizzata l'istanza ASCS/SCS hello, toocluster nodo a cluster

![Figura 61: Gestione Cluster di Failover: gruppo di cluster SAP < SID > hello è in esecuzione in un nodo del cluster][sap-ha-guide-figure-5000]

_**Figura 61:** gestione Cluster di Failover: hello SAP <*SID*> gruppo di cluster è in esecuzione in un nodo del cluster_

In hello SIOS DataKeeper gestione e lo strumento di configurazione, è possibile visualizzare tale disco condiviso hello i dati vengono replicati in modo sincrono da hello volume unità di origine S sul nodo del cluster di un'unità di volume di destinazione S toohello nel nodo B. Ad esempio, viene replicata dal **pr1-ascs-0 [10.0.0.40]** troppo**pr1-ascs-1 [10.0.0.41]**.

![Figura 62: In SIOS DataKeeper, replicare volume locale hello dal nodo del cluster un nodo toocluster B][sap-ha-guide-figure-5001]

_**Figura 62:** In SIOS DataKeeper, replicare volume locale hello dal nodo del cluster un nodo toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover dal nodo toonode B

1.  Scegliere una di queste opzioni tooinitiate un failover di hello SAP <*SID*> gruppo di cluster dal nodo toocluster del nodo cluster b:
  - Usare Gestione cluster di failover  
  - Usare PowerShell per Clustering di failover

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Riavviare un nodo di cluster all'interno del sistema operativo guest di Windows hello (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).  
3.  Riavviare un nodo del cluster da hello portale di Azure (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).  
4.  Riavviare un nodo del cluster tramite Azure PowerShell (si avvia un failover automatico di SAP hello <*SID*> gruppo di cluster dal nodo toonode B).

  Dopo il failover, hello SAP <*SID*> gruppo di cluster è in esecuzione nel nodo B. Ad esempio, è in esecuzione **pr1-ascs-1**.

  ![Figura 63: In Gestione Cluster di Failover, gruppo di cluster SAP < SID > hello è in esecuzione sul nodo del cluster B][sap-ha-guide-figure-5002]

  _**Figura 63**: In Gestione Cluster di Failover, hello SAP <*SID*> gruppo di cluster è in esecuzione sul nodo del cluster B_

  Hello disco condiviso è ora installato nel cluster nodo B. SIOS DataKeeper è la replica dei dati dall'unità di volume di origine S nel cluster del nodo B tootarget volume unità S nel nodo del cluster A. Ad esempio, è la replica da **pr1-ascs-1 [10.0.0.41]** troppo**pr1-ascs-0 [10.0.0.40]**.

  ![Figura 64: SIOS DataKeeper replica volume locale hello dal cluster nodo B toocluster nodo][sap-ha-guide-figure-5003]

  _**Figura 64:** SIOS DataKeeper replica volume locale hello dal nodo del cluster del nodo B toocluster A_
