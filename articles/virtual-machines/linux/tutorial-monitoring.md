---
title: Monitorare le macchine virtuali Linux in Azure | Microsoft Docs
description: Informazioni su come monitorare la diagnostica di avvio e le metriche delle prestazioni in una macchina virtuale Linux in Azure
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
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="88b38-103">Come monitorare una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="88b38-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="88b38-104">Per verificare che le macchine virtuali in Azure funzionino correttamente, è possibile esaminare le metriche delle prestazioni e la diagnostica di avvio.</span><span class="sxs-lookup"><span data-stu-id="88b38-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="88b38-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="88b38-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88b38-106">Abilitare la diagnostica di avvio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="88b38-107">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="88b38-107">View boot diagnostics</span></span>
> * <span data-ttu-id="88b38-108">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="88b38-108">View host metrics</span></span>
> * <span data-ttu-id="88b38-109">Abilitare l'estensione della diagnostica nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="88b38-110">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-110">View VM metrics</span></span>
> * <span data-ttu-id="88b38-111">Creare avvisi basati sulle metriche di diagnostica</span><span class="sxs-lookup"><span data-stu-id="88b38-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="88b38-112">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="88b38-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="88b38-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="88b38-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="88b38-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="88b38-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="88b38-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88b38-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="88b38-116">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-116">Create VM</span></span>

<span data-ttu-id="88b38-117">Per visualizzare la diagnostica e le metriche in azione, è necessaria una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88b38-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="88b38-118">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="88b38-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="88b38-119">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupMonitor* nella località *eastus*.</span><span class="sxs-lookup"><span data-stu-id="88b38-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="88b38-120">Creare quindi una macchina virtuale con il comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="88b38-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="88b38-121">L'esempio seguente crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="88b38-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="88b38-122">Abilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="88b38-122">Enable boot diagnostics</span></span>

<span data-ttu-id="88b38-123">All'avvio delle macchine virtuali Linux, l'estensione diagnostica di avvio acquisisce l'output e lo memorizza nell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b38-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="88b38-124">Questi dati possono essere usati per risolvere i problemi di avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88b38-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="88b38-125">La diagnostica di avvio non viene abilitata automaticamente quando si crea una macchina virtuale Linux tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b38-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="88b38-126">Prima di abilitare la diagnostica di avvio, è necessario creare un account di archiviazione per l'archiviazione dei log di avvio.</span><span class="sxs-lookup"><span data-stu-id="88b38-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="88b38-127">Gli account di archiviazione devono avere un nome univoco globale, che abbia tra i 3 e i 24 caratteri e devono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="88b38-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="88b38-128">Creare un account di archiviazione con il comando [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="88b38-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="88b38-129">In questo esempio, viene usata una stringa casuale per creare un nome univoco per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="88b38-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="88b38-130">Quando si abilita la diagnostica di avvio, è necessario l'URI per il contenitore di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="88b38-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="88b38-131">Il comando seguente esegue una query sull'account di archiviazione per restituire questo URI.</span><span class="sxs-lookup"><span data-stu-id="88b38-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="88b38-132">Il valore URI viene archiviato nei nomi di variabile *bloburi* e verrà usato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="88b38-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="88b38-133">Abilitare ora la diagnostica di avvio con [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="88b38-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="88b38-134">Il valore `--storage` è l'URI del BLOB raccolto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="88b38-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="88b38-135">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="88b38-135">View boot diagnostics</span></span>

<span data-ttu-id="88b38-136">Quando la diagnostica di avvio è abilitata, ogni volta che si arresta e si avvia la macchina virtuale, in un file log vengono scritte le informazioni sul processo di avvio.</span><span class="sxs-lookup"><span data-stu-id="88b38-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="88b38-137">Per questo esempio, deallocare prima la macchina virtuale con il comando [az vm deallocate](/cli/azure/vm#deallocate) come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="88b38-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="88b38-138">Ora avviare la macchina virtuale con il comando [az vm start]( /cli/azure/vm#stop) come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="88b38-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="88b38-139">È possibile ottenere i dati della diagnostica di avvio per *myVM* con il comando [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="88b38-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="88b38-140">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="88b38-140">View host metrics</span></span>

<span data-ttu-id="88b38-141">Una macchina virtuale Linux è un host dedicato in Azure con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="88b38-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="88b38-142">Le metriche per l'host vengono raccolte automaticamente e possono essere visualizzate nel portale di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="88b38-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="88b38-143">Nel portale di Azure, fare clic su **Gruppi di risorse** selezionare **myResourceGroupMonitor**, quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="88b38-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="88b38-144">Per visualizzare le prestazioni della macchina virtuale host, fare clic su **Metriche** nel pannello della macchina virtuale, quindi selezionare una metrica *[Host]* in **Metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="88b38-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="88b38-146">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="88b38-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88b38-147">Questo documento descrive la versione 2.3 dell'estensione Diagnostica per Linux, che è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="88b38-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="88b38-148">La versione 2.3 sarà supportata fino al 30 giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="88b38-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="88b38-149">È invece possibile abilitare la versione 3.0 dell'estensione Diagnostica per Linux.</span><span class="sxs-lookup"><span data-stu-id="88b38-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="88b38-150">Per altre informazioni, vedere [la documentazione](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="88b38-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="88b38-151">Sono disponibili le metriche di base host, ma per visualizzare metriche specifiche per la macchina virtuale e più granulari è necessario installare l'estensione Diagnostica di Azure nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88b38-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="88b38-152">L'estensione Diagnostica di Azure consente un monitoraggio aggiuntivo e il recupero dei dati di diagnostica dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88b38-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="88b38-153">È possibile visualizzare queste metriche delle prestazioni e creare avvisi in base al funzionamento della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88b38-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="88b38-154">L'estensione Diagnostica viene installata tramite il portale di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="88b38-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="88b38-155">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="88b38-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="88b38-156">Fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="88b38-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="88b38-157">L'elenco mostra che *Diagnostica di avvio* è già stata abilitata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="88b38-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="88b38-158">Selezionare la casella di controllo per *Metriche di base*.</span><span class="sxs-lookup"><span data-stu-id="88b38-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="88b38-159">Nella sezione *Account di archiviazione* individuare e selezionare l'account *mydiagdata[1234]* creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="88b38-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="88b38-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="88b38-160">Click the **Save** button.</span></span>

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="88b38-162">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-162">View VM metrics</span></span>

<span data-ttu-id="88b38-163">È possibile visualizzare le metriche della macchina virtuale nello stesso modo in cui sono state visualizzate le metriche della macchina virtuale host:</span><span class="sxs-lookup"><span data-stu-id="88b38-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="88b38-164">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="88b38-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="88b38-165">Per visualizzare le prestazioni della macchina virtuale, fare clic su **Metriche** nel pannello della macchina virtuale, quindi selezionare una metrica di diagnostica in **Metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="88b38-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="88b38-167">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="88b38-167">Create alerts</span></span>

<span data-ttu-id="88b38-168">È possibile creare avvisi basati sulle metriche di prestazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="88b38-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="88b38-169">Gli avvisi possono essere usati, ad esempio, per inviare una notifica quando l'uso medio della CPU supera una determinata soglia o lo spazio su disco disponibile è inferiore a una determinata quantità.</span><span class="sxs-lookup"><span data-stu-id="88b38-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="88b38-170">Gli avvisi vengono visualizzati nel portale di Azure o possono essere inviati tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="88b38-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="88b38-171">In risposta agli avvisi generati, è anche possibile attivare i runbook di Automazione di Azure o App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b38-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="88b38-172">L'esempio seguente crea un avviso per l'uso medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="88b38-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="88b38-173">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="88b38-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="88b38-174">Nel pannello della macchina virtuale fare clic su **Regole di avviso**, quindi fare clic su **Aggiungi avviso per la metrica** nella parte superiore del pannello degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="88b38-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="88b38-175">Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="88b38-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="88b38-176">Per attivare un avviso quando la percentuale di CPU supera 1.0 per cinque minuti, lasciare tutte le altre impostazioni predefinite selezionate.</span><span class="sxs-lookup"><span data-stu-id="88b38-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="88b38-177">Facoltativamente, è possibile selezionare la casella per *Invia messaggio di posta elettronica a proprietari, collaboratori e lettori* per inviare una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="88b38-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="88b38-178">L'azione predefinita è di presentare una notifica nel portale.</span><span class="sxs-lookup"><span data-stu-id="88b38-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="88b38-179">Fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="88b38-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="88b38-180">Monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="88b38-180">Advanced monitoring</span></span> 

<span data-ttu-id="88b38-181">È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="88b38-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="88b38-182">Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="88b38-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="88b38-183">Quando si ha accesso al portale di OMS, è possibile trovare la chiave e l'identificatore dell'area di lavoro nel pannello Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="88b38-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="88b38-184">Sostituire <workspace-key> e <workspace-id> con i valori dell'area di lavoro OMS, quindi è possibile usare **az vm extension set** per aggiungere l'estensione OMS alla macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="88b38-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

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

<span data-ttu-id="88b38-185">Nel pannello Ricerca log del portale OMS si dovrebbe vedere *myVM* come mostrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="88b38-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="88b38-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88b38-187">Next steps</span></span>

<span data-ttu-id="88b38-188">In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b38-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="88b38-189">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="88b38-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88b38-190">Abilitare la diagnostica di avvio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="88b38-191">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="88b38-191">View boot diagnostics</span></span>
> * <span data-ttu-id="88b38-192">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="88b38-192">View host metrics</span></span>
> * <span data-ttu-id="88b38-193">Abilitare l'estensione della diagnostica nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="88b38-194">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="88b38-194">View VM metrics</span></span>
> * <span data-ttu-id="88b38-195">Creare avvisi basati sulle metriche di diagnostica</span><span class="sxs-lookup"><span data-stu-id="88b38-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="88b38-196">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="88b38-196">Set up advanced monitoring</span></span>

<span data-ttu-id="88b38-197">Passare all'esercitazione successiva per informazioni sul Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="88b38-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="88b38-198">Gestire la sicurezza delle VM</span><span class="sxs-lookup"><span data-stu-id="88b38-198">Manage VM security</span></span>](./tutorial-azure-security.md)