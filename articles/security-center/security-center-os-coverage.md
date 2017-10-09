---
title: piattaforme aaaSupported nel Centro protezione di Azure | Documenti Microsoft
description: Questo documento offre un elenco di sistemi operativi Windows e Linux supportati nel Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Piattaforme supportate nel Centro sicurezza di Azure
Monitoraggio dello stato di sicurezza e le indicazioni sono disponibili per le macchine virtuali (VM) create utilizzando hello classic sia modelli di distribuzione di gestione risorse.

> [!NOTE]
> Altre informazioni su hello [classica e modelli di distribuzione di gestione risorse](../azure-classic-rm.md) per le risorse di Azure.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Piattaforme supportate per le macchine virtuali Windows
Sistemi operativi Windows supportati:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Le valutazioni delle vulnerabilità del sistema operativo non sono ancora disponibili per Windows Server 2016.
* Il rilevamento dell'analisi di arresto anomalo è supportato solo per Windows Server 2012 e Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Piattaforme supportate per le macchine virtuali Linux
Sistemi operativi Linux supportati:

* Versioni di Ubuntu 12.04, 14.04, 16.04, 16.10
* Versioni di Debian 7, 8
* Versioni di CentOS 6.\*, 7.*
* Versioni di Red Hat Enterprise Linux (RHEL) 6.\*, 7.*
* Versioni di SUSE Linux Enterprise Server (SLES) 11 SP4+, 12.*
* Versioni di Oracle Linux 6.\*, 7.*

> [!NOTE]
> L'analisi comportamentali della macchina virtuale non è ancora disponibile per i sistemi operativi Linux.
>
>

## <a name="vms-and-cloud-services"></a>Macchine virtuali e servizi cloud
Sono supportate anche macchine virtuali in esecuzione in un servizio cloud. Vengono monitorati solo i ruoli Web e di lavoro dei servizi cloud in esecuzione negli slot di produzione. toolearn più sul servizio cloud, vedere [Cenni preliminari sui servizi Cloud](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Passaggi successivi

- [Centro sicurezza di Azure Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md) , informazioni come tooplan e comprendere considerazioni sulla progettazione hello tooadopt Centro sicurezza di Azure
- [Avvisi di sicurezza per tipo nel Centro sicurezza di Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis): altre informazioni sull'analisi comportamentale della macchina virtuale e sull'analisi della memoria dump di arresto anomalo del sistema nel Centro sicurezza
- [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca
- [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure
