---
title: aaaTroubleshoot l'installazione del cluster di Service Fabric locale | Documenti Microsoft
description: In questo articolo viene illustrata una serie di suggerimenti per la risoluzione dei problemi del cluster di sviluppo locale
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Risolvere i problemi di configurazione del cluster di sviluppo locale
Se verifica un problema durante l'interazione con il cluster di sviluppo di Azure Service Fabric locale, esaminare hello seguenti suggerimenti per le soluzioni possibili.

## <a name="cluster-setup-failures"></a>Errori di configurazione del cluster
### <a name="cannot-clean-up-service-fabric-logs"></a>Impossibile pulire i log di Infrastruttura di servizi
#### <a name="problem"></a>Problema
Durante l'esecuzione di script DevClusterSetup hello, viene visualizzato un errore simile al seguente:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Soluzione
Finestra di PowerShell corrente hello, chiudere e aprire una nuova finestra di PowerShell come amministratore. Dovrebbe ora essere toosuccessfully in grado di eseguire script hello.

## <a name="cluster-connection-failures"></a>Errori di connessione del cluster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Cmdlet di PowerShell di Service Fabric non sono riconosciute in Azure PowerShell
#### <a name="problem"></a>Problema
Se si tenta toorun qualsiasi hello cmdlet PowerShell di Service Fabric, ad esempio `Connect-ServiceFabricCluster` in una finestra di PowerShell di Azure, ha esito negativo, indicante che tale cmdlet hello non è riconosciuto. motivo Hello è che Azure PowerShell utilizza versione a 32 bit hello di Windows PowerShell (anche in versioni del sistema operativo a 64 bit), mentre i cmdlet di Service Fabric hello funzionano solo in ambienti a 64 bit.

#### <a name="solution"></a>Soluzione
Eseguire sempre i cmdlet di Service Fabric direttamente da Windows PowerShell.

> [!NOTE]
> più recente di Azure PowerShell Hello non viene creato un collegamento speciale, pertanto questa situazione non dovrebbe verificarsi.
> 
> 

### <a name="type-initialization-exception"></a>Eccezione di inizializzazione del tipo
#### <a name="problem"></a>Problema
Quando ci si connette toohello cluster in PowerShell, viene visualizzato l'errore hello TypeInitializationException per System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Soluzione
La variabile di percorso non è stata impostata correttamente durante l'installazione. Disconnettersi da Windows e accedere nuovamente. Il percorso risulterà aggiornato.

### <a name="cluster-connection-fails-with-object-is-closed"></a>La connessione del cluster ha esito negativo con il messaggio "L’oggetto è chiuso"
#### <a name="problem"></a>Problema
Una chiamata tooConnect-ServiceFabricCluster genera un errore simile al seguente:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Soluzione
Finestra di PowerShell corrente hello, chiudere e aprire una nuova finestra di PowerShell come amministratore. A questo punto dovrebbe essere in grado di connettersi toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Eccezione di connessione a Fabric negata
#### <a name="problem"></a>Problema
Durante il debug da Visual Studio, si verifica un errore FabricConnectionDeniedException.

#### <a name="solution"></a>Soluzione
In genere questo errore si verifica quando si tenta un processo host del servizio toostart manualmente, anziché consentire hello Service Fabric runtime toostart per.

Assicurarsi di non disporre di progetti di servizio impostati come progetti di avvio nella soluzione. Solo i progetti di applicazione di Infrastruttura di servizi devono essere impostati come progetti di avvio.

> [!TIP]
> Se, dopo l'installazione, il cluster locale inizia toobehave in modo anomalo, è possibile reimpostarlo utilizzando un'applicazione hello cluster locale manager sistema barra delle applicazioni. Questo rimuove hello cluster esistente e impostare uno nuovo. Tenere presente che verranno rimosse anche tutte le applicazioni distribuite e i dati associati.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Comprendere e risolvere i problemi del cluster con report di integrità del sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

