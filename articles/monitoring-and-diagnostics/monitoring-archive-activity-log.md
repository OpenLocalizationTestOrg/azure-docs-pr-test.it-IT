---
title: "hello aaaArchive Log attività di Azure | Documenti Microsoft"
description: "Informazioni su come tooarchive accedere l'attività di Azure per la conservazione a lungo termine in un account di archiviazione."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="73f83-103">Archiviare hello Log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="73f83-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="73f83-104">In questo articolo, ecco come è possibile utilizzare hello portale di Azure, PowerShell Cmdlets o tooarchive CLI multipiattaforma il [ **Log attività Azure** ](monitoring-overview-activity-logs.md) in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73f83-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="73f83-105">Questa opzione è utile se si desidera tooretain il Log attività di più di 90 giorni (con controllo completo sui criteri di conservazione hello) per controllare, analisi statica, o eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="73f83-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="73f83-106">Se è necessario solo tooretain gli eventi per 90 giorni o meno è tooset tooa dell'archivio account di archiviazione, non è necessario poiché gli eventi del registro attività vengono conservati per 90 giorni senza abilitare archiviazione nella piattaforma Azure hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73f83-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73f83-107">Prerequisites</span></span>
<span data-ttu-id="73f83-108">Prima di iniziare, è necessario troppo[creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich è possibile archiviare i Log di attività.</span><span class="sxs-lookup"><span data-stu-id="73f83-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="73f83-109">Si consiglia di non utilizzare un account di archiviazione esistente che dispone di altri, non di monitoraggio di dati in essa archiviati in modo che è possibile controllare meglio toomonitoring accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="73f83-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="73f83-110">Tuttavia, se si desidera archiviare anche i log di diagnostica e account di archiviazione tooa metriche, può avere senso toouse tale account di archiviazione per l'attività di Log anche tookeep tutti i dati di monitoraggio in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="73f83-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="73f83-111">account di archiviazione Hello utilizzato deve essere un account di archiviazione generico, non un account di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="73f83-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="73f83-112">account di archiviazione Hello non presenti toobe hello stessa sottoscrizione come sottoscrizione hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.</span><span class="sxs-lookup"><span data-stu-id="73f83-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="73f83-113">Profilo del log</span><span class="sxs-lookup"><span data-stu-id="73f83-113">Log Profile</span></span>
<span data-ttu-id="73f83-114">hello tooarchive Log attività utilizzando uno dei metodi di hello indicati di seguito, si imposta hello **profilo Log** per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="73f83-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="73f83-115">definisce il tipo di hello di eventi che vengono archiviate o trasmessi Hello profilo Log e gli output di hello: hub account e/o eventi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73f83-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="73f83-116">Definisce inoltre i criteri di conservazione hello (numero di giorni tooretain) per gli eventi archiviati in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73f83-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="73f83-117">Se i criteri di conservazione hello sono impostato toozero, gli eventi vengono archiviati in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="73f83-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="73f83-118">In caso contrario, può essere impostato tooany valore compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="73f83-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="73f83-119">Criteri di conservazione vengono applicati al giorno, verranno eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="73f83-120">Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri dovrebbero essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="73f83-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="73f83-121">[Fare clic qui per altre informazioni sui profili dei log](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="73f83-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="73f83-122">Archivio hello Log attività tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="73f83-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="73f83-123">Nel portale di hello, fare clic su hello **Log attività** collegamento di navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="73f83-124">Se non viene visualizzato un collegamento per hello registro attività, fare clic su hello **più servizi** collegare prima.</span><span class="sxs-lookup"><span data-stu-id="73f83-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Passare a pannello Log tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="73f83-126">Nella parte superiore di hello del Pannello di hello, fare clic su **esportare**.</span><span class="sxs-lookup"><span data-stu-id="73f83-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Fare clic su pulsante Esporta hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="73f83-128">Nel pannello hello che viene visualizzato, selezionare casella hello per **esportare l'account di archiviazione tooa** e selezionare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73f83-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Impostare un account di archiviazione](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="73f83-130">Dispositivo di scorrimento hello o casella di testo, di definire un numero di giorni per cui gli eventi del registro attività devono essere conservati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73f83-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="73f83-131">Se si preferisce toohave che persistenti i dati nell'account di archiviazione hello per un periodo illimitato, impostare questo numero toozero.</span><span class="sxs-lookup"><span data-stu-id="73f83-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="73f83-132">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="73f83-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="73f83-133">Archiviare hello Log attività tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="73f83-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="73f83-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="73f83-134">Property</span></span> | <span data-ttu-id="73f83-135">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73f83-135">Required</span></span> | <span data-ttu-id="73f83-136">Description</span><span class="sxs-lookup"><span data-stu-id="73f83-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73f83-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="73f83-137">StorageAccountId</span></span> |<span data-ttu-id="73f83-138">No</span><span class="sxs-lookup"><span data-stu-id="73f83-138">No</span></span> |<span data-ttu-id="73f83-139">ID di risorsa dell'Account di archiviazione di hello toowhich log attività deve essere salvato.</span><span class="sxs-lookup"><span data-stu-id="73f83-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="73f83-140">Località</span><span class="sxs-lookup"><span data-stu-id="73f83-140">Locations</span></span> |<span data-ttu-id="73f83-141">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-141">Yes</span></span> |<span data-ttu-id="73f83-142">Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi.</span><span class="sxs-lookup"><span data-stu-id="73f83-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="73f83-143">È possibile visualizzare un elenco di tutte le aree [visitando la pagina](https://azure.microsoft.com/en-us/regions) o utilizzando [hello API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="73f83-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="73f83-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="73f83-144">RetentionInDays</span></span> |<span data-ttu-id="73f83-145">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-145">Yes</span></span> |<span data-ttu-id="73f83-146">Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="73f83-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="73f83-147">Un valore pari a zero vengono archiviati i log di hello illimitata (sempre).</span><span class="sxs-lookup"><span data-stu-id="73f83-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="73f83-148">Categorie</span><span class="sxs-lookup"><span data-stu-id="73f83-148">Categories</span></span> |<span data-ttu-id="73f83-149">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-149">Yes</span></span> |<span data-ttu-id="73f83-150">Elenco delimitato da virgole di categorie di eventi che devono essere raccolti.</span><span class="sxs-lookup"><span data-stu-id="73f83-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="73f83-151">I valori possibili sono Write, Delete e Action.</span><span class="sxs-lookup"><span data-stu-id="73f83-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="73f83-152">Archiviare i Log di attività tramite CLI hello</span><span class="sxs-lookup"><span data-stu-id="73f83-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="73f83-153">Proprietà</span><span class="sxs-lookup"><span data-stu-id="73f83-153">Property</span></span> | <span data-ttu-id="73f83-154">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73f83-154">Required</span></span> | <span data-ttu-id="73f83-155">Description</span><span class="sxs-lookup"><span data-stu-id="73f83-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73f83-156">name</span><span class="sxs-lookup"><span data-stu-id="73f83-156">name</span></span> |<span data-ttu-id="73f83-157">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-157">Yes</span></span> |<span data-ttu-id="73f83-158">Nome del profilo di log.</span><span class="sxs-lookup"><span data-stu-id="73f83-158">Name of your log profile.</span></span> |
| <span data-ttu-id="73f83-159">storageId</span><span class="sxs-lookup"><span data-stu-id="73f83-159">storageId</span></span> |<span data-ttu-id="73f83-160">No</span><span class="sxs-lookup"><span data-stu-id="73f83-160">No</span></span> |<span data-ttu-id="73f83-161">ID di risorsa dell'Account di archiviazione di hello toowhich log attività deve essere salvato.</span><span class="sxs-lookup"><span data-stu-id="73f83-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="73f83-162">locations</span><span class="sxs-lookup"><span data-stu-id="73f83-162">locations</span></span> |<span data-ttu-id="73f83-163">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-163">Yes</span></span> |<span data-ttu-id="73f83-164">Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi.</span><span class="sxs-lookup"><span data-stu-id="73f83-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="73f83-165">È possibile visualizzare un elenco di tutte le aree [visitando la pagina](https://azure.microsoft.com/en-us/regions) o utilizzando [hello API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="73f83-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="73f83-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="73f83-166">retentionInDays</span></span> |<span data-ttu-id="73f83-167">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-167">Yes</span></span> |<span data-ttu-id="73f83-168">Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="73f83-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="73f83-169">Un valore pari a zero verrà archiviati i log di hello in modo indefinito (sempre).</span><span class="sxs-lookup"><span data-stu-id="73f83-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="73f83-170">Categorie</span><span class="sxs-lookup"><span data-stu-id="73f83-170">categories</span></span> |<span data-ttu-id="73f83-171">Sì</span><span class="sxs-lookup"><span data-stu-id="73f83-171">Yes</span></span> |<span data-ttu-id="73f83-172">Elenco delimitato da virgole di categorie di eventi che devono essere raccolti.</span><span class="sxs-lookup"><span data-stu-id="73f83-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="73f83-173">I valori possibili sono Write, Delete e Action.</span><span class="sxs-lookup"><span data-stu-id="73f83-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="73f83-174">Schema di archiviazione di hello Log attività</span><span class="sxs-lookup"><span data-stu-id="73f83-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="73f83-175">Dopo aver impostato dell'archivio, è verrà creato un contenitore di archiviazione nell'account di archiviazione hello non appena si verifica un evento di registro attività.</span><span class="sxs-lookup"><span data-stu-id="73f83-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="73f83-176">BLOB Hello all'interno del contenitore hello seguire hello stesso formato in hello Log attività e i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="73f83-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="73f83-177">struttura Hello di tali BLOB è:</span><span class="sxs-lookup"><span data-stu-id="73f83-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="73f83-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID sottoscrizione}/y={anno a quattro cifre}/m={mese a due cifre}/d={giorno a due cifre}/h={ora a due cifre in formato 24 ore}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="73f83-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="73f83-179">Ad esempio, un nome BLOB potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="73f83-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="73f83-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="73f83-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="73f83-181">Ciascun blob PT1H.json contiene un blob JSON di eventi che si sono verificati entro ora hello specificata nell'URL blob hello (ad esempio h = 12).</span><span class="sxs-lookup"><span data-stu-id="73f83-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="73f83-182">Durante l'ora presenta hello, gli eventi sono accodati toohello PT1H.json file che si verificano.</span><span class="sxs-lookup"><span data-stu-id="73f83-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="73f83-183">valore dei minuti Hello (m = 00) è sempre 00, poiché gli eventi del registro attività sono suddivisi in singoli BLOB all'ora.</span><span class="sxs-lookup"><span data-stu-id="73f83-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="73f83-184">Nel file PT1H.json hello, ogni evento viene archiviato nella matrice di record"hello", il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="73f83-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="73f83-185">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="73f83-185">Element name</span></span> | <span data-ttu-id="73f83-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73f83-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73f83-187">time</span><span class="sxs-lookup"><span data-stu-id="73f83-187">time</span></span> |<span data-ttu-id="73f83-188">Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="73f83-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="73f83-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="73f83-189">resourceId</span></span> |<span data-ttu-id="73f83-190">ID di risorsa di hello influisce sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="73f83-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="73f83-191">operationName</span><span class="sxs-lookup"><span data-stu-id="73f83-191">operationName</span></span> |<span data-ttu-id="73f83-192">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-192">Name of hello operation.</span></span> |
| <span data-ttu-id="73f83-193">category</span><span class="sxs-lookup"><span data-stu-id="73f83-193">category</span></span> |<span data-ttu-id="73f83-194">Categoria di azione hello, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="73f83-194">Category of hello action, eg.</span></span> <span data-ttu-id="73f83-195">scrittura o lettura.</span><span class="sxs-lookup"><span data-stu-id="73f83-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="73f83-196">resultType</span><span class="sxs-lookup"><span data-stu-id="73f83-196">resultType</span></span> |<span data-ttu-id="73f83-197">Hello tipo di risultato hello, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="73f83-197">hello type of hello result, eg.</span></span> <span data-ttu-id="73f83-198">operazione riuscita, esito negativo, avvio</span><span class="sxs-lookup"><span data-stu-id="73f83-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="73f83-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="73f83-199">resultSignature</span></span> |<span data-ttu-id="73f83-200">Dipende dal tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="73f83-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="73f83-201">durationMs</span></span> |<span data-ttu-id="73f83-202">Durata dell'operazione di hello in millisecondi</span><span class="sxs-lookup"><span data-stu-id="73f83-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="73f83-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="73f83-203">callerIpAddress</span></span> |<span data-ttu-id="73f83-204">Indirizzo IP dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="73f83-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="73f83-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="73f83-205">correlationId</span></span> |<span data-ttu-id="73f83-206">In genere un GUID in formato stringa hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="73f83-207">Gli eventi che condividono un valore correlationId appartengono toohello stessa azione.</span><span class="sxs-lookup"><span data-stu-id="73f83-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="73f83-208">identity</span><span class="sxs-lookup"><span data-stu-id="73f83-208">identity</span></span> |<span data-ttu-id="73f83-209">Blob JSON che descrive le attestazioni e l'autorizzazione di hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="73f83-210">autorizzazione</span><span class="sxs-lookup"><span data-stu-id="73f83-210">authorization</span></span> |<span data-ttu-id="73f83-211">BLOB di proprietà RBAC dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="73f83-212">In genere include le proprietà di "azione", "role" e "scope" hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="73f83-213">level</span><span class="sxs-lookup"><span data-stu-id="73f83-213">level</span></span> |<span data-ttu-id="73f83-214">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-214">Level of hello event.</span></span> <span data-ttu-id="73f83-215">Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"</span><span class="sxs-lookup"><span data-stu-id="73f83-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="73f83-216">location</span><span class="sxs-lookup"><span data-stu-id="73f83-216">location</span></span> |<span data-ttu-id="73f83-217">Area nella quale percorso hello durante l'esecuzione (o globale).</span><span class="sxs-lookup"><span data-stu-id="73f83-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="73f83-218">properties</span><span class="sxs-lookup"><span data-stu-id="73f83-218">properties</span></span> |<span data-ttu-id="73f83-219">Set di `<Key, Value>` coppie (ad esempio Dictionary) che descrive hello dettagli dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="73f83-220">proprietà Hello e l'utilizzo di tali proprietà può variare a seconda delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="73f83-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="73f83-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73f83-221">Next steps</span></span>
* [<span data-ttu-id="73f83-222">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="73f83-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="73f83-223">Flusso hello Log attività tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="73f83-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="73f83-224">Per ulteriori informazioni su hello Log attività</span><span class="sxs-lookup"><span data-stu-id="73f83-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

