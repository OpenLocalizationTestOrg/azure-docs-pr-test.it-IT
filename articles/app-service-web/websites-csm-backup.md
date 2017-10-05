---
title: Usare REST per eseguire il backup e il ripristino di app del servizio App
description: Informazioni su come usare chiamate API RESTful per eseguire il backup e il ripristino di un'app in Servizio app di Azure
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
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="12389-103">Usare REST per eseguire il backup e il ripristino di app del servizio App</span><span class="sxs-lookup"><span data-stu-id="12389-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12389-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12389-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="12389-105">API REST</span><span class="sxs-lookup"><span data-stu-id="12389-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="12389-106">[app del servizio App](https://azure.microsoft.com/services/app-service/web/) come BLOB nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="12389-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="12389-107">Il backup può contenere anche i database delle app.</span><span class="sxs-lookup"><span data-stu-id="12389-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="12389-108">Se si elimina l'app accidentalmente o se è necessario ripristinarne una versione precedente, è possibile farlo da un backup precedente.</span><span class="sxs-lookup"><span data-stu-id="12389-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="12389-109">I backup possono essere eseguito in qualsiasi momento su richiesta o pianificati a intervalli appropriati.</span><span class="sxs-lookup"><span data-stu-id="12389-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="12389-110">Questo articolo illustra le procedure di backup e ripristino di un'app con le richieste API RESTful.</span><span class="sxs-lookup"><span data-stu-id="12389-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="12389-111">Se si vogliono creare e gestire i backup di app graficamente tramite il portale di Azure, vedere [Eseguire il backup di un'app Web nel servizio app di Azure](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="12389-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="12389-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="12389-112">Getting Started</span></span>
<span data-ttu-id="12389-113">Per inviare richieste REST, è necessario conoscere **nome**, **gruppo di risorse** e **ID sottoscrizione** dell'app. Per trovare queste informazioni, fare clic sull'app nel pannello **Servizio app** del [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12389-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="12389-114">Per gli esempi in questo articolo, verrà configurato il sito Web **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="12389-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="12389-115">È archiviato nel gruppo di risorse Default-Web-WestUS ed è in esecuzione in una sottoscrizione con l'ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="12389-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informazioni sul sito Web di esempio][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="12389-117">API REST per backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="12389-117">Backup and restore REST API</span></span>
<span data-ttu-id="12389-118">Verranno ora esaminati alcuni esempi relativi all'uso dell'API REST per il backup e il ripristino di un'app.</span><span class="sxs-lookup"><span data-stu-id="12389-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="12389-119">Ogni esempio include un URL e il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="12389-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="12389-120">L'URL di esempio contiene segnaposto racchiusi tra parentesi graffe, ad esempio {subscription-id}.</span><span class="sxs-lookup"><span data-stu-id="12389-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="12389-121">Sostituire i segnaposto con le informazioni corrispondenti per la propria app.</span><span class="sxs-lookup"><span data-stu-id="12389-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="12389-122">Come riferimento, ecco una descrizione di ogni segnaposto visualizzato negli URL di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="12389-123">subscription-id: ID della sottoscrizione di Azure che include l'app</span><span class="sxs-lookup"><span data-stu-id="12389-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="12389-124">resource-group-name: nome del gruppo di risorse che include l'app</span><span class="sxs-lookup"><span data-stu-id="12389-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="12389-125">name: nome dell'app</span><span class="sxs-lookup"><span data-stu-id="12389-125">name – Name of the app</span></span>
* <span data-ttu-id="12389-126">backup-id: ID del backup dell'app</span><span class="sxs-lookup"><span data-stu-id="12389-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="12389-127">Per la documentazione completa dell'API, inclusi i diversi parametri opzionali che possono essere inclusi nella richiesta HTTP, vedere [Esplora risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="12389-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="12389-128">Eseguire il backup di un'app su richiesta</span><span class="sxs-lookup"><span data-stu-id="12389-128">Backup an app on demand</span></span>
<span data-ttu-id="12389-129">Per eseguire immediatamente il backup di un'app, inviare una richiesta **POST** a **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span><span class="sxs-lookup"><span data-stu-id="12389-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="12389-130">Ecco l'aspetto dell'URL se si usa il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="12389-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="12389-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="12389-132">È necessario fornire un oggetto JSON nel corpo della richiesta per specificare l'account di archiviazione da usare per archiviare il backup.</span><span class="sxs-lookup"><span data-stu-id="12389-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="12389-133">L'oggetto JSON deve avere una proprietà denominata **storageAccountUrl**, che contiene un [URL di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) che concede dell'accesso in scrittura al contenitore di archiviazione di Azure che contiene il BLOB di backup.</span><span class="sxs-lookup"><span data-stu-id="12389-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="12389-134">Se si vuole eseguire il backup dei database, è necessario fornire anche un elenco contenente i nomi, tipi e le stringhe di connessione dei database di cui eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="12389-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

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

<span data-ttu-id="12389-135">Il backup dell'app inizia immediatamente alla ricezione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="12389-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="12389-136">Il completamento del processo di backup può richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="12389-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="12389-137">La risposta HTTP contiene un ID che è possibile usare in un'altra richiesta per visualizzare lo stato del backup.</span><span class="sxs-lookup"><span data-stu-id="12389-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="12389-138">Ecco un esempio del corpo della risposta HTTP alla richiesta di backup.</span><span class="sxs-lookup"><span data-stu-id="12389-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

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
> <span data-ttu-id="12389-139">I messaggi di errore si trovano nella proprietà log della risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="12389-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="12389-140">Pianificare backup automatici</span><span class="sxs-lookup"><span data-stu-id="12389-140">Schedule automatic backups</span></span>
<span data-ttu-id="12389-141">Oltre al backup di un'app su richiesta, è anche possibile pianificare l'esecuzione automatica di un backup.</span><span class="sxs-lookup"><span data-stu-id="12389-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="12389-142">Configurare una nuova pianificazione di backup automatico</span><span class="sxs-lookup"><span data-stu-id="12389-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="12389-143">Per pianificare un backup, inviare una richiesta **PUT** a **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span><span class="sxs-lookup"><span data-stu-id="12389-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="12389-144">Ecco l'aspetto dell'URL per il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="12389-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="12389-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="12389-146">Il corpo della richiesta deve includere un oggetto JSON che specifica la configurazione di backup.</span><span class="sxs-lookup"><span data-stu-id="12389-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="12389-147">Ecco un esempio con tutti i parametri necessari.</span><span class="sxs-lookup"><span data-stu-id="12389-147">Here is an example with all the required parameters.</span></span>

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
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="12389-148">Questo esempio configura l'app per l'esecuzione automatica del backup ogni sette giorni.</span><span class="sxs-lookup"><span data-stu-id="12389-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="12389-149">I parametri **frequencyInterval** e **frequencyUnit** determinano insieme la frequenza con cui verranno eseguiti i backup.</span><span class="sxs-lookup"><span data-stu-id="12389-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="12389-150">I valori validi per **frequencyUnit** sono **hour** e **day**.</span><span class="sxs-lookup"><span data-stu-id="12389-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="12389-151">Ad esempio, per eseguire il backup di un'app per ogni 12 ore, impostare frequencyInterval su 12 e frequencyUnit su hour.</span><span class="sxs-lookup"><span data-stu-id="12389-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="12389-152">I backup precedenti saranno rimossi automaticamente dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="12389-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="12389-153">È possibile controllare la durata dei backup impostando il parametro **retentionPeriodInDays** .</span><span class="sxs-lookup"><span data-stu-id="12389-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="12389-154">Se si vuole avere sempre almeno un backup salvato, indipendentemente dalla durata definita, impostare **keepAtLeastOneBackup** su true.</span><span class="sxs-lookup"><span data-stu-id="12389-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="12389-155">Ottenere una pianificazione di backup automatico</span><span class="sxs-lookup"><span data-stu-id="12389-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="12389-156">Per ottenere la configurazione del backup di un'app, inviare una richiesta **POST** all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="12389-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="12389-157">L'URL per il sito di esempio è **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="12389-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="12389-158">Ottenere lo stato di un backup</span><span class="sxs-lookup"><span data-stu-id="12389-158">Get the status of a backup</span></span>
<span data-ttu-id="12389-159">A seconda delle dimensioni dell'app, il completamento di un backup può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="12389-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="12389-160">I backup possono anche non riuscire, raggiungere il timeout o riuscire parzialmente.</span><span class="sxs-lookup"><span data-stu-id="12389-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="12389-161">Per visualizzare lo stato di tutti i backup di un'app, inviare una richiesta **GET** all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="12389-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="12389-162">Per visualizzare lo stato di un backup specifico, inviare una richiesta GET all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="12389-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="12389-163">Ecco l'aspetto dell'URL per il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="12389-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="12389-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="12389-165">Il corpo della risposta contiene un oggetto JSON simile a questo esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-165">The response body contains a JSON object similar to this example.</span></span>

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

<span data-ttu-id="12389-166">Lo stato di un backup è un tipo enumerato.</span><span class="sxs-lookup"><span data-stu-id="12389-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="12389-167">Ecco tutti gli stati possibili.</span><span class="sxs-lookup"><span data-stu-id="12389-167">Here is every possible state.</span></span>

* <span data-ttu-id="12389-168">0 – InProgress: il backup è stato avviato ma non è ancora stato completato.</span><span class="sxs-lookup"><span data-stu-id="12389-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="12389-169">1 – Failed: il backup non riuscito.</span><span class="sxs-lookup"><span data-stu-id="12389-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="12389-170">2 – Succeeded: il backup è stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="12389-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="12389-171">3 – TimedOut: il backup non è stato completato entro il tempo previsto ed è stato annullato.</span><span class="sxs-lookup"><span data-stu-id="12389-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="12389-172">4 – Created: la richiesta di backup è in coda, ma non è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="12389-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="12389-173">5 – Skipped: il backup non ha potuto continuare, perché una pianificazione ha attivato troppi backup.</span><span class="sxs-lookup"><span data-stu-id="12389-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="12389-174">6 – PartiallySucceeded: il backup è riuscito, ma alcuni file non sono stati inclusi nel backup perché non hanno potuto essere letti.</span><span class="sxs-lookup"><span data-stu-id="12389-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="12389-175">Ciò accade di solito perché è stato attivato un blocco esclusivo sui file.</span><span class="sxs-lookup"><span data-stu-id="12389-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="12389-176">7 – DeleteInProgress: è stata richiesta l'eliminazione del backup, ma l'operazione non è ancora stata completata.</span><span class="sxs-lookup"><span data-stu-id="12389-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="12389-177">8 – DeleteFailed: non è stato possibile eliminare il backup.</span><span class="sxs-lookup"><span data-stu-id="12389-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="12389-178">Ciò può verificarsi perché l'URL di firma di accesso condiviso usata per creare il backup è scaduta.</span><span class="sxs-lookup"><span data-stu-id="12389-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="12389-179">9 – Deleted: il backup è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="12389-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="12389-180">Ripristinare un'app da un backup</span><span class="sxs-lookup"><span data-stu-id="12389-180">Restore an app from a backup</span></span>
<span data-ttu-id="12389-181">Se l'app è stata eliminata o se si vuole tornare a una versione precedente dell'app, è possibile ripristinarla da un backup.</span><span class="sxs-lookup"><span data-stu-id="12389-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="12389-182">Per richiamare un ripristino, inviare una richiesta **POST** all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span><span class="sxs-lookup"><span data-stu-id="12389-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="12389-183">Ecco l'aspetto dell'URL per il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="12389-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="12389-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="12389-185">Nel corpo della richiesta inviare un oggetto JSON che contiene le proprietà per l'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="12389-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="12389-186">Di seguito è riportato un esempio che contiene tutte le proprietà richieste:</span><span class="sxs-lookup"><span data-stu-id="12389-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="12389-187">Ripristinare una nuova app</span><span class="sxs-lookup"><span data-stu-id="12389-187">Restore to a new app</span></span>
<span data-ttu-id="12389-188">Quando si ripristina un backup, in alcuni casi è consigliabile creare una nuova app, invece di sovrascriverne una esistente.</span><span class="sxs-lookup"><span data-stu-id="12389-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="12389-189">A tale scopo, modificare l'URL della richiesta in modo che punti alla nuova app che si vuole creare e modificare la proprietà **overwrite** in JSON su **false**.</span><span class="sxs-lookup"><span data-stu-id="12389-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="12389-190">Eliminare un backup dell'app</span><span class="sxs-lookup"><span data-stu-id="12389-190">Delete an app backup</span></span>
<span data-ttu-id="12389-191">Per eliminare un backup, inviare una richiesta **DELETE** all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="12389-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="12389-192">Ecco l'aspetto dell'URL per il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="12389-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="12389-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="12389-194">Gestire L'URL di firma di accesso condiviso di un backup</span><span class="sxs-lookup"><span data-stu-id="12389-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="12389-195">Servizio app di Azure tenta di eliminare il backup dall'archiviazione di Azure usando l'URL di firma di accesso condiviso specificato al momento della creazione del backup.</span><span class="sxs-lookup"><span data-stu-id="12389-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="12389-196">Se questo URL di firma di accesso condiviso non è più valido, il backup non potrà essere eliminato tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="12389-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="12389-197">È possibile tuttavia aggiornare l'URL della firma di accesso condiviso associato a un backup inviando una richiesta **POST** all'URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="12389-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="12389-198">Ecco l'aspetto dell'URL per il sito Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="12389-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="12389-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="12389-200">Nel corpo della richiesta inviare un oggetto JSON che contiene il nuovo URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="12389-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="12389-201">Di seguito è fornito un esempio.</span><span class="sxs-lookup"><span data-stu-id="12389-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="12389-202">Per motivi di sicurezza, l'URL di firma di accesso condiviso associato a un backup non viene restituito quando si invia una richiesta GET per un backup specifico.</span><span class="sxs-lookup"><span data-stu-id="12389-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="12389-203">Se si vuole visualizzare l'URL di firma di accesso condiviso associato a un backup, inviare una richiesta POST allo stesso URL precedente</span><span class="sxs-lookup"><span data-stu-id="12389-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="12389-204">e includere semplicemente un oggetto JSON vuoto nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="12389-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="12389-205">La risposta dal server contiene tutte le informazioni del backup, incluso l'URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="12389-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
