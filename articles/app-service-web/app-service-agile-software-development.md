---
title: sviluppo di software aaaAgile con il servizio App di Azure
description: "Informazioni su come toocreate a scalabilità elevata applicazioni complesse con il servizio App di Azure in modo che supporta lo sviluppo agile di software."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Agile Software Development con il servizio app di Azure
In questa esercitazione si apprenderà come applicazioni complesse di toocreate su vasta scala con [Azure App Service](/azure/app-service/) in modo che supporti [sviluppo del software agile](https://en.wikipedia.org/wiki/Agile_software_development). Si presuppone che si conosce già la modalità troppo[distribuire applicazioni complesse in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md).

Limitazioni di processi tecnici spesso utili in modo hello della corretta implementazione delle metodologie agile. Servizio App di Azure con funzionalità, ad esempio [la pubblicazione continua](app-service-continuous-deployment.md), [ambienti di gestione temporanea](web-sites-staged-publishing.md) (slot), e [monitoraggio](web-sites-monitor.md), quando è associata in modo appropriato a orchestrazione hello e gestione della distribuzione in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), possono far parte di un'ottima soluzione per gli sviluppatori che adottano sviluppo agile di software.

Nella tabella seguente Hello è un breve elenco di requisiti associati a sviluppo agile e come servizi di Azure attivare ognuno di essi.

| Requisito | Abilitazione mediante Azure |
| --- | --- |
| - Compilazione con ogni commit<br>- Compilazione automatica e rapida |Quando viene configurato con la distribuzione continua, il servizio app di Azure può funzionare come una compilazione con esecuzione live basata su un ramo di sviluppo. Ogni volta che il ramo toohello push del codice, è in esecuzione e generati automaticamente in tempo reale in Azure. |
| - Compilazioni testate automaticamente |Caricare i test, test web e così via, possono essere distribuiti con il modello di gestione risorse di Azure hello. |
| - Esecuzione di test in un clone dell'ambiente di produzione |Modelli di gestione risorse di Azure possono essere toocreate utilizzati cloni di hello Azure ambiente di produzione (incluse le impostazioni dell'app, modelli di stringa di connessione, scalabilità, e così via) per il test rapido e prevedibile. |
| - Facile visualizzazione del risultato dell'ultima compilazione |TooAzure distribuzione continua da un repository significa che è possibile testare nuovo codice in un'applicazione in tempo reale immediatamente dopo il commit delle modifiche. |
| -Eseguire il commit ramo principale toohello ogni giorno<br>- Automatizzazione della distribuzione |Integrazione continua di un'applicazione di produzione con ramo principale del repository distribuisce automaticamente ogni tooproduction di commit/unione toohello branch principale. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Verrà illustrata una tipica dev-test-fase di produzione del flusso di lavoro in ordine toopublish nuove modifiche toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) applicazione di esempio, costituita da due [le app web](/services/app-service/web/), uno da un front-end (FE) e Hello altro con un back-end Web API (BE) e un [database SQL](/services/sql-database/). Si utilizzeranno hello architettura di distribuzione seguenti:

![](./media/app-service-agile-software-development/what-1-architecture.png)

immagine di hello tooput in parole:

* architettura delle distribuzioni Hello è suddivisa in tre ambienti distinti (o [gruppi di risorse](../azure-resource-manager/resource-group-overview.md) in Azure), ciascuno con il proprio [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [scalabilità](web-sites-scale.md) impostazioni, e il database SQL. 
* Ogni ambiente può essere gestito separatamente. Possono anche essere presenti in sottoscrizioni diverse.
* Gestione temporanea e produzione sono implementati come due slot di hello stessa applicazione di servizio App. ramo master Hello è configurato per l'integrazione continuata con hello slot di staging.
* Quando un ramo toomaster commit viene verificato nei hello slot (con dati di produzione) di gestione temporanea, hello verificata app di gestione temporanea è scambiate nello slot di produzione hello [senza tempi di inattività](web-sites-staged-publishing.md).

Hello ambiente di produzione e gestione temporanea è definito dal modello hello in [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Hello dev e negli ambienti di test sono definiti dal modello hello in [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Strategia di diramazione hello tipico, si utilizzerà inoltre con codice lo spostamento dal branch dev hello backup toohello ramo di test, quindi toohello ramo master (spostando verso l'alto in qualità, toospeak in questo caso).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Elementi necessari
* Un account Azure
* Un account [GitHub](https://github.com/)
* GIT Shell (installato con [GitHub per Windows](https://windows.github.com/))-Abilita si toorun entrambi hello Git e PowerShell i comandi hello stessa sessione 
* Ultimi bit di [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)
* Conoscenza di base di hello seguenti strumenti:
  * Distribuzione di modelli di [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (vedere anche [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> È necessario un account di Azure di toocomplete questa esercitazione:
> 
> * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che consentono è possibile tenere conto di hello e libero di utilizzare servizi di Azure, ad esempio le applicazioni Web.
> * È possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione Visual Studio ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
> 
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="set-up-your-production-environment"></a>Configurare l'ambiente di produzione
> [!NOTE]
> script Hello utilizzato automaticamente in questa esercitazione consente di configurare la pubblicazione continua dall'archivio GitHub. È necessario che le credenziali per GitHub già archiviate in Azure, in caso contrario hello basato su script per distribuzione presenta un errore durante il tentativo di impostazioni di controllo tooconfigure origine per le app web hello. 
> 
> toostore il GitHub credenziali in Azure, creare un'app web in hello [portale di Azure](https://portal.azure.com/) e [configurare la distribuzione di GitHub](app-service-continuous-deployment.md). È necessario solo toodo questo volta. 
> 
> 

In uno scenario tipico DevOps, si dispone di un'applicazione che è in esecuzione in tempo reale in Azure e si desidera toomake modifiche tooit tramite la pubblicazione continua. In questo scenario, è necessario un modello che è sviluppato, testato e utilizzati toodeploy hello ambiente di produzione. che verrà configurato in questa sezione.

1. Creare il propria fork di hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository. Per informazioni sulla creazione della biforcazione, vedere la pagina relativa alla [biforcazione di un repository](https://help.github.com/articles/fork-a-repo/). Una volta creata la biforcazione, è possibile visualizzarla nel browser.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Aprire una sessione di Git Shell. Se non si ha ancora Git Shell, installare [GitHub per Windows](https://windows.github.com/) .
3. Creare un clone locale nel fork eseguendo hello comando seguente:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Dopo aver creato il clone locale, passare troppo*&lt;repository_root >*\ARMTemplates e deploy.ps1 hello esecuzione degli script come indicato di seguito:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Quando richiesto, digitare nome utente hello desiderato e la password per l'accesso al database.
   
   Dovrebbe essere hello provisioning lo stato di avanzamento delle varie risorse di Azure. Al termine del processo di distribuzione, script hello Avvia applicazione hello nel browser hello e fornire un segnale acustico descrittivo.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Dare un'occhiata  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee come genera risorse con un ID univoco. È possibile utilizzare hello stesso approccio toocreate cloni di hello stessa distribuzione senza doversi preoccupare di nomi di risorse in conflitto.
   > 
   > 
6. Tornare alla sessione di Git Shell ed eseguire:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Al termine dell'esecuzione dello script hello, tornare indietro indirizzo del toobrowse toohello server front-end (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee un'applicazione hello in esecuzione nell'ambiente di produzione.
8. Accedi toohello [portale di Azure](https://portal.azure.com/) e diamo un'occhiata a ciò che viene creato.
   
   Dovrebbe essere in grado di toosee due web App in hello stesso gruppo di risorse, uno con hello `Api` suffisso nel nome hello. Se si osserva visualizzazione gruppo risorse di hello, è inoltre possibile visualizzare hello Database SQL e server, hello piano di servizio App e slot di gestione temporanea hello per le app web hello. Esplorare le diverse risorse hello e confrontarle con  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json modo in cui sono configurati nel modello di hello.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Ora impostate hello dell'ambiente di produzione. Successivamente, consente di avviare una nuova applicazione toohello update.

## <a name="create-dev-and-test-branches"></a>Creare i rami di sviluppo e di test
Dopo aver creato un'applicazione complessa in esecuzione nell'ambiente di produzione in Azure, sarà possibile prendere un'applicazione tooyour update in base alle metodologia agile. In questa sezione si creerà hello branch di sviluppo e test che è necessario toomake hello necessario aggiornamenti.

1. Creare innanzitutto l'ambiente di test hello. Nella sessione di Git Shell ambiente hello toocreate per un nuovo ramo denominato i comandi seguenti di esecuzione hello **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Quando richiesto, digitare nome utente hello desiderato e la password per l'accesso al database. 
   
   Al termine del processo di distribuzione, script hello Avvia applicazione hello nel browser hello e fornire un segnale acustico descrittivo. È ora disponibile un nuovo ramo con il proprio ambiente di testing. Richiedere un tooreview momento alcuni aspetti di questo ambiente di test:
   
   * È possibile crearlo in qualsiasi sottoscrizione di Azure. Ciò significa che l'ambiente di produzione hello può essere gestite separatamente dall'ambiente di test.
   * L'ambiente di test è in esecuzione in Azure.
   * Ambiente di test è l'ambiente di produzione toohello identiche, ad eccezione di hello slot di gestione temporanea e hello le impostazioni di scalabilità. Si conosce in quanto sono hello solo ProdandStage.json e differenze DEV.
   * È possibile gestire l'ambiente di test nel piano di servizio app, con un livello di prezzo diverso (ad esempio, **Gratuito**).
   * L'eliminazione di questo ambiente di test è semplice come gruppo di risorse hello di eliminazione. Sono disponibili come toodo questo [in un secondo momento](#delete).
3. Andare toocreate hello di un branch dev eseguendo i comandi seguenti:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Quando richiesto, digitare nome utente hello desiderato e la password per l'accesso al database. 
   
   Richiedere un tooreview momento alcuni aspetti di questo ambiente di sviluppo: 
   
   * L'ambiente di sviluppo è un ambiente di test di configurazione toohello identiche perché è distribuita utilizzando hello stesso modello.
   * È possibile creare nella sottoscrizione di Azure per gli sviluppatori hello, lasciando hello toobe di ambiente di test gestito separatamente ogni ambiente di sviluppo.
   * L'ambiente di sviluppo è in esecuzione in Azure.
   * Ambiente di sviluppo hello di eliminazione è semplice come l'eliminazione gruppo di risorse hello. Sono disponibili come toodo questo [in un secondo momento](#delete).

> [!NOTE]
> Quando si dispone di più sviluppatori che lavorano su nuovo aggiornamento hello, ognuno di essi possa creare facilmente un ramo e l'ambiente di sviluppo dedicato con hello alla procedura seguente:
> 
> 1. Creare i propri divisione del repository hello in GitHub (vedere [dividere un repository](https://help.github.com/articles/fork-a-repo/)).
> 2. Clonare la biforcazione hello sul proprio computer locale
> 3. Eseguire hello stesso comandi toocreate proprio ambiente e il branch dev.
> 
> 

Al termine, la biforcazione GitHub dovrebbe avere tre rami:

![](./media/app-service-agile-software-development/test-1-github-view.png)

E dovrebbero essere presenti sei app Web (tre set di due) in tre gruppi di risorse separati:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json specifica hello toouse ambiente produzione di hello **Standard** tariffario, che è appropriato per la scalabilità dell'applicazione di produzione hello.
> 
> 

## <a name="build-and-test-every-commit"></a>Compilare e testare ogni commit
il file di modello ProdAndStage.json Hello e dev già specificare parametri di controllo origine hello, che per impostazione predefinita consente di impostare la pubblicazione continua per app web hello. Pertanto, ogni ramo GitHub toohello di commit viene attivato un tooAzure di distribuzione automatica da tale branch. Ecco come funziona ora la configurazione.

1. Assicurarsi che hai nel branch Dev hello del repository locale hello. toodo, hello esecuzione comando Git shell seguente:
   
        git checkout Dev
2. Verificare il livello di interfaccia utente dell'applicazione di toohello modifica modificando toouse codice hello [Bootstrap](http://getbootstrap.com/components/) Elenca. Aprire  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml e apportare hello evidenziato modifica seguente:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Se non è possibile leggere hello immagine precedente: 
    > 
    > * Nella riga 18 modificare `check-list` troppo`list-group`.
    > * Nella riga 19 modificare `class="check-list-item"` troppo`class="list-group-item"`.
    > 
    > 
3. Salvare modifiche hello. Nella Shell di Git, eseguire nuovamente hello seguenti comandi:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Questi comandi git sono simili troppo "controllo del codice" in un altro controllo del codice sorgente come TFS. Quando si esegue `git push`, commit nuovo hello attiva un tooAzure push automatica del codice, che consente di ricompilare quindi hello tooreflect hello modifica dell'applicazione nell'ambiente di sviluppo hello.
4. tooverify che si è verificato questo ambiente di sviluppo di codice push tooyour, Vai a pagina dell'app web dell'ambiente di sviluppo tooyour ed esaminare hello **distribuzione** parte. È necessario essere in grado di toosee l'ultimo commit del messaggio non esiste.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Da qui, fare clic su **Sfoglia** toosee hello nuova modifica in un'applicazione hello in tempo reale in Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Si tratta di un'applicazione di toohello modifica secondaria. Tuttavia, molte volte una nuova applicazione web complesse di tooa modifiche hanno effetti collaterali imprevisti e indesiderati. Tooeasily in grado di test da ogni commit nelle compilazioni in tempo reale consente si toocatch questi problemi prima che i clienti visualizzarli.

A questo punto, è necessario familiarità con la realizzazione di hello che, in quanto uno sviluppatore hello **NewUpdate** progetto, è possibile creare un ambiente di sviluppo per se stessi, quindi compilare ogni commit e testare ogni compilazione.

## <a name="merge-code-into-test-environment"></a>Unire il codice nell'ambiente di test
Quando sarai pronto toopush ramo del codice da Dev backup tooNewUpdate branch, è il processo di git standard hello:

1. Consente di unire qualsiasi nuova tooNewUpdate di commit del branch Dev hello in GitHub, ad esempio commit creato da altri sviluppatori. Qualsiasi commit di nuovo su GitHub attiva una compilazione nell'ambiente di sviluppo hello e il push di codice. È possibile verificare che il codice nel branch Dev continui a funzionare con i bit più recenti di hello NewUpdate branch.
2. Unire tutti i nuovi commit del ramo Dev nel ramo NewUpdate in GitHub. Questa azione avvia un push di codice e la compilazione nell'ambiente di test hello. 

Si noti, inoltre, non perché la distribuzione continua è già configurata con questi rami git, è necessario tootake compilazioni di qualsiasi altra azione simile all'esecuzione di integrazione. È sufficiente tooperform origine standard control Objectives usando git e Azure esegue tutti i processi di compilazione hello automaticamente.

A questo punto, si inserisce il codice troppo**NewUpdate** ramo. Nella Shell di Git, eseguire hello seguenti comandi:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

La procedura è terminata. 

Pagina dell'app web toohello passare per il toosee ambiente di test del nuovo commit (unito nel branch NewUpdate) inserito ora toohello ambiente di test. Quindi, fare clic su **Sfoglia** toosee che modifica lo stile di hello è in esecuzione in tempo reale in Azure.

## <a name="deploy-update-tooproduction"></a>Distribuire l'aggiornamento tooproduction
Inserimento di codice toohello ambiente di gestione temporanea e produzione deve essere non differisce le modifiche già apportate quando è inserito l'ambiente di test di codice toohello. È davvero molto semplice. 

Nella Shell di Git, eseguire hello seguenti comandi:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Tenere presente che in base alle modalità di hello ambiente di gestione temporanea e produzione hello viene impostato nel ProdandStage.json, il nuovo codice viene inserito toohello **di gestione temporanea** slot e sia in esecuzione non esiste. Pertanto, se si passa l'URL dello slot gestione temporanea toohello, vedrai nuovo codice hello in esecuzione. toodo, hello esecuzione seguente cmdlet nella Shell di Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

E questo punto, dopo aver verificato aggiornamento hello in hello slot di staging, hello solo cosa toodo a sinistra è tooswap in produzione. In Git Shell, è sufficiente eseguire hello seguenti comandi:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Congratulazioni. È stato pubblicato correttamente una nuova applicazione web di aggiornamento tooyour produzione. Ancora più importante, per eseguire questa operazione è stato sufficiente creare con facilità gli ambienti di sviluppo e di testing e compilare e testare ogni commit. Questi sono gli elementi essenziali per Agile Software Development.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Eliminare gli ambienti di sviluppo e di testing
Poiché deliberatamente di progettazione del dev e gruppi di risorse indipendente toobe ambienti di test, è facile toodelete li. hello toodelete quelli creato in questa esercitazione, i rami di GitHub hello sia elementi di Azure, è sufficiente eseguire hello seguente in Git Shell comandi:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Riepilogo
Lo sviluppo di software Agile è necessaria per molte aziende che desiderano tooadopt Azure come propria piattaforma dell'applicazione. In questa esercitazione, si è appreso come toocreate e tear down repliche esatte o in prossimità di repliche di hello ambiente di produzione con facilità, anche per applicazioni complesse. È stato inoltre la modalità di elaborare questo toocreate possibilità per lo sviluppo di tooleverage cui è possibile compilare e testare ogni singolo commit in Azure. Questa esercitazione è probabilmente illustrato migliore utilizzo di servizio App di Azure e Azure Resource Manager toocreate insieme una soluzione DevOps che soddisfa le metodologie tooagile. Successivamente, è possibile compilare questo scenario eseguendo le tecniche avanzate di DevOps, ad esempio [test in produzione](app-service-web-test-in-production-get-start.md). Per uno scenario comune di test in produzione, vedere [Distribuzione Flighting (test beta) nel servizio di Azure App](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Altre risorse
* [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md)
* [Sviluppo Agile in pratica: suggerimenti e consigli per un ciclo di sviluppo rinnovato](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Strategie di distribuzione avanzate per le app Web di Azure che usano modelli di Gestione risorse](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello Validator JSON](http://jsonlint.com/)
* [ARMClient: impostare toosite pubblicazione GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Diramazione Git - Diramazione e unione di base](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog di David Ebbo](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Strumenti della riga di comando multipiattaforma di Azure](../cli-install-nodejs.md)
* [Creare o modificare utenti in Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Wiki del progetto Kudu](https://github.com/projectkudu/kudu/wiki)

