---
title: Esempi di avvio rapido dell'interfaccia della riga di comando 1.0 per Monitoraggio di Azure. | Documentazione Microsoft
description: "Comandi dell'interfaccia della riga di comando 1.0 di esempio per le funzionalità di Monitoraggio di Azure. Monitoraggio di Azure è un servizio di Microsoft Azure che permette di inviare notifiche di avviso, chiamare URL Web in base ai valori dei dati di telemetria configurati e ridimensionare automaticamente servizi cloud, macchine virtuali e app Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="5897f-105">Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma 1.0 per Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="5897f-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="5897f-106">Questo articolo illustra i comandi dell'interfaccia della riga di comando di esempio per accedere alle funzionalità di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="5897f-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="5897f-107">Monitoraggio di Azure consente di ridimensionare automaticamente servizi cloud, macchine virtuali e app Web e di inviare notifiche di avviso o chiamare URL Web in base ai valori dei dati di telemetria configurati.</span><span class="sxs-lookup"><span data-stu-id="5897f-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="5897f-108">Dal 25 settembre 2016 Monitoraggio di Azure è il nuovo nome di "Azure Insights".</span><span class="sxs-lookup"><span data-stu-id="5897f-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="5897f-109">Tuttavia, gli spazi dei nomi e quindi i comandi seguenti contengono ancora il termine "insights".</span><span class="sxs-lookup"><span data-stu-id="5897f-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5897f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5897f-110">Prerequisites</span></span>
<span data-ttu-id="5897f-111">Se l'interfaccia della riga di comando di Azure non è stata ancora installata, vedere [Installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5897f-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="5897f-112">Se non si ha familiarità con l'interfaccia della riga di comando di Azure, è possibile trovare altre informazioni nell'articolo [Usare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5897f-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="5897f-113">In Windows installare npm dal [sito Web Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="5897f-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="5897f-114">Dopo avere completato l'installazione, usando CMD.exe con i privilegi Esegui come amministratore, eseguire quanto segue dalla cartella di installazione di npm:</span><span class="sxs-lookup"><span data-stu-id="5897f-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="5897f-115">Passare quindi alla cartella o al percorso preferito e digitare nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="5897f-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="5897f-116">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="5897f-116">Log in to Azure</span></span>
<span data-ttu-id="5897f-117">Il primo passaggio prevede l'accesso all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="5897f-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="5897f-118">Dopo aver eseguito questo comando, è necessario eseguire l'accesso tramite le istruzioni visualizzate sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="5897f-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="5897f-119">Vengono quindi visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito. Tutti i comandi operano nel contesto della sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5897f-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="5897f-120">Per elencare i dettagli della sottoscrizione corrente, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5897f-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="5897f-121">Per modificare il contesto di lavoro in una sottoscrizione diversa, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5897f-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="5897f-122">Per usare i comandi di Azure Resource Manager e di Monitoraggio di Azure, è necessario essere in modalità Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5897f-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="5897f-123">Per visualizzare un elenco di tutti i comandi di Monitoraggio di Azure supportati, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5897f-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="5897f-124">Visualizzare il registro attività di una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5897f-124">View activity log for a subscription</span></span>
<span data-ttu-id="5897f-125">Per visualizzare un elenco degli eventi del registro attività, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="5897f-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="5897f-126">Per visualizzare tutte le opzioni disponibili, provare a eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="5897f-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="5897f-127">Ecco un esempio per elencare i log in base a resourceGroup</span><span class="sxs-lookup"><span data-stu-id="5897f-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="5897f-128">Esempio per elencare i log in base al chiamante</span><span class="sxs-lookup"><span data-stu-id="5897f-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="5897f-129">Esempio per elencare i log in base al chiamante in un tipo di risorsa, compresi tra una data di inizio e una di fine</span><span class="sxs-lookup"><span data-stu-id="5897f-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="5897f-130">Usare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="5897f-130">Work with alerts</span></span>
<span data-ttu-id="5897f-131">È possibile usare le informazioni della sezione per lavorare con gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5897f-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="5897f-132">Ottenere regole di avviso in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5897f-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="5897f-133">Creare una regola di avviso metrica</span><span class="sxs-lookup"><span data-stu-id="5897f-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="5897f-134">Creare una regola di avviso test Web</span><span class="sxs-lookup"><span data-stu-id="5897f-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="5897f-135">Eliminare una regola di avviso</span><span class="sxs-lookup"><span data-stu-id="5897f-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="5897f-136">Profili dei log</span><span class="sxs-lookup"><span data-stu-id="5897f-136">Log profiles</span></span>
<span data-ttu-id="5897f-137">Usare le informazioni di questa sezione per lavorare con i profili dei log.</span><span class="sxs-lookup"><span data-stu-id="5897f-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="5897f-138">Acquisizione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="5897f-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="5897f-139">Aggiungere un profilo di log senza conservazione</span><span class="sxs-lookup"><span data-stu-id="5897f-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="5897f-140">Rimozione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="5897f-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="5897f-141">Aggiungere un profilo di log con conservazione</span><span class="sxs-lookup"><span data-stu-id="5897f-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="5897f-142">Aggiungere un profilo di log con conservazione e hub eventi</span><span class="sxs-lookup"><span data-stu-id="5897f-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="5897f-143">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="5897f-143">Diagnostics</span></span>
<span data-ttu-id="5897f-144">Usare le informazioni di questa sezione per lavorare con le impostazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="5897f-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="5897f-145">Ottenere un'impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="5897f-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="5897f-146">Disabilitare un'impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="5897f-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="5897f-147">Abilitare un'impostazione di diagnostica senza conservazione</span><span class="sxs-lookup"><span data-stu-id="5897f-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="5897f-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="5897f-148">Autoscale</span></span>
<span data-ttu-id="5897f-149">Usare le informazioni di questa sezione per lavorare con le impostazioni di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="5897f-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="5897f-150">È necessario modificare questi esempi.</span><span class="sxs-lookup"><span data-stu-id="5897f-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="5897f-151">Ottenere le impostazioni di scalabilità automatica per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5897f-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="5897f-152">Ottenere le impostazioni di scalabilità automatica per nome in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5897f-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="5897f-153">Configurare le impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="5897f-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
