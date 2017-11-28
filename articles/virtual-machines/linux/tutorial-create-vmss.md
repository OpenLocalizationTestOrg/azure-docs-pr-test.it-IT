---
title: "un set di scalabilità di macchine virtuali Linux in Azure aaaCreate | Documenti Microsoft"
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="df679-103">Creare un set di scalabilità di macchine virtuali e distribuire un'app a disponibilità elevata in Linux</span><span class="sxs-lookup"><span data-stu-id="df679-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="df679-104">Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="df679-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="df679-105">È possibile ridimensionare manualmente numero hello di macchine virtuali nel set di scalabilità hello o definire tooautoscale regole in base all'utilizzo della CPU, la richiesta di memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="df679-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="df679-106">In questa esercitazione viene distribuito un set di scalabilità di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="df679-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="df679-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="df679-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df679-108">Utilizzare cloud init toocreate tooscale un'app</span><span class="sxs-lookup"><span data-stu-id="df679-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="df679-109">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="df679-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="df679-110">Aumentare o diminuire il numero di hello di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="df679-111">Visualizzare le informazioni di connessione per le istanze del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="df679-112">Usare dischi di dati in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="df679-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="df679-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="df679-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="df679-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="df679-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="df679-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="df679-116">Informazioni generali sui set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-116">Scale Set overview</span></span>
<span data-ttu-id="df679-117">Un set di scalabilità della macchina virtuale consente toodeploy e gestire un set di macchine virtuali identiche e la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="df679-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="df679-118">Scala imposta utilizzare hello stessi componenti come sono state descritte nell'esercitazione precedente hello troppo[creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="df679-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="df679-119">Le macchine virtuali di un set di scalabilità vengono create in un set di disponibilità e distribuite in domini logici di errore e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="df679-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="df679-120">Le macchine virtuali vengono create in base alle esigenze in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="df679-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="df679-121">Definire toocontrol le regole di scalabilità automatica come e quando le macchine virtuali vengono aggiunti o rimossi dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="df679-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="df679-122">Queste regole possono essere attivate in base a determinate metriche, ad esempio il carico della CPU, l'utilizzo della memoria o il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="df679-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="df679-123">Scala imposta supporto backup too1, 000 macchine virtuali quando si utilizza un'immagine della piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="df679-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="df679-124">Per i carichi di lavoro, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="df679-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="df679-125">È possibile creare le macchine virtuali too100 in una scala impostata quando si utilizza un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="df679-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="df679-126">Creare un'app tooscale</span><span class="sxs-lookup"><span data-stu-id="df679-126">Create an app tooscale</span></span>
<span data-ttu-id="df679-127">Per la produzione, è preferibile troppo[creare un'immagine di macchina virtuale personalizzata](tutorial-custom-images.md) che include l'applicazione installata e configurata.</span><span class="sxs-lookup"><span data-stu-id="df679-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="df679-128">Per questa esercitazione consente di personalizzare le macchine virtuali di primo avvio tooquickly vedere una scala in azione hello.</span><span class="sxs-lookup"><span data-stu-id="df679-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="df679-129">In un'esercitazione precedente, si è appreso [come una macchina virtuale Linux al primo avvio toocustomize](tutorial-automate-vm-deployment.md) con cloud init.</span><span class="sxs-lookup"><span data-stu-id="df679-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="df679-130">È possibile utilizzare hello stesso tooinstall file di configurazione cloud init NGINX ed eseguire una semplice app Node.js 'Hello World'.</span><span class="sxs-lookup"><span data-stu-id="df679-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="df679-131">Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="df679-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="df679-132">Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="df679-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="df679-133">Immettere `sensible-editor cloud-init.txt` toocreate hello file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="df679-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="df679-134">Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="df679-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="df679-135">Creare un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-135">Create a scale set</span></span>
<span data-ttu-id="df679-136">Per poter creare un set di scalabilità, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="df679-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="df679-137">esempio Hello crea un gruppo di risorse denominato *myResourceGroupScaleSet* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="df679-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="df679-138">Si può ora creare un set di scalabilità di macchine virtuali con il comando [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="df679-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="df679-139">esempio Hello crea un set denominato di scalabilità *myScaleSet*, utilizza hello toocustomize di file cloud init hello VM e genera le chiavi SSH se non sono presenti:</span><span class="sxs-lookup"><span data-stu-id="df679-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="df679-140">Accetta toocreate di pochi minuti e configurare tutti i set di hello scalabilità delle risorse e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="df679-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="df679-141">Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="df679-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="df679-142">Potrebbe essere un altro paio di minuti prima di poter accedere app hello.</span><span class="sxs-lookup"><span data-stu-id="df679-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="df679-143">Consentire il traffico Web</span><span class="sxs-lookup"><span data-stu-id="df679-143">Allow web traffic</span></span>
<span data-ttu-id="df679-144">Un servizio di bilanciamento del carico è stato creato automaticamente come parte del set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="df679-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="df679-145">servizio di bilanciamento del carico Hello distribuisce il traffico tra un set di macchine virtuali definite utilizzando regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="df679-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="df679-146">Maggiori informazioni su concetti del servizio di bilanciamento carico e la configurazione nella prossima esercitazione hello, [come tooload bilanciare le macchine virtuali in Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="df679-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="df679-147">tooallow traffico tooreach hello web app, creare una regola con [creare una regola lb rete az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="df679-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="df679-148">esempio Hello crea una regola denominata *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="df679-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="df679-149">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="df679-149">Test your app</span></span>
<span data-ttu-id="df679-150">toosee l'app di Node.js nel web hello, ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="df679-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="df679-151">esempio Hello Ottiene hello di indirizzo IP per *myScaleSetLBPublicIP* creati come parte del set di scalabilità hello:</span><span class="sxs-lookup"><span data-stu-id="df679-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="df679-152">Immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="df679-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="df679-153">viene visualizzata, Hello app, inclusi hostname hello di hello VM che hello il carico del traffico di bilanciamento del carico distribuito per:</span><span class="sxs-lookup"><span data-stu-id="df679-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Esecuzione dell'app Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="df679-155">toosee set nell'azione di scalabilità hello, è possibile forza l'aggiornamento del carico di web browser toosee hello distribuire il servizio di bilanciamento del traffico tra tutte le macchine virtuali hello esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="df679-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="df679-156">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="df679-156">Management tasks</span></span>
<span data-ttu-id="df679-157">Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="df679-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="df679-158">Inoltre, è consigliabile toocreate script che automatizzano le varie attività di ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="df679-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="df679-159">Hello Azure CLI 2.0 fornisce toodo un modo rapido alle attività.</span><span class="sxs-lookup"><span data-stu-id="df679-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="df679-160">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="df679-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="df679-161">Visualizzare le macchine virtuali in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-161">View VMs in a scale set</span></span>
<span data-ttu-id="df679-162">imposta un elenco di macchine virtuali in esecuzione nella scala tooview, utilizzare [istanze di elenco di az vmss](/cli/azure/vmss#list-instances) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="df679-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="df679-163">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="df679-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="df679-164">Aumentare o diminuire le istanze delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="df679-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="df679-165">numero di hello toosee di istanze attualmente in una scala impostate, utilizzare [Mostra vmss az](/cli/azure/vmss#show) ed eseguire query su *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="df679-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="df679-166">È possibile quindi manualmente aumentare o diminuire il numero di hello di macchine virtuali in hello set di scalabilità con [scala vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="df679-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="df679-167">Hello che segue viene impostato il numero di hello di macchine virtuali la scala impostata troppo*5*:</span><span class="sxs-lookup"><span data-stu-id="df679-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="df679-168">Le regole di scalabilità automatica consentono di definire come tooscale verso l'alto o verso il basso numero hello di macchine virtuali nella scala è impostata nella risposta toodemand, ad esempio il traffico di rete o l'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="df679-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="df679-169">Non è attualmente possibile impostare queste regole nell'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="df679-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="df679-170">Hello utilizzare [portale di Azure](https://portal.azure.com) scalabilità automatica tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="df679-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="df679-171">Ottenere informazioni sulla connessione</span><span class="sxs-lookup"><span data-stu-id="df679-171">Get connection info</span></span>
<span data-ttu-id="df679-172">informazioni di connessione tooobtain circa hello macchine virtuali nel set di scalabilità, utilizzare [az vmss elenco--connessione-informazioni sull'istanza](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="df679-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="df679-173">Questo comando restituisce l'indirizzo IP pubblico hello e la porta per ogni macchina virtuale che consente di tooconnect con SSH:</span><span class="sxs-lookup"><span data-stu-id="df679-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="df679-174">Usare dischi di dati con set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-174">Use data disks with scale sets</span></span>
<span data-ttu-id="df679-175">È possibile creare e usare dischi di dati con set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="df679-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="df679-176">In un'esercitazione precedente, si è appreso come troppo[dischi gestire Azure](tutorial-manage-disks.md) che strutture hello procedure consigliate e i miglioramenti delle prestazioni per la compilazione di applicazioni nei dischi dati, anziché disco hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="df679-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="df679-177">Creare un set di scalabilità con dischi di dati</span><span class="sxs-lookup"><span data-stu-id="df679-177">Create scale set with data disks</span></span>
<span data-ttu-id="df679-178">toocreate scala impostata e collegare dischi dati, aggiungere hello `--data-disk-sizes-gb` parametro toohello [vmss az creare](/cli/azure/vmss#create) comando.</span><span class="sxs-lookup"><span data-stu-id="df679-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="df679-179">esempio Hello crea un set di scalabilità con *50*Gb i dischi dati collegati tooeach istanza:</span><span class="sxs-lookup"><span data-stu-id="df679-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="df679-180">Quando le istanze vengono rimosse da un set di scalabilità, vengono rimossi anche tutti i dischi di dati collegati.</span><span class="sxs-lookup"><span data-stu-id="df679-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="df679-181">Aggiungere dischi di dati</span><span class="sxs-lookup"><span data-stu-id="df679-181">Add data disks</span></span>
<span data-ttu-id="df679-182">impostare un tooinstances disco dati la scala tooadd, utilizzare [collega disco vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="df679-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="df679-183">Hello seguente viene aggiunto un *50*istanza tooeach del disco Gb:</span><span class="sxs-lookup"><span data-stu-id="df679-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="df679-184">Scollegare dischi di dati</span><span class="sxs-lookup"><span data-stu-id="df679-184">Detach data disks</span></span>
<span data-ttu-id="df679-185">impostare un tooinstances disco dati la scala tooremove, utilizzare [Scollega disco vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="df679-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="df679-186">esempio Hello rimuove il disco dati hello nel LUN *2* da ogni istanza di:</span><span class="sxs-lookup"><span data-stu-id="df679-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="df679-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df679-187">Next steps</span></span>
<span data-ttu-id="df679-188">In questa esercitazione è stato creato un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="df679-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="df679-189">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="df679-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df679-190">Utilizzare cloud init toocreate tooscale un'app</span><span class="sxs-lookup"><span data-stu-id="df679-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="df679-191">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="df679-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="df679-192">Aumentare o diminuire il numero di hello di istanze in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="df679-193">Visualizzare le informazioni di connessione per le istanze del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="df679-194">Usare dischi di dati in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="df679-194">Use data disks in a scale set</span></span>

<span data-ttu-id="df679-195">Spostare toolearn esercitazione successiva toohello ulteriori informazioni su concetti per le macchine virtuali di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="df679-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df679-196">Bilanciare il carico di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="df679-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)