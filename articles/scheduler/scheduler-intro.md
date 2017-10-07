---
title: "aaaWhat è utilità di pianificazione di Azure? | Microsoft Docs"
description: Pianificazione di Azure consente toodeclaratively descrivono toorun azioni nel cloud hello. e quindi pianifica ed esegue tali azioni automaticamente.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Che cos'è l'Utilità di pianificazione di Azure?
Pianificazione di Azure consente toodeclaratively descrivono toorun azioni nel cloud hello. e quindi pianifica ed esegue tali azioni automaticamente.  Utilità di pianificazione avviene usando [hello Azure portal](scheduler-get-started-portal.md), codice, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), o Azure PowerShell.

L’Utilità di pianificazione crea, gestisce e richiama il lavoro programmato.  L’Utilità di pianificazione non ospita carichi di lavoro, né esegue codice. *Richiama* soltanto codice ospitato altrove, ad esempio in Azure, in locale o presso un altro provider. Richiama tramite HTTP, HTTPS, una coda di archiviazione, una coda del bus di servizio o un argomento del bus di servizio.

Le pianificazioni dell'utilità di pianificazione [processi](scheduler-concepts-terms.md), mantiene una cronologia dei risultati di esecuzione processo che uno è possibile esaminare e in modo deterministico e affidabile le pianificazioni dei carichi di lavoro toobe eseguire. Processi Web di Azure (parte della funzionalità di App Web hello in Azure App Service) e altre funzionalità di pianificazione di Azure è possibile utilizzare utilità di pianificazione in background hello. Hello [API REST dell'utilità di pianificazione](https://msdn.microsoft.com/library/mt629143.aspx) consente di gestiscono le comunicazioni hello per le azioni. Quindi, l’Utilità di pianificazione supporta facilmente [pianificazioni complesse e operazioni ricorrenti avanzate](scheduler-advanced-complexity.md) .

Esistono diversi scenari che si prestano toohello utilizzo dell'utilità di pianificazione. ad esempio:

* *Azioni ricorrenti delle applicazioni*: raccolta periodica di dati da Twitter in un feed.
* *Manutenzione quotidiana*: eliminazione giornaliera dei registri, esecuzione di backup e altre attività di manutenzione. Ad esempio, un amministratore può scegliere tooback backup database hello alle ore 01:00 ogni giorno per hello nove mesi successivi.

Utilità di pianificazione consente toocreate, aggiornare, eliminare, visualizzare e gestire i processi e [le raccolte di processi](scheduler-concepts-terms.md) a livello di programmazione, utilizzando gli script e nel portale di hello.

## <a name="see-also"></a>Vedere anche
 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure](scheduler-advanced-complexity.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

