---
title: aaaCreate un'app web Python in Azure | Documenti Microsoft
description: Distribuire la prima app Python Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a>Creare un'app Web Python in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.  Questa Guida rapida illustra in dettaglio come toodevelop e distribuire un tooAzure app Python App Web. Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si usa Git toodeploy esempio Python codice toohello web app.

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux. Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.
## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

1. [Installare Git](https://git-scm.com/)
1. [Installare Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Scaricare l'esempio hello

In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.

Spostarsi nella directory toohello che contiene il codice di esempio hello.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Eseguire app hello in locale

Installare i pacchetti hello necessario utilizzando `pip`.

```bash
pip install -r requirements.txt
```

Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `Python` comando toolaunch hello Python server web predefinito.

```bash
python main.py
```

Aprire un web browser e passare l'app di esempio toohello all'indirizzo http://localhost:5000/.

È possibile visualizzare hello **Hello World** messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.

![App di esempio in esecuzione in locale](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-python/app-service-web-service-created.png)

È stata creata una nuova app Web vuota in Azure.

## <a name="configure-toouse-python"></a>Configurare toouse Python

Hello utilizzare [az webapp config set](/cli/azure/webapp/config#set) versione di Python di comando tooconfigure hello web app toouse `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


L'impostazione di tale versione di Python hello utilizza un contenitore predefinito fornito dalla piattaforma hello. toouse contenitore, vedere hello riferimento CLI per hello [az webapp configurazione contenitore set](/cli/azure/webapp/config/container#set) comando.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Esplorare app toohello

Sfoglia toohello distribuito l'applicazione tramite il web browser.

```bash
http://<app_name>.azurewebsites.net
```

esempio di codice Python Hello è in esecuzione in un'applicazione web di servizio App di Azure.

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Congratulazioni.** Il primo tooApp di app Python servizio distribuiti.

## <a name="update-and-redeploy-hello-code"></a>Aggiornare e ridistribuire codice hello

Utilizzare un editor di testo locale, aprire hello `main.py` file nell'app Python hello e verificare un toohello di modifica di piccole dimensioni toohello testo successivo `return` istruzione:

```python
return 'Hello, Azure!'
```

Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.

```bash
git commit -am "updated output"
git push azure master
```

Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello [Sfoglia toohello app](#browse-to-the-app) passaggio e aggiornare la pagina hello.

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [Python con PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
