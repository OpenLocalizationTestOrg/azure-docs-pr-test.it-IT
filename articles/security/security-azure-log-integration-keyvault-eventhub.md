---
title: registri aaaIntegrate dall'insieme di credenziali chiave di Azure tramite gli hub di eventi | Documenti Microsoft
description: Esercitazione hello necessarie toomake insieme di credenziali chiave registri disponibile tooa SIEM tramite l'integrazione di Log di Azure
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Esercitazione sull'integrazione dei log di Azure: elaborazione degli eventi di Azure Key Vault tramite Hub eventi

È possibile utilizzare gli eventi registrati tooretrieve integrazione di Log di Azure e renderli disponibili tooyour sicurezza informazioni ed eventi (SIEM) sistema di gestione. Questa esercitazione viene illustrato un esempio di come integrazione di Log di Azure può essere utilizzato tooprocess registri acquisite tramite hub di eventi di Azure.
 
Utilizzare questa esercitazione tooget familiarità con la modalità di integrazione di Log di Azure e hub eventi lavoro insieme dal seguente hello procedure di esempio e comprensione del modo in cui ogni passaggio supporta soluzioni hello. Quindi è possibile eseguire ciò che si è appreso qui toocreate proprio toosupport passaggi requisiti univoci della società.

>[!WARNING]
Hello passaggi e comandi in questa esercitazione non sono previsti toobe copiati e incollati. Si tratta solo di esempi. Non utilizzare i comandi di PowerShell hello "così com'è" nell'ambiente in tempo reale. in quanto devono essere personalizzati in base all'ambiente univoco.


In questa esercitazione viene illustrato il processo di hello di recupero di hub di eventi registrati tooan attività insieme credenziali chiavi Azure e rende disponibile come sistema SIEM tooyour file JSON. È quindi possibile configurare i file JSON di SIEM sistema tooprocess hello.

>[!NOTE]
>La maggior parte dei passaggi di hello in questa esercitazione implica la configurazione di insiemi di credenziali chiave, gli account di archiviazione e gli hub di eventi. passaggi per l'integrazione di Log di Azure specifici Hello sono alla fine di hello di questa esercitazione. Non eseguire questi passaggi in un ambiente di produzione. Sono concepiti solo per un ambiente lab. Prima di utilizzarli nell'ambiente di produzione, è necessario personalizzare i passaggi di hello.

Informazioni fornite lungo hello modo consente che comprendere motivazioni hello alla base di ogni passaggio. Gli articoli tooother collegamenti forniscono maggiori dettagli su determinati argomenti.

Per ulteriori informazioni sui servizi hello menzionato in questa esercitazione, vedere: 

- [Insieme di credenziali chiave Azure](../key-vault/key-vault-whatis.md)
- [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Integrazione dei log di Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Configurazione iniziale

Prima di poter completare i passaggi di hello in questo articolo, è necessario hello segue:

1. Una sottoscrizione di Azure e l'account per tale sottoscrizione con diritti di amministratore. Se non si ha una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/).
 
2. Un sistema con accesso toohello internet che soddisfa i requisiti di hello per l'installazione di integrazione di Log di Azure. sistema Hello può trovarsi su un servizio cloud oppure ospitato in locale.

3. [Integrazione dei log di Azure](https://www.microsoft.com/download/details.aspx?id=53324) installato. tooinstall è:

   a. Utilizzare Desktop remoto tooconnect toohello sistema indicato nel passaggio 2.   
   b. Copiare sistema toohello programma di installazione di hello integrazione di Log di Azure. È possibile [scaricare il file di installazione di hello](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Avviare Installazione guidata di hello e accettazione delle condizioni di licenza Software Microsoft hello.   
   d. Se si fornisce informazioni di telemetria, lasciare selezionata hello casella di controllo. Se invece non inviare tooMicrosoft informazioni sull'utilizzo, deselezionare la casella di controllo hello.
   
   Per ulteriori informazioni sull'integrazione di Log di Azure e come tooinstall, vedere [integrazione di Log di Azure con la registrazione di diagnostica di Azure e l'inoltro degli eventi di Windows](security-azure-log-integration-get-started.md).

4. Hello PowerShell più recente.
 
   Se è installato Windows Server 2016 e la versione disponibile di PowerShell è almeno la versione 5.0. Se si usa qualsiasi altra versione di Windows Server, l'utente potrebbe aver installato una versione precedente di PowerShell. È possibile controllare la versione hello immettendo ```get-host``` in una finestra di PowerShell. Se PowerShell 5.0 non è installato, è possibile [scaricarlo](https://www.microsoft.com/download/details.aspx?id=50395).

   Dopo aver creato almeno PowerShell 5.0, è possibile passare una versione più recente di tooinstall hello:
   
   a. In una finestra di PowerShell, immettere hello ```Install-Module Azure``` comando. Completare i passaggi di installazione di hello.    
   b. Immettere hello ```Install-Module AzureRM``` comando. Completare i passaggi di installazione di hello.

   Per altre informazioni, vedere [Installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Creare elementi dell'infrastruttura di supporto

1. Aprire una finestra di PowerShell con privilegi elevata e passare troppo**C:\Program Files\Microsoft Azure Log integrazione**.
2. Importare i cmdlet AzLog hello eseguendo script hello LoadAzLogModule.ps1. Immettere hello `.\LoadAzLogModule.ps1` comando. (Hello notifica ". \" in quel comando.) Verrà visualizzata una schermata analoga alla seguente:</br>

   ![Elenco dei moduli caricati](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Immettere hello `Login-AzureRmAccount` comando. Nella finestra di accesso hello, immettere le informazioni sulle credenziali hello per sottoscrizione hello che verrà utilizzato per questa esercitazione.

   >[!NOTE]
   >Se si tratta hello prima volta che ci si connette in tooAzure da questo computer, si verrà visualizzato un messaggio su come consentire i dati di utilizzo di PowerShell toocollect Microsoft. È consigliabile abilitare questa raccolta di dati in quanto sarà tooimprove usato Azure PowerShell.

4. Dopo l'autenticazione, si è connessi e visualizzati informazioni hello in hello seguente schermata. Prendere nota del nome della sottoscrizione hello ID e la sottoscrizione, poiché sarà necessario toocomplete i passaggi in un secondo momento.

   ![Finestra di PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Creare variabili valori toostore che verranno utilizzati in un secondo momento. Immettere ogni hello seguendo le linee di PowerShell. Potrebbe essere necessario tooadjust hello valori toomatch l'ambiente.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` Il nome della sottoscrizione potrebbe essere diverso. È possibile visualizzarlo come parte dell'output di hello del comando precedente hello.)
    - ```$location = 'West US'```(Questa variabile è il percorso di hello toopass utilizzati in cui le risorse devono essere create. È possibile modificare questa variabile toobe qualsiasi posizione di propria scelta.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(possibile scegliere qualsiasi nome hello, ma deve includere solo lettere minuscole e numeri).
    - ``` $storageName = $name```(Verrà utilizzata questa variabile per il nome di account di archiviazione hello).
    - ```$rgname = $name ```(Verrà utilizzata questa variabile per nome gruppo di risorse hello).
    - ``` $eventHubNameSpaceName = $name```(Si tratta di nome hello dello spazio dei nomi di hub eventi hello).
6. Specificare una sottoscrizione di hello che verranno usate con:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Creare un gruppo di risorse:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Se si immette `$rg` a questo punto, dovrebbe essere simile schermata di toothis output:

   ![Output dopo la creazione di un gruppo di risorse](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Creare un account di archiviazione che verrà utilizzato tookeep traccia delle informazioni sullo stato:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Creare spazio dei nomi hub di eventi hello. Questo è necessario toocreate un hub eventi.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Ottenere l'ID regola hello che verrà utilizzato con il provider di insights hello:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Ottenere tutti i possibili percorsi di Azure e aggiungere hello nomi tooa variabile può essere utilizzato in un passaggio successivo:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Se si immette `$locations` a questo punto, verranno visualizzati i nomi di percorso di hello senza informazioni aggiuntive di hello restituite da Get-AzureRmLocation.
12. Creare un profilo di log di Azure Resource Manager: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Per ulteriori informazioni su hello profilo log di Azure, vedere [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> È possibile che venga visualizzato un messaggio di errore quando si tenta di toocreate un profilo di log. È quindi possibile controllare la documentazione di hello per Get-AzureRmLogProfile e Remove-AzureRmLogProfile. Se si esegue Get AzureRmLogProfile, vedrai informazioni sul profilo log hello. È possibile eliminare il profilo di log esistente hello immettendo hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.
>
>![Errore del profilo di Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi

1. Creare l'insieme di credenziali chiave di hello:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Configurare la registrazione per l'insieme di credenziali chiave hello:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Generare l'attività di log

Le richieste devono toobe inviati tooKey attività del log toogenerate insieme di credenziali. Azioni quali la generazione di chiavi, l'archiviazione di segreti o la lettura di segreti da Key Vault creeranno le voci dei log.

1. Visualizzare le chiavi di archiviazione corrente hello:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Generare un nuovo **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Visualizzare nuovamente le chiavi di hello e verificare che **key2** contiene un valore diverso:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Impostare e leggere un segreto toogenerate voci di log aggiuntive:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segreto restituito](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Configurare Integrazione dei log di Azure

Dopo aver configurato tutti hello elementi obbligatori toohave registrazione insieme credenziali chiavi tooan hub eventi, è necessario tooconfigure integrazione di Log di Azure:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Eseguire il comando AzLog hello per ogni hub eventi:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Dopo un minuto e dell'esecuzione hello ultimi due comandi, verrà visualizzato il file JSON generati. È possibile confermare che il monitoraggio directory hello **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Passaggi successivi

- [Domande frequenti su Integrazione dei log di Azure](security-azure-log-integration-faq.md)
- [Introduzione all'integrazione dei log di Azure](security-azure-log-integration-get-started.md)
- [Integrare i log delle risorse di Azure nei sistemi SIEM](security-azure-log-integration-overview.md)
