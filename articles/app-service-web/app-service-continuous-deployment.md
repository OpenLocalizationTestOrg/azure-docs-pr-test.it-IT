---
title: aaaContinuous tooAzure distribuzione servizio App | Documenti Microsoft
description: Informazioni su come la distribuzione continua di tooenable tooAzure servizio App.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>TooAzure distribuzione continua servizio App
In questa esercitazione illustra come tooconfigure un flusso di lavoro di distribuzione continua per il [Azure App Service] app. Integrazione del servizio App con BitBucket, GitHub, e [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) consente un continuo del flusso di lavoro di distribuzione in Azure esegue il pull degli aggiornamenti più recenti di hello dal progetto pubblicati tooone di questi servizi. La distribuzione continua è un'ottima opzione per i progetti in cui vengono integrati contributi numerosi e frequenti.

toofind out come la distribuzione continua tooconfigure manualmente da un repository di cloud non elencata hello portale di Azure (ad esempio [GitLab](https://gitlab.com/)), vedere [configurazione di distribuzione continua tramite i passaggi manuali](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Abilitare la distribuzione continua
distribuzione continua tooenable,

1. Pubblicare il repository di contenuto toohello app che verrà utilizzato per la distribuzione continua.  
    Per ulteriori informazioni sulla pubblicazione di servizi toothese progetto, vedere [creare un repository (GitHub)], [creare un repository (BitBucket)], e [Introduzione a Visual Studio Team Services].
2. Nel Pannello di menu dell'applicazione in hello [portale di Azure], fare clic su **distribuzione dell'APP > Opzioni di distribuzione**. Fare clic su **Scegli origine**, quindi selezionare origine distribuzione hello.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure un account di Visual Studio Team Services per la distribuzione di servizio App, vedere [esercitazione](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Completamento del flusso di lavoro di hello autorizzazione.
4. In hello **origine distribuzione** pannello, scegliere il progetto hello e creare rami toodeploy da. Al termine, fare clic su **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Se si abilita la distribuzione continua con GitHub o BitBucket, verranno visualizzati progetti sia pubblici che privati.
   > 
   > 
   
    Servizio App crea un'associazione con repository selezionato hello, inserisce nel file hello dal ramo specificato hello e mantiene un clone del repository per l'applicazione di servizio App. Quando si configura una distribuzione continua VSTS dal portale di Azure hello, integrazione di hello utilizza hello servizio App [motore di distribuzione Kudu](https://github.com/projectkudu/kudu/wiki), che già automatizza le attività di compilazione e distribuzione con ogni `git push`. Tooseparately non è necessario impostare la distribuzione continua in Visual Studio Team Services. Dopo il completamento del processo, hello **opzioni di distribuzione** pannello app verrà visualizzata una distribuzione attiva che indica la distribuzione ha avuto esito positivo.
5. è stata distribuita correttamente tooverify hello app, fare clic su hello **URL** nella parte superiore di hello del pannello dell'applicazione hello in hello portale di Azure.
6. tooverify in corso la distribuzione continua dal repository hello di propria scelta, push di un repository toohello di modifica. L'app deve aggiornare le modifiche di hello tooreflect a breve termine repository toohello di hello push. È possibile verificare che è estratta nell'aggiornamento hello in hello **opzioni di distribuzione** pannello dell'app.

## <a name="VSsolution"></a>Distribuzione continua di una soluzione di Visual Studio
Inserendo un tooAzure di soluzioni di Visual Studio servizio App è semplice come l'inserimento di un file index.html semplice. il processo di distribuzione di servizio App Hello semplifica tutti i dettagli di hello, incluso il ripristino NuGet dipendenze e la creazione di file binari dell'applicazione hello. È possibile seguire hello origine controllo procedure consigliate di gestione del codice solo nel repository Git e fare in modo che la distribuzione del servizio App rest hello.

Hello passaggi per l'inserimento del tooApp soluzione Visual Studio sono servizio hello stesso come hello [precedente sezione](#overview), a condizione che si configura la soluzione e il repository come indicato di seguito:

* Utilizzare hello Visual Studio origine controllo opzione toogenerate un `.gitignore` file, ad esempio l'immagine di hello seguente o aggiungere manualmente un `.gitignore` file nella radice del repository con contenuto toothis simile [esempio con estensione gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Aggiungi repository di tooyour struttura ad albero di directory hello intera soluzione, con il file con estensione sln hello nella radice del repository hello.

Dopo aver impostato il repository come descritto e configurata l'app in Azure per la pubblicazione continua da uno dei repository Git online hello, è possibile sviluppare l'applicazione ASP.NET in locale in Visual Studio e in modo continuo di semplicemente da distribuire il codice inserendo il repository Git in linea del tooyour le modifiche.

## <a name="disableCD"></a>Disabilitare la distribuzione continua
distribuzione continua toodisable,

1. Nel Pannello di menu dell'applicazione in hello [portale di Azure], fare clic su **distribuzione dell'APP > Opzioni di distribuzione**. Quindi fare clic su **Disconnect** in hello **opzioni di distribuzione** blade.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Dopo la risposta **Sì** toohello messaggio di conferma, è possibile restituire pannello tooyour dell'app e fare clic su **distribuzione dell'APP > Opzioni di distribuzione** se si desidera tooset la pubblicazione da un'altra origine.

## <a name="additional-resources"></a>Risorse aggiuntive
* [La modalità di problemi comuni di tooinvestigate con una distribuzione continua](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Come toouse PowerShell per Azure]
* [Come toouse hello strumenti da riga di comando di Azure per Mac e Linux]
* [Documentazione su Git]
* [Progetto Kudu](https://github.com/projectkudu/kudu/wiki)
* [Usare Azure tooautomatically genera un'app di CI/CD pipeline toodeploy un ASP.NET 4](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portale di Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Come toouse PowerShell per Azure]: /powershell/azureps-cmdlets-docs
[Come toouse hello strumenti da riga di comando di Azure per Mac e Linux]:../cli-install-nodejs.md
[Documentazione su Git]: http://git-scm.com/documentation

[creare un repository (GitHub)]: https://help.github.com/articles/create-a-repo
[creare un repository (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Introduzione a Visual Studio Team Services]: https://www.visualstudio.com/docs/vsts-tfs-overview
