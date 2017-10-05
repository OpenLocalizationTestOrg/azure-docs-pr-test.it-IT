---
title: Gestire Azure Data Lake Analytics con Azure PowerShell | Microsoft Docs
description: 'Informazioni su come gestire gli account, le origini dati, i processi e gli elementi del catalogo di Data Lake Analytics. '
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
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="bb013-103">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb013-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="bb013-104">Informazioni su come gestire gli account, le origini dati, i processi e gli elementi del catalogo di Azure Data Lake Analytics usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb013-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb013-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb013-105">Prerequisites</span></span>

<span data-ttu-id="bb013-106">Durante la creazione di un account di Data Lake Analytics, è necessario sapere:</span><span class="sxs-lookup"><span data-stu-id="bb013-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="bb013-107">**ID sottoscrizione**: l'ID di sottoscrizione di Azure in cui risiede l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="bb013-108">**Gruppo di risorse**: il nome del gruppo di risorse di Azure che contiene l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="bb013-109">**Nome dell'account Data Lake Analytics**: il nome dell'account deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="bb013-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="bb013-110">**Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="bb013-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="bb013-111">Questi account devono essere nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="bb013-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="bb013-112">**Posizione**: la posizione dell'account di Data Lake Analytics, ad esempio "Stati Uniti orientali 2" o altre posizioni supportate.</span><span class="sxs-lookup"><span data-stu-id="bb013-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="bb013-113">Le posizioni supportate possono essere visualizzate nella [pagina dei prezzi](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="bb013-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="bb013-114">I frammenti di codice di PowerShell in questa esercitazione usano le variabili seguenti per archiviare queste informazioni</span><span class="sxs-lookup"><span data-stu-id="bb013-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="bb013-115">Accesso</span><span class="sxs-lookup"><span data-stu-id="bb013-115">Log in</span></span>

<span data-ttu-id="bb013-116">Accesso con un ID di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bb013-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="bb013-117">Accesso con un nome di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bb013-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="bb013-118">Il cmdlet `Login-AzureRmAccount` richiede sempre le credenziali.</span><span class="sxs-lookup"><span data-stu-id="bb013-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="bb013-119">È possibile evitare tale richiesta usando i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb013-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="bb013-120">Gestione di account</span><span class="sxs-lookup"><span data-stu-id="bb013-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="bb013-121">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="bb013-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="bb013-122">Se non si ha già un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) da usare, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="bb013-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="bb013-123">Per ogni account Data Lake Analytics deve essere configurato un account Data Lake Store che viene usato per l'archiviazione dei log.</span><span class="sxs-lookup"><span data-stu-id="bb013-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="bb013-124">È possibile riusare un account esistente o creare un account.</span><span class="sxs-lookup"><span data-stu-id="bb013-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="bb013-125">Quando sono disponibili un gruppo di risorse e un account Data Lake Store, creare un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="bb013-126">Ottenere informazioni su un account</span><span class="sxs-lookup"><span data-stu-id="bb013-126">Get information about an account</span></span>

<span data-ttu-id="bb013-127">Ottenere dettagli su un account.</span><span class="sxs-lookup"><span data-stu-id="bb013-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="bb013-128">Verificare l'esistenza di un account specifico di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="bb013-129">Il cmdlet restituisce `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="bb013-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="bb013-130">Verificare l'esistenza di un account specifico di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bb013-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="bb013-131">Il cmdlet restituisce `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="bb013-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="bb013-132">Elenco di account</span><span class="sxs-lookup"><span data-stu-id="bb013-132">Listing accounts</span></span>

<span data-ttu-id="bb013-133">Elencare gli account di Data Lake Analytics all'interno della sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="bb013-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="bb013-134">Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="bb013-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="bb013-135">Gestione delle regole del firewall</span><span class="sxs-lookup"><span data-stu-id="bb013-135">Managing firewall rules</span></span>

<span data-ttu-id="bb013-136">Elencare le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="bb013-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="bb013-137">Aggiungere una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="bb013-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="bb013-138">Modificare una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="bb013-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="bb013-139">Rimuovere una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="bb013-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="bb013-140">Consentire gli indirizzi IP di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb013-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="bb013-141">Gestione delle origini dati</span><span class="sxs-lookup"><span data-stu-id="bb013-141">Managing data sources</span></span>
<span data-ttu-id="bb013-142">Azure Data Lake Analytics supporta attualmente le origini dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb013-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="bb013-143">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="bb013-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="bb013-144">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bb013-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="bb013-145">Quando si crea un account di Analytics, è necessario impostare un account di Data Lake Store come origine dati predefinita.</span><span class="sxs-lookup"><span data-stu-id="bb013-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="bb013-146">L'account di Data Lake Store predefinito viene usato per archiviare i metadati e i log di controllo dei processi.</span><span class="sxs-lookup"><span data-stu-id="bb013-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="bb013-147">Dopo aver creato un account di Data Lake Analytics, è possibile aggiungere altri account di Data Lake Store e/o account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bb013-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="bb013-148">Trovare l'account di Data Lake Store predefinito</span><span class="sxs-lookup"><span data-stu-id="bb013-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="bb013-149">È possibile trovare l'account Data Lake Store predefinito filtrando l'elenco di origine dati secondo il criterio di proprietà `IsDefault`:</span><span class="sxs-lookup"><span data-stu-id="bb013-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="bb013-150">Aggiungere un'origine dati</span><span class="sxs-lookup"><span data-stu-id="bb013-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="bb013-151">Elencare le origini dati</span><span class="sxs-lookup"><span data-stu-id="bb013-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="bb013-152">Inviare processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="bb013-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="bb013-153">Inviare una stringa come script U-SQL</span><span class="sxs-lookup"><span data-stu-id="bb013-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="bb013-154">Inviare un file come script U-SQL</span><span class="sxs-lookup"><span data-stu-id="bb013-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="bb013-155">Elencare i processi in un account</span><span class="sxs-lookup"><span data-stu-id="bb013-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="bb013-156">Elencare tutti i processi nell'account.</span><span class="sxs-lookup"><span data-stu-id="bb013-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="bb013-157">L'output include i processi attualmente in esecuzione e quelli completati di recente.</span><span class="sxs-lookup"><span data-stu-id="bb013-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="bb013-158">Elencare un numero specifico di processi</span><span class="sxs-lookup"><span data-stu-id="bb013-158">List a specific number of jobs</span></span>

<span data-ttu-id="bb013-159">Per impostazione predefinita, l'elenco dei processi viene ordinato in base all'ora di invio.</span><span class="sxs-lookup"><span data-stu-id="bb013-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="bb013-160">Pertanto, i processi inviati di recente vengono visualizzati per primi.</span><span class="sxs-lookup"><span data-stu-id="bb013-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="bb013-161">Per impostazione predefinita, l’account di ADLA memorizza i processi per 180 giorni, ma il cmdlet Ge AdlJob ne restituisce solo i primi 500.</span><span class="sxs-lookup"><span data-stu-id="bb013-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="bb013-162">Utilizzare i parametri superiori per elencare un numero specifico di processi.</span><span class="sxs-lookup"><span data-stu-id="bb013-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="bb013-163">Elencare i processi in base al valore della proprietà processo</span><span class="sxs-lookup"><span data-stu-id="bb013-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="bb013-164">Uso del parametro `-State`.</span><span class="sxs-lookup"><span data-stu-id="bb013-164">Using the `-State` parameter.</span></span> <span data-ttu-id="bb013-165">È possibile combinare questi valori:</span><span class="sxs-lookup"><span data-stu-id="bb013-165">You can combine any of these values:</span></span>

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
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="bb013-166">Usare il parametro `-Result` per rilevare se i processi finiti sono stati completati correttamente.</span><span class="sxs-lookup"><span data-stu-id="bb013-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="bb013-167">Dispone di questi valori:</span><span class="sxs-lookup"><span data-stu-id="bb013-167">It has these values:</span></span>

* <span data-ttu-id="bb013-168">Operazione annullata</span><span class="sxs-lookup"><span data-stu-id="bb013-168">Cancelled</span></span>
* <span data-ttu-id="bb013-169">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="bb013-169">Failed</span></span>
* <span data-ttu-id="bb013-170">Nessuna</span><span class="sxs-lookup"><span data-stu-id="bb013-170">None</span></span>
* <span data-ttu-id="bb013-171">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="bb013-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="bb013-172">Il parametro `-Submitter` consente di identificare chi ha inviato un processo.</span><span class="sxs-lookup"><span data-stu-id="bb013-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="bb013-173">Il `-SubmittedAfter` è utile per un filtraggio in base a un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="bb013-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="bb013-174">Scenari comuni per elencare i processi</span><span class="sxs-lookup"><span data-stu-id="bb013-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="bb013-175">Filtrare un elenco di processi</span><span class="sxs-lookup"><span data-stu-id="bb013-175">Filtering a list of jobs</span></span>

<span data-ttu-id="bb013-176">Dopo aver creato un elenco dei processi nella sessione corrente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb013-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="bb013-177">È possibile utilizzare i cmdlet normali di PowerShell per filtrare l'elenco.</span><span class="sxs-lookup"><span data-stu-id="bb013-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="bb013-178">Filtrare un elenco di processi per i processi inviati nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="bb013-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="bb013-179">Filtrare un elenco di processi per i processi terminati nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="bb013-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="bb013-180">Filtrare un elenco di processi per i processi con esecuzione avviata.</span><span class="sxs-lookup"><span data-stu-id="bb013-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="bb013-181">Un processo potrebbe non riuscire in fase di compilazione, e pertanto non essere mai avviato.</span><span class="sxs-lookup"><span data-stu-id="bb013-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="bb013-182">Esaminiamo i processi non riusciti, in cui l’esecuzione è stata avviata ma non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="bb013-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="bb013-183">Analizzare un elenco di processi</span><span class="sxs-lookup"><span data-stu-id="bb013-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="bb013-184">Utilizzare il cmdlet `Group-Object` per analizzare un elenco di processi.</span><span class="sxs-lookup"><span data-stu-id="bb013-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="bb013-185">Quando si esegue un'analisi, può essere utile aggiungere proprietà agli oggetti di processo per rendere più semplice il filtraggio e il raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="bb013-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="bb013-186">Il frammento di codice seguente mostra come annotare un JobInfo con proprietà calcolate.</span><span class="sxs-lookup"><span data-stu-id="bb013-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="bb013-187">Ottenere informazioni sulle pipeline e l'intervallo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="bb013-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="bb013-188">Utilizzare il cmdlet `Get-AdlJobPipeline` per visualizzare le informazioni di pipeline dei processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bb013-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="bb013-189">Utilizzare il cmdlet `Get-AdlJobRecurrence` per visualizzare le informazioni relative all'intervallo di esecuzione dei processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bb013-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="bb013-190">Ottenere informazioni su un processo</span><span class="sxs-lookup"><span data-stu-id="bb013-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="bb013-191">Ottenere lo stato di processo</span><span class="sxs-lookup"><span data-stu-id="bb013-191">Get job status</span></span>

<span data-ttu-id="bb013-192">Ottenere lo stato di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="bb013-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="bb013-193">Esaminare gli output di processo</span><span class="sxs-lookup"><span data-stu-id="bb013-193">Examine the job outputs</span></span>

<span data-ttu-id="bb013-194">Al termine del processo, controllare se il file di output esiste elencando i file in una cartella.</span><span class="sxs-lookup"><span data-stu-id="bb013-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="bb013-195">Gestire i processi in esecuzione</span><span class="sxs-lookup"><span data-stu-id="bb013-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="bb013-196">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="bb013-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="bb013-197">Attendere il completamento di un processo</span><span class="sxs-lookup"><span data-stu-id="bb013-197">Wait for a job to finish</span></span>

<span data-ttu-id="bb013-198">Anziché ripetere `Get-AdlAnalyticsJob` finché non termina un processo, è possibile usare il cmdlet `Wait-AdlJob` per attendere la fine del processo.</span><span class="sxs-lookup"><span data-stu-id="bb013-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="bb013-199">Gestire i criteri di calcolo</span><span class="sxs-lookup"><span data-stu-id="bb013-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="bb013-200">Elenco di criteri di calcolo esistenti</span><span class="sxs-lookup"><span data-stu-id="bb013-200">List existing compute policies</span></span>

<span data-ttu-id="bb013-201">Il cmdlet `Get-AdlAnalyticsComputePolicy` recupera informazioni sui criteri di calcolo per un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="bb013-202">Creare un criterio di calcolo</span><span class="sxs-lookup"><span data-stu-id="bb013-202">Create a compute policy</span></span>

<span data-ttu-id="bb013-203">Il cmdlet `New-AdlAnalyticsComputePolicy` crea un nuovo criterio di calcolo per un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb013-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="bb013-204">In questo esempio le unità di analisi massime disponibili per l'utente specificato sono 50 e la priorità minima del processo è pari a 250.</span><span class="sxs-lookup"><span data-stu-id="bb013-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="bb013-205">Verificare l'esistenza di un file.</span><span class="sxs-lookup"><span data-stu-id="bb013-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="bb013-206">Caricamento e download</span><span class="sxs-lookup"><span data-stu-id="bb013-206">Uploading and downloading</span></span>

<span data-ttu-id="bb013-207">Caricare un file.</span><span class="sxs-lookup"><span data-stu-id="bb013-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="bb013-208">Caricare in modo ricorsivo un'intera cartella.</span><span class="sxs-lookup"><span data-stu-id="bb013-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="bb013-209">Scaricare un file.</span><span class="sxs-lookup"><span data-stu-id="bb013-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="bb013-210">Scaricare in modo ricorsivo un'intera cartella.</span><span class="sxs-lookup"><span data-stu-id="bb013-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="bb013-211">Se il processo di caricamento o download viene interrotto, è possibile tentare di riprendere il processo eseguendo nuovamente il cmdlet con il flag ``-Resume``.</span><span class="sxs-lookup"><span data-stu-id="bb013-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="bb013-212">Gestire gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="bb013-212">Manage catalog items</span></span>

<span data-ttu-id="bb013-213">Il catalogo di U-SQL viene usato per definire la struttura dei dati e del codice in modo da poterli condividere mediante U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bb013-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="bb013-214">Il catalogo consente di ottenere le migliori prestazioni possibili con i dati in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bb013-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="bb013-215">Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="bb013-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="bb013-216">Elencare elementi nel catalogo U-SQL</span><span class="sxs-lookup"><span data-stu-id="bb013-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="bb013-217">Elencare tutti gli assembly in tutti i database in un account ADLA.</span><span class="sxs-lookup"><span data-stu-id="bb013-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="bb013-218">Ottenere informazioni dettagliate su un elemento del catalogo</span><span class="sxs-lookup"><span data-stu-id="bb013-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="bb013-219">Creare le credenziali in un catalogo</span><span class="sxs-lookup"><span data-stu-id="bb013-219">Create credentials in a catalog</span></span>

<span data-ttu-id="bb013-220">All'interno di un database U-SQL creare un oggetto credenziali per un database ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="bb013-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="bb013-221">Attualmente le credenziali di U-SQL sono l'unico tipo di elemento del catalogo che è possibile creare tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb013-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="bb013-222">Ottenere le informazioni di base relative all'account ADLA</span><span class="sxs-lookup"><span data-stu-id="bb013-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="bb013-223">Dato un nome di account, il codice seguente cerca le informazioni di base sull'account</span><span class="sxs-lookup"><span data-stu-id="bb013-223">Given an account name, the following code looks up basic information about the account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="bb013-224">Utilizzo di Azure</span><span class="sxs-lookup"><span data-stu-id="bb013-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="bb013-225">Ottenere i dettagli di errore di AzureRm</span><span class="sxs-lookup"><span data-stu-id="bb013-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="bb013-226">Verificare che il processo sia in esecuzione in modalità amministratore</span><span class="sxs-lookup"><span data-stu-id="bb013-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="bb013-227">Trovare un ID tenant</span><span class="sxs-lookup"><span data-stu-id="bb013-227">Find a TenantID</span></span>

<span data-ttu-id="bb013-228">Da un nome di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="bb013-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="bb013-229">Da un ID di sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="bb013-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="bb013-230">Da un indirizzo di dominio, ad esempio "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="bb013-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="bb013-231">Elencare tutte le sottoscrizioni e i relativi ID tenant</span><span class="sxs-lookup"><span data-stu-id="bb013-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="bb013-232">Creare un account Data Lake Analytics usando un modello</span><span class="sxs-lookup"><span data-stu-id="bb013-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="bb013-233">È inoltre possibile usare un modello di gruppo di risorse di Azure tramite lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bb013-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="bb013-234">Per altre informazioni, vedere [Distribuire un'applicazione con un modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md) e [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bb013-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="bb013-235">**Modello di esempio**</span><span class="sxs-lookup"><span data-stu-id="bb013-235">**Example template**</span></span>

<span data-ttu-id="bb013-236">Salvare il testo seguente come un file `.json` e usare lo script di PowerShell precedente per usare il modello.</span><span class="sxs-lookup"><span data-stu-id="bb013-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
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

## <a name="next-steps"></a><span data-ttu-id="bb013-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb013-237">Next steps</span></span>
* [<span data-ttu-id="bb013-238">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bb013-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="bb013-239">Introduzione a Data Lake Analytics con [ il portale di Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [l'interfaccia della riga di comando 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="bb013-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="bb013-240">Gestire Azure Data Lake Analytics con [il portale di Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [l'interfaccia della riga di comando](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bb013-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
