---
title: un'app di WordPress nel portale di Azure in cinque minuti hello aaaDeploy | Documenti Microsoft
description: "Informazioni su come è facile toorun App web nel servizio App distribuendo un'applicazione WordPress. Visualizzare i risultati immediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Distribuire un'app di WordPress nel portale di Azure hello in cinque minuti

In questa esercitazione illustra come toodeploy il primo [WordPress](https://wordpress.org/) app web troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuti.

![Sito WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Prerequisiti
È necessario un account Microsoft Azure. Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure. Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Distribuire app WordPress hello
1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Aprire [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Questo collegamento è un tooimmediately di scelta rapida configurare una nuova app di WordPress in hello portale di Azure.

3. In **Nome app**, digitare un nome per l'App Web. Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `azurewebsites.net` dominio.
   
5. In **gruppo di risorse**, fare clic su **Crea nuovo** toocreate un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), assegnargli un nome.

6. In **Provider di database** selezionare **CleaDB**.

7. Fare clic su **Piano di servizio app/Località** > **Crea nuovo**. Configurare hello [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:

    - In **piano di servizio App**, il nome di tipo hello desiderato.
    - In **percorso**, scegliere un percorso toohost il piano.
    - Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.
    - Fare clic su **OK**.

8. Fare clic su **Database** > **Creare nuovo**. Configurare hello Database SQL, come illustrato:

    - In **Nome database** digitare un nome per il database. 
    - In **percorso**, scegliere hello stesso percorso hello piano di servizio App.
    - Fare clic su **Piano tariffario**, quindi selezionare **Mercurio** o un altro livello adatto e fare clic su **Seleziona**.
    - Fare clic su **Note legali** e quindi su **Acquista**.
    - Fare clic su **OK**.

9. Fare clic su **Crea**.

    A questo punto, Azure crea l'app di WordPress in base alla configurazione. Verrà visualizzata la notifica **La distribuzione è stata avviata...**.

    ![Distribuzione avviata, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Avviare e gestire l'app Web WordPress

Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.

![Distribuzione riuscita, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Fare clic sulla notifica hello. Se non viene individuato, è sempre possibile accedervi facendo clic sul controllo del segnale acustico notifica hello (![di sotto di notifica - primo WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'app Web (*pannello*: una pagina del portale visualizzata in orizzontale).

3. Nella parte superiore di hello della pagina di panoramica hello, fare clic su **Sfoglia**.
   
    ![Sfoglia, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/browse.png)

    Ora vengono visualizzate hello WordPress **iniziale** pagina. Configurare l'installazione WordPress hello e avviare la riproduzione con esso.

    ![Configurazione di WordPress, la prima app di WordPress nel Servizio app di Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Passaggi successivi
* [Creare, configurare e distribuire un tooAzure di app web Laravel](app-service-web-php-get-started.md) -acquisire le competenze di base hello è necessario toorun qualsiasi applicazione web PHP in Azure, ad esempio:

    * Creare e configurare app in Azure da PowerShell/Bash.
    * Impostare la versione di PHP.
    * Utilizzare un file di avvio che non è presente nella directory dell'applicazione hello radice.
    * Abilitare l'automazione Composer.
    * Accedere a variabili specifiche dell'ambiente.
    * Risolvere i problemi comuni.

* [Distribuire il servizio App di tooAzure codice](web-sites-deploy.md)-informazioni su come toodeploy da FTP o da origine controllare repository.
* [Aggiungere app web prima di funzionalità tooyour](app-service-web-get-started-2.md) -richiedere toohello l'applicazione Azure che successivamente livello. autenticare gli utenti, ridimensionare l'app in base alla richiesta e configurare alcuni avvisi sulle prestazioni, tutto con pochi clic.
