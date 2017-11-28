---
title: esempi di avvio rapido aaaAzure monitoraggio CLI 1.0. | Microsoft Docs
description: "Comandi dell'interfaccia della riga di comando 1.0 di esempio per le funzionalità di Monitoraggio di Azure. Monitoraggio di Azure è un servizio di Microsoft Azure che consente le notifiche di avviso toosend, gli URL web di chiamata in base ai valori di dati di telemetria configurati e servizi Cloud di scalabilità automatica, macchine virtuali e le applicazioni Web."
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
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="0d51b-105">Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma 1.0 per Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="0d51b-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="0d51b-106">In questo articolo viene indicato il campionamento toohelp comandi dell'interfaccia della riga di comando (CLI) accedere alle funzionalità di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d51b-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="0d51b-107">Monitoraggio di Azure consente tooAutoScale servizi Cloud, macchine virtuali e le applicazioni Web e toosend notifiche di avviso o URL web chiamata in base ai valori dei dati di telemetria configurato.</span><span class="sxs-lookup"><span data-stu-id="0d51b-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="0d51b-108">Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016.</span><span class="sxs-lookup"><span data-stu-id="0d51b-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="0d51b-109">Tuttavia, gli spazi dei nomi hello e pertanto comandi hello seguenti comunque contengono approfondite"hello".</span><span class="sxs-lookup"><span data-stu-id="0d51b-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0d51b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d51b-110">Prerequisites</span></span>
<span data-ttu-id="0d51b-111">Se non è ancora installato hello CLI di Azure, vedere [installazione hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0d51b-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="0d51b-112">Se non si ha familiarità con l'interfaccia CLI di Azure, è possibile leggere altre informazioni, vedere [hello utilizzare CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0d51b-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="0d51b-113">In Windows, installare npm da hello [sito Web Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="0d51b-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="0d51b-114">Dopo aver completato l'installazione di hello, di CMD.exe con privilegi di Esegui come amministratore, eseguire l'esempio hello dalla cartella hello in cui è installato npm:</span><span class="sxs-lookup"><span data-stu-id="0d51b-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="0d51b-115">Passare tooany/percorso della cartella desiderata e hello della riga di comando digitare:</span><span class="sxs-lookup"><span data-stu-id="0d51b-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="0d51b-116">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="0d51b-116">Log in tooAzure</span></span>
<span data-ttu-id="0d51b-117">primo passaggio Hello è toologin tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="0d51b-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="0d51b-118">Dopo aver eseguito questo comando, si disporrà toosign tramite istruzioni hello nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="0d51b-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="0d51b-119">Vengono quindi visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito. Tutti i comandi di lavoro nel contesto di hello della sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0d51b-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="0d51b-120">dettagli di hello toolist della sottoscrizione corrente, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0d51b-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="0d51b-121">toochange lavoro contesto tooa sottoscrizione diversa, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0d51b-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="0d51b-122">i comandi toouse Azure Resource Manager e il monitoraggio di Azure, è necessario toobe in modalità Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d51b-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="0d51b-123">tooview un elenco di tutti i comandi di monitoraggio di Azure supportati, eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="0d51b-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="0d51b-124">Visualizzare il registro attività di una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="0d51b-124">View activity log for a subscription</span></span>
<span data-ttu-id="0d51b-125">tooview un elenco di attività del log eventi, eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="0d51b-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="0d51b-126">Provare hello seguente tooview tutte le opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="0d51b-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="0d51b-127">Di seguito è riportato un esempio registri toolist da un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d51b-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="0d51b-128">Log di esempio toolist dal chiamante</span><span class="sxs-lookup"><span data-stu-id="0d51b-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="0d51b-129">Log di esempio toolist chiamante in un tipo di risorsa, all'interno di una data di inizio e fine</span><span class="sxs-lookup"><span data-stu-id="0d51b-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="0d51b-130">Usare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="0d51b-130">Work with alerts</span></span>
<span data-ttu-id="0d51b-131">È possibile utilizzare le informazioni di hello in hello sezione toowork con avvisi.</span><span class="sxs-lookup"><span data-stu-id="0d51b-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="0d51b-132">Ottenere regole di avviso in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d51b-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="0d51b-133">Creare una regola di avviso metrica</span><span class="sxs-lookup"><span data-stu-id="0d51b-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="0d51b-134">Creare una regola di avviso test Web</span><span class="sxs-lookup"><span data-stu-id="0d51b-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="0d51b-135">Eliminare una regola di avviso</span><span class="sxs-lookup"><span data-stu-id="0d51b-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="0d51b-136">Profili dei log</span><span class="sxs-lookup"><span data-stu-id="0d51b-136">Log profiles</span></span>
<span data-ttu-id="0d51b-137">Utilizzare informazioni hello toowork questa sezione con i profili di log.</span><span class="sxs-lookup"><span data-stu-id="0d51b-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="0d51b-138">Acquisizione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="0d51b-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="0d51b-139">Aggiungere un profilo di log senza conservazione</span><span class="sxs-lookup"><span data-stu-id="0d51b-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="0d51b-140">Rimozione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="0d51b-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="0d51b-141">Aggiungere un profilo di log con conservazione</span><span class="sxs-lookup"><span data-stu-id="0d51b-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="0d51b-142">Aggiungere un profilo di log con conservazione e hub eventi</span><span class="sxs-lookup"><span data-stu-id="0d51b-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="0d51b-143">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="0d51b-143">Diagnostics</span></span>
<span data-ttu-id="0d51b-144">Utilizzare informazioni hello toowork questa sezione con le impostazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0d51b-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="0d51b-145">Ottenere un'impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="0d51b-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="0d51b-146">Disabilitare un'impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="0d51b-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="0d51b-147">Abilitare un'impostazione di diagnostica senza conservazione</span><span class="sxs-lookup"><span data-stu-id="0d51b-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="0d51b-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="0d51b-148">Autoscale</span></span>
<span data-ttu-id="0d51b-149">Utilizzare informazioni hello toowork questa sezione con le impostazioni di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="0d51b-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="0d51b-150">È necessario toomodify questi esempi.</span><span class="sxs-lookup"><span data-stu-id="0d51b-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="0d51b-151">Ottenere le impostazioni di scalabilità automatica per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d51b-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="0d51b-152">Ottenere le impostazioni di scalabilità automatica per nome in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d51b-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="0d51b-153">Configurare le impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="0d51b-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
