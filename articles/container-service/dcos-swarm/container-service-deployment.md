---
title: un contenitore Docker aaaDeploy cluster in Azure | Documenti Microsoft
description: Distribuire una soluzione Kubernetes, controller di dominio o del sistema operativo o Docker Swarm contenitore nel servizio di Azure usando hello portale di Azure o un modello di gestione risorse.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, servizio contenitore di azure, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="2fdcc-104">Distribuire un contenitore Docker usando il portale di Azure hello soluzione di hosting</span><span class="sxs-lookup"><span data-stu-id="2fdcc-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="2fdcc-105">Il servizio contenitore di Azure consente la distribuzione rapida delle soluzioni open source di clustering e orchestrazione dei contenitori più diffuse.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="2fdcc-106">Questo documento illustra la distribuzione di un cluster di servizio di contenitore di Azure tramite hello portale di Azure o un modello di avvio rapido di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="2fdcc-107">È inoltre possibile distribuire un cluster il servizio contenitore di Azure tramite hello [CLI di Azure 2.0](container-service-create-acs-cluster-cli.md) o hello API del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="2fdcc-108">Per le informazioni di base, vedere [Introduzione al servizio contenitore di Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2fdcc-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2fdcc-109">Prerequisites</span></span>

* <span data-ttu-id="2fdcc-110">**Sottoscrizione di Azure**: nel caso in cui non sia disponibile è possibile usare una [versione di prova gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="2fdcc-111">Per cluster di maggiori dimensioni, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2fdcc-112">L'utilizzo della sottoscrizione di Azure e [le quote di risorse](../../azure-subscription-service-limits.md), ad esempio le quote di core, limitare l'ambito dimensione hello del cluster di hello si distribuisce.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="2fdcc-113">toorequest un aumento della quota, aprire un [richiesta di supporto clienti online](../../azure-supportability/how-to-create-azure-support-request.md) senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="2fdcc-114">**Chiave pubblica SSH RSA**: durante la distribuzione tramite il portale di hello o uno dei modelli di avvio rapido di Azure hello, chiave pubblica di tooprovide hello è necessario per l'autenticazione nel servizio contenitore di Azure le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="2fdcc-115">le chiavi RSA Secure Shell (SSH) toocreate, vedere hello [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../../virtual-machines/linux/ssh-from-windows.md) informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="2fdcc-116">**ID dell'entità client e il segreto del servizio** (solo Kubernetes): per ulteriori informazioni e istruzioni toocreate un'entità servizio di Azure Active Directory, vedere [sulle entità servizio hello per un cluster Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="2fdcc-117">Creare un cluster usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2fdcc-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="2fdcc-118">Accedi toohello portale di Azure selezionare **New**e hello Azure Marketplace per la ricerca **servizio contenitore di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Servizio contenitore di Azure nel Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="2fdcc-120">Fare clic su **Azure Container Service** (Servizio contenitore di Azure) e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="2fdcc-121">In hello **nozioni di base** pannello immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="2fdcc-122">**Orchestrator**: selezionare una delle hello contenitore orchestrators toodeploy nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="2fdcc-123">**DC/OS**: distribuisce un cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="2fdcc-124">**Swarm**: distribuisce un cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="2fdcc-125">**Kubernetes**: consente di distribuire un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="2fdcc-126">**Sottoscrizione**: selezionare una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="2fdcc-127">**Gruppo di risorse**: hello nome di un nuovo gruppo di risorse per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="2fdcc-128">**Percorso**: selezionare un'area di Azure per la distribuzione del servizio di contenitore di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="2fdcc-129">Per verificare la disponibilità, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Impostazioni di base](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="2fdcc-131">Fare clic su **OK** quando si è pronti tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="2fdcc-132">In hello **Master configurazione** pannello immettere hello seguendo le impostazioni di nodo principale di hello Linux o i nodi cluster hello (alcune impostazioni sono specifiche tooeach orchestrator):</span><span class="sxs-lookup"><span data-stu-id="2fdcc-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="2fdcc-133">**Nome DNS master**: hello prefisso utilizzato toocreate univoco nome dominio completo (FQDN) per master hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="2fdcc-134">Hello FQDN master è formato hello *prefisso*gestione*percorso*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="2fdcc-135">**Nome utente**: nome utente hello per un account in ognuna delle macchine virtuali Linux di hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="2fdcc-136">**Chiave pubblica SSH RSA**: aggiungere hello toobe chiave pubblica utilizzata per l'autenticazione hello le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="2fdcc-137">È importante che questa chiave non contiene interruzioni di riga e include hello `ssh-rsa` prefisso.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="2fdcc-138">Hello `username@domain` suffisso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="2fdcc-139">Hello chiave dovrebbe essere simile alla seguente hello: **AAAAB3Nz ssh-rsa … <>...... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="2fdcc-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="2fdcc-140">**Entità servizio**: se si seleziona orchestrator Kubernetes hello, immettere una Azure Active Directory **ID client dell'entità servizio** (detto anche appId hello) e **segreto client dell'entità servizio** (password).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="2fdcc-141">Per ulteriori informazioni, vedere [sulle entità servizio hello per un cluster Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="2fdcc-142">**Master conteggio**: numero di schemi in cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="2fdcc-143">**Diagnostica delle macchine Virtuali**: per alcuni orchestrators, è possibile abilitare la diagnostica di VM su schemi hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Configurazione master](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="2fdcc-145">Fare clic su **OK** quando si è pronti tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="2fdcc-146">In hello **configurazione agente** pannello immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="2fdcc-147">**Numero di agenti**: per sciame Docker e Kubernetes, questo valore è numero iniziale di hello degli agenti in set di scalabilità di hello agente.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="2fdcc-148">Per i controller di dominio o del sistema operativo, è numero iniziale di hello degli agenti in un set di scalabilità privata.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="2fdcc-149">Per DC/OS viene creato anche un set di scalabilità pubblico contenente un numero predeterminato di agenti.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="2fdcc-150">Hello numero di agenti in questo set di scalabilità pubblico è determinato dal numero hello di schemi in cluster hello: un agente pubblico per uno schema e due agenti pubblici per tre o cinque schemi.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="2fdcc-151">**Dimensioni della macchina virtuale agente**: hello dimensioni delle macchine virtuali di hello agente.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="2fdcc-152">**Sistema operativo**: questa impostazione è attualmente disponibile solo se si seleziona orchestrator Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="2fdcc-153">Scegliere una distribuzione di Linux o un toorun del sistema operativo Windows Server su agenti hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="2fdcc-154">Questa impostazione determina se il cluster sarà in grado di eseguire applicazioni contenitore Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="2fdcc-155">Il supporto dei contenitori Windows è disponibile in anteprima per i cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="2fdcc-156">Nei cluster DC/OS e Swarm, al momento sono supportati solo gli agenti Linux nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="2fdcc-157">**Le credenziali dell'agente**: se si seleziona sistema operativo di Windows hello, immettere un amministratore **nome utente** e **Password** per agente hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Configurazione dell'agente](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="2fdcc-159">Fare clic su **OK** quando si è pronti tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="2fdcc-160">Al termine della convalida del servizio, fare clic su **OK** .</span><span class="sxs-lookup"><span data-stu-id="2fdcc-160">After service validation finishes, click **OK**.</span></span>

    ![Convalida](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="2fdcc-162">Esaminare le condizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-162">Review hello terms.</span></span> <span data-ttu-id="2fdcc-163">processo di distribuzione hello toostart, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="2fdcc-164">Se si è scelto toopin hello distribuzione toohello portale di Azure, è possibile visualizzare lo stato di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Stato della distribuzione](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="2fdcc-166">distribuzione di Hello richiede diversi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="2fdcc-167">Quindi, i cluster del servizio di contenitore di Azure hello è pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="2fdcc-168">Creare un cluster usando un modello di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="2fdcc-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="2fdcc-169">I modelli di avvio rapido di Azure sono disponibili toodeploy un cluster nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="2fdcc-170">modelli di avvio rapido possono essere modificato tooinclude aggiuntive o avanzate configurazione di Azure Hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="2fdcc-171">toocreate un cluster il servizio contenitore di Azure utilizzando un modello di avvio rapido di Azure, è necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="2fdcc-172">Se non si ha una sottoscrizione, è possibile iscriversi per ottenere una [versione di prova gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="2fdcc-173">Seguire questi passaggi toodeploy un cluster utilizzando un modello e hello Azure CLI 2.0 (vedere [istruzioni di installazione e configurazione](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="2fdcc-174">Se si è in un sistema di Windows, è possibile utilizzare un modello usando Azure PowerShell simile passaggi toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="2fdcc-175">Vedere i passaggi più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-175">See steps later in this section.</span></span> <span data-ttu-id="2fdcc-176">È inoltre possibile distribuire un modello tramite hello [portale](../../azure-resource-manager/resource-group-template-deploy-portal.md) o altri metodi.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="2fdcc-177">toodeploy un controller di dominio o del sistema operativo, Docker Swarm o Kubernetes cluster, selezionare uno dei modelli di avvio rapido disponibile hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="2fdcc-178">Di seguito viene inserito un elenco parziale.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-178">A partial list follows.</span></span> <span data-ttu-id="2fdcc-179">Hello DC/OS e modelli sciame sono hello stesso, ad eccezione di hello orchestrator predefinita.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="2fdcc-180">Modello DC/OS</span><span class="sxs-lookup"><span data-stu-id="2fdcc-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="2fdcc-181">Modello Swarm</span><span class="sxs-lookup"><span data-stu-id="2fdcc-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="2fdcc-182">Modello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2fdcc-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="2fdcc-183">Accedi tooyour account Azure (`az login`) e assicurarsi che tale hello CLI di Azure viene connesso tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="2fdcc-184">È possibile visualizzare la sottoscrizione predefinita hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="2fdcc-185">Se si dispone più tooset sottoscrizione ed è necessario un abbonamento predefinite diverse, eseguire `az account set --subscription` e specificare l'ID sottoscrizione hello o nome.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="2fdcc-186">Come procedura consigliata, utilizzare un nuovo gruppo di risorse per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="2fdcc-187">toocreate un gruppo di risorse, utilizzare hello `az group create` comando specificare un nome gruppo di risorse e il percorso:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="2fdcc-188">Creare un file contenente hello obbligatorio modello JSON parametri.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="2fdcc-189">File dei parametri hello download denominato `azuredeploy.parameters.json` che accompagna il modello di servizio di contenitore di Azure hello `azuredeploy.json` in GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="2fdcc-190">Immettere i valori dei parametri necessari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="2fdcc-191">Ad esempio, toouse hello [modello DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), specificare i valori di parametro per `dnsNamePrefix` e `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="2fdcc-192">Visualizzare le descrizioni di hello in `azuredeploy.json` e le opzioni per gli altri parametri.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="2fdcc-193">Creare un cluster il servizio contenitore, passando i file dei parametri di distribuzione hello con hello seguente comando, dove:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="2fdcc-194">**RESOURCE_GROUP** nome hello hello del gruppo di risorse creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="2fdcc-195">**DEPLOYMENT_NAME** (facoltativo) è un nome con cui toohello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="2fdcc-196">**TEMPLATE_URI** hello percorso del file di distribuzione hello `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="2fdcc-197">Deve trattarsi di un URI file non elaborato hello, non un puntatore toohello UI GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="2fdcc-198">toofind questo URI, seleziona hello `azuredeploy.json` file in GitHub e fare clic su hello **Raw** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="2fdcc-199">È anche possibile fornire parametri sotto forma di stringa in formato JSON nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="2fdcc-200">Utilizzare una comando simile toohello che segue:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="2fdcc-201">distribuzione di Hello richiede diversi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="2fdcc-202">Comandi di PowerShell equivalenti</span><span class="sxs-lookup"><span data-stu-id="2fdcc-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="2fdcc-203">È anche possibile distribuire un modello di cluster del servizio contenitore di Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="2fdcc-204">Questo documento si basa sulla versione di hello 1.0 [modulo Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="2fdcc-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="2fdcc-205">toodeploy un controller di dominio o del sistema operativo, Docker Swarm o Kubernetes cluster, selezionare uno dei modelli di avvio rapido disponibile hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="2fdcc-206">Di seguito viene inserito un elenco parziale.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-206">A partial list follows.</span></span> <span data-ttu-id="2fdcc-207">Si noti che hello DC/OS e modelli sciame sono hello stesso, con l'eccezione hello di hello orchestrator predefinita.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="2fdcc-208">Modello DC/OS</span><span class="sxs-lookup"><span data-stu-id="2fdcc-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="2fdcc-209">Modello Swarm</span><span class="sxs-lookup"><span data-stu-id="2fdcc-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="2fdcc-210">Modello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2fdcc-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="2fdcc-211">Prima di creare un cluster nella sottoscrizione di Azure, verificare che la sessione di PowerShell è stata firmata in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="2fdcc-212">È possibile farlo con hello `Get-AzureRMSubscription` comando:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="2fdcc-213">Se è necessario toosign in tooAzure, utilizzare hello `Login-AzureRMAccount` comando:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="2fdcc-214">Come procedura consigliata, utilizzare un nuovo gruppo di risorse per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="2fdcc-215">toocreate un gruppo di risorse, utilizzare hello `New-AzureRmResourceGroup` comandi e specificare un'area del nome e la destinazione gruppo risorse:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="2fdcc-216">Dopo aver creato un gruppo di risorse, è possibile creare il cluster con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="2fdcc-217">URI di hello Hello desiderato è specificato un modello con hello `-TemplateUri` parametro.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="2fdcc-218">Quando si esegue questo comando, PowerShell richiede i valori dei parametri di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="2fdcc-219">Fornire i parametri del modello</span><span class="sxs-lookup"><span data-stu-id="2fdcc-219">Provide template parameters</span></span>
<span data-ttu-id="2fdcc-220">Se si ha familiarità con PowerShell, significa che è possibile scorrere tra i parametri disponibili per un cmdlet hello digitando un segno meno (-) e quindi premere tasto TAB hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="2fdcc-221">Questa stessa funzionalità può essere usata anche con i parametri definiti nel modello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="2fdcc-222">Non appena si digita il nome di modello hello, hello cmdlet recupera modello hello analizza parametri hello e aggiunge comando toohello parametri di modello hello in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="2fdcc-223">In questo modo i valori dei parametri modello hello toospecify semplice.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="2fdcc-224">E, se si dimentica di un valore di parametro obbligatorio, PowerShell richiede il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="2fdcc-225">Ecco comando completo hello, con i parametri inclusi.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="2fdcc-226">Fornire i valori per i nomi di hello delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="2fdcc-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="2fdcc-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fdcc-227">Next steps</span></span>
<span data-ttu-id="2fdcc-228">Ora che si ha a disposizione un cluster funzionante, vedere i documenti seguenti per informazioni dettagliate sulla connessione e la gestione:</span><span class="sxs-lookup"><span data-stu-id="2fdcc-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="2fdcc-229">Connettersi tooan cluster del servizio di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="2fdcc-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="2fdcc-230">Gestione di contenitori tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="2fdcc-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="2fdcc-231">Gestione dei contenitori con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="2fdcc-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="2fdcc-232">Uso del servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2fdcc-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
