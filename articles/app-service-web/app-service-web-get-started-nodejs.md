---
title: aaaCreate un'app web Node.js in Azure | Documenti Microsoft
description: Distribuire la prima app Node.js Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Creare un'app Web Node.js in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.  Questa Guida introduttiva viene illustrato come toodeploy un tooAzure app Node.js App Web. Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si usa Git toodeploy esempio Node.js codice toohello web app.

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux. Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Prerequisiti

toocomplete questa Guida rapida:

* [Installare Git](https://git-scm.com/)
* [Installare Node.js e NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Scaricare l'esempio hello

In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.

Spostarsi nella directory toohello che contiene il codice di esempio hello.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Eseguire app hello in locale

Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `npm start` hello toolaunch script compilato nel server Node.js HTTP.

```bash
npm start
```

Aprire un web browser e passare l'app di esempio toohello in http://localhost:1337.

Vedrai hello **Hello World** messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.

![App di esempio in esecuzione in locale](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

È stata creata una nuova app Web vuota in Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Esplorare app toohello

Sfoglia toohello distribuito l'applicazione tramite il web browser.

```bash
http://<app_name>.azurewebsites.net
```

codice di esempio Node.js Hello è in esecuzione in un'applicazione web di servizio App di Azure.

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Congratulazioni.** Il primo tooApp di app Node.js servizio distribuiti.

## <a name="update-and-redeploy-hello-code"></a>Aggiornare e ridistribuire codice hello

Utilizzando un editor di testo, aprire hello `index.js` file nell'app Node.js hello e consente di applicare una piccola modifica toohello testo nella chiamata di hello troppo`response.end`:

```nodejs
response.end("Hello Azure!");
```

Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.

```bash
git commit -am "updated output"
git push azure master
```

Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello **Sfoglia toohello app** passaggio e fare clic su Aggiorna.

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gestire la nuova app Web di Azure

Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app. 

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menu a sinistra di Hello fornisce diverse pagine di configurazione app. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Node.js con MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
