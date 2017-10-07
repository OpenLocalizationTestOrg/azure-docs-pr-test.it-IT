---
title: con le funzioni di Azure e gli avvisi di monitoraggio di rete aaaUse pacchetto acquisizione toodo proattiva | Documenti Microsoft
description: In questo articolo viene descritto come un avviso toocreate attivata acquisizione pacchetto con il Watcher di rete di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Usare l'acquisizione di pacchetti per il monitoraggio proattivo della rete con avvisi e Funzioni di Azure

Acquisizione di pacchetti di rete controllo crea le sessioni di acquisizione tootrack traffico da e verso le macchine virtuali. Hello file di acquisizione può avere un filtro definito tootrack hello solo il traffico che si desidera toomonitor. Questi dati vengono quindi archiviati in un blob di archiviazione o in locale nella macchina guest hello.

Questa funzionalità può essere avviata in remoto da altri scenari di automazione, ad esempio Funzioni di Azure. Consente di acquisizione di pacchetti a che Hello proattiva acquisizioni toorun funzionalità in base definito anomalie di rete. Altri utilizzi comprendono la raccolta di statistiche di rete, l'ottenimento di informazioni sulle intrusioni nella rete, il debug delle comunicazioni client-server e molto altro ancora.

Le risorse distribuite in Azure sono in esecuzione 24 ore su 24, 7 giorni su 7. I tecnici non è possibile monitorare attivamente lo stato di hello di tutte le risorse 24/7. Si pensi a cosa può accadere se si verifica un problema alle 2 del mattino.

Utilizzando Watcher di rete, avvisi e funzioni dall'interno di hello ecosistema di Azure, è possibile in modo proattivo rispondere con problemi di toosolve hello strumenti e i dati nella rete.

![Scenario][scenario]

## <a name="prerequisites"></a>Prerequisiti

* versione più recente di Hello di [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Un'istanza esistente di Network Watcher. Se non è già presente, creare un'[istanza di Network Watcher](network-watcher-create.md).
* Una macchina virtuale esistente in hello stessa area Watcher di rete con hello [estensione Windows](../virtual-machines/windows/extensions-nwa.md) o [estensione della macchina virtuale Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Scenario

In questo esempio, la macchina virtuale invia più segmenti TCP superiore al normale e si desidera toobe un avviso. Come esempio qui vengono usati i segmenti TCP, ma è possibile usare qualsiasi condizione di avviso.

Quando viene generato un avviso, è opportuno tooreceive toounderstand di dati a livello di pacchetto perché la comunicazione è è aumentato. È quindi possibile eseguire passaggi comunicazione tooregular della macchina virtuale tooreturn hello.

Questo scenario presuppone che esistano già un'istanza di Network Watcher e un gruppo di risorse con una macchina virtuale valida.

Hello seguente elenco viene fornita una panoramica del flusso di lavoro hello che ha luogo:

1. Nella macchina virtuale viene attivato un avviso.
1. avviso di Hello chiama la funzione di Azure tramite un webhook.
1. La funzione Azure elabora avviso hello e avvia una sessione di acquisizione pacchetto Watcher di rete.
1. acquisizione di pacchetti Hello viene eseguito su hello VM e raccoglie il traffico.
1. Hello file di acquisizione pacchetto viene caricato tooa account di archiviazione per la revisione e la diagnosi.

tooautomate questo processo, viene creata e la connessione di un avviso nel nostro tootrigger VM quando si verifica l'evento imprevisto di hello. È inoltre possibile creare toocall una funzione in Watcher di rete.

Questo scenario hello seguenti:

* Crea una funzione di Azure che avvia un'acquisizione di pacchetti.
* Crea una regola di avviso in una macchina virtuale e configura hello toocall di regola di avviso hello Azure (funzione).

## <a name="create-an-azure-function"></a>Creare una funzione di Azure

primo passaggio Hello è toocreate un avviso di hello tooprocess funzione Azure e creare un'acquisizione di pacchetti.

1. In hello [portale di Azure](https://portal.azure.com)selezionare **New** > **calcolo** > **funzione App**.

    ![Creazione di un'app per le funzioni][1-1]

2. In hello **funzione App** pannello, immettere i seguenti valori hello e quindi selezionare **OK** toocreate hello app:

    |**Impostazione** | **Valore** | **Dettagli** |
    |---|---|---|
    |**Nome app**|PacketCaptureExample|nome Hello di hello funzione app.|
    |**Sottoscrizione**|[La sottoscrizione] hello sottoscrizione per le app di funzione hello toocreate.||
    |**Gruppo di risorse**|PacketCaptureRG|Hello risorsa gruppo toocontain hello funzione app.|
    |**Piano di hosting**|Piano a consumo| tipo Hello di pianificare l'applicazione utilizzi (funzione). Le opzioni sono Consumo e Piano di servizio app di Azure. |
    |**Posizione**|Stati Uniti centrali| area Hello nella quale app di funzione hello toocreate.|
    |**Storage Account**|{generato automaticamente}| account di archiviazione Hello necessarie funzioni di Azure per l'archiviazione di uso generale.|

3. In hello **PacketCaptureExample funzione app** pannello seleziona **funzioni** > **funzione personalizzata**  >  **+**.

4. Selezionare **HttpTrigger Powershell**, quindi immettere hello rimanenti informazioni. Infine, toocreate hello funzione, selezionare **crea**.

    |**Impostazione** | **Valore** | **Dettagli** |
    |---|---|---|
    |**Scenario**|Sperimentale|Tipo di scenario|
    |**Dare un nome alla funzione**|AlertPacketCapturePowerShell|Nome della funzione hello|
    |**Livello di autorizzazione**|Funzione|Livello di autorizzazione per la funzione hello|

![Esempio di funzioni][functions1]

> [!NOTE]
> modello di PowerShell Hello è sperimentale e non dispone del supporto completo.

Le personalizzazioni sono necessari per questo esempio e vengono spiegate in hello alla procedura seguente.

### <a name="add-modules"></a>Aggiungere moduli

cmdlet di PowerShell Watcher di rete, toouse caricare hello app più recente di PowerShell modulo toohello (funzione).

1. Nel computer locale con hello più recente di Azure PowerShell i moduli installati, eseguire il comando PowerShell seguente hello:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    In questo modo di esempio hello percorso locale dei moduli di Azure PowerShell. Queste cartelle verranno usate in un passaggio successivo. i moduli di Hello che vengono utilizzati in questo scenario sono:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Cartelle di PowerShell][functions5]

1. Selezionare **funzione impostazioni app** > **passare tooApp servizio Editor**.

    ![Impostazioni dell'app per le funzioni][functions2]

1. Pulsante destro del mouse hello **AlertPacketCapturePowershell** cartella, quindi creare una cartella denominata **azuremodules**. 

4. Creare una sottocartella per ogni modulo necessario.

    ![Cartelle e sottocartelle][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Pulsante destro del mouse hello **AzureRM.Network** sottocartella e quindi selezionare **Carica file**. 

6. Passare tooyour Azure i moduli. Hello locale **AzureRM.Network** cartella, selezionare tutti i file hello nella cartella hello. Selezionare **OK**. 

7. Ripetere questi passaggi per **AzureRM.Profile** e **AzureRM.Resources**.

    ![Caricare file][functions6]

1. Dopo aver completato, ogni cartella deve disporre di file di modulo di PowerShell hello dal computer locale.

    ![File di PowerShell][functions7]

### <a name="authentication"></a>Autenticazione

i cmdlet di PowerShell toouse hello, è necessario eseguire l'autenticazione. Configurare l'autenticazione nell'app di funzione hello. l'autenticazione tooconfigure, è necessario configurare le variabili di ambiente e caricare un'app di funzione toohello file della chiave crittografata.

> [!NOTE]
> Questo scenario fornisce solo un esempio di come l'autenticazione tooimplement con le funzioni di Azure. Esistono altri modi toodo questo.

#### <a name="encrypted-credentials"></a>Credenziali crittografate

Hello lo script di PowerShell seguente crea un file di chiave denominato **PassEncryptKey.key**. Fornisce inoltre una versione crittografata della password hello fornito. Questa password è hello stessa password definita per un'applicazione hello Azure Active Directory che viene utilizzata per l'autenticazione.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

Nell'Editor di servizio App di app di funzione hello hello, creare una cartella denominata **chiavi** in **AlertPacketCapturePowerShell**. Caricare quindi hello **PassEncryptKey.key** file creato nel precedente esempio di PowerShell hello.

![Chiave delle funzioni][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Recuperare i valori per le variabili di ambiente

requisito finale Hello è tooset variabili di ambiente hello che sono valori hello tooaccess necessarie per l'autenticazione. Hello elenco seguente mostra le variabili di ambiente hello creati:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

ID client hello è hello ID applicazione di un'applicazione in Azure Active Directory.

1. Se si dispone già di un'applicazione toouse, eseguire un'applicazione hello toocreate riportato di seguito.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > password di Hello utilizzati durante la creazione di un'applicazione hello deve essere hello stessa password creato in precedenza durante il salvataggio dei file di chiave hello.

1. Nel portale di Azure hello, selezionare **sottoscrizioni**. Selezionare hello toouse di sottoscrizione, quindi **Access control (IAM)**.

    ![IAM delle funzioni][functions9]

1. Scegliere toouse account hello e quindi selezionare **proprietà**. Copiare l'ID applicazione hello

    ![ID applicazione per le funzioni][functions10]

#### <a name="azuretenant"></a>AzureTenant

Ottenere l'ID tenant hello eseguendo hello seguente esempio di PowerShell:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

valore di Hello della variabile di ambiente AzureCredPassword hello è valore hello ottenute dall'esecuzione hello seguente esempio di PowerShell. In questo esempio è hello corrisponde a quello illustrato nella precedente hello **le credenziali crittografate** sezione. valore che è necessario Hello hello output di hello `$Encryptedpassword` variabile.  Si tratta di hello principale password del servizio che si è crittografato tramite script di PowerShell hello.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Archiviare le variabili di ambiente hello

1. Passare toohello funzione app. Selezionare quindi **Impostazioni dell'app per le funzioni** > **Configurare le impostazioni dell'app**.

    ![Configurare le impostazioni applicazione][functions11]

1. Aggiungere le variabili di ambiente hello e le relative impostazioni di app toohello di valori e quindi selezionare **salvare**.

    ![Impostazioni app][functions12]

### <a name="add-powershell-toohello-function"></a>Aggiungi funzione toohello di PowerShell

È in corso tempo toomake chiama Watcher di rete all'interno di hello Azure (funzione). A seconda dei requisiti di hello, l'implementazione di hello di questa funzione può variare. Tuttavia, il flusso generale di hello di codice hello è:

1. Elaborare i parametri di input.
2. Pacchetto esistente query acquisisce tooverify limiti e risolvere i conflitti di nome.
3. Creare un'acquisizione di pacchetti con i parametri appropriati.
4. Eseguire periodicamente il polling dell'acquisizione di pacchetti fino al completamento.
5. Notifica utente hello che sessione di acquisizione di pacchetti hello è stata completata.

Hello esempio seguente il codice di PowerShell che può essere utilizzato nella funzione hello. Sono presenti valori che devono toobe sostituito per **subscriptionId**, **resourceGroupName**, e **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Recuperare l'URL di hello (funzione) 
1. Dopo aver creato la funzione, è possibile configurare l'URL di hello toocall avviso associato a funzione hello. tooget questo valore, l'URL di funzione hello copia dall'app di funzione.

    ![URL di individuazione hello (funzione)][functions13]

2. Copia URL funzione hello per l'app di funzione.

    ![Copia l'URL di hello (funzione)][2]

Se si richiedono proprietà personalizzate nel payload hello della richiesta POST per hello webhook, fare riferimento troppo[configurare un webhook su un avviso di metrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Configurare un avviso in una VM

Gli avvisi possono essere singoli utenti configurato toonotify quando una metrica specifica supera una soglia assegnato tooit. In questo esempio è di avviso hello in hello segmenti TCP inviati, ma hello avviso può essere attivato per molte altre metriche. In questo esempio, un avviso è configurata toocall una funzione di hello toocall webhook.

### <a name="create-hello-alert-rule"></a>Creare una regola di avviso hello

Macchina virtuale esistente tooan go e quindi aggiungere una regola di avviso. Per informazioni più dettagliate sulla configurazione di avvisi, vedere [Creazione di avvisi in Monitoraggio di Azure per i servizi Azure - Portale di Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Immettere i seguenti valori hello hello **regola di avviso** blade e quindi selezionare **OK**.

  |**Impostazione** | **Valore** | **Dettagli** |
  |---|---|---|
  |**Nome**|TCP_Segments_Sent_Exceeded|Nome della regola di avviso hello.|
  |**Descrizione**|Soglia superata segmenti TCP inviati|descrizione di Hello per regola di avviso hello.||
  |**Metrica**|Segmenti TCP inviati| Hello toouse metrica tootrigger hello dell'avviso. |
  |**Condition**|Maggiore di| Hello toouse condizione durante la valutazione della metrica hello.|
  |**Soglia**|100| valore di Hello della metrica hello che Attiva avviso hello. Questo valore deve essere impostato tooa valore valido per l'ambiente.|
  |**Periodo**|Su hello ultimi 5 minuti| Determina il periodo di hello in cui toolook per soglia hello in metrica hello.|
  |**Webhook**|[URL webhook dell'app per le funzioni]| URL del webhook Hello da app di funzione hello creato nei passaggi precedenti hello.|

> [!NOTE]
> metrica di segmenti TCP Hello non è abilitato per impostazione predefinita. Per ulteriori informazioni su tooenable altre metriche visitando [attivazione del monitoraggio e diagnostica](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Esaminare i risultati di hello

Dopo aver criteri hello per i trigger di avviso hello, viene creata un'acquisizione di pacchetti. Passare tooNetwork controllo e quindi selezionare **acquisizione pacchetto**. In questa pagina, è possibile selezionare hello acquisizione file collegamento toodownload hello pacchetto acquisizione di pacchetti.

![Visualizzare l'acquisizione di pacchetti][functions14]

Se il file di acquisizione hello è archiviato in locale, è possibile recuperare, effettuando l'accesso alla macchina virtuale toohello.

Per istruzioni relative al download di file dagli account di archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Un altro strumento è [Storage Explorer](http://storageexplorer.com/).

Dopo il download dell'acquisizione, è possibile visualizzarla con qualsiasi strumento per la lettura di un file **.cap**. Di seguito sono collegamenti tootwo di questi strumenti:

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooview acquisisce il pacchetto, visitare il sito [analysis acquisizione pacchetto con Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
