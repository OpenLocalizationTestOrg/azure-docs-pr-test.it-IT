---
title: aaaUsing SAP nelle macchine virtuali Windows | Documenti Microsoft
description: Informazioni sull'uso di SAP in macchine virtuali (VM) Windows in Microsoft Azure
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Uso di SAP su macchine virtuali Windows in Azure
Il cloud Computing è un termine ampiamente diffuso importanza sempre maggiore di hello settore IT, dalle piccole imprese di società toolarge e implementazione. Microsoft Azure è una piattaforma di servizi Cloud Microsoft che offre un'ampia gamma di nuove possibilità hello. I clienti sono ora toorapidly in grado di effettuare il provisioning e la prestazione applicazioni come servizi Cloud, in modo che non siano tootechnical limitato o restrizioni budget. Invece di investire tempo e denaro nell'infrastruttura hardware, le organizzazioni possono dedicarsi applicazione hello, i processi di business e i vantaggi per clienti e utenti.

Grazie alle macchine virtuali Microsoft Azure, Microsoft offre una piattaforma IaaS (Infrastructure as a Service, infrastruttura distribuita come servizio) completa. Le applicazioni basate su SAP NetWeaver sono supportate in Macchine virtuali di Azure (IaaS). white paper Hello riportato di seguito viene descritto come tooplan e implementare SAP NetWeaver su applicazioni basate su macchine virtuali Windows in Azure. È anche possibile implementare applicazioni basate su SAP NetWeaver in [Macchine virtuali Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver in Azure - Disponibilità elevata
titolo: aaaSAP NetWeaver in Azure - Clustering SAP ASCS/SCS istanze con i Cluster di Failover di Windows Server in Azure con SIOS DataKeeper

Riepilogo: ' in questo documento descrive come toouse SIOS DataKeeper tooset per una configurazione a disponibilità elevata di SAP ASCS/SCS in Azure. SAP protegge i componenti con singolo punto di errore, ad esempio SAP ASCS/SCS o Enqueue Replication Services tramite configurazioni cluster di failover di Windows Server che richiedono dischi condivisi. Questi componenti SAP sono essenziali per la funzionalità di hello di un sistema SAP. Necessità di funzionalità a disponibilità elevata toobe inserire in inserire pertanto toomake assicurarsi che tali componenti in grado di sostenere un errore di un server o una macchina virtuale come avviene con le configurazioni di Cluster di Windows per ambienti Hyper-V e bare metal. A partire da agosto 2015 Azure su se stesso non può fornire i dischi condivisi necessari per Windows hello in base a disponibilità elevata configurazioni richieste per questi componenti SAP critici. Tuttavia con l'aiuto di hello del prodotto hello DataKeeper di SIOS, è possono creare configurazioni di Cluster di Failover di Windows Server in base alle esigenze per SAP ASCS/SCS sulla piattaforma IaaS di Azure hello. Questo documento descrive un approccio passo per passo come tooinstall una configurazione di Windows Server Failover Clustering con disco condiviso fornito da SIOS Datakeeper in Azure. documento di Hello illustrerà i dettagli delle configurazioni sul lato Azure, Windows e SAP hello che configurazione a disponibilità elevata hello funziona in modo ottimale. Hello carta integra hello documentazione di installazione di SAP e note su SAP che rappresentano le risorse primarie hello per le distribuzioni del software SAP e le installazioni dato piattaforme.

Ultimo aggiornamento: agosto 2015

[Scaricare la guida](http://go.microsoft.com/fwlink/?LinkId=613056)

