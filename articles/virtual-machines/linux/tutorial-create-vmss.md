---
title: "Creare un set di scalabilità di macchine virtuali Linux in Azure | Microsoft Docs"
description: "Creare e distribuire un'applicazione a disponibilità elevata in macchine virtuali Linux usando un set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="e231c-103">Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Linux</span><span class="sxs-lookup"><span data-stu-id="e231c-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="e231c-104">Un set di scalabilità di macchine virtuali consente di distribuire e gestire un set di macchine virtuali identiche con scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e231c-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="e231c-105">È possibile adattare manualmente il numero di VM nel set di scalabilità o definire regole di scalabilità automatica in base all'utilizzo della CPU, alla richiesta di memoria o al traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="e231c-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="e231c-106">In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e231c-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="e231c-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="e231c-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e231c-108">Usare cloud-init per creare un'app per la scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="e231c-109">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e231c-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e231c-110">Aumentare o diminuire il numero di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="e231c-111">Visualizzare le informazioni di connessione per le istanze del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="e231c-112">Usare dischi di dati in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e231c-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e231c-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e231c-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="e231c-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e231c-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e231c-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="e231c-116">Informazioni generali sui set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-116">Scale Set overview</span></span>
<span data-ttu-id="e231c-117">Un set di scalabilità di macchine virtuali consente di distribuire e gestire un set di macchine virtuali identiche con scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e231c-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="e231c-118">I set di scalabilità usano gli stessi componenti descritti nell'esercitazione precedente [Creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e231c-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="e231c-119">Le macchine virtuali di un set di scalabilità vengono create in un set di disponibilità e distribuite in domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e231c-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="e231c-120">Le macchine virtuali vengono create in base alle esigenze in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e231c-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="e231c-121">È possibile definire regole di scalabilità automatica per controllare le modalità e i tempi di aggiunta e rimozione delle VM dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e231c-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="e231c-122">Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="e231c-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="e231c-123">I set di scalabilità supportano fino a 1000 macchine virtuali quando si usa un'immagine della piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="e231c-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="e231c-124">Per i carichi di lavoro di produzione, è opportuno [creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="e231c-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="e231c-125">È possibile creare fino a 100 macchine virtuali in un set di scalabilità quando si usa un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e231c-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="e231c-126">Creare un'app per la scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-126">Create an app to scale</span></span>
<span data-ttu-id="e231c-127">Per l'uso in ambiente di produzione, è opportuno [creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md) che includa l'applicazione installata e configurata.</span><span class="sxs-lookup"><span data-stu-id="e231c-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="e231c-128">Per questa esercitazione si esegue la personalizzazione delle macchine virtuali al primo avvio per verificare rapidamente il funzionamento di un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e231c-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="e231c-129">In un'esercitazione precedente, [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), è stato descritto come personalizzare una macchina virtuale al primo avvio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e231c-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="e231c-130">È possibile usare lo stesso file di configurazione cloud-init per installare NGINX ed eseguire una semplice app Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="e231c-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="e231c-131">Nella shell corrente creare un file denominato *cloud-init.txt* e incollare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="e231c-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="e231c-132">Ad esempio, creare il file in Cloud Shell anziché nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e231c-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="e231c-133">Immettere `sensible-editor cloud-init.txt` per creare il file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="e231c-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="e231c-134">Assicurarsi che l'intero file cloud-init venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="e231c-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="e231c-135">Creare un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-135">Create a scale set</span></span>
<span data-ttu-id="e231c-136">Per poter creare un set di scalabilità, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e231c-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e231c-137">Nell'esempio seguente viene creato un gruppo di risorse denominato *myResourceGroupScaleSet* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="e231c-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="e231c-138">Si può ora creare un set di scalabilità di macchine virtuali con il comando [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="e231c-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="e231c-139">Nell'esempio seguente viene creato un set di scalabilità denominato *myScaleSet*, viene usato il file cloud-int per personalizzare la VM e vengono generate le chiavi SSH, se non sono presenti:</span><span class="sxs-lookup"><span data-stu-id="e231c-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="e231c-140">La creazione e la configurazione di tutte le macchine virtuali e risorse del set di scalabilità richiedono alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="e231c-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="e231c-141">Sono presenti attività in background la cui esecuzione continua dopo che l'interfaccia della riga di comando di Azure è tornata al prompt.</span><span class="sxs-lookup"><span data-stu-id="e231c-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="e231c-142">Potrebbe trascorrere ancora qualche minuto prima che sia possibile accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="e231c-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="e231c-143">Consentire il traffico Web</span><span class="sxs-lookup"><span data-stu-id="e231c-143">Allow web traffic</span></span>
<span data-ttu-id="e231c-144">Un bilanciamento del carico è stato creato automaticamente come parte del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e231c-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="e231c-145">Il bilanciamento del carico distribuisce il traffico ad un set di macchine virtuali definite usando le proprie regole.</span><span class="sxs-lookup"><span data-stu-id="e231c-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="e231c-146">Altre informazioni sui concetti di bilanciamento del carico e sulla configurazione saranno illustrate nella prossima esercitazione, [Come bilanciare il carico di macchine virtuali in Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="e231c-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="e231c-147">Per consentire al traffico di raggiungere l'app Web, creare una regola con il comando [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="e231c-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="e231c-148">Nell'esempio seguente viene creata una regola denominata *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="e231c-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="e231c-149">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="e231c-149">Test your app</span></span>
<span data-ttu-id="e231c-150">Per visualizzare l'app Node.js sul Web, ottenere l'indirizzo IP pubblico del bilanciamento del carico con il comando [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="e231c-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="e231c-151">Nell'esempio seguente si ottiene l'indirizzo IP per *myScaleSetLBPublicIP* creato come parte del set di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="e231c-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="e231c-152">Immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="e231c-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="e231c-153">Verrà visualizzata l'app, con il nome host della VM a cui il servizio di bilanciamento del carico ha distribuito il traffico:</span><span class="sxs-lookup"><span data-stu-id="e231c-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Esecuzione dell'app Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="e231c-155">Per verificare il funzionamento del set di scalabilità, è possibile imporre l'aggiornamento del Web browser per visualizzare la distribuzione del traffico da parte del bilanciamento del carico tra tutte le macchine virtuali che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="e231c-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="e231c-156">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="e231c-156">Management tasks</span></span>
<span data-ttu-id="e231c-157">Nel ciclo di vita del set di scalabilità, potrebbe essere necessario eseguire una o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="e231c-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="e231c-158">Si potrebbe anche voler creare script per automatizzare le attività di ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="e231c-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="e231c-159">L'interfaccia della riga di comando di Azure 2.0 offre un modo rapido per eseguire tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="e231c-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="e231c-160">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="e231c-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="e231c-161">Visualizzare le macchine virtuali in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-161">View VMs in a scale set</span></span>
<span data-ttu-id="e231c-162">Per visualizzare un elenco di macchine virtuali in esecuzione nel set di scalabilità, usare il comando [az vmss list-instances](/cli/azure/vmss#list-instances) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e231c-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="e231c-163">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e231c-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="e231c-164">Aumentare o diminuire le istanze delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e231c-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="e231c-165">Per visualizzare il numero di istanze attualmente presenti in un set di scalabilità, usare il comando [az vmss show](/cli/azure/vmss#show) ed eseguire una query su *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="e231c-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="e231c-166">È possibile aumentare o ridurre manualmente il numero di macchine virtuali nel set di scalabilità con il comando [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="e231c-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="e231c-167">L'esempio seguente imposta il numero di VM del set di scalabilità su *5*:</span><span class="sxs-lookup"><span data-stu-id="e231c-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="e231c-168">Le regole di scalabilità automatica consentono di definire come aumentare o ridurre il numero di macchine virtuali del set di scalabilità in base alla domanda, ad esempio il traffico di rete o l'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="e231c-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="e231c-169">Non è attualmente possibile impostare queste regole nell'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="e231c-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="e231c-170">Usare il [Portale di Azure](https://portal.azure.com) per configurare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e231c-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="e231c-171">Ottenere informazioni sulla connessione</span><span class="sxs-lookup"><span data-stu-id="e231c-171">Get connection info</span></span>
<span data-ttu-id="e231c-172">Per ottenere informazioni sulla connessione delle macchine virtuali nel set di scalabilità, usare [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="e231c-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="e231c-173">Questo comando restituisce l'indirizzo IP pubblico e la porta per ogni macchina virtuale che consente la connessione con SSH:</span><span class="sxs-lookup"><span data-stu-id="e231c-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="e231c-174">Usare dischi di dati con set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-174">Use data disks with scale sets</span></span>
<span data-ttu-id="e231c-175">È possibile creare e usare dischi di dati con set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e231c-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="e231c-176">Nell'esercitazione precedente si è appreso come [gestire i dischi di Azure](tutorial-manage-disks.md), con le procedure consigliate e i miglioramenti delle prestazioni per la creazione di applicazioni su dischi di dati piuttosto che sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e231c-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="e231c-177">Creare un set di scalabilità con dischi di dati</span><span class="sxs-lookup"><span data-stu-id="e231c-177">Create scale set with data disks</span></span>
<span data-ttu-id="e231c-178">Per creare un set di scalabilità e collegare dischi di dati, aggiungere il parametro `--data-disk-sizes-gb` al comando [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="e231c-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="e231c-179">Nell'esempio seguente viene creato un set di scalabilità con dischi di dati da *50* Gb collegati a ogni istanza:</span><span class="sxs-lookup"><span data-stu-id="e231c-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="e231c-180">Quando le istanze vengono rimosse da un set di scalabilità, vengono rimossi anche tutti i dischi di dati collegati.</span><span class="sxs-lookup"><span data-stu-id="e231c-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="e231c-181">Aggiungere dischi di dati</span><span class="sxs-lookup"><span data-stu-id="e231c-181">Add data disks</span></span>
<span data-ttu-id="e231c-182">Per aggiungere un disco di dati per le istanze nel set di scalabilità, usare [az vmss disk attach](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e231c-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="e231c-183">Nell'esempio seguente viene aggiunto un disco di dati da *50* Gb a ogni istanza:</span><span class="sxs-lookup"><span data-stu-id="e231c-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="e231c-184">Scollegare dischi di dati</span><span class="sxs-lookup"><span data-stu-id="e231c-184">Detach data disks</span></span>
<span data-ttu-id="e231c-185">Per rimuovere un disco di dati per le istanze nel set di scalabilità, usare [az vmss disk detach](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="e231c-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="e231c-186">Nell'esempio seguente viene rimosso il disco di dati del LUN *2* da ogni istanza:</span><span class="sxs-lookup"><span data-stu-id="e231c-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="e231c-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e231c-187">Next steps</span></span>
<span data-ttu-id="e231c-188">In questa esercitazione è stato creato un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e231c-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="e231c-189">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="e231c-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e231c-190">Usare cloud-init per creare un'app per la scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="e231c-191">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e231c-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e231c-192">Aumentare o diminuire il numero di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="e231c-193">Visualizzare le informazioni di connessione per le istanze del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="e231c-194">Usare dischi di dati in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="e231c-194">Use data disks in a scale set</span></span>

<span data-ttu-id="e231c-195">Passare all'esercitazione successiva per maggiori informazioni sui concetti di bilanciamento del carico per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e231c-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e231c-196">Bilanciare il carico delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e231c-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)