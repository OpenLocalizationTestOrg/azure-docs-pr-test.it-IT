---
title: Automation DSC la distribuzione continua con Chocolatey aaaAzure | Documenti Microsoft
description: Distribuzione continua in DevOps con Gestione pacchetti di Automation DSC per Azure e Chocolatey.  Esempio con modello ARM JSON completo e codice sorgente di PowerShell.
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Esempio di utilizzo: La distribuzione continua tooVirtual macchine tramite DSC di automazione e Chocolatey
In un mondo DevOps sono disponibili molti strumenti tooassist con vari punti nella pipeline di integrazione continua hello.  Configurazione dello stato desiderato di automazione di Azure (DSC) è un nuovo aggiunta toohello le opzioni di installazione in grado di utilizzare i team DevOps.  Questo articolo illustra come configurare la distribuzione continua per un computer Windows.  È possibile estendere facilmente hello tecnica tooinclude tutti i computer Windows in base alle esigenze nel ruolo hello (ad esempio un sito web) e da tooadditional sono anche i ruoli.

![Distribuzione continua con VM IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>A livello generale
Gli aspetti da considerare sono molteplici, ma possono comunque essere suddivisi in due processi principali: 

* Scrittura di codice e test, creazione e pubblicazione di pacchetti di installazione per le versioni principale e secondaria del sistema hello. 
* Creazione e gestione di macchine virtuali che verranno installati e di eseguire codice hello in pacchetti hello.  

Quando entrambi i processi principali sono presenti, passaggio breve tooautomatically hello pacchetto di aggiornamento sia in esecuzione su qualsiasi determinata macchina virtuale come nuove versioni create e distribuite.

## <a name="component-overview"></a>Panoramica dei componenti
Creare un pacchetto, ad esempio gestori di [apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) sono molto ben noti in Linux HelloWorld, ma non tanto in ambito Windows hello.  [Chocolatey](https://chocolatey.org/) è tale aspetto e di Scott Hanselman [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) su hello argomento è un'ottima introduzione.  In breve, Chocolatey consente tooinstall pacchetti da un repository centrale dei pacchetti in un sistema di Windows tramite riga di comando hello.  È possibile creare e gestire un repository personalizzato e Chocolatey può installare pacchetti da tutti i repository designati dall'utente.

Desired State Configuration (DSC) ([Panoramica](https://technet.microsoft.com/library/dn249912.aspx)) è uno strumento di PowerShell che consente una configurazione di hello toodeclare desiderata per una macchina.  Si può ad esempio dichiarare di voler installare Chocolatey o IIS, di voler aprire la porta 80 e di voler installare la versione 1.0.0 del proprio sito Web.  Hello DSC Gestione configurazione locale (LCM) implementa la configurazione. Un server di pull DSC mantiene un repository di configurazioni per i computer dell'utente. Hello Gestione configurazione locale in ogni computer archivia toosee periodicamente se la configurazione corrisponde la configurazione archiviata hello. Può segnalare lo stato o tentare macchina hello toobring in allineamento con la configurazione archiviata hello. È possibile modificare hello configurazione archiviata nel hello pull server toocause un computer o un set di macchine toocome in allineamento con configurazione hello modificato.

Automazione di Azure è un servizio gestito in Microsoft Azure che consente di tooautomate varie attività con i runbook, i nodi, le credenziali, risorse e risorse, ad esempio le pianificazioni e le variabili globali. DSC di automazione di Azure estende questa automazione strumenti di PowerShell DSC tooinclude funzionalità.  Ecco un'interessante [panoramica](automation-dsc-overview.md).

Una risorsa DSC è un modulo di codice con funzionalità specifiche, ad esempio per la gestione della rete, di Active Directory o SQL Server.  Hello Chocolatey risorsa DSC, nota come tooaccess un NuGet Server (tra gli altri), scaricare i pacchetti, installare i pacchetti e così via.  Sono disponibili molte altre risorse DSC in hello [PowerShell Gallery](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Questi moduli vengono installati dall'utente nel server di pull di Automation DSC per Azure, per poter essere usati nelle configurazioni personalizzate.

I modelli di Resource Manager offrono un modo dichiarativo per la generazione dell'infrastruttura, ad esempio reti, subnet, routing e sicurezza di rete, servizi di bilanciamento del carico, NIC, VM e così via.  Ecco un [articolo](../azure-resource-manager/resource-manager-deployment-model.md) che confronta hello modello di distribuzione di gestione risorse (dichiarativo) con hello Azure Service Management (ASM o classica) la distribuzione del modello (imperativo) e vengono illustrati risorse principali hello provider, calcolo, archiviazione e rete.

Una caratteristica fondamentale di un modello di gestione risorse è relativo tooinstall possibilità un'estensione della macchina virtuale nella macchina virtuale hello è disponibile.  Un'estensione VM include funzionalità specifiche, come l'esecuzione di uno script personalizzato, l'installazione di software antivirus o l'esecuzione di uno script di configurazione DSC.  Sono disponibili molti altri tipi di estensioni VM.

## <a name="quick-trip-around-hello-diagram"></a>Rapido viaggi diagramma hello
A partire dalla parte superiore di hello, la scrittura del codice, compilare e testare, quindi creare un pacchetto di installazione.  Chocolatey può gestire diversi tipi di pacchetti di installazione, ad esempio MSI, MSU, ZIP.  E si dispone di potenza hello di installazione di PowerShell toodo hello effettivo se alle funzionalità native del Chocolatey non sono abbastanza alto tooit.  Inserire i pacchetti hello in identificabile raggiungibile: un repository di pacchetti.  Questo esempio di utilizzo usa una cartella pubblica in un account di archiviazione BLOB di Azure, ma può trovarsi anche in un'altra posizione.  Chocolatey funziona in modalità nativa con i server NuGet e alcuni altri per la gestione dei metadati dei pacchetti.  [In questo articolo](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) vengono descritte le opzioni di hello.  Questo esempio di utilizzo usa NuGet.  Nuspec sono i metadati relativi ai pacchetti.  Nuspec Hello "compilazione" in NuPkg e archiviati in un server NuGet.  Quando la configurazione richiede un pacchetto in base al nome e fa riferimento a un server NuGet, hello Chocolatey risorsa DSC (ora su hello VM) acquisisce pacchetto hello e lo installa automaticamente.  È anche possibile richiedere una versione specifica di un pacchetto.

Hello a sinistra nella parte inferiore dell'immagine di hello, prevede un modello di Azure Resource Manager (ARM).  In questo esempio di utilizzo, hello estensione della macchina virtuale registra hello VM con hello Azure Server di Pull DSC di automazione (ovvero, un server di pull) come un nodo.  configurazione di Hello viene archiviata nel server di pull hello.  In realtà viene archiviata due volte, cioè una volta come testo normale e una volta compilata come file MOF, un'indicazione per coloro che hanno familiarità con questi elementi.  Nel portale di hello hello MOF è una configurazione"nodi" (come toosimply anziché "configurazione").  Di hello artefatto associato a un nodo in modo nodo hello riconoscerà la relativa configurazione.  I dettagli di seguito mostrano come tooassign hello toohello nodo configurazione.

Probabilmente si sta già eseguendo bit hello nella parte superiore di hello o la maggior parte di esso.  Creazione di hello nuspec, la compilazione e archiviare i dati in un server NuGet è una piccola cosa.  e si stanno già gestendo le VM.  Tenendo hello successivo passaggio toocontinuous distribuzione richiede l'impostazione server di pull hello (una volta), registrazione i nodi con esso () e la creazione e archiviazione sono configurazione hello (inizialmente).  Aggiornare quindi i pacchetti vengono aggiornati e distribuiti toohello repository, hello configurazione e configurazione di un nodo nel server di pull hello (ripetizione in base alle necessità).

Il procedimento funziona anche se non si inizia con un modello ARM.  Esistono PowerShell cmdlet progettati toohelp registrare le macchine virtuali con server di pull hello e tutte le restanti hello. Per altre informazioni dettagliate, vedere l'articolo [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Passaggio 1: Impostazione di account di automazione e i server di pull hello
In una riga di comando di PowerShell (Add-AzureRmAccount) autenticata: (può richiedere alcuni minuti mentre viene configurato il server di pull hello)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

È possibile inserire l'account di automazione in una delle seguenti aree (detto anche percorso) hello: Stati Uniti orientali 2, centro-meridionali, ci Gov Virginia, Europa occidentale, Asia sudorientale, Giappone orientale, India centrale e Australia sudorientale, centrale Canada, Europa settentrionale.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Passaggio 2: Modello ARM toohello di modifiche per estensione della macchina virtuale
Dettagli per la registrazione della macchina virtuale (con estensione VM DSC PowerShell hello) forniti in questo [il modello di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Questo passaggio registra la nuova macchina virtuale con il server di pull hello nell'elenco di hello dei nodi DSC.  Parte di questa registrazione specificano hello nodo Configurazione toohello toobe applicato.  Questa configurazione del nodo non ha tooexist ancora nel server di pull hello, pertanto è OK di passaggio 4 in cui questa operazione viene eseguita per hello prima volta.  Ma nel passaggio 2 di seguito è necessario nome hello deciso toohave del nodo hello e il nome di hello della configurazione di hello.  In questo esempio di utilizzo, nodo hello è 'isvbox' e la configurazione di hello è 'ISVBoxConfig'.  Nome configurazione del nodo hello (toobe specificato in DeploymentTemplate.json) è così 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Passaggio 3: Aggiunta di server di pull toohello DSC risorse necessarie
Hello PowerShell Gallery è instrumentato tooinstall le risorse DSC nell'account di automazione di Azure.  Passare toohello risorsa desiderato e fare clic sul pulsante "Distribuisci tooAzure automazione" hello.

![Esempio di PowerShell Gallery](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Un'altra tecnica aggiunto di recente toohello portale di Azure consente toopull in moduli di aggiornamento esistente o di nuovo. Fare clic sulle risorse di Account di automazione hello riquadro asset hello e infine riquadro moduli hello.  icona Sfoglia raccolta Hello consente elenco hello toosee dei moduli nella raccolta di hello, drill-down nei dettagli e infine importare nell'Account di automazione. Questo è tookeep un modo utile per i moduli di toodate da tootime ora. E funzionalità di importazione hello controlla le dipendenze con altri tooensure moduli che Nothing Ottiene sincronizzato.

In alternativa, è l'approccio manuale hello.  struttura di cartelle Hello di un modulo di integrazione per un computer di Windows PowerShell è leggermente diversa dalla struttura delle cartelle hello previsto dal hello automazione di Azure.  perciò richiede alcune modifiche da parte dell'utente.  Ma non è difficile e viene eseguita una sola volta per ogni risorsa (a meno che non si desidera tooupgrade in futuro.)  Per altre informazioni sulla creazione di moduli di integrazione di PowerShell, vedere l'articolo relativo alla [creazione di moduli di integrazione per Automazione di Azure](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* Installare il modulo hello desiderati nella workstation, come indicato di seguito:
  * Installare [Windows Management Framework versione 5](http://aka.ms/wmf5latest) (non necessario per Windows 10).
  * `Install-Module –Name MODULE-NAME`<-acrobazie hello modulo dalla hello PowerShell Gallery 
* Cartella del modulo hello copia da `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa la cartella temp 
* Eliminare gli esempi e documentazione dalla cartella principale di hello 
* Cartella principale hello ZIP, denominazione esattamente i file ZIP hello hello stesso come cartella hello 
* Inserire file ZIP di hello in un percorso HTTP raggiungibile, ad esempio l'archiviazione di blob in un Account di archiviazione di Azure.
* Eseguire questo comando di PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

esempio Hello incluso esegue questi passaggi per cChoco e xNetworking. Vedere hello [note](#notes) per una gestione speciale per cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Passaggio 4: Aggiunta di server di pull toohello hello nodo Configurazione
Non è speciale hello prima che importare la configurazione in compilazione e il server di pull hello.  Importazione/compila tutti i successivi di hello stessa configurazione controllare esattamente hello stesso.  Ogni volta che si aggiorna il pacchetto ed è necessario impostarlo tooproduction eseguire questo passaggio dopo aver verificato il file di configurazione di hello toopush sia corretto: inclusi hello nuova versione del pacchetto.  Ecco il file di configurazione di hello e PowerShell:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Risultato questi passaggi in una nuova configurazione nodo denominato "ISVBoxConfig.isvbox" viene inserito nel server di pull hello.  nome di configurazione del nodo Hello viene compilato come "configurationName.nodeName".

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Passaggio 5: Creazione e gestione dei metadati del pacchetto
Per ogni pacchetto che inserite nel repository di pacchetti hello, è necessario un nuspec che lo descrive.  Questo Nuspec deve essere compilato e archiviato nel server NuGet. Questo processo è descritto [qui](http://docs.nuget.org/create/creating-and-publishing-a-package).  È possibile usare MyGet.org come server NuGet.  Il servizio è a pagamento, ma viene offerto gratuitamente uno SKU di avvio.  In NuGet.org sono disponibili istruzioni sull'installazione di un server NuGet personalizzato per i pacchetti privati.

## <a name="step-6-tying-it-all-together"></a>Passaggio 6: Verifica di tutti gli elementi
Ogni volta che una versione passa QA e viene approvata per la distribuzione, viene creato il pacchetto di hello, nupkg e nuspec aggiornata e distribuita toohello NuGet server.  Inoltre, hello configurazione (passaggio 4 sopra) deve essere aggiornato tooagree con il nuovo numero di versione hello.  Server di pull toohello inviato e compilato.  Da quel momento in poi è le VM toohello che dipendono da tale aggiornamento della configurazione toopull hello e installarlo.  Questi aggiornamenti sono semplici: solo una o due righe di PowerShell.  Nel caso di hello di Visual Studio Team Services, alcuni di essi vengono incapsulati in attività di compilazione che possono essere concatenate in una compilazione.  Per altre informazioni dettagliate, vedere questo [articolo](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery).  Questo [repository GitHub](https://github.com/Microsoft/vso-agent-tasks) dettagli hello varie attività di compilazione disponibile.

## <a name="notes"></a>Note
Questo esempio di utilizzo inizia con una macchina virtuale da un'immagine di Windows Server 2012 R2 generica da hello raccolta di Azure.  È possibile iniziare da qualsiasi immagine archiviata e quindi modificare da lì, con la configurazione DSC hello.  Tuttavia, la modifica di configurazione che è baked in un'immagine è molto più difficile rispetto all'aggiornamento in modo dinamico configurazione hello Usa DSC.

Non è disponibile un modello ARM toouse e hello VM estensione toouse questa tecnica con le macchine virtuali.  E le macchine virtuali non toobe in Azure toobe sotto la gestione di CD-ROM.  Tutto ciò che è necessario sia tale Chocolatey e hello configurato Gestione configurazione locale nella macchina virtuale hello indicargli hello server di pull in.  

Naturalmente, quando si aggiorna un pacchetto in una macchina virtuale nell'ambiente di produzione, è necessario tootake tale macchina virtuale dalla rotazione durante l'installazione dell'aggiornamento hello.  La procedura per eseguire questa operazione varia ampiamente.  Ad esempio, per una VM con bilanciamento del carico di Azure è possibile aggiungere un probe personalizzato.  Durante l'aggiornamento hello VM, hanno endpoint probe hello restituiscono un 400.  Hello tweak necessarie toocause questa modifica può essere all'interno della configurazione, come possibile hello tooswitch tweak nuovamente tooreturning 200 dopo l'aggiornamento di hello è stata completata.

Il codice sorgente completo per questo esempio di utilizzo si trova in [questo progetto di Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) su GitHub.

## <a name="related-articles"></a>Articoli correlati
* [Panoramica della piattaforma DSC di Automazione di Azure](automation-dsc-overview.md)
* [Cmdlet di Automation DSC per Azure](https://msdn.microsoft.com/library/mt244122.aspx)
* [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md)

