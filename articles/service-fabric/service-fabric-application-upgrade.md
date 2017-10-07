---
title: aggiornamento dell'applicazione Fabric aaaService | Documenti Microsoft
description: "Questo articolo fornisce un'introduzione tooupgrading un'applicazione di Service Fabric, tra cui scegliere le modalità di aggiornamento e di eseguire controlli di integrità."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Aggiornamento di un'applicazione di infrastruttura di servizi
Un'applicazione di Azure Service Fabric è una raccolta di servizi. Durante un aggiornamento, Service Fabric Confronta hello nuovo [manifesto dell'applicazione](service-fabric-application-model.md#describe-an-application) con la versione precedente di hello e determina quali servizi in un'applicazione hello richiedono gli aggiornamenti. Versione di hello numeri nel servizio hello manifesti con numeri di versione di hello nella versione precedente di hello viene confrontata Service Fabric. Se un servizio non è cambiato, non viene aggiornato.

## <a name="rolling-upgrades-overview"></a>Panoramica degli aggiornamenti in sequenza
In un aggiornamento dell'applicazione in sequenza, l'aggiornamento di hello viene eseguita in fasi. In ogni fase, l'aggiornamento di hello è applicato tooa subset di nodi nel cluster di hello, denominato di un dominio di aggiornamento. Di conseguenza, un'applicazione hello rimane disponibile per tutta l'aggiornamento di hello. Durante l'aggiornamento di hello, cluster hello può contenere una combinazione di versioni nuove e precedenti hello.

Per questo motivo, le versioni di hello due devono essere avanti e indietro compatibile. Se non sono compatibili, l'amministratore dell'applicazione hello è responsabile della gestione temporanea di una disponibilità toomaintain aggiornamento multifase. In un aggiornamento di più fasi, innanzitutto hello aggiornamento tooan versione intermedia dell'applicazione hello compatibile con la versione precedente di hello. secondo passaggio Hello è tooupgrade hello versione finale che interrompe la compatibilità con la versione di hello pre-aggiornamento, ma è compatibile con la versione intermedia hello.

Domini di aggiornamento vengono specificati nel manifesto del cluster hello quando si configura il cluster hello. I domini di aggiornamento non ricevono gli aggiornamenti in un ordine particolare. Un dominio di aggiornamento è un'unità logica di distribuzione per un'applicazione. Domini di aggiornamento consentono hello servizi tooremain la disponibilità elevata durante un aggiornamento.

Gli aggiornamenti in sequenza non sono possibili se l'aggiornamento di hello è applicato tooall i nodi cluster hello, che è il caso di hello quando un'applicazione hello ha solo un dominio di aggiornamento. Questo approccio è sconsigliato, perché il servizio hello diventa inattiva e non è disponibile al momento di hello dell'aggiornamento. Azure, inoltre, non offre alcuna garanzia per i casi in cui un cluster è configurato con un solo dominio di aggiornamento.

## <a name="health-checks-during-upgrades"></a>Controlli di integrità durante gli aggiornamenti
Per un aggiornamento, criteri di integrità impostare toobe oppure possono essere utilizzati i valori predefiniti. Un aggiornamento è denominato esito positivo quando tutti i domini di aggiornamento vengono aggiornati all'interno di hello di timeout specificato, e quando aggiornare tutti i domini sono considerati integro.  Un dominio di aggiornamento integro, significa che tale dominio di aggiornamento hello superato tutti i controlli di integrità di hello specificati nei criteri di integrità hello. Un criterio di integrità, ad esempio, può richiedere che tutti i servizi all'interno di un'istanza dell'applicazione siano *integri*, secondo quanto definito per l'integrità da Service Fabric.

I criteri e i controlli di integrità durante l'aggiornamento da parte dell’infrastruttura di servizi sono indipendenti dai servizi e dalle applicazioni. In altre parole, non vengono eseguiti test specifici per i servizi.  Ad esempio, il servizio potrebbe essere un requisito della velocità effettiva, ma non dispone della velocità effettiva di hello informazioni toocheck Service Fabric. Fare riferimento toohello [articoli integrità](service-fabric-health-introduction.md) per i controlli di hello che vengono eseguiti. controlli di Hello che si verificano durante un test di aggiornamento sono per se il pacchetto di applicazione hello è stato copiato correttamente, se l'istanza di hello è stata avviata e così via.

integrità applicazione Hello è un'aggregazione di entità figlio hello di un'applicazione hello. In breve, Service Fabric valuta l'integrità di hello applicazione hello tramite integrità hello segnalato a un'applicazione hello. Valuta inoltre integrità hello di tutti i servizi di hello per un'applicazione hello in questo modo. Service Fabric ulteriormente valuta l'integrità di hello di servizi dell'applicazione hello aggregando integrità hello dei relativi elementi figlio, ad esempio di replica del servizio hello. Una volta che i criteri di integrità dell'applicazione hello viene soddisfatto, l'aggiornamento di hello può continuare. Se i criteri di integrità hello viene violato, l'aggiornamento dell'applicazione hello ha esito negativo.

## <a name="upgrade-modes"></a>Modalità di aggiornamento
Hello modalità consigliata per l'aggiornamento dell'applicazione è hello monitorato, che rappresenta la modalità hello comunemente utilizzato. Modalità monitorata esegue un aggiornamento hello nel dominio di un aggiornamento, e se i controlli di integrità di tutti i passata (per ogni criterio di hello specificato), sposta nel dominio di aggiornamento successivo toohello automaticamente.  Se i controlli di integrità non riescono e/o vengono raggiunti i timeout, l'aggiornamento di hello di rollback per il dominio di aggiornamento hello o modalità hello è toounmonitored modificate manuale. È possibile configurare i toochoose aggiornamento hello una di queste due modalità per gli aggiornamenti non riusciti. 

Non monitorato in modalità manuale è necessario un intervento manuale dopo ogni aggiornamento in un dominio di aggiornamento, tookick disattivare l'aggiornamento di hello in hello dominio di aggiornamento successivo. Non viene eseguito alcun controllo di integrità su Service Fabric. messaggio per l'amministratore esegue controlli di integrità o lo stato di hello prima di avviare l'aggiornamento di hello in hello dominio di aggiornamento successivo.

## <a name="upgrade-default-services"></a>Aggiornare i servizi predefiniti
Servizi predefiniti all'interno dell'applicazione di Service Fabric possono essere aggiornati durante il processo di aggiornamento di un'applicazione hello. Servizi predefiniti definiti in hello [manifesto dell'applicazione](service-fabric-application-model.md#describe-an-application). Hello regole standard di aggiornamento dei servizi predefiniti sono:

1. Servizi in hello nuovo predefiniti [manifesto dell'applicazione](service-fabric-application-model.md#describe-an-application) che non sono presenti nel cluster hello vengono creati.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) esigenze toobe impostare hello tooenable tootrue alle regole. Questa funzionalità è supportata dalla versione 5.5.

2. I servizi predefiniti che esistono sia nel [manifesto dell'applicazione](service-fabric-application-model.md#describe-an-application) precedente sia nella nuova versione vengono aggiornati. Le descrizioni del servizio nella nuova versione di hello sovrascriverebbe quelli già presente nel cluster hello. L'aggiornamento di un'applicazione subisce automaticamente il rollback in caso di errore dell'aggiornamento del servizio predefinito.
3. Servizi in hello precedente predefiniti [manifesto dell'applicazione](service-fabric-application-model.md#describe-an-application) ma non nella nuova versione di hello vengono eliminati. **Si noti che questa eliminazione dei servizi predefiniti non è reversibile.**

In caso di un'applicazione l'aggiornamento viene eseguito il rollback, servizi predefiniti sono stato ripristinato toohello prima di avviata l'aggiornamento. I servizi eliminati non possono in alcun caso essere creati.

## <a name="application-upgrade-flowchart"></a>Diagramma di flusso di aggiornamento di un'applicazione
diagramma di flusso Hello dopo il paragrafo consentono di comprendere hello processo di aggiornamento di un'applicazione di Service Fabric. In particolare, viene descritto il flusso di hello hello come valori di timeout, tra cui *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, e *UpgradeHealthCheckInterval*, consentono di controllare quando l'aggiornamento di hello nel dominio di un aggiornamento viene considerato un esito positivo o un errore.

![processo di aggiornamento Hello per un'applicazione di Service Fabric][image]

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
