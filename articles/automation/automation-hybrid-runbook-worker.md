---
title: Runbook worker ibridi automazione aaaAzure | Documenti Microsoft
description: "In questo articolo vengono fornite informazioni sull'installazione e utilizzo di Runbook Worker ibrido che è una funzionalità di automazione di Azure che consente i runbook toorun nelle macchine nel proprio data center locale o un provider di cloud."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatizzare le risorse nel centro dati o nel cloud con i ruoli di lavoro ibrido per runbook
I runbook in automazione di Azure non è possibile accedere alle risorse in altri cloud o nell'ambiente locale perché vengono eseguite nel cloud di Azure hello.  Hello lavoro ibridi per Runbook di automazione di Azure consente di toorun runbook direttamente nel computer di hello ospita il ruolo di hello e sulle risorse in hello ambiente toomanage tali risorse locali. I runbook vengono archiviati e gestiti in automazione di Azure e quindi recapitati tooone o più computer designati.  

Questa funzionalità è illustrata nella seguente immagine hello:<br>  

![Panoramica di Hybrid Runbook Workers](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Per una panoramica tecnica sulle considerazioni di ruolo e la distribuzione di Runbook Worker ibrido hello, vedere [Cenni preliminari sull'architettura di automazione](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Gruppi di computer di lavoro runbook ibridi
Ogni Runbook Worker ibrido è un membro di un gruppo di lavoro ibridi per Runbook specificato quando si installa agente hello.  Un gruppo può includere un solo agente, ma è possibile installarvi più agenti per garantire una disponibilità elevata.

Quando si avvia un runbook in un Runbook Worker ibrido, specificare il gruppo hello cui è in esecuzione.  i membri del gruppo di hello Hello determinano quale lavoro hello richiesta.  Non è possibile scegliere un computer di lavoro specifico.

## <a name="relationship-tooservice-management-automation"></a>Relazione tooService Management Automation
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) consente toorun hello stesso runbook che sono supportati da automazione di Azure nel data center locale. SMA viene in genere distribuito insieme a Windows Azure Pack, dal momento che Windows Azure Pack contiene un'interfaccia grafica per la gestione di SMA. A differenza di automazione di Azure, SMA richiede un'installazione locale che include hello toohost di server web API, un runbook toocontain database e la configurazione di SMA e i processi del runbook tooexecute Runbook worker. Automazione di Azure fornisce questi servizi in cloud hello e richiede solo toomaintain hello ibridi per Runbook nell'ambiente locale.

Nel caso di un utente esistente di SMA, è possibile spostare il toobe di automazione runbook tooAzure utilizzato con i Runbook Worker ibrido senza modifiche, presupponendo che eseguono le proprie tooresources autenticazione come descritto in [eseguire i runbook in un Runbook ibrida Lavoro](automation-hrw-run-runbooks.md).  I runbook in SMA eseguite nel contesto di hello dell'account di servizio hello server worker hello assicurando che l'autenticazione per i runbook hello.

È possibile utilizzare hello seguente toodetermine criteri se automazione di Azure con Runbook Worker ibrido o Service Management Automation è più adatta alle proprie esigenze.

* SMA richiede un'installazione locale di componenti sottostanti che sono connessi tooWindows Azure Pack, se è necessaria un'interfaccia di gestione con interfaccia grafica. Sono necessarie più risorse locali con costi di manutenzione superiori rispetto ad Automazione di Azure, che richiede solo l'installazione di un agente nei ruoli lavoro per runbook locali. gli agenti di Hello sono gestiti da Operations Management Suite, un'ulteriore riduzione dei costi di manutenzione.
* Automazione di Azure archivia i runbook nel cloud hello e li recapita i Runbook worker ibridi tooon locale. Se i criteri di sicurezza non consentono questo comportamento, è consigliabile usare SMA.
* SMA è incluso in System Center e richiede pertanto una licenza di System Center 2012 R2. Automazione di Azure si basa su un modello di sottoscrizione a livelli.
* Automazione di Azure offre funzionalità avanzate, tra cui runbook grafici, non disponibili in SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>L'installazione di Runbook Worker ibrido Windows hello 

tooinstall e configurare un Runbook Worker ibrido di Windows, sono disponibili due metodi.  Hello consigliato metodo utilizza un'automazione runbook toocompletely automatizzare il processo di hello necessario tooconfigure un computer Windows.  secondo metodo Hello di seguito è illustrata un'installazione di toomanually procedura e configurare il ruolo di hello.  

> [!NOTE]
> configurazione di hello toomanage dei server che supporta il ruolo di lavoro ibridi per Runbook hello con configurazione DSC (Desired State), è necessario tooadd come nodi DSC.  Per informazioni sul caricamento dei server per la gestione con DSC, vedere [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md).           
><br>
>Se si abilita hello [soluzione di gestione degli aggiornamenti](../operations-management-suite/oms-solution-update-management.md), qualsiasi computer Windows connesso tooyour area di lavoro OMS viene automaticamente configurato come un runbook di Runbook Worker ibrido toosupport incluso in questa soluzione.  Non viene però eseguita la registrazione con i gruppi di ruoli di lavoro ibridi già definiti nell'account di Automazione.  computer Hello è possibile aggiungere il gruppo di lavoro ibridi per Runbook tooa nel toosupport di account di automazione runbook di automazione, purché si utilizza hello stesso account per la soluzione hello e l'appartenenza al gruppo di lavoro ibridi per Runbook.  Questa funzionalità è stata aggiunta tooversion 7.2.12024.0 di hello Runbook Worker ibrido.  

Hello esaminare le seguenti informazioni riguardanti hello [requisiti hardware e software](automation-offering-get-started.md#hybrid-runbook-worker) e [informazioni per preparare la rete](automation-offering-get-started.md#network-planning) prima di iniziare la distribuzione di un Runbook Worker ibrido.  Dopo avere distribuito correttamente un runbook worker, esaminare [eseguire i runbook in un Runbook Worker ibrido](automation-hrw-run-runbooks.md) toolearn come tooconfigure tooautomate il runbook processi nel data center locale o un altro ambiente cloud.  
 
### <a name="automated-deployment"></a>Distribuzione automatizzata

Eseguire l'esempio hello passaggi tooautomate hello installazione e configurazione del ruolo di lavoro ibridi Windows hello.  

1. Scaricare hello *New OnPremiseHybridWorker.ps1* script da hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) direttamente dal computer di hello che eseguono il ruolo di lavoro ibridi per Runbook hello o da un altro computer nel ambiente e copiarlo toohello lavoro.  

    Hello *New OnPremiseHybridWorker.ps1* script richiede hello seguenti parametri durante l'esecuzione:

  * *AutomationAccountName* (obbligatorio) - nome hello dell'account di automazione.  
  * *ResourceGroupName* (obbligatorio) - nome hello hello del gruppo di risorse associata all'account di automazione.  
  * *HybridGroupName* (obbligatorio) - nome hello di un gruppo di lavoro ibridi per Runbook specificato come destinazione per i runbook hello supportare questo scenario. 
  *  *SubscriptionID* (obbligatorio) - hello Id sottoscrizione di Azure che l'account di automazione.
  *  *WorkspaceName* (facoltativo): hello OMS nome area di lavoro.  Se non si dispone di un'area di lavoro OMS, script hello crea e configura uno.  

     > [!NOTE]
     > Attualmente sono aree automazione sole hello è supportate per l'integrazione con OMS - **Australia sudorientale**, **Stati Uniti orientali 2**, **Asia sudorientale**, e **occidentale Europa**.  Se l'account di automazione non è in uno di tali aree, hello script consente di creare un'area di lavoro OMS ma segnala che è possibile collegarli tra loro.
     > 
2. Nel computer, avviare **Windows PowerShell** da hello **avviare** dello schermo in modalità amministratore.  
3. Hello shell della riga di comando di PowerShell, passare toohello cartella che contiene lo script hello è scaricato ed eseguito la modifica dei valori di hello per i parametri *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, e *- WorkspaceName*.

     > [!NOTE] 
     > Si è richiesta tooauthenticate con Azure dopo l'esecuzione di script hello.  Si **deve** accedere con un account che sia un membro del ruolo di amministratori della sottoscrizione hello e al coamministratore della sottoscrizione hello.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. Si è richiesta tooagree tooinstall **NuGet** e tooauthenticate richiesta con le credenziali di Azure.<br><br> ![Esecuzione dello script New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Al termine dello script hello, blade di gruppi di lavoro ibridi hello verrà visualizzati il nuovo gruppo di hello e numero di membri o se un gruppo esistente, viene incrementato il numero di hello di membri.  È possibile selezionare il gruppo di hello elenco hello hello **gruppi di lavoro ibrido** pannello e seleziona hello **di lavoro ibridi** riquadro.  In hello **di lavoro ibridi** pannello viene visualizzato ogni membro del gruppo di hello elencato.  

### <a name="manual-deployment"></a>Distribuzione manuale 
Eseguire i primi due passaggi hello una volta per l'ambiente di automazione, quindi ripetere hello rimanenti passaggi per ogni computer di lavoro.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Creare l'area di lavoro di Operations Management Suite
Se non si ha ancora un'area di lavoro di Operations Management Suite, crearne una seguendo le istruzioni in [Gestire le aree di lavoro](../log-analytics/log-analytics-manage-access.md). Se già si dispone di un'area di lavoro, è possibile usarla.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Aggiungere una soluzione di automazione tooOperations area di lavoro Suite di gestione
Le soluzioni aggiungono funzionalità tooOperations Management Suite.  soluzione di automazione Hello aggiunge la funzionalità per l'automazione di Azure, incluso il supporto per i Runbook Worker ibrido.  Quando si aggiunge l'area di lavoro tooyour soluzione hello, viene inserito automaticamente verso il basso lavoro componenti toohello agente computer in cui verrà installato nel passaggio successivo hello.

Seguire le istruzioni di hello in [tooadd una soluzione utilizzando la raccolta di soluzioni hello](../log-analytics/log-analytics-add-solutions.md) tooadd hello **automazione** dell'area di lavoro di soluzione tooyour Operations Management Suite.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Installare Microsoft Monitoring Agent hello
Hello Microsoft Monitoring Agent si connette a computer tooOperations Management Suite.  Quando si installa l'agente hello nel computer locale e connetterla tooyour dell'area di lavoro, verrà automaticamente scaricato componenti hello di Runbook Worker ibrido.

Seguire le istruzioni di hello in [tooLog computer Windows di connettersi Analitica](../log-analytics/log-analytics-windows-agents.md) agente hello tooinstall nel computer locale hello.  È possibile ripetere questo processo per più computer tooadd tooyour ambiente con più processi di lavoro.

Quando l'agente di hello connesso tooOperations Management Suite, verrà elencata in hello **Connected Sources** scheda di hello Operations Management Suite **impostazioni** riquadro.  È possibile verificare che l'agente di hello scaricato correttamente la soluzione di automazione hello quando dispone di una cartella denominata **AzureAutomationFiles** in C:\Program Files\Microsoft Monitoring Agent\Agent.  versione di hello tooconfirm di hello Runbook Worker ibrido, è possibile passare tooC:\Program Files\Microsoft monitoraggio Agent\Agent\AzureAutomation\ e Nota hello \\ *versione* sottocartella.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Installare hello runbook ambiente e connettersi tooAzure automazione
Quando si aggiunge un tooOperations agente Management Suite, hello soluzione di automazione inserisce verso il basso hello **HybridRegistration** modulo di PowerShell, che contiene hello **Add-HybridRunbookWorker** cmdlet.  Utilizzare questo cmdlet tooinstall hello runbook un ambiente nel computer di hello e registrarlo con automazione di Azure.

Aprire una sessione di PowerShell in modalità amministratore ed eseguire hello seguente modulo hello tooimport di comandi.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Eseguire quindi hello **Add-HybridRunbookWorker** cmdlet con hello la seguente sintassi:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

È possibile ottenere informazioni hello necessarie per questo cmdlet da hello **Gestisci chiavi** pannello in hello portale di Azure.  Aprire il pannello selezionando hello **chiavi** opzione hello **impostazioni** pannello nell'account di automazione.

![Panoramica di Hybrid Runbook Workers](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** nome hello di hello gruppo Runbook Worker ibrido. Se questo gruppo esiste già nell'account di automazione hello, computer corrente hello viene aggiunto tooit.  Se il gruppo ancora non esiste, verrà aggiunto.
* **EndPoint** è hello **URL** campo hello **Gestisci chiavi** blade.
* **Token** è hello **chiave di accesso primaria** in hello **Gestisci chiavi** blade.  

Hello utilizzare **-Verbose** con **Add-HybridRunbookWorker** tooreceive informazioni dettagliate sull'installazione di hello.

#### <a name="5-install-powershell-modules"></a>5. Installare i moduli di PowerShell
I runbook è possono utilizzare una delle attività di hello e cmdlet definiti nei moduli di hello installati nell'ambiente di automazione di Azure.  Questi moduli non sono computer locali tooon distribuito automaticamente, pertanto è necessario installarli manualmente.  eccezione Hello è hello modulo Azure, che viene installato per impostazione predefinita per fornire accesso toocmdlets per tutte le attività e i servizi di Azure per l'automazione di Azure.

Poiché lo scopo primario della funzionalità di Runbook Worker ibrido hello hello toomanage di risorse locali, è probabilmente necessario moduli hello tooinstall che supportano queste risorse.  È possibile fare riferimento troppo[installazione moduli](http://msdn.microsoft.com/library/dd878350.aspx) per informazioni sull'installazione di moduli di Windows PowerShell.  I moduli installati devono trovarsi in una posizione a cui fa riferimento la variabile di ambiente PSModulePath in modo che vengono importati automaticamente dal thread di lavoro ibridi hello.  Per ulteriori informazioni, vedere [hello modifica il percorso di installazione PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Rimozione del ruolo di lavoro ibrido per runbook 
È possibile rimuovere uno o più Runbook worker ibridi da un gruppo oppure è possibile rimuovere il gruppo di hello, a seconda dei requisiti.  tooremove un Runbook Worker ibrido da un computer locale, eseguire hello alla procedura seguente.

1. Nel portale di Azure hello, passare tooyour account di automazione.  
2. Da hello **impostazioni** pannello seleziona **chiavi** e prendere nota dei valori di hello per il campo **URL** e **chiave di accesso primaria**.  Queste informazioni sono necessarie per il passaggio successivo hello.
3. Aprire una sessione di PowerShell in modalità amministratore ed eseguire l'esempio hello command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Hello utilizzare **-Verbose** passare per un log dettagliato del processo di rimozione hello.

> [!NOTE]
> Ciò non rimuove hello Microsoft Monitoring Agent dal computer hello, solo funzionalità hello e la configurazione del ruolo di lavoro ibridi per Runbook hello.  

## <a name="remove-hybrid-worker-groups"></a>Rimuovere gruppi di ruoli di lavoro ibridi
tooremove un gruppo, è necessario innanzitutto tooremove hello Runbook Worker ibrido da tutti i computer che è un membro del gruppo di hello hello procedura illustrata in precedenza e quindi si esegue hello seguente gruppo di passaggi tooremove hello.  

1. Aprire l'account di automazione hello in hello portale di Azure.
2. Seleziona hello **gruppi di lavoro ibrido** riquadro e hello **gruppi di lavoro ibrido** blade, gruppo selezionare hello desiderato toodelete.  Dopo aver selezionato il gruppo specifico di hello, hello **gruppo di lavoro ibridi** viene visualizzato il Pannello proprietà.<br> ![Pannello Gruppi di ruoli di lavoro ibridi ](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Nel Pannello proprietà di hello per il gruppo selezionato di hello, fare clic su **eliminare**.  In cui viene chiesto di tooconfirm viene visualizzato un messaggio, questa azione Seleziona **Sì** se si è sicuri di voler tooproceed.<br> ![Finestra di dialogo di conferma dell'eliminazione del gruppo](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Questo processo può richiedere alcuni secondi toocomplete ed è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello.  

## <a name="troubleshooting"></a>Risoluzione dei problemi 
Hello Runbook Worker ibrido dipende hello toocommunicate Microsoft Monitoring Agent con il lavoro di automazione account tooregister hello, i processi del runbook e segnalare lo stato di ricezione. Se si verifica un errore di registrazione del server Web worker hello, ecco alcune possibili cause di errore hello:  

1. ruolo di lavoro ibrido Hello è dietro un proxy o firewall.  
    Verificare i computer di hello disponga dell'accesso in uscita too*.azure-automation.net sulla porta 443.  

2. Hello di lavoro ibridi hello computer è in esecuzione su è minore di requisiti hardware minimi hello [requisiti](automation-offering-get-started.md#hybrid-runbook-worker).  
    I computer che eseguono lavoro ibridi per Runbook deve soddisfare hello hello requisiti hardware minimi prima designazione di toohost questa funzionalità. In caso contrario, a seconda di hello utilizzo delle risorse di altri processi in background e contesa causata da runbook durante l'esecuzione, hello computer verranno diventano sovraccarico e causare ritardi processo runbook o i timeout.
   Verificare che il computer di hello designato funzionalità di Runbook Worker ibrido hello toorun soddisfi i requisiti hardware minimi hello.  In caso affermativo, monitorare eventuali correlazioni tra le prestazioni di hello di processi di lavoro ibridi per Runbook e Windows toodetermine di utilizzo della CPU e memoria.  Se è presente memoria o a utilizzo elevato della CPU, questo potrebbe indicare tooupgrade necessità hello o aggiungere processori aggiuntivi o aumento della memoria tooaddress hello collo di bottiglia e risolvere l'errore hello. In alternativa, selezionare una risorsa di calcolo diversi che può supportare i requisiti minimi di hello e scalabilità quando le richieste di carico di lavoro indicano che un aumento è necessario.
    
3. Hello servizio Microsoft Monitoring Agent non è in esecuzione.  
    Se non è in esecuzione il servizio Microsoft Monitoring Agent di Windows hello, questa operazione impedisce hello lavoro ibridi per Runbook di comunicare con l'automazione di Azure.  Verificare che agente hello è in esecuzione immettendo hello comando PowerShell seguente: `get-service healthservice`.  Se il servizio hello viene arrestato, immettere hello comando nel servizio hello toostart di PowerShell seguente: `start-service healthservice`.  

4. In hello **applicazioni e servizi di Logs\Operations** registro eventi, viene visualizzato l'evento 4502 ed EventMessage contenente **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**con hello seguente descrizione: *certificato hello presentato dal servizio hello <wsid>. c o m non è stato rilasciato da un'autorità di certificazione usata per i servizi Microsoft. Se sono in esecuzione un proxy che intercetta la comunicazione TLS/SSL, contattare il toosee di amministratore di rete. articolo di Hello KB3126513 contiene altre informazioni sulla risoluzione dei problemi di connettività.*
    Questo può dipendere da del proxy o rete firewall blockking comunicazione tooMicrosoft Azure.  Verificare i computer di hello disponga dell'accesso in uscita too*.azure-automation.net sulle porte 443.

I log vengono archiviati localmente in ogni ruolo di lavoro ibrido in C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  È possibile verificare se sono presenti eventuali eventi avviso o errore scritti toohello **applicazioni e servizi Logs\Microsoft-SMA\Operations** e **applicazioni e servizi di Logs\Operations** del registro eventi che indica una connettività o su altri problemi che interessano l'onboarding di hello ruolo tooAzure automazione o un problema durante l'esecuzione di operazioni normali.  

## <a name="next-steps"></a>Passaggi successivi
Revisione [eseguire i runbook in un Runbook Worker ibrido](automation-hrw-run-runbooks.md) toolearn come tooconfigure tooautomate il runbook processi nel data center locale o un altro ambiente cloud.
