---
title: aaaManage Azure Data Lake Analitica con Azure PowerShell | Documenti Microsoft
description: 'Informazioni su come account Data Lake Analitica toomanage, origini dati, processi e gli elementi del catalogo. '
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="fc0c2-103">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc0c2-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="fc0c2-104">Informazioni su come account di Azure Data Lake Analitica toomanage, origini dati, processi e gli elementi del catalogo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc0c2-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fc0c2-105">Prerequisites</span></span>

<span data-ttu-id="fc0c2-106">Quando si crea un account Data Lake Analitica, è necessario tooknow:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="fc0c2-107">**ID sottoscrizione**: hello ID sottoscrizione di Azure in cui risiede l'account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="fc0c2-108">**Gruppo di risorse**: nome hello hello Azure del gruppo di risorse che contiene l'account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="fc0c2-109">**Nome dell'account data Lake Analitica**: hello account nome deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="fc0c2-110">**Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="fc0c2-111">Questi account devono essere in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="fc0c2-112">**Percorso**: percorso hello dell'account Data Lake Analitica, ad esempio "Stati Uniti orientali 2" o altre supportati percorsi.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="fc0c2-113">Le posizioni supportate possono essere visualizzate nella [pagina dei prezzi](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="fc0c2-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="fc0c2-114">frammenti di codice PowerShell Hello in questa esercitazione usare questi toostore variabili queste informazioni</span><span class="sxs-lookup"><span data-stu-id="fc0c2-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="fc0c2-115">Accesso</span><span class="sxs-lookup"><span data-stu-id="fc0c2-115">Log in</span></span>

<span data-ttu-id="fc0c2-116">Accesso con un ID di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="fc0c2-117">Accesso con un nome di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="fc0c2-118">Hello `Login-AzureRmAccount` cmdlet richiede sempre le credenziali.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="fc0c2-119">È possibile evitare che venga richiesto tramite hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="fc0c2-120">Gestione di account</span><span class="sxs-lookup"><span data-stu-id="fc0c2-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="fc0c2-121">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="fc0c2-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="fc0c2-122">Se dispone già di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="fc0c2-123">Per ogni account Data Lake Analytics deve essere configurato un account Data Lake Store che viene usato per l'archiviazione dei log.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="fc0c2-124">È possibile riusare un account esistente o creare un account.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="fc0c2-125">Quando sono disponibili un gruppo di risorse e un account Data Lake Store, creare un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="fc0c2-126">Ottenere informazioni su un account</span><span class="sxs-lookup"><span data-stu-id="fc0c2-126">Get information about an account</span></span>

<span data-ttu-id="fc0c2-127">Ottenere dettagli su un account.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="fc0c2-128">Verificare l'esistenza di hello di uno specifico account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="fc0c2-129">Restituisce i cmdlet di Hello `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="fc0c2-130">Verificare l'esistenza di hello di uno specifico account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="fc0c2-131">Restituisce i cmdlet di Hello `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="fc0c2-132">Elenco di account</span><span class="sxs-lookup"><span data-stu-id="fc0c2-132">Listing accounts</span></span>

<span data-ttu-id="fc0c2-133">Account di Analitica elenco Data Lake nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="fc0c2-134">Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="fc0c2-135">Gestione delle regole del firewall</span><span class="sxs-lookup"><span data-stu-id="fc0c2-135">Managing firewall rules</span></span>

<span data-ttu-id="fc0c2-136">Elencare le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="fc0c2-137">Aggiungere una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="fc0c2-138">Modificare una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="fc0c2-139">Rimuovere una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="fc0c2-140">Consentire gli indirizzi IP di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="fc0c2-141">Gestione delle origini dati</span><span class="sxs-lookup"><span data-stu-id="fc0c2-141">Managing data sources</span></span>
<span data-ttu-id="fc0c2-142">Azure Data Lake Analitica supporta attualmente hello seguenti origini dati:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="fc0c2-143">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="fc0c2-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="fc0c2-144">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fc0c2-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="fc0c2-145">Quando si crea un account Analitica, è necessario specificare un'origine dati di archivio Data Lake account toobe hello predefinita.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="fc0c2-146">Hello account archivio Data Lake predefinito viene utilizzato toostore metadati del processo e processo di log di controllo.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="fc0c2-147">Dopo aver creato un account di Data Lake Analytics, è possibile aggiungere altri account di Data Lake Store e/o account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="fc0c2-148">Trovare l'account archivio Data Lake di hello predefinito</span><span class="sxs-lookup"><span data-stu-id="fc0c2-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="fc0c2-149">È possibile trovare account archivio Data Lake di hello predefinito filtrando l'elenco di hello di origini dati da hello `IsDefault` proprietà:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="fc0c2-150">Aggiungere un'origine dati</span><span class="sxs-lookup"><span data-stu-id="fc0c2-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="fc0c2-151">Elencare le origini dati</span><span class="sxs-lookup"><span data-stu-id="fc0c2-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="fc0c2-152">Inviare processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="fc0c2-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="fc0c2-153">Inviare una stringa come script U-SQL</span><span class="sxs-lookup"><span data-stu-id="fc0c2-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="fc0c2-154">Inviare un file come script U-SQL</span><span class="sxs-lookup"><span data-stu-id="fc0c2-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="fc0c2-155">Elencare i processi in un account</span><span class="sxs-lookup"><span data-stu-id="fc0c2-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="fc0c2-156">Elencare tutti i processi di hello nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="fc0c2-157">output di Hello include hello attualmente in esecuzione processi e i processi completati di recente.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="fc0c2-158">Elencare un numero specifico di processi</span><span class="sxs-lookup"><span data-stu-id="fc0c2-158">List a specific number of jobs</span></span>

<span data-ttu-id="fc0c2-159">Per impostazione predefinita viene ordinato l'elenco hello dei processi nel tempo di invio.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="fc0c2-160">In modo più recente inviata hello visualizzati per primi i processi.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="fc0c2-161">Per impostazione predefinita, hello account ADLA memorizza i processi per 180 giorni, ma cmdlet hello Ge AdlJob per impostazione predefinita restituisce hello solo i primi 500.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="fc0c2-162">Utilizzare - toolist parametro superiore un numero specifico di processi.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="fc0c2-163">Elencare i processi in base al valore di hello della proprietà processo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="fc0c2-164">Utilizzo di hello `-State` parametro.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="fc0c2-165">È possibile combinare questi valori:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="fc0c2-166">Hello utilizzare `-Result` parametro toodetect se processi scaduti è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="fc0c2-167">Dispone di questi valori:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-167">It has these values:</span></span>

* <span data-ttu-id="fc0c2-168">Operazione annullata</span><span class="sxs-lookup"><span data-stu-id="fc0c2-168">Cancelled</span></span>
* <span data-ttu-id="fc0c2-169">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="fc0c2-169">Failed</span></span>
* <span data-ttu-id="fc0c2-170">Nessuna</span><span class="sxs-lookup"><span data-stu-id="fc0c2-170">None</span></span>
* <span data-ttu-id="fc0c2-171">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="fc0c2-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="fc0c2-172">Hello `-Submitter` parametro consente di identificare che ha inviato un processo.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="fc0c2-173">Hello `-SubmittedAfter` è utile per filtrare l'intervallo di tempo tooa.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="fc0c2-174">Scenari comuni per elencare i processi</span><span class="sxs-lookup"><span data-stu-id="fc0c2-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="fc0c2-175">Filtrare un elenco di processi</span><span class="sxs-lookup"><span data-stu-id="fc0c2-175">Filtering a list of jobs</span></span>

<span data-ttu-id="fc0c2-176">Dopo aver creato un elenco dei processi nella sessione corrente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="fc0c2-177">È possibile utilizzare l'elenco di hello toofilter PowerShell cmdlet normale.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="fc0c2-178">Filtrare un elenco di processi toohello processi inviate in hello ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="fc0c2-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="fc0c2-179">Filtrare un elenco di processi toohello i processi in hello ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="fc0c2-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="fc0c2-180">Filtrare un elenco di processi toohello processi che è stata avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="fc0c2-181">Un processo potrebbe non riuscire in fase di compilazione, e pertanto non essere mai avviato.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="fc0c2-182">Esaminiamo i processi di hello non riuscito che effettivamente avviata l'esecuzione e quindi non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="fc0c2-183">Analizzare un elenco di processi</span><span class="sxs-lookup"><span data-stu-id="fc0c2-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="fc0c2-184">Hello utilizzare `Group-Object` cmdlet tooanalyze un elenco di processi.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="fc0c2-185">Quando si esegue un'analisi, può essere utile tooadd proprietà toohello processo oggetti toomake di filtro e raggruppamento più semplice.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="fc0c2-186">Hello seguente frammento di codice viene illustrato come tooannotate a JobInfo con calcolati delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="fc0c2-187">Ottenere informazioni sulle pipeline e l'intervallo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="fc0c2-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="fc0c2-188">Hello utilizzare `Get-AdlJobPipeline` informazioni sulle pipeline di cmdlet toosee hello i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="fc0c2-189">Hello utilizzare `Get-AdlJobRecurrence` cmdlet toosee hello le informazioni sull'occorrenza per i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="fc0c2-190">Ottenere informazioni su un processo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="fc0c2-191">Ottenere lo stato di processo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-191">Get job status</span></span>

<span data-ttu-id="fc0c2-192">Ottenere lo stato di hello di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="fc0c2-193">Esaminare gli output dei processi hello</span><span class="sxs-lookup"><span data-stu-id="fc0c2-193">Examine hello job outputs</span></span>

<span data-ttu-id="fc0c2-194">Dopo aver completato il processo di hello, controllare se il file di output di hello elencando file hello in una cartella.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="fc0c2-195">Gestire i processi in esecuzione</span><span class="sxs-lookup"><span data-stu-id="fc0c2-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="fc0c2-196">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="fc0c2-197">Attendere un toofinish processo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-197">Wait for a job toofinish</span></span>

<span data-ttu-id="fc0c2-198">Anziché ripetere `Get-AdlAnalyticsJob` finché non termina un processo, è possibile utilizzare hello `Wait-AdlJob` toowait cmdlet per tooend processo hello.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="fc0c2-199">Gestire i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="fc0c2-200">Elenco di criteri di calcolo esistenti</span><span class="sxs-lookup"><span data-stu-id="fc0c2-200">List existing compute policies</span></span>

<span data-ttu-id="fc0c2-201">Hello `Get-AdlAnalyticsComputePolicy` cmdlet recupera informazioni sui criteri di calcolo per un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="fc0c2-202">Creare un criterio di calcolo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-202">Create a compute policy</span></span>

<span data-ttu-id="fc0c2-203">Hello `New-AdlAnalyticsComputePolicy` cmdlet crea un nuovo criterio di calcolo per un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="fc0c2-204">In questo esempio imposta hello toohello disponibile a AUs massimo specificato utente too50 e hello processo minimo priorità too250.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="fc0c2-205">Verificare l'esistenza di hello di un file.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="fc0c2-206">Caricamento e download</span><span class="sxs-lookup"><span data-stu-id="fc0c2-206">Uploading and downloading</span></span>

<span data-ttu-id="fc0c2-207">Caricare un file.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="fc0c2-208">Caricare in modo ricorsivo un'intera cartella.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="fc0c2-209">Scaricare un file.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="fc0c2-210">Scaricare in modo ricorsivo un'intera cartella.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="fc0c2-211">Se hello caricare o il processo di download viene interrotto, è possibile tentare processo hello tooresume dal cmdlet hello in esecuzione con hello ``-Resume`` flag.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="fc0c2-212">Gestire gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-212">Manage catalog items</span></span>

<span data-ttu-id="fc0c2-213">catalogo Hello U-SQL è usato toostructure dati e il codice affinché possano essere condivisi da script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="fc0c2-214">catalogo Hello consente prestazioni più elevate hello possibile i dati in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="fc0c2-215">Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="fc0c2-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="fc0c2-216">Elencare gli elementi nel catalogo di hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="fc0c2-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="fc0c2-217">Elencare tutti gli assembly hello in tutti i database in un Account ADLA hello.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="fc0c2-218">Ottenere informazioni dettagliate su un elemento del catalogo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="fc0c2-219">Creare le credenziali in un catalogo</span><span class="sxs-lookup"><span data-stu-id="fc0c2-219">Create credentials in a catalog</span></span>

<span data-ttu-id="fc0c2-220">All'interno di un database U-SQL creare un oggetto credenziali per un database ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="fc0c2-221">Attualmente, le credenziali di U-SQL sono hello unico tipo di elemento del catalogo che è possibile creare tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="fc0c2-222">Ottenere le informazioni di base relative all'account ADLA</span><span class="sxs-lookup"><span data-stu-id="fc0c2-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="fc0c2-223">Specificato un nome di account, hello seguente di codice cerca le informazioni di base sull'account hello</span><span class="sxs-lookup"><span data-stu-id="fc0c2-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="fc0c2-224">Utilizzo di Azure</span><span class="sxs-lookup"><span data-stu-id="fc0c2-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="fc0c2-225">Ottenere i dettagli di errore di AzureRm</span><span class="sxs-lookup"><span data-stu-id="fc0c2-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="fc0c2-226">Verificare che il processo sia in esecuzione in modalità amministratore</span><span class="sxs-lookup"><span data-stu-id="fc0c2-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="fc0c2-227">Trovare un ID tenant</span><span class="sxs-lookup"><span data-stu-id="fc0c2-227">Find a TenantID</span></span>

<span data-ttu-id="fc0c2-228">Da un nome di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="fc0c2-229">Da un ID di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="fc0c2-230">Da un indirizzo di dominio, ad esempio "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="fc0c2-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="fc0c2-231">Elencare tutte le sottoscrizioni e i relativi ID tenant</span><span class="sxs-lookup"><span data-stu-id="fc0c2-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="fc0c2-232">Creare un account Data Lake Analytics usando un modello</span><span class="sxs-lookup"><span data-stu-id="fc0c2-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="fc0c2-233">È inoltre possibile utilizzare un modello di gruppo di risorse di Azure tramite hello lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="fc0c2-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="fc0c2-234">Per altre informazioni, vedere [Distribuire un'applicazione con un modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md) e [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fc0c2-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fc0c2-235">**Modello di esempio**</span><span class="sxs-lookup"><span data-stu-id="fc0c2-235">**Example template**</span></span>

<span data-ttu-id="fc0c2-236">Salvare hello segue testo come una `.json` file e quindi utilizzare hello precedente modello hello toouse dello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0c2-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="fc0c2-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc0c2-237">Next steps</span></span>
* [<span data-ttu-id="fc0c2-238">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fc0c2-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="fc0c2-239">Introduzione a Data Lake Analytics con [ il portale di Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [l'interfaccia della riga di comando 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="fc0c2-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="fc0c2-240">Gestire Azure Data Lake Analytics con [il portale di Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [l'interfaccia della riga di comando](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="fc0c2-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
