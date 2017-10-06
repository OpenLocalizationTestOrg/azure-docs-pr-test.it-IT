---
title: "aaaScheduler ad alta disponibilità e affidabilità"
description: "Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione
## <a name="azure-scheduler-high-availability"></a>Livelli elevati di disponibilità dell'Utilità di pianificazione
In quanto servizio core della piattaforma Azure, l’Utilità di pianificazione di Azure ha un’elevata disponibilità e funzionalità di distribuzione del servizio con ridondanza geografica e replica geografica internazionale del processo.

### <a name="geo-redundant-service-deployment"></a>Distribuzione del servizio con ridondanza geografica
Pianificazione di Azure è disponibile tramite hello dell'interfaccia utente in quasi tutte le aree geografiche che sono attualmente in Azure. l'elenco di aree dell'utilità di pianificazione di Azure è disponibile in Hello è [elencati di seguito](https://azure.microsoft.com/regions/#services). Se un data center in un'area ospitata non risulta più disponibile, la funzionalità di failover hello dell'utilità di pianificazione di Azure è tali da servizio hello è disponibile da un altro data center.

### <a name="geo-regional-job-replication"></a>Replica geografica internazionale dei processi
Non solo è hello dell'utilità di pianificazione disponibili per le richieste di gestione, mentre un processo viene anche replicato geograficamente front-end. Quando è presente un'interruzione in un'unica area, utilità di pianificazione di Azure viene eseguito il failover e assicura che il processo di hello viene eseguito da un altro data center nell'area geografica associata hello.

Ad esempio, se è stato creato un processo negli USA centro-meridionali, l’Utilità di pianificazione di Azure replica automaticamente tale processo negli USA centro-settentrionale. Quando si verifica un errore nel centro-meridionali, utilità di pianificazione di Azure garantisce che il processo di hello viene eseguito da North Central US. 

![][1]

Di conseguenza, dell'utilità di pianificazione assicura che i dati rimangono all'interno di hello stessa area geografica generale in caso di errore di Azure. Di conseguenza, non è necessario duplicare il processo tooadd solo la disponibilità elevata: utilità di pianificazione di Azure fornisce automaticamente funzionalità a disponibilità elevata per i processi.

## <a name="azure-scheduler-reliability"></a>Affidabilità dell'Utilità di pianificazione di Azure
Pianificazione di Azure garantisce la propria disponibilità elevata e adotta un approccio diverso i processi creati toouser. Ad esempio, il processo può richiamare un endpoint HTTP che non è disponibile. Pianificazione di Azure tenta comunque tooexecute al processo correttamente, offrendo opzioni alternative toodeal con un errore. L’Utilità di pianificazione di Azure fa ciò in due modi:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Criteri di tentativi ripetuti configurabili tramite "retryPolicy"
Pianificazione di Azure consente tooconfigure un criterio di ripetizione. Per impostazione predefinita, se un processo non riesce, utilità di pianificazione prova processo hello nuovamente quattro volte, a intervalli di 30 secondi. È possibile configurare di nuovo questo tentativo criteri toobe più aggressiva (ad esempio dieci volte a intervalli di 30 secondi) o più blando (ad esempio, due volte, a intervalli giornalieri.)

Come esempio di quando ciò può essere utile, è possibile creare un processo che viene eseguito una volta alla settimana e richiama un endpoint HTTP. Se l'endpoint HTTP hello è inattivo per alcune ore quando viene eseguito il processo, è possibile evitare toowait una settimana ulteriori per hello processo toorun nuovamente poiché anche criteri di ripetizione predefiniti hello avrà esito negativo. In tali casi, è possibile riconfigurare hello nuovi tentativi standard criteri tooretry ogni tre ore, ad esempio, anziché ogni 30 secondi.

toolearn come tooconfigure un criterio di ripetizione, vedere troppo[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Configurabilità endpoint alternativo tramite "errorAction"
Se l'endpoint di destinazione hello per il processo dell'utilità di pianificazione di Azure rimane non raggiungibile, utilità di pianificazione di Azure esegue il fallback endpoint di gestione degli errori alternativo toohello dopo aver seguito i criteri di ripetizione. Se è configurato un endpoint alternativo per la gestione degli errori, l’Utilità di pianificazione Azure lo richiama. Con un endpoint alternativo, i propri processi sono a disponibilità elevata in faccia hello dell'errore.

Ad esempio, nel seguente diagramma di hello dell'utilità di pianificazione di Azure segue relativi toohit di criteri di ripetizione un servizio web di New York. Dopo hello tentativi hanno esito negativo, verifica la presenza di un'alternativa. Quindi prosegue e inizierà a inviare richieste toohello alternativi con hello stessi criteri di ripetizione.

![][2]

Si noti che hello stessi criteri di ripetizione si applicano l'azione originale di tooboth hello e hello errore alternativo. Tipo di azione anche possibile toohave hello azione di errore alternativa può essere diverso dal tipo dell'azione principale hello. Ad esempio, mentre l'azione principale hello può richiamare un endpoint HTTP, azione di errore hello potrebbe invece essere una coda di archiviazione, una coda di service bus o azione argomento del bus di servizio che esegue la registrazione degli errori.

toolearn come tooconfigure un endpoint alternativo, fare riferimento troppo[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure](scheduler-advanced-complexity.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
