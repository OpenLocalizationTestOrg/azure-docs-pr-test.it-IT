---
title: Gestire le macchine virtuali con Automazione di Azure | Microsoft Docs
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire le macchine virtuali di Azure su vasta scala."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a>Gestione delle Macchine virtuali di Azure mediante Automazione di Azure
Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione delle macchine virtuali di Azure.

## <a name="what-is-azure-automation"></a>Informazioni su Automazione di Azure
[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi. Usando Automazione di Azure, è possibile automatizzare attività a esecuzione prolungata, manuali, soggette a errori e ripetute frequentemente per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione.

Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali in base alla crescita dell'organizzazione. In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.

È possibile ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie all'esecuzione automatica delle attività di gestione del cloud con Automazione di Azure.

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a>Come può Automazione di Azure aiutare nella gestione delle macchine virtuali di Azure?
Le macchine virtuali possono essere gestite in Automazione di Azure tramite [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Automazione di Azure include i cmdlet di Azure PowerShell per consentire l'esecuzione di tutte le attività di gestione delle macchine virtuali dall'interno del servizio. È anche possibile abbinare i cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.

## <a name="next-steps"></a>Passaggi successivi
A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e del modo in cui può essere usato per gestire le macchine virtuali di Azure, usare i collegamenti seguenti per altre informazioni:

* [Panoramica di Automazione di Azure](../../automation/automation-intro.md)
* [Il primo runbook](../../automation/automation-first-runbook-graphical.md)
* [Mappa di apprendimento di Automazione di Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)

