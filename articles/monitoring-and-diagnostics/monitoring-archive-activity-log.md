---
title: "Archiviare il registro attività di Azure | Microsoft Docs"
description: "Informazioni su come archiviare il log attività di Azure per la conservazione a lungo termine in un account di archiviazione."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="ee096-103">Archiviare il log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="ee096-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="ee096-104">In questo articolo viene illustrato come è possibile usare il Portale di Azure, i cmdlet di PowerShell o l'interfaccia della riga di comando multipiattaforma per archiviare il [**registro attività di Azure**](monitoring-overview-activity-logs.md) in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="ee096-105">Questa opzione è utile per conservare il log attività per più di 90 giorni (con il controllo completo sui criteri di conservazione) per il controllo, l'analisi statica o il backup.</span><span class="sxs-lookup"><span data-stu-id="ee096-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="ee096-106">Se è necessario conservare gli eventi per non più di 90 giorni, non è necessario configurare l'archiviazione in un account di archiviazione, perché gli eventi del log attività vengono conservati nella piattaforma Azure per 90 giorni senza abilitare l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee096-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ee096-107">Prerequisites</span></span>
<span data-ttu-id="ee096-108">Prima di iniziare, è necessario [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in cui poter archiviare il log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="ee096-109">È consigliabile non usare un account di archiviazione esistente in cui sono archiviati altri dati non di monitoraggio, per poter controllare meglio l'accesso ai dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="ee096-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="ee096-110">Se tuttavia in un account di archiviazione si archiviano anche log di diagnostica e metriche, può avere senso non solo usare tale account di archiviazione per il log attività, ma anche tenere tutti i dati di monitoraggio in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="ee096-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="ee096-111">L'account di archiviazione usato deve essere un account di archiviazione per utilizzo generico, non un account di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="ee096-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="ee096-112">L'account di archiviazione non deve trovarsi nella stessa sottoscrizione della sottoscrizione che emette log, purché l'utente che configura l'impostazione abbia un accesso RBAC appropriato a entrambe le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="ee096-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="ee096-113">Profilo del log</span><span class="sxs-lookup"><span data-stu-id="ee096-113">Log Profile</span></span>
<span data-ttu-id="ee096-114">Per archiviare il log attività con uno dei metodi seguenti, impostare il **profilo del log** per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ee096-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="ee096-115">Il profilo del log definisce il tipo di eventi archiviati o trasmessi e gli output (account di archiviazione e/o hub eventi).</span><span class="sxs-lookup"><span data-stu-id="ee096-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="ee096-116">Definisce anche i criteri di conservazione (numero di giorni di conservazione) per gli eventi archiviati in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="ee096-117">Se il criterio di conservazione viene impostato su zero, gli eventi vengono archiviati a tempo indeterminato.</span><span class="sxs-lookup"><span data-stu-id="ee096-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="ee096-118">In caso contrario, si può impostare un valore qualsiasi compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="ee096-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="ee096-119">I criteri di conservazione vengono applicati su base giornaliera. Al termine della giornata, i log relativi a tale giornata non rientrano quindi più nei criteri di conservazione e verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="ee096-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="ee096-120">Se, ad esempio, è presente un criterio di conservazione di un giorno, all'inizio della giornata attuale vengono eliminati i log relativi alla giornata precedente a ieri.</span><span class="sxs-lookup"><span data-stu-id="ee096-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="ee096-121">[Fare clic qui per altre informazioni sui profili dei log](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="ee096-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="ee096-122">Archiviare il log attività con il portale</span><span class="sxs-lookup"><span data-stu-id="ee096-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="ee096-123">Nel portale fare clic sul collegamento **Log attività** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ee096-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="ee096-124">Se il collegamento Log attività non è visualizzato, fare prima clic sul collegamento **Altri servizi** .</span><span class="sxs-lookup"><span data-stu-id="ee096-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Passare al pannello Log attività](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="ee096-126">Nella parte superiore del pannello fare clic su **Esporta**.</span><span class="sxs-lookup"><span data-stu-id="ee096-126">At the top of the blade, click **Export**.</span></span>
   
    ![Fare clic sul pulsante Esporta](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="ee096-128">Nel pannello visualizzato selezionare la casella **Esporta in un account di archiviazione** e selezionare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![Impostare un account di archiviazione](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="ee096-130">Usando il dispositivo di scorrimento o la casella di testo, definire un numero di giorni per cui gli eventi del log attività devono essere conservati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="ee096-131">Se si preferisce che i dati rimangano nell'account di archiviazione a tempo indeterminato, impostare questo numero su zero.</span><span class="sxs-lookup"><span data-stu-id="ee096-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="ee096-132">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="ee096-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="ee096-133">Archiviare il log attività con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee096-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="ee096-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee096-134">Property</span></span> | <span data-ttu-id="ee096-135">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ee096-135">Required</span></span> | <span data-ttu-id="ee096-136">Description</span><span class="sxs-lookup"><span data-stu-id="ee096-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee096-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="ee096-137">StorageAccountId</span></span> |<span data-ttu-id="ee096-138">No</span><span class="sxs-lookup"><span data-stu-id="ee096-138">No</span></span> |<span data-ttu-id="ee096-139">ID risorsa dell'account di archiviazione in cui salvare i log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="ee096-140">Località</span><span class="sxs-lookup"><span data-stu-id="ee096-140">Locations</span></span> |<span data-ttu-id="ee096-141">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-141">Yes</span></span> |<span data-ttu-id="ee096-142">Elenco delimitato da virgole di aree per cui raccogliere eventi del log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="ee096-143">È possibile visualizzare un elenco di tutte le aree [visitando questa pagina](https://azure.microsoft.com/en-us/regions) o usando [l'API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee096-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="ee096-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="ee096-144">RetentionInDays</span></span> |<span data-ttu-id="ee096-145">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-145">Yes</span></span> |<span data-ttu-id="ee096-146">Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="ee096-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="ee096-147">Se il valore è zero, i log vengono mantenuti per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="ee096-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="ee096-148">Categorie</span><span class="sxs-lookup"><span data-stu-id="ee096-148">Categories</span></span> |<span data-ttu-id="ee096-149">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-149">Yes</span></span> |<span data-ttu-id="ee096-150">Elenco delimitato da virgole di categorie di eventi che devono essere raccolti.</span><span class="sxs-lookup"><span data-stu-id="ee096-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="ee096-151">I valori possibili sono Write, Delete e Action.</span><span class="sxs-lookup"><span data-stu-id="ee096-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="ee096-152">Archiviare il log attività con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="ee096-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="ee096-153">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee096-153">Property</span></span> | <span data-ttu-id="ee096-154">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ee096-154">Required</span></span> | <span data-ttu-id="ee096-155">Description</span><span class="sxs-lookup"><span data-stu-id="ee096-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee096-156">name</span><span class="sxs-lookup"><span data-stu-id="ee096-156">name</span></span> |<span data-ttu-id="ee096-157">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-157">Yes</span></span> |<span data-ttu-id="ee096-158">Nome del profilo di log.</span><span class="sxs-lookup"><span data-stu-id="ee096-158">Name of your log profile.</span></span> |
| <span data-ttu-id="ee096-159">storageId</span><span class="sxs-lookup"><span data-stu-id="ee096-159">storageId</span></span> |<span data-ttu-id="ee096-160">No</span><span class="sxs-lookup"><span data-stu-id="ee096-160">No</span></span> |<span data-ttu-id="ee096-161">ID risorsa dell'account di archiviazione in cui salvare i log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="ee096-162">Località</span><span class="sxs-lookup"><span data-stu-id="ee096-162">locations</span></span> |<span data-ttu-id="ee096-163">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-163">Yes</span></span> |<span data-ttu-id="ee096-164">Elenco delimitato da virgole di aree per cui raccogliere eventi del log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="ee096-165">È possibile visualizzare un elenco di tutte le aree [visitando questa pagina](https://azure.microsoft.com/en-us/regions) o usando [l'API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee096-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="ee096-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="ee096-166">retentionInDays</span></span> |<span data-ttu-id="ee096-167">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-167">Yes</span></span> |<span data-ttu-id="ee096-168">Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="ee096-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="ee096-169">Se il valore è zero, i log vengono archiviati per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="ee096-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="ee096-170">Categorie</span><span class="sxs-lookup"><span data-stu-id="ee096-170">categories</span></span> |<span data-ttu-id="ee096-171">Sì</span><span class="sxs-lookup"><span data-stu-id="ee096-171">Yes</span></span> |<span data-ttu-id="ee096-172">Elenco delimitato da virgole di categorie di eventi che devono essere raccolti.</span><span class="sxs-lookup"><span data-stu-id="ee096-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="ee096-173">I valori possibili sono Write, Delete e Action.</span><span class="sxs-lookup"><span data-stu-id="ee096-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="ee096-174">Schema di archiviazione del log attività</span><span class="sxs-lookup"><span data-stu-id="ee096-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="ee096-175">Una volta configurata l'archiviazione, verrà creato un contenitore di archiviazione nell'account di archiviazione non appena si verificherà un evento del log attività.</span><span class="sxs-lookup"><span data-stu-id="ee096-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="ee096-176">I BLOB nel contenitore seguono lo stesso formato nel log attività e nei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ee096-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="ee096-177">La struttura di questi BLOB è:</span><span class="sxs-lookup"><span data-stu-id="ee096-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="ee096-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID sottoscrizione}/y={anno a quattro cifre}/m={mese a due cifre}/d={giorno a due cifre}/h={ora a due cifre in formato 24 ore}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="ee096-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="ee096-179">Ad esempio, un nome BLOB potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="ee096-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="ee096-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="ee096-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="ee096-181">Ogni BLOB PT1H.json contiene un BLOB JSON di eventi che si sono verificati nell'ora specificata nell'URL BLOB (ad esempio, h=12).</span><span class="sxs-lookup"><span data-stu-id="ee096-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="ee096-182">Durante l'ora attuale, gli eventi vengono aggiunti al file PT1H.json man mano che si verificano.</span><span class="sxs-lookup"><span data-stu-id="ee096-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="ee096-183">Il valore dei minuti (m=00) è sempre 00, perché gli eventi del log attività vengono sempre suddivisi in singoli BLOB per ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ee096-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="ee096-184">Nel file PT1H.json ogni evento viene archiviato nella matrice "records", con questo formato:</span><span class="sxs-lookup"><span data-stu-id="ee096-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="ee096-185">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="ee096-185">Element name</span></span> | <span data-ttu-id="ee096-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ee096-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee096-187">time</span><span class="sxs-lookup"><span data-stu-id="ee096-187">time</span></span> |<span data-ttu-id="ee096-188">Timestamp del momento in cui l'evento è stato generato dal servizio di Azure che ha elaborato la richiesta corrispondente all'evento.</span><span class="sxs-lookup"><span data-stu-id="ee096-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="ee096-189">ResourceId</span><span class="sxs-lookup"><span data-stu-id="ee096-189">resourceId</span></span> |<span data-ttu-id="ee096-190">ID risorsa della risorsa interessata.</span><span class="sxs-lookup"><span data-stu-id="ee096-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="ee096-191">operationName</span><span class="sxs-lookup"><span data-stu-id="ee096-191">operationName</span></span> |<span data-ttu-id="ee096-192">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ee096-192">Name of the operation.</span></span> |
| <span data-ttu-id="ee096-193">category</span><span class="sxs-lookup"><span data-stu-id="ee096-193">category</span></span> |<span data-ttu-id="ee096-194">Categoria dell'azione, ad esempio</span><span class="sxs-lookup"><span data-stu-id="ee096-194">Category of the action, eg.</span></span> <span data-ttu-id="ee096-195">scrittura o lettura.</span><span class="sxs-lookup"><span data-stu-id="ee096-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="ee096-196">resultType</span><span class="sxs-lookup"><span data-stu-id="ee096-196">resultType</span></span> |<span data-ttu-id="ee096-197">Il tipo di risultato, ad esempio</span><span class="sxs-lookup"><span data-stu-id="ee096-197">The type of the result, eg.</span></span> <span data-ttu-id="ee096-198">operazione riuscita, esito negativo, avvio</span><span class="sxs-lookup"><span data-stu-id="ee096-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="ee096-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="ee096-199">resultSignature</span></span> |<span data-ttu-id="ee096-200">Dipende dal tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="ee096-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="ee096-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="ee096-201">durationMs</span></span> |<span data-ttu-id="ee096-202">Durata dell'operazione in millisecondi</span><span class="sxs-lookup"><span data-stu-id="ee096-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="ee096-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="ee096-203">callerIpAddress</span></span> |<span data-ttu-id="ee096-204">Indirizzo IP dell'utente che ha eseguito l'operazione, attestazione UPN o attestazione SPN, a seconda della disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ee096-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="ee096-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="ee096-205">correlationId</span></span> |<span data-ttu-id="ee096-206">In genere un GUID in formato stringa.</span><span class="sxs-lookup"><span data-stu-id="ee096-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="ee096-207">Gli eventi che condividono un elemento correlationId appartengono alla stessa azione.</span><span class="sxs-lookup"><span data-stu-id="ee096-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="ee096-208">identity</span><span class="sxs-lookup"><span data-stu-id="ee096-208">identity</span></span> |<span data-ttu-id="ee096-209">BLOB JSON che descrive l'autorizzazione e le attestazioni.</span><span class="sxs-lookup"><span data-stu-id="ee096-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="ee096-210">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="ee096-210">authorization</span></span> |<span data-ttu-id="ee096-211">BLOB delle proprietà RBAC dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ee096-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="ee096-212">In genere include le proprietà "action", "role" e "scope".</span><span class="sxs-lookup"><span data-stu-id="ee096-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="ee096-213">level</span><span class="sxs-lookup"><span data-stu-id="ee096-213">level</span></span> |<span data-ttu-id="ee096-214">Livello dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ee096-214">Level of the event.</span></span> <span data-ttu-id="ee096-215">Uno dei valori seguenti: "Critical", "Error", "Warning", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="ee096-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="ee096-216">location</span><span class="sxs-lookup"><span data-stu-id="ee096-216">location</span></span> |<span data-ttu-id="ee096-217">Area in cui si trova la località (o global).</span><span class="sxs-lookup"><span data-stu-id="ee096-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="ee096-218">properties</span><span class="sxs-lookup"><span data-stu-id="ee096-218">properties</span></span> |<span data-ttu-id="ee096-219">Set di coppie `<Key, Value>` ad esempio Dictionary, che descrivono i dettagli dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ee096-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="ee096-220">Le proprietà e l'utilizzo di tali proprietà possono variare a seconda della risorsa.</span><span class="sxs-lookup"><span data-stu-id="ee096-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ee096-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee096-221">Next steps</span></span>
* [<span data-ttu-id="ee096-222">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="ee096-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="ee096-223">Stream the Activity Log to Event Hubs (Trasmettere il log attività a Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="ee096-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="ee096-224">Read more about the Activity Log (Altre informazioni sul log attività)</span><span class="sxs-lookup"><span data-stu-id="ee096-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

