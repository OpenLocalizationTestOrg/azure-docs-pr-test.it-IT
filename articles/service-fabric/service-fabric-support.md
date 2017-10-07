---
title: aaaLearn sulle opzioni di supporto dell'infrastruttura del servizio di Azure | Documenti Microsoft
description: Versioni di Azure Service Fabric cluster supportato e collega i ticket di supporto toofile
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Opzioni di supporto di Azure Service Fabric

il supporto appropriato toodeliver hello per i cluster di Service Fabric che si esegue il lavoro dell'applicazione viene caricato su, e abbiamo impostato varie opzioni per l'utente. Variano a seconda di hello livello di supporto e gravità hello del problema hello, ottenere toopick opzioni corrette hello. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Segnalare problemi di produzione o relativi al sito live o richiedere supporto a pagamento per Azure

Per la segnalazione di problemi relativi al sito live nel cluster di Service Fabric distribuito in Azure, aprire un ticket per il supporto professionale nel [portale di Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) o nel [portale di supporto Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Altre informazioni su:
 
- [Supporto professionale Microsoft per Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Supporto tecnico Premier Microsoft](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Segnalare problemi di produzione o relativi al sito live o richiedere supporto a pagamento per i cluster di Service Fabric autonomi

Per la segnalazione di problemi relativi al sito live nel cluster di Service Fabric distribuito in locale o in altri cloud, aprire un ticket per il supporto professionale nel [portale del supporto tecnico di Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Altre informazioni su:

- [Supporto professionale Microsoft per la distribuzione in locale](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Supporto tecnico Premier Microsoft](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Segnalare problemi di Azure Service Fabric 
È disponibile un archivio GitHub per la segnalazione dei problemi relativi a Service Fabric.  Si sta monitorando anche attivamente hello seguenti forum.

### <a name="github-repo"></a>Archivio GitHub 
Segnalare i problemi di Azure Service Fabric nell'[archivio Git dei problemi relativi a Service Fabric](https://github.com/Azure/service-fabric-issues). Questo archivio è destinato alla segnalazione e al rilevamento dei problemi di Azure Service Fabric e all'invio di richieste di funzionalità minori. **Non utilizzare questo sito in tempo reale tooreport problemi**.

### <a name="stackoverflow-and-msdn-forums"></a>Forum StackOverflow e MSDN

Hello [tag Service Fabric su StackOverflow] [ stackoverflow] hello e [forum di Service Fabric su MSDN] [ msdn-forum] migliore vengono utilizzati per porre domande sulle come funziona la piattaforma hello e illustrato come effettuare alcune attività con esso.

### <a name="azure-feedback-forum"></a>Forum di commenti e suggerimenti su Azure

Hello [Forum di commenti e suggerimenti di Azure per Service Fabric] [ uservoice-forum] è hello migliore per l'invio di idee big funzionalità è necessario per il prodotto hello come esaminando le richieste più diffusi hello fanno parte del nostro medio termine toolong la pianificazione. Si consiglia di supporto toorally i suggerimenti all'interno della community di hello.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Versioni di Service Fabric supportate

Verificare che il cluster esegua sempre una versione di Service Fabric supportata. Come e quando è annunciare il rilascio di hello di una nuova versione di Service Fabric, la versione precedente di hello è contrassegnata per la fine del supporto dopo un minimo di 60 giorni dalla data. Hello nuovi rilasci vengono annunciate [sul blog del team di Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).

Fare riferimento toohello seguito documenti sulle informazioni dettagliate su come tookeep il cluster che esegue una versione supportata di Service Fabric.

- [Aggiornare un cluster di Azure Service Fabric ](service-fabric-cluster-upgrade.md)
- [Aggiornare il cluster autonomo di Service Fabric in Windows Server ](service-fabric-cluster-upgrade-windows-server.md)
 
Ecco l'elenco hello delle versioni di Service Fabric hello supportati e la data di fine di supporto.

| **Cluster runtime di Service Fabric** | **Versioni di SDK / pacchetto NuGet compatibili** | **Data di fine supporto** |
| --- | --- | --- |
| Tutti i cluster too5.3.121 di versioni precedenti |Minore o uguale tooversion 2.3 |20 gennaio 2017 |
| 5.3.* |Minore o uguale tooversion 2.3 |24 febbraio 2017 |
| 5.4.* |Minore o uguale tooversion 2.4 |10 maggio 2017     |
| 5.5.* |Minore o uguale tooversion 2.5 |10 agosto 2017    |
| 5.6.* |Minore o uguale tooversion 2.6 |13 ottobre 2017    |
| 5.7.* |Minore o uguale tooversion 2.7 |Versione corrente, nessuna data di fine supporto

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Versioni di anteprima di Service Fabric non supportate per l'uso in produzione
Da ora tootime, abbiamo versione versioni che dispongono di funzionalità significative che vogliamo commenti e suggerimenti, vengono rilasciate come anteprime. Queste versioni di anteprima devono essere usate solo a scopo di test. In un cluster di produzione deve essere sempre in esecuzione una versione di Service Fabric supportata e stabile. Una versione di anteprima inizia sempre con un numero di versione principale e secondario uguale a 255. Ad esempio, se viene visualizzato un esempio di Service Fabric versione 255.255.5703.949, tale versione è utilizzato in cluster di test e toobe solo in anteprima. Queste versioni di anteprima vengono annunciate anche sulla hello [blog del team di Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric) e dispone di informazioni sulle funzionalità di hello inclusione.

Non esiste alcuna opzione di supporto a pagamento per queste versioni di anteprima. Utilizzare una delle opzioni di hello sotto [genera Report Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask domande o fornire commenti e suggerimenti.

## <a name="next-steps"></a>Passaggi successivi

- [Aggiornare un cluster di Azure Service Fabric ](service-fabric-cluster-upgrade.md)
- [Aggiornare il cluster autonomo di Service Fabric in Windows Server ](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
