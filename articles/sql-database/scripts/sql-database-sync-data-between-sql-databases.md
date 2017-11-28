---
title: "esempio aaaPowerShell-sincronizzazione tra più database SQL di Azure | Documenti Microsoft"
description: "Azure PowerShell script di esempio toosync tra più database SQL di Azure"
services: sql-database
documentationcenter: sql-database
author: jognanay
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/31/2017
ms.author: douglasl
ms.openlocfilehash: 5bf92da25051bd53db536b295959b6f9af9625a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toosync-between-multiple-azure-sql-databases"></a><span data-ttu-id="2d2e3-103">Utilizzare PowerShell toosync tra più database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="2d2e3-103">Use PowerShell toosync between multiple Azure SQL databases</span></span>
 
<span data-ttu-id="2d2e3-104">In questo esempio di PowerShell Configura sincronizzazione dati toosync tra più database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-104">This PowerShell example configures Data Sync toosync between multiple Azure SQL databases.</span></span>

<span data-ttu-id="2d2e3-105">In questo esempio richiede hello Azure PowerShell modulo 4.2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-105">This sample requires hello Azure PowerShell module version 4.2 or later.</span></span> <span data-ttu-id="2d2e3-106">Eseguire `Get-Module -ListAvailable AzureRM` toofind versione di hello installato.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-106">Run `Get-Module -ListAvailable AzureRM` toofind hello installed version.</span></span> <span data-ttu-id="2d2e3-107">Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2d2e3-107">If you need tooinstall or upgrade, see [Install Azure PowerShell module](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span>
 
<span data-ttu-id="2d2e3-108">Eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-108">Run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2d2e3-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2d2e3-109">Sample script</span></span>

```powershell
# prerequisites: 
# 1. Create an Azure Database from AdventureWorksLT sample database as hub database
# 2. Create an Azure Database in hello same region as sync database
# 3. Create an Azure Database as member database
# 4. Update hello parameters below before running hello sample
#
using namespace Microsoft.Azure.Commands.Sql.DataSync.Model
using namespace System.Collections.Generic

# Hub database info
# Subscription id for hub database
$SubscriptionId = "subscription_guid"
# Resrouce group name for hub database
$ResourceGroupName = "ResourceGroup"
# Server name for hub database
$ServerName = "Server"
# Database name for hub database
$DatabaseName = "AdventureWorks"

# Sync database info
# Resource group name for sync database
$SyncDatabaseResourceGroupName = "ResourceGroup"
# Server name for sync database
$SyncDatabaseServerName = "Server"
# Sync database name
$SyncDatabaseName = "SyncDatabase"

# Sync group info
# Sync group name
$SyncGroupName = "SampleSyncGroup1"
# Conflict resolution Policy. Value can be HubWin or MemberWin
$ConflictResolutionPolicy = "HubWin"
# Sync interval in seconds. Value must be no less than 300
$IntervalInSeconds = 300

# Member database info
# Member name
$SyncMemberName = "member"
# Member server name
$MemberServerName = "MemberServer"
# Member database name
$MemberDatabaseName = "SyncDatabase1"
# Member database type. Value can be AzureSqlDatabase or SqlServerDatabase
$MemberDatabaseType = "AzureSqlDatabase"
# Sync direction. Value can be Bidirectional, Onewaymembertohub, Onewayhubtomember
$SyncDirection = "Bidirectional"

# Other info
# Temp file toosave hello sync schema
$TempFile = $env:TEMP+"\syncSchema.json"

# List of included columns and tables in quoted name
$IncludedColumnsAndTables =  "[SalesLT].[Address].[AddressID]",
                             "[SalesLT].[Address].[AddressLine2]",
                             "[SalesLT].[Address].[rowguid]",
                             "[SalesLT].[Address].[PostalCode]",
                             "[SalesLT].[ProductDescription]"
$MetadataList = [System.Collections.ArrayList]::new($IncludedColumnsAndTables)


add-azurermaccount 
select-azurermsubscription -SubscriptionId $SubscriptionId

# Use this section if it is safe tooshow password in hello script.
# Otherwise, use hello PromptForCredential
# $User = "username"
# $PWord = ConvertTo-SecureString -String "Password" -AsPlainText -Force
# $Credential = New-Object -TypeName "System.Management.Automation.PSCredential" -ArgumentList $User, $PWord

$Credential = $Host.ui.PromptForCredential("Need credential", 
              "Please enter your user name and password for server "+$ServerName+".database.windows.net", 
              "", 
              "")

# Create a new sync group
Write-Host "Creating Sync Group"$SyncGroupName
New-AzureRmSqlSyncGroup   -ResourceGroupName $ResourceGroupName `
                            -ServerName $ServerName `
                            -DatabaseName $DatabaseName `
                            -Name $SyncGroupName `
                            -SyncDatabaseName $SyncDatabaseName `
                            -SyncDatabaseServerName $SyncDatabaseServerName `
                            -SyncDatabaseResourceGroupName $SyncDatabaseResourceGroupName `
                            -ConflictResolutionPolicy $ConflictResolutionPolicy `
                            -DatabaseCredential $Credential

# Use this section if it is safe tooshow password in hello script.
#$User = "username"
#$Password = ConvertTo-SecureString -String "password" -AsPlainText -Force
#$Credential = New-Object -TypeName "System.Management.Automation.PSCredential" -ArgumentList $User, $Password

$Credential = $Host.ui.PromptForCredential("Need credential", 
              "Please enter your user name and password for server "+$MemberServerName, 
              "", 
              "")

# Add a new sync member
Write-Host "Adding member"$SyncMemberName" toohello sync group"
New-AzureRmSqlSyncMember   -ResourceGroupName $ResourceGroupName `
                            -ServerName $ServerName `
                            -DatabaseName $DatabaseName `
                            -SyncGroupName $SyncGroupName `
                            -Name $SyncMemberName `
                            -MemberDatabaseCredential $Credential `
                            -MemberDatabaseName $MemberDatabaseName `
                            -MemberServerName ($MemberServerName + ".database.windows.net" `
                            -MemberDatabaseType $MemberDatabaseType `
                            -SyncDirection $SyncDirection

# Refresh database schema from hub database
# Specify hello -SyncMemberName parameter if you want toorefresh schema from hello member database
Write-Host "Refreshing database schema from hub database"
$StartTime= Get-Date
Update-AzureRmSqlSyncSchema   -ResourceGroupName $ResourceGroupName `
                              -ServerName $ServerName `
                              -DatabaseName $DatabaseName `
                              -SyncGroupName $SyncGroupName


#Waiting for successful refresh

$StartTime=$StartTime.ToUniversalTime()
$timer=0
$timeout=90
# Check hello log and see if refresh has gone through
Write-Host "Check for successful refresh"
$IsSucceeded = $false
While ($IsSucceeded -eq $false)
{
    Start-Sleep -s 10
    $timer=$timer+1
    $Details = Get-AzureRmSqlSyncSchema -SyncGroupName $SyncGroupName -ServerName $ServerName -DatabaseName $DatabaseName -ResourceGroupName $ResourceGroupName
    if ($Details.LastUpdateTime -gt $StartTime)
      {
        Write-Host "Refresh was successful"
        $IsSucceeded = $true
      }
    if ($timer -eq $timeout) 
      {
              Write-Host "Refresh timed out"
        break;
      }
}



# Get hello database schema 
Write-Host "Adding tables and columns toohello sync schema"
$databaseSchema = Get-AzureRmSqlSyncSchema   -ResourceGroupName $ResourceGroupName `
                                             -ServerName $ServerName `
                                             -DatabaseName $DatabaseName `
                                             -SyncGroupName $SyncGroupName `

$databaseSchema | ConvertTo-Json -depth 5 -Compress | Out-File "c:\tmp\databaseSchema"     
$newSchema = [AzureSqlSyncGroupSchemaModel]::new()
$newSchema.Tables = [List[AzureSqlSyncGroupSchemaTableModel]]::new();

# Add columns and tables toohello sync schema
foreach ($tableSchema in $databaseSchema.Tables)
{
    $newTableSchema = [AzureSqlSyncGroupSchemaTableModel]::new()
    $newTableSchema.QuotedName = $tableSchema.QuotedName
    $newTableSchema.Columns = [List[AzureSqlSyncGroupSchemaColumnModel]]::new();
    $addAllColumns = $false
    if ($MetadataList.Contains($tableSchema.QuotedName))
    {
        if ($tableSchema.HasError)
        {
            $fullTableName = $tableSchema.QuotedName
            Write-Host "Can't add table $fullTableName toohello sync schema" -foregroundcolor "Red"
            Write-Host $tableSchema.ErrorId -foregroundcolor "Red"
            continue;
        }
        else
        {
            $addAllColumns = $true
        }
    }
    foreach($columnSchema in $tableSchema.Columns)
    {
        $fullColumnName = $tableSchema.QuotedName + "." + $columnSchema.QuotedName
        if ($addAllColumns -or $MetadataList.Contains($fullColumnName))
        {
            if ((-not $addAllColumns) -and $tableSchema.HasError)
            {
                Write-Host "Can't add column $fullColumnName toohello sync schema" -foregroundcolor "Red"
                Write-Host $tableSchema.ErrorId -foregroundcolor "Red"c            }
            elseif ((-not $addAllColumns) -and $columnSchema.HasError)
            {
                Write-Host "Can't add column $fullColumnName toohello sync schema" -foregroundcolor "Red"
                Write-Host $columnSchema.ErrorId -foregroundcolor "Red"
            }
            else
            {
                Write-Host "Adding"$fullColumnName" toohello sync schema"
                $newColumnSchema = [AzureSqlSyncGroupSchemaColumnModel]::new()
                $newColumnSchema.QuotedName = $columnSchema.QuotedName
                $newColumnSchema.DataSize = $columnSchema.DataSize
                $newColumnSchema.DataType = $columnSchema.DataType
                $newTableSchema.Columns.Add($newColumnSchema)
            }
        }
    }
    if ($newTableSchema.Columns.Count -gt 0)
    {
        $newSchema.Tables.Add($newTableSchema)
    }
}

# Convert sync schema tooJson format
$schemaString = $newSchema | ConvertTo-Json -depth 5 -Compress

# workaround a powershell bug
$schemaString = $schemaString.Replace('"Tables"', '"tables"').Replace('"Columns"', '"columns"').Replace('"QuotedName"', '"quotedName"').Replace('"MasterSyncMemberName"','"masterSyncMemberName"')

# Save hello sync schema tooa temp file
$schemaString | Out-File $TempFile

# Update sync schema
Write-Host "Updating hello sync schema"
Update-AzureRmSqlSyncGroup  -ResourceGroupName $ResourceGroupName `
                            -ServerName $ServerName `
                            -DatabaseName $DatabaseName `
                            -Name $SyncGroupName `
                            -Schema $TempFile

$SyncStartTime = Get-Date

# Trigger sync manually
Write-Host "Trigger sync manually"
Start-AzureRmSqlSyncGroupSync  -ResourceGroupName $ResourceGroupName `
                               -ServerName $ServerName `
                               -DatabaseName $DatabaseName `
                               -SyncGroupName $SyncGroupName

# Check hello sync log and wait until hello first sync succeeded
Write-Host "Check hello sync log"
$IsSucceeded = $false
For ($i = 0; ($i -lt 300) -and (-not $IsSucceeded); $i = $i + 10)
{
    Start-Sleep -s 10
    $SyncLogEndTime = Get-Date
    $SyncLogList = Get-AzureRmSqlSyncGroupLog  -ResourceGroupName $ResourceGroupName `
                                           -ServerName $ServerName `
                                           -DatabaseName $DatabaseName `
                                           -SyncGroupName $SyncGroupName `
                                           -StartTime $SyncLogStartTime.ToUniversalTime() `
                                           -EndTime $SyncLogEndTime.ToUniversalTime()
    if ($SynclogList.Length -gt 0)
    {
        foreach ($SyncLog in $SyncLogList)
        {
            if ($SyncLog.Details.Contains("Sync completed successfully"))
            {
                Write-Host $SyncLog.TimeStamp : $SyncLog.Details
                $IsSucceeded = $true
            }
        }
    }
}

if ($IsSucceeded)
{
    # Enable scheduled sync
    Write-Host "Enable hello scheduled sync with 300 seconds interval"
    Update-AzureRmSqlSyncGroup  -ResourceGroupName $ResourceGroupName `
                                -ServerName $ServerName `
                                -DatabaseName $DatabaseName `
                                -Name $SyncGroupName `
                                -IntervalInSeconds $IntervalInSeconds
}
else
{
    # Output all log if sync doesn't succeed in 300 seconds
    $SyncLogEndTime = Get-Date
    $SyncLogList = Get-AzureRmSqlSyncGroupLog  -ResourceGroupName $ResourceGroupName `
                                           -ServerName $ServerName `
                                           -DatabaseName $DatabaseName `
                                           -SyncGroupName $SyncGroupName `
                                           -StartTime $SyncLogStartTime.ToUniversalTime() `
                                           -EndTime $SyncLogEndTime.ToUniversalTime()
    if ($SynclogList.Length -gt 0)
    {
        foreach ($SyncLog in $SyncLogList)
        {
            Write-Host $SyncLog.TimeStamp : $SyncLog.Details
        }
    }
}
```

## <a name="clean-up-deployment"></a><span data-ttu-id="2d2e3-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-110">Clean up deployment</span></span>

<span data-ttu-id="2d2e3-111">Dopo aver eseguito uno script di esempio hello, è possibile eseguire hello seguente gruppo di risorse di comando tooremove hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-111">After you run hello sample script, you can run hello following command tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2d2e3-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2d2e3-112">Script explanation</span></span>

<span data-ttu-id="2d2e3-113">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-113">This script uses hello following commands.</span></span> <span data-ttu-id="2d2e3-114">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="2d2e3-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="2d2e3-115">Comando</span><span class="sxs-lookup"><span data-stu-id="2d2e3-115">Command</span></span> | <span data-ttu-id="2d2e3-116">Note</span><span class="sxs-lookup"><span data-stu-id="2d2e3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d2e3-117">New-AzureRmSqlSyncAgent</span><span class="sxs-lookup"><span data-stu-id="2d2e3-117">New-AzureRmSqlSyncAgent</span></span>](/powershell/module/azurerm.sql/New-AzureRmSqlSyncAgent) |  <span data-ttu-id="2d2e3-118">Crea un nuovo agente di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-118">Creates a new Sync Agent</span></span> |
| [<span data-ttu-id="2d2e3-119">New-AzureRmSqlSyncAgentKey</span><span class="sxs-lookup"><span data-stu-id="2d2e3-119">New-AzureRmSqlSyncAgentKey</span></span>](/powershell/module/azurerm.sql/New-AzureRmSqlSyncAgentKey) |  <span data-ttu-id="2d2e3-120">Genera chiave agente hello associata con l'agente di sincronizzazione hello</span><span class="sxs-lookup"><span data-stu-id="2d2e3-120">Generates hello agent key associated with hello Sync agent</span></span> |
| [<span data-ttu-id="2d2e3-121">Get-AzureRmSqlSyncAgentLinkedDatabase</span><span class="sxs-lookup"><span data-stu-id="2d2e3-121">Get-AzureRmSqlSyncAgentLinkedDatabase</span></span>](/powershell/module/azurerm.sql/Get-AzureRmSqlSyncAgentLinkedDatabase) |  <span data-ttu-id="2d2e3-122">Ottenere tutte le informazioni di hello per hello agente di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-122">Get all hello information for hello Sync Agent</span></span> |
| [<span data-ttu-id="2d2e3-123">New-AzureRmSqlSyncMember</span><span class="sxs-lookup"><span data-stu-id="2d2e3-123">New-AzureRmSqlSyncMember</span></span>](/powershell/module/azurerm.sql/New-AzureRmSqlSyncMember) |  <span data-ttu-id="2d2e3-124">Aggiungere un nuovo toohello membro gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-124">Add a new member toohello Sync Group</span></span> |
| [<span data-ttu-id="2d2e3-125">Update-AzureRmSqlSyncSchema</span><span class="sxs-lookup"><span data-stu-id="2d2e3-125">Update-AzureRmSqlSyncSchema</span></span>](/powershell/module/azurerm.sql/Update-AzureRmSqlSyncSchema) |  <span data-ttu-id="2d2e3-126">Aggiorna le informazioni sullo schema di database hello</span><span class="sxs-lookup"><span data-stu-id="2d2e3-126">Refreshes hello database schema information</span></span> |
| [<span data-ttu-id="2d2e3-127">Get-AzureRmSqlSyncSchema</span><span class="sxs-lookup"><span data-stu-id="2d2e3-127">Get-AzureRmSqlSyncSchema</span></span>](/powershell/module/azurerm.sql/Get-AzureRmSqlSyncSchem) |  <span data-ttu-id="2d2e3-128">Ottenere informazioni dello schema di database hello</span><span class="sxs-lookup"><span data-stu-id="2d2e3-128">Get hello database schema information</span></span> |
| [<span data-ttu-id="2d2e3-129">Update-AzureRmSqlSyncGroup</span><span class="sxs-lookup"><span data-stu-id="2d2e3-129">Update-AzureRmSqlSyncGroup</span></span>](/powershell/module/azurerm.sql/Update-AzureRmSqlSyncGroup) |  <span data-ttu-id="2d2e3-130">Gli aggiornamenti hello gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-130">Updates hello Sync Group</span></span> |
| [<span data-ttu-id="2d2e3-131">Start-AzureRmSqlSyncGroupSync</span><span class="sxs-lookup"><span data-stu-id="2d2e3-131">Start-AzureRmSqlSyncGroupSync</span></span>](/powershell/module/azurerm.sql/Start-AzureRmSqlSyncGroupSync) | <span data-ttu-id="2d2e3-132">Attiva una sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-132">Triggers a Sync</span></span> |
| [<span data-ttu-id="2d2e3-133">Get-AzureRmSqlSyncGroupLog</span><span class="sxs-lookup"><span data-stu-id="2d2e3-133">Get-AzureRmSqlSyncGroupLog</span></span>](/powershell/module/azurerm.sql/Get-AzureRmSqlSyncGroupLog) |  <span data-ttu-id="2d2e3-134">Controlla hello Log di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2d2e3-134">Checks hello Sync Log</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2d2e3-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d2e3-135">Next steps</span></span>

<span data-ttu-id="2d2e3-136">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d2e3-136">For more information about Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2d2e3-137">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e3-137">Additional SQL Database PowerShell script samples can be found in [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
