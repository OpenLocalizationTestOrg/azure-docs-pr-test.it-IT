---
title: "App per le API del servizio - novità aaaApp | Documenti Microsoft"
description: "Informazioni sulle novità relative alle app per le API nel servizio app di Azure."
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App per le API del servizio app: Modifiche apportate
Evento di hello Connect () di novembre 2015, una serie di miglioramenti tooAzure servizio App sono state [annunciato](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Questi miglioramenti includono modifiche sottostante tooAPI App toobetter allineare con dispositivi mobili e App Web, ridurre il numero di concetto e migliorare le prestazioni di runtime e di distribuzione. A partire dal 30 novembre 2015, nuove API App creata tramite il portale di gestione di Azure hello o gli strumenti più recenti di hello rifletterà le modifiche. In questo articolo vengono descritte queste modifiche, nonché il modo tooredeploy esistente App tootake sfruttare funzionalità hello.

## <a name="feature-changes"></a>Modifiche apportate alle funzionalità
le funzionalità principali di Hello di App per le API-autenticazione, i metadati API e CORS-sono stati spostati direttamente nel servizio App. Con questa modifica, hello funzionalità sono disponibili in App per le API, mobili e Web. In effetti, tutti i tre condivisione hello stesso **Microsoft.Web/sites** in Gestione risorse di tipo di risorsa. gateway di Hello App per le API non è più necessario o offerto con App per le API. Questo rende più semplice toouse gestione API di Azure poiché sarà sufficiente hello singolo API gateway di gestione.

![Panoramica delle app per le API](./media/app-service-api-whats-changed/api-apps-overview.png)

Un principio di progettazione principale con aggiornamento di App per le API hello è tooenable toobring è l'API come, nel linguaggio desiderato.  Se l'API sono già distribuita come un'App Web o App per dispositivi mobili, non si dispone tooredeploy comodamente app tootake delle nuove funzionalità di hello. Se le app per le API vengono usate in anteprima, seguire le istruzioni per la migrazione riportate di seguito.

### <a name="authentication"></a>Autenticazione
Hello turnkey App per le API, servizi o App per dispositivi mobili e App Web autenticazione e le funzionalità esistenti sono state unificate sono disponibili in un singolo pannello di autenticazione servizio App di Azure nel portale di gestione di hello. Per i servizi di tooauthentication un'introduzione nel servizio App, vedere [l'autenticazione del servizio App di espansione / autorizzazione](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

Per gli scenari di API, sono disponibili varie nuove funzionalità:

* **Supporto per l'utilizzo di Azure Active Directory direttamente**, senza il codice client con token AAD hello tooexchange per un token di sessione: il client può includere solo token AAD hello nell'intestazione di autorizzazione hello, in base a token di connessione toohello specifica. Questo significa anche SDK non specifico del servizio App è obbligatorio in sul lato client o server hello. 
* **Accesso al servizio o "Interno"**: se si dispone di un processo del daemon o un altro client che richiedono accesso tooAPIs senza un'interfaccia, è possibile richiedere un token con un'entità servizio AAD e passarlo tooApp servizio per l'autenticazione con il applicazione.
* **Autorizzazione posticipata**: molte applicazioni hanno restrizioni di accesso diversi per le diverse parti dell'applicazione hello. Si supponga toobe alcune API disponibile pubblicamente, mentre altri richiedono l'accesso. la funzionalità di autenticazione/autorizzazione originale Hello è radicale, con l'intero sito hello che richiedono account di accesso. Questa opzione esiste ancora, ma è possibile in alternativa consente il codice dell'applicazione le decisioni di accesso toorender dopo servizio App ha autenticato l'utente di hello.

Per ulteriori informazioni sulle nuove funzionalità di autenticazione hello, vedere [autenticazione e autorizzazione per App per le API in Azure App Service](app-service-api-authentication.md). Per informazioni su come toomigrate esistente App per le API da precedente App hello per le API del modello vedere a una nuova toohello [App per le API esistenti migrazione](#migrating-existing-api-apps) più avanti in questo articolo.

### <a name="cors"></a>CORS
Anziché delimitato da virgole **MS_CrossDomainOrigins** app impostazione, è ora disponibile un pannello nel portale di gestione di Azure hello per la configurazione CORS. In alternativa, è possibile eseguirne la configurazione usando strumenti di Gestione risorse come Azure PowerShell, l'interfaccia della riga di comando o [Esplora risorse](https://resources.azure.com/). Set hello **cors** proprietà hello **Microsoft.Web/sites/config** tipo di risorsa per il  **&lt;nome sito&gt;/web** risorse. ad esempio:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Metadati dell'API
Pannello di definizione API Hello è ora disponibile in App per le API, mobili e Web. Nel portale di gestione di hello, è possibile specificare un url relativo o un url assoluto verso endpoint tooan tale rappresentazione host un Swagger 2.0 dell'API. In alternativa, è possibile eseguire la configurazione usando gli strumenti di Gestione risorse. Set hello **apiDefinition** proprietà hello **Microsoft.Web/sites/config** tipo di risorsa per il  **&lt;nome sito&gt;/web** risorse. ad esempio:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

In questo momento, endpoint di metadati hello deve toobe accessibile pubblicamente senza autenticazione per molti client downstream (generazione di client, ad esempio Visual Studio API REST e del flusso di "Aggiungi API" PowerApps) tooconsume è. Ciò significa che se si utilizza l'autenticazione del servizio App e si desidera definizione dell'API hello tooexpose all'interno dell'app stessa, è necessario l'opzione di autenticazione posticipata hello toouse descritto in precedenza in modo che i metadati Swagger tooyour route hello sono pubblico.

## <a name="management-portal"></a>Portale di gestione
Selezione **nuovo > Web e dispositivi mobili > App per le API** in hello portale verrà creata l'App per le API che riflettono le nuove funzionalità hello descritta nell'articolo hello. **Esplora &gt; App per le API** consente solo di visualizzare le nuove app per le API. Dopo la visualizzazione in un'app di API, hello pannello condivisioni hello stesso layout e le funzionalità dell'App Web e dispositivi mobili. Hello uniche differenze sono il contenuto delle Guide rapide e ordinamento delle impostazioni.

App per le API esistenti (o App per le API Marketplace creato da logica App) con hello funzionalità di anteprima precedente continuerà a essere visibile nella finestra di progettazione logica App hello e durante l'esplorazione di tutte le risorse in un gruppo di risorse.

## <a name="visual-studio"></a>Visual Studio
La maggior parte delle applicazioni Web strumenti funzionerà con nuove API App poiché condividono hello sottostante stesso **Microsoft.Web/sites** tipo di risorsa. gli strumenti di Azure per Visual Studio Hello, tuttavia, deve essere aggiornato tooversion 2.8.1 o versioni successive poiché espone un numero di funzionalità specifiche tooAPIs. Scaricare il SDK di hello da hello [pagina di download di Azure](https://azure.microsoft.com/downloads/).

Razionalizzazione hello di hello tipi di servizio App, di pubblicare anche unificata in **pubblica > Microsoft Azure App Service**:

![Pubblicazione di app per le API](./media/app-service-api-whats-changed/api-apps-publish.png)

ulteriori informazioni sul SDK, 2.8.1 annuncio hello lettura toolearn [post di blog](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

In alternativa, è possibile importare manualmente hello pubblicare tooenable portale di gestione hello profilo di pubblicazione. Per Cloud Explorer, la generazione di codice e la selezione/creazione di app per le API, tuttavia, sarà necessario l'SDK 2.8.1 o versione successiva.

## <a name="migrating-existing-api-apps"></a>Migrazione delle app per le API esistenti
Se l'API personalizzata è distribuita toohello precedente versione di anteprima dell'App per le API, è richiesta migrare toohello nuovo modello per App per le API del 31 dicembre 2015. Poiché sia il modello di vecchi e nuovi hello è basato su API Web ospitate nel servizio App, la maggior parte hello del codice esistente può essere riutilizzato.

### <a name="hosting-and-redeployment"></a>Hosting e ridistribuzione
passaggi di Hello per ridistribuire sono hello uguale a qualsiasi esistente tooApp API Web del servizio di distribuzione. Passaggi:

1. Creare un'app per le API vuota. Questa operazione può essere eseguita nel portale di hello con nuovo > App per le API, in Visual Studio da pubblica o da strumenti di gestione risorse. Se si utilizza strumenti di gestione risorse o i modelli, impostare hello **tipo** valore troppo**api** su hello **Microsoft.Web/sites** risorse tipo toohave hello delle Guide rapide e impostazioni portale di gestione di Hello orientate ad applicazioni scenari API.
2. Connettersi e distribuire il progetto toohello vuoto API app utilizzando uno dei meccanismi di distribuzione hello è supportati dal servizio App. Lettura [documentazione sulla distribuzione di servizio App di Azure](../app-service-web/web-sites-deploy.md) toolearn altre. 

### <a name="authentication"></a>Autenticazione
Hello supporto di servizi di autenticazione del servizio App hello stesse funzionalità disponibili con modello di App per le API precedente hello. Se si utilizza il token di sessione che richiedono gli SDK, usare hello SDK client e server seguenti:

* Client: [Azure Mobile Client SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Server: [pacchetto di estensione di Microsoft Azure Mobile .NET Server Authentication](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Se invece si utilizzano hello alfa di servizio App SDK, queste sono ora deprecate:

* Client: [Microsoft Azure AppService SDK](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Server: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

In particolare con Azure Active Directory, tuttavia, non specifico del servizio App è obbligatorio se si utilizza il token AAD hello direttamente.

### <a name="internal-access"></a>Accesso interno
modello di App per le API precedente Hello incluso un livello di accesso interno incorporato. Utilizzo di hello SDK questa operazione necessaria per la firma di richieste. Come descritto in precedenza, con hello nuova App per le API del modello, entità servizio AAD è utilizzabile come alternativa per l'autenticazione al servizio senza richiedere un servizio specifico dell'App SDK. Per altre informazioni, vedere [Autenticazione dell'entità servizio per app per le API nel servizio app di Azure](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Individuazione
modello aveva API per l'individuazione in fase di esecuzione in altre App per le API precedenti App per le API hello stesso gruppo di risorse dietro Hello hello stesso gateway. Ciò risulta particolarmente utile nelle architetture che implementano modelli di microservizio. Questa funzionalità non è più supportata direttamente, ma sono disponibili diverse opzioni:

1. Utilizzare hello dell'API di gestione risorse di Azure per l'individuazione.
2. Inserire Gestione API di Azure prima delle API ospitate dal servizio app. Usare Gestione API di Azure come un'interfaccia che può fornire un URL esterno stabile anche se la topologia interna viene modificata.
3. Compilazione di un'app di API di individuazione e dispone di altre applicazioni di API registrare con app individuazione hello all'avvio.
4. In fase di distribuzione, popolare impostazioni dell'app hello tutti hello API App (e client) con gli endpoint hello di hello App per le altre API. Questo è valido nelle distribuzioni di modello e dall'App per le API ora consentono di controllo dell'url hello.

## <a name="using-api-apps-with-logic-apps"></a>Uso delle app per le API con app per la logica
nuovo modello di App API Hello funziona bene con [logica App versione dello schema 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Passaggi successivi
toolearn più, leggere gli articoli di hello in hello [sezione della documentazione di App API](https://azure.microsoft.com/documentation/services/app-service/api/). Sono stati aggiornati tooreflect hello nuovo modello di per App per le API. Inoltre, raggiungere nei forum di hello per altri dettagli o informazioni aggiuntive sulla migrazione:

* [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

