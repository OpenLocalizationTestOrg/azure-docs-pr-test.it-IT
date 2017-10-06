---
title: aaaCreate ASP.NET web app in Azure | Documenti Microsoft
description: Informazioni su come le app web di toorun distribuendo predefinito hello ASP.NET in Azure App Service app web.
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Creare un'app Web ASP.NET in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.  Questa Guida introduttiva viene illustrato come toodeploy prima ASP.NET web app tooAzure App Web. Al termine della procedura si avrà un gruppo di risorse costituito da un piano di servizio App e da un'app Web di Azure con un'applicazione Web distribuita.

Guardare video toosee di hello questa Guida introduttiva nell'azione e quindi seguire hello passaggi manualmente toopublish della prima applicazione .NET in Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

* Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello carichi di lavoro seguente:
    - **Sviluppo Web e ASP.NET**
    - **Sviluppo di Azure**

    ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Creare un'app Web ASP.NET

In Visual Studio creare un progetto selezionando **File > Nuovo > Progetto**. 

In hello **nuovo progetto** finestra di dialogo Seleziona **Visual c# > Web > applicazione Web ASP.NET (.NET Framework)**.

Nome di un'applicazione hello _myFirstAzureWebApp_, quindi selezionare **OK**.
   
![Finestra di dialogo Nuovo progetto](./media/app-service-web-get-started-dotnet/new-project.png)

È possibile distribuire qualsiasi tipo di tooAzure di app web ASP.NET. Per questa Guida rapida, selezionare hello **MVC** , modello e assicurarsi che l'autenticazione è impostata troppo**Nessuna autenticazione**.
      
Selezionare **OK**.

![Finestra di dialogo Nuovo progetto ASP.NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Scegliere dal menu hello **Debug > Avvia senza eseguire debug** toorun hello web app localmente.

![Eseguire l'app in locale](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Pubblicare tooAzure

In hello **Esplora**, hello rapida **myFirstAzureWebApp** del progetto e selezionare **pubblica**.

![Pubblicare da Esplora soluzioni](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Verificare che **Servizio app di Microsoft Azure** sia selezionato e scegliere **Pubblica**.

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Verrà visualizzata hello **Crea servizio App** finestra di dialogo che consente di creare tutti hello necessarie risorse di Azure toorun hello app web ASP.NET in Azure.

## <a name="sign-in-tooazure"></a>Accedi tooAzure

In hello **Crea servizio App** finestra di dialogo Seleziona **aggiungere un account**ed eseguire l'accesso tooyour sottoscrizione di Azure. Se hai già effettuato l'accesso, account selezionare hello contenente hello desiderato sottoscrizione dall'elenco a discesa hello.

> [!NOTE]
> Se si è già connessi, non selezionare ancora l'opzione **Crea**.
>
>
   
![Accedi tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Avanti troppo**gruppo di risorse**selezionare **New**.

Nome gruppo di risorse hello **myResourceGroup** e selezionare **OK**.

## <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Avanti troppo**piano di servizio App**selezionare **New**. 

In hello **configurare il piano di servizio App** finestra di dialogo, utilizza le impostazioni di hello nella tabella hello hello schermata seguente.

![Creare un piano di servizio app](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Impostazione | Valore consigliato | Descrizione |
|-|-|-|
|Piano di servizio app| myAppServicePlan | Nome del piano di servizio App hello. |
| Percorso | Europa occidentale | Hello Data Center in cui è ospitato app web hello. |
| Dimensione | Gratuito | [Piano tariffario](https://azure.microsoft.com/pricing/details/app-service/) che determina le funzionalità di hosting. |

Selezionare **OK**.

## <a name="create-and-publish-hello-web-app"></a>Creare e pubblicare app web hello

In **nome dell'applicazione Web**, digitare un nome univoco dell'app (i caratteri validi sono `a-z`, `0-9`, e `-`), o accettare hello generato automaticamente un nome univoco. l'URL dell'app web hello Hello è `http://<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'applicazione web.

Selezionare **crea** toostart creazione hello risorse di Azure.

![Configurare il nome dell'app Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

Una volta completata la procedura guidata hello, pubblica tooAzure di app web ASP.NET hello e quindi avvia hello app nel browser predefinito hello.

![App Web ASP.NET pubblicata in Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

nome dell'applicazione web Hello specificato in hello [creare e pubblicare passaggio](#create-and-publish-the-web-app) viene utilizzato come prefisso di URL in formato hello hello `http://<app_name>.azurewebsites.net`.

L'app Web ASP.NET è ora in esecuzione nel servizio app di Azure.

## <a name="update-hello-app-and-redeploy"></a>Ridistribuzione e l'applicazione hello aggiornamento

Da hello **Esplora**aprire _Views\Home\Index.cshtml_.

Trovare hello `<div class="jumbotron">` HTML tag superiore hello e sostituire l'intero elemento hello con hello seguente codice:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, hello rapida **myFirstAzureWebApp** nel progetto **Esplora** e selezionare **pubblica**.

Pagina pubblica hello, selezionare **pubblica**.

Al termine del processo di pubblicazione, Visual Studio avvia un browser toohello URL hello web app.

![App Web ASP.NET aggiornata in Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Gestire app web di Azure hello

Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app.

Scegliere dal menu a sinistra hello **servizi App**, quindi selezionare il nome di hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-dotnet/access-portal.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app. 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

menu a sinistra di Hello fornisce diverse pagine di configurazione app. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [ASP.NET con database SQL](app-service-web-tutorial-dotnet-sqldatabase.md)
