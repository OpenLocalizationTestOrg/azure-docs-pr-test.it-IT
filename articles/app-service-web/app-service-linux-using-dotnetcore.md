---
title: aaaUse .NET Core nell'App Web in Linux | Documenti Microsoft
description: Usare .NET Core in un'app Web in Linux.
keywords: Servizio app di Azure, app Web, dotnet, core, linux, oss
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Usare .NET Core in un'app Web di Azure in Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[App Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) in Linux fornisce un servizio di hosting web scalabile, applicazione automatica di patch utilizzando hello del sistema operativo Linux. In questa esercitazione vengono fornite istruzioni dettagliate che mostra come toocreate un [.NET Core](https://docs.microsoft.com/aspnet/core/) app in app web di Azure in Linux. 

![App Web in Linux][10]

È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.

## <a name="prerequisites"></a>Prerequisiti ##

toocomplete questa esercitazione: 

* Installare hello [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Installare [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Creare un'applicazione .NET Core locale ##

Avviare una nuova sessione terminal. Creare una directory denominata `hellodotnetcore`e modificare hello tooit di directory corrente. Quindi digitare hello segue: 

```
dotnet new web
``` 

  Questo comando crea tre file (*hellodotnetcore.csproj*, *Program.cs*, e *Startup.cs*) e una cartella vuota (*wwwroot /*) nella directory corrente hello. contenuto di Hello `.csproj` file dovrebbe essere simile hello seguente: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Poiché questa applicazione è un'applicazione web, tooan un riferimento pacchetto ASP.NET Core è stato automaticamente aggiunto toohello *hellodotnetcore.csproj* file. numero di versione di Hello del pacchetto di hello è impostato in base toohello framework scelto. Questo esempio fa riferimento ad ASP.NET Core versione 1.1.2 perché è in uso .NET Core 1.1.

## <a name="build-and-test-hello-application-locally"></a>Compilare e testare un'applicazione hello in locale ##

È possibile compilare ed eseguire l'app .NET Core con hello `dotnet restore` comando seguito da hello `dotnet run` comando, come illustrato di seguito:

```
dotnet restore
dotnet run
```


All'avvio di un'applicazione hello, viene visualizzato un messaggio che indica l'applicazione hello è in ascolto delle richieste di tooincoming su una porta. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Test esplorando troppo`http://localhost:5000/` con il browser. Se tutto funziona correttamente, viene visualizzato il testo come testo risultato hello.

![Eseguire il test con il browser][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Creare un'applicazione .NET Core in hello portale di Azure ##

È necessario innanzitutto toocreate un'app web vuota. Accedi toohello [portale di Azure](https://portal.azure.com/) e creare un nuovo [App Web in Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Creazione di un'app Web][1]

Quando hello **crea** verrà visualizzata la pagina, fornire i dettagli sull'app web:

![Scelta di uno stack di runtime .NET Core][2]

Seguente hello utilizzare tabella come una Guida toofill out hello **crea** pagina, quindi selezionare **OK** e **crea** toocreate hello app.

| Impostazione      | Valore consigliato  | Descrizione                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nome app | hellodotnetcore  | nome Hello dell'app. Il nome deve essere univoco. |
| Subscription | Scelta di una sottoscrizione esistente | Hello sottoscrizione di Azure. |
| Gruppo di risorse | myResourceGroup |  risorse di Azure gruppo toocontain hello web app Hello. |
| Piano di servizio app | Nome del piano di servizio app esistente |  Hello piano di servizio App.  |
| Configura contenitore | .NET Core 1.1 | tipo di contenitore per questa app web Hello: Registro di sistema predefinite, Docker o Private. |
| Origine immagine  | Predefinito  |  origine Hello dell'immagine di hello. |
| Stack di runtime  | .NET Core 1.1  | stack di runtime Hello e versione.  |

## <a name="deploy-your-application-via-git"></a>Distribuire l'applicazione tramite Git ##

Usare Git toodeploy hello .NET Core applicazione tooAzure App del servizio Web App in Linux.

nuova app web di Azure di Hello dispone già di distribuzione Git configurata. URL di distribuzione Git hello noterai passando toohello URL seguente dopo aver inserito il nome dell'applicazione web:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

URL Git Hello è hello modulo basato sul nome dell'app web seguenti:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Eseguire hello seguenti app web di Azure tooyour di comandi toodeploy hello applicazione locale: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Non è necessario di tutti i file in toopush *bin /* o *obj /* directory perché la compilazione dell'applicazione nel cloud hello quando hello dell'applicazione i file di origine vengono inseriti tooAzure. Una volta completato il processo di compilazione hello, i file binari vengono copiati nella directory dell'applicazione hello in */home/sito/wwwroot/*.

Verificare che le operazioni di distribuzione remoto hello segnalano l'esito positivo. Le operazioni di push potrebbero richiedere alcuni minuti dopo la risoluzione di pacchetto ed eseguito nel cloud hello processo di compilazione. Verranno visualizzati alcuni messaggi di stato, di cui uno informa che i file sono stati copiati. output di Hello dovrebbe essere simile toohello seguenti:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Una volta completata la distribuzione di hello, riavviare l'app web per effetto di tootake distribuzione hello. toodo, andare toohello portale di Azure e passare toohello **Panoramica** pagina dell'app web. Seleziona hello **riavviare** nella pagina hello. Quando una finestra popup viene visualizzato, selezionare **Sì** tooconfirm. È quindi possibile passare all'app Web, come illustrato di seguito:

![Esplorazione di .NET Core app distribuita tooAzure servizio App in Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Passaggi successivi
* [Domande frequenti su App Web del Servizio app di Azure su Linux](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
