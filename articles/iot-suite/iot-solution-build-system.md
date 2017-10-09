---
title: 'Esempio di IoT di Azure MyDriving: compilare l''applicazione | Microsoft Docs'
description: "Creazione di un'applicazione che è una dimostrazione completa di come tooarchitect un sistema IoT utilizzando Microsoft Azure, tra cui flusso Analitica, Machine Learning e hub eventi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Compilare e distribuire l'ambiente di hello MyDriving soluzione tooyour
MyDriving è una soluzione di Internet delle cose (IoT) che raccoglie dati dall'automobile, li elabora con Machine Learning e li presenta sul telefono cellulare. back-end Hello è costituito da un'ampia gamma di servizi forniti da Microsoft Azure. i client Hello possono essere telefoni Android, iOS o Windows 10.

Abbiamo creato hello MyDriving soluzione toogive di base per la creazione del proprio sistema IoT. Da hello [MyDriving repository in GitHub](https://github.com/Azure-Samples/MyDriving), è possibile ottenere gli script di gestione risorse di Azure architettura back-end di hello toodeploy nell'account Azure. Da questo punto, può riconfigurare servizi diversi hello, modificare hello query toosuit i propri dati e così via. È possibile trovare questi script, insieme a codice per app per dispositivi mobili hello, il progetto di API di servizio App di Azure hello e altro ancora, nel repository MyDriving hello.

Se non hai ancora provato app hello, esaminare hello [Guida introduttiva Get](iot-solution-get-started.md).

Un account dettagliato dell'architettura di hello in hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs). In sintesi, esistono diverse parti che impostiamo toocreate un progetto simile:

* Un' **app client** viene eseguita su telefoni Android, iOS e Windows 10. Utilizziamo hello Xamarin piattaforma tooshare gran parte del codice hello, che viene archiviato su GitHub in `src/MobileApp`. app Hello eseguirà in realtà due funzioni distinte:
  * L'inoltro di dati di telemetria da dispositivo di hello sistemi diagnostici (OBD) e dal back-end di un proprio percorso servizio toohello sistema cloud.
  * Si tratta di un'interfaccia utente che consente di eseguire query sui dati dei viaggi su strada registrati.
* Oggetto **servizio cloud** inserisce i dati di viaggio hello in tempo reale e lo elabora. Hello principale di creazione di questo servizio è toochoose, parametrizzare e associare un'ampia gamma di servizi di Azure. Alcune delle parti hello richiedono script toofilter dati e processi hello in arrivo. Utilizziamo un tooconfigure modello di gestione risorse di Azure tutte le parti hello.
* Oggetto **servizio mobile app** hello il servizio web protetto da parte dell'interfaccia utente di hello dell'app per dispositivi hello. Il processo principale è database hello tooquery dei dati archiviati, elaborati. Il relativo codice è disponibile su GitHub in `src/MobileAppService`.
* **Visual Studio con Xamarin** . Xamarin, esiste come un componente di Visual Studio e come un ambiente autonomo di sviluppo integrato (IDE), viene utilizzato codice multipiattaforma dispositivo di toobuild hello. codice di iOS toobuild hello, è necessario toohave un'istanza di Xamarin in esecuzione in un computer di OS X. Se necessario, Xamarin può essere eseguito come agente gestito da Visual Studio.
* **Unit test** del dispositivo hello App viene eseguita in Xamarin Test Cloud.
* **GitHub** hello repository in cui vengono archiviati tutti i codice hello, script e i modelli.
* **Visual Studio Team Services** è un servizio cloud utilizzato compilazione continua di toomanage hello e test di hello servizio App web e dispositivi.
* **HockeyApp** è toodistribute utilizzate versioni del codice dispositivo hello. Raccoglie anche report di utilizzo e arresto anomalo e commenti degli utenti.
* **Visual Studio Application Insights** monitoraggi hello servizio web per dispositivi mobili.

Ora verrà esaminata la procedura. 

> [!NOTE] 
> Molte delle hello seguendo i passaggi sono facoltativi.
>
>

## <a name="sign-up-for-accounts"></a>Iscrizione per la creazione di account
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Questo programma gratuito fornisce gli strumenti di sviluppo toomany un accesso semplice e servizi, tra cui Visual Studio, Visual Studio Team Services e Azure. Offre un credito di $ 25 al mese per Azure per dodici mesi. Include anche sottoscrizioni tooPluralsight training e Xamarin University. È anche possibile iscriversi separatamente per accedere ai livelli gratuiti di [Azure](https://azure.com) e [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), che tuttavia non offrono crediti Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (facoltativo) per gestire la distribuzione di test di app per dispositivi mobili e raccogliere dati di telemetria.
* [Xamarin](https://xamarin.com/) (obbligatorio), per la compilazione di esecuzioni di debug e test di app per dispositivi mobili hello e in esecuzione in [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (facoltativo), toocreate repository pubblico disponibile per il proprio codice (repository privati sono a pagamento). In alternativa, è possibile utilizzare piano base hello in Visual Studio Team Services per i repository privati.
* [Power BI](https://powerbi.microsoft.com/) le visualizzazioni dettagliate toocreate (facoltativo), dei dati tra l'intero sistema hello.

> [!NOTE]
> Non è necessario un archivio GitHub tooaccess account hello codice MyDriving [hello repository GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Installare gli strumenti di sviluppo
Hello seguente è per lo sviluppo di soluzioni completa hello: un iOS, Android e Windows 10 Mobile app multipiattaforma, con un Azure back-end.

In alternativa, è possibile utilizzare Xamarin Studio su Mac o Windows toodevelop hello App per dispositivi mobili, se non sono in uso in hello Azure nuovamente terminare.

Vedere qui per una [descrizione più dettagliata di questa configurazione](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Computer di sviluppo Windows
lo strumento centrale Hello in Windows è Visual Studio, per l'utilizzo di hello MyDriving app per Android e Windows, il progetto di API del servizio App hello e le estensioni del microservizio.

Xamarin, Git, emulatori e altri componenti utili sono tutti integrati in Visual Studio.

Installare:

* [Visual Studio con Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (qualsiasi edizione; l'edizione Community è gratuita).
* [SQLite per la piattaforma UWP (Universal Windows Platform)](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Necessario codice di Windows 10 Mobile toobuild hello.
* [Azure SDK per Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Consente di SDK hello per le applicazioni in esecuzione in Azure, insieme agli strumenti da riga di comando per la gestione di Azure.
* [Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Hello obbligatorio toobuild [microservizio](../service-fabric/service-fabric-get-started.md) estensione.

Assicurarsi di disporre di estensioni di Visual Studio destra hello. Verificare che in **Strumenti** siano visualizzati **Android, iOS, Xamarin e così via**. In caso contrario, aprire Visual Studio, eseguire la ricerca di Xamarin e seguire tooinstall prompt hello è. Verificare anche che sia installato **GitHub per Windows**. Se non è, in Visual Studio, effettuare una ricerca e seguire tooinstall prompt hello è. 

### <a name="mac-development-machine"></a>Computer di sviluppo Mac
Hello Mac (Yosemite o versione successiva) è necessario se si desidera toodevelop per iOS. Anche se si usa Visual Studio con Xamarin su Windows toodevelop e gestione tutto il codice hello, Xamarin utilizza un agente installato su un Mac in ordine toobuild e sign hello codice iOS.

![Sviluppare in Windows e compilare in Mac](./media/iot-solution-build-system/image1.png)

(In alternativa, è possibile utilizzare Xamarin Studio direttamente in App multipiattaforma di hello Mac toodevelop.)

Se non si desidera tooinclude iOS come piattaforma di destinazione non è necessario hello Mac.

Installare:

* [Xamarin Studio per iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). È anche possibile configurare Visual Studio e Xamarin in un computer Mac che esegue una macchina virtuale Windows. Vedere [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) su MSDN.
* [Strumenti di sviluppo Azure](https://azure.microsoft.com/downloads/) (facoltativo).

Abilitare l'accesso remoto nell'hello Mac. Aprire **Preferenze di Sistema** > **Condivisione** e quindi selezionare **Account di accesso remoto**.

Quando si apre un progetto iOS in Visual Studio in Windows, hello Xamarin plug-in verrà richiesto per l'ID di hello di hello Mac.

## <a name="fetch-hello-github-repository"></a>Recuperare il repository di GitHub hello
Recuperare una copia locale di [hello repository GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) utilizzando hello **ZIP di Download** pulsante in un altro client Git, GitHub o Visual Studio.

Decomprimere tooa cartella hello con un nome di percorso breve, ad esempio c:\\codice.

In alternativa, se si desidera tookeep backup toodate con o fornire codice tooour, eseguire la clonazione hello repository come indicato di seguito:

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Ottenere una chiave API di Bing Mappe
[Eseguire la registrazione per ottenere una chiave API di Bing Mappe](https://msdn.microsoft.com/library/ff428642.aspx).

È necessario tooreplace di questa riga in 22 `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Compilare app demo hello
In Visual Studio aprire le soluzioni seguenti:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Verranno visualizzati prompt per:

* Considerare attendibili alcuni progetti potenzialmente non attendibili. Scegliere tooopen, se si desidera toogo-ahead.
* Impostare la modalità sviluppatore se si usa un nuovo computer Windows 10.
* Fornire le credenziali Xamarin.
* Connettersi toohello Mac. Xamarin Se non si dispone di un computer Mac, iOS hello rapida del progetto in Visual Studio e quindi selezionare **Scarica progetto**.

Ricompila soluzione hello.

Se si dispone di compilazione di problemi, provare a hello tooquirks di soluzioni che è stata trovata:

* *Non viene caricato il progetto VINLookupApplication*: assicurarsi che sia installato hello [Azure SDK per Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Non compila il progetto Service Fabric*: compilare progetti interfaccia hello innanzitutto e assicurarsi che sia installato hello Service Fabric SDK.
* *L'app per Android non viene compilata*:
  
  * Aprire **Strumenti** > **Android** > **Android SDK Manager** e quindi assicurarsi che la piattaforma Android 6 (API 23)/SDK sia installata.
  * Eliminare questa directory e quindi ricompilare:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Ottenere il codice hello tooknow
Nella soluzione hello, sono disponibili:

* Estensioni di Azure: Service Fabric.
* Azure HDInsight: script per l'elaborazione dei dati di viaggio in Azure.
* App per dispositivi mobili: hello App per dispositivi.
* MobileAppsService/MyDrivingService: terminare web hello nuovamente.
* Power BI: definizione di report hello.
* Scripts:
  
  * Gestione risorse: modelli toobuild hello risorse di Azure.
  * PowerShell: Modelli di gestione risorse hello toorun script.
  * Database SQL di Azure: debug dei database.
* Database SQL: CreateTables: definizioni dello schema.
* Azure flusso Analitica: Esegue una query di trasformazione hello in arrivo del flusso di dati.

## <a name="run-hello-apps-in-development-mode"></a>Eseguire App hello in modalità di sviluppo
Eseguire toorun azione App hello, basata sul dispositivo hello in uso:

* Back-end: MyDrivingService Set come progetto di avvio hello, premere F5 toorun hello back-end servizio. Si aprirà una visualizzazione esplorazione dell'elenco di hello API.
* Client mobili: hello [App per dispositivi mobili vengono sviluppate in Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: per i dettagli, vedere l'articolo relativo al [debug di Android in Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: per i dettagli, vedere l'articolo relativo al [debug in iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: per i dettagli, vedere l'articolo relativo a [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Caricare hello tooHockeyApp di app per dispositivi mobili
HockeyApp gestisce la distribuzione hello gli utenti di tootest app Android, iOS o Windows, la notifica agli utenti di nuove versioni. Raccoglie anche utili segnalazioni di arresti anomali, commenti degli utenti con screenshot e metriche di utilizzo.

[Iniziare caricando](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) l'app compilata. Quindi, eseguire l'accesso troppo[HockeyApp](https://rink.hockeyapp.net) dal computer di sviluppo. Nel dashboard sviluppatore hello, fare clic su **nuova App**, quindi trascinare file hello compilato finestra hello. (In un secondo momento, è possibile automatizzare il toodo servizio di compilazione questo.)

Viene visualizzato il dashboard dell'app.

![Panoramica sul dashboard app hello](./media/iot-solution-build-system/image2.png)

Ripetere il processo di hello per ogni piattaforma per l'app viene eseguita in. Quindi, è possibile eseguire il seguente hello:

* Hello utilizzare [ID app](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) dai dati di arresto anomalo di hello dashboard toosend e commenti e suggerimenti dall'app. In MyDriving, aggiornare gli ID hello in src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Invitare utenti di test](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). È possibile ottenere un toorecruit URL agli utenti di tester. Essi verrà toosign grado per il team, scaricare l'applicazione hello e inviare commenti e suggerimenti.
* Se si preferisce una versione beta più aperta, impostare toopublic distribuzione hello. Fare clic su **Manage App** (Gestisci app) > **Distribution** (Distribuzione) > **Download = Public (Download = Pubblico)**. In questo modo tutti gli utenti possono scaricare l'app e inviare commenti, oltre a visualizzare una notifica quando viene pubblicata una nuova versione, ed è anche possibile ricevere da loro alcune segnalazioni di arresti anomali.
  
   ![Team nel dashboard di hello](./media/iot-solution-build-system/image3.png)
* [Arresto anomalo di collegamento report tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Fare clic su **Manage App** (Gestisci app) > **Visual Studio Team Services**. HockeyApp è in grado di creare automaticamente gli elementi di lavoro in Team Services quando sono presenti segnalazioni di arresti anomali o si ricevono commenti.

Lettura di più, a hello [HockeyApp sito](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Test di app per dispositivi mobili hello in Xamarin Test Cloud
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatizza il test dell'interfaccia utente nei dispositivi reali nel cloud hello. Tramite il framework di NUnit hello, scrivere test che eseguono l'app tramite interfaccia utente di hello.

toouse Xamarin, si incorpora hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK nell'applicazione, è disponibile come pacchetto NuGet. Sono disponibili in app demo hello e è incluso quando si creano nuovi progetti di test con hello modelli di Xamarin.

![Dove toofind hello SDK multipiattaforma sull'interfaccia hello](./media/iot-solution-build-system/image4.png)

Un progetto di test di esempio è incluso in hello app in repository hello. In [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService) cercare in [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Se si usa una compilazione di Visual Studio Team Services, è facile toowrite unità UI Xamarin test ed eseguirli come parte della compilazione.

## <a name="deploy-azure-services"></a>Distribuire servizi di Azure
tooperform una distribuzione automatica di servizi di Azure e servizi di compilazione di Team Services, vedere toohello dettagliate in **scripts/README.md**.

Microsoft Azure offre una vasta gamma di servizi diversi che è possibile utilizzare le applicazioni cloud toobuild. Sebbene molte possono essere utilizzate singolarmente (ad esempio applicazioni di servizio Web e App), ma sono a loro scelta migliore quando si sono stai interconnesse tooform un sistema integrato come quello utilizziamo MyDriving.

È possibile toocreate e interconnessione manualmente i servizi di Azure, ma è molto più veloci e più affidabili i modelli di toouse Gestione risorse di Azure. [Gestione risorse](../azure-resource-manager/resource-group-overview.md) automatizza hello la distribuzione delle risorse di una soluzione e rendendo interconnessioni hello tra di essi.

Sono disponibili per il sistema di MyDriving hello modello hello nel repository GitHub hello in [script/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Fornisce una visualizzazione completa e concisa della modalità di interconnessione tra diversi servizi di hello nell'architettura. Tutti questi elementi in modo dettagliato in hello spiegheremo [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs), ma è possibile ottenere molte semplicemente leggendo modello hello stesso.

> [!NOTE]
> Servizi di Azure più avere un costo associato, a seconda di hello piano tariffario. Se si tooAzure nuova, è possibile [provare gratuitamente](https://azure.microsoft.com/free/). Tuttavia, se non si intende toouse alcuni componenti di sistema MyDriving hello, essere tooremove che li tooavoid i costi di assunzione. sezione "Stima dei costi operativi" Hello più avanti in questo articolo viene fornito un riepilogo delle spese di servizio tipico.
> 
> 

### <a name="edit-hello-template"></a>Modifica modello hello
toocustomize la distribuzione, ad esempio tooremove necessari componenti o tooadd ad altri utenti, innanzitutto copie dello scenario\_complete.params.json e scenario\_complete.json in cui le modifiche toomake.

È possibile utilizzare uno scenario di hello\_complete.params.json file toooverride vari valori predefiniti, ad esempio hello servizio SKU o hello replica tipo di archiviazione, come descritto in hello nella tabella seguente. i valori predefiniti di Hello selezionare le opzioni di costo più basso hello.

| **Parametro** | **Descrizione** | **Valore predefinito** |
| --- | --- | --- |
| SKU per hub IoT |Livello per il servizio hub IoT di Azure |F1 |
| Tipo di account di archiviazione |Tipo di replica di archiviazione |Archiviazione con ridondanza locale Standard |
| Obiettivo del servizio SQL |Utilizzo di slot di concorrenza |DW100 |
| SKU del piano di hosting |Piano di servizio per il servizio app |F1 |

In scenario\_complete.json:

* Cercare "base" e modificarlo tooa nome desiderato.
* Cercare "Create". Ognuna di queste sezioni crea una risorsa.
* Impostare sqlServerAdminLogin e sqlServerAdminPassword toosuitable valori.
* Prima di eliminare una sezione che crea una risorsa, controllare la presenza di dipendenti, cercare il nome in un' posizione nel file hello. Si noti che ogni sezione che crea un servizio include una sezione *dependsOn* che elenca le relative dipendenze.

Ecco il modello di hello Configura. Dettagli inclusi nel hello [Guida di riferimento](http://aka.ms/mydrivingdocs).

| **Servizio** | **Descrizione e dettagli** |
| --- | --- |
| Account di archiviazione |Hello modello consente di creare tre account: |
| -Un database SQL che riceve dati di telemetria aggregati dal flusso Analitica e funge da archivio di backup hello per le tabelle di Azure App Service che espongono i dati tramite gli endpoint dell'API. | |
| -L'archiviazione blob accumula i dati cronologici da un altro processo di flusso Analitica, toobe elaborati da HDInsight. | |
| -   Un database SQL che riceve i risultati elaborati da HDInsight per l'uso con Power BI. | |
| Hub IoT Azure |Stabilisce un dispositivo connesso tooeach di connessione bidirezionale. Nella soluzione MyDriving hello, app per dispositivi mobili hello agisce come un tooAzure di dati toosend gateway campo IoT Hub. IoT Hub Azure funge quindi da un input tooStream Analitica. |
| Hub eventi di Azure |Un output per un processo di flusso Analitica che code hello tooextensions di output creati con Azure Service Fabric. |
| Azure SQL Data Warehouse | |
| Processi di analisi di flusso |La connessione di input e output con una query, ovvero tooaggregate utilizzati dati cronologici e in tempo reale per hello App API dei servizi, Azure Machine Learning, estensioni e Power BI. |
| Area di lavoro di Machine Learning |Include esperimenti, codice R e servizio API. |
| Data factory di Azure |Ripetizione del training di Machine Learning pianificata. |
| Piano di hosting di Service Fabric |Per le estensioni. |
| Servizio app ("App per dispositivi mobili") |Progetto API App Mobile hello host che fornisce gli endpoint hello App per dispositivi mobili. Hello codice API deve essere distribuito tooApp servizio da Visual Studio. |
| Regole di avviso |Invia che posta elettronica se le risposte app hello indicano gli errori. |
| Application Insights |Per il monitoraggio delle prestazioni di hello API nel servizio App. Si ha una connessione hello tooconfigure in Visual Studio. |
| Insieme di credenziali chiave Azure |Per salvare il certificato del cluster del servizio web hello. |

### <a name="run-hello-template"></a>Eseguire il modello di hello
In **scripts/README.md**, sono disponibili istruzioni dettagliate per il modello di hello in esecuzione.

tooprovision tutti questi servizi del proprio account Azure utilizzando uno script di hello, effettuare una delle seguenti hello:

* Usare PowerShell:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *percorso* è hello [località di Azure](https://azure.microsoft.com/regions/), ad esempio `North Europe` o `West US`. Utilizzare `Get-AzureLocation` toofind un elenco dei percorsi disponibili.
  * *resourceGroupName* hello nome che si desidera toogive toohello gruppo appartenenti a tutte le risorse di hello. Quando si è finito di lavorare con le risorse di hello, è possibile eliminare tali tutti insieme tramite l'eliminazione di questo gruppo.
* Eseguire DeploymentScripts/Bash/deploy.sh con Bash.
* Aprire e compilare la soluzione di Visual Studio hello DeploymentScripts/VS/DeployARM.sln.

Si noti che ogni modello hello in fase di esecuzione, viene creato un nuovo set di risorse con i nuovi nomi. risorse hello toodelete, passare toohello portale ed eliminare il gruppo di risorse hello.

Se lo script hello non riesce per qualsiasi motivo, è possibile eseguirla nuovamente.

Consente di script Hello hello opzione di configurazione di integrazione continua in Visual Studio Team Services. Se è stato configurato un progetto Team Services, sarà disponibile un URL https://yourAccountName.visualstudio.com. Immettere l'URL completo di hello quando viene richiesto. È possibile assegnare all'URL un nome nuovo o esistente per un progetto Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Configurare definizioni di compilazione e test in Visual Studio Team Services
In questo progetto viene usato Team Services principalmente per le relative funzionalità di compilazione e test. Offre tuttavia anche un supporto eccellente per la collaborazione, ad esempio la gestione delle attività con le lavagne Kanban, la revisione del codice integrata con le attività e il controllo del codice sorgente e le compilazioni gestite. Si integra bene con altri strumenti, ad esempio GitHub, Xamarin, HockeyApp e naturalmente Visual Studio. È possibile accedervi tramite l'interfaccia web hello o Visual Studio, a seconda del valore è più conveniente in qualsiasi momento.

Hello di passaggi di compilazione hello e definizioni di versione utilizzano un'ampia gamma di plug-in servizi disponibili in hello Team Services [Marketplace](https://marketplace.visualstudio.com/VSTS). In righe di comando toorun utilità toobasic aggiunta o la copia di file, sono presenti servizi che richiamano le compilazioni da altri fornitori, Android e Xamarin e che si connettono tooHockeyApp.

![Opzioni di compilazione in Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definizioni di compilazione
Sono disponibili definizioni di compilazione per ciascuna delle destinazioni di hello principale. Sono anche disponibili varianti per test di funzionalità e di regressione. Le definizioni sono le seguenti:

* MyDriving.Services (hello back-end dell'app web app per dispositivi mobili hello)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android: funzionalità
  * MyDriving.Xamarin.Android: regressione
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS: funzionalità
  * MyDriving.Xamarin.iOS: regressione
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP: funzionalità
  * MyDriving.Xamarin.UWP: regressione

Se si desidera toosee hello dettagli completi la configurazione, vedere la sezione 4.7 di hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs), "Compilazione e configurazione di rilascio". Le funzioni seguono hello stesso modello generale. script Hello:

1. Ripristina pacchetto NuGet hello. È non mantenere il codice compilato nel repository di hello, in modo hello prima di ogni compilazione passaggi hello toorestore necessari pacchetti NuGet.
2. Attiva licenza hello. Hello compilazione viene eseguita nel cloud hello, pertanto, in cui è necessaria una licenza, in particolare, hello - servizio di compilazione Xamarin può essere tooactivate la licenza nel computer di compilazione corrente hello. Quindi, abbiamo disattivarlo immediatamente dopo, tooallow è toobe utilizzato in un altro computer.
3. Compilazioni tramite servizio appropriato hello. Utilizziamo compilazioni Xamarin hello App per dispositivi mobili e Visual Studio viene compilato per il servizio back-end web hello.
4. Compila i test.
5. Esegue i test. Esegui test di app per dispositivi mobili hello nel Xamarin Test Cloud.
6. Pubblica percorso di rilascio toohello risultati compilazione hello.

trigger Hello per le compilazioni principale hello è impostato toocontinuous integration. Compilazione di hello, ovvero viene eseguito ogni volta che viene archiviato il codice nel ramo master toohello.

![Interfaccia in cui il trigger di hello è set toocontinuous integrazione](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definizioni di versione
Definizioni di versione sono configurate in quantità hello stesso modo.

Per il servizio web hello, impostiamo distribuzione come un'app web di Azure:

![Interfaccia per la configurazione della distribuzione come app Web di Azure](./media/iot-solution-build-system/image7.png)

E viene impostato in modo hello rilascio trigger toocontinuous della distribuzione. Ogni archiviazione, seguito da una compilazione corretta risultati in un'app web toohello di aggiornamento.

![Interfaccia per l'impostazione hello rilascio trigger toocontinuous della distribuzione](./media/iot-solution-build-system/image8.png)

App per dispositivi mobili, distribuire tooHockeyApp:

![Interfaccia per la distribuzione di un tooHockeyApp app per dispositivi mobili](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Esplorare i dati di telemetria con Application Insights
[Application Insights](../application-insights/app-insights-overview.md) raccoglie dati di telemetria sull'utilizzo dei servizi web e le prestazioni di hello. Application Insights SDK Hello invia dati di telemetria da hello servizio toohello risorsa di Application Insights in Azure.

Sfoglia risorsa di Application Insights toohello tale modello hello impostato. Non esiste, è possibile esplorare i grafici delle prestazioni hello il [progetto di servizio App Mobile](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Nei grafici sono mostrate le richieste di server e i tempi di risposta, gli errori e i conteggi delle eccezioni. Sono inoltre grafici dipendenza dei tempi di risposta, ovvero database toohello chiamate e tooREST API, ad esempio Machine Learning. Se sono presenti problemi di prestazioni, sarà in grado di toosee sta provocando quale parte del sistema.

![Esempio di grafico delle prestazioni](./media/iot-solution-build-system/image11.png)

Se si dispone di un servizio web configurata manualmente, è facile tooget hello grafici stesso. Nel Pannello di servizio web di hello, fare clic su **strumenti** > **estensioni** > **Aggiungi**. Selezionare **Application Insights**.

![Interfaccia per la selezione di grafici di hello tooget Application Insights](./media/iot-solution-build-system/image12.png)

funzionalità di Hello funziona tramite strumentazione dell'applicazione con hello Application Insights SDK.

È possibile aggiungere dati di telemetria personalizzati (o instrumentare un'applicazione è in esecuzione in un punto qualsiasi all'esterno di Azure) da [aggiunta hello Application Insights SDK](../application-insights/app-insights-asp-net.md) in fase di sviluppo. Questo è utile toolog metriche che dipendono da un'applicazione hello, ad esempio lunghezza media di andata e ritorno degli utenti o al chilometraggio in totale. In Visual Studio, fare clic sul progetto hello e quindi selezionare **Aggiungi Application Insights**.

![Interfaccia per la selezione di dati di telemetria personalizzati tooadd Aggiungi Application Insights](./media/iot-solution-build-system/image10.png)

Application Insights invierà avvisi di posta elettronica se rileva un numero insolito di risposte di errore. È anche possibile impostare avvisi su diverse metriche, ad esempio i tempi di risposta.

Toobe semplicemente che il servizio web è sempre attivo e in esecuzione, è possibile impostare [disponibilità test](../application-insights/app-insights-monitor-web-app-availability.md). Questi test il ping del sito da diverse posizioni in tutto il mondo hello ogni 15 minuti. Nuovamente, verrà visualizzato un messaggio di posta elettronica se ci toobe un problema.

## <a name="estimate-operational-costs"></a>Stimare i costi operativi
È molto basso costo toorun un'app come questa su scala ridotta. Molti dei servizi di hello hanno livelli di base gratuiti, in modo che lo sviluppo e piccole dimensioni operazione costi molto limitata. E, naturalmente, le app non dispone di tutte le funzionalità di hello illustrate in MyDriving toouse.

Ecco una stima approssimativa dei costi per l'impostazione di configurazione di sviluppo hello per MyDriving. Si notino anche alcune alternative che *non* sono state usate. Queste informazioni possono essere utili per la stima dei costi.

Si presuppone quanto segue:

* Un team di non più di cinque membri, ai quali si aggiungono stakeholder che hanno un ruolo di osservatori.
* Esecuzione per circa un mese.
* 100 utenti che effettuano 4 viaggi al giorno.

> [!NOTE]
> Se si tooAzure nuova, è presente un [libero account](https://azure.microsoft.com/free/).
> 
> 

| **Servizio/Componente** | **Note** | **Costo/mese** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) con [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Ambiente di sviluppo multipiattaforma |Visual Studio Community. (Necessario [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) per [xamarin. Forms](https://xamarin.com/forms), toodesign multipiattaforma da una sola codebase.) |$ 0 |
| [Hub IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Toodevices connessione bidirezionale dei dati |8.000 messaggi + 0,5 KB/messaggio gratuiti. |$ 0 |
| [Analisi di flusso](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Elaborazione di volumi elevati di dati del flusso |Costo di $ 0,031 per unità di streaming all'ora, quando è abilitata. Scegliere il numero di hello di unità di streaming che si desidera. tooscale ulteriori backup. |$ 23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Risposte adattive |$ 10/postazione/mese. <br/>                                                                                                                                                                                 + esperimento di 3 ore \* $ 1/ora di esperimento. <br/>                                                                                                                                                           + CPU API da 3,5 ore \* $2/ora di CPU di produzione. <br/>                                                                                                                                                          Il tempo per CPU API presuppone 5 min/giorno di ripetizione del training, anche se questo valore potrebbe aumentare con l'incremento dei dati di input.                   <br/>                                                                                                                                                                     + assegnazione dei punteggi tooprocess 400 trip/giorno 2 min al giorno. |$ 20 |
| [Servizio app](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Host per back-end per dispositivi mobili |Livello B1: app Web di produzione. |$ 56 |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Gestione della compilazione, degli unit test e delle versioni; gestione delle attività |Agenti privati, cinque utenti. |$ 0 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Monitoraggio delle prestazioni e dell'utilizzo di servizi Web e siti |Livello gratuito. |$ 0 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Distribuzione di app beta e raccolta di commenti e dati su utilizzo e arresti anomali |Due app gratuite per i nuovi utenti.<br/> In seguito $ 30/mese. |$ 0 |
| [Xamarin](https://store.xamarin.com/)<br/> Codice su una piattaforma uniforme per più dispositivi |Versione di valutazione gratuita. <br/>In seguito $ 25/mese. |$ 0 |
| [Database SQL](https://azure.microsoft.com/pricing/details/sql-database/) per servizio app di Azure |Piano Basic, modello di database singolo. |$ 5 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (facoltativo) |Consente di eseguire un cluster locale. |$ 0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Visualizzazioni versatili e analisi dei dati di flusso e statici |Livello gratuito: 1 GB, 10.000 righe/ora, aggiornamento giornaliero. <br/> $ 10/utente/mese per [limiti più elevati](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), altre opzioni di connessione, collaborazione. |$ 0 |
| [Archiviazione](https://azure.microsoft.com/pricing/details/storage/) |L (con ridondanza locale) &lt; 100 G $0,024/GB. |$ 3 |
| [Data Factory](https://azure.microsoft.com/pricing/details/data-factory/) |$ 0,60 per attività \* (8-5 FOC). |$ 2 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Cluster on demand per la ripetizione giornaliera del training |Tre nodi A3 a $ 0,32/ora per 1 ora al giorno * 31 giorni. |$ 30 |
| [Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/) |Basic con unità elaborate di $ 11/mese + ingresso $ 0,028. |$ 11 |
| Adattatore OBD | |$ 12 |
| **Totale** | |**$ 157** |

Per altre informazioni, vedere:

* Riepilogo di [limiti e quote dei servizi di Azure](../azure-subscription-service-limits.md#iot-hub-limits)
* [Calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Invio di commenti
Perché abbiamo creato MyDriving toohelp iniziare subito a usare i propri sistemi IoT, si desidera certamente toohear da parte dell'utente, sulle modalità di funzionamento. Indicare se:

* Si sono riscontrate difficoltà o problematiche.
* C'è un punto di estensione che potrebbe renderlo scenario tooyour più adatto.
* Trovare un tooaccomplish modo più efficiente determinate esigenze.
* Si hanno altri suggerimenti per migliorare MyDriving o questa documentazione.

commenti e suggerimenti toogive, [problema su GitHub] del file o lasciare un commento di seguito (en-us edition).

Saremo lieti toohearing da parte dell'utente.

## <a name="next-steps"></a>Passaggi successivi
Si consiglia di hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs), che è una descrizione completa di progettazione di hello del sistema hello e i relativi componenti.

