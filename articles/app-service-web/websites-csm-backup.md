---
title: aaaUse REST tooback backup e ripristino di applicazioni di servizio App
description: Informazioni su come toouse API REST chiama tooback e ripristino di un'app in Azure App Service
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Utilizzare tooback REST e ripristino di applicazioni di servizio App
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [API REST](websites-csm-backup.md)
> 
> 

[app del servizio App](https://azure.microsoft.com/services/app-service/web/) come BLOB nell'archiviazione di Azure. backup di Hello può contenere anche i database dell'applicazione hello. Se l'applicazione hello viene mai accidentalmente eliminato o se hello app esigenze toobe ripristinata la versione precedente di tooa, può essere ripristinato da un backup precedente. I backup possono essere eseguito in qualsiasi momento su richiesta o pianificati a intervalli appropriati.

Questo articolo spiega come toobackup e ripristino di un'app con l'API REST richieste. Se desideri toocreate e gestire i backup di app graficamente tramite hello portale di Azure, vedere [eseguire il backup di un'app web nel servizio App di Azure](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Introduzione
le richieste di toosend REST, è necessario tooknow dell'app **nome**, **gruppo di risorse**, e **id sottoscrizione**. Queste informazioni sono reperibile facendo l'app in hello **servizio App** blade di hello [portale di Azure](https://portal.azure.com). Per esempi di hello in questo articolo, è fase di configurazione del sito Web hello **backuprestoreapiexamples.azurewebsites.net**. Viene archiviato nel gruppo di risorse predefinito-Web-WestUS hello ed è in esecuzione in una sottoscrizione con ID 00001111-2222-3333-4444-555566667777 hello.

![Informazioni sul sito Web di esempio][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>API REST per backup e ripristino
Ora illustra alcuni esempi di come toouse hello toobackup API REST e il ripristino di un'app. Ogni esempio include un URL e il corpo della richiesta HTTP. URL di esempio Hello contiene segnaposto incapsulati tra parentesi graffe, ad esempio {id sottoscrizione}. Sostituire i segnaposto hello con informazioni corrispondenti di hello per l'app. Per riferimento, ecco una spiegazione di ogni segnaposto visualizzato negli URL di esempio hello.

* id sottoscrizione: ID di contenitore hello app di hello sottoscrizione di Azure
* Resource-group-name: nome della risorsa hello gruppo contenitore app hello
* Name: nome dell'applicazione hello
* backup-id: ID di backup di app hello

Per una documentazione completa di hello di hello API, inclusi i diversi parametri facoltativi che possono essere inclusi nella richiesta HTTP hello, vedere hello [Esplora inventario risorse di Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Eseguire il backup di un'app su richiesta
tooback di un'app immediatamente, inviare un **POST** richiesta troppo**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backup /**.

Ecco l'aspetto hello URL tramite il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Fornire un oggetto JSON nel corpo di hello di toospecify la richiesta hello backup quali toostore toouse account di archiviazione. oggetto JSON Hello deve avere una proprietà denominata **storageAccountUrl**, che contiene un [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) concessione dell'accesso in scrittura toohello di archiviazione di Azure contenitore di blob di backup hello. Se si desidera tooback backup dei database, è necessario fornire anche un elenco contenente i nomi di hello, tipi e le stringhe di connessione di hello database toobe sottoposti a backup.

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

Un backup dell'applicazione hello inizia immediatamente quando viene ricevuta la richiesta di hello. processo di backup Hello potrebbe richiedere un toocomplete molto tempo. Hello risposta HTTP contiene un ID che è possibile utilizzare un'altra richiesta toosee hello dello stato backup hello. Di seguito è riportato un esempio di corpo hello di richiesta tooour di risposta HTTP hello backup.

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> I messaggi di errore sono reperibile nella proprietà log hello di hello risposta HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Pianificare backup automatici
In toobacking aggiunta di un'app su richiesta, è anche possibile pianificare un backup toohappen automaticamente.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Configurare una nuova pianificazione di backup automatico
tooset di una pianificazione di backup, invia un **inserire** richiesta troppo**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / backup**.

Ecco l'aspetto hello URL per il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

corpo della richiesta Hello deve disporre di un oggetto JSON che specifica la configurazione del backup hello. Di seguito è riportato un esempio con tutti i parametri necessario hello.

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

In questo esempio Configura hello app toobe backup automatico ogni sette giorni. Hello parametri **frequencyInterval** e **frequencyUnit** determinano la frequenza con cui hello backup eseguito. I valori validi per **frequencyUnit** sono **hour** e **day**. Ad esempio, tooback backup ogni 12 ore, un'app impostare frequencyInterval too12 e frequencyUnit toohour.

I backup precedenti vengono automaticamente rimossi dall'account di archiviazione hello. È possibile controllare hello risale backup possono essere dall'impostazione hello **retentionPeriodInDays** parametro. Se si desidera tooalways avere almeno un backup salvato, indipendentemente dalla modalità precedente, viene **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Ottenere la pianificazione di backup automatici di hello
della tooget un'app configurazione di backup, invia un **POST** toohello URL della richiesta **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siti / {name} / config/backup/elenco**.

l'URL per il sito di esempio Hello è **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Ottenere lo stato di hello di un backup
A seconda delle dimensioni app hello è una copia di backup potrebbe richiedere qualche minuto toocomplete. I backup possono anche non riuscire, raggiungere il timeout o riuscire parzialmente. stato di hello toosee dei backup di tutti di un'app, inviare un **ottenere** toohello URL della richiesta **https://management.azure.com/subscriptions/ {id sottoscrizione} / ResourceGroups / {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.

stato hello toosee di un backup specifico, inviare un URL di toohello richiesta GET **https://management.azure.com/subscriptions/ {{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ backup-id}**.

Ecco l'aspetto hello URL per il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

corpo della risposta Hello contiene un esempio di toothis simile oggetto JSON.

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

lo stato di Hello di un backup è un tipo enumerato. Ecco tutti gli stati possibili.

* 0 – InProgress: backup hello è stato avviato ma non è ancora stata completata.
* 1-non riuscito: backup hello non riuscito.
* 2 – completata: backup hello completato.
* 3 – TimedOut: backup hello non è stata completata nel tempo ed è stato annullato.
* 4-creato: richiesta di backup hello è in coda ma non è stato avviato.
* 5-ignorato: backup hello non è stata eseguita a causa di pianificazione tooa attivazione di un numero eccessivo di backup.
* 6-completato parzialmente: backup hello completata, ma alcuni file non eseguiti perché non è possibile leggere. Ciò si verifica in genere perché è stato inserito un blocco esclusivo sui file hello.
* 7-DeleteInProgress: hello backup è stato richiesto toobe eliminato, ma non è ancora stato eliminato.
* 8-eliminazione non riuscita: non è stato possibile eliminare i backup di hello. Questa situazione può verificarsi perché hello URL SAS backup hello toocreate usato è scaduto.
* 9-eliminati: hello backup è stato eliminato correttamente.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Ripristinare un'app da un backup
Se l'app è stata eliminata o se si desidera toorevert la versione precedente di app tooa, è possibile ripristinare l'applicazione hello da un backup. tooinvoke un ripristino, inviare un **POST** toohello URL della richiesta **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backup / {backup-id} / ripristino**.

Ecco l'aspetto hello URL per il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

Nel corpo della richiesta hello, inviare un oggetto JSON che contiene le proprietà di hello per operazione di ripristino hello. Di seguito è riportato un esempio che contiene tutte le proprietà richieste:

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a>Ripristinare tooa nuova app
In alcuni casi potrebbe essere toocreate una nuova app quando si ripristina un backup, anziché sovrascrivere un'app già esistente. toodo, questa modifica richiesta URL toopoint toohello nuova app hello toocreate desiderato e modificare hello **sovrascrivere** proprietà hello JSON troppo**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Eliminare un backup dell'app
Se si desidera toodelete una copia di backup, invia un **eliminare** toohello URL della richiesta **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siti / {name} {backup-id} /backups/**.

Ecco l'aspetto hello URL per il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Gestire L'URL di firma di accesso condiviso di un backup
Servizio App di Azure tenterà toodelete il backup nell'archiviazione di Azure usando l'URL di firma di accesso condiviso fornito al momento della creazione hello backup hello. Se l'URL di firma di accesso condiviso non è più valido, backup hello non possono essere eliminati tramite hello API REST. Tuttavia, è possibile aggiornare hello URL SAS associata a un backup mediante l'invio di un **POST** toohello URL della richiesta **https://management.azure.com/subscriptions/ {id sottoscrizione} / ResourceGroups / {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Ecco l'aspetto hello URL per il sito Web di esempio. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

Nel corpo della richiesta hello, inviare un oggetto JSON contenente hello nuovo URL di firma di accesso condiviso. Di seguito è fornito un esempio.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Per motivi di sicurezza hello che URL SAS associata a un backup non viene restituito quando l'invio di una richiesta GET per un determinato backup. Se si desidera hello tooview URL SAS associata a un backup, inviare un toohello richiesta POST stesso URL precedente. Includere un oggetto JSON vuoto nel corpo della richiesta hello. risposta Hello hello server contiene le informazioni di backup, inclusi il relativo URL di firma di accesso condiviso.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
