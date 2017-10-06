---
title: "aaaPlans e fatturazione in utilità di pianificazione di Azure"
description: "Piani e fatturazione nell'utilità di pianificazione di Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Piani e fatturazione nell'utilità di pianificazione di Azure
## <a name="job-collection-plans"></a>Piani di raccolta di processi
Raccolte di processi sono entità fatturabili di hello nell'utilità di pianificazione di Azure. Raccolte di processi contengono un numero di processi e sono disponibili in tre combinazioni – Free, Standard e Premium: descritti di seguito.

| **Piano di raccolta di processi** | **Numero massimo di processi per ogni raccolta di processi** | **Max ricorrenza** | **Raccolte di processi Max per ogni sottoscrizione** | **Limiti** |
|:--- |:--- |:--- |:--- |:--- |
| **Free** |5 processi per la raccolta attività |Una volta ogni ora. Impossibile eseguire i processi più spesso di una volta all'ora |È consentita una sottoscrizione di una raccolta di processi gratuita too1 |Non è possibile utilizzare [oggetto autorizzazione in uscita HTTP](scheduler-outbound-authentication.md) |
| **Standard** |50 processi per la raccolta attività |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |Una sottoscrizione è consentita di raccolte processi standard too100 |Set di funzionalità di accesso toofull di utilità di pianificazione |
| **P10 Premium** |50 processi per la raccolta attività |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |Una sottoscrizione è consentita di too10, raccolte di processi Premium P10 000. <a href="mailto:wapteams@microsoft.com">Contattaci</a> per ulteriori informazioni. |Set di funzionalità di accesso toofull di utilità di pianificazione |
| **P20 Premium** |1000 processi per ogni raccolta processi |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |Una sottoscrizione è consentita di too10, raccolte di processi Premium P20 000. <a href="mailto:wapteams@microsoft.com">Contattaci</a> per ulteriori informazioni. |Set di funzionalità di accesso toofull di utilità di pianificazione |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Effettua il downgrade dei piani di raccolta di processi e gli aggiornamenti
È possibile aggiornare o effettuare il downgrade di un processo piano di raccolta in qualsiasi momento tra i piani gratuito, Standard e Premium hello. Tuttavia, quando la raccolta di processi gratuita tooa il downgrade, downgrade hello potrebbe non riuscire per uno dei seguenti motivi hello:

* Esiste già una raccolta di processi gratuita nella sottoscrizione hello
* Un processo nella raccolta di processi hello ha una ricorrenza superiore a quello consentito per i processi in raccolte di processi gratuita. è consentita in una raccolta di processi gratuita la ricorrenza massima Hello una volta ogni ora
* Sono presenti più di 5 processi nella raccolta di processi hello
* Un processo nella raccolta di processi hello è un'azione HTTP o HTTPS che utilizza un [oggetto di autorizzazione in uscita HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Piani di fatturazione e Azure
Alle sottoscrizioni non vengono addebitate le raccolte di processi gratuite. Se si dispone di più di 100 raccolte processi standard (10 fatturazione unità standard), viene utilizzato un migliore toohave gestiscono tutte le raccolte di processi nel piano premium hello.

Se si dispone di una raccolta di processi standard e di una raccolta di processi premium, verranno fatturate un'unità di fatturazione standard *e* un'unità di fatturazione premium. Hello distinte di servizio dell'utilità di pianificazione in base al numero di hello di raccolte di processi attivi impostati tooeither standard o premium; Questa configurazione viene spiegata in maggiore dettaglio nel hello nelle due sezioni successive.

## <a name="standard-billable-units"></a>Unità fatturabili standard
Un'unità fatturabile standard può includere le raccolte processi standard too10. Poiché una raccolta di processi standard può avere too50 processi per ogni raccolta di processi, un'unità di fatturazione standard consente un toohave sottoscrizione too500 operazioni di backup: backup tooalmost 22 milioni di esecuzioni di processi al mese.

Se si trovano tra 1 e 10 raccolte di processi standard, verrà addebitata per 1 unità standard di fatturazione. Se si trovano tra 11 e 20 raccolte di processi standard, verranno addebitate 2 unità standard di fatturazione. Se si trovano tra 21 e 30 raccolte di processi standard, verranno addebitate 3 unità standard di fatturazione.

## <a name="p10-premium-billable-units"></a>Unità fatturabili P10 Premium
Un'unità di fatturabili premium P10 può includere backup too10, raccolte di processi premium P10 000. Poiché una raccolta di processi premium P10 può avere too50 processi per ogni raccolta di processi, un'unità di fatturazione premium consente toohave una sottoscrizione di too500, i processi 000: backup tooalmost miliardi 22 esecuzioni del processo al mese.

Se il numero di raccolte processi Premium è compreso tra 1 e 10.000 , verrà addebitata 1 unità fatturazione P10 Premium. Se il numero di raccolte processi Premium è compreso tra 10,001 e 20,000, verranno addebitate 2 unità fatturazione P10 Premium e così via.

Di conseguenza, processo premium P10 raccolte presentano hello stessa funzionalità come le raccolte di processi standard di hello ma consentono un'interruzione di prezzo nel caso in cui l'applicazione richiede una quantità elevata di raccolte di processi.

## <a name="p20-premium-billable-units"></a>Unità fatturabili P20 Premium
Un'unità di fatturabili premium P20 può includere backup too5, raccolte di processi premium P20 000. Poiché una raccolta di processi premium P20 può esistere fino a too1, 000 processi per ogni raccolta di processi, un'unità di fatturazione premium consente un toohave sottoscrizione backup too5 000, processi 000: backup tooalmost miliardi 220 esecuzioni del processo al mese.

Raccolte di processi premium P20 fornisce hello stesse funzionalità di raccolte di processi premium P10 ma supporta anche un numero maggiore i processi per ogni raccolta di processi e un maggior numero totale dei processi complessivi di P10 premium consentendo si toohave maggiore scalabilità.

## <a name="billing-and-active-status"></a>Stato attivo e fatturazione
Raccolte di processi sono sempre attive a meno che non rientra in uno stato temporaneo disabilitato a causa di problemi di toobilling l'intera sottoscrizione. Hello solo tooensure di modo che una raccolta di processi non viene addebitata è tooeither impostarlo toohello *libero* piano o toodelete raccolta di processi hello.

Anche se è possibile disabilitare tutti i processi all'interno di una raccolta di processi in un'unica operazione, non modifica lo stato di fatturazione hello della raccolta di processi hello: raccolta di processi hello verrà *ancora* fatturato. Analogamente, raccolte di processi vuoto vengono considerati attivi e verranno fatturati.

## <a name="pricing"></a>Prezzi
Per informazioni sui prezzi, vedere [Utilità di pianificazione prezzi](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

