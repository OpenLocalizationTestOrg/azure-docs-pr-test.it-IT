---
title: aaaCreate della prima applicazione web Java in Azure
description: Informazioni su come toorun app nel servizio App web tramite la distribuzione di un'applicazione Java di base.
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Creare la prima app Web Java in Azure

Hello [App Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funzionalità di [Azure App Service](../app-service/app-service-value-prop-what-is.md) fornisce un servizio di hosting web scalabile, applicazione automatica di patch. Questa Guida introduttiva viene illustrato come un linguaggio toodeploy web app tooApp servizio utilizzando hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).

![App Web di esempio "Hello Azure" app Web di esempio](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa Guida rapida, installare:

* Hello libero [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/). In questa guida introduttiva viene usato Eclipse Neon.
* Hello [Azure Toolkit per Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Creare un progetto Web dinamico in Eclipse

In Eclipse selezionare **File** > **Nuovo** > **Dynamic Web Project** (Progetto Web dinamico).

In hello **nuovo progetto Web dinamico** della finestra di dialogo progetto hello nome **MyFirstJavaOnAzureWebApp**e selezionare **fine**.
   
![Finestra di dialogo New Dynamic Web Project (Nuovo progetto Web dinamico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Aggiungere una pagina JSP

Se Esplora progetti non viene visualizzato, è necessario ripristinarlo.

![Area di lavoro Java EE per Eclipse](./media/app-service-web-get-started-java/pe.png)

In Esplora progetti espandere hello **MyFirstJavaOnAzureWebApp** progetto.
Fare doppio clic su **WebContent** e quindi selezionare **Nuovo** > **JSP File** (File JSP).

![Menu per un nuovo file JSP in Esplora progetti](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

In hello **New JSP File** la finestra di dialogo:

* File con nome hello **index.jsp**.
* Selezionare **Fine**.

  ![Finestra di dialogo New JSP File (Nuovo file JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

Nel file index.jsp hello sostituire hello `<body></body>` elemento con hello markup seguente:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Salvare le modifiche di hello.

## <a name="publish-hello-web-app-tooazure"></a>Pubblicare hello web app tooAzure

In Esplora progetti, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come App Web di Azure**.

![Menu di scelta rapida Publish as Azure Web App (Pubblica come app Web di Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

In hello **Azure Accedi** della finestra di dialogo keep hello **Interactive** opzione e quindi selezionare **Accedi**.

Istruzioni hello Accedi.

### <a name="deploy-web-app-dialog-box"></a>Finestra di dialogo Distribuisci app Web

Dopo avere effettuato l'accesso in tooyour account Azure, hello **distribuire App Web** viene visualizzata la finestra di dialogo.

Selezionare **Crea**.

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Finestra di dialogo Crea servizio app

Hello **Crea servizio App** viene visualizzata la finestra di dialogo con i valori predefiniti. numero di Hello **170602185241** illustrato nella seguente hello immagine è diversa nella finestra di dialogo.

![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/cas1.png)

In hello **Crea servizio App** la finestra di dialogo:

* Mantenere il nome di hello generato per l'app web hello. Il nome deve essere univoco in Azure nome Hello è parte dell'indirizzo URL hello hello web app. Ad esempio: se il nome dell'app web hello è **MyJavaWebApp**, hello URL *myjavawebapp.azurewebsites.net*.
* Mantenere contenitore web predefinito di hello.
* Selezionare una sottoscrizione di Azure.
* In hello **piano di servizio App** scheda:

  * **Creare nuovi**: mantenere il valore predefinito hello, ovvero nome hello del piano di servizio App hello.
  * **Località**: selezionare **Europa occidentale** o un'area geografica nelle vicinanze.
  * **Piano tariffario**: selezionare hello opzione disponibile. Per le funzionalità, vedere [Prezzi di Servizio app](https://azure.microsoft.com/pricing/details/app-service/).

   ![Finestra di dialogo Crea servizio app](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Scheda Gruppo di risorse

Seleziona hello **gruppo di risorse** scheda. Mantenere il valore predefinito generato hello per il gruppo di risorse hello.

![Scheda Gruppo di risorse](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Selezionare **Crea**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello Azure Toolkit crea app web hello e visualizza una finestra di dialogo di stato di avanzamento.

![Finestra di dialogo di avanzamento Crea servizio app](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Finestra di dialogo Distribuisci app Web

In hello **distribuire App Web** nella finestra di dialogo **distribuire tooroot**. Se si dispone di un servizio app *wingtiptoys.azurewebsites.net* e non si distribuisce toohello radice, app web hello denominata **MyFirstJavaOnAzureWebApp** viene distribuito troppo *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Finestra di dialogo Distribuisci app Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

Hello della finestra di dialogo Mostra hello Azure JDK e le selezioni di contenitore di web.

Selezionare **Distribuisci** toopublish hello web app tooAzure.

Al termine della pubblicazione hello, selezionare hello **pubblicato** collegamento hello **Log attività Azure** la finestra di dialogo.

![Finestra di dialogo Log attività di Azure](./media/app-service-web-get-started-java/aal.png)

Congratulazioni. È stata distribuita la tooAzure app web. 

![App Web di esempio "Hello Azure" app Web di esempio](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Aggiornare l'app web hello

Modifica hello esempio JSP codice tooa messaggi diversi.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Salvare le modifiche di hello.

In Esplora progetti, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come App Web di Azure**.

Hello **distribuire App Web** viene visualizzata la finestra di dialogo e Mostra hello servizio app creata in precedenza. 

> [!NOTE]
> Selezionare **distribuire tooroot** ogni volta che si esegue la pubblicazione.
>

Selezionare l'app web hello e selezionare **Distribuisci**, che vengono pubblicate modifiche hello.

Quando hello **pubblicazione** collegamento viene visualizzato, selezionarlo toobrowse toohello web app e visualizzare le modifiche di hello.

## <a name="manage-hello-web-app"></a>Gestire app web hello

Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toosee hello web app a cui è stato creato.

Scegliere dal menu a sinistra hello **gruppi di risorse**.

![Gruppi di navigazione del portale tooresource](media/app-service-web-get-started-java/rg.png)

Selezionare il gruppo di risorse hello. pagina Hello Mostra risorse hello creati in questa Guida rapida.

![Gruppo di risorse myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Selezionare hello web app (**webapp 170602193915** in hello prima immagine).

Hello **Panoramica** verrà visualizzata la pagina. Questa pagina offre una visualizzazione di svolgimento app hello. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app. schede di Hello sul lato sinistro di hello della pagina hello mostrano hello diverse configurazioni che è possibile aprire. 

![Pagina del servizio app nel portale di Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire il mapping di un dominio personalizzato](app-service-web-tutorial-custom-domain.md)
