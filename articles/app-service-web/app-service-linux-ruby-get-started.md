---
title: Creare un'app Ruby con le App Web in Linux | Microsoft Docs
description: Informazioni su come creare app Ruby con app web in Linux.
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
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Creare un'app Ruby con le App Web in Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. In questa guida introduttiva viene illustrato come creare un'applicazione Ruby on Rails di base e quindi distribuirla in App Web di Azure in Linux.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Prerequisiti

* [Ruby 2.4.1 o versione successiva](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Una [sottoscrizione di Azure attiva](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a>Scaricare l'esempio

In una finestra del terminale eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a>Eseguire l'applicazione in locale

Eseguire il server della barra di scorrimento per il funzionamento dell'applicazione. Passare alla directory *hello-world* e il comando `rails server` avvia il server.

```bash
cd hello-world\bin
rails server
```
    
Tramite il Web browser, passare a `http://localhost:3000` per testare l'app in locale.    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a>Modificare l'app per visualizzare il messaggio di benvenuto

Modificare l'applicazione in modo da visualizzare un messaggio di benvenuto. Modificare il controller dell'applicazione in modo che restituisca il messaggio in formato HTML nel browser. 

Aprire *~/workspace/hello-world/app/controllers/application_controller.rb* per la modifica. Modificare la classe `ApplicationController` per avere l'aspetto dell'esempio di codice seguente:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Ora l'app è configurata. Tramite il Web browser, passare a `http://localhost:3000` per confermare la pagina di destinazione principale.

![Hello World configurato](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Creare una app web Ruby in Azure

Usare il comando [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) per creare un piano di servizio app per l'app web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Eseguire quindi il comando [az webapp create](https://docs.microsoft.com/cli/azure/webapp) per creare l'app web che usa il piano di servizio appena creato. Si noti che il runtime è impostato su `ruby|2.3`. Non dimenticare di sostituire `<app name>` con un nome univoco dell'app.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Una volta creato l'app web, è disponibile una pagina **Panoramica** per la visualizzazione. Passare ad essa. Viene visualizzata la pagina iniziale seguente:

![Pagina iniziale](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Distribuire l'applicazione

Usare Git per distribuire l'applicazione Ruby in Azure. La app web ha già una distribuzione Git configurata. È possibile recuperare l'URL di distribuzione tramite l'emissione di un comando [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment).  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Si noti che l'URL Git ha il formato seguente, in base al nome dell'app Web:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Eseguire i comandi seguenti per distribuire l'applicazione locale al sito Web di Azure:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Verificare che per le operazioni di distribuzione in remoto venga segnalato l'esito positivo. I comandi generano un output simile al testo seguente:

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Dopo aver completato la distribuzione, riavviare l'app Web affinché la distribuzione venga applicata tramite il comando [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), come mostrato di seguito:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Passare al sito e verificare i risultati.

```bash
http://<your web app name>.azurewebsites.net
```
![app Web aggiornata](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Mentre l'app viene riavviata, il tentativo di aprire il sito genera un codice di stato HTTP `Error 503 Server unavailable`. Il completamento del riavvio potrebbe richiedere alcuni minuti.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Passaggi successivi

[Domande frequenti su App Web del Servizio app di Azure su Linux](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)