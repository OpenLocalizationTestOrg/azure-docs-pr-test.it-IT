---
title: aaaManage insieme credenziali chiavi Azure utilizzando l'automazione di Azure | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage insieme credenziali chiavi Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Gestione dell'insieme di credenziali chiave usando Automazione di Azure
Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione delle chiavi e segreti nell'insieme di credenziali chiave di Azure.

## <a name="what-is-azure-automation"></a>Informazioni su Automazione di Azure
[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi e la configurazione preferita per lo stato. Attività manuali ripetute, con esecuzione prolungata e soggetta a errori utilizzando l'automazione di Azure, può essere automatizzata tooincrease affidabilità, efficienza e toovalue tempo per l'organizzazione.

Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze. In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.

Liberare e ridurre i costi operativi IT e DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>In che modo è possibile gestire l'insieme di credenziali chiave di Azure con Automazione di Azure?
Insieme di credenziali chiave possono essere gestiti in automazione di Azure con hello [i cmdlet di Azure Resource Manager insieme di credenziali chiave](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [i cmdlet di Azure classico insieme di credenziali di chiave](https://msdn.microsoft.com/library/azure/dn868052.aspx). Hello modulo Azure per gestire l'insieme di credenziali chiave classico è disponibile automaticamente in automazione di Azure ed è possibile importare hello [modulo di Azure Resource Manager KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in automazione di Azure, in modo che è possibile eseguire molte della gestione dell'insieme di credenziali chiave attività all'interno del servizio hello. È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.

I cmdlet di hello insieme credenziali chiavi Azure è possibile eseguire queste attività tra gli altri: 

* Creare e configurare un insieme di credenziali delle chiavi
* Creare o importare una chiave
* Creare o aggiornare un segreto
* Aggiornare gli attributi di una chiave
* Ottenere una chiave o un segreto
* Eliminare una chiave o un segreto

Ecco alcuni esempi di utilizzo di PowerShell toomanage insieme di credenziali chiave:  

* [Insieme di credenziali delle chiavi di Azure - Procedura dettagliata](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Installazione e configurazione di un insieme di credenziali delle chiavi di Azure](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage insieme di credenziali chiave di Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.

* Vedere hello automazione di Azure [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md).
* Vedere hello [insieme di credenziali chiave di Azure PowerShell script](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

