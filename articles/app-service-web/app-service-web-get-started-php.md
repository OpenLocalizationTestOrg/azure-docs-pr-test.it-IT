---
title: aaaCreate PHP web app in Azure | Documenti Microsoft
description: Distribuire la prima app PHP Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Creare un'app Web PHP in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.  Questa esercitazione Guida introduttiva viene illustrato come toodeploy un tooAzure app PHP App Web. Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) nella Shell di Cloud e si usa Git toodeploy esempio PHP codice toohello web app.

![App di esempio in esecuzione in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux. Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa Guida rapida:

* [Installare Git](https://git-scm.com/)
* [Installare PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Scaricare l'esempio hello in locale

In una finestra terminale, eseguire hello i comandi seguenti. Verrà Clona macchina locale tooyour hello esempio applicazione e spostarsi nel codice di esempio di toohello directory contenitore hello.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Eseguire app hello in locale

Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `php` comando toolaunch hello PHP server web predefinito.

```bash
php -S localhost:8080
```

Aprire un web browser e passare l'app di esempio toohello in http://localhost:8080.

Vedrai hello **Hello World!** messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.

![App di esempio in esecuzione in locale](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

È stata creata una nuova app Web vuota in Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>Esplorare app toohello localmente

Sfoglia toohello distribuito l'applicazione tramite il web browser.

```bash
http://<app_name>.azurewebsites.net
```

codice di esempio PHP Hello è in esecuzione in un'applicazione web di servizio App di Azure.

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Congratulazioni.** Il primo tooApp di app PHP servizio distribuiti.

## <a name="update-locally-and-redeploy-hello-code"></a>In locale e ridistribuire codice hello

Utilizzare un editor di testo locale, aprire hello `index.php` file all'interno di app PHP hello e consente di applicare un piccola modifica toohello testo all'interno di stringa hello accanto troppo`echo`:

```php
echo "Hello Azure!";
```

Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.

```bash
git commit -am "updated output"
git push azure master
```

Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello **Sfoglia toohello app** passaggio e aggiornare la pagina hello.

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gestire la nuova app Web di Azure

Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menu a sinistra di Hello fornisce diverse pagine di configurazione app. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [PHP con MySQL](app-service-web-tutorial-php-mysql.md)
