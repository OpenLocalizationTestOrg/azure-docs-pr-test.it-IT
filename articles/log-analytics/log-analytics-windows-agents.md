---
title: aaaConnect Windows computer tooAzure Log Analitica | Documenti Microsoft
description: Questo articolo illustra i computer Windows hello passaggi tooconnect hello nel toohello infrastruttura on-premise servizio Analitica Log utilizzando una versione personalizzata di hello Microsoft Monitoring Agent (MMA).
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Connettere i computer toohello Log Analitica servizio Windows Azure

Questo articolo illustra i passaggi di hello i computer Windows tooconnect nelle aree di lavoro tooOMS infrastruttura locale utilizzando una versione personalizzata di hello Microsoft Monitoring Agent (MMA). È necessario tooinstall e collegare gli agenti per tutti i computer hello che si desidera tooonboard affinché possano toosend data toohello Log Analitica e tooview e agire su tali dati. Ogni agente può segnalare toomultiple aree di lavoro.

È possibile installare gli agenti tramite il programma di installazione, la riga di comando o con Configurazione dello stato desiderato in Automazione di Azure.  

>[!NOTE]
Per le macchine virtuali in esecuzione in Azure, è possibile semplificare l'installazione utilizzando hello [estensione della macchina virtuale](log-analytics-azure-vm-extension.md).

Nei computer con connettività Internet, l'agente hello utilizza hello connessione toohello Internet toosend dati tooOMS. Per i computer che non dispongono di connettività Internet, è possibile utilizzare un proxy o hello [OMS Gateway](log-analytics-oms-gateway.md).

Connette il tooOMS computer Windows è semplice con tre semplici passaggi:

1. Scaricare i file di programma di installazione dell'agente di hello dal portale OMS hello
2. Installazione dell'agente di hello tramite il metodo hello che scelto
3. Configurare l'agente di hello o aggiungere altre aree di lavoro, se necessario

Hello diagramma seguente mostra la relazione hello tra OMS e computer Windows dopo aver installato e configurato gli agenti.

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect la rete Internet, è possibile configurare il toohello tooconnect computer Gateway OMS. Per ulteriori informazioni e procedure su come tooconfigure toocommunicate del server tramite un servizio OMS toohello Gateway OMS, vedere [connettersi tooOMS computer tramite Gateway OMS hello](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Requisiti di sistema e configurazione richiesta
Prima di installare o distribuire gli agenti, esaminare hello seguenti siano soddisfatti i requisiti di hello tooensure di dettagli.

- È possibile installare solo hello OMS MMA su computer che eseguono Windows Server 2008 SP 1 o versioni successive o Windows 7 SP1 o versione successiva.
- È necessaria una sottoscrizione di Azure.  Per altre informazioni, vedere [Introduzione a Log Analytics](log-analytics-get-started.md).
- Ogni computer Windows deve essere in grado di tooconnect toohello Internet utilizzando HTTPS o toohello OMS Gateway. La connessione può essere direttamente tramite un proxy, o hello OMS Gateway.
- È possibile installare hello MMA OMS in computer autonomi, server e macchine virtuali. Se si desidera tooconnect tooOMS di macchine virtuali ospitate di Azure, vedere [tooLog di macchine virtuali di Azure connettersi Analitica](log-analytics-azure-vm-extension.md).
- agente di Hello deve toouse la porta TCP 443 per varie risorse.

### <a name="network"></a>Rete

È necessario che Windows agenti tooconnect tooand registro servizio OMS hello, accedere alle risorse di toonetwork, inclusi i numeri di porta hello e gli URL di dominio.

- Per i server proxy, è necessario tooensure che hello server proxy corretto le risorse vengono configurate nelle impostazioni dell'agente.
- Per i firewall che limitano l'accesso toohello Internet, si o ai tecnici di rete necessario tooconfigure tooOMS di accesso toopermit il firewall. Non è necessaria alcuna azione sulle impostazioni dell'agente.

Hello nella tabella seguente mostra le risorse necessarie per la comunicazione.

>[!NOTE]
>Alcune delle seguenti risorse hello citati di Operational Insights, che è stato un nome precedente di Log Analitica.

| Risorsa agente | Porte | Ignorare l'analisi HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sì |
| *.oms.opinsights.azure.com | 443 | Sì |
| *.blob.core.windows.net | 443 | Sì |
| *.azure-automation.net | 443 | Sì |



## <a name="download-hello-agent-setup-file-from-oms"></a>Scaricare i file di programma di installazione dell'agente di hello da OMS
1. Nel portale di OMS hello in hello **Panoramica** pagina, fare clic su hello **impostazioni** riquadro.  Fare clic su hello **Connected Sources** scheda nella parte superiore di hello.  
    ![Scheda Origini connesse](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Fare clic su **server Windows** e quindi fare clic su **Download Windows Agent** file di installazione di tooyour applicabile computer processore tipo toodownload hello.
3. In hello destra **ID area di lavoro**, fare clic sull'icona di hello copia e Incolla hello ID nel blocco note.
4. In hello destra **chiave primaria**, fare clic sull'icona di copia hello e incollare la chiave hello nel blocco note.     

## <a name="install-hello-agent-using-setup"></a>Installazione dell'agente di hello tramite il programma di installazione
1. Esecuzione agente hello tooinstall di programma di installazione in un computer che si desidera toomanage.
2. Nella pagina di benvenuto hello, fare clic su **Avanti**.
3. Nella pagina condizioni di licenza hello leggere hello di licenza e quindi fare clic su **accetto**.
4. Nella pagina di destinazione cartella hello, modificare o mantenere una cartella di installazione predefinita di hello e quindi fare clic su **Avanti**.
5. Nella pagina di opzioni di installazione agente hello, è possibile scegliere tooAzure tooconnect agente hello Analitica Log (OMS), Operations Manager, oppure è possibile omettere le scelte di hello se si desidera agente hello tooconfigure in un secondo momento. Fare clic su **Avanti**.   
    - Se si sceglie tooconnect tooAzure Analitica Log (OMS), incollare hello **ID area di lavoro** e **chiave dell'area di lavoro (chiave primaria)** copiati nel blocco note nella procedura precedente hello e quindi fare clic su  **Avanti**.  
        ![incollare ID area di lavoro e chiave primaria](./media/log-analytics-windows-agents/connect-workspace.png)
    - Se si sceglie tooconnect tooOperations Manager, digitare hello **nome gruppo di gestione**, **Server di gestione** nome, e **porta Server di gestione**, quindi fare clic su **Avanti**. Nella pagina Account azione agente hello, scegliere l'account di sistema locale hello o un account di dominio locale e quindi fare clic su **Avanti**.  
        ![Configurazione del gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Nella pagina Pronto tooInstall hello, rivedere le scelte effettuate e quindi fare clic su **installare**.
7. Pagina Configurazione completata hello, fare clic su **fine**.
8. Al termine, hello **Microsoft Monitoring Agent** viene visualizzato **Pannello di controllo**. È possibile verificare la configurazione non esiste e verificare che l'agente di hello è connesso tooOperational Insights (OMS). Quando connesso tooOMS, hello agente viene visualizzato un messaggio che informa: **hello Microsoft Monitoring Agent è connesso correttamente il servizio di Microsoft Operations Management Suite toohello.**

## <a name="configure-proxy-settings"></a>Configurare le impostazioni proxy

È possibile utilizzare hello seguendo le impostazioni di proxy tooconfigure di procedure per hello Microsoft Monitoring Agent tramite il pannello di controllo. È necessario toouse questa procedura per ogni server. Se si dispone di molti server, che è necessario tooconfigure, può risultare più semplice toouse un tooautomate script questo processo. In questo caso, vedere la procedura successiva hello [tooconfigure impostazioni del proxy per Microsoft Monitoring Agent tramite uno script hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>impostazioni di proxy tooconfigure per hello Microsoft Monitoring Agent tramite il pannello di controllo
1. Aprire il **Pannello di controllo**.
2. Aprire **Microsoft Monitoring Agent**.
3. Fare clic su hello **le impostazioni del Proxy** scheda.  
    ![Scheda Impostazioni proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Selezionare **utilizza un server proxy** e digitare l'URL di hello e numero di porta, se necessario, in modo analogo toohello esempio illustrato. Se il server proxy richiede l'autenticazione, digitare hello nome utente e password tooaccess hello server proxy.


### <a name="verify-agent-connectivity-toooms"></a>Verificare tooOMS di connettività agente

È possibile verificare facilmente se gli agenti comunicano con OMS con hello seguente procedura:

1.  Nel computer di hello con agente di Windows hello, aprire Pannello di controllo.
2.  Aprire Microsoft Monitoring Agent.
3.  Fare clic sulla scheda di hello Analitica Log di Azure (OMS).
4.  Nella colonna Stato hello, dovrebbe essere che l'agente di hello stabilita la connessione del servizio Operations Management Suite toohello.

![agente connesso](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>impostazioni di proxy tooconfigure per hello Microsoft Monitoring Agent tramite uno script
Copiare hello seguente esempio, aggiornarlo con l'ambiente specifico tooyour informazioni, salvarlo con un'estensione di file PS1 e quindi eseguire script hello in ogni computer che si connette direttamente servizio OMS toohello.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Installazione dell'agente di hello tramite riga di comando hello
- Modificare e quindi utilizzare hello seguente agente hello tooinstall di esempio tramite la riga di comando hello. esempio Hello esegue un'installazione completamente invisibile all'utente.

    >[!NOTE]
    Se si desidera tooupgrade un agente, è necessario toouse hello Log Analitica API di scripting. Vedere hello successiva sezione tooupgrade un agente.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

agente Hello utilizza IExpress come il programma di autoestrazione utilizzando hello `/c` comando. È possibile visualizzare i parametri della riga di comando di hello in [della riga di comando per IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e quindi aggiornamento hello esempio toosuit le proprie esigenze.

|Opzioni specifiche di MMA                   |Note         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = l'area di lavoro Configura hello agente tooreport tooa                |
|OPINSIGHTS_WORKSPACE_ID                | Id area di lavoro (guid) per hello dell'area di lavoro tooadd                    |
|OPINSIGHTS_WORKSPACE_KEY               | Eseguire l'autenticazione tooinitially utilizzato chiave dell'area di lavoro con area di lavoro hello |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Specificare l'ambiente cloud hello in cui si trova l'area di lavoro hello <br> 0 = Cloud commerciale di Azure (impostazione predefinita) <br> 1 = Azure per enti pubblici |
|OPINSIGHTS_PROXY_URL               | URI per hello proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Nome utente tooaccess un proxy autenticato |
|OPINSIGHTS_PROXY_PASSWORD               | Password tooaccess un proxy autenticato |

>[!NOTE]
tooavoid che colpisce hello della riga di comando lunghezza massima di IExpress, installare agente hello con nessuna area di lavoro configurato e quindi usare una configurazione tooset script per area di lavoro hello.

>[!NOTE]
Se viene visualizzato un `Command line option syntax error.` quando si utilizza hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametro, è possibile utilizzare hello seguente soluzione alternativa:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Aggiungere un'area di lavoro usando uno script
Aggiungere un'area di lavoro con API di scripting di hello Analitica Log agente hello di esempio seguente:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd un'area di lavoro in Azure per governo, hello utilizzare script di esempio seguente:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Se si utilizza la riga di comando hello o script precedentemente tooinstall o configurare l'agente di hello, `EnableAzureOperationalInsights` è stato sostituito da `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Installazione dell'agente di hello tramite DSC in automazione di Azure

È possibile utilizzare hello seguente agente hello tooinstall esempio di script con DSC in automazione di Azure. esempio Hello installa hello agente a 64 bit, identificato da hello `URI` valore. È inoltre possibile utilizzare versione a 32 bit hello sostituendo il valore URI hello. Hello URI per entrambe le versioni sono:

- Agente di Windows a 64 bit - https://go.microsoft.com/fwlink/?LinkId=828603
- Agente di Windows a 32 bit - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
La procedura e lo script di esempio riportati di seguito non determinano l'aggiornamento di un agente esistente.

1. Importare hello xPSDesiredStateConfiguration modulo DSC da [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) in automazione di Azure.  
2.  Creare gli asset variabili di Automazione di Azure per *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*. Impostare *OPSINSIGHTS_WS_ID* ID area di lavoro di OMS Log Analitica tooyour e impostare *OPSINSIGHTS_WS_KEY* toohello chiave primaria dell'area di lavoro.
3.  Utilizzare hello seguente script e salvarlo come MMAgent.ps1
4.  Modificare e quindi utilizzare hello seguente agente hello tooinstall di esempio con DSC in automazione di Azure. Importare MMAgent.ps1 in automazione di Azure tramite l'interfaccia di automazione di Azure hello o un cmdlet.
5.  Assegnare una configurazione di toohello del nodo. Entro 15 minuti, il nodo hello controlla la configurazione e hello MMA viene inserito il nodo toohello.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Ottenere il valore ProductId più recente di hello

Hello `ProductId value` in hello MMAgent.ps1 script è univoco tooeach versione dell'agente. Quando viene pubblicata una versione aggiornata di ogni agente, il valore di ProductId hello cambia. In tal caso, quando hello ProductId viene modificato in futuro hello, è possibile trovare la versione di agente hello utilizzando un semplice script. Dopo aver hello ultima versione dell'agente installato in un server di prova, è possibile utilizzare il valore di ProductId hello installato tooget script seguente hello. Utilizza il valore ProductId più recente di hello, è possibile aggiornare il valore di hello in hello MMAgent.ps1 script.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Configurare manualmente un agente o aggiungere nuove aree di lavoro
Se sono stati installati gli agenti, ma non sono stati configurati o se si desidera che le aree di lavoro di hello agente tooreport toomultiple, è possibile utilizzare hello seguente informazioni tooenable un agente o riconfigurarlo. Dopo aver configurato l'agente hello, verrà registrato con il servizio agente hello e otterrà le informazioni di configurazione necessarie nonché i management pack che contengono informazioni sulla soluzione.

1. Dopo aver installato Microsoft Monitoring Agent hello, aprire **Pannello di controllo**.
2. Aprire **Microsoft Monitoring Agent** e quindi fare clic su hello **Analitica Log di Azure (OMS)** scheda.   
3. Fare clic su **Aggiungi** tooopen hello **aggiungere un'area di lavoro Analitica Log** casella.
4. Hello Incolla **ID area di lavoro** e **chiave dell'area di lavoro (chiave primaria)** copiati nel blocco note nella procedura precedente per hello area di lavoro che desidera tooadd e quindi fare clic su **OK**.  
    ![Configurare Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

Dopo la raccolta dei dati dai computer monitorati dall'agente di hello, numero di hello di computer monitorati da OMS verrà visualizzato nel portale OMS hello in hello **Connected Sources** scheda **impostazioni** come  **Server collegati**.


## <a name="toodisable-an-agent"></a>toodisable un agente
1. Dopo aver installato l'agente di hello, aprire **Pannello di controllo**.
2. Aprire Microsoft Monitoring Agent e quindi fare clic su hello **Analitica Log di Azure (OMS)** scheda.
3. Selezionare un'area di lavoro e quindi fare clic su **Rimuovi**. Ripetere questo passaggio per tutte le altre aree di lavoro.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Facoltativamente, configurare il gruppo gestione Operations Manager di agenti tooreport tooan

Se si utilizza Operations Manager dell'infrastruttura IT, è possibile utilizzare anche l'agente MMA hello come un agente Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>gruppo di gestione di tooconfigure MMA agenti tooreport tooan Operations Manager
1.  Nel computer in cui è installato l'agente di hello hello aprire **Pannello di controllo**.  
2.  Aprire **Microsoft Monitoring Agent** e quindi fare clic su hello **Operations Manager** scheda.  
    ![Microsoft Monitoring Agent scheda Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)
3.  Se i server di Operations Manager sono configurati per l'integrazione con Active Directory, fare clic su **Aggiorna automaticamente assegnazioni gruppi di gestione da Servizi di dominio Active Directory**.
4.  Fare clic su **Aggiungi** tooopen hello **aggiungere un gruppo di gestione** la finestra di dialogo.  
    ![Microsoft Monitoring Agent Aggiungi gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  In **nome gruppo di gestione** casella, il nome del tipo hello del gruppo di gestione.
6.  In hello **server di gestione primario** casella, il nome di computer tipo hello del server di gestione primario hello.
7.  In hello **porta server di gestione** casella, numero di porta TCP di tipo hello.
8.  In **Account azione agente**, scegliere l'account di sistema locale hello o un account di dominio locale.
9.  Fare clic su **OK** tooclose hello **aggiungere un gruppo di gestione** la finestra di dialogo e quindi fare clic su **OK** tooclose hello **Microsoft Monitoring Agent proprietà**la finestra di dialogo.


## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.
