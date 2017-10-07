---
title: stato della macchina virtuale di Azure in formato JSON tag tooschedule aaaUse | Documenti Microsoft
description: In questo articolo viene illustrato come le stringhe di toouse JSON in hello pianificazione tooautomate tag di chiusura e avvio VM.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Scenario di automazione di Azure: con formato JSON tag toocreate una pianificazione per la macchina virtuale di Azure avvio e arresto
I clienti desiderano spesso avvio hello tooschedule e arresto di macchine virtuali toohelp ridurre i costi di sottoscrizione o supportare i requisiti aziendali e tecnici.

Hello nello scenario seguente consente di tooset backup automatizzato di avvio e arresto delle macchine virtuali, utilizzando un tag denominato pianificazione a un livello di macchina virtuale in Azure o il livello di gruppo di risorse. Questa pianificazione può essere configurata da domenica tooSaturday con un'ora di avvio e arresto.

Sono disponibili opzioni predefinite. incluse le seguenti:

* [Set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) con le impostazioni di scalabilità automatica che consentono di tooscale in o out.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) servizio, che dispone di funzionalità predefinite di hello della pianificazione di operazioni di avvio e arresto.

Tuttavia, queste opzioni solo supportano scenari specifici e non possono essere macchine virtuali applicato tooinfrastructure-as-a-service (IaaS).

Quando hello tag pianificazione è il gruppo di risorse tooa applicato, è inoltre applicato tooall le macchine virtuali all'interno di tale gruppo di risorse. Se una pianificazione è anche tooa applicato direttamente VM, ultima pianificazione hello ha la precedenza in hello seguente ordine:

1. Gruppo di risorse applicata tooa pianificazione
2. Pianificare il gruppo di risorse tooa applicato e la macchina virtuale nel gruppo di risorse hello
3. Macchina virtuale di pianificazione applicato tooa

Questo scenario è essenzialmente accetta una stringa JSON con un formato specificato e lo aggiunge come valore di hello per un tag denominato pianificazione. Quindi, un runbook sono elencati tutti i gruppi di risorse e le macchine virtuali e identifica le pianificazioni di hello per ogni macchina virtuale in base agli scenari di hello elencati in precedenza. Successivamente scorre in ciclo hello macchine virtuali con pianificazioni collegate e restituisce l'azione che deve essere eseguita. Ad esempio, determina che le macchine virtuali devono toobe arrestato, arrestare o ignorato.

Questi runbook autenticare con hello [account RunAs di Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Scarica runbook hello per scenario hello
Questo scenario è composto da quattro runbook del flusso di lavoro di PowerShell che è possibile scaricare da hello [Raccolta TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) o hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository per il progetto.

| Runbook | Descrizione |
| --- | --- |
| Test-ResourceSchedule |Controlla pianificazione ogni macchina virtuale ed esegue l'arresto o l'avvio a seconda della pianificazione hello. |
| Add-ResourceSchedule |Aggiunge hello tag tooa VM o una risorsa gruppo di pianificazione. |
| Update-ResourceSchedule |Modifica tag pianificazione esistente hello sostituendolo con uno nuovo. |
| Remove-ResourceSchedule |Rimuove i tag di pianificazione hello da un macchina virtuale, un gruppo di risorse. |

## <a name="install-and-configure-this-scenario"></a>Installare e configurare lo scenario
### <a name="install-and-publish-hello-runbooks"></a>Installare e pubblicare i runbook hello
Dopo aver scaricato hello runbook, è possibile importarli usando la procedura hello in [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Pubblicare ogni runbook dopo averlo importato correttamente nell'account di automazione.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Aggiungere un runbook toohello ResourceSchedule di Test di pianificazione
Attenersi alla pianificazione di hello tooenable questi passaggi per hello ResourceSchedule di Test runbook. Si tratta runbook hello che verifica le macchine virtuali che deve essere avviate, arrestata, o lasciati inalterati.

1. Dal portale di Azure hello, aprire l'account di automazione e quindi fare clic su hello **runbook** riquadro.
2. In hello **Test ResourceSchedule** pannello, fare clic su hello **pianificazioni** riquadro.
3. In hello **pianificazioni** pannello, fare clic su **aggiungere una pianificazione**.
4. In hello **pianificazioni** pannello seleziona **collega un runbook tooyour pianificazione**. Selezionare quindi **Crea una nuova pianificazione**.
5. In hello **nuova pianificazione** pannello, digitare il nome di hello della pianificazione, ad esempio: *HourlyExecution*.
6. Per la pianificazione di hello **avviare**, impostare hello inizio tooan ora tempo.
7. Selezionare **Ricorrenza** e quindi in **Ricorre ogni** (intervallo) selezionare **1 ora**.
8. Verificare che **scadenza Set di** è troppo**n**, quindi fare clic su **crea** toosave la nuova pianificazione.
9. In hello **pianificazione Runbook** Pannello opzioni, seleziona **parametri e le impostazioni di esecuzione**. In hello Test ResourceSchedule **parametri** pannello, immettere il nome di hello della sottoscrizione in hello **SubscriptionName** campo.  Questo parametro solo hello che ha richiesto per il runbook hello è.  Al termine, fare clic su **OK**.

pianificazione del runbook Hello dovrebbe essere simile hello seguente completata:

![Runbook Test-ResourceSchedule configurato](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Hello formato stringa JSON
Questa soluzione fondamentalmente ha un formato JSON di stringhe con un formato specificato e lo aggiunge come valore di hello per un tag chiamato pianificazione. Quindi, un runbook sono elencati tutti i gruppi di risorse e le macchine virtuali e identifica le pianificazioni di hello per ogni macchina virtuale.

runbook Hello esaminati hello macchine che dispongono di pianificazioni collegate e controlla quali operazioni devono essere eseguite. Hello Ecco un esempio di modalità di formattazione delle soluzioni di hello:

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Ecco alcune informazioni dettagliate su questa struttura:

1. formato di Hello di questa struttura JSON è ottimizzato toowork intorno al limite di 256 caratteri hello di un valore singolo tag in Azure.
2. *TzId* rappresenta hello fuso orario della macchina virtuale hello. Questo ID può essere ottenuto utilizzando classe TimeZoneInfo .NET hello in una sessione di PowerShell -**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones in PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Giorni della settimana sono rappresentati con un valore numerico pari a zero toosix. il valore di Hello zero è uguale a domenica.
   * Hello ora di inizio è rappresentato dalla hello **S** attributo e il relativo valore è nel formato 24 ore.
   * Hello ora di fine o l'arresto è rappresentato dalla hello **E** attributo e il relativo valore è nel formato 24 ore.

     Se hello **S** e **E** ogni attributo dispone di un valore pari a zero (0), macchina virtuale hello rimarrà nello stato attuale in fase di valutazione di hello.
3. Se si desidera tooskip valutazione per un giorno specifico della settimana hello, non aggiungere una sezione per tale giorno della settimana hello. In hello seguente esempio, solo lunedì viene valutata e hello altri giorni della settimana hello vengono ignorati:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Aggiungere tag a gruppi di risorse o macchine virtuali
tooshut verso il basso le macchine virtuali, è necessario tootag macchine virtuali hello o gruppi di risorse hello in cui si trovano. Le macchine virtuali che non hanno un tag Schedule non vengono valutate. Di conseguenza, non vengono avviate né arrestate.

Esistono due macchine virtuali o i gruppi di risorse tootag modi con questa soluzione. È possibile farlo direttamente dal portale hello. È possibile utilizzare hello Aggiungi ResourceSchedule aggiornamento ResourceSchedule e Remove-ResourceSchedule runbook.

### <a name="tag-through-hello-portal"></a>Tag tramite il portale di hello
Seguire questi passaggi tootag una macchina virtuale o un gruppo di risorse nel portale di hello:

1. Convertire una stringa JSON hello e verificare che non vi siano spazi.  La stringa JSON dovrebbe avere un aspetto simile al seguente:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Seleziona hello **Tag** icona per una macchina virtuale o di una risorsa gruppo tooapply questa pianificazione.

   ![Opzione per i tag delle VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. I tag vengono definiti in base a una coppia chiave/valore. Tipo **pianificazione** in hello **chiave** campo e quindi incollare stringa JSON hello hello **valore** campo. Fare clic su **Salva**. Il nuovo tag verrà ora visualizzato nell'elenco di hello di tag per la risorsa.

   ![Tag di pianificazione delle VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Aggiungere tag da PowerShell
Tutti i runbook importati contengono le informazioni della Guida all'inizio di hello dello script hello che descrive la modalità tooexecute hello runbook direttamente da PowerShell. È possibile chiamare i runbook Aggiungi ScheduleResource e aggiornamento ScheduleResource hello da PowerShell. Questo caso passando i parametri necessari che consentono di tag di pianificazione di hello toocreate o update in un gruppo di macchina virtuale o una risorsa all'esterno di portale hello.

toocreate, aggiungere ed eliminare i tag mediante PowerShell, è innanzitutto necessario troppo[configurare l'ambiente di PowerShell per Azure](/powershell/azure/overview). Dopo aver completato l'installazione di hello, è possibile procedere con hello alla procedura seguente.

### <a name="create-a-schedule-tag-with-powershell"></a>Creare un tag di pianificazione con PowerShell
1. Aprire una sessione di PowerShell. Utilizzare quindi hello tooauthenticate di esempio con l'account RunAs e toospecify una sottoscrizione di seguito:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Definire una tabella hash di pianificazione. Di seguito è riportato un esempio di come dovrebbe essere costruita:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Definire i parametri di hello richiesti dal runbook hello. Nell'esempio seguente di hello, destinazione interessato una macchina virtuale:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Se si sta tag a un gruppo di risorse, rimuovere hello *VMName* parametro dall'hash hello $params tabella come segue:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Eseguire runbook hello Aggiungi ResourceSchedule con hello successivo tag di pianificazione hello toocreate parametri:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate un tag delle risorse gruppo o una macchina virtuale, eseguire hello **aggiornamento ResourceSchedule** runbook con hello seguenti parametri:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Rimuovere un tag di pianificazione con PowerShell
1. Aprire una sessione di PowerShell eseguire hello seguente tooauthenticate con l'account RunAs e tooselect e specificare una sottoscrizione:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Definire i parametri di hello richiesti dal runbook hello. Nell'esempio seguente di hello, destinazione interessato una macchina virtuale:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Se si elimina un tag da un gruppo di risorse, rimuovere hello *VMName* parametro dall'hash hello $params tabella come segue:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Eseguire i tag di hello Remove ResourceSchedule runbook tooremove hello pianificazione:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate un tag delle risorse gruppo o una macchina virtuale, eseguire Remove-ResourceSchedule hello runbook con hello seguenti parametri:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> È consigliabile monitorare in modo proattivo questi runbook (e degli stati della macchina virtuale hello) tooverify che le macchine virtuali vengono arrestato e avviato di conseguenza.
>

dettagli di hello tooview di runbook hello Test ResourceSchedule processo portale di Azure seleziona hello hello **processi** tessera di hello runbook. Hello processo Visualizza riepilogo hello i parametri di input e output di hello flussi, inoltre toogeneral informazioni processo hello e alle eventuali eccezioni se si sono verificate.

Hello **riepilogo** include i messaggi da flussi di errore, avviso e di output di hello. Seleziona hello **Output** tooview riquadro risultati dell'esecuzione di runbook hello dettagliati.

![Output di Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md).
* toolearn ulteriori informazioni sui tipi di runbook e i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md).
* Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Supporto di script PowerShell nativi in Automazione di Azure).
* toolearn ulteriori informazioni su registrazione runbook e l'output, vedere [Runbook in automazione di Azure messaggi e output](automation-runbook-output-and-messages.md).
* informazioni su un account RunAs di Azure e come tooauthenticate runbook con questo nuovo modello, vedere toolearn [autenticare runbook con l'account RunAs di Azure](automation-sec-configure-azure-runas-account.md).
