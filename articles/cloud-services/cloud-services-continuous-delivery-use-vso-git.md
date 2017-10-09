---
title: il recapito aaaContinuous con Git e di Visual Studio Team Services in Azure | Documenti Microsoft
description: "Informazioni su come tooconfigure il Visual Studio Team Services i progetti team toouse Git tooautomatically compilare e distribuire toohello funzionalità App Web di servizi cloud o di servizio App di Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>TooAzure il recapito continuo con Visual Studio Team Services e Git
È possibile utilizzare toohost di progetti team di Visual Studio Team Services un repository Git per il codice sorgente e automaticamente generare e distribuire le app web tooAzure o servizi cloud, ogni volta che si esegue il push del repository toohello un commit.

È necessario Visual Studio 2013 e Azure SDK installata hello. Se si dispone già di Visual Studio 2013, scaricarlo scegliendo hello **possibile iniziare gratuitamente** collegamento [www.visualstudio.com](http://www.visualstudio.com). Installazione hello Azure SDK da [qui](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> È necessario un toocomplete di account di Visual Studio Team Services in questa esercitazione: È possibile [aprire un account di Visual Studio Team Services gratuito](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset backup un tooautomatically servizio cloud compilare e distribuire tooAzure utilizzando Visual Studio Team Services, seguire questi passaggi.

## <a name="1-create-a-git-repository"></a>1: Creare un repository Git
1. Se non si ha già un account Visual Studio Team Services, è possibile ottenerne uno [qui](http://go.microsoft.com/fwlink/?LinkId=397665). Quando si crea il progetto team, scegliere Git come sistema di controllo del codice sorgente. Eseguire il progetto di team tooyour hello istruzioni tooconnect Visual Studio.
2. In **Team Explorer**, scegliere hello **clonare questo repository** collegamento.
   
    ![][3]
3. Specificare il percorso di hello della copia locale di hello e quindi scegliere hello **Clone** pulsante.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: creare un progetto e di eseguirne il commit toohello repository
1. In **Team Explorer**, in hello **soluzioni** , scegliere hello **New** collegare un nuovo progetto nel repository locale hello toocreate.
   
    ![][4]
2. È possibile distribuire un'app web o un servizio cloud (applicazione di Azure) da hello seguente passaggi in questa procedura dettagliata. Creare un nuovo progetto servizio cloud di Azure o un nuovo progetto ASP.NET MVC. Verificare che le destinazioni progetto hello hello .NET Framework 4 o versione successiva. Se si crea un progetto di servizio cloud, aggiungere un ruolo Web ASP.NET MVC e un ruolo di lavoro.
   Se si desidera toocreate un'app web, scegliere hello **applicazione Web ASP.NET** modello di progetto e quindi scegliere **MVC**. Per altre informazioni, vedere [Creare un'app Web ASP.NET in Servizio app di Azure](../app-service-web/app-service-web-get-started-dotnet.md) .
3. Aprire il menu di scelta rapida hello per soluzione hello e scegliere **Commit**.
   
    ![][7]
4. Se si tratta di hello prima volta che si utilizza Git in Visual Studio Team Services, è necessario tooprovide tooidentify alcune informazioni manualmente in Git. In hello **modifiche in sospeso** area di **Team Explorer**, immettere il nome utente e l'indirizzo di posta elettronica. Immettere un commento per il commit di hello e quindi scegliere hello **Commit** pulsante.
   
    ![][8]
5. Si noti hello opzioni tooinclude o escludere modifiche specifiche quando si archivia. Se le modifiche hello desidera sono esclusi, scegliere **Includi tutto**.
6. È stato ora eseguito il commit hello modifiche nella copia locale del repository hello. Successivamente, sincronizzare le modifiche con server hello scegliendo hello **sincronizzazione** collegamento.

## <a name="3-connect-hello-project-tooazure"></a>3: connettere hello progetto tooAzure
1. Dopo aver creato un repository Git in Visual Studio Team Services con un codice di origine in essa contenuti, si è pronti tooconnect il tooAzure repository git.  In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), selezionare l'applicazione web o servizio cloud o crearne uno nuovo facendo clic sull'icona in basso a sinistra di hello e scegliendo + hello **servizio Cloud** o **App Web**quindi **creazione rapida**.
   
    ![][9]
2. Per i servizi cloud, scegliere hello **impostare la pubblicazione con Visual Studio Team Services** collegamento. Per le app web, scegliere hello **imposta distribuzione dal controllo del codice sorgente** collegamento.
   
    ![][10]
3. Nella procedura guidata hello, digitare il nome di hello dell'account di Visual Studio Team Services nella casella di testo hello e scegliere hello **autorizzare ora** collegamento. Potrebbe essere necessario toosign in.
   
    ![][11]
4. In hello **richiesta di connessione** finestra di dialogo popup scegliere **Accept** tooauthorize tooconfigure Azure il progetto team in Visual Studio Team Services.
   
    ![][12]
5. Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services.  Selezionare il nome del progetto team creato nei passaggi precedenti hello hello e scegliere il pulsante di segno di spunta della procedura guidata di hello.
   
    ![][13]
   
    Hello successivo che si inserisce un repository tooyour commit, Visual Studio Team Services verrà compilato e distribuito tooAzure il progetto.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Attivare una ricompilazione e ridistribuire il progetto
1. In Visual Studio aprire un file e modificarlo. Ad esempio, modificare il file hello `_Layout.cshtml` in visualizzazioni hello\\cartella condivisa in un ruolo web MVC.
   
    ![][17]
2. Modificare il testo del piè di pagina hello per il sito hello e salvare file hello.
   
    ![][18]
3. In **Esplora**, aprire il menu di scelta rapida di hello per hello nodo della soluzione, il nodo di progetto o hello file modificato e quindi scegliere **Commit**.
4. Digitare un commento e scegliere **Commit**.
   
    ![][20]
5. Scegliere hello **sincronizzazione** collegamento.
   
    ![][38]
6. Scegliere hello **Push** collegamento toopush il repository toohello commit in Visual Studio Team Services. (È anche possibile usare hello **sincronizzazione** pulsante toocopy il repository toohello commit. Hello differenza è che **sincronizzazione** inoltre esegue il pull hello modifiche più recenti dal repository hello.)
   
    ![][39]
7. Scegliere hello **Home** pulsante tooreturn toohello **Team Explorer** pagina iniziale.
   
    ![][21]
8. Scegliere **compilazioni** tooview hello compilazioni in corso.
   
    ![][22]
   
    **Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.
   
    ![][23]
9. tooview un log dettagliato hello compilazione avanza, fare doppio clic sul nome hello di hello compilazione in corso.
10. Durante la compilazione hello è in corso, esaminare una definizione di compilazione hello creato quando si utilizza hello guidata toolink tooAzure.  Aprire il menu di scelta rapida hello hello la definizione di compilazione e scegliere **Modifica definizione di compilazione**.
    
    ![][25]
11. In hello **Trigger** scheda, si noterà che la definizione di compilazione hello è impostata toobuild su ogni archiviazione, per impostazione predefinita. (Per un servizio cloud, Visual Studio Team Services compila e distribuisce hello ramo master toohello ambiente di gestione temporanea automaticamente. È comunque necessario toodo un sito di passaggio manuale toodeploy toohello in tempo reale. Per un'applicazione web che non ha l'ambiente di gestione temporanea, distribuisce ramo master hello direttamente toohello live del sito.
    
    ![][26]
12. In hello **processo** scheda, è possibile vedere ambiente di distribuzione hello è impostato toohello nome dell'app web o servizio cloud.
    
     ![][27]
13. Se si desiderano valori diversi da quelli predefiniti hello, specificare i valori per le proprietà di hello. salve le proprietà per la pubblicazione di Azure sono in hello **distribuzione** sezione e si potrebbero anche essere necessario tooset MSBuild parametri. Ad esempio, in un progetto di servizio cloud, toospecify una configurazione del servizio diverso da "Cloud", impostare i parametri di MSbuild hello troppo`/p:TargetProfile=[YourProfile]` in *[YourProfile]* corrisponde a un file di configurazione del servizio con un nome come ServiceConfiguration. *YourProfile*. cscfg.
    
     Hello nella tabella seguente mostra le proprietà disponibili hello in hello **distribuzione** sezione:
    
    | Proprietà | Valore predefinito |
    | --- | --- |
    | Consenti certificati non attendibili |Se è false, i certificati SSL devono essere firmati da un'autorità radice. |
    | Consenti aggiornamento |Consente di hello distribuzione tooupdate una distribuzione esistente anziché crearne uno nuovo. Consente di mantenere l'indirizzo IP hello. |
    | Non eliminare |Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito). |
    | Percorso tooDeployment impostazioni |Hello percorso tooyour pubxml file per un'app web, toohello relativo di cartella radice del repository hello. Viene ignorato per i servizi cloud. |
    | Ambiente di distribuzione SharePoint |nome del servizio hello, Hello stesso. |
    | Ambiente di distribuzione Azure |Hello app o cloud nome del servizio web. |
14. A questo punto la compilazione sarà stata completata correttamente.
    
     ![][28]
15. Se si fa doppio clic sul nome di compilazione hello, Visual Studio visualizza un **Riepilogo compilazione**, compresi i risultati dei test da associati progetti di unit test.
    
     ![][29]
16. In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), è possibile visualizzare la distribuzione di hello associata nella hello **distribuzioni** scheda quando viene selezionato l'ambiente di gestione temporanea hello.
    
     ![][30]
17. Individuare l'URL del sito tooyour. Per un'app web, è sufficiente scegliere hello **Sfoglia** pulsante nel portale di hello. Per un servizio cloud, scegliere URL hello in hello **Quick Glance** sezione di hello **Dashboard** pagina che mostra l'ambiente di gestione temporanea hello.
    
    Le distribuzioni di integrazione continua per i servizi cloud sono pubblicati toohello ambiente di gestione temporanea per impostazione predefinita. È possibile modificare questa impostazione hello **ambiente del servizio Cloud alternativo** proprietà troppo**produzione**. Ecco dove l'URL del sito hello è nella pagina dashboard del servizio cloud hello.
    
    ![][31]
    
    Una nuova scheda del browser verrà aperto tooreveal del sito in esecuzione.
    
    ![][32]
18. Se si apportano altre modifiche delle tooyour progetto, i trigger è più compila e si accumuleranno più distribuzioni. Hello più recente uno è contrassegnato come attivo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Ridistribuire una compilazione precedente
Questo passaggio è facoltativo. Nel portale di Azure classico hello, scegliere una distribuzione precedente e scegliere **ridistribuire** toorewind il sito tooan precedentemente check-in. Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: modificare la distribuzione di produzione hello
Quando si è pronti, è possibile alzare di livello hello gestione temporanea toohello ambiente di produzione scegliendo **scambiare** nel portale di Azure classico hello. ambiente di gestione temporanea appena distribuito Hello è tooProduction innalzate di livello e ambiente di produzione hello precedente, se presente, diventa un ambiente di gestione temporanea. distribuzione attiva Hello potrebbe essere diverso per ambienti di gestione temporanea e produzione hello, ma la cronologia della distribuzione hello di compilazioni recenti è hello uguali indipendentemente dal fatto che dell'ambiente.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: Eseguire la distribuzione da un ramo di lavoro.
Quando si usa Git, vengono in genere modifiche in un ramo di lavoro e integra nel ramo master di hello quando lo sviluppo delle raggiunge uno stato completato. Durante la fase di sviluppo hello di un progetto, sarà toobuild che desideri distribuire tooAzure ramo di lavoro hello.

1. In **Team Explorer**, scegliere hello **Home** pulsante e quindi scegliere hello **rami** pulsante.
   
    ![][40]
2. Scegliere hello **nuovo ramo** collegamento.
   
    ![][41]
3. Immettere il nome di hello del ramo hello, ad esempio "working" e scegliere **Crea ramo**. Verrà creato un nuovo branch locale.
   
    ![][42]
4. Pubblicare il ramo hello. Scegliere il nome di ramo hello in **non pubblicato rami**e scegliere **pubblica**.
   
    ![][44]
5. Per impostazione predefinita, solo di modificare il trigger di ramo master toohello una compilazione continua. tooset la compilazione continua per un ramo di lavoro, scegliere hello **compilazioni** pagina **Team Explorer**e scegliere **Modifica definizione di compilazione**.
6. Aprire hello **le impostazioni dell'origine** scheda. In **monitorati rami per l'integrazione continua e compilazione**, scegliere **fare clic qui tooadd una nuova riga**.
   
    ![][47]
7. Specificare il ramo hello che è stato creato, ad esempio funzionante/testine/refs.
   
    ![][48]
8. Apportare una modifica nel codice hello, menu di scelta rapida aprire hello hello modificato file e quindi scegliere **Commit**.
   
    ![][43]
9. Scegliere hello **commit non sincronizzati** collegamento e scegliere hello **sincronizzazione** pulsante o hello **Push** hello toocopy collegamento Cambia copia toohello del ramo di lavoro hello in Visual Studio Team Services.
   
   ![][45]
10. Passare toohello **compilazioni** consente di visualizzare e trovare compilazione hello attivate solo ottenuto per il ramo di lavoro hello.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori suggerimenti sull'uso di Git con Visual Studio Team Services, vedere [sviluppare e condividere il codice in Git in Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) e per informazioni sull'utilizzo di un repository Git che non è gestito da Visual Studio Team Services toopublish tooAzure, vedere [tooAzure distribuzione continua servizio App](../app-service-web/app-service-continuous-deployment.md). Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
