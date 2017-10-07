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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Gestire Azure Data Lake Analytics tramite Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Informazioni su come account di Azure Data Lake Analitica toomanage, origini dati, processi e gli elementi del catalogo con Azure PowerShell. 

## <a name="prerequisites"></a>Prerequisiti

Quando si crea un account Data Lake Analitica, è necessario tooknow:

* **ID sottoscrizione**: hello ID sottoscrizione di Azure in cui risiede l'account Data Lake Analitica.
* **Gruppo di risorse**: nome hello hello Azure del gruppo di risorse che contiene l'account Data Lake Analitica.
* **Nome dell'account data Lake Analitica**: hello account nome deve contenere solo lettere minuscole e numeri.
* **Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito. Questi account devono essere in hello nello stesso percorso.
* **Percorso**: percorso hello dell'account Data Lake Analitica, ad esempio "Stati Uniti orientali 2" o altre supportati percorsi. Le posizioni supportate possono essere visualizzate nella [pagina dei prezzi](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

frammenti di codice PowerShell Hello in questa esercitazione usare questi toostore variabili queste informazioni

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Accesso

Accesso con un ID di sottoscrizione.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Accesso con un nome di sottoscrizione.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Hello `Login-AzureRmAccount` cmdlet richiede sempre le credenziali. È possibile evitare che venga richiesto tramite hello seguente cmdlet:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Gestione di account

### <a name="create-a-data-lake-analytics-account"></a>Creare un account di Analisi Data Lake

Se dispone già di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crearne uno. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Per ogni account Data Lake Analytics deve essere configurato un account Data Lake Store che viene usato per l'archiviazione dei log. È possibile riusare un account esistente o creare un account. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Quando sono disponibili un gruppo di risorse e un account Data Lake Store, creare un account Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Ottenere informazioni su un account

Ottenere dettagli su un account.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Verificare l'esistenza di hello di uno specifico account Data Lake Analitica. Restituisce i cmdlet di Hello `True` o `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Verificare l'esistenza di hello di uno specifico account archivio Data Lake. Restituisce i cmdlet di Hello `True` o `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Elenco di account

Account di Analitica elenco Data Lake nella sottoscrizione corrente hello.

```powershell
Get-AdlAnalyticsAccount
```

Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Gestione delle regole del firewall

Elencare le regole del firewall.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Aggiungere una regola del firewall.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Modificare una regola del firewall.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Rimuovere una regola del firewall.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Consentire gli indirizzi IP di Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Gestione delle origini dati
Azure Data Lake Analitica supporta attualmente hello seguenti origini dati:

* [Archivio Data Lake di Azure](../data-lake-store/data-lake-store-overview.md)
* [Archiviazione di Azure](../storage/common/storage-introduction.md)

Quando si crea un account Analitica, è necessario specificare un'origine dati di archivio Data Lake account toobe hello predefinita. Hello account archivio Data Lake predefinito viene utilizzato toostore metadati del processo e processo di log di controllo. Dopo aver creato un account di Data Lake Analytics, è possibile aggiungere altri account di Data Lake Store e/o account di archiviazione. 

### <a name="find-hello-default-data-lake-store-account"></a>Trovare l'account archivio Data Lake di hello predefinito

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

È possibile trovare account archivio Data Lake di hello predefinito filtrando l'elenco di hello di origini dati da hello `IsDefault` proprietà:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Aggiungere un'origine dati

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Elencare le origini dati

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Inviare processi U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Inviare una stringa come script U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Inviare un file come script U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Elencare i processi in un account

### <a name="list-all-hello-jobs-in-hello-account"></a>Elencare tutti i processi di hello nell'account hello. 

output di Hello include hello attualmente in esecuzione processi e i processi completati di recente.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Elencare un numero specifico di processi

Per impostazione predefinita viene ordinato l'elenco hello dei processi nel tempo di invio. In modo più recente inviata hello visualizzati per primi i processi. Per impostazione predefinita, hello account ADLA memorizza i processi per 180 giorni, ma cmdlet hello Ge AdlJob per impostazione predefinita restituisce hello solo i primi 500. Utilizzare - toolist parametro superiore un numero specifico di processi.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Elencare i processi in base al valore di hello della proprietà processo

Utilizzo di hello `-State` parametro. È possibile combinare questi valori:

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

Hello utilizzare `-Result` parametro toodetect se processi scaduti è stata completata correttamente. Dispone di questi valori:

* Operazione annullata
* Operazione non riuscita
* Nessuna
* Operazione completata

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Hello `-Submitter` parametro consente di identificare che ha inviato un processo.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Hello `-SubmittedAfter` è utile per filtrare l'intervallo di tempo tooa.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Scenari comuni per elencare i processi


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

## <a name="filtering-a-list-of-jobs"></a>Filtrare un elenco di processi

Dopo aver creato un elenco dei processi nella sessione corrente di PowerShell. È possibile utilizzare l'elenco di hello toofilter PowerShell cmdlet normale.

Filtrare un elenco di processi toohello processi inviate in hello ultime 24 ore

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrare un elenco di processi toohello i processi in hello ultime 24 ore

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtrare un elenco di processi toohello processi che è stata avviata l'esecuzione. Un processo potrebbe non riuscire in fase di compilazione, e pertanto non essere mai avviato. Esaminiamo i processi di hello non riuscito che effettivamente avviata l'esecuzione e quindi non è riuscita.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Analizzare un elenco di processi

Hello utilizzare `Group-Object` cmdlet tooanalyze un elenco di processi.

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
Quando si esegue un'analisi, può essere utile tooadd proprietà toohello processo oggetti toomake di filtro e raggruppamento più semplice. Hello seguente frammento di codice viene illustrato come tooannotate a JobInfo con calcolati delle proprietà.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Ottenere informazioni sulle pipeline e l'intervallo di esecuzione

Hello utilizzare `Get-AdlJobPipeline` informazioni sulle pipeline di cmdlet toosee hello i processi inviati in precedenza.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Hello utilizzare `Get-AdlJobRecurrence` cmdlet toosee hello le informazioni sull'occorrenza per i processi inviati in precedenza.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Ottenere informazioni su un processo

### <a name="get-job-status"></a>Ottenere lo stato di processo

Ottenere lo stato di hello di un processo specifico.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Esaminare gli output dei processi hello

Dopo aver completato il processo di hello, controllare se il file di output di hello elencando file hello in una cartella.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Gestire i processi in esecuzione

### <a name="cancel-a-job"></a>Annullare un processo

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Attendere un toofinish processo

Anziché ripetere `Get-AdlAnalyticsJob` finché non termina un processo, è possibile utilizzare hello `Wait-AdlJob` toowait cmdlet per tooend processo hello.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Gestire i criteri di calcolo

### <a name="list-existing-compute-policies"></a>Elenco di criteri di calcolo esistenti

Hello `Get-AdlAnalyticsComputePolicy` cmdlet recupera informazioni sui criteri di calcolo per un account Data Lake Analitica.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Creare un criterio di calcolo

Hello `New-AdlAnalyticsComputePolicy` cmdlet crea un nuovo criterio di calcolo per un account Data Lake Analitica. In questo esempio imposta hello toohello disponibile a AUs massimo specificato utente too50 e hello processo minimo priorità too250.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Verificare l'esistenza di hello di un file.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Caricamento e download

Caricare un file.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Caricare in modo ricorsivo un'intera cartella.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Scaricare un file.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Scaricare in modo ricorsivo un'intera cartella.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Se hello caricare o il processo di download viene interrotto, è possibile tentare processo hello tooresume dal cmdlet hello in esecuzione con hello ``-Resume`` flag.

## <a name="manage-catalog-items"></a>Gestire gli elementi del catalogo

catalogo Hello U-SQL è usato toostructure dati e il codice affinché possano essere condivisi da script U-SQL. catalogo Hello consente prestazioni più elevate hello possibile i dati in Azure Data Lake. Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Elencare gli elementi nel catalogo di hello U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Elencare tutti gli assembly hello in tutti i database in un Account ADLA hello.

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

### <a name="get-details-about-a-catalog-item"></a>Ottenere informazioni dettagliate su un elemento del catalogo

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Creare le credenziali in un catalogo

All'interno di un database U-SQL creare un oggetto credenziali per un database ospitato in Azure. Attualmente, le credenziali di U-SQL sono hello unico tipo di elemento del catalogo che è possibile creare tramite PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Ottenere le informazioni di base relative all'account ADLA

Specificato un nome di account, hello seguente di codice cerca le informazioni di base sull'account hello

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

## <a name="working-with-azure"></a>Utilizzo di Azure

### <a name="get-details-of-azurerm-errors"></a>Ottenere i dettagli di errore di AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Verificare che il processo sia in esecuzione in modalità amministratore

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Trovare un ID tenant

Da un nome di sottoscrizione:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

Da un ID di sottoscrizione:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

Da un indirizzo di dominio, ad esempio "contoso.com"


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Elencare tutte le sottoscrizioni e i relativi ID tenant

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Creare un account Data Lake Analytics usando un modello

È inoltre possibile utilizzare un modello di gruppo di risorse di Azure tramite hello lo script di PowerShell seguente:

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

Per altre informazioni, vedere [Distribuire un'applicazione con un modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md) e [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Modello di esempio**

Salvare hello segue testo come una `.json` file e quindi utilizzare hello precedente modello hello toouse dello script di PowerShell. 

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

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* Introduzione a Data Lake Analytics con [ il portale di Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [l'interfaccia della riga di comando 2.0](data-lake-analytics-get-started-cli2.md)
* Gestire Azure Data Lake Analytics con [il portale di Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [l'interfaccia della riga di comando](data-lake-analytics-manage-use-cli.md) 
