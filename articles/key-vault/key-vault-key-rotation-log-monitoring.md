---
title: aaaSet backup insieme credenziali chiavi Azure con la rotazione della chiave end-to-end e il controllo | Documenti Microsoft
description: Utilizzare questa procedura-tootoohelp che impostare rotazione delle chiavi e i registri di monitoraggio dell'insieme di credenziali chiave.
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Configurare l'insieme di credenziali delle chiavi di Azure con rotazione e controllo delle chiavi end-to-end
## <a name="introduction"></a>Introduzione
Dopo la creazione di credenziali delle chiavi, sarà in grado di toostart utilizzando toostore tale insieme di credenziali, le chiavi e segreti. Le applicazioni non è più necessitano toopersist le chiavi o i segreti, ma piuttosto verranno richiesti dall'insieme di credenziali chiave hello in base alle esigenze. Ciò permette tooupdate chiavi e segreti senza influire sul comportamento di hello dell'applicazione, che consente un'ampia gamma di possibilità per la chiave e la gestione di informazioni segrete.

Questo articolo descrive un esempio di utilizzo insieme credenziali chiavi Azure toostore un segreto, in questo caso una chiave dell'Account di archiviazione Azure che si accede da un'applicazione. Dimostra anche l'implementazione di una rotazione pianificata della chiave dell'account di archiviazione. Infine, esamina una dimostrazione di come toomonitor hello i log di controllo dell'insieme di credenziali chiave e generano avvisi quando vengono effettuate le richieste impreviste.

> [!NOTE]
> In questa esercitazione non è previsto tooexplain dettaglio hello la configurazione iniziale di credenziali delle chiavi. Per altre informazioni, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md). Per le istruzioni relative all'interfaccia della riga di comando multipiattaforma, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Configurare l'insieme di credenziali delle chiavi
tooenable un tooretrieve applicazione un segreto dall'insieme di credenziali chiave, è necessario creare segreto hello e caricarlo tooyour insieme di credenziali. Questo può essere eseguito avviando una sessione di PowerShell di Azure e la firma in tooyour account Azure con hello comando seguente:

```powershell
Login-AzureRmAccount
```

Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password. PowerShell recupera tutte le sottoscrizioni di hello che sono associate a questo account. Usa PowerShell hello primo per impostazione predefinita.

Se si dispone di più sottoscrizioni, potrebbe essere toospecify hello che è stato utilizzato toocreate credenziali delle chiavi. Immettere hello sottoscrizioni hello toosee per l'account di seguito:

```powershell
Get-AzureRmSubscription
```

sottoscrizione di hello toospecify è associato alla chiave dell'insieme di credenziali di hello effettuerà l'accesso, immettere:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Dato che questo articolo illustra l'archiviazione di una chiave dell'account di archiviazione come segreto, è necessario ottenere la chiave dell'account di archiviazione.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Dopo aver recuperato il segreto (in questo caso, la chiave di account di archiviazione), è necessario convertire la stringa sicura tooa e quindi creare una chiave privata con tale valore nell'insieme di credenziali chiave.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Quindi, è possibile ottenere hello URI per il segreto hello che è stato creato. Quando si chiama hello tooretrieve di insieme di credenziali chiave segreta viene utilizzato in un passaggio successivo. Eseguire il comando PowerShell seguente hello e prendere nota del valore di ID hello, ovvero segreto hello URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Configurare un'applicazione hello
Dopo aver creato un segreto archiviato, è possibile utilizzare codice tooretrieve e utilizzarlo. Esistono alcuni tooachieve necessarie di passaggi questo. Hello primo e più importante passaggio è registrazione dell'applicazione con Azure Active Directory e quindi di comunicare le informazioni dell'applicazione insieme di credenziali chiave in modo che questa operazione può consentire le richieste dall'applicazione.

> [!NOTE]
> L'applicazione deve essere creato in hello stesso tenant di Azure Active Directory come credenziali delle chiavi.
>
>

Aprire scheda applicazioni hello di Azure Active Directory.

![Aprire applicazioni in Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Scegliere **aggiungere** tooadd un tooyour applicazione Azure Active Directory.

![Scegliere Aggiungi](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Lasciare il tipo di applicazione hello come **applicazione WEB, e/o API WEB** e assegnare un nome di applicazione.

![Applicazione hello nome](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Immettere **URL accesso** e **URI ID app** per l'applicazione. È possibile usare qualsiasi valore per questa demo. Sarà comunque possibile modificarli in un secondo momento se necessario.

![Specificare gli URI necessari](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Dopo l'aggiunta di un'applicazione hello tooAzure Active Directory, verrà inserito nella pagina dell'applicazione hello. Fare clic su hello **configura** scheda e quindi individuare e copiare hello **ID Client** valore. Prendere nota dell'ID client hello per i passaggi successivi.

Generare quindi una chiave per l'applicazione in modo che possa interagire con Azure Active Directory. È possibile creare questo in hello **chiavi** sezione hello **configurazione** scheda. Prendere nota della chiave di hello appena generato dall'applicazione Azure Active Directory per l'utilizzo in un passaggio successivo.

![Chiavi delle applicazioni di Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Prima di stabilire tutte le chiamate dall'applicazione in insieme di credenziali chiave di hello, è necessario indicare l'insieme di credenziali chiave hello sull'applicazione e le relative autorizzazioni. Hello comando seguente accetta hello insieme di credenziali nome e ID client hello da app di Azure Active Directory e concede **ottenere** accesso tooyour chiave dell'insieme di credenziali per un'applicazione hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

A questo punto, si è pronti toostart compilazione l'applicazione chiama. Nell'applicazione, è necessario installare hello NuGet pacchetti necessari toointeract con l'insieme di credenziali chiave di Azure e Azure Active Directory. Dalla console di gestione di pacchetti di Visual Studio hello, immettere hello i comandi seguenti. Al momento della stesura di hello di questo articolo, versione corrente di hello del pacchetto di Azure Active Directory hello è 3.10.305231913, pertanto si tooconfirm versione più recente di hello e aggiornare di conseguenza.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

Nel codice dell'applicazione, creare un metodo della classe toohold hello per l'autenticazione di Azure Active Directory. In questo esempio, la classe è denominata **Utils**. Aggiungere hello seguente istruzione using:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Successivamente, aggiungere hello seguente token di metodo tooretrieve hello JWT da Azure Active Directory. Per manutenzione, è consigliabile valori stringa hardcoded di hello toomove alla configurazione del web o applicazione.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Aggiungere hello codice necessario toocall insieme di credenziali chiave e recuperare il valore segreto. È innanzitutto necessario aggiungere il seguente hello istruzione using:

```csharp
using Microsoft.Azure.KeyVault;
```

Aggiungere tooinvoke chiamate di metodo hello insieme di credenziali chiave e recuperare il segreto. In questo metodo, fornire il segreto hello URI che è stato salvato in un passaggio precedente. Si noti utilizzo hello di hello **GetToken** metodo hello **Utils** classe creata in precedenza.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Quando si esegue l'applicazione, si dovrebbe ora autenticazione tooAzure Active Directory e quindi recuperare il valore segreto dall'insieme di credenziali chiave di Azure.

## <a name="key-rotation-using-azure-automation"></a>Rotazione delle chiavi con Automazione di Azure
Sono disponibili diverse opzioni per l'implementazione di una strategia di rotazione per i valori memorizzati come segreti dell'insieme di credenziali delle chiavi di Azure. La rotazione dei segreti può essere eseguita nell'ambito di un processo manuale, a livello di codice usando chiamate API oppure con uno script di automazione. Ai fini di hello di questo articolo, sarà con Azure PowerShell combinato con automazione di Azure toochange una chiave di accesso di Account di archiviazione Azure. Verrà quindi aggiornato un segreto dell'insieme di credenziali delle chiavi con la nuova chiave.

tooallow automazione di Azure tooset i valori dei segreti nell'insieme di credenziali chiave, è necessario ottenere l'ID client hello per connessione hello denominato AzureRunAsConnection, che è stata creata quando è stata stabilita l'istanza di automazione di Azure. È possibile trovare l'ID scegliendo **Asset** dall'istanza di Automazione di Azure. Da qui, si sceglie **connessioni** e quindi selezionare hello **AzureRunAsConnection** principio del servizio. Prendere nota di hello **ID applicazione**.

![ID client di Automazione di Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

In **Asset** scegliere **Moduli**. Da **moduli**selezionare **raccolta**e quindi cercare e **importazione** le versioni aggiornate di ciascuno dei seguenti moduli hello:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> Al momento della stesura di hello di questo articolo, hello indicato in precedenza i moduli necessari toobe aggiornata solo per lo script seguente hello. Se si verificano errori nel processo di automazione, verificare di avere importato tutti i moduli necessari e le relative dipendenze.
>
>

Dopo avere recuperato ID applicazione hello per la connessione di automazione di Azure, è necessario che l'insieme di credenziali chiave che l'applicazione disponga di accesso tooupdate segreti nell'insieme di credenziali. Questo può essere eseguita con hello comando PowerShell seguente:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Selezionare quindi **Runbook** nell'istanza di Automazione di Azure e quindi selezionare **Aggiungi runbook**. Selezionare **Creazione rapida**. Nome del runbook, quindi selezionare **PowerShell** come tipo di runbook hello. È necessario hello opzione tooadd una descrizione. Fare infine clic su **Crea**.

![Creare un runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Incollare lo script di PowerShell nel riquadro dell'editor per il nuovo runbook hello seguente hello:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

Riquadro editor hello scegliere **riquadro Test** tootest lo script. Hello script viene eseguito senza errori, è possibile selezionarlo **pubblica**, ed è quindi possibile applicare una pianificazione per hello runbook nel riquadro di configurazione del runbook hello.

## <a name="key-vault-auditing-pipeline"></a>Pipeline di controllo dell'insieme di credenziali delle chiavi
Quando si configura un insieme di credenziali chiave, è possibile attivare il controllo toocollect accede toohello chiave insieme di credenziali di accesso richieste. Questi log vengono archiviati in un apposito account di archiviazione di Azure e possono essere estratti, monitorati e analizzati. Hello nello scenario seguente Usa funzioni di Azure, App per la logica di Azure e insieme di credenziali chiave audit log toocreate toosend una pipeline tramite posta elettronica quando un'app che corrisponde a hello app ID dell'app web hello recupera i segreti dall'insieme di credenziali hello.

È prima di tutto necessario abilitare la registrazione per l'insieme di credenziali delle chiavi. Questa operazione può essere eseguita tramite i seguenti comandi PowerShell hello (è possibile visualizzare i dettagli completi [chiave dell'insieme di credenziali-registrazione](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Dopo questa opzione è abilitata, i log di controllo Avvia la raccolta in hello designato account di archiviazione. Questi log contengono eventi relativi alla modalità di accesso all'insieme di credenziali delle chiavi, a quando avviene l'accesso e a chi lo esegue.

> [!NOTE]
> È possibile accedere a informazioni di registrazione 10 minuti dopo l'operazione di insieme di credenziali chiave hello. ma in genere saranno disponibili anche prima.
>
>

passaggio successivo Hello è troppo[creare una coda di Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Questa è la posizione in cui verrà eseguito il push dei log di controllo dell'insieme di credenziali delle chiavi. Quando i messaggi di log di controllo hello presenti nella coda di hello, hello logica app li preleva e interviene su di essi. Creare un bus di servizio con hello alla procedura seguente:

1. Creare uno spazio dei nomi del Bus di servizio (se si dispone già di quello che si desidera toouse a tale scopo, ignorare tooStep 2).
2. Selezionare il bus di servizio toohello hello portale di Azure e spazio dei nomi selezionare hello coda hello toocreate in.
3. Selezionare **New** e scegliere **Service Bus > coda** e immettere i dettagli di hello necessario.
4. Selezionare informazioni di connessione del Bus di servizio hello scegliendo hello dello spazio dei nomi e fare clic su **informazioni di connessione**. Queste informazioni è necessario per la sezione successiva di hello.

Successivamente, [creare una funzione Azure](../azure-functions/functions-create-first-azure-function.md) toopoll insieme di credenziali chiave interno hello account di archiviazione e registri prelevati nuovi eventi. Questa funzione verrà attivata in base alla pianificazione.

toocreate una funzione di Azure, scegliere **nuovo > funzione App** in hello portale di Azure. Durante la creazione è possibile usare un piano di hosting esistente o crearne uno nuovo. È anche possibile optare per l'hosting dinamico. Ulteriori informazioni sulla funzione Opzioni di hosting sono reperibile in [come tooscale Azure funzioni](../azure-functions/functions-scale.md).

Quando viene creato hello funzione Azure, passare tooit e scegliere un timer di funzione e C\#. quindi fare clic su **Creare questa funzione**.

![Pannello iniziale di Funzioni di Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

In hello **sviluppare** scheda, sostituire il codice di run.csx hello con hello seguente:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Le variabili di hello tooreplace che all'hello precedente account di archiviazione tooyour toopoint codice in cui vengono scritti i log di insieme di credenziali chiave di hello, creato in precedenza, il bus di servizio hello e hello registri del percorso specifico toohello insieme di credenziali chiave di archiviazione.
>
>

funzione Hello preleva hello ultimo file di log dall'account di archiviazione hello in cui vengono scritti i log dell'insieme di credenziali chiave di hello, acrobazie hello gli eventi più recenti da tale file, e li inserisce tooa della coda del Bus di servizio. Un singolo file potrebbero essere più eventi, è necessario creare un file sync.txt funzione hello prende in considerazione anche toodetermine hello timestamp dell'hello ultimo evento che è stato prelevato. In questo modo si garantisce che non push hello stesso evento più volte. Questo file sync.txt contiene un timestamp per l'evento è stato rilevato ultimo hello. i registri, quando caricati, Hello hanno toobe ordinati in base a hello timestamp tooensure vengono ordinati correttamente.

Per questa funzione è fare riferimento a un paio di librerie aggiuntive che non sono disponibili predefinito hello nelle funzioni di Azure. tooinclude, abbiamo bisogno di funzioni di Azure toopull loro tramite NuGet. Scegliere hello **Visualizza file** opzione.

![Opzione Visualizza file](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Aggiungere poi un file denominato project.json con il contenuto seguente:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Al momento **salvare**, le funzioni di Azure verranno scaricati i file binari hello necessario.

Passare toohello **integrazione** scheda e assegnare il parametro di timer hello toouse un nome significativo all'interno di funzione hello. In hello codice precedente, è previsto che hello timer toobe chiamato *myTimer*. Specificare un [espressione CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) nel modo seguente: 0 \* \* \* \* \* di timer hello che causerà toorun funzione hello una volta al minuto.

Hello nella stessa **integrazione** scheda, aggiungere un input di tipo hello **archiviazione Blob di Azure**. Questo punterà toohello sync.txt file che contiene il timestamp di hello dell'ultimo evento hello esaminato dalla funzione hello. Questo sarà disponibile nell'ambito di funzione hello in base al nome di parametro hello. Nel codice precedente di hello, hello input di archiviazione Blob di Azure prevede hello parametro nome toobe *inputBlob*. Scegliere l'account di archiviazione hello in cui risiederà file sync.txt hello (potrebbe essere hello stesso o in un altro account di archiviazione). Nel campo percorso hello, specificare il percorso di hello in cui si trova il file hello in formato hello {container-name}/path/to/sync.txt.

Aggiungere un output di tipo hello *archiviazione Blob di Azure* output. Questo punterà toohello sync.txt file definito nell'input hello. Viene utilizzato da hello funzione toowrite hello timestamp dell'ultimo evento hello esaminato. il codice precedente Hello prevede toobe questo parametro chiamato *outputBlob*.

A questo punto, la funzione hello è pronta. Verificare che tooswitch indietro toohello **sviluppare** scheda e salvare il codice hello. Esaminare la finestra di output di hello per gli errori di compilazione e correggerle di conseguenza. Se il codice hello viene compilato, codice hello deve ora controllare i registri di insieme di credenziali chiave hello ogni minuto e inserendo nuovi eventi in hello definita coda del Bus di servizio. Dovrebbe essere informazioni di registrazione scrivono finestra log toohello ogni volta che viene attivata la funzione hello.

### <a name="azure-logic-app"></a>App per la logica di Azure
Successivamente è necessario creare un'app di Azure logica che preleva eventi hello funzione hello è push toohello della coda del Bus di servizio, analizza il contenuto di hello e invia un messaggio di posta elettronica in base a una condizione viene cercata la corrispondenza.

[Creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md) passando troppo**nuovo > App per la logica**.

Una volta creato, hello logica app passare tooit e scegliere **modifica**. Nell'editor di hello logica app scegliere **coda di Service Bus** e immettere tooconnect di credenziali del Bus di servizio è toohello coda.

![Bus di servizio dell'app per la logica di Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Scegliere quindi **Aggiungi una condizione**. Nella condizione di hello, passare toohello editor avanzato e immettere hello nel codice seguente, sostituendo APP_ID con hello APP_ID effettivo dell'app web:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Questa espressione restituisce essenzialmente **false** se hello *appid* da hello evento in entrata (ovvero il corpo di hello del messaggio hello del Bus di servizio) è non hello *appid* di hello app.

Creare ora un'azione in **Se no, non fare nulla** .

![Scelta dell'azione per l'app per la logica di Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Per l'azione di hello, scegliere **Office 365 - invio di email**. Compilare hello campi toocreate toosend un messaggio di posta elettronica quando hello definito condizione restituisce **false**. Se non si dispone di Office 365, da prendere in considerazione alternative tooachieve hello stessi risultati.

A questo punto, si dispone di una pipeline tooend fine che cerca i log di controllo nuovo insieme di credenziali chiave di una volta al minuto. Inserisce nuovi registri trova tooa coda del bus di servizio. app per la logica Hello viene attivata quando un nuovo messaggio inserita nella coda di hello. Se hello *appid* all'interno di hello evento non corrisponde all'ID di app hello di hello applicazione chiamante, invia un messaggio di posta elettronica.
