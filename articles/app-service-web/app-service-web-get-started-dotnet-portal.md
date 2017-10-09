---
title: un'app web Umbraco nel portale di Azure in cinque minuti hello aaaDeploy | Documenti Microsoft
description: "Informazioni su come è facile toorun App web nel servizio App distribuendo un'applicazione ASP.NET di esempio. Visualizzare i risultati immediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Distribuire un'app web Umbraco nel portale di Azure hello in cinque minuti

In questa esercitazione consente di distribuire n [Umbraco](https://our.umbraco.org/) app web troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuti.

![App Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Prerequisiti
È necessario un account Microsoft Azure. Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure. Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Distribuire l'applicazione ASP.NET hello
1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Aprire [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    Questo collegamento è un tooimmediately di scelta rapida configurare una nuova app Umbraco hello portale di Azure.

3. In **Nome app**, digitare un nome per l'App Web. Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `azurewebsites.net` dominio.
   
5. In **gruppo di risorse**, fare clic su **Crea nuovo** toocreate un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), assegnargli un nome.

7. Fare clic su **Piano di servizio app/Località** > **Crea nuovo**. Configurare hello [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:

    - In **piano di servizio App**, il nome di tipo hello desiderato.
    - In **percorso**, scegliere un percorso toohost il piano.
    - Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.
    - Fare clic su **OK**.

    La configurazione di Umbraco CMS sarà ora simile hello seguente schermata:

    ![Configurazione in corso: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Fare clic su **Database SQL** > **Crea un nuovo database**. Configurare hello Database SQL, come illustrato:

    - In **Nome** digitare un nome, ad esempio **myDB**.
    - Fare clic su **Piano tariffario**, quindi selezionare **F Free** (F gratuito) o un altro livello adatto e fare clic su **Seleziona**.
    - Fare clic su **Server di destinazione** > **Creare un nuovo server**. Configurare il server di database di hello, come illustrato:

        - In **Nome server** digitare il nome del server. Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `.database.windows.net` dominio.
        - In **account di accesso amministratore Server**, hello tipo desiderato di nome utente amministratore.
        - In **Password** e **Conferma password**, digitare la password desiderata hello.
        - Nel percorso, selezionare hello nello stesso percorso utilizzato per l'app web hello.
        - Assicurarsi che **server tooaccess di servizi di azure Consenti** è selezionata.
        - Fare clic su **Seleziona**.
    
    - Fare clic su **Seleziona**.

13. Fare clic su **impostazioni app Web**, specificare nome utente di database hello e una password e fare clic su **OK**.

    La configurazione di Umbraco CMS sarà ora simile hello seguente schermata:

    ![Configurazione completata: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Fare clic su **Crea**.
    
    A questo punto, Azure crea l'app di Umbraco in base alla configurazione. Verrà visualizzata la notifica **La distribuzione è stata avviata...**.

    ![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Avviare e gestire l'app Web Umbraco

Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.

![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Fare clic sulla notifica hello. Se non viene individuato, è sempre possibile accedervi facendo clic sul controllo del segnale acustico notifica hello (![di sotto di notifica - Umbraco prima in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'app Web (*pannello*: una pagina del portale visualizzata in orizzontale).

3. Nella parte superiore di hello della pagina di panoramica hello, fare clic su **Sfoglia**.
   
    ![Sfoglia, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Ora vengono visualizzate hello Umbraco **iniziale** pagina. Configurare l'installazione Umbraco hello e avviare la riproduzione con esso.

    ![Configurazione di Umbraco: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Passaggi successivi
* [Distribuire un tooAzure di app web ASP.NET servizio App, tramite Visual Studio](app-service-web-get-started-dotnet.md) -informazioni su come una nuova app web di Azure da Visual Studio, utilizzando uno qualsiasi dei hello toocreate inclusi modelli di applicazione.
* [Distribuire il servizio App di tooAzure codice](web-sites-deploy.md)-informazioni su come toodeploy da FTP o da origine controllare repository.
* [Aggiungere app web prima di funzionalità tooyour](app-service-web-get-started-2.md) -richiedere toohello l'applicazione Azure che successivamente livello. autenticare gli utenti, ridimensionare l'app in base alla richiesta e configurare alcuni avvisi sulle prestazioni, tutto con pochi clic.
