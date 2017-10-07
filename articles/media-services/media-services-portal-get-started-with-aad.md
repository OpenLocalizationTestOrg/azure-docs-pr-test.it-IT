---
title: aaaGet avviato con l'autenticazione di Azure AD con hello portale di Azure | Documenti Microsoft
description: Informazioni su come toouse hello Azure tooaccess portale Azure Active Directory (Azure AD) autenticazione tooconsume hello API di servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Introduzione all'autenticazione di Azure AD tramite hello portale di Azure

Informazioni su come toouse hello Azure tooaccess portale Azure Active Directory (Azure AD) autenticazione tooaccess hello API di servizi multimediali di Azure.

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Account di Servizi multimediali. Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).
- Verificare hello [accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AD Azure](media-services-use-aad-auth-to-access-ams-api.md). 

Quando si usa l'autenticazione di Azure AD con Servizi multimediali di Azure, sono disponibili due opzioni di autenticazione:

- **Autenticazione utente**. Eseguire l'autenticazione di una persona che utilizza hello app toointeract con risorse di servizi multimediali. applicazione interattiva Hello deve prima richiedere le credenziali utente hello. Un esempio è un'applicazione console di gestione usata dai processi di codifica toomonitor gli utenti autorizzati o streaming live. 
- **Autenticazione basata su entità servizio**. Consente di autenticare un servizio. Le applicazioni che solitamente usano questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati, ad esempio App Web, app per le funzioni, app per la logica, API o microservizi.

> [!IMPORTANT]
> Attualmente servizi multimediali supporta modello di autenticazione hello Azure Access Control service. L'autorizzazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018. Si consiglia di migrare il modello di autenticazione di Azure AD toohello appena possibile.

## <a name="select-hello-authentication-method"></a>Selezionare il metodo di autenticazione hello

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali.
2. Selezionare come tooconnect toohello API di servizi multimediali.

    ![Selezionare la pagina del metodo di connessione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Autenticazione utente

tooconnect toohello API di servizi multimediali usando hello opzione di autenticazione utente, app client hello deve toorequest un token di Azure AD che ha hello seguenti parametri:  

* Endpoint del tenant di Azure AD
* URI di risorsa di Servizi multimediali
* ID client dell'applicazione Servizi multimediali (nativa) 
* URI di reindirizzamento dell'applicazione Servizi multimediali (nativa) 
* URI di risorsa per Servizi multimediali REST

È possibile ottenere i valori hello per questi parametri in hello **API dei servizi multimediali con l'autenticazione utente** pagina. 

![Connettersi con la pagina di autenticazione utente](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Se ci si connette toohello API di servizi multimediali con Media Services Microsoft .NET SDK hello, hello necessari valori tooyou disponibile come parte di hello SDK. Per ulteriori informazioni, vedere [usano Azure AD authentication tooaccess hello API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md).

Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di Azure AD utilizzando i parametri di hello descritti in precedenza. Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Autenticazione di un'entità servizio

tooconnect toohello API di servizi multimediali usando hello opzione dell'entità servizio, l'applicazione di livello intermedio (API web o applicazione web) deve toorequest un token di Azure AD che ha hello seguenti parametri:  

* Endpoint del tenant di Azure AD
* URI di risorsa di Servizi multimediali 
* URI di risorsa per Servizi multimediali REST
* I valori dell'applicazione Azure AD: hello **ID client** e **segreto client**

È possibile ottenere i valori hello per questi parametri in hello **connettersi tooMedia API dei servizi con un'entità servizio** pagina. Utilizzare questo toocreate pagina Azure un nuova applicazione AD o tooselect uno esistente. Dopo aver selezionato hello Azure AD app, è possibile ottenere l'ID client hello (ID applicazione) e generare i valori di hello client secret (chiave). 

![Connettersi alla pagina entità servizio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Quando hello **dell'entità servizio** pannello viene aperto, è selezionata l'applicazione Azure AD prima hello che soddisfi i seguenti criteri hello:

- Si tratta di un'applicazione Azure AD registrata.
- Disponga di autorizzazioni di collaboratore o il controllo di accesso Owner Role-Based account hello.

Dopo aver creato o selezionare un'app di Azure AD, è possibile creare un segreto client (chiave) e copiare hello ID client (ID applicazione). ID client e il segreto client Hello sono token di accesso obbligatorio tooget hello in questo scenario.

Se non si dispone delle autorizzazioni app di Azure AD toocreate nel dominio, non vengono visualizzati i controlli app di Azure AD hello del pannello hello e viene visualizzato un messaggio di avviso.

Se ci si connette toohello API di servizi multimediali con Media Services .NET SDK hello, vedere [usano Azure AD authentication tooaccess hello API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md).

Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di Azure AD utilizzando parametri hello descritti in precedenza. Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Ottenere il client di hello ID e client secret

Dopo aver selezionato un'app di Azure AD esistente o hello selezionare opzione toocreate uno nuovo, verrà visualizzato hello seguenti pulsanti:

![Pulsante Gestisci autorizzazioni e pulsante Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

hello tooopen pannello applicazione Azure AD, fare clic su **Gestisci applicazione**. In hello **Gestisci applicazione** pannello, è possibile ottenere l'ID client dell'applicazione hello (ID applicazione). un segreto client (chiave), seleziona toogenerate **chiavi**.

![Opzione Chiavi del pannello Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Gestire le autorizzazioni e l'applicazione hello

Dopo aver selezionato un'applicazione hello Azure AD, è possibile gestire le autorizzazioni e l'applicazione hello. tooset backup il tooaccess applicazione Azure AD altre applicazioni, fare clic su **gestire le autorizzazioni**. Per le attività di gestione, ad esempio la modifica di chiavi e gli URL di risposta o il manifesto dell'applicazione hello tooedit, fare clic su **Gestisci applicazione**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Modificare le impostazioni dell'applicazione hello o manifesto

le impostazioni dell'applicazione hello tooedit o manifesto, fare clic su **Gestisci applicazione**.

![Pagina Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Passaggi successivi

Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).
