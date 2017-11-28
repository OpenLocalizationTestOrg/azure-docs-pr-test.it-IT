---
title: macchine virtuali Linux di aaaMonitor in Azure | Documenti Microsoft
description: Informazioni su come toomonitor avvio metriche delle prestazioni e diagnostica in una macchina virtuale di Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="abde6-103">Come toomonitor una macchina virtuale di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="abde6-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="abde6-104">tooensure che eseguono correttamente le macchine virtuali (VM) in Azure, è possibile esaminare le metriche delle prestazioni e diagnostica di avvio.</span><span class="sxs-lookup"><span data-stu-id="abde6-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="abde6-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="abde6-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abde6-106">Abilitare la diagnostica di avvio su hello VM</span><span class="sxs-lookup"><span data-stu-id="abde6-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="abde6-107">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="abde6-107">View boot diagnostics</span></span>
> * <span data-ttu-id="abde6-108">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="abde6-108">View host metrics</span></span>
> * <span data-ttu-id="abde6-109">Abilitare l'estensione di diagnostica per hello VM</span><span class="sxs-lookup"><span data-stu-id="abde6-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="abde6-110">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abde6-110">View VM metrics</span></span>
> * <span data-ttu-id="abde6-111">Creare avvisi basati sulle metriche di diagnostica</span><span class="sxs-lookup"><span data-stu-id="abde6-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="abde6-112">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="abde6-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="abde6-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="abde6-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="abde6-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="abde6-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="abde6-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="abde6-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="abde6-116">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abde6-116">Create VM</span></span>

<span data-ttu-id="abde6-117">diagnostica toosee e metriche in azione, è necessario una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="abde6-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="abde6-118">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="abde6-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="abde6-119">esempio Hello crea un gruppo di risorse denominato *myResourceGroupMonitor* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="abde6-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="abde6-120">Creare quindi una macchina virtuale con il comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="abde6-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="abde6-121">esempio Hello crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="abde6-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="abde6-122">Abilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="abde6-122">Enable boot diagnostics</span></span>

<span data-ttu-id="abde6-123">Come avviare le macchine virtuali Linux, estensione di diagnostica di avvio hello acquisisce l'output di avvio e lo archivia nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="abde6-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="abde6-124">Questi dati possono essere utilizzati tootroubleshoot problemi di avvio VM.</span><span class="sxs-lookup"><span data-stu-id="abde6-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="abde6-125">Diagnostica di avvio non è abilitata automaticamente quando si crea una VM Linux di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="abde6-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="abde6-126">Prima di abilitare la diagnostica di avvio, un account di archiviazione deve toobe creato per l'archiviazione dei log di avvio.</span><span class="sxs-lookup"><span data-stu-id="abde6-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="abde6-127">Gli account di archiviazione devono avere un nome univoco globale, che abbia tra i 3 e i 24 caratteri e devono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="abde6-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="abde6-128">Creare un account di archiviazione con hello [creare account di archiviazione az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="abde6-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="abde6-129">In questo esempio, una stringa casuale è toocreate utilizzati un nome di account di archiviazione univoco.</span><span class="sxs-lookup"><span data-stu-id="abde6-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="abde6-130">Quando si abilita la diagnostica di avvio, è necessario contenitore di archiviazione blob toohello hello URI.</span><span class="sxs-lookup"><span data-stu-id="abde6-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="abde6-131">Hello seguenti query di comando hello tooreturn account di archiviazione questo URI.</span><span class="sxs-lookup"><span data-stu-id="abde6-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="abde6-132">valore dell'URI Hello viene archiviato nei nomi di variabili *bloburi*, che viene utilizzato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="abde6-133">Abilitare ora la diagnostica di avvio con [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="abde6-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="abde6-134">Hello `--storage` valore è il blob hello URI raccolti nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="abde6-135">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="abde6-135">View boot diagnostics</span></span>

<span data-ttu-id="abde6-136">Quando è abilitata la diagnostica di avvio, ogni volta che si arresta e avvia hello VM, informazioni sul processo di avvio hello viene scritto il file di log tooa.</span><span class="sxs-lookup"><span data-stu-id="abde6-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="abde6-137">Per questo esempio, prima deallocare hello VM con hello [az vm deallocare](/cli/azure/vm#deallocate) comando come segue:</span><span class="sxs-lookup"><span data-stu-id="abde6-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="abde6-138">Ora avviare hello VM con hello [inizio vm az]( /cli/azure/vm#stop) comando come segue:</span><span class="sxs-lookup"><span data-stu-id="abde6-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="abde6-139">È possibile ottenere dati di diagnostica di avvio hello per *myVM* con hello [az vm get diagnostica di avvio-avvio-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando come segue:</span><span class="sxs-lookup"><span data-stu-id="abde6-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="abde6-140">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="abde6-140">View host metrics</span></span>

<span data-ttu-id="abde6-141">Una macchina virtuale Linux è un host dedicato in Azure con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="abde6-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="abde6-142">Le metriche vengono automaticamente raccolte per host hello e possono essere visualizzate nel portale di Azure hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="abde6-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="abde6-143">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroupMonitor**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="abde6-144">toosee come macchina virtuale host hello viene eseguita, fare clic su **metriche** nel pannello VM hello, quindi selezionare una qualsiasi delle hello *[Host]* metriche in **le metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="abde6-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="abde6-146">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="abde6-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abde6-147">Questo documento descrive versione 2.3 di hello estensione diagnostica per Linux, che è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="abde6-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="abde6-148">La versione 2.3 sarà supportata fino al 30 giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="abde6-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="abde6-149">Versione 3.0 di hello che estensione diagnostica per Linux può invece essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="abde6-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="abde6-150">Per ulteriori informazioni, vedere [hello documentazione](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="abde6-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="abde6-151">le metriche di base host Hello sono disponibili, ma toosee più granulare e metriche specifiche di macchina virtuale, si tooneed tooinstall hello Azure estensione diagnostica per hello VM.</span><span class="sxs-lookup"><span data-stu-id="abde6-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="abde6-152">Hello estensione diagnostica di Azure consente un monitoraggio aggiuntivo e toobe di dati di diagnostica recuperati hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="abde6-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="abde6-153">È possibile visualizzare queste misurazioni delle prestazioni e creare avvisi basati sulle modalità di funzionamento hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="abde6-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="abde6-154">estensione di diagnostica Hello viene installata tramite il portale di Azure hello come segue:</span><span class="sxs-lookup"><span data-stu-id="abde6-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="abde6-155">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="abde6-156">Fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="abde6-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="abde6-157">elenco di Hello mostra che *diagnostica di avvio* è già stata abilitata dalla sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="abde6-158">Fare clic sulla casella di controllo hello *metriche base*.</span><span class="sxs-lookup"><span data-stu-id="abde6-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="abde6-159">In hello *account di archiviazione* sezione, passare hello selezionare tooand *mydiagdata [1234]* account creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="abde6-160">Fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="abde6-160">Click hello **Save** button.</span></span>

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="abde6-162">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abde6-162">View VM metrics</span></span>

<span data-ttu-id="abde6-163">È possibile visualizzare le metriche VM hello in hello allo stesso modo visualizzato metriche di hello host macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="abde6-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="abde6-164">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="abde6-165">toosee come hello macchina virtuale viene eseguita, fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche di diagnostica hello in **le metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="abde6-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="abde6-167">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="abde6-167">Create alerts</span></span>

<span data-ttu-id="abde6-168">È possibile creare avvisi basati sulle metriche di prestazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="abde6-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="abde6-169">Gli avvisi possono essere ad esempio toonotify utilizzato per l'utilizzo medio della CPU supera una determinata soglia o spazio su disco disponibile scende di sotto di una certa quantità.</span><span class="sxs-lookup"><span data-stu-id="abde6-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="abde6-170">Gli avvisi vengono visualizzati nel portale di Azure hello o possono essere inviati tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="abde6-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="abde6-171">È inoltre possibile attivare i runbook di automazione di Azure o Azure logica App in tooalerts risposta in corso la generazione.</span><span class="sxs-lookup"><span data-stu-id="abde6-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="abde6-172">Hello seguente viene creato un avviso per l'utilizzo medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="abde6-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="abde6-173">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="abde6-174">Fare clic su **regole di avviso** nel pannello VM hello, quindi fare clic su **Aggiungi avviso metrica** in alto di hello del pannello avvisi hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="abde6-175">Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="abde6-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="abde6-176">tootrigger un avviso quando la percentuale della CPU supera 1.0 per cinque minuti, lasciare hello tutti gli altri valori predefiniti selezionati.</span><span class="sxs-lookup"><span data-stu-id="abde6-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="abde6-177">Facoltativamente, selezionare la casella di hello per *i proprietari, collaboratori e lettori di posta elettronica* toosend notifica di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="abde6-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="abde6-178">azione predefinita Hello è toopresent una notifica nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="abde6-179">Fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="abde6-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="abde6-180">Monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="abde6-180">Advanced monitoring</span></span> 

<span data-ttu-id="abde6-181">È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="abde6-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="abde6-182">Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="abde6-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="abde6-183">Quando si dispone di accesso toohello OMS portale, è possibile trovare l'identificatore di chiave e dell'area di lavoro dell'area di lavoro hello nel pannello impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="abde6-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="abde6-184">Sostituire < chiave dell'area di lavoro > e < id area di lavoro > con i valori hello per le OMS è possibile utilizzare area di lavoro e quindi **az vm estensione set** tooadd hello OMS estensione toohello VM:</span><span class="sxs-lookup"><span data-stu-id="abde6-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="abde6-185">Nel Pannello di hello ricerca nei Log del portale OMS hello, dovrebbe essere *myVM* , ad esempio quello mostrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="abde6-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="abde6-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abde6-187">Next steps</span></span>

<span data-ttu-id="abde6-188">In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="abde6-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="abde6-189">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="abde6-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abde6-190">Abilitare la diagnostica di avvio su hello VM</span><span class="sxs-lookup"><span data-stu-id="abde6-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="abde6-191">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="abde6-191">View boot diagnostics</span></span>
> * <span data-ttu-id="abde6-192">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="abde6-192">View host metrics</span></span>
> * <span data-ttu-id="abde6-193">Abilitare l'estensione di diagnostica per hello VM</span><span class="sxs-lookup"><span data-stu-id="abde6-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="abde6-194">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abde6-194">View VM metrics</span></span>
> * <span data-ttu-id="abde6-195">Creare avvisi basati sulle metriche di diagnostica</span><span class="sxs-lookup"><span data-stu-id="abde6-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="abde6-196">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="abde6-196">Set up advanced monitoring</span></span>

<span data-ttu-id="abde6-197">Spostare toohello toolearn esercitazione successiva sul Centro protezione di Azure.</span><span class="sxs-lookup"><span data-stu-id="abde6-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abde6-198">Gestire la sicurezza delle VM</span><span class="sxs-lookup"><span data-stu-id="abde6-198">Manage VM security</span></span>](./tutorial-azure-security.md)