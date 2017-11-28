---
title: applicazioni di Service Fabric con Analitica di Log di Azure con PowerShell aaaAssess | Documenti Microsoft
description: "È possibile utilizzare soluzioni di Service Fabric hello in Analitica Log usando PowerShell tooassess hello rischio e l'integrità delle applicazioni di Service Fabric, micro servizi, nodi e i cluster."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="6bbe4-103">Valutare le applicazioni e i microservizi di Azure Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bbe4-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bbe4-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="6bbe4-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="6bbe4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bbe4-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Simbolo di Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="6bbe4-107">In questo articolo viene descritto come toouse hello soluzione Service Fabric in Log Analitica toohelp identificare e risolvere i problemi del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="6bbe4-108">Consente di vedere come si comportano i nodi di Service Fabric e come si eseguono le applicazioni e i microservizi.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="6bbe4-109">Hello soluzione Service Fabric utilizza i dati di diagnostica di Azure delle macchine virtuali dell'infrastruttura di servizio, raccogliendo i dati dalle tabelle di Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="6bbe4-110">Log Analitica legge quindi hello dopo gli eventi di Service Fabric framework:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="6bbe4-111">**Eventi di Reliable Services**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="6bbe4-112">**Eventi relativi agli attori**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-112">**Actor Events**</span></span>
- <span data-ttu-id="6bbe4-113">**Eventi operativi**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-113">**Operational Events**</span></span>
- <span data-ttu-id="6bbe4-114">**Eventi ETW personalizzati**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-114">**Custom ETW events**</span></span>

<span data-ttu-id="6bbe4-115">dashboard di soluzione di Service Fabric Hello Mostra problemi rilevanti e degli eventi di Service Fabric nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="6bbe4-116">Installazione e configurazione di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="6bbe4-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="6bbe4-117">Seguire questi tooinstall tre semplici passaggi e configurare la soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="6bbe4-118">Associare hello sottoscrizione di Azure usata toocreate tutte le risorse cluster, inclusi gli account di archiviazione, con l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="6bbe4-119">Vedere [Introduzione a Log Analytics](log-analytics-get-started.md) per informazioni sulla creazione di un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="6bbe4-120">Configurare toocollect Log Analitica e visualizzare i log di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="6bbe4-121">Abilitare soluzioni di Service Fabric hello nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="6bbe4-122">Configurare toocollect Log Analitica e visualizzare i log di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bbe4-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="6bbe4-123">In questa sezione viene illustrato modalità di registrazione tooconfigure Log Analitica tooretrieve Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="6bbe4-124">Hello log consentono di tooview, analizzare e risolvere i problemi del cluster o in applicazioni hello e servizi in esecuzione in tale cluster, tramite il portale di OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbe4-125">Configurare hello Azure estensione tooupload hello i log di diagnostica per le tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="6bbe4-126">tabelle Hello devono corrispondere a ciò che cerca Analitica Log.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="6bbe4-127">Per ulteriori informazioni, vedere [modalità di registrazione con diagnostica Azure toocollect](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="6bbe4-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="6bbe4-128">esempi di impostazioni di configurazione di Hello in questo articolo si mostrano i nomi di hello di archiviazione hello tabelle devono essere.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="6bbe4-129">Dopo diagnostica è configurata nel cluster hello ed è il caricamento di account di archiviazione di registri tooa hello è tooconfigure Log Analitica toocollect questi registri.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="6bbe4-130">Assicurarsi di aggiornare hello **EtwEventSourceProviderConfiguration** sezione hello **template.json** tooadd voci per hello EventSources nuovo prima di applicare la configurazione hello aggiornare da file esecuzione **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="6bbe4-131">tabella Hello per il caricamento è hello stesso come (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="6bbe4-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="6bbe4-132">In un momento hello, Log Analitica può solo leggere gli eventi ETW di applicazione hello *WADETWEventTable* tabella.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="6bbe4-133">Hello sono i seguenti strumenti tooperform usate alcune delle operazioni di hello in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="6bbe4-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bbe4-134">Azure PowerShell</span></span>
* [<span data-ttu-id="6bbe4-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6bbe4-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="6bbe4-136">Configurare un log di cluster Analitica di Log dell'area di lavoro tooshow hello</span><span class="sxs-lookup"><span data-stu-id="6bbe4-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="6bbe4-137">Dopo aver creato un'area di lavoro Log Analitica, configurare i registri di hello dell'area di lavoro toopull dalle tabelle di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="6bbe4-138">Eseguire quindi hello lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="6bbe4-139">Dopo aver configurato hello Analitica di Log dell'area di lavoro tooread da hello Azure tabelle nell'account di archiviazione, accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="6bbe4-140">Selezione area di lavoro Log Analitica hello da **tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="6bbe4-141">viene visualizzato il numero di Hello dell'area di lavoro toohello registri connesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="6bbe4-142">Seleziona hello **log dell'account di archiviazione** riquadro.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="6bbe4-143">Elenco di account di archiviazione hello registra tooverify che l'account di archiviazione è connesso toohello corretto dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Log dell'account di archiviazione](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="6bbe4-145">Abilitare soluzioni di Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="6bbe4-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="6bbe4-146">Utilizzare hello seguenti script tooadd hello soluzione tooyour Log Analitica dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="6bbe4-147">Eseguire script hello in PowerShell, con sottoscrizione di Azure associato hello Analitica di Log dell'area di lavoro che si desidera che tooenable hello Service Fabric soluzione in hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="6bbe4-148">Dopo aver abilitato la soluzione hello, riquadro di Service Fabric hello viene aggiunto tooyour Log Analitica *Panoramica* pagina.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="6bbe4-149">pagina Hello Mostra una visualizzazione di problemi quali errori runAsync e annullamenti che si sono verificati in hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Riquadro Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="6bbe4-151">Visualizzare gli eventi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bbe4-151">View Service Fabric events</span></span>
<span data-ttu-id="6bbe4-152">Fare clic su hello **Service Fabric** riquadro tooopen hello Service Fabric dashboard.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="6bbe4-153">dashboard Hello include le colonne di hello tabella hello che segue.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="6bbe4-154">Ogni colonna elenca gli eventi di 10 superiore di hello associando conteggio che i criteri della colonna per hello specificato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="6bbe4-155">È possibile eseguire una ricerca di log che fornisce l'intero elenco hello facendo **tutti** hello in basso a destra di ogni colonna, oppure facendo clic sull'intestazione di colonna hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="6bbe4-156">**Evento di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-156">**Service Fabric event**</span></span> | <span data-ttu-id="6bbe4-157">**description**</span><span class="sxs-lookup"><span data-stu-id="6bbe4-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="6bbe4-158">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="6bbe4-158">Notable Issues</span></span> | <span data-ttu-id="6bbe4-159">Visualizza i problemi, compresi RunAsyncFailures, RunAsynCancellations e Node Downs.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="6bbe4-160">Eventi operativi</span><span class="sxs-lookup"><span data-stu-id="6bbe4-160">Operational Events</span></span> | <span data-ttu-id="6bbe4-161">Visualizza gli eventi operativi rilevanti, compresi l'aggiornamento dell'applicazione e le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="6bbe4-162">Eventi del servizio affidabile</span><span class="sxs-lookup"><span data-stu-id="6bbe4-162">Reliable Service Events</span></span> | <span data-ttu-id="6bbe4-163">Visualizza gli eventi di Reliable Services rilevanti, compreso Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="6bbe4-164">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="6bbe4-164">Actor Events</span></span> | <span data-ttu-id="6bbe4-165">Visualizza gli eventi rilevanti relativi agli attori generati dai microservizi.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="6bbe4-166">Gli eventi includono le eccezioni generate da un metodo attore, le attivazioni e disattivazioni attore e così via.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="6bbe4-167">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6bbe4-167">Application Events</span></span> | <span data-ttu-id="6bbe4-168">Visualizza tutti gli eventi ETW personalizzati che sono stati generati dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-168">Displays all custom ETW events generated by your applications.</span></span> |

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="6bbe4-171">Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per l'infrastruttura del servizio:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="6bbe4-172">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="6bbe4-172">platform</span></span> | <span data-ttu-id="6bbe4-173">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="6bbe4-173">Direct Agent</span></span> | <span data-ttu-id="6bbe4-174">Agente di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="6bbe4-174">Operations Manager agent</span></span> | <span data-ttu-id="6bbe4-175">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6bbe4-175">Azure Storage</span></span> | <span data-ttu-id="6bbe4-176">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="6bbe4-176">Operations Manager required?</span></span> | <span data-ttu-id="6bbe4-177">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="6bbe4-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="6bbe4-178">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="6bbe4-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6bbe4-179">Windows</span><span class="sxs-lookup"><span data-stu-id="6bbe4-179">Windows</span></span> |  |  | <span data-ttu-id="6bbe4-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6bbe4-180">&#8226;</span></span> |  |  |<span data-ttu-id="6bbe4-181">10 minuti</span><span class="sxs-lookup"><span data-stu-id="6bbe4-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="6bbe4-182">Modificare l'ambito di hello degli eventi con **i dati basati su negli ultimi sette giorni** nella parte superiore di hello del dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="6bbe4-183">È inoltre possibile visualizzare gli eventi generati all'interno di hello ultimi sette giorni, un giorno o sei ore.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="6bbe4-184">In alternativa, è possibile selezionare **personalizzato** toospecify un intervallo di date personalizzato.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="6bbe4-185">Risolvere i problemi di configurazione di Service Fabric e di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6bbe4-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="6bbe4-186">Se è necessario tooverify la configurazione di Log Analitica perché si dispone di dati dell'evento nel registro Analitica tooview non è possibile, utilizzare lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="6bbe4-187">Lo strumento esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="6bbe4-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="6bbe4-188">Legge la configurazione della diagnostica di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bbe4-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="6bbe4-189">Controlli per i dati scritti in tabelle hello</span><span class="sxs-lookup"><span data-stu-id="6bbe4-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="6bbe4-190">Verifica che Analitica Log sia configurato tooread dalle tabelle hello</span><span class="sxs-lookup"><span data-stu-id="6bbe4-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="6bbe4-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bbe4-191">Next steps</span></span>
* <span data-ttu-id="6bbe4-192">Utilizzare [ricerche nei Log nel Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di evento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6bbe4-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
