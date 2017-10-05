---
title: Accedere ad applicazioni Service Fabric con Log Analytics di Azure mediante PowerShell | Microsoft Docs
description: "È possibile usare la soluzione Service Fabric in Log Analytics mediante PowerShell per valutare i rischi e l'integrità delle applicazioni Service Fabric, dei microservizi, dei nodi e dei cluster."
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="75cd6-103">Valutare le applicazioni e i microservizi di Azure Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="75cd6-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75cd6-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="75cd6-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="75cd6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75cd6-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Simbolo di Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="75cd6-107">In questo articolo viene descritto come usare la soluzione Service Fabric in Log Analytics per identificare e risolvere i problemi nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="75cd6-108">Consente di vedere come si comportano i nodi di Service Fabric e come si eseguono le applicazioni e i microservizi.</span><span class="sxs-lookup"><span data-stu-id="75cd6-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="75cd6-109">La soluzione Service Fabric usa i dati della Diagnostica di Azure provenienti dalle macchine virtuali Service Fabric, raccogliendo questi dati dalle tabelle di Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="75cd6-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="75cd6-110">Log Analytics legge quindi gli eventi seguenti del framework di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="75cd6-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="75cd6-111">**Eventi di Reliable Services**</span><span class="sxs-lookup"><span data-stu-id="75cd6-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="75cd6-112">**Eventi relativi agli attori**</span><span class="sxs-lookup"><span data-stu-id="75cd6-112">**Actor Events**</span></span>
- <span data-ttu-id="75cd6-113">**Eventi operativi**</span><span class="sxs-lookup"><span data-stu-id="75cd6-113">**Operational Events**</span></span>
- <span data-ttu-id="75cd6-114">**Eventi ETW personalizzati**</span><span class="sxs-lookup"><span data-stu-id="75cd6-114">**Custom ETW events**</span></span>

<span data-ttu-id="75cd6-115">Il dashboard della soluzione Service Fabric mostra i problemi degni di nota e gli eventi rilevanti nell'ambiente Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="75cd6-116">Installazione e configurazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="75cd6-116">Installing and configuring the solution</span></span>
<span data-ttu-id="75cd6-117">Seguire questi tre semplici passaggi per installare e configurare la soluzione:</span><span class="sxs-lookup"><span data-stu-id="75cd6-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="75cd6-118">Associare la sottoscrizione di Azure usata per creare tutte le risorse del cluster, inclusi gli account di archiviazione, all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="75cd6-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="75cd6-119">Vedere [Introduzione a Log Analytics](log-analytics-get-started.md) per informazioni sulla creazione di un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="75cd6-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="75cd6-120">Configurare Log Analytics per raccogliere e visualizzare i log di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="75cd6-121">Abilitare la soluzione Service Fabric nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="75cd6-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="75cd6-122">Configurare Log Analytics per raccogliere e visualizzare i log di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="75cd6-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="75cd6-123">Questa sezione illustra come configurare Log Analytics per recuperare i log di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="75cd6-124">I log consentono di visualizzare, analizzare e risolvere i problemi nel cluster o nelle applicazioni e nei servizi in esecuzione nel cluster usando il portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="75cd6-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="75cd6-125">Configurare l'estensione di Diagnostica di Azure per caricare i log per le tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="75cd6-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="75cd6-126">Le tabelle devono corrispondere a quanto Log Analytics sta cercando.</span><span class="sxs-lookup"><span data-stu-id="75cd6-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="75cd6-127">Per altre informazioni, vedere [Raccogliere log con Diagnostica di Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="75cd6-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="75cd6-128">Gli esempi di impostazioni di configurazione disponibili in questo articolo indicano i nomi ottimali per le tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="75cd6-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="75cd6-129">Dopo avere configurato la Diagnostica nel cluster e avere avviato il caricamento dei log in un account di archiviazione, il passaggio successivo consiste nel configurare Log Analytics per raccogliere questi log.</span><span class="sxs-lookup"><span data-stu-id="75cd6-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="75cd6-130">Assicurarsi di aggiornare la sezione**EtwEventSourceProviderConfiguration** nel file **template.json** per aggiungere le voci relative al nuovo canale EventSources prima di applicare l'aggiornamento della configurazione eseguendo **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="75cd6-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="75cd6-131">La tabella per il caricamento è identica a (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="75cd6-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="75cd6-132">Log Analytics al momento può leggere solo gli eventi ETW dell'applicazione dalla tabella *WADETWEventTable*.</span><span class="sxs-lookup"><span data-stu-id="75cd6-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="75cd6-133">I seguenti strumenti vengono usati per eseguire alcune delle operazioni descritte in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="75cd6-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="75cd6-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="75cd6-134">Azure PowerShell</span></span>
* [<span data-ttu-id="75cd6-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="75cd6-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="75cd6-136">Configurare un'area di lavoro di Log Analytics per visualizzare i log dei cluster</span><span class="sxs-lookup"><span data-stu-id="75cd6-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="75cd6-137">Dopo aver creato un'area di lavoro di Log Analytics, configurare l'area di lavoro per eseguire il pull dei log dalle tabelle di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75cd6-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="75cd6-138">Quindi eseguire lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="75cd6-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="75cd6-139">Dopo avere configurato l'area di lavoro di Log Analytics per la lettura dalle tabelle di Azure nell'account di archiviazione, accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="75cd6-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="75cd6-140">Selezionare l'area di lavoro di Log Analytics da **Tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="75cd6-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="75cd6-141">Viene visualizzato il numero di log dell'account di archiviazione connesso all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="75cd6-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="75cd6-142">Selezionare il riquadro **Log account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="75cd6-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="75cd6-143">Esaminare l'elenco dei log dell'account di archiviazione per verificare che l'account di archiviazione sia connesso all'area di lavoro corretta.</span><span class="sxs-lookup"><span data-stu-id="75cd6-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Log dell'account di archiviazione](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="75cd6-145">Abilitare la soluzione Service Fabric</span><span class="sxs-lookup"><span data-stu-id="75cd6-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="75cd6-146">Usare lo script seguente per aggiungere la soluzione all'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="75cd6-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="75cd6-147">Eseguire lo script in PowerShell, usando la sottoscrizione di Azure associata all'area di lavoro di Log Analytics in cui si vuole abilitare la soluzione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="75cd6-148">Dopo aver abilitato la soluzione, il riquadro di Service Fabric viene aggiunto alla pagina di Log Analytics *Panoramica*.</span><span class="sxs-lookup"><span data-stu-id="75cd6-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="75cd6-149">La pagina mostra una visualizzazione dei problemi rilevanti, ad esempio gli errori di runAsync e gli annullamenti che si sono verificati nelle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="75cd6-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Riquadro Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="75cd6-151">Visualizzare gli eventi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="75cd6-151">View Service Fabric events</span></span>
<span data-ttu-id="75cd6-152">Fare clic sul riquadro **Service Fabric** per aprire il dashboard di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="75cd6-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="75cd6-153">Il dashboard include le colonne nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="75cd6-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="75cd6-154">Ogni colonna elenca i primi dieci eventi per numero corrispondente ai criteri della colonna per l'intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="75cd6-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="75cd6-155">È possibile eseguire una ricerca di log che fornisce l'intero elenco facendo clic su **Visualizza tutto** nella parte inferiore destra di ciascuna colonna o facendo clic sull'intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="75cd6-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="75cd6-156">**Evento di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="75cd6-156">**Service Fabric event**</span></span> | <span data-ttu-id="75cd6-157">**description**</span><span class="sxs-lookup"><span data-stu-id="75cd6-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="75cd6-158">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="75cd6-158">Notable Issues</span></span> | <span data-ttu-id="75cd6-159">Visualizza i problemi, compresi RunAsyncFailures, RunAsynCancellations e Node Downs.</span><span class="sxs-lookup"><span data-stu-id="75cd6-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="75cd6-160">Eventi operativi</span><span class="sxs-lookup"><span data-stu-id="75cd6-160">Operational Events</span></span> | <span data-ttu-id="75cd6-161">Visualizza gli eventi operativi rilevanti, compresi l'aggiornamento dell'applicazione e le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="75cd6-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="75cd6-162">Eventi del servizio affidabile</span><span class="sxs-lookup"><span data-stu-id="75cd6-162">Reliable Service Events</span></span> | <span data-ttu-id="75cd6-163">Visualizza gli eventi di Reliable Services rilevanti, compreso Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="75cd6-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="75cd6-164">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="75cd6-164">Actor Events</span></span> | <span data-ttu-id="75cd6-165">Visualizza gli eventi rilevanti relativi agli attori generati dai microservizi.</span><span class="sxs-lookup"><span data-stu-id="75cd6-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="75cd6-166">Gli eventi includono le eccezioni generate da un metodo attore, le attivazioni e disattivazioni attore e così via.</span><span class="sxs-lookup"><span data-stu-id="75cd6-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="75cd6-167">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="75cd6-167">Application Events</span></span> | <span data-ttu-id="75cd6-168">Visualizza tutti gli eventi ETW personalizzati che sono stati generati dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="75cd6-168">Displays all custom ETW events generated by your applications.</span></span> |

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="75cd6-171">La tabella seguente illustra i metodi di raccolta dei dati e altri dettagli sulla modalità di raccolta dei dati per Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="75cd6-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="75cd6-172">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="75cd6-172">platform</span></span> | <span data-ttu-id="75cd6-173">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="75cd6-173">Direct Agent</span></span> | <span data-ttu-id="75cd6-174">Agente di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="75cd6-174">Operations Manager agent</span></span> | <span data-ttu-id="75cd6-175">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="75cd6-175">Azure Storage</span></span> | <span data-ttu-id="75cd6-176">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="75cd6-176">Operations Manager required?</span></span> | <span data-ttu-id="75cd6-177">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="75cd6-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="75cd6-178">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="75cd6-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="75cd6-179">Windows</span><span class="sxs-lookup"><span data-stu-id="75cd6-179">Windows</span></span> |  |  | <span data-ttu-id="75cd6-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="75cd6-180">&#8226;</span></span> |  |  |<span data-ttu-id="75cd6-181">10 minuti</span><span class="sxs-lookup"><span data-stu-id="75cd6-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="75cd6-182">Modificare l'ambito degli eventi con i **Dati basati sugli ultimi sette giorni** nella parte superiore del dashboard.</span><span class="sxs-lookup"><span data-stu-id="75cd6-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="75cd6-183">È anche possibile mostrare gli eventi generati negli ultimi sette giorni, nell'ultimo giorno o nelle ultime sei ore.</span><span class="sxs-lookup"><span data-stu-id="75cd6-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="75cd6-184">In alternativa, è possibile selezionare **Personalizzato** e specificare un intervallo di date personalizzato.</span><span class="sxs-lookup"><span data-stu-id="75cd6-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="75cd6-185">Risolvere i problemi di configurazione di Service Fabric e di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="75cd6-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="75cd6-186">Se si deve verificare la configurazione di Log Analytics perché non si riesce a visualizzare i dati degli eventi in Log Analytics, usare lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="75cd6-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="75cd6-187">Esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="75cd6-187">It performs the following actions:</span></span>

1. <span data-ttu-id="75cd6-188">Legge la configurazione della diagnostica di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="75cd6-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="75cd6-189">Verifica la presenza di dati scritti nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="75cd6-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="75cd6-190">Verifica che Log Analytics sia configurato per la lettura dalle tabelle</span><span class="sxs-lookup"><span data-stu-id="75cd6-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="75cd6-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75cd6-191">Next steps</span></span>
* <span data-ttu-id="75cd6-192">Per visualizzare i dati dettagliati sugli eventi Service Fabric usare [Ricerche log in Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="75cd6-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
