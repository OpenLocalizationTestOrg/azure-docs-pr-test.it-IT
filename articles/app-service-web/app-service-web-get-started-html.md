---
title: app web aaaCreate HTML statico in Azure | Documenti Microsoft
description: Informazioni su come le app web toorun in Azure App Service distribuendo un HTML statico app di esempio.
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Creare un'app Web HTML statica in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.  Questa Guida rapida illustra toodeploy HTML + CSS base dei siti tooAzure Web App. Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si utilizza Git toodeploy app web di esempio HTML toohello contenuto.

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux. Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa Guida rapida:

- [Installare Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Scaricare l'esempio hello

In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.

## <a name="view-hello-html"></a>Visualizzare hello HTML

Passare toohello directory che contiene l'esempio hello HTML. Aprire hello *index.html* file nel browser.

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-html/app-service-web-service-created.png)

È stata creata una nuova app Web vuota in Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Esplorare app toohello

In un browser, passare l'URL dell'app web di Azure toohello:

```
http://<app_name>.azurewebsites.net
```

pagina Hello è in esecuzione come un'app web di servizio App di Azure.

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Congratulazioni.** È stato distribuito il primo tooApp di app HTML del servizio.

## <a name="update-and-redeploy-hello-app"></a>Aggiornare e ridistribuire l'applicazione hello

Aprire hello *index.html* file in un editor di testo e verificare un markup toohello di modifica. Ad esempio, modificare l'intestazione H1 hello da "Azure App Service – esempio sito HTML statico" toojust "servizio App di Azure'.

Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.

```bash
git commit -am "updated HTML"
git push azure master
```

Una volta completata la distribuzione, aggiornare le modifiche di hello toosee browser.

![Home page dell'app di esempio aggiornata](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Gestire la nuova app Web di Azure

Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-html/portal1.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app. 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-html/portal2.png)

menu a sinistra di Hello fornisce diverse pagine di configurazione app. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire il mapping di un dominio personalizzato](app-service-web-tutorial-custom-domain.md)
