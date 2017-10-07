---
title: aaaDeploy processi Web usando Visual Studio
description: Informazioni su come toodeploy processi Web di Azure tooAzure applicazione servizio Web App con Visual Studio.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Distribuzione di processi Web usando Visual Studio
## <a name="overview"></a>Panoramica
Questo argomento viene illustrato come toouse Visual Studio toodeploy un'applicazione Console progetto app web tooa [servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) come un [processo Web di Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Per informazioni su come toodeploy processi Web usando hello [portale Azure](https://portal.azure.com), vedere [attività eseguire in Background con processi Web](web-sites-create-web-jobs.md).

Quando distribuisce un progetto di applicazione console abilitato per i processi Web, Visual Studio esegue due attività:

* File di runtime di copie di toohello cartella appropriata in hello web app (*App_Data/processi/continua* per processi Web continui, *App_Data, processi/attivato* per processi Web pianificati e su richiesta).
* Consente di impostare [processi dell'utilità di pianificazione di Azure](#scheduler) per processi Web che vengono pianificati toorun in determinati momenti. Tale operazione non è necessaria per l'esecuzione dei processi Web in modalità continua.

Un progetto processi Web abilitati presenta hello tooit aggiunti gli elementi seguenti:

* Hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacchetto NuGet.
* File [webjob-publish-settings.json](#publishsettings) che contiene le impostazioni di distribuzione e dell'utilità di pianificazione. 

![Diagramma che mostra ciò che viene aggiunto tooa App Console tooenable deployment come un processo Web](./media/websites-dotnet-deploy-webjobs/convert.png)

È possibile aggiungere questi tooan elementi progetto di applicazione Console esistente o utilizzare un toocreate modello un nuovo progetto applicazione Console abilitata per processi Web. 

È possibile distribuire un progetto come un processo Web da solo o collegare il progetto di web tooa in modo che venga distribuito automaticamente ogni volta che si distribuisce il progetto di web hello. toolink progetti di Visual Studio include il nome di hello del progetto abilitato processi Web hello in un [processi Web list.json](#webjobslist) file nel progetto web hello.

![Diagramma che illustra il progetto processo Web collegamento tooweb progetto](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Prerequisiti
Funzionalità di distribuzione di processi Web sono disponibili in Visual Studio quando si installa hello Azure SDK per .NET:

* [Azure SDK per .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Abilitare la distribuzione dei processi Web per un progetto di applicazione console esistente
Sono disponibili due opzioni:

* [Abilitare la distribuzione automatica con un progetto Web](#convertlink).
  
    Configurare un progetto di applicazione console esistente in modo tale che venga distribuito automaticamente come processo Web quando viene distribuito un progetto Web. Utilizzare questa opzione quando si desidera che il processo Web in hello toorun stessa app web in cui si esegue hello correlati dell'applicazione web.
* [Abilitare la distribuzione senza un progetto Web](#convertnolink).
  
    Configurare un toodeploy di progetto applicazione Console esistente come un processo Web da sola, con alcun progetto web tooa di collegamento. Utilizzare questa opzione quando si desidera toorun un processo Web in un'app web di per sé con nessuna applicazione web in esecuzione nell'app web hello. È possibile toodo questo ordine tooscale in grado di toobe le risorse di processo Web indipendentemente dalle risorse dell'applicazione web.

### <a id="convertlink"></a> Abilitare la distribuzione automatica dei processi Web con un progetto Web
1. Progetto web di hello pulsante destro del mouse in **Esplora**, quindi fare clic su **Aggiungi** > **progetto esistente come processo Web di Azure**.
   
    ![Progetto esistente come processo Web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo.
2. In hello **nome progetto** elenco a discesa, tooadd di progetto applicazione Console hello selezionare come un processo Web.
   
    ![Selezione del progetto nella finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Hello completo [Aggiungi processo Web di Azure](#configure) finestra di dialogo e quindi fare clic su **OK**. 

### <a id="convertnolink"></a> Abilitare la distribuzione dei processi Web senza un progetto Web
1. Progetto di applicazione Console hello pulsante destro del mouse in **Esplora**, quindi fare clic su **pubblica come processo Web di Azure...** . 
   
    ![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo, con progetto hello in hello **nome progetto** casella.
2. Hello completo [Aggiungi processo Web di Azure](#configure) la finestra di dialogo e quindi fare clic su **OK**.
   
   Hello **pubblica sul Web** procedura guidata viene visualizzata.  Se si desidera toopublish immediatamente, chiudere la procedura guidata hello. le impostazioni di Hello immessi vengono salvate per quando si desidera troppo[distribuire il progetto hello](#deploy).

## <a id="create"></a>Creare un nuovo progetto abilitato per i processi Web
toocreate un nuovo progetto processi Web abilitata, è possibile utilizzare hello applicazione Console progetto modello e abilitare processi Web distribuzione come spiegato in [hello precedente sezione](#convert). In alternativa, è possibile utilizzare modello nuovo progetto di hello processi Web:

* [Modello di hello processi Web nuovo progetto per un processo indipendente dal Web](#createnolink)
  
    Creare un progetto e configurare toodeploy da se stesso come un processo Web, un progetto di web tooa alcun collegamento. Utilizzare questa opzione quando si desidera toorun un processo Web in un'app web di per sé con nessuna applicazione web in esecuzione nell'app web hello. È possibile toodo questo ordine tooscale in grado di toobe le risorse di processo Web indipendentemente dalle risorse dell'applicazione web.
* [Modello di hello processi Web nuovo progetto per un progetto di web tooa collegato processo Web](#createlink)
  
    Creare un progetto toodeploy configurato automaticamente come un processo Web quando un progetto web nella stessa soluzione viene distribuita hello. Utilizzare questa opzione quando si desidera che il processo Web in hello toorun stessa app web in cui si esegue hello correlati dell'applicazione web.

> [!NOTE]
> modello nuovo progetto processi Web di Hello automaticamente installa i pacchetti NuGet e include il codice in *Program.cs* per hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Se non si desidera toouse hello WebJobs SDK, rimuovere o modificare hello `host.RunAndBlock` istruzione *Program.cs*.
> 
> 

### <a id="createnolink"></a>Modello di hello processi Web nuovo progetto per un processo indipendente dal Web
1. Fare clic su **File** > **nuovo progetto**e quindi in hello **nuovo progetto** finestra di dialogo fare clic su **Cloud**  >   **Processo Web di Azure (.NET Framework)**.
   
    ![Finestra di dialogo Nuovo progetto con il modello processo Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. Seguire le direzioni di hello illustrate in precedenza troppo[rendere hello progetto applicazione Console come un progetto processi Web indipendente](#convertnolink).

### <a id="createlink"></a>Modello di hello processi Web nuovo progetto per un progetto di web tooa collegato processo Web
1. Progetto web di hello pulsante destro del mouse in **Esplora**, quindi fare clic su **Aggiungi** > **nuovo progetto processo Web di Azure**.
   
    ![Voce del menu Nuovo progetto processo Web Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo.
2. Hello completo [Aggiungi processo Web di Azure](#configure) la finestra di dialogo e quindi fare clic su **OK**.

## <a id="configure"></a>finestra di dialogo Aggiungi processo Web di Azure Hello
Hello **Aggiungi processo Web di Azure** finestra di dialogo consente di immettere il nome di processo Web hello ed eseguire l'impostazione della modalità per il processo Web. 

![Finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

i campi di Hello in questa finestra di dialogo corrispondono toofields su hello **nuovo processo** finestra di dialogo di hello portale di Azure. Per ulteriori informazioni, vedere [attività in Background eseguito con WebJobs](web-sites-create-web-jobs.md).

> [!NOTE]
> * Per informazioni sulla distribuzione da riga di comando, vedere [Abilitazione della riga di comando o del recapito continuo di processi Web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Se si distribuisce un processo Web e quindi si decide toochange hello tipo processo Web e ridistribuzione, è necessario file Settings pubblicare processi Web di toodelete hello. In questo modo Visual Studio Mostra hello opzioni di pubblicazione, pertanto è possibile modificare il tipo di hello del processo Web.
> * Se si distribuisce un processo Web e successivamente si cambia modalità di esecuzione da continuo continua a toonon hello o viceversa, Visual Studio crea un nuovo processo di Web in Azure quando si ridistribuisce. Se è modificare altre impostazioni di pianificazione, ma lasciare eseguire modalità hello stesso o alternare pianificati e su richiesta, gli aggiornamenti di Visual Studio hello processo esistente anziché crearne uno nuovo.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Quando si configura un'applicazione Console per la distribuzione di processi Web, Visual Studio installa hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package e archivi la programmazione di informazioni in un *Settings pubblicare processo Web*  file nel progetto hello *proprietà* nella cartella del progetto processi Web hello. Di seguito è riportato un esempio di tale file:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense. schema del file Hello è archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e può essere visualizzata.  

## <a id="webjobslist"></a>webjobs-list.json
Quando si collega un progetto di web tooa progetto processi Web, Visual Studio archivia il nome di hello del progetto processi Web hello in un *processi Web list.json* file nel progetto hello web *proprietà* cartella. elenco di Hello potrebbe contenere più progetti processi Web, come illustrato nell'esempio seguente hello:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense. schema del file Hello è archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e può essere visualizzata.

## <a id="deploy"></a>Distribuire un progetto processi Web
Un progetto processi Web che è stato collegato un progetto web tooa distribuisce automaticamente un progetto web hello. Per informazioni sulla distribuzione dei progetti web, vedere [come toodeploy tooWeb app](web-sites-deploy.md).

un progetto processi Web di per sé toodeploy fare clic sul progetto hello in **Esplora** e fare clic su **pubblica come processo Web di Azure...** . 

![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Per un processo Web indipendenti, hello stesso **pubblica sul Web** procedura guidata che viene utilizzato per i progetti web viene visualizzato, ma con un numero inferiore toochange disponibili di impostazioni.

## <a id="nextsteps"></a>Passaggi successivi
Questo articolo è stato spiegato come toodeploy processi Web usando Visual Studio. Per ulteriori informazioni su come toodeploy processi Web di Azure, vedere [processi Web di Azure - consigliato risorse - distribuzione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

