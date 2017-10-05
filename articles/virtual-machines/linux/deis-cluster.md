---
title: Distribuire un cluster Deis a 3 nodi | Microsoft Docs
description: In questo articolo viene descritto come creare un cluster Deis a 3 nodi utilizzando un modello di Gestione risorse di Azure.
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="5281c-103">Distribuire e configurare un cluster Deis a 3 nodi in Azure</span><span class="sxs-lookup"><span data-stu-id="5281c-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="5281c-104">In questo articolo viene illustrato il provisioning di un cluster [Deis](http://deis.io/) su Azure.</span><span class="sxs-lookup"><span data-stu-id="5281c-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="5281c-105">Vengono descritti tutti i passaggi dalla creazione dei certificati necessari per la distribuzione e la scalabilità di un’applicazione **Go** di esempio sul cluster di cui è stato appena eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="5281c-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="5281c-106">Nel diagramma seguente viene mostrata l'architettura del sistema distribuito.</span><span class="sxs-lookup"><span data-stu-id="5281c-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="5281c-107">Un amministratore di sistema gestisce il cluster usando strumenti Deis come **deis** e **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="5281c-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="5281c-108">Le connessioni vengono stabilite tramite un servizio di bilanciamento del carico di Azure, che inoltra le connessioni a uno dei nodi membri sul cluster.</span><span class="sxs-lookup"><span data-stu-id="5281c-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="5281c-109">Anche i client effettuano l’accesso alle applicazioni distribuite tramite il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5281c-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="5281c-110">In questo caso, il servizio di bilanciamento del carico inoltra il traffico a un router mesh Deis, che indirizza ulteriormente il traffico ai contenitori Docker corrispondenti ospitati sul cluster.</span><span class="sxs-lookup"><span data-stu-id="5281c-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Diagramma dell'architettura del cluster Deis distribuito](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="5281c-112">Per eseguire i passaggi seguenti, saranno necessari:</span><span class="sxs-lookup"><span data-stu-id="5281c-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="5281c-113">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5281c-113">An active Azure subscription.</span></span> <span data-ttu-id="5281c-114">Se non si dispone di una sottoscrizione, è possibile ottenere una versione di valutazione gratuita su [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5281c-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="5281c-115">Un ID di lavoro o di scuola per utilizzare i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5281c-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="5281c-116">Se si dispone di un account personale e si accede con un ID di Microsoft, è necessario [creare un ID di lavoro da quello personale](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5281c-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5281c-117">A seconda del sistema operativo del client, [Azure PowerShell](/powershell/azureps-cmdlets-docs) o l'[interfaccia della riga di comando di Azure per Mac, Linux e Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5281c-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="5281c-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="5281c-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="5281c-119">OpenSSL viene utilizzato per generare i certificati necessari.</span><span class="sxs-lookup"><span data-stu-id="5281c-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="5281c-120">Un client Git, come [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="5281c-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="5281c-121">Per eseguire un test sull'applicazione di esempio, sarà necessario anche un server DNS.</span><span class="sxs-lookup"><span data-stu-id="5281c-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="5281c-122">È possibile utilizzare tutti i server o i servizi DNS che supportano i record A con carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="5281c-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="5281c-123">Un computer per eseguire gli strumenti client Deis.</span><span class="sxs-lookup"><span data-stu-id="5281c-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="5281c-124">È possibile utilizzare una macchina locale o una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5281c-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="5281c-125">È possibile eseguire questi strumenti in qualsiasi distribuzione Linux, ma nelle istruzioni seguenti viene utilizzato Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5281c-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="5281c-126">Provisioning del database</span><span class="sxs-lookup"><span data-stu-id="5281c-126">Provision the cluster</span></span>
<span data-ttu-id="5281c-127">In questa sezione, verrà usato un modello [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) dal repository open source [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5281c-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="5281c-128">Innanzitutto, verrà copiato il modello.</span><span class="sxs-lookup"><span data-stu-id="5281c-128">First, you'll copy down the template.</span></span> <span data-ttu-id="5281c-129">Quindi, verrà creata una nuova coppia di chiavi SSH per l'autenticazione e</span><span class="sxs-lookup"><span data-stu-id="5281c-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="5281c-130">verrà configurato un nuovo identificatore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="5281c-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="5281c-131">Infine, verrà utilizzato lo script Shell o lo script PowerShell per eseguire il provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="5281c-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="5281c-132">Clonare il repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5281c-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="5281c-133">Andare alla cartella del modello:</span><span class="sxs-lookup"><span data-stu-id="5281c-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="5281c-134">Creare una nuova coppia di chiavi SSH utilizzando ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="5281c-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="5281c-135">Generare un certificato utilizzando la chiave privata riportata in precedenza:</span><span class="sxs-lookup"><span data-stu-id="5281c-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="5281c-136">Andare a [https://discovery.etcd.io/new](https://discovery.etcd.io/new) per generare un nuovo token del cluster, simile a:</span><span class="sxs-lookup"><span data-stu-id="5281c-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="5281c-137">Ciascun cluster CoreOS deve disporre di un token univoco da questo servizio gratuito.</span><span class="sxs-lookup"><span data-stu-id="5281c-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="5281c-138">Vedere [Documentazione CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="5281c-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="5281c-139">Modificare il file **cloud-config.yaml** per sostituire il token **discovery** esistente con il nuovo token:</span><span class="sxs-lookup"><span data-stu-id="5281c-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="5281c-140">Modificare il file **azuredeploy-parameters.json** : aprire il certificato creato nel passaggio 4 in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="5281c-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="5281c-141">Copiare tutto il testo tra `----BEGIN CERTIFICATE-----` e `-----END CERTIFICATE-----` nel parametro **sshKeyData** (sarà necessario rimuovere tutti i caratteri di nuova riga).</span><span class="sxs-lookup"><span data-stu-id="5281c-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="5281c-142">Modificare il parametro **newStorageAccountName** .</span><span class="sxs-lookup"><span data-stu-id="5281c-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="5281c-143">Si tratta dell'account di archiviazione per i dischi del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5281c-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="5281c-144">Questo nome account deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="5281c-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="5281c-145">Modificare il parametro **publicDomainName**.</span><span class="sxs-lookup"><span data-stu-id="5281c-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="5281c-146">che diventerà parte del nome DNS associato all’IP pubblico del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5281c-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="5281c-147">L'FQDN finale avrà il formato di *[valore di questo parametro]*.*[area geografica]*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5281c-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="5281c-148">Ad esempio, se il nome viene specificato come deishbai32 e il gruppo di risorse viene distribuito all’area geografica Stati Uniti Occidentali, l’FQDN finale per il servizio di bilanciamento del carico sarà deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5281c-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="5281c-149">Salvare il file del parametro.</span><span class="sxs-lookup"><span data-stu-id="5281c-149">Save the parameter file.</span></span> <span data-ttu-id="5281c-150">Quindi è possibile eseguire il provisioning del cluster utilizzando Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5281c-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="5281c-151">o l’interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="5281c-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="5281c-152">Una volta che viene eseguito il provisioning del gruppo di risorse, è possibile visualizzare tutte le risorse nel gruppo sul portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="5281c-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="5281c-153">Come illustrato nella schermata seguente, il gruppo di risorse contiene una rete virtuale con tre macchine virtuali, che hanno effettuato l’accesso allo stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5281c-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="5281c-154">Il gruppo contiene inoltre un servizio di bilanciamento del carico, che dispone di un IP pubblico associato.</span><span class="sxs-lookup"><span data-stu-id="5281c-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Il gruppo di risorse di cui è stato eseguito il provisioning nel portale di Azure classico](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="5281c-156">Installazione del client</span><span class="sxs-lookup"><span data-stu-id="5281c-156">Install the client</span></span>
<span data-ttu-id="5281c-157">Per controllare il cluster Deis, è necessario **deisctl** .</span><span class="sxs-lookup"><span data-stu-id="5281c-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="5281c-158">Anche se deisctl viene installato automaticamente in tutti i nodi del cluster, si consiglia di utilizzare deisctl su una macchina amministrativa separata.</span><span class="sxs-lookup"><span data-stu-id="5281c-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="5281c-159">Inoltre, poiché tutti i nodi vengono configurati con soli indirizzi IP privati, sarà necessario utilizzare il tunneling SSH tramite il servizio di bilanciamento del carico, che dispone di un indirizzo IP pubblico per eseguire la connessione alle macchine dei nodi.</span><span class="sxs-lookup"><span data-stu-id="5281c-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="5281c-160">Di seguito vengono riportati i passaggi per la configurazione di deisctl su una macchina fisica o virtuale Ubuntu separata.</span><span class="sxs-lookup"><span data-stu-id="5281c-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="5281c-161">Installare deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="5281c-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="5281c-162">Aggiungere la chiave privata all’agente SSH:</span><span class="sxs-lookup"><span data-stu-id="5281c-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="5281c-163">Configurare deisctl:</span><span class="sxs-lookup"><span data-stu-id="5281c-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="5281c-164">Il modello definisce le regole NAT in entrata che eseguono il mapping 2223 all’istanza 1, 2224 all’istanza 2 e 2225 all’istanza 3.</span><span class="sxs-lookup"><span data-stu-id="5281c-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="5281c-165">Ciò fornisce ridondanza per utilizzare lo strumento deisctl.</span><span class="sxs-lookup"><span data-stu-id="5281c-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="5281c-166">È possibile esaminare queste regole sul portale di Azure classico:</span><span class="sxs-lookup"><span data-stu-id="5281c-166">You can examine these rules on Azure classic portal:</span></span>

![Regole NAT sul servizio di bilanciamento del carico](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="5281c-168">Il modello supporta attualmente solo cluster a 3 nodi.</span><span class="sxs-lookup"><span data-stu-id="5281c-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="5281c-169">Ciò a causa di un limite nella definizione delle regole NAT del modello di Gestione risorse di Azure, che non supporta la sintassi del ciclo.</span><span class="sxs-lookup"><span data-stu-id="5281c-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="5281c-170">Installazione e avvio della piattaforma Deis</span><span class="sxs-lookup"><span data-stu-id="5281c-170">Install and start the Deis platform</span></span>
<span data-ttu-id="5281c-171">Ora è possibile utilizzare deisctl per installare e avviare la piattaforma Deis:</span><span class="sxs-lookup"><span data-stu-id="5281c-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="5281c-172">L’avvio della piattaforma richiede alcuni minuti (fino a 10).</span><span class="sxs-lookup"><span data-stu-id="5281c-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="5281c-173">In particolare, l'avvio del servizio generatore può richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="5281c-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="5281c-174">E talvolta può richiedere alcuni tentativi per avere esito positivo: se l'operazione sembra bloccarsi, provare a digitare `ctrl+c` per interrompere l'esecuzione del comando e riprovare.</span><span class="sxs-lookup"><span data-stu-id="5281c-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="5281c-175">È possibile utilizzare `deisctl list` per verificare se tutti i servizi sono in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="5281c-175">You can use `deisctl list` to verify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="5281c-176">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="5281c-176">Congratulations!</span></span> <span data-ttu-id="5281c-177">Ora si dispone di un cluster Deis in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="5281c-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="5281c-178">Successivamente, si procederà alla distribuzione di un’applicazione Go di esempio per vedere il cluster in azione.</span><span class="sxs-lookup"><span data-stu-id="5281c-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="5281c-179">Distribuzione e scalabilità di un'applicazione Hello World</span><span class="sxs-lookup"><span data-stu-id="5281c-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="5281c-180">Nei passaggi seguenti viene illustrato come distribuire un’applicazione Go "Hello World" al cluster.</span><span class="sxs-lookup"><span data-stu-id="5281c-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="5281c-181">I passaggi si basano sulla [documentazione Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="5281c-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="5281c-182">Affinché il router mesh funzioni correttamente, sarà necessario disporre di un record A con carattere jolly per il dominio che punti all'indirizzo IP pubblico del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5281c-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="5281c-183">Nella schermata seguente viene mostrato il record A per la registrazione di un dominio di esempio su GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="5281c-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Record A GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="5281c-185">Per installare deis:</span><span class="sxs-lookup"><span data-stu-id="5281c-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="5281c-186">Creare una nuova chiave SSH, quindi aggiungere la chiave pubblica su GitHub (ovviamente, è possibile riutilizzare le chiavi esistenti).</span><span class="sxs-lookup"><span data-stu-id="5281c-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="5281c-187">Per creare una nuova coppia di chiavi SSH, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5281c-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="5281c-188">Aggiungere id_rsa.pub o la chiave pubblica di propria scelta su GitHub.</span><span class="sxs-lookup"><span data-stu-id="5281c-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="5281c-189">È possibile eseguire questa operazione utilizzando il pulsante Aggiungi chiave SSH nella schermata di configurazione delle chiavi SSH:</span><span class="sxs-lookup"><span data-stu-id="5281c-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Chiave GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="5281c-191">Per registrare un nuovo utente:</span><span class="sxs-lookup"><span data-stu-id="5281c-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="5281c-192">Per aggiungere la chiave SSH:</span><span class="sxs-lookup"><span data-stu-id="5281c-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="5281c-193">Creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5281c-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="5281c-194">
8. Il git push attiverà le immagini Docker per essere compilato e distribuito, operazione che potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5281c-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="5281c-195">In base alla mia esperienza, in alcuni casi l’esecuzione del passaggio 10 (push dell’immagine sul repository privato) potrebbe bloccarsi.</span><span class="sxs-lookup"><span data-stu-id="5281c-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="5281c-196">In questo caso, è possibile arrestare il processo, rimuovere l'applicazione usando 'deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list' per individuare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5281c-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="5281c-197">Se tutto funziona, si otterrà un risultato simile al seguente alla fine dell'output del comando:</span><span class="sxs-lookup"><span data-stu-id="5281c-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="5281c-198">Verificare se l'applicazione funziona:</span><span class="sxs-lookup"><span data-stu-id="5281c-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="5281c-199">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="5281c-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="5281c-200">Scalabilità dell'applicazione a 3 istanze:</span><span class="sxs-lookup"><span data-stu-id="5281c-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="5281c-201">Facoltativamente, è possibile utilizzare deis info per esaminare i dettagli dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5281c-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="5281c-202">Gli output seguenti provengono dalla distribuzione della mia applicazione:</span><span class="sxs-lookup"><span data-stu-id="5281c-202">The following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="5281c-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5281c-203">Next Steps</span></span>
<span data-ttu-id="5281c-204">In questo articolo vengono illustrati tutti i passaggi per eseguire il provisioning di un nuovo cluster Deis su Azure utilizzando un modello di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5281c-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="5281c-205">Il modello supporta la ridondanza nelle connessioni degli strumenti, nonché il bilanciamento del carico per le applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="5281c-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="5281c-206">Il modello consente anche di evitare l'utilizzo di IP pubblici nei nodi membri. Ciò consente di risparmiare preziose risorse IP pubbliche e di fornire un ambiente più protetto per ospitare le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5281c-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="5281c-207">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="5281c-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="5281c-208">[Panoramica di Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="5281c-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="5281c-209">[Come usare l'interfaccia della riga di comando di Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="5281c-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="5281c-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager] (Uso di Azure PowerShell con Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="5281c-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
