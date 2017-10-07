---
title: recapito aaaContinuous per cloud services con TFS in Azure | Documenti Microsoft
description: Informazioni su come App cloud tooset le opzioni di distribuzione continua per Azure. Esempi di codice Code per istruzioni della riga di comando MSBuild e script di PowerShell.
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Recapito continuo per Servizi cloud in Azure
Hello processo descritto in questo articolo illustra come tooset le opzioni di distribuzione continua per le applicazioni cloud di Azure. Questo processo consente di creare automaticamente i pacchetti e distribuire hello pacchetto tooAzure dopo ogni archiviazione codice. il processo di compilazione pacchetto descritto in questo articolo Hello è equivalente toohello **pacchetto** comandi di Visual Studio e la procedura per la pubblicazione è equivalente toohello **pubblica** comando in Visual Studio.
Hello articolo include informazioni su hello metodi utilizzare toocreate un server di compilazione con le istruzioni della riga di comando di MSBuild e script di Windows PowerShell e viene inoltre illustrato come toooptionally configurare Visual Studio Team Foundation Server - definizioni di compilazione Team i comandi di MSBuild hello toouse e gli script di PowerShell. il processo di Hello è personalizzabile per gli ambienti di Azure di destinazione e l'ambiente di compilazione.

È inoltre possibile utilizzare Visual Studio Team Services, una versione di TFS che è ospitato in Azure, toodo questo più facilmente. 

Prima di iniziare, pubblicare l'applicazione da Visual Studio.
Ciò garantisce che tutte le risorse di hello siano disponibili e inizializzato quando si tenta di processo di pubblicazione tooautomate hello.

## <a name="1-configure-hello-build-server"></a>1: configurare hello Build Server
Prima di creare un pacchetto Azure utilizzando MSBuild, è necessario installare il software necessario hello e gli strumenti nel server di compilazione hello.

Visual Studio non è necessario toobe installato nel server di compilazione hello. Se si desidera toouse servizio Team Foundation Build toomanage il server di compilazione, seguire le istruzioni hello hello [servizio Team Foundation Build] [ Team Foundation Build Service] documentazione.

1. Nel server di compilazione hello, installare hello [.NET Framework 4.5.2][.NET Framework 4.5.2], che include MSBuild.
2. Installare più recente hello [gli strumenti di creazione di Azure per .NET](https://azure.microsoft.com/develop/net/).
3. Installare hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Server di compilazione copia del file WebApplication hello da un toohello di installazione di Visual Studio.

   In un computer con installato Visual Studio, questo file si trova nella directory hello c:\\programmi (x86)\\MSBuild\\Microsoft\\VisualStudio\\v 14.0\\WebApplications. È necessario copiarlo toohello stessa directory nel server di compilazione hello.
5. Installare hello [strumenti di Azure per Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2: Compilare un pacchetto usando i comandi MSBuild
In questa sezione viene descritto come tooconstruct un MSBuild comando che compila un pacchetto di Azure. Eseguire questo passaggio in hello tooverify server di compilazione che tutto è configurato correttamente e che il comando di MSBuild hello consente di eseguire le operazioni desiderate toodo. È possibile aggiungere tooexisting questa riga di comando script o compilano sui server di compilazione hello, è possibile utilizzare la riga di comando hello in una definizione di compilazione TFS, come descritto nella sezione successiva hello. Per altre informazioni sui parametri della riga di comando e su MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Se Visual Studio è installato nel server di compilazione hello, individuare e selezionare **prompt dei comandi di Visual Studio** in hello **Visual Studio Tools** cartella Windows.

   Se Visual Studio non è installato nel server di compilazione hello, aprire un prompt dei comandi e assicurarsi che sia accessibile nel percorso di MSBuild.exe. MSBuild viene installato con .NET Framework Ciao hello percorso % WINDIR %\\Microsoft.NET\\Framework\\*versione*. Ad esempio, per aggiungere variabile di ambiente PATH di MSBuild.exe toohello dopo aver installato .NET Framework 4, digitare hello comando al prompt dei comandi di hello seguente:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. Al prompt dei comandi di hello, spostarsi sulla cartella toohello contenente il file di progetto Azure che si desidera toobuild.
3. Eseguire MSBuild con hello /target: opzione come hello di esempio seguente per la pubblicazione:

       MSBuild /target:Publish

   Per questa opzione è possibile usare la sintassi abbreviata /t:Publish. opzione /t:Publish Hello in MSBuild non deve essere confuso con i comandi di pubblicazione hello disponibili in Visual Studio quando si dispone di hello che Azure SDK installato. Hello /t: opzione per la pubblicazione solo le compilazioni hello Azure pacchetti. Non è possibile distribuire i pacchetti hello come comandi pubblica hello in Visual Studio.

   Facoltativamente, è possibile specificare il nome di progetto hello come parametro di MSBuild. Se non specificato, viene utilizzata la directory corrente di hello. Per altre informazioni sulle opzioni della riga di comando di MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Individuare l'output di hello. Per impostazione predefinita, questo comando crea una directory nella cartella radice toohello di relazione per il progetto di hello, ad esempio *ProjectDir*\\bin\\*configurazione* \\ app.publish\\. Quando si compila un progetto Azure, si genera due file: hello file del pacchetto e hello che accompagna i file di configurazione:

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   Per impostazione predefinita, ogni progetto Azure include un file di configurazione del servizio (file con estensione cscfg) per compilazioni locali (debug) e un altro per le compilazioni nel cloud (gestione temporanea o produzione), ma è possibile aggiungere o rimuovere file di configurazione del servizio in base alle necessità. Quando si compila un pacchetto all'interno di Visual Studio, verrà richiesto quale tooinclude file di configurazione del servizio insieme ai pacchetti hello.
5. Specificare il file di configurazione servizio hello. Quando si compila un pacchetto utilizzando MSBuild, i file di configurazione di servizio locale hello è incluso per impostazione predefinita. tooinclude un file di configurazione del servizio diverso, impostare la proprietà TargetProfile del comando di MSBuild hello, come in hello di esempio seguente:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Specificare il percorso di hello per l'output di hello. Imposta percorso hello utilizzando i /p: PublishDir =*Directory* \\ opzione, tra cui hello separatore barra rovesciata, come l'esempio seguente hello finale:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Dopo avere creato e testato un appropriato MSBuild toobuild riga di comando dei progetti e combinarli in un pacchetto di Azure, è possibile aggiungere script di compilazione tooyour questa riga di comando. Se il server di compilazione usa script personalizzati, questo processo dipende dalle specifiche del processo personalizzato di compilazione. Se si usa TFS come un ambiente di compilazione, quindi è possibile seguire le istruzioni hello hello passaggio successivo del processo di compilazione tooyour tooadd hello Azure pacchetto compilazione.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: Compilare un pacchetto usando TFS Team Build
Se dispone di Team Foundation Server (TFS) impostato come server di compilazione di un controller di compilazione e hello impostato come un computer di compilazione TFS, quindi è possibile facoltativamente configurare una compilazione automatica per il pacchetto di Azure. Per informazioni su come tooset backup e utilizzare Team Foundation server come un sistema di compilazione, vedere [scalabilità del sistema di compilazione][Scale out your build system]. In particolare, la procedura seguente si presuppone che il server di compilazione è stato configurato come descritto in [distribuire e configurare un server di compilazione][Deploy and configure a build server], e che hanno creato un progetto team, creare un cloud progetto di servizio nel progetto team hello.

tooconfigure TFS toobuild Azure pacchetti, eseguire hello alla procedura seguente:

1. In Visual Studio nel computer di sviluppo, nel menu Visualizza di hello, scegliere **Team Explorer**, oppure scegliere Ctrl +\\, Ctrl + M. Nella finestra Team Explorer, espandere hello **compilazioni** nodo oppure scegliere hello **compilazioni** , quindi selezionare **nuova definizione di compilazione**.

   ![Opzione Nuova definizione di compilazione][0]
2. Scegliere hello **Trigger** scheda e specificare hello desiderate le condizioni per cui si desidera hello toobe pacchetto generato. Ad esempio, specificare **integrazione continua** si verifica il pacchetto hello toobuild ogni volta che un controllo origine check-in.
3. Scegliere hello **le impostazioni dell'origine** scheda e assicurarsi che la cartella del progetto sia elencata in hello **cartella del codice sorgente** colonna, senza che sia stato hello **Active**.
4. Scegliere hello **impostazioni predefinite compilazione** e controller di compilazione, verificare il nome di hello del server di compilazione hello.  Inoltre, scegliere l'opzione hello **operazioni seguenti toohello output di compilazione Copia cartella di ricezione** e specificare il percorso di rilascio hello desiderato.
5. Scegliere hello **processo** scheda. Nella scheda processo hello scegliere modello predefinito hello in **compilare**, scegliere il progetto di hello se non è già selezionata, espandere hello **avanzate** sezione hello **compilare**sezione della griglia hello.
6. Scegliere **argomenti MSBuild**e impostare gli argomenti della riga di comando MSBuild appropriati hello, come descritto nel passaggio 2 precedente. Ad esempio, immettere **/t: pubblicare /p: PublishDir =\\\\myserver\\Elimina\\**  toohello percorso dei file di un pacchetto di hello pacchetto e copia toobuild \\ \\myserver\\Elimina\\:

   ![Argomenti MSBuild][2]

   > [!NOTE]
   > Copia tooa file hello condivisione pubblica rende più semplice toomanually distribuire i pacchetti hello dal computer di sviluppo.
7. Test successo hello dell'istruzione di compilazione mediante il controllo in un progetto tooyour modifica o una nuova compilazione accodati. tooqueue di una nuova compilazione, in Team Explorer, fare doppio clic su **tutte le definizioni di compilazione,** e quindi scegliere **Accoda nuova compilazione**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: Pubblicare un pacchetto usando uno script PowerShell
In questa sezione viene descritto come uno script di Windows PowerShell per la pubblicazione del pacchetto di app Cloud hello tooconstruct output tooAzure utilizzando i parametri facoltativi. Questo script può essere chiamato dopo la compilazione hello passaggio in automazione di compilazione personalizzata. È possibile chiamare lo script anche da attività del flusso di lavoro del modello di processo in Visual Studio TFS Team Build.

1. Installare hello [cmdlet di Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 o versione successiva).
   Durante la fase di installazione di cmdlet hello, scegliere tooinstall come uno snap-in. Si noti che questa versione supportata ufficialmente sostituisce versione precedente di hello è disponibile in CodePlex, anche se le versioni precedenti di hello numero 2.
2. Avviare PowerShell di Azure utilizzando il menu di avvio hello o alla pagina iniziale. Se si avvia in questo modo, verrà caricato hello cmdlet di Azure PowerShell.
3. Al prompt dei comandi PowerShell hello, verificare che i cmdlet di PowerShell hello vengono caricati con comando parziale hello `Get-Azure` e quindi premere il tasto Tab per il completamento delle istruzioni di hello.

   Se si preme tasto Tab hello ripetutamente, vedrai vari comandi di PowerShell di Azure.
4. Verificare che sia possibile connettersi tooyour sottoscrizione di Azure importando le informazioni di sottoscrizione da file con estensione publishsettings hello.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Quindi immettere il comando hello

   `Get-AzureSubscription`

   Vengono visualizzate le informazioni relative alla sottoscrizione. Verificarne la correttezza.
5. Salvare il modello di script hello fornito alla fine di hello di questo articolo per la cartella di script come c:\\script\\Azure\\**PublishCloudService.ps1**.
6. Nella sezione hello parametri dello script hello. Aggiungere o modificare i valori predefiniti. Questi valori possono sempre essere sostituiti mediante il passaggio di parametri espliciti.
7. Verificare che esistono in modo univoco il servizio cloud valido e gli account di archiviazione creati nella sottoscrizione che può essere la destinazione hello dello script di pubblicazione. L'account di archiviazione (archiviazione blob) verrà utilizzato tooupload e archiviare temporaneamente i file di pacchetto e i file di configurazione della distribuzione hello durante la creazione della distribuzione.

   * toocreate un nuovo servizio cloud, è possibile chiamare questo script o l'utilizzo di hello [portale di Azure](https://portal.azure.com). nome del servizio cloud Hello verrà utilizzato come un prefisso in un nome di dominio completo e pertanto deve essere univoco.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate un nuovo account di archiviazione, è possibile chiamare questo script o l'utilizzo di hello [portale di Azure](https://portal.azure.com). nome account di archiviazione Hello verrà utilizzato come un prefisso in un nome di dominio completo e pertanto deve essere univoco. È possibile provare a utilizzare hello stesso nome del servizio cloud.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Chiamare lo script hello direttamente da Azure PowerShell o associare questa automazione toooccur generazione di script tooyour host dopo la compilazione del pacchetto hello.

   > [!IMPORTANT]
   > script Hello sempre eliminerà o sostituire le distribuzioni esistenti per impostazione predefinita, se vengono rilevati. Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente.
   >
   >

   **Scenario di esempio 1:** toohello distribuzione continua l'ambiente di un servizio di gestione temporanea:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Questo è in genere seguito da verifica tramite esecuzione di test e da uno scambio di indirizzi VIP. scambio VIP Hello può essere eseguito tramite hello [portale di Azure](https://portal.azure.com) o con cmdlet hello Move-distribuzione.

   **Scenario di esempio 2:** ambiente di produzione toohello distribuzione continua di un servizio di test dedicato

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Desktop remoto:**

   Se Desktop remoto sia abilitato nel progetto Azure, è necessario tooperform ulteriori passaggi monouso hello tooensure che corretto certificato del servizio Cloud è caricato tooall servizi di cloud di destinazione da questo script.

   Individuare i valori di identificazione personale certificato hello previsti dai ruoli. I valori di identificazione personale sono visibili nella sezione relativa ai certificati hello del file di configurazione cloud (ad esempio ServiceConfiguration). È inoltre visibile nella finestra di dialogo Configurazione Desktop remoto hello in Visual Studio quando si hello Mostra opzioni e di visualizzazione selezionato alcun certificato.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Caricare i certificati di Desktop remoto come un passaggio di installazione singola utilizzando hello lo script di cmdlet seguente:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   ad esempio:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   In alternativa è possibile esportare il file di certificato hello PFX con chiave privata e caricare i certificati tooeach servizio di destinazione cloud con il [portale di Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Aggiorna distribuzione ed Elimina distribuzione -** Nuova distribuzione\>

   Hello script per impostazione predefinita esegue un aggiornamento della distribuzione ($enableDeploymentUpgrade = 1) quando non viene passato alcun parametro o il valore 1 viene passato in modo esplicito. Per singole istanze, questo ha il vantaggio di richiedere meno tempo rispetto a una distribuzione completa. Per le istanze che richiedono disponibilità elevata, che ciò presenta inoltre il vantaggio di hello di lasciare alcune istanze in esecuzione mentre altri vengono aggiornate (esame del dominio di aggiornamento), nonché il VIP non verrà eliminato.

   Distribuzione dell'aggiornamento può essere disabilitata in script hello ($enableDeploymentUpgrade = 0) o passando *- enableDeploymentUpgrade 0* come parametro, che modifica l'eliminazione di script comportamento toofirst qualsiasi distribuzione esistente e quindi creare un nuova distribuzione.

   > [!IMPORTANT]
   > script Hello sempre eliminerà o sostituire le distribuzioni esistenti per impostazione predefinita, se vengono rilevati. Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente/operatore.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: Pubblicare un pacchetto usando TFS Team Build
Questo passaggio facoltativo si connette a Team di TFS Build toohello script creato nel passaggio 4, che gestisce la pubblicazione di hello pacchetto compilazione tooAzure. Ciò comporta hello modifica modello di processo usato per la definizione di compilazione in modo che venga eseguito un'attività di pubblicazione alla fine del flusso di lavoro hello hello. Hello pubblica attività eseguirà il comando di PowerShell passando i parametri dalla compilazione hello. Nell'output di compilazione standard di hello verrà inoltrato tramite pipe l'output di hello ha come destinazione di MSBuild e script di pubblicazione.

1. Modifica hello responsabile della definizione di compilazione continua distribuire.
2. Seleziona hello **processo** scheda.
3. Seguire [queste istruzioni](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un progetto di attività per hello modello di processo di compilazione, scaricare il modello predefinito di hello, aggiungerlo al progetto hello e archiviarlo. Assegnare un nuovo nome, ad esempio AzureBuildProcessTemplate di modello di processo di compilazione hello.
4. Restituire toohello **processo** scheda e utilizzare **Mostra dettagli** tooshow un elenco dei modelli di processo di compilazione disponibile. Scegliere hello **New...**  pulsante e passare toohello progetto appena aggiunto e archiviato. Individuare il modello di hello appena creato e scegliere **OK**.
5. Aprire hello selezionato del modello di processo per la modifica. È possibile aprire direttamente nella finestra di progettazione del flusso di lavoro hello o toowork editor XML di hello con hello XAML.
6. Aggiungere hello seguente elenco di nuovi argomenti come elementi distinti di riga nella scheda argomenti hello della finestra di progettazione del flusso di lavoro hello. Tutti gli argomenti devono presentare direction=In e type=String. Questi saranno i parametri utilizzati tooflow dalla definizione di compilazione hello in hello del flusso di lavoro, che quindi hello toocall utilizzato get dello script di pubblicazione.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Elenco di argomenti][3]

   Hello che XAML corrispondente è simile al seguente:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Aggiungere una nuova sequenza alla fine hello Esegui su agente:

   1. Per iniziare, aggiungere un toocheck attività istruzione If per un file di script valido. Impostare il valore toothis della condizione hello:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. In hello quindi i case di hello istruzione If, aggiungere una nuova attività di sequenza. Pubblicare set hello visualizzazione nome too'Start'
   3. Con hello inizio pubblicare sequenza ancora selezionato, aggiungere il seguente elenco di nuove variabili come elementi distinti di riga nella scheda variabili della finestra di progettazione del flusso di lavoro hello. Tutte le variabili presentare Variable type =String e Scope=Start publish. Questi saranno i parametri utilizzati tooflow dalla definizione di compilazione hello nel flusso di lavoro, che quindi hello toocall utilizzato get dello script di pubblicazione.

      * SubscriptionDataFilePath, di tipo String
      * PublishScriptFilePath, di tipo String

        ![Nuove variabili][4]
   4. Se si usa TFS 2012 o versioni precedenti, aggiungere un'attività di ConvertWorkspaceItem inizio hello hello nuova sequenza. Se si usa TFS 2013 o versioni successive, è possibile aggiungere un'attività GetLocalPath all'inizio di hello della nuova sequenza di hello. Per un ConvertWorkspaceItem, impostare la proprietà hello come segue: direzione = ServerToLocal, DisplayName = 'Convert publish nome file di script,' Input 'PublishScriptLocation', risultato = = 'PublishScriptFilePath', area di lavoro = 'Area di lavoro'. Per un'attività GetLocalPath, impostare hello proprietà IncomingPath too'PublishScriptLocation', e hello too'PublishScriptFilePath risultati '. Questo percorso toohello di attività converte hello script da percorsi di TFS server di pubblicazione (se applicabile) percorso del disco locale standard tooa.
   5. Se si usa TFS 2012 o versioni precedenti, aggiungere un'altra attività di ConvertWorkspaceItem alla fine hello hello nuova sequenza. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. Se si usa TFS 2013 o versione successiva, aggiungere un'altra attività GetLocalPath. IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'
   6. Aggiungere un'attività InvokeProcess alla fine hello hello nuova sequenza.
      Questo chiama attività PowerShell.exe con argomenti hello passato dal hello definizione di compilazione.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Execute publish script
      + FileName = "PowerShell" (che includono le offerte di hello)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. In hello **Gestisci Output Standard** sezione casella di testo del InvokeProcess, impostare hello casella di testo valore too'data'. Si tratta di dati di output standard una variabile toostore hello.
   8. Aggiungere un'attività WriteBuildMessage di sotto hello **Gestisci Output Standard** sezione. Impostare hello importanza = 'BuildMessageImportance' e messaggio hello = 'data'. In questo modo l'output standard di hello dello script verranno scritte toohello l'output di compilazione.
   9. In hello **Gestisci Output errore** sezione casella di testo del InvokeProcess, impostare hello casella di testo valore too'data'. Si tratta di un dati di errore standard hello toostore variabile.
   10. Aggiungere un'attività WriteBuildError sotto hello **Gestisci Output errore** sezione. Impostare hello messaggio = 'data'. In questo modo verranno scritti hello standard errori di script hello output degli errori di compilazione toohello.
   11. Correggere eventuali errori, indicati da punti esclamativi blu. Passare il puntatore di tooget punti esclamativi un suggerimento su errore hello. Salva flusso di lavoro di hello per cancellare gli errori.

   risultato finale di Hello di hello pubblicazione del flusso di lavoro attività saranno simile al seguente nella finestra di progettazione hello:

   ![Attività flusso di lavoro][5]

   risultato finale di Hello di hello pubblicare attività saranno simile al seguente in XAML del flusso di lavoro:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Salvare un flusso di lavoro modello processo compilazione hello e archivia il file.
9. Modificare la definizione di compilazione hello (chiuderla se è già aperto) e seleziona hello **New** pulsante se non viene ancora visualizzato nuovo modello di hello nell'elenco di hello dei modelli di processo.
10. Impostare i valori delle proprietà parametro hello hello sezione varie nel modo seguente:

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Questo valore deriva da: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Questo valore deriva da: ($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *utilizzare hello appropriato nome del servizio cloud qui*
    5. Environment = 'Staging'
    6. StorageAccountName = 'mystorageaccountname' *nome account di uso hello appropriato archiviazione qui*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![Valori delle proprietà dei parametri][6]
11. Salvare le modifiche di hello toohello definizione di compilazione.
12. Accodare una compilazione tooexecute entrambi hello build del pacchetto e pubblicare. Se si dispone di un trigger tooContinuous integrazione impostato, questo comportamento verrà eseguita a ogni archiviazione.

### <a name="publishcloudserviceps1-script-template"></a>Modello di script PublishCloudService.ps1
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Passaggi successivi
debug remoto tooenable quando si utilizza il recapito continuo, vedere [abilitare il debug remoto quando si utilizza il recapito continuo toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
