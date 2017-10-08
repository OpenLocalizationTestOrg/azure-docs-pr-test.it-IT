---
title: aaaDeploy Deis 3 nodi cluster | Documenti Microsoft
description: Questo articolo viene descritto come toocreate 3 nodi Deis cluster in Azure utilizzando un modello di gestione risorse di Azure
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
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="35a82-103">Distribuire e configurare un cluster Deis a 3 nodi in Azure</span><span class="sxs-lookup"><span data-stu-id="35a82-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="35a82-104">In questo articolo viene illustrato il provisioning di un cluster [Deis](http://deis.io/) su Azure.</span><span class="sxs-lookup"><span data-stu-id="35a82-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="35a82-105">Copre tutti i passaggi di hello creazione hello toodeploying di certificati necessari e la scalabilità di un campione **passare** applicazione in cluster appena sottoposti a provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="35a82-106">Hello diagramma seguente mostra hello architettura del sistema hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="35a82-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="35a82-107">Un amministratore di sistema gestisce hello cluster mediante Deis strumenti, ad esempio **deis** e **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="35a82-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="35a82-108">Le connessioni vengono stabilite tramite un servizio di bilanciamento del carico di Azure, che inoltra i nodi nel cluster hello tooone connessioni hello del membro hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="35a82-109">Hello ai client di accedere alle applicazioni tramite anche bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="35a82-110">In questo caso, bilanciamento del carico hello inoltra hello traffico tooa Deis reticolato router, che routs ulteriormente i contenitori di Docker toocorresponding traffico ospitati nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Diagramma dell'architettura del cluster Deis distribuito](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="35a82-112">In ordine toorun tramite hello alla procedura seguente, è necessario:</span><span class="sxs-lookup"><span data-stu-id="35a82-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="35a82-113">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="35a82-113">An active Azure subscription.</span></span> <span data-ttu-id="35a82-114">Se non si dispone di una sottoscrizione, è possibile ottenere una versione di valutazione gratuita su [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="35a82-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="35a82-115">Un lavoro o i gruppi di risorse di Azure toouse id dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="35a82-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="35a82-116">Se si dispone di un account personale e accedere con un id Microsoft, è necessario troppo[creare un id di lavoro da quello personale](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35a82-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="35a82-117">Uno - a seconda del sistema operativo client - hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [CLI di Azure per Mac, Linux e Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="35a82-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="35a82-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="35a82-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="35a82-119">OpenSSL è toogenerate utilizzati certificati hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="35a82-120">Un client Git, come [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="35a82-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="35a82-121">applicazione di esempio hello tootest, è inoltre necessario un server DNS.</span><span class="sxs-lookup"><span data-stu-id="35a82-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="35a82-122">È possibile utilizzare tutti i server o i servizi DNS che supportano i record A con carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="35a82-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="35a82-123">Un computer toorun Deis gli strumenti client.</span><span class="sxs-lookup"><span data-stu-id="35a82-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="35a82-124">È possibile utilizzare una macchina locale o una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="35a82-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="35a82-125">È possibile eseguire questi strumenti in quasi tutte le distribuzioni di Linux, ma le istruzioni seguenti hello utilizzano Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="35a82-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="35a82-126">Cluster hello effettuare il provisioning</span><span class="sxs-lookup"><span data-stu-id="35a82-126">Provision hello cluster</span></span>
<span data-ttu-id="35a82-127">In questa sezione, si userà un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modello dal repository di origine aprire hello [modelli di azure-Guida introduttiva](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="35a82-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="35a82-128">In primo luogo, si copierà modello hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="35a82-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="35a82-129">Quindi, verrà creata una nuova coppia di chiavi SSH per l'autenticazione e</span><span class="sxs-lookup"><span data-stu-id="35a82-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="35a82-130">verrà configurato un nuovo identificatore per il cluster.</span><span class="sxs-lookup"><span data-stu-id="35a82-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="35a82-131">E, infine, si utilizzerà script della Shell hello o cluster di hello PowerShell script tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="35a82-132">Repository di hello clone: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="35a82-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="35a82-133">Cartella modello toohello passare:</span><span class="sxs-lookup"><span data-stu-id="35a82-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="35a82-134">Creare una nuova coppia di chiavi SSH utilizzando ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="35a82-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="35a82-135">Generare un certificato utilizzando hello sopra la chiave privata:</span><span class="sxs-lookup"><span data-stu-id="35a82-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="35a82-136">Andare troppo[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nuovo token di cluster, che ha un aspetto simile:</span><span class="sxs-lookup"><span data-stu-id="35a82-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="35a82-137">Ogni cluster CoreOS deve toohave un token univoco da questo servizio gratuito.</span><span class="sxs-lookup"><span data-stu-id="35a82-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="35a82-138">Vedere [Documentazione CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="35a82-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="35a82-139">Modificare hello **cloud config.yaml** file tooreplace hello esistente **individuazione** token con il nuovo token di hello:</span><span class="sxs-lookup"><span data-stu-id="35a82-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="35a82-140">Modificare hello **azuredeploy parameters.json** file: il certificato aprire hello creato nel passaggio 4 in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="35a82-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="35a82-141">Copiare tutto il testo tra `----BEGIN CERTIFICATE-----` e `-----END CERTIFICATE-----` in hello **sshKeyData** parametro (sarà necessario tooremove tutti i caratteri di nuova riga).</span><span class="sxs-lookup"><span data-stu-id="35a82-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="35a82-142">Modificare hello **newStorageAccountName** parametro.</span><span class="sxs-lookup"><span data-stu-id="35a82-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="35a82-143">Si tratta di account di archiviazione hello per i dischi del sistema operativo VM.</span><span class="sxs-lookup"><span data-stu-id="35a82-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="35a82-144">Questo nome dell'account è univoco globale toobe.</span><span class="sxs-lookup"><span data-stu-id="35a82-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="35a82-145">Modificare hello **publicDomainName** parametro.</span><span class="sxs-lookup"><span data-stu-id="35a82-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="35a82-146">Che diventerà parte del nome DNS hello associato IP pubblico del servizio di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="35a82-147">Hello FQDN finale avrà il formato di hello di *[valore di questo parametro]*. *[region]* . cloudapp.azure.com. Ad esempio, se si specifica il nome di hello come deishbai32 e gruppo di risorse hello area Stati Uniti occidentali toohello distribuito, quindi hello finale bilanciamento del carico FQDN tooyour sarà deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="35a82-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="35a82-148">Salvare il file di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-148">Save hello parameter file.</span></span> <span data-ttu-id="35a82-149">E quindi è possibile eseguire il provisioning di cluster hello tramite Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="35a82-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="35a82-150">o l’interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="35a82-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="35a82-151">Una volta che il gruppo di risorse hello viene eseguito il provisioning, è possibile visualizzare tutte le risorse hello hello gruppo nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="35a82-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="35a82-152">Come illustrato nella seguente schermata hello hello gruppo di risorse contiene una rete virtuale con tre macchine virtuali, che vengono unite toohello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="35a82-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="35a82-153">gruppo di Hello contiene inoltre un bilanciamento del carico, con un indirizzo IP pubblico associato.</span><span class="sxs-lookup"><span data-stu-id="35a82-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![gruppo di risorse di provisioning di Hello nel portale di Azure classico](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="35a82-155">Installare il client hello</span><span class="sxs-lookup"><span data-stu-id="35a82-155">Install hello client</span></span>
<span data-ttu-id="35a82-156">È necessario **deisctl** toocontrol il Deis cluster.</span><span class="sxs-lookup"><span data-stu-id="35a82-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="35a82-157">Sebbene deisctl viene installato automaticamente in tutti i nodi del cluster di hello, è un deisctl toouse buona norma in un computer di amministrazione separato.</span><span class="sxs-lookup"><span data-stu-id="35a82-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="35a82-158">Inoltre, poiché tutti i nodi sono configurati con solo gli indirizzi IP privati, è necessario toouse SSH tunneling tramite bilanciamento del carico di hello, che ha un indirizzo IP pubblico, le macchine nodo toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="35a82-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="35a82-159">Hello seguenti sono hello passaggi di configurazione di deisctl in una macchina virtuale o un Ubuntu fisico separato.</span><span class="sxs-lookup"><span data-stu-id="35a82-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="35a82-160">Installare deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="35a82-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="35a82-161">Aggiungere l'agente toossh chiave privata:</span><span class="sxs-lookup"><span data-stu-id="35a82-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="35a82-162">Configurare deisctl:</span><span class="sxs-lookup"><span data-stu-id="35a82-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="35a82-163">modello di Hello definisce le regole NAT in ingresso che eseguono il mapping 2223 tooinstance 1, tooinstance 2224 2 e 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="35a82-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="35a82-164">Questo fornisce la ridondanza per lo strumento deisctl hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="35a82-165">È possibile esaminare queste regole sul portale di Azure classico:</span><span class="sxs-lookup"><span data-stu-id="35a82-165">You can examine these rules on Azure classic portal:</span></span>

![Regole NAT nel servizio di bilanciamento del carico hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="35a82-167">Modello hello supporta attualmente solo 3 nodi cluster.</span><span class="sxs-lookup"><span data-stu-id="35a82-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="35a82-168">Ciò a causa di un limite nella definizione delle regole NAT del modello di Gestione risorse di Azure, che non supporta la sintassi del ciclo.</span><span class="sxs-lookup"><span data-stu-id="35a82-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="35a82-169">Installare e avviare hello Deis piattaforma</span><span class="sxs-lookup"><span data-stu-id="35a82-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="35a82-170">È ora possibile utilizzare deisctl tooinstall e avviare hello Deis piattaforma:</span><span class="sxs-lookup"><span data-stu-id="35a82-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="35a82-171">Piattaforma hello iniziale richiede un certo tempo (fino a 10 minuti).</span><span class="sxs-lookup"><span data-stu-id="35a82-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="35a82-172">In particolare, l'avvio del servizio generatore hello può richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="35a82-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="35a82-173">E può talvolta richiedere alcuni tentativi toosucceed: se l'operazione di hello sembra toohang, provare a digitare `ctrl+c` toobreak esecuzione del comando hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="35a82-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="35a82-174">È possibile utilizzare `deisctl list` tooverify se tutti i servizi sono in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="35a82-174">You can use `deisctl list` tooverify if all services are running:</span></span>

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

<span data-ttu-id="35a82-175">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="35a82-175">Congratulations!</span></span> <span data-ttu-id="35a82-176">Ora si dispone di un cluster Deis in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="35a82-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="35a82-177">Successivamente, consente di distribuire un esempio Go cluster hello toosee di applicazione in azione.</span><span class="sxs-lookup"><span data-stu-id="35a82-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="35a82-178">Distribuzione e scalabilità di un'applicazione Hello World</span><span class="sxs-lookup"><span data-stu-id="35a82-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="35a82-179">Hello passaggi seguenti viene illustrato come toodeploy "Hello World" Vai cluster toohello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35a82-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="35a82-180">passaggi di Hello dipendono [Deis documentazione](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="35a82-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="35a82-181">Per hello routing mesh toowork correttamente, è necessario un record con caratteri jolly A toohave per il dominio che punta toohello indirizzo IP pubblico del servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="35a82-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="35a82-182">Hello cattura di schermata seguente mostra hello un record per la registrazione di un dominio di esempio su GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="35a82-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Record A GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="35a82-184">Per installare deis:</span><span class="sxs-lookup"><span data-stu-id="35a82-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="35a82-185">Creare una nuova chiave SSH e quindi aggiungere hello tooGitHub di chiave pubblica (Naturalmente, è inoltre possibile riutilizzare le chiavi esistenti).</span><span class="sxs-lookup"><span data-stu-id="35a82-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="35a82-186">toocreate una coppia di chiavi SSH nuovo, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="35a82-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="35a82-187">Aggiungere id_rsa.pub o chiave pubblica di hello di propria scelta, tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="35a82-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="35a82-188">È possibile farlo tramite hello aggiungere SSH pulsante chiave nella schermata Configurazione chiavi SSH:</span><span class="sxs-lookup"><span data-stu-id="35a82-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Chiave GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="35a82-190">Per registrare un nuovo utente:</span><span class="sxs-lookup"><span data-stu-id="35a82-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="35a82-191">Aggiungere la chiave SSH hello:</span><span class="sxs-lookup"><span data-stu-id="35a82-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="35a82-192">Creare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35a82-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="35a82-193">
8.push git Hello attiverà toobe di immagini Docker compilato e distribuito, che potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="35a82-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="35a82-194">L'esperienza, in alcuni casi, potrebbe bloccarsi passaggio 10 (repository di tooprivate Pushing immagine).</span><span class="sxs-lookup"><span data-stu-id="35a82-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="35a82-195">In questo caso, è possibile arrestare il processo di hello, remove hello applicazione utilizzando ' deis App:: destroy <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nome hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35a82-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="35a82-196">Se tutto funziona, dovrebbe essere simile alla seguente hello alla fine di hello dell'output dei comandi:</span><span class="sxs-lookup"><span data-stu-id="35a82-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="35a82-197">Verificare se un'applicazione hello funzioni:</span><span class="sxs-lookup"><span data-stu-id="35a82-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="35a82-198">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="35a82-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="35a82-199">Istanze too3 dell'applicazione hello scala:</span><span class="sxs-lookup"><span data-stu-id="35a82-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="35a82-200">Facoltativamente, è possibile utilizzare deis info tooexamine dettagli dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35a82-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="35a82-201">Hello gli output seguenti sono la distribuzione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="35a82-201">hello following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="35a82-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35a82-202">Next Steps</span></span>
<span data-ttu-id="35a82-203">In questo articolo è descritta in dettaglio tutti i tooprovision passaggi hello Deis un nuovo cluster in Azure utilizzando un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="35a82-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="35a82-204">il modello di Hello supporta ridondanza in strumenti di connessioni, nonché il bilanciamento del carico per le applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="35a82-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="35a82-205">modello Hello consente anche di evitare l'utilizzo di indirizzi IP pubblici su nodi di membro, che consente di risparmiare preziose risorse IP pubbliche e offre un ambiente più sicuro toohost applicazioni.</span><span class="sxs-lookup"><span data-stu-id="35a82-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="35a82-206">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="35a82-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="35a82-207">[Panoramica di Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="35a82-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="35a82-208">[Come toouse hello CLI di Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="35a82-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="35a82-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager] (Uso di Azure PowerShell con Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="35a82-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
