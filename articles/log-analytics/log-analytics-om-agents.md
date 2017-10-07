---
title: aaaConnect Operations Manager tooLog Analitica | Documenti Microsoft
description: "toomaintain l'investimento esistente in System Center Operations Manager e usare le funzionalità con Log Analitica, è possibile integrare Operations Manager con l'area di lavoro OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>La connessione di Operations Manager tooLog Analitica
toomaintain l'investimento esistente in System Center Operations Manager e usare le funzionalità con Log Analitica, è possibile integrare Operations Manager con l'area di lavoro OMS.  Ciò consente sfruttare le opportunità di hello di OMS continuando toouse Operations Manager per:

* Continuare il monitoraggio di integrità hello dei servizi IT con Operations Manager
* Gestire l'integrazione con le soluzioni ITSM che supportano la gestione di eventi imprevisti e problemi
* Gestione del ciclo di vita di hello di tooon locali degli agenti distribuiti e macchine virtuali di IaaS al cloud pubblico che eseguono il monitoraggio con Operations Manager

L'integrazione con System Center Operations Manager aggiunge strategia di operazioni di valore tooyour assistenza utilizzando hello velocità e l'efficienza di OMS nella raccolta, all'archiviazione e l'analisi dei dati da Operations Manager.  OMS consente di correlazione e lavoro verso l'identificazione di errori di hello dei problemi e superfici ricorrenze per supportare il processo di gestione esistente del problema.   Hello flessibilità di hello ricerca motore tooexamine delle prestazioni, eventi e avvisi dati, con dashboard avanzati e reporting funzionalità tooexpose questi dati in modi significativi, illustrato forza hello OMS attiva la modalità integrata dalla Operations Manager.

agenti di Hello reporting toohello gruppo di gestione di Operations Manager raccolgono i dati dai server in base alle origini dati di Log Analitica hello e soluzioni che è stata abilitata nella sottoscrizione OMS.  A seconda della soluzione hello che è stata abilitata, i dati da queste soluzioni sono inviato direttamente da un server di gestione di Operations Manager toohello OMS servizio web o a causa di hello volume dei dati raccolti nel sistema gestito tramite agenti hello, vengono inviati direttamente dal servizio web di hello agente tooOMS. il server di gestione di Hello inoltra i dati di OMS hello direttamente toohello OMS web servizio. database di Operations Manager o OperationsManagerDW toohello mai scritto.  Quando un server di gestione perde la connettività con il servizio web OMS hello, memorizza nella cache i dati hello localmente finché non viene ristabilita con OMS la comunicazione.  Se il server di gestione di hello è offline a causa di un'interruzione non pianificata o manutenzione tooplanned, un altro server di gestione nel gruppo di gestione di hello riprende la connettività con OMS.  

Hello diagramma seguente è illustrata hello connessione tra il server di gestione di hello e gli agenti in un gruppo di gestione di System Center Operations Manager e OMS, incluse le porte e direzione hello.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect Internet la rete, server di gestione può essere informazioni di configurazione tooreceive OMS Gateway configurato tooconnect toohello e inviare i dati raccolti dipende soluzione hello sono abilitate.  Per ulteriori informazioni e procedure su come tooconfigure il toocommunicate gruppo di gestione di Operations Manager tramite un servizio OMS toohello Gateway OMS, vedere [connettersi tooOMS computer tramite Gateway OMS hello](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Requisiti di sistema
Prima di iniziare, esaminare hello tooverify dettagli soddisfi i prerequisiti seguenti.

* OMS supporta solo Operations Manager 2016, Operations Manager 2012 SP1 UR6 e versioni successive e Operations Manager 2012 R2 UR2 e versioni successive.  Il supporto per il proxy è stato aggiunto in Operations Manager 2012 SP1 UR7 e Operations Manager 2012 R2 UR3.
* Tutti gli agenti di Operations Manager devono soddisfare i requisiti di supporto minimo. Verificare che gli agenti sono al momento dell'aggiornamento minimo di hello, in caso contrario il traffico di agente di Windows potrebbe non riuscire e molti errori potrebbero riempire hello registro eventi di Operations Manager.
* Una sottoscrizione di OMS.  Per ulteriori informazioni, vedere [Introduzione a Log Analytics](log-analytics-get-started.md).

### <a name="network"></a>Rete
informazioni di Hello seguito elenco hello proxy e firewall informazioni di configurazione necessarie per l'agente di Operations Manager hello e i server di gestione Operations console toocommunicate con OMS.  Il traffico proveniente da ogni componente è in uscita dal servizio OMS toohello rete.     

|Risorsa | Numero della porta| Ignorare l'analisi HTTPS|  
|---------|------|-----------------------|  
|**Agent**|||  
|\*.ods.opinsights.azure.com| 443 |Sì|  
|\*.oms.opinsights.azure.com| 443|Sì|  
|\*.blob.core.windows.net| 443|Sì|  
|\*.azure-automation.net| 443|Sì|  
|**Server di gestione**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Sì|  
|\*.ods.opinsights.azure.com| 443| Sì|  
|*.azure-automation.net | 443| Sì|  
|**TooOMS console di Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 e 443||  
|\*.microsoft.com| 80 e 443||  
|\*.microsoftonline.com| 80 e 443||  
|\*.mms.microsoft.com| 80 e 443||  
|login.windows.net| 80 e 443||  


## <a name="connecting-operations-manager-toooms"></a>Connessione tooOMS Operations Manager
Eseguire hello serie di passaggi tooconfigure il tooone di tooconnect gruppo di Operations Manager Gestione le aree di lavoro OMS.

1. Nella console di Operations Manager hello selezionare hello **amministrazione** dell'area di lavoro.
2. Espandere il nodo di hello Operations Management Suite e fare clic su **connessione**.
3. Fare clic su hello **registrare tooOperations Management Suite** collegamento.
4. In hello **Caricamento guidato di Operations Management Suite: autenticazione** pagina, immettere la password dell'account di amministratore hello che è associato alla sottoscrizione di OMS e il numero di telefono o indirizzo di posta elettronica hello e fare clic su  **Accedi**.
5. Dopo il completamento dell'autenticazione, in hello **Caricamento guidato di Operations Management Suite: area di lavoro selezionare** pagina, si è richiesto tooselect area di lavoro OMS.  Se si dispone di più di un'area di lavoro, selezionare hello dell'area di lavoro desidera tooregister con gruppo di gestione di Operations Manager hello dall'elenco a discesa hello e quindi fare clic su **Avanti**.
   
   > [!NOTE]
   > Operations Manager supporta solo un'area di lavoro di OMS alla volta. connessione di Hello e computer di hello che sono stati registrati tooOMS con area di lavoro hello precedente vengono rimossi da OMS.
   > 
   > 
6. In hello **Caricamento guidato di Operations Management Suite: riepilogo** pagina, confermare le impostazioni e se sono corretti, fare clic su **crea**.
7. In hello **Caricamento guidato di Operations Management Suite: fine** pagina, fare clic su **Chiudi**.

### <a name="add-agent-managed-computers"></a>Aggiungere computer gestiti dagli agenti
Dopo aver configurato l'integrazione con l'area di lavoro OMS, si stabilisce solo una connessione con OMS, non vengono raccolti dati dagli agenti hello tooyour gruppo di gestione di reporting. Questo avverrà solo dopo aver configurato i computer specifici gestiti dagli agenti che devono raccogliere i dati per Log Analytics. È possibile selezionare gli oggetti computer hello singolarmente oppure è possibile selezionare un gruppo che contiene gli oggetti computer Windows. Non è possibile selezionare un gruppo contenente istanze di un'altra classe, ad esempio dischi logici o database SQL.

1. Console di Operations Manager aprire hello e seleziona hello **amministrazione** dell'area di lavoro.
2. Espandere il nodo di hello Operations Management Suite e fare clic su **connessione**.
3. Fare clic su hello **aggiungere un gruppo diComputer/** collegamento hello azioni titolo sul lato destro hello del riquadro hello.
4. In hello **ricerca Computer** nella finestra di dialogo è possibile cercare i computer o i gruppi monitorati da Operations Manager. Selezionare i computer o gruppi tooOMS tooonboard, fare clic su **Aggiungi**, quindi fare clic su **OK**.

È possibile visualizzare i computer e gruppi configurati toocollect dati dal nodo di computer gestiti hello in Operations Management Suite in hello **amministrazione** area di lavoro della console operatore hello.  Da qui è possibile aggiungere o rimuovere i computer e i gruppi in base alle esigenze.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Configurare le impostazioni del proxy OMS nella console operatore hello
Eseguire hello seguendo i passaggi, se un server proxy interno tra il gruppo di gestione di hello e servizio web OMS.  Queste impostazioni vengono gestite centralmente dal gruppo di gestione di hello e distribuiti tooagent sistemi gestiti che vengono inclusi nei dati di hello ambito toocollect per OMS.  Ciò è utile per quando alcune soluzioni ignorare hello management server e per l'invio dei dati direttamente tooOMS servizio web.

1. Console di Operations Manager aprire hello e seleziona hello **amministrazione** dell'area di lavoro.
2. Espandere Operations Management Suite e quindi fare clic su **Connessioni**.
3. Nella visualizzazione OMS Connection hello, fare clic su **Configure Proxy Server**.
4. In **guidato di Operations Management Suite: Server Proxy** selezionare **utilizzare hello di tooaccess un server proxy Operations Management Suite**, quindi digitare l'URL di hello con numero di porta hello, ad esempio, http:// corpproxy:80 e quindi fare clic su **fine**.

Se il server proxy richiede l'autenticazione, eseguire questa procedura di hello tooconfigure credenziali e le impostazioni che devono toopropagate toomanaged computer che segnala tooOMS nel gruppo di gestione di hello.

1. Console di Operations Manager aprire hello e seleziona hello **amministrazione** dell'area di lavoro.
2. In **Configurazione RunAs** selezionare **Profili**.
3. Aprire hello **System Center Advisor Proxy del profilo runas** profilo.
4. In hello eseguire Creazione guidata profilo runas, fare clic su Aggiungi toouse un account RunAs. È possibile creare un [account RunAs](https://technet.microsoft.com/library/hh321655.aspx) oppure usare un account esistente. Questo account deve toohave toopass di autorizzazioni sufficienti tramite server proxy hello.
5. tooset hello toomanage account, scegliere **una classe, gruppo o oggetto selezionato**, fare clic su **Seleziona...** e su **Gruppo...** hello tooopen **gruppo ricerca** casella.
6. Cercare e quindi selezionare **Gruppo di server di monitoraggio di Microsoft System Center Advisor**.  Fare clic su **OK** dopo aver selezionato hello di hello gruppo tooclose **gruppo ricerca** casella.
7. Fare clic su **OK** tooclose hello **aggiungere un account RunAs** casella.
8. Fare clic su **salvare** toocomplete hello procedura guidata e salvare le modifiche.

Dopo la connessione hello viene creata e si configura gli agenti raccoglierà e tooOMS di dati del report, hello configurazione seguente viene applicata nel gruppo di gestione di hello, non necessariamente nell'ordine:

* Account runas Hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** viene creato.  È associato al profilo runas hello **Microsoft System Center Advisor eseguire come Blob del profilo** ed è destinato a due classi - **Server raccolta** e **il gruppo di gestione di Operations Manager** .
* Vengono creati due connettori.  Hello innanzitutto denominato **Microsoft.SystemCenter.Advisor.DataConnector** e viene configurato automaticamente con una sottoscrizione che inoltra tutti gli avvisi generati da istanze di tutte le classi di hello gestione gruppo tooOMS Log Analitica. secondo connettore Hello è **Advisor Connector**, che è responsabile per la comunicazione con il servizio web OMS e la condivisione dei dati.
* Gli agenti e i gruppi che sono stati selezionati i dati di toocollect nel gruppo di gestione di hello viene aggiunto toohello **Microsoft System Center Advisor Monitoring Server Group**.

## <a name="management-pack-updates"></a>Aggiornamenti di Management Pack
Dopo la configurazione viene completata, il gruppo di gestione di Operations Manager hello stabilisce una connessione con hello servizio OMS.  il server di gestione di Hello Sincronizza con il servizio web hello e ricevere informazioni di configurazione aggiornate nel modulo hello dei management pack per le soluzioni hello integrano con Operations Manager è stata abilitata.   Operations Manager cerca gli aggiornamenti per questi Management Pack e, se disponibili, li scarica e li importa automaticamente.  Esistono due regole in particolare che controllano questo comportamento:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -Aggiorna management pack di hello base OMS. Per impostazione predefinita, viene eseguita ogni 12 ore.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** : aggiorna i Management Pack delle soluzioni abilitati nell'area di lavoro. Per impostazione predefinita, viene eseguita ogni cinque (5) minuti.

È possibile eseguire l'override di queste due regole tooeither evitare download automatico da disabilitazione o modificare la frequenza di hello per la frequenza con cui hello server di gestione si sincronizza con OMS toodetermine se un nuovo management pack è disponibile e deve essere scaricato.  Seguire i passaggi di hello [come tooOverride una regola o monitoraggio](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **frequenza** parametro con un valore in secondi toochange hello pianificazione della sincronizzazione o modifica di hello **abilitato**  regole hello toodisable di parametro.  Hello destinazione sostituzioni tooall oggetti della classe gruppo di gestione di Operations Manager.

Se si desidera toocontinue seguendo la procedura di controllo di modifica esistente per il controllo delle versioni del management pack nel gruppo di gestione di produzione, è possibile disabilitare le regole di hello e attivarli in orari specifici quando gli aggiornamenti sono consentiti. Se si dispone di sviluppo o di un gruppo di gestione del controllo di qualità nel proprio ambiente e ha toohello connettività Internet, è possibile configurare il gruppo di gestione con un toosupport dell'area di lavoro OMS questo scenario.  Questo consente tooreview e valutare le versioni iterativo hello del management pack di OMS hello prima di essere rilasciate nel gruppo di gestione di produzione.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Passare un tooa gruppo Operations Manager nuova area di lavoro OMS
1. Accedi a sottoscrizione OMS tooyour e creare un'area di lavoro [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Console di Operations Manager aprire hello con un account membro del ruolo di amministratori di Operations Manager hello e seleziona hello **amministrazione** dell'area di lavoro.
3. Espandere Operations Management Suite e selezionare **Connessioni**.
4. Seleziona hello **riconfigurare operazione Management Suite** collegamento intermedio hello sul lato del riquadro hello.
5. Seguire hello **Caricamento guidato di Operations Management Suite** immettere hello indirizzo e-mail o telefono numero e la password dell'account di amministratore hello associata con la nuova area di lavoro OMS.
   
   > [!NOTE]
   > Hello **Caricamento guidato di Operations Management Suite: area di lavoro selezionare** pagina presenta hello area di lavoro esistente che è in uso.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Convalidare l'integrazione di Operations Manager con OMS
Esistono alcuni modi diversi, è possibile verificare che l'integrazione di gestione di tooOperations OMS ha esito positivo.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>integrazione di tooconfirm dal portale OMS hello
1. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro
2. Selezionare **Origini connesse**.
3. Nella tabella hello hello sezione di System Center Operations Manager, verrà visualizzato il nome di hello del gruppo di gestione di hello elencato con il numero di hello di agenti e lo stato quando l'ultima ricezione di dati.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Hello nota **ID area di lavoro** valore hello lato sinistro della pagina Impostazioni hello.  Convalidarlo rispetto al gruppo di gestione Operations Manager seguente.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>integrazione di tooconfirm dalla console operatore hello
1. Console di Operations Manager aprire hello e seleziona hello **amministrazione** dell'area di lavoro.
2. Selezionare **Management Pack** e hello **cercare:** tipo casella di testo **Advisor** o **Intelligence**.
3. A seconda delle soluzioni di hello che è stata abilitata, vedrai un management pack corrispondente elencati nei risultati della ricerca hello.  Ad esempio, se è stata abilitata la soluzione Alert Management hello, hello management pack Gestione avvisi di Microsoft System Center Advisor è nell'elenco di hello.
4. Da hello **monitoraggio** visualizzare, esplorare toohello **Operations Management Suite\Health stato** visualizzazione.  Selezionare un server di gestione in hello **stato Server di gestione** riquadro e hello **visualizzazione dettagli** riquadro confermare il valore di hello per la proprietà **URI del servizio di autenticazione** ID area di lavoro OMS hello corrispondente
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Rimuovere l’integrazione con OMS
Quando non è più necessario integrazione tra il gruppo di gestione di Operations Manager e l'area di lavoro OMS, sono disponibili diversi passaggi necessari tooproperly remove hello connessione e la configurazione nel gruppo di gestione di hello. Hello procedura riportata di seguito si aggiorna l'area di lavoro OMS eliminando hello riferimento del gruppo di gestione, eliminare i connettori di OMS hello e quindi eliminare management pack OMS di supporto.   

Management Pack per le soluzioni hello integrano con Operations Manager che è stata attivata e hello management pack necessari toosupport integrazione hello servizio OMS non può essere facilmente cancellati dal gruppo di gestione di hello.  Questo avviene perché alcuni dei management pack di OMS hello presentano dipendenze correlate management pack.  toodelete management pack avente una dipendenza da altri management pack, scaricare script hello [rimuovere un management pack con le dipendenze](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) da TechNet Script Center.  

1. Aprire hello Shell comandi Operations Manager con un account che sia un membro del ruolo amministratori di Operations Manager hello.
   
    > [!WARNING]
    > Verificare che non è un management pack personalizzati con la parola hello Advisor o IntelligencePack nel nome hello prima di procedere, in caso contrario hello passaggi eliminarli dal gruppo di gestione di hello.
    > 

2. Dal prompt della shell comandi hello, digitare`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Quindi digitare `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. Comprime tutti i management pack rimanenti che presentano una dipendenza da altri servizi di gestione System Center Advisor tooremove, utilizzare script hello *RecursiveRemove.ps1* scaricato dall'area hello TechNet Script Center.  
 
    > [!NOTE]
    > Non eliminare hello Microsoft System Center Advisor o Advisor interni di Microsoft System Center management pack.  
    >  

5. Aprire console operatore di Operations Manager hello con un account che sia un membro del ruolo amministratori di Operations Manager hello.
6. In **amministrazione**selezionare hello **Management Pack** nodo e in hello **cercare:** digitare **Advisor** e verificare hello management pack seguenti sono ancora importati nel gruppo di gestione:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Internal
7. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro.
8. Selezionare **Origini connesse**.
9. Nella tabella hello hello sezione di System Center Operations Manager, verrà visualizzato il nome di hello hello gruppo di gestione desiderato tooremove dall'area di lavoro hello.  Nella colonna hello **ultimi dati**, fare clic su **rimuovere**.  
   
    > [!NOTE]
    > Hello **rimuovere** collegamento non sarà disponibile fino a dopo 14 giorni se è presente alcuna attività rilevato dal gruppo di gestione connesso hello.  
    > 

10. Verrà visualizzata una finestra in cui viene richiesto che si desidera tooproceed con la rimozione di hello tooconfirm.  Fare clic su **Sì** tooproceed. 

toodelete hello due connettori - Microsoft.SystemCenter.Advisor.DataConnector e il connettore Advisor, salvare uno script di PowerShell hello sotto tooyour computer ed eseguire hello seguono esempi di utilizzo:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> eseguire questo script dal computer di Hello, se non è un server di gestione deve disporre di shell dei comandi di Operations Manager hello installata a seconda della versione di hello del gruppo di gestione.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

In futuro hello se si intende la riconnessione gestione gruppo tooan OMS workspace, è necessario toore importazione hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` file del management pack dall'aggiornamento cumulativo più recente di hello applicato tooyour gruppo di gestione.  È possibile trovare questo file in hello `%ProgramFiles%\Microsoft System Center 2012` o hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` cartella.

## <a name="next-steps"></a>Passaggi successivi
funzionalità tooadd e raccogliere dati, vedere [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).


