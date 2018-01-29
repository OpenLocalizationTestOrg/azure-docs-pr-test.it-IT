---
title: "Piani e fatturazione nell'utilità di pianificazione di Azure"
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
ms.openlocfilehash: f0662230c5d1663e37ee2be58f234934ec3d55dd
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Piani e fatturazione nell'utilità di pianificazione di Azure
## <a name="job-collection-plans"></a>Piani di raccolta di processi
Raccolte di processi sono entità fatturabili nell'utilità di pianificazione di Azure. Raccolte di processi contengono un numero di processi e sono disponibili in tre combinazioni – Free, Standard e Premium: descritti di seguito.

| **Piano di raccolta di processi** | **Numero massimo di processi per ogni raccolta di processi** | **Max ricorrenza** | **Raccolte di processi Max per ogni sottoscrizione** | **Limiti** |
|:--- |:--- |:--- |:--- |:--- |
| **Free** |5 processi per la raccolta attività |Una volta ogni ora. Impossibile eseguire i processi più spesso di una volta all'ora |A una sottoscrizione è consentita 1 sola raccolta processi gratuita |Non è possibile utilizzare [oggetto autorizzazione in uscita HTTP](scheduler-outbound-authentication.md) |
| **Standard** |50 processi per la raccolta attività |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |A una sottoscrizione è consentito un massimo di 100 raccolte di processi standard |Accesso al set completo di funzionalità dell'utilità di pianificazione |
| **P10 Premium** |50 processi per la raccolta attività |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |A una sottoscrizione sono consentite fino a 10.000 raccolte di processi P10 Premium. <a href="mailto:wapteams@microsoft.com">Contattaci</a> per ulteriori informazioni. |Accesso al set completo di funzionalità dell'utilità di pianificazione |
| **P20 Premium** |1000 processi per ogni raccolta processi |Una volta al minuto. Impossibile eseguire i processi più spesso di una volta all'ora |A una sottoscrizione sono consentite fino a 10.000 raccolte di processi P20 Premium. <a href="mailto:wapteams@microsoft.com">Contattaci</a> per ulteriori informazioni. |Accesso al set completo di funzionalità dell'utilità di pianificazione |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Effettua il downgrade dei piani di raccolta di processi e gli aggiornamenti
È possibile aggiornare o effettuare il downgrade di un processo piano di raccolta in qualsiasi momento tra i piani Free, Standard e Premium. Tuttavia, quando il downgrade a una raccolta di processi gratuita, il declassamento potrebbe non riuscire per uno dei seguenti motivi:

* Esiste già una raccolta processi gratuita nella sottoscrizione
* Un processo nella raccolta con una frequenza superiore a quello consentito per i processi in raccolte di processi gratuita. È la ricorrenza massima consentita in una raccolta di processi gratuita una volta ogni ora
* Sono presenti più di 5 processi nella raccolta di processi
* Un processo nella raccolta di processi con un'azione HTTP o HTTPS che utilizza un [oggetto autorizzazione in uscita HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Piani di fatturazione e Azure
Alle sottoscrizioni non vengono addebitate le raccolte di processi gratuite. Se si dispone di più di 100 raccolte di processi standard (10 unità fatturazione standard), è un ottimo affare affinché tutte le raccolte di processi nel piano premium.

Se si dispone di una raccolta di processi standard e di una raccolta di processi premium, verranno fatturate un'unità di fatturazione standard *e* un'unità di fatturazione premium. Gli effetti del servizio Utilità di pianificazione in base al numero di raccolte di processi attivi impostati su standard o premium; questo viene illustrato più dettagliatamente in due sezioni successive.

## <a name="standard-billable-units"></a>Unità fatturabili standard
Un'unità fatturabile standard può includere fino a 10 raccolte di processi standard. Poiché una raccolta processi standard può avere al massimo 50 processi per raccolta, un'unità di fatturazione standard consente che una sottoscrizione abbia fino a 500 processi: fino a quasi 22 milioni di esecuzioni di processi al mese.

Se si trovano tra 1 e 10 raccolte di processi standard, verrà addebitata per 1 unità standard di fatturazione. Se si trovano tra 11 e 20 raccolte di processi standard, verranno addebitate 2 unità standard di fatturazione. Se si trovano tra 21 e 30 raccolte di processi standard, verranno addebitate 3 unità standard di fatturazione.

## <a name="p10-premium-billable-units"></a>Unità fatturabili P10 Premium
Un'unità fatturabile P10 Premium può includere fino a 10.000 raccolte processi P10 Premium. Poiché una raccolta processi P10 Premium può avere un massimo di 50 processi per raccolta, un'unità di fatturazione Premium consente che una sottoscrizione abbia un massimo di 500.000 processi, fino a quasi 22 miliardi di esecuzioni di processi al mese.

Se il numero di raccolte processi Premium è compreso tra 1 e 10.000 , verrà addebitata 1 unità fatturazione P10 Premium. Se il numero di raccolte processi Premium è compreso tra 10,001 e 20,000, verranno addebitate 2 unità fatturazione P10 Premium e così via.

Le raccolte processi P10 Premium hanno la stessa funzionalità delle raccolte processi Standard ma offrono una riduzione di prezzo nel caso in cui l'applicazione richieda una notevole quantità di raccolte processi.

## <a name="p20-premium-billable-units"></a>Unità fatturabili P20 Premium
Un'unità fatturabile P20 Premium può includere fino a 5.000 raccolte processi P20 Premium. Poiché una raccolta processi P20 Premium può avere un massimo di 1.000 processi per raccolta, un'unità di fatturazione Premium consente che una sottoscrizione abbia un massimo di 5.000.000 di processi, fino a quasi 220 miliardi esecuzioni di processi al mese.

Le raccolte di processi P20 Premium forniscono le stesse funzionalità delle raccolte di processi P10 Premium ma supportano anche un maggiore numero processi per ogni raccolta e un numero totale di processi maggiore rispetto alla raccolta P10 Premium assicurando maggiore scalabilità.

## <a name="billing-and-active-status"></a>Stato attivo e fatturazione
Le raccolte di processi sono sempre attive, a meno che l'intera sottoscrizione entri in uno stato di disabilitazione temporanea a causa di problemi di fatturazione. L'unico modo per assicurarsi che una raccolta di processi non venga addebitata è di impostarla sul piano *gratuito* o di eliminarla.

Anche se è possibile disabilitare tutti i processi all'interno di una raccolta di processi in un'unica operazione, ciò non modifica lo stato di fatturazione della raccolta processi, che pertanto verrà *ancora* fatturata. Analogamente, raccolte di processi vuoto vengono considerati attivi e verranno fatturati.

## <a name="pricing"></a>Prezzi
Per informazioni sui prezzi, vedere [Utilità di pianificazione prezzi](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'Utilità di pianificazione di Azure nel portale di Azure](scheduler-get-started-portal.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

