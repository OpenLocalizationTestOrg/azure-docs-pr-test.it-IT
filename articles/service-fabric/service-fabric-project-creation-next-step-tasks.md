---
title: passaggi successivi creazione progetto infrastruttura aaaService | Documenti Microsoft
description: "In questo articolo contiene collegamenti un set di tooa delle attività di sviluppo di componenti di base per l'infrastruttura di servizio"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Applicazione dell'infrastruttura di servizi e fasi successive
L'applicazione Service Fabric di Azure è stata creata. In questo articolo descrive composizione di hello del progetto e alcuni possibili passaggi successivi.

## <a name="your-application"></a>L'applicazione
Ogni nuova applicazione include un progetto di applicazione. Potrebbero essere presenti uno o due progetti aggiuntivi, in base al tipo di hello di servizio scelto.

### <a name="hello-application-project"></a>progetto di applicazione Hello
progetto di applicazione Hello è costituito da:

* Un set di servizi di toohello riferimenti che costituiscono l'applicazione.
* Tre profili (1-nodo locale, 5-nodo locale e Cloud) che è possibile utilizzare toomaintain preferenze per l'utilizzo di ambienti diversi, ad esempio le preferenze tooa correlati cluster endpoint e se tooperform aggiornare le distribuzioni per impostazione predefinita di pubblicazione.
* Tre i file dei parametri dell'applicazione (come sopra) che è possibile utilizzare le configurazioni di applicazione specifico dell'ambiente toomaintain, ad esempio il numero di hello di toocreate partizioni per un servizio.
* Uno script di distribuzione che è possibile utilizzare toodeploy l'applicazione dalla riga di comando hello o come parte di una pipeline automatizzata integrazione e la distribuzione continua.
* manifesto dell'applicazione di Hello, che descrive un'applicazione hello. È possibile trovare hello manifesto nella cartella ApplicationPackageRoot hello.

### <a name="stateless-service"></a>Servizio senza stato
Quando si aggiunge un nuovo servizio senza stato, Visual Studio aggiunge una soluzione tooyour di progetto di servizio che include un tipo discende da `StatelessService`. servizio Hello incrementa una variabile locale in un contatore.

### <a name="stateful-service"></a>Servizio con stato
Quando si aggiunge un nuovo servizio con stato, Visual Studio aggiunge una soluzione tooyour di progetto di servizio che include un tipo discende da `StatefulService`. servizio Hello incrementa un contatore nel relativo `RunAsync` (metodo) e archivia il risultato hello in un `ReliableDictionary`.

### <a name="actor-service"></a>Servizio Actor
Quando si aggiunge un nuovo attore affidabile, Visual Studio aggiunge due soluzioni di tooyour progetti: un progetto attore e un progetto di interfaccia.

progetto attore Hello fornisce metodi per l'impostazione e recupero valore hello di un contatore che viene mantenuto in modo affidabile all'interno dello stato dell'actor hello. Hello interfaccia progetto fornisce un'interfaccia che altri servizi possono utilizzare attore hello tooinvoke.

### <a name="stateless-web-api"></a>API Web senza stato
progetto API Web senza stato Hello fornisce un base che è possibile utilizzare tooopen tooexternal client dell'applicazione di servizio web. Per ulteriori informazioni su come progetto di hello strutturato, vedere [servizi API Web dell'infrastruttura del servizio con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET Core
Hello Service Fabric SDK fornisce hello stesso insieme di modelli ASP.NET Core disponibili per i progetti ASP.NET Core autonoma: vuoto, [API Web][aspnet-webapi], e [applicazione Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Eseguibili guest e contenitori guest

Un'infrastruttura di servizio 'guest' è un servizio che non viene compilato con modelli di programmazione della piattaforma hello. È possibile comprimere i file binari hello per un utente guest è [direttamente nel pacchetto di applicazione hello](service-fabric-deploy-existing-app.md) o [tramite un'immagine contenitore](service-fabric-deploy-container.md). In entrambi i casi, Visual Studio crea hello gli elementi necessari in hello **ApplicationPackageRoot** nella cartella del progetto di applicazione hello. Visual Studio non creerà un nuovo progetto di servizio codice hello esiste già in un' posizione. Se si desidera toomanage il guest progetti insieme a progetto di applicazione di Service Fabric hello, è possibile aggiungerli toohello stessa soluzione di Visual Studio.

## <a name="next-steps"></a>Passaggi successivi
### <a name="create-an-azure-cluster"></a>Creare un cluster di Azure
Hello Service Fabric SDK fornisce un cluster locale per lo sviluppo e test. toocreate un cluster in Azure, vedere [impostazione di un cluster di Service Fabric dal portale di Azure hello][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Pubblicare l'applicazione tooAzure
È possibile pubblicare l'applicazione direttamente da Visual Studio tooan cluster di Azure. toolearn, vedere [tooAzure l'applicazione di pubblicazione][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Usare un cluster di Service Fabric Explorer toovisualize
Service Fabric Explorer offre un modo semplice di toovisualize del cluster, incluse le applicazioni distribuite e il layout fisico. vedere, più toolearn [la visualizzazione del cluster usando Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Effettuare il versioning e aggiornare i servizi
Service Fabric consente il controllo indipendente delle versioni e l'aggiornamento di servizi indipendenti in un'applicazione. vedere, più toolearn [controllo delle versioni e l'aggiornamento dei servizi][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configurare l'integrazione continua con Visual Studio Team Services
toolearn come è possibile impostare un processo di integrazione continua per l'applicazione di Service Fabric, vedere [configurare l'integrazione continua con Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
