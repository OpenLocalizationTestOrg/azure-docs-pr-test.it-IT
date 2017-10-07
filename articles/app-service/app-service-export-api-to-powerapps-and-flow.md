---
title: aaaExporting un tooPowerApps API ospitato di Azure e Microsoft Flow | Documenti Microsoft
description: Panoramica di come tooexpose un'API ospitato nel servizio App tooPowerApps e Microsoft Flow
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Esportazione di un tooPowerApps API ospitato di Azure e Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Creare connettori personalizzati per PowerApps e Microsoft Flow

[PowerApps](https://powerapps.com) è un servizio per la creazione e uso di App di business personalizzata che si connettono tooyour dati e di lavoro tra le piattaforme. [Microsoft Flow](https://flow.microsoft.com) rende facile tooautomate flussi di lavoro e i processi di business tra i servizi e App preferite. PowerApps sia Microsoft Flow includono una gamma di origini toodata connettori incorporati, ad esempio Office 365, Dynamics 365, Salesforce e altro ancora. Tuttavia, gli utenti devono inoltre toobe tooleverage in grado di origini dei dati e le API compilate dall'organizzazione.

Analogamente, gli sviluppatori che vogliono tooexpose le rispettive API ulteriori su vasta scala all'interno di hello organizzazione opportuno toomake i relativi utenti di Microsoft Flow e l'API tooPowerApps disponibili. In questo argomento illustra la modalità di compilazione con tooPowerApps Azure App Service o funzioni di Azure e Microsoft Flow tooexpose un'API. [Servizio App di Azure](https://azure.microsoft.com/services/app-service/) è un'offerta platform-as-a-service che consente agli sviluppatori tooquickly e facilmente web aziendale di compilazione, applicazioni mobili e API. [Funzioni di Azure](https://azure.microsoft.com/services/functions/) è una soluzione di calcolo senza server basato su eventi che consente a codice autore tooquickly che può rispondere tooother parti del sistema e scala in base alle esigenze.

toolearn informazioni su questi servizi, vedere:
- [Formazione guidata di PowerApps](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Formazione guidata di Microsoft Flow](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Informazioni sul servizio app](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Che cos'è Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Condividere la definizione di un'API

Le API vengono spesso descritti tramite un [OpenAPI documento](https://www.openapis.org/) (talvolta definita tooas un documento "Swagger"). Contiene le informazioni di hello sulle operazioni che sono disponibili come dati di hello devono essere strutturati. PowerApps e Microsoft Flow possono creare connettori personalizzati per qualsiasi documento OpenAPI 2.0. Dopo aver creato un connettore personalizzato, può essere utilizzato in hello esattamente come uno dei connettori incorporati hello e possono essere integrati rapidamente in un'applicazione.

Il Servizio app di Azure e Funzioni di Azure dispongono di [supporto integrato](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) per la creazione, l'hosting e la gestione di un documento OpenAPI. In ordine toocreate un connettore personalizzato per un web per dispositivi mobili, API o app di funzione, flusso e PowerApps necessario toobe assegnata una copia della definizione di hello.

> [!NOTE]
> Perché è in uso una copia della definizione dell'API di hello, PowerApps e Microsoft Flow non immediatamente conosceranno aggiornamenti o applicazione toohello modifiche di rilievo. Se una nuova versione dell'API di hello viene resa disponibile, questa procedura deve essere ripetuta per la nuova versione di hello. 

tooprovide PowerApps e Microsoft Flow con hello ospitato di definizione dell'API per l'app, seguire questi passaggi:

1. Aprire hello [portale Azure](https://portal.azure.com) e passare tooyour applicazione di servizio App o funzioni di Azure.

    Se si utilizza servizio App di Azure, selezionare **di definizione dell'API** dall'elenco di impostazioni hello. 
    
    Se si usa Funzioni di Azure, selezionare l'app per le funzioni interessata, scegliere **Funzionalità della piattaforma** e quindi **Definizione API**. È anche possibile scegliere hello tooopen **(anteprima) di definizione dell'API** scheda invece.

2. Se è stata specificata una definizione dell'API, verrà visualizzato un **esportare tooPowerApps + Microsoft Flow** pulsante. Fare clic su questo processo di esportazione hello toobegin pulsante.

3. Seleziona hello **modalità esportazione**. Consente di determinare i passaggi di hello che sarà necessario toofollow toocreate un connettore. Il servizio app offre due opzioni per fornire la definizione dell'API a PowerApps e Microsoft Flow:

    **Express** consente di creare connettore personalizzato hello all'interno di hello portale di Azure. Richiede che hello correnti utente connesso dispone di autorizzazione toocreate connettori nell'ambiente di destinazione hello. Si tratta di hello approccio consigliato se tale requisito può essere soddisfatto. Se si utilizza questa modalità, seguire hello [Express esportazione](#express) istruzioni riportate di seguito.

    **Manuale** consente di esportare una copia della definizione di hello API che può essere importato utilizzando hello PowerApps o Microsoft Flow portali. Si tratta di hello approccio consigliato se hello utente di Azure e hello con i connettori toocreate autorizzazioni sono diverse o se il connettore di hello deve toobe creato in un altro tenant. Se si utilizza questa modalità, seguire hello [importazione ed esportazione manuale](#manual) istruzioni riportate di seguito.

<a name="express"></a>
## <a name="express-export"></a>Esportazione rapida

In questa sezione si creerà un nuovo connettore personalizzato all'interno di hello portale di Azure. È necessario essere connessi in hello tenant toowhich desiderato tooexport e, è necessario disporre dell'autorizzazione toocreate un connettore personalizzato nell'ambiente di destinazione hello.

1. Selezionare l'ambiente hello in cui si desidera connettore hello toocreate. Specificare quindi un nome per il connettore personalizzato.

2. Se la definizione dell'API include definizioni di sicurezza, queste verranno indicate nel passaggio 2. Se necessario, fornire sicurezza hello dettagli di configurazione necessarie toogrant accesso API tooyour. Per altre informazioni, vedere [Autenticazione](#auth) di seguito. 

3. Fare clic su **OK** toocreate il connettore personalizzato.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Esportazione e importazione manuali

In ordine toocreate un connettore personalizzato per un web per dispositivi mobili, API o app di funzione, saranno necessari due passaggi:

1. [Recupero definizione dell'API hello dal servizio App o funzioni di Azure](#export)
2. [Importazione di definizione dell'API hello in PowerApps e Microsoft Flow](#import)

È possibile che questi due passaggi necessario toobe svolte dai singoli utenti separati all'interno dell'organizzazione, come un determinato utente non dispone dell'autorizzazione tooperform entrambe le azioni. Uno sviluppatore che ha collaboratore toohello di accesso dell'applicazione di servizio App o funzioni di Azure in questo caso, sarà necessario definizione hello API tooobtain (un singolo file JSON) o tooit un collegamento. Sarà quindi necessario tooprovide tale definizione tooa PowerApps o Microsoft Flow il proprietario. Il proprietario può usare connettore personalizzato hello toocreate metadati hello.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Recupero definizione dell'API hello dal servizio App o funzioni di Azure

In questa sezione, si esporterà definizione dell'API per l'API del servizio App, usato in un secondo momento nel portale di PowerApps o Microsoft Flow hello toobe hello.

1. È possibile scegliere tooeither **Scarica definizione hello API** o **di ottenere un collegamento**. A seconda del valore scelto, il risultato di hello verrà fornito nella sezione successiva hello. Selezionare una delle seguenti opzioni e seguire le istruzioni di hello.
 
2. Se la definizione dell'API include definizioni di sicurezza, queste verranno indicate nel passaggio 2. Durante l'importazione, PowerApps e Microsoft Flow le rileveranno e richiederanno informazioni sulla sicurezza. Raccogliere hello credenziali tooeach correlati definizione per l'utilizzo nella sezione successiva hello. Per altre informazioni, vedere [Autenticazione](#auth) di seguito. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Importazione di definizione dell'API hello in PowerApps e Microsoft Flow

In questa sezione si creerà un connettore personalizzato in PowerApps e Microsoft Flow utilizzando definizione hello API ottenuta in precedenza. Connettori personalizzati vengono condivisi tra hello due servizi, pertanto è necessario solo definizione di hello tooimport una sola volta. Per altre informazioni sui connettori personalizzati, vedere [registrare e utilizzare i connettori personalizzati in PowerApps] e [registrare e utilizzare i connettori personalizzati in Microsoft Flow].

1. Aprire hello [portale web Powerapps](https://web.powerapps.com) o hello [portale web di Microsoft Flow](https://flow.microsoft.com/)ed eseguire l'accesso. 

2. Fare clic su hello **impostazioni** pulsante (icona a forma di ingranaggio hello) in alto a destra hello della pagina hello e selezionare **connettori personalizzati**. 

3. Fare clic su **Create custom connector** (Crea connettore personalizzato).

4. In hello **generale** scheda, specificare un nome per l'API e quindi caricare definizione OpenAPI hello o incollare nell'URL dei metadati hello. Fare clic su **Continue**.

4. In hello **sicurezza** scheda, in caso di richiesta tooprovide dettagli relativi all'autenticazione, immettere i valori hello ottenuti nella sezione precedente hello. In caso contrario, procedere toohello successivo.

5. In hello **definizioni** scheda tutte le operazioni definite nel file OpenAPI hello vengono popolati automaticamente. Se si definiscono tutte le operazioni necessarie, è possibile passare toohello successivo. In caso contrario, è possibile aggiungere e modificare qui le operazioni.

6. Fare clic su **Crea connettore**. Se si desidera tootest le chiamate API, visitare toohello successivo.

7. In hello **Test** scheda, creare una connessione, selezionare un'operazione tootest e immettere i dati necessari per l'operazione di hello.

8. Fare clic su **Verifica operazione**.


<a name="auth"></a>
## <a name="authentication"></a>Autenticazione

PowerApps e Microsoft Flow supporto nativo per una raccolta di provider di identità che può essere utilizzato toolog gli utenti del connettore personalizzato. Se l'API richiede l'autenticazione, assicurarsi che venga acquisita come _definizione di sicurezza_ nel documento OpenAPI. Durante l'esportazione, sarà necessario tooprovide i valori di configurazione che consentono a un'azione di account di accesso di Microsoft Flow tooperform PowerApps.

Questa sezione vengono descritti i tipi di autenticazione hello supportate dal flusso express hello: chiave API, Azure Active Directory e generico OAuth 2.0. Per un elenco completo di provider e ogni istanza richiede le credenziali di hello, vedere [registrare e utilizzare i connettori personalizzati in PowerApps] e [registrare e utilizzare i connettori personalizzati in Microsoft Flow].

### <a name="api-key"></a>Chiave API
Quando viene utilizzato questo schema di sicurezza, gli utenti di hello del connettore saranno chiave hello tooprovide richiesta durante la creazione di una connessione. È possibile fornire un toohelp nome chiave API che li sapere quale chiave è necessaria. Per le funzioni di Azure, ciò corrisponderà in genere una delle chiavi di host hello, che coprono diverse funzioni all'interno di app di funzione hello.

### <a name="azure-active-directory"></a>Azure Active Directory
Quando si configura un connettore personalizzato che richiede account di accesso AAD, sono necessari due registrazioni del applicazione AAD: un'API di back-end hello toomodel e un connettore di hello toomodel PowerApps e del flusso.

L'API deve essere toowork configurata con la registrazione del primo hello e questo verrà già essere preso in considerazione se è stato utilizzato hello [autenticazione/autorizzazione del servizio App](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) funzionalità.

Sarà necessario toomanually creare hello registrazione secondo per il connettore di hello, attenendosi alla procedura hello analizzata in [aggiunta di un'applicazione AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Hello registrazione necessita toohave delegato accesso tooyour API e un URL di risposta `https://msmanaged-na.consent.azure-apim.net/redirect`. Vedere [in questo esempio](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) per maggiori dettagli, sostituendo l'API per hello Azure Resource Manager.

Hello seguente i valori di configurazione è necessario:
- **ID client** -hello client ID del connettore registrazione in AAD
- **Segreto client** -segreto client hello del connettore registrazione in AAD
- **URL di accesso** : hello URL di base per AAD. In Azure pubblico questo URL è in genere `https://login.windows.net`.
- **ID tenant** -hello ID di hello tenant toobe usata per l'accesso hello. Questo deve essere "common" oppure hello ID del tenant hello in cui hello connettore viene creato.
- **URL della risorsa** -hello URL della risorsa della registrazione del AAD API back-end

> [!IMPORTANT]
> Se un altro individuo importeranno definizione hello API in PowerApps e Microsoft Flow come parte del flusso di hello manuale, occorrerà tooprovide con chiave privata client e l'ID client hello **di registrazione del connettore hello**, nonché come URL della risorsa hello dell'API. Assicurarsi che questi segreti siano gestiti in modo sicuro. **Non condividere le credenziali di sicurezza hello di hello stessa interfaccia API.**

### <a name="generic-oauth-20"></a>OAuth 2.0 generica
supporto per OAuth 2.0 generico Hello consente toointegrate con qualsiasi provider OAuth 2.0. In questo modo si toobring qualsiasi provider personalizzati che non è supportato in modo nativo.

Hello seguente i valori di configurazione è necessario:
- **ID client** -hello ID client OAuth 2.0
- **Segreto client** -segreto client hello OAuth 2.0
- **Autorizzazione URL** -hello URL di autorizzazione OAuth 2.0
- **Token URL** -hello URL token OAuth 2.0
- **Aggiorna URL** -hello URL di aggiornamento OAuth 2.0



[registrare e utilizzare i connettori personalizzati in PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registrare e utilizzare i connettori personalizzati in Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
