---
title: aaaAbout App per dispositivi mobili in Azure App Service
description: Informazioni sui vantaggi di hello che servizio App attiva enterprise tooyour App per dispositivi mobili.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ab96af11c3df196acfb9ecec1339e7f6093c7066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>Informazioni su App per dispositivi mobili nel servizio app di Azure
Il servizio app di Azure è un'offerta di [piattaforma distribuita come servizio ](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) interamente gestita per sviluppatori professionisti. servizio Hello offre una vasta gamma di funzionalità scenari tooweb, mobili e l'integrazione. 

funzionalità di App per dispositivi mobili Hello di servizio App di Azure offre agli sviluppatori enterprise e piattaforma di sviluppo integratori un'applicazione mobile sistema altamente scalabili e disponibili a livello globale.

![Panoramica visiva delle funzionalità di App per dispositivi mobili](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a>Perché le app per dispositivi mobili?
Grazie a funzionalità di hello App per dispositivi mobili, è possibile:

* **Compilare app native e multipiattaforma**. Sia che si compilino app native iOS, Android e Windows o app multipiattaforma Xamarin o Cordova (PhoneGap), è possibile sfruttare il servizio app usando SDK nativi.
* **Connettersi a sistemi aziendali tooyour**: grazie a funzionalità di App per dispositivi mobili hello, è possibile aggiungere Accedi aziendale in minuti e connettersi tooyour enterprise locale o risorse cloud.
* **Creazione di applicazioni disponibile offline con sincronizzazione dati**: stabilire più produttivi alla forza lavoro mobile tramite la creazione di applicazioni che funzionano in modalità offline e utilizzare dati toosync App per dispositivi mobili in background hello quando la connettività è presente con le proprie origini dati aziendali o software come servizio (SaaS) API.
* **Eseguire il push delle notifiche toomillions in secondi**: contattare i clienti con le notifiche push immediata in qualsiasi dispositivo personalizzati tootheir esigenze e inviato quando il tempo di hello è corretto.

## <a name="mobile-apps-features"></a>Funzionalità di App per dispositivi mobili
Hello seguenti caratteristiche è importanti abilitato toocloud sviluppo di applicazioni mobile:

* **Autenticazione e autorizzazione**. È possibile scegliere da un elenco in costante crescita di provider di identità, tra cui Azure Active Directory per l'autenticazione aziendale, nonché provider di servizi di social networking come Facebook, Google, Twitter e account Microsoft. App per dispositivi mobili offre un servizio OAuth 2.0 per ogni provider. È inoltre possibile integrare hello SDK per il provider di identità hello per le funzionalità specifiche del provider.

    Altre informazioni sulle [funzionalità di autenticazione].

* **Accesso ai dati**: App per dispositivi mobili fornisce un'origine dati OData v3 per mobile descrittivi che è collegato tooAzure Database SQL o un server SQL locale. Dato che questo servizio può essere basato su Entity Framework, consente una facile integrazione con altri provider di dati NoSQL e SQL, tra cui [Archiviazione tabelle di Azure], MongoDB e [Azure Cosmos DB], e provider di API SaaS come Office 365 e Salesforce.com.

* **Sincronizzazione non in linea**: il client SDK renderlo toobuild facile affidabile e reattive applicazioni per dispositivi mobili che operano con un set di dati non in linea. È possibile sincronizzare questo set di dati automaticamente con i dati di back-end hello, incluso il supporto di risoluzione dei conflitti.

  Altre informazioni sulle [funzionalità dati].

* **Le notifiche push**: il client SDK si integrano perfettamente con le funzionalità di registrazione hello Azure degli hub di notifica, pertanto è possibile inviare contemporaneamente toomillions le notifiche push degli utenti.

  Altre informazioni sulle [funzionalità di notifica push].

* **SDK client**. Viene offerto un set completo di SDK client che coprono lo sviluppo nativo ([iOS], [Android] e [Windows]), multipiattaforma ([Xamarin.iOS, Xamarin.Android] e [Xamarin.Forms]) e di applicazioni ibride ([Apache Cordova]). Ogni SDK client è disponibile con una licenza MIT ed è open source.

## <a name="azure-app-service-features"></a>Funzionalità del servizio app di Azure
Hello seguenti funzionalità della piattaforma sono utile per i siti di produzione per dispositivi mobili:

* **La scalabilità automatica**: con il servizio App, è possibile applicare la scalabilità verticale rapidamente o scalabilità toohandle qualsiasi carico di clienti in ingresso. Manualmente selezionare hello numero e le dimensioni delle macchine virtuali oppure impostare la scalabilità automatica tooscale il back-end app per dispositivi mobili in base a una pianificazione o di carico.

  Altre informazioni sulla [scalabilità automatica].

* **Ambienti di staging**. Il servizio app può eseguire più versioni del sito e consente così di eseguire test A/B, test in ambiente di produzione nell'ambito di un piano DevOps più ampio e staging sul posto di un nuovo back-end.

  Altre informazioni sugli [ambienti di staging].

* **La distribuzione continua**: servizio App può essere integrato con sistemi di Gestione (controllo servizi SCM) catena alimentazione comune, pertanto è possibile distribuire automaticamente una nuova versione del back-end mediante il push tooa branch del sistema di Gestione controllo servizi.

  Altre informazioni sulle [opzioni di distribuzione].

* **La rete virtuale**: servizio App possono connettersi le risorse locali tooon tramite connessioni di rete, Azure ExpressRoute o ibrida virtuale.

  Altre informazioni su [connessioni ibride], [reti virtuali] ed [ExpressRoute].

* **Ambienti isolati e dedicati**. È possibile eseguire il servizio app in un ambiente completamente isolato e dedicato per l'esecuzione sicura delle app del servizio app di Azure su larga scala. Un ambiente di questo tipo è ideale per i carichi di lavoro delle applicazioni che richiedono scalabilità elevata, isolamento o accesso alla rete sicuro.

  Altre informazioni sugli [ambienti del servizio app].

## <a name="next-steps"></a>Passaggi successivi

tooget avviato con l'App per dispositivi mobili in Azure App Service, hello completo [Introduzione] esercitazione. esercitazione Hello copre nozioni fondamentali di hello di produrre mobili nuovamente terminare e client di propria scelta. nonché l'integrazione dell'autenticazione, della sincronizzazione offline e delle notifiche push. È possibile completare Esercitazione hello più volte, una volta per ogni applicazione client.

Per altre informazioni su App per dispositivi mobili, vedere la [mappa di apprendimento].
Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service].

<!-- URLs. -->
[Migrate your mobile service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Introduzione]: app-service-mobile-ios-get-started.md
[Archiviazione tabelle di Azure]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[funzionalità di autenticazione]: ./app-service-mobile-auth.md
[funzionalità dati]: ./app-service-mobile-offline-data-sync.md
[funzionalità di notifica push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS, Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[scalabilità automatica]: ../app-service-web/web-sites-scale.md
[ambienti di staging]: ../app-service-web/web-sites-staged-publishing.md
[opzioni di distribuzione]: ../app-service-web/web-sites-deploy.md
[connessioni ibride]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[reti virtuali]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[ambienti del servizio app]: ../app-service-web/app-service-app-service-environment-intro.md
[mappa di apprendimento]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
