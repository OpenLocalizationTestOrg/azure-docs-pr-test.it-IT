---
title: aaaCreate un'app web ASP.NET Core in Visual Studio Code
description: In questa esercitazione viene illustrato come toocreate un Core di ASP.NET web app con codice di Visual Studio.
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Creare un'app Web ASP.NET Core in Visual Studio Code
## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come toocreate un Core di ASP.NET web app usando [codice di Visual Studio (Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode) e distribuirlo troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Sebbene in questo articolo si riferisce tooweb App, si applica anche tooAPI App e App per dispositivi mobili. 
> 
> 

ASP.NET Core è un'importante riprogettazione di ASP.NET. Costituisce un nuovo framework open source e multipiattaforma per la creazione tramite .NET di moderne app Web basate sul cloud. Per ulteriori informazioni, vedere [tooASP.NET introduzione Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Per altre informazioni sulle app Web del servizio app di Azure, vedere [Panoramica delle app Web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Prerequisiti
* Installare [Visual Studio Code](http://code.visualstudio.com/Docs/setup).
* Installare Git: è possibile installarlo da una delle seguenti posizioni: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads). Se si tooGit nuovo, scegliere [git scm.com](http://git-scm.com/downloads) e selezionare opzione hello troppo**usare Git dal prompt dei comandi di Windows hello**. Dopo aver installato Git, è necessario anche nome utente di tooset hello Git e di posta elettronica come è necessario più avanti nell'esercitazione hello (quando si esegue un'operazione di commit dal codice di Visual Studio).  

## <a name="install-aspnet-core"></a>Installare ASP.NET Core
ASP.NET Core è uno stack .NET snello per la creazione di un cloud moderno e di app Web in esecuzione su OS X, Linux e Windows. Si è stato compilato dalla hello messa a terra backup tooprovide un framework di sviluppo ottimizzato per le app che sono entrambi cloud toohello distribuito o vengono eseguiti in locale. È costituito da componenti modulari con un overhead minimo, in modo da garantire la massima flessibilità durante la creazione di soluzioni.

In questa esercitazione è progettata tooget viene avviata la compilazione di applicazioni con versioni di sviluppo più recenti di hello di ASP.NET Core. Hello attenendosi alle istruzioni è tooWindows specifico. Per istruzioni sull'installazione in OS X, Linux e Windows, vedere [Getting started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Introduzione ad ASP.NET Core). 


> [!NOTE]
> Per istruzioni di installazione più dettagliate per OS X, Linux e Windows, vedere [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx) (Installazione di ASP.NET Core). 
> 
> 

## <a name="create-hello-web-app"></a>Creare l'app web hello
In questa sezione viene illustrato come una nuova app ASP.NET tooscaffold web app usando lo strumento .NET CLI hello. 

1. Immettere seguente hello al prompt dei comandi toocreate hello progetto cartella e lo scaffolding hello app hello.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Generatore dell'interfaccia della riga di comando dotnet - ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello pacchetti NuGet necessari, eseguire hello comando seguente:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Eseguire localmente l'app web hello
Ora che è creato hello web app e recuperare tutti i pacchetti NuGet hello per hello app, è possibile eseguire app web hello in locale.

1. Eseguire app hello (hello `dotnet run` comando verrà compilata l'applicazione hello quando è aggiornata):
    ```terminal
    dotnet run
    ```
2. Aprire un browser e passare toohello URL seguente.
   
    **http://localhost:5000**
   
    pagina predefinita Hello dell'app web hello apparirà come segue.
   
    ![App Web locale in un browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Chiudere il browser. In hello **finestra di comando**, premere **Ctrl + C** tooshut verso il basso di un'applicazione hello e chiude hello **finestra di comando**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Creare un'app web nel portale di Azure hello
Hello seguente verrà procedura consente di creare un'app web nel portale di Azure hello.

1. Accedi toohello [portale Azure](https://portal.azure.com).
2. Fare clic su **NEW** in hello in alto a sinistra del portale hello.
3. Fare clic su **App Web > App Web**.
   
    ![Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Immettere un valore in **Nome**, ad esempio **SampleWebAppDemo**. Si noti che questo nome deve toobe univoco e portale hello imporrà che quando si tenta di nome hello tooenter. Pertanto, se si seleziona un invio di un valore diverso, è necessario toosubstitute tale valore per ogni occorrenza di **SampleWebAppDemo** visualizzati in questa esercitazione. 
5. Selezionare un piano esistente in **Piano di servizio app** o crearne uno nuovo. Se si crea un nuovo piano, selezionare hello piano tariffario, posizione e altre opzioni. Per ulteriori informazioni sui piani di servizio App, vedere l'articolo hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Pannello Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Fare clic su **Crea**.
   
    ![Pannello dell'app Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Abilitare la pubblicazione Git per hello nuova app web
GIT è un sistema di controllo della versione distribuita che è possibile utilizzare toodeploy l'app web di servizio App di Azure. Archiviare il codice hello che scritto per l'app web in un repository Git locale e si distribuiranno tooAzure del codice mediante il push dei repository remoto tooa.   

1. Accedere al hello [portale Azure](https://portal.azure.com).
2. Fare clic su **Sfoglia**.
3. Fare clic su **App Web** tooview un elenco di App web hello associati alla sottoscrizione di Azure.
4. Selezionare l'app web hello che è stato creato in questa esercitazione.
5. Nel Pannello di hello web app, fare clic su **impostazioni** > **distribuzione continua**. 
   
    ![Host dell'app Web di Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Fare clic su **Scegliere l'origine > Repository Git locale**.
7. Fare clic su **OK**.
   
    ![Repository Git locale di Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Se le credenziali di distribuzione per la pubblicazione di un'app Web o di un'altra app del servizio app non sono ancora state configurate, è possibile farlo ora:
   
   * Fare clic su **Impostazioni** > **Credenziali di distribuzione**. Hello **impostare le credenziali di distribuzione** pannello verrà visualizzato.
   * Creare un nome utente e una password.  La password sarà necessaria più avanti durante la configurazione di Git.
   * Fare clic su **Save**.
9. Nel pannello dell'app Web fare clic su **Impostazioni > Proprietà**. URL di Hello del repository Git remoto hello che verranno distribuite toois indicato nel **URL GIT**.
10. Hello copia **URL GIT** valore per un utilizzo successivo in esercitazione hello.
    
    ![URL Git di Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Pubblicare il tooAzure app web del servizio App
In questa sezione si crea un repository Git locale e push da tale toodeploy tooAzure repository del tooAzure app web.

1. Nel codice di Visual Studio, selezionare hello **Git** opzione nella barra di spostamento sinistra hello.
   
    ![Icona di Git in Visual Studio Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Selezionare **repository git Initialize** toomake che l'area di lavoro è nel controllo del codice sorgente git. 
   
    ![Initialize Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Aprire una finestra di comando hello e passare alla directory di toohello directory dell'app web. Immettere quindi hello comando seguente:
   
        git config core.autocrlf false
   
    Questo comando evita un problema relativo al testo che concerne le terminazioni CRLF e LF.
4. Nel codice di Visual Studio, aggiungere un messaggio di conferma e fare clic su hello **tutti i Commit** il segno di spunta.
   
    ![Commit All in Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Al termine dell'elaborazione Git, si noterà che non sono presenti file elencati nella finestra di Git hello in **modifiche**. 
   
    ![Nessuna modifica in Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Modificare toohello back-finestra di comando al prompt dei comandi di hello quale fa riferimento toohello directory in cui si trova l'app web.
7. Creare un riferimento remoto per l'inserimento di app web tooyour di aggiornamenti tramite hello URL Git (che termina con "GIT") che è stato copiato in precedenza.
   
        git remote add azure [URL for remote repository]
8. Configurare Git toosave le credenziali in locale in modo che siano tooyour aggiunti automaticamente i comandi di push generati dal codice di Visual Studio.
   
        git config credential.helper store
9. Effettuare il push del tooAzure modifiche immettendo hello comando seguente. Dopo questo tooAzure push iniziale, sarà in grado di toodo push hello tutti i comandi di Visual Studio Code. 
   
        git push -u azure master
   
    Viene chiesto di immettere la password di hello creato in precedenza in Azure. **Nota: La password non sarà visibile.**
   
    output di Hello dalla hello sopra comando termina con un messaggio che la distribuzione ha esito positivo.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Se si apportano modifiche tooyour app, è possibile ripubblicare direttamente nel codice di Visual Studio con Git funzionalità hello selezionando hello **Commit tutti** opzione seguita da hello **Push** opzione. Si noterà hello **Push** opzione è disponibile in hello dal menu a discesa successivo toohello **Commit tutti** e **aggiornamento** pulsanti.
> 
> 

Se è necessario toocollaborate su un progetto, è consigliabile push tooGitHub tra tooAzure push.

## <a name="run-hello-app-in-azure"></a>Eseguire l'applicazione hello in Azure
Ora che è stato distribuito l'app web, eseguire app hello mentre ospitato in Azure. 

A questo scopo, è possibile eseguire una delle due operazioni seguenti:

* Aprire un browser e immettere il nome di hello dell'app web come indicato di seguito.   
  
        http://SampleWebAppDemo.azurewebsites.net
* In hello portale di Azure, individuare pannello app web di hello per le app web e fare clic su **Sfoglia** tooview l'app 
* nel browser predefinito.

![App Web di Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Riepilogo
In questa esercitazione, si è appreso come toocreate un'app web nel codice di Visual Studio e distribuirlo tooAzure. Per ulteriori informazioni sul codice di Visual Studio, vedere l'articolo hello [perché Visual Studio Code?](https://code.visualstudio.com/Docs/) Per altre informazioni sulle app Web del servizio app, vedere [Panoramica delle app Web](app-service-web-overview.md). 

