---
title: gli errori di client Docker aaaTroubleshooting in Windows usando Visual Studio | Documenti Microsoft
description: Risolvere i problemi riscontrati quando si utilizza Visual Studio toocreate e distribuire tooDocker App web in Windows usando Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Risoluzione dei problemi di sviluppo di Docker in Visual Studio

Quando si lavora con Visual Studio Tools per Docker Preview, è possibile riscontrare alcuni problemi a causa di natura hello dell'anteprima di hello.
Di seguito vengono riportati alcuni problemi comuni e le soluzioni relative.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Contenitori Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Si verificano errori di compilazione durante il debug di un'applicazione console o Web .NET Core  

Questo potrebbe essere correlato toonot condividono unità hello in cui si trova il progetto hello con Docker per Windows.  Potrebbe essere visualizzato un errore analogo hello seguente:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve questo problema:

1. Fare doppio clic su **Docker per Windows** in hello area di notifica e quindi selezionare **impostazioni**.  
2. Selezionare **unità condivise** e condividere hello unità in cui si trova il progetto hello.

### <a name="windows-containers"></a>**Contenitori Windows**

Hello problemi descritti di seguito sono toodebugging specifico .NET Framework web e console applicazioni nei contenitori di Windows.

#### <a name="prerequisites"></a>Prerequisiti

1. Visual Studio 2017 RC (o versioni successive) con hello .NET Core e carico di lavoro di anteprima di Docker deve essere installato.
2. Windows 10 Anniversary Update con le patch di Windows Update più recenti. È in particolare necessario installare [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016). 
3. È necessario installare [Docker per Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 o versione successiva).
4. **Passare a contenitori tooWindows** deve essere selezionato. Nell'area di notifica hello, fare clic su **Docker per Windows**, quindi selezionare **passare contenitori tooWindows**. Dopo il riavvio del computer hello, assicurarsi che questa impostazione viene mantenuta.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>L'output della console non viene visualizzato nella finestra di output di Visual Studio durante il debug di un'applicazione console

Si tratta di un problema noto con debugger di Visual Studio hello (msvsmon.exe), che attualmente non è progettato per questo scenario. Il supporto per questo scenario potrà essere incluso in una versione futura. toosee output da un'applicazione console in Visual Studio, usare hello **Docker: Avvia progetto**, che equivale troppo**Avvia senza eseguire debug**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Debug di applicazioni web con hello versione di configurazione non riesce con errore di accesso negato (403)

toowork questo problema, aprire web.release.config soluzione hello e impostare come commento o eliminare hello seguenti righe:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Contenitori Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Mapping del volume non è possibile toovalidate
Mapping del volume è il codice sorgente hello tooshare necessarie e i file binari dell'applicazione con cartella dell'applicazione hello nel contenitore hello.  Mapping del volume specifici sono contenuti all'interno dei file docker-compose.dev.debug.yml e docker-compose.dev.release.yml. Come i file vengono modificati nel computer host, i contenitori di hello riflettono tali modifiche in una struttura di cartelle simile.

mapping del volume tooenable:

1. Fare clic su **Moby** nell'area di notifica hello e selezionare **impostazioni**.
2. Selezionare **Unità condivise**.
3. Selezionare un'unità che ospita il progetto e hello sul disco in cui si trova in % USERPROFILE % hello.
4. Fare clic su **Apply**.

tootest se funziona mapping del volume, ricompilare e selezionare F5 da Visual Studio dopo che sono stati condivisione o hello seguente di codice da un prompt dei comandi eseguire uno o più unità.

> [!NOTE]
> Questo esempio presuppone che la cartella Utenti si trovi nell'unità C e che sia stata condivisa.
> Se è stata condivisa un'unità diversa, aggiornare di conseguenza.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Eseguire hello seguente codice nel contenitore di Linux hello.

```
/ # ls
```

Verrà visualizzato un'elenco delle directory da hello utenti o delle cartelle pubbliche. Se non vengono visualizzati file e la cartella in /c/Users/Public non è vuota, il mapping del volume non è configurato correttamente.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Modificare toohello spaziale toosee hello contenuto della directory di hello `/c/Users/Public` directory:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Quando si lavora con le macchine virtuali Linux, hello contenitore file system è tra maiuscole e minuscole.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Build: errore imprevisto dell'attività "PrepareForBuild"

Microsoft.DotNet.Docker.CommandLine.ClientException: Errore durante il tentativo di tooconnect.

Verificare che host Docker di hello predefinito sia in esecuzione. Aprire un prompt dei comandi ed eseguire questo comando:

```
docker info
```

Se viene restituito un errore, quindi tentare di hello toostart **Docker per Windows** app desktop. Se viene eseguita l'app desktop hello, quindi **Moby** deve essere visibile nell'area di notifica hello. Fare doppio clic su **Moby** e aprire **Impostazioni**. Fare clic su **Reimposta** e quindi riavviare Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Una finestra di dialogo di errore si verifica durante il tentativo di tooadd Docker supporto o il debug (F5) di un'applicazione ASP.NET Core in un contenitore

Dopo la disinstallazione e l'installazione delle estensioni, può risultare danneggiato hello cache Managed Extensibility Framework (MEF) in Visual Studio. In questo caso, può provocare diversi messaggi di errore quando si è aggiunta del supporto di Docker e/o il tentativo di toorun o eseguire il debug (F5) dell'applicazione ASP.NET Core. Come soluzione alternativa temporanea, utilizzare hello seguendo i passaggi toodelete e rigenerare hello cache MEF.

1. Chiudere tutte le istanze di Visual Studio.
1. Aprire %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Eliminare hello seguenti cartelle:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Aprire Visual Studio.
1. Tentare nuovamente di scenario hello.
