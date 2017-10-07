---
title: un'App Ruby con le app Web in Linux aaaCreate | Documenti Microsoft
description: Informazioni su toocreate Ruby App con del sito web di Azure in Linux.
keywords: servizio app di azure, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Creare un'app Ruby con le App Web in Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa Guida introduttiva viene illustrato come una base Ruby sull'applicazione Guide toocreate quindi distribuirlo tooAzure come un'App Web in Linux.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Prerequisiti

* [Ruby 2.4.1 o versione successiva](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Una [sottoscrizione di Azure attiva](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Scaricare l'esempio hello

In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale

Eseguire il server di guide hello affinché toowork applicazione hello. Modificare toohello *hello world* directory e hello `rails server` comando Avvia hello server.

```bash
cd hello-world\bin
rails server
```
    
Tramite il browser, passare troppo`http://localhost:3000` app di hello tootest localmente.  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Modifica messaggio di benvenuto toodisplay app

Modificare un'applicazione hello in modo da visualizzare un messaggio di benvenuto. Modificare il controller dell'applicazione hello in modo che restituisca il messaggio hello come browser toohello HTML. 

Aprire *~/workspace/hello-world/app/controllers/application_controller.rb* per la modifica. Modificare hello `ApplicationController` toolook classe come hello nell'esempio di codice seguente:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Ora l'app è configurata. Tramite il browser, passare troppo`http://localhost:3000` pagina di destinazione tooconfirm hello radice.

![Hello World configurato](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Creare una app web Ruby in Azure

Hello utilizzare [crea piano di servizio App az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate un piano di servizio app per l'app web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Eseguire quindi hello [az webapp creare](https://docs.microsoft.com/cli/azure/webapp) comando toocreate hello web app che utilizza il piano di servizio hello appena creato. Si noti che runtime hello è impostato troppo`ruby|2.3`. Non dimenticare tooreplace `<app name>` con un nome univoco dell'app.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Una volta creato l'app web hello, un **Panoramica** pagina è disponibile tooview. Passare tooit. viene visualizzato dopo la pagina iniziale di Hello:

![Pagina iniziale](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Distribuire l'applicazione

Usare Git toodeploy hello applicazione Ruby tooAzure. app web Hello dispone già di una distribuzione Git configurata. È possibile recuperare l'URL di distribuzione hello generando un [distribuzione webapp az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Si noti che l'URL Git hello sono hello modulo basato sul nome dell'app web seguenti:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Eseguire hello seguenti comandi toodeploy hello applicazione locale tooyour sito Web di Azure:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Verificare che le operazioni di distribuzione remoto hello segnalano l'esito positivo. Hello comandi producono output simili toohello seguente testo:

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Una volta completata la distribuzione di hello, riavviare l'app web per effetto di hello distribuzione tootake utilizzando hello [riavvio webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) comando, come illustrato di seguito:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Passare tooyour sito e verificare i risultati di hello.

```bash
http://<your web app name>.azurewebsites.net
```
![app Web aggiornata](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Durante l'applicazione hello è il riavvio, il tentativo di toobrowse hello del sito genera un codice di stato HTTP `Error 503 Server unavailable`. Potrebbe richiedere alcuni minuti toofully riavvio.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Passaggi successivi

[Domande frequenti su App Web del Servizio app di Azure su Linux](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)