---
title: App aaaDebugging in un contenitore Docker locale | Documenti Microsoft
description: "Informazioni su come toomodify un'app è in esecuzione in un contenitore Docker locale, aggiornare il contenitore di hello mediante modifica e aggiornamento e impostare i punti di interruzione di debug"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Debug delle applicazioni in un contenitore Docker locale
## <a name="overview"></a>Panoramica
Hello Visual Studio Tools per Docker offre un modo coerente di toodevelop in e convalidare l'applicazione localmente in un contenitore Linux Docker.
Non è il contenitore di hello toorestart ogni volta che si applica un codice di modifica.
Questo articolo illustra come toouse hello "Modifica e Aggiorna" funzionalità toostart un'app Web di ASP.NET Core in un contenitore Docker locale, apportare le modifiche necessarie e quindi aggiornare hello browser toosee tali modifiche.
In questo articolo illustra anche come tooset i punti di interruzione per il debug.

> [!NOTE]
> Il supporto del contenitore di Windows sarà disponibile nelle versioni future
>
>

## <a name="prerequisites"></a>Prerequisiti
Hello seguenti strumenti deve essere installato.

* [Ultima versione di Visual Studio](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

toorun contenitori di Docker in locale, è necessario un client di docker locale.
È possibile utilizzare hello [della casella degli strumenti di Docker](https://www.docker.com/products/docker-toolbox), che richiede di Hyper-V toobe disabilitato o è possibile utilizzare [Docker per Windows](https://www.docker.com/get-docker), che utilizza la tecnologia Hyper-V e Windows 10 è necessario.

Utilizzo della casella degli strumenti di Docker, è necessario troppo[configurare hello client di Docker](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Creare un'app Web
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Aggiungere il supporto di Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Modificare il codice e aggiornarlo
tooquickly scorrere le modifiche, è possibile avviare l'applicazione in un contenitore e continuare toomake modifiche, visualizzarli come si farebbe con IIS Express.

1. Impostare hello configurazione soluzione troppo`Debug` e premere  **&lt;CTRL + F5 >** toobuild il docker immagine ed eseguirlo in locale.

    Una volta immagine contenitore hello è stata compilata e viene eseguito in un contenitore Docker, Visual Studio verrà avviato hello app Web nel browser predefinito.
    Se si utilizza browser Microsoft Edge hello o in caso contrario sono errori, vedere [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) sezione.
2. Passare toohello sulla pagina, è qui che vedremo toomake le modifiche.
3. Restituire tooVisual Studio e aprire `Views\Home\About.cshtml`.
4. Aggiungere hello successivo HTML toohello contenuto alla fine del file hello e salvare le modifiche di hello.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Visualizza finestra di output di hello, quando viene completata hello compilazione .NET e viene visualizzato di queste righe, passa indietro tooyour browser e aggiornare hello sulla pagina.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Le modifiche sono state applicate.

## <a name="4-debug-with-breakpoints"></a>4. Eseguire il debug con punti di interruzione
Spesso, le modifiche saranno necessario ulteriore ispezione, sfruttando le funzionalità di Visual Studio di debug hello.

1. Restituire tooVisual Studio e aprire`Controllers\HomeController.cs`
2. Sostituire il contenuto di hello del metodo di hello About () con il seguente hello:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Toohello un punto di interruzione a sinistra di hello set `string message`… riga.
4. Riscontri  **&lt;F5 >** toostart debug.
5. Passare toohello sulla pagina toohit il punto di interruzione.
6. Commutatore tooVisual Studio tooview hello punto di interruzione e per controllare il valore di hello del messaggio.

   ![][2]

## <a name="summary"></a>Riepilogo
Con [Visual Studio 2015 Tools per Docker](https://aka.ms/DockerToolsForVS), è possibile ottenere una produttività hello dell'utilizzo in locale, realismo produzione hello di sviluppo all'interno di un contenitore Docker.

## <a name="troubleshooting"></a>Risoluzione dei problemi
[Risoluzione dei problemi di sviluppo di Docker in Visual Studio](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Altre informazioni su Docker con Visual Studio, Windows e Azure
* [Docker Tools for Visual Studio 2015](http://aka.ms/dockertoolsforvs) : sviluppo di codice .NET Core in un contenitore
* [Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : compilare e distribuire contenitori Docker
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) : servizi di linguaggio per la modifica dei file di Docker, con altri scenari e2e presto disponibili
* [Documentazione dei contenitori di Windows](http://aka.ms/containers): informazioni su Windows Server e Nano Server
* [Servizio contenitore di Azure](https://azure.microsoft.com/services/container-service/) - [Contenuto servizio contenitore di Azure](http://aka.ms/AzureContainerService)
* Per ulteriori esempi di utilizzo di Docker, vedere [utilizzo Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) da hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connetti [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Per altre guide rapide dalla demo HealthClinic.biz hello, vedere [strumenti Guida introduttiva per sviluppatori di Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Altri strumenti di Docker
[Some great docker tools  (Importanti strumenti di Docker, blog di Steve Lasker)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Articoli utili
[Introduzione tooMicroservices da NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Presentazioni
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Presentazione dal vivo a Las Vegas nel 2016: e2e di Docker)](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Introduzione tooASP.NET Core @ compilazione 2016 - in cui è in Demo](https://channel9.msdn.com/Events/Build/2016/B810)
* [Developing .NET apps in containers, Channel 9 (Sviluppo di applicazioni .NET in contenitori, Channel 9)](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
