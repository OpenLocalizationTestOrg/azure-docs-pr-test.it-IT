---
title: i parametri di input aaaRunbook | Documenti Microsoft
description: "Parametri di input runbook aumentare la flessibilità di hello dei runbook, consentendo toopass dati tooa runbook quando viene avviata. Questo articolo descrive vari scenari in cui i parametri di input vengono usati nei runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Parametri di input dei runbook
Parametri di input runbook aumentare la flessibilità di hello dei runbook, consentendo toopass dati tooit quando viene avviata. i parametri di Hello consentono hello runbook azioni toobe di destinazione per gli ambienti e scenari specifici. Questo articolo illustra vari scenari in cui i parametri di input vengono usati nei runbook.

## <a name="configure-input-parameters"></a>Configurare i parametri di input
È possibile configurare i parametri di input nei runbook grafici e in quelli di PowerShell e del flusso di lavoro PowerShell. Un runbook può avere più parametri con tipi di dati diversi oppure non avere parametri. I parametri di input possono essere obbligatori o facoltativi ed è possibile assegnare un valore predefinito per i parametri facoltativi. È possibile assegnare valori toohello i parametri di input per un runbook quando viene avviato tramite uno dei metodi disponibili hello. Questi metodi includono l'avvio di un runbook dal portale di hello o un servizio web. È inoltre possibile avviare un runbook come figlio, definito inline in un altro runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Configurare i parametri di input nei runbook di PowerShell e nei runbook del flusso di lavoro PowerShell
PowerShell e [runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md) in automazione di Azure supporta i parametri di input che vengono definiti tramite hello gli attributi seguenti.  

| **Proprietà** | **Descrizione** |
|:--- |:--- |
| Type |Obbligatorio. tipo di dati Hello previsto per il valore di parametro hello. Qualsiasi tipo .NET è valido. |
| Nome |Obbligatorio. nome di Hello del parametro hello. Questo deve essere univoco all'interno di runbook hello e può contenere solo lettere, numeri o caratteri di sottolineatura. Deve iniziare con una lettera. |
| Obbligatorio |Facoltativo. Specifica se è necessario specificare un valore per il parametro hello. Se si imposta questa troppo**$true**, quindi è necessario fornire un valore alla hello runbook viene avviato. Se si imposta questa troppo**$false**, quindi un valore è facoltativo. |
| Valore predefinito |Facoltativo.  Specifica un valore che verrà utilizzato per il parametro hello se un valore non sia stato passato quando hello runbook viene avviato. Un valore predefinito può essere impostato per qualsiasi parametro e verrà apportate automaticamente il parametro hello facoltativo indipendentemente dall'impostazione obbligatoria hello. |

Windows PowerShell supporta più attributi dei parametri di input di quelli elencati di seguito, ad esempio la convalida, gli alias e i set di parametri. Tuttavia, automazione di Azure supporta attualmente solo hello parametri di input elencati in precedenza.

Una definizione di parametro nei runbook del flusso di lavoro di PowerShell ha hello seguente formato generale, in cui più parametri sono separati da virgole.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Quando si definiscono i parametri, se non si specifica hello **obbligatorio** attributo, per impostazione predefinita, il parametro hello è considerato facoltativo. Inoltre, se si imposta un valore predefinito per un parametro nei runbook del flusso di lavoro di PowerShell, verrà considerato da PowerShell come un parametro facoltativo, indipendentemente dal hello **obbligatorio** valore dell'attributo.
> 
> 

Ad esempio, è possibile configurare parametri di input hello per un runbook del flusso di lavoro di PowerShell che restituisce informazioni dettagliate su macchine virtuali, una singola macchina virtuale o tutte le macchine virtuali all'interno di un gruppo di risorse. Questo runbook ha due parametri, come illustrato nella seguente schermata hello: nome hello della macchina virtuale e il nome di hello hello del gruppo di risorse.

![Flusso di lavoro PowerShell di Automazione](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

In questa definizione di parametro hello parametri **$VMName** e **$resourceGroupName** semplice ai parametri di tipo stringa. I runbook di PowerShell e del flusso di lavoro PowerShell supportano tuttavia tutti i tipi semplici e complessi, ad esempio **object** o **PSCredential** per i parametri di input.

Se il runbook include un parametro di input di tipo di oggetto, quindi utilizzare una tabella hash di PowerShell con (nome, valore) coppie toopass in un valore. Ad esempio, se si dispone di hello segue parametro in un runbook:

     [Parameter (Mandatory = $true)]
     [object] $FullName

È quindi possibile passare hello segue valore toohello parametro:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Configurare i parametri di input in runbook grafici
troppo[configurare un runbook grafico](automation-first-runbook-graphical.md) con parametri di input, creare un runbook con interfaccia grafico che restituisce informazioni dettagliate sulle macchine virtuali, ovvero una singola macchina virtuale o tutte le macchine virtuali all'interno di un gruppo di risorse. La configurazione di un runbook è costituita da due attività principali, come descritto di seguito.

[**L'autenticazione di runbook con account RunAs di Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate con Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) proprietà hello tooget di una macchina virtuale.

È possibile utilizzare hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nomi hello toooutput delle attività delle macchine virtuali. Hello attività **Get AzureRmVm** accetta due parametri, hello **nome della macchina virtuale** hello e **nome gruppo di risorse**. Poiché questi parametri potrebbero richiedere valori diversi a ogni avvio di runbook hello, è possibile aggiungere parametri di input tooyour runbook. Di seguito sono parametri di input tooadd hello passaggi:

1. Selezionare hello runbook grafico da hello **runbook** blade e quindi fare clic su [ **modifica** ](automation-graphical-authoring-intro.md) è.
2. Nell'editor di runbook hello, fare clic su **Input e output** tooopen hello **Input e output** blade.
   
    ![Runbook grafico di Automazione](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Hello **Input e output** pannello viene visualizzato un elenco di parametri di input definiti per il runbook hello. In questo pannello, è possibile aggiungere un nuovo parametro di input o modificare la configurazione di hello di un parametro di input esistente. tooadd un nuovo parametro per hello runbook, fare clic su **aggiungere input** tooopen hello **parametro di input Runbook** blade. Non esiste, è possibile configurare hello seguenti parametri:
   
   | **Proprietà** | **Descrizione** |
   |:--- |:--- |
   | Nome |Obbligatorio.  nome di Hello del parametro hello. Questo deve essere univoco all'interno di runbook hello e può contenere solo lettere, numeri o caratteri di sottolineatura. Deve iniziare con una lettera. |
   | Descrizione |Facoltativo. Descrizione dello scopo hello del parametro di input. |
   | Tipo |Facoltativo. tipo di dati Hello prevista per il valore del parametro hello. I tipi di parametro supportati sono **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**. Se un tipo di dati non è selezionato, il valore predefinito troppo**stringa**. |
   | Mandatory |Facoltativo. Specifica se è necessario specificare un valore per il parametro hello. Se si sceglie **Sì**, quindi è necessario fornire un valore alla hello runbook viene avviato. Se si sceglie **non**, un valore non è necessario quando hello runbook viene avviato e può essere impostato un valore predefinito. |
   | Default Value |Facoltativo. Specifica un valore che verrà utilizzato per il parametro hello se un valore non sia stato passato quando hello runbook viene avviato. È possibile impostare un valore predefinito per un parametro non obbligatorio. Scegliere un valore predefinito, tooset **personalizzato**. Questo valore viene utilizzato a meno che un altro valore viene fornito quando hello runbook viene avviato. Scegliere **Nessuno** se non si desidera tooprovide qualsiasi valore predefinito. |
   
    ![Aggiunta di nuovo input](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Creare due parametri con le proprietà che verranno utilizzate da hello seguenti hello **Get AzureRmVm** attività:
   
   * **Parametro 1:**
     
     * Nome: VMName
     * Tipo: String
     * Obbligatorio: no
   * **Parametro2:**
     
     * Nome: resourceGroupName
     * Tipo: String
     * Obbligatorio: no
     * Valore predefinito: personalizzato
     * Il valore predefinito personalizzato - \<nome hello del gruppo di risorse contenente le macchine virtuali hello >
5. Dopo aver aggiunto i parametri di hello, fare clic su **OK**.  È ora possibile visualizzarli in hello **Input e output blade**. Fare nuovamente clic su **OK**, quindi su **Salva** e **pubblicare** il runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Assegnare valori tooinput parametri nei runbook
È possibile passare valori tooinput parametri nei runbook in hello seguenti scenari.

### <a name="start-a-runbook-and-assign-parameters"></a>Avviare un runbook e assegnare parametri
Un runbook può essere avviato molti modi: tramite hello portale di Azure con un webhook, con i cmdlet di PowerShell, con l'API REST hello o con hello SDK. Di seguito vengono illustrati vari metodi per avviare un runbook e assegnare parametri.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Avviare un runbook pubblicato tramite il portale di Azure hello e assegnare i parametri
Quando si [avviare runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **avvia Runbook** pannello viene aperto ed è possibile configurare i valori per parametri hello appena creato.

![Iniziare a usare il portale di hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

In etichetta hello sotto la casella di hello input, è possibile visualizzare gli attributi di hello che sono stati impostati per il parametro hello. Gli attributi includono obbligatorio o facoltativo, tipo e valore predefinito. Nella hello Guida fumetto toohello parametro nome successivo, è possibile visualizzare tutte le informazioni chiave hello è necessario toomake decisioni sui valori dei parametri input. Queste informazioni indicano se un parametro è obbligatorio o facoltativo. Include inoltre il tipo di hello e il valore predefinito (se presente) e ad altre note utili.

![Fumetto della Guida](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> I parametri di tipo String supportano valori di stringa **vuoti** .  Immissione **[EmptyString]** nel parametro di input hello casella verrà passato un parametro di toohello una stringa vuota. I parametri di tipo String non supportano il passaggio di valori **Null** . Se si non passa qualsiasi parametro di stringa di valore toohello, quindi PowerShell verrà interpretarlo come null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Avviare un runbook pubblicato usando i cmdlet di PowerShell e assegnare parametri
* **Cmdlet di Azure Resource Manager:** è possibile avviare un runbook di Automazione creato in un gruppo di risorse usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Esempio:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Cmdlet di Gestione dei servizi di Azure:** è possibile avviare un runbook di automazione creato in un gruppo di risorse predefinito usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Esempio:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Quando si avvia un runbook con i cmdlet di PowerShell, un parametro predefinito, **MicrosoftApplicationManagementStartedBy** creato con il valore di hello **PowerShell**. È possibile visualizzare questo parametro in hello **processo dettagli** blade.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Avviare un runbook usando un SDK e assegnare parametri
* **Metodo di gestione delle risorse Azure:** è possibile avviare un runbook tramite hello SDK di un linguaggio di programmazione. Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione. È possibile visualizzare tutto il codice hello al nostro [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Metodo di gestione dei servizi Azure:** è possibile avviare un runbook tramite hello SDK di un linguaggio di programmazione. Di seguito è riportato un frammento di codice C# per l'avvio di un runbook nell'account di automazione. È possibile visualizzare tutto il codice hello al nostro [repository GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart questo metodo, creare un hello toostore dizionario di parametri del runbook, **VMName** e **resourceGroupName**e i relativi valori. Quindi, avviare runbook hello. Di seguito è hello c# frammento di codice per chiamare il metodo hello è definito in precedenza.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Avviare un runbook tramite l'API REST hello e assegnare i parametri
Un processo del runbook può essere creato e avviato con hello API REST di automazione di Azure tramite hello **inserire** metodo con hello seguente URI della richiesta.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Nell'URI della richiesta hello, sostituire hello seguenti parametri:

* **subscription-id:** ID della sottoscrizione di Azure.  
* **cloud-service-name:** hello Nome richiesta hello cloud servizio toowhich hello deve essere inviati.  
* **Automation-account-name:** hello dell'account di automazione che viene ospitato all'interno di hello Nome servizio cloud.  
* **id processo:** hello GUID per il processo di hello. GUID in PowerShell possono essere create usando hello **[GUID]::NewGuid(). ToString ()** comando.

Nel processo del runbook toohello parametri toopass ordine, utilizzare il corpo della richiesta hello. Avrà hello seguenti due proprietà fornita in formato JSON:

* **Nome del runbook:** obbligatorio. nome Hello del runbook hello toostart processo hello.  
* **Parametri del runbook:** facoltativi. Un dizionario di elenco di parametri hello (nome, valore) formato in cui nome deve essere di tipo stringa e può essere qualsiasi valore JSON valido.

Se si desidera hello toostart **Get AzureVMTextual** runbook che è stato creato in precedenza con **VMName** e **resourceGroupName** come parametri, utilizzare hello seguendo il formato JSON Per corpo della richiesta hello.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Se il processo di hello è stato creato, viene restituito un codice di stato HTTP 201. Per ulteriori informazioni su intestazioni e corpo della risposta hello, fare riferimento toohello articolo su come troppo[creare un processo del runbook con hello API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Eseguire il test di un runbook e assegnare parametri
Quando si [test hello versione bozza del runbook](automation-testing-runbook.md) utilizzando l'opzione di verifica hello, hello **Test** pannello viene aperto ed è possibile configurare i valori per parametri hello appena creato.

![Esecuzione di test e assegnazione di parametri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Collega un runbook tooa pianificazione e assegnare i parametri
È possibile [collegare una pianificazione](automation-schedules.md) tooyour runbook in modo tale runbook hello viene avviato in un momento specifico. Assegnare i parametri di input quando si crea una pianificazione hello e hello runbook userà questi valori quando viene avviato dalla pianificazione hello. È possibile salvare la pianificazione hello fino a quando non vengono forniti tutti i valori di parametro obbligatorio.

![Pianificazione e assegnazione di parametri](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Creare un webhook per un runbook e assegnare parametri
È possibile creare un [webhook](automation-webhooks.md) per il runbook e configurare i parametri di input del runbook. Impossibile salvare il webhook hello fino a quando non vengono forniti tutti i valori di parametro obbligatorio.

![Creazione di webhook e assegnazione di parametri](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Quando si eseguirà un runbook tramite un webhook hello predefiniti di parametro di input  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  viene inviato, insieme ai parametri di input di hello è definito. È possibile fare clic su hello tooexpand **WebhookData** parametro per maggiori dettagli.

![Parametro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni su input e output dei runbook, vedere l'articolo [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automazione di Azure: input e output del runbook e runbook nidificati).
* Per informazioni dettagliate sui diversi modi toostart un runbook, vedere [avvio di un runbook](automation-starting-a-runbook.md).
* tooedit un runbook testuale, fare riferimento troppo[modifica runbook testuale](automation-edit-textual-runbook.md).
* tooedit un runbook grafico, fare riferimento troppo[grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).

