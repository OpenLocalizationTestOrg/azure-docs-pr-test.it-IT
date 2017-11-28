---
title: aaaInstall e configurare le macchine virtuali tooprovision Terraform e altre infrastrutture in Azure | Documenti Microsoft
description: Informazioni su come tooinstall e Terraform toocreate Azure di configurare le risorse
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="07597-103">Installare e configurare le macchine virtuali tooprovision Terraform e altre infrastrutture in Azure</span><span class="sxs-lookup"><span data-stu-id="07597-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="07597-104">Questo articolo descrive tooinstall necessarie hello e configurare le risorse di tooprovision Terraform quali macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="07597-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="07597-105">Si apprenderà come toocreate e utilizzare Azure credenziali tooenable Terraform tooprovision risorse del cloud in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="07597-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="07597-106">HashiCorp Terraform fornisce un modo semplice di toodefine e distribuire un'infrastruttura cloud utilizzando un linguaggio di modelli personalizzati denominato HashiCorp linguaggio di configurazione (elenco).</span><span class="sxs-lookup"><span data-stu-id="07597-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="07597-107">Questa lingua personalizzata è [toowrite semplice e facile toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="07597-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="07597-108">Inoltre, tramite hello `terraform plan` comando, è possibile visualizzare l'infrastruttura di hello modifiche tooyour prima del commit.</span><span class="sxs-lookup"><span data-stu-id="07597-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="07597-109">Seguire questi toostart passaggi utilizzando Terraform con Azure.</span><span class="sxs-lookup"><span data-stu-id="07597-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="07597-110">Installazione di Terraform</span><span class="sxs-lookup"><span data-stu-id="07597-110">Install Terraform</span></span>
<span data-ttu-id="07597-111">tooinstall Terraform, [scaricare](https://www.terraform.io/downloads.html) pacchetto hello appropriato per il sistema operativo in una directory di installazione separato.</span><span class="sxs-lookup"><span data-stu-id="07597-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="07597-112">download di Hello contiene un singolo file eseguibile per il quale è inoltre necessario definire un percorso globale.</span><span class="sxs-lookup"><span data-stu-id="07597-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="07597-113">Per istruzioni su come tooset hello percorso su Linux e Mac, visitare troppo[questa pagina Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="07597-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="07597-114">Per istruzioni su come tooset hello percorso in Windows, visitare troppo[questa pagina Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="07597-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="07597-115">tooverify l'installazione, eseguire hello `terraform` comando.</span><span class="sxs-lookup"><span data-stu-id="07597-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="07597-116">Si dovrebbe vedere un elenco di opzioni Terraform disponibili come output.</span><span class="sxs-lookup"><span data-stu-id="07597-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="07597-117">Successivamente, è necessario tooallow Terraform accesso tooyour sottoscrizione di Azure tooperform il provisioning dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="07597-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="07597-118">Impostare Terraform accesso tooAzure</span><span class="sxs-lookup"><span data-stu-id="07597-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="07597-119">tooenable Terraform tooprovision risorse in Azure, è necessario toocreate due entità in Azure Active Directory (Azure AD): un'applicazione Azure AD e un'entità servizio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07597-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="07597-120">Gli identificatori di queste entità verranno usati negli script Terraform.</span><span class="sxs-lookup"><span data-stu-id="07597-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="07597-121">L'entità servizio è un'istanza locale di un'applicazione Azure AD globale.</span><span class="sxs-lookup"><span data-stu-id="07597-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="07597-122">Un'entità servizio consente risorse tooglobal del controllo di accesso locale granulare.</span><span class="sxs-lookup"><span data-stu-id="07597-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="07597-123">Esistono diversi modi toocreate un'applicazione Azure AD e un'entità servizio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07597-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="07597-124">Hello rapido e semplice è modo oggi toouse CLI di Azure 2.0, che [è possibile scaricare e installare su Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07597-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="07597-125">È inoltre possibile utilizzare infrastruttura di sicurezza necessarie hello toocreate PowerShell o Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="07597-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="07597-126">Hello istruzioni che seguono viene illustrato come tooconfigure Terraform per Azure tramite tutti questi approcci.</span><span class="sxs-lookup"><span data-stu-id="07597-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="07597-127">Usare l'interfaccia della riga di comando di Azure 2.0 (per gli utenti di Windows, Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="07597-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="07597-128">Dopo aver scaricato e installato hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), accedi tooadminister la sottoscrizione di Azure mediante l'emissione di hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="07597-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="07597-129">Se si utilizza hello Cina, Azure in Germania o cloud di Azure per enti pubblici, è necessario toofirst configurare hello Azure CLI toowork con il cloud.</span><span class="sxs-lookup"><span data-stu-id="07597-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="07597-130">È possibile farlo eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="07597-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="07597-131">Se si dispone di più sottoscrizioni di Azure, i relativi dettagli vengono restituiti da hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="07597-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="07597-132">Set hello `SUBSCRIPTION_ID` ambiente toohold variabile hello hello restituito `id` campo sottoscrizione hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="07597-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="07597-133">Impostare una sottoscrizione di hello che si desidera toouse per questa sessione.</span><span class="sxs-lookup"><span data-stu-id="07597-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="07597-134">ID sottoscrizione di hello account tooget hello di query e i valori di ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="07597-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="07597-135">Successivamente, creare credenziali separate per Terraform.</span><span class="sxs-lookup"><span data-stu-id="07597-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="07597-136">Vengono restituiti appId, password, sp_name e tenant.</span><span class="sxs-lookup"><span data-stu-id="07597-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="07597-137">Prendere nota dell'ID applicazione hello e una password.</span><span class="sxs-lookup"><span data-stu-id="07597-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="07597-138">tooconfirm le credenziali (entità servizio), aprire una nuova shell ed eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="07597-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="07597-139">Hello Substitute restituito valori per sp_name, password e tenant:</span><span class="sxs-lookup"><span data-stu-id="07597-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="07597-140">Uso di PowerShell (per gli utenti di Windows)</span><span class="sxs-lookup"><span data-stu-id="07597-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="07597-141">toouse Windows toowrite del computer ed eseguire il Terraform toouse PowerShell per attività di configurazione e script di configurazione del computer con gli strumenti di PowerShell destra hello.</span><span class="sxs-lookup"><span data-stu-id="07597-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="07597-142">Installare gli strumenti di PowerShell alla procedura seguente hello in [installare e configurare Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="07597-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="07597-143">Scaricare ed eseguire hello [script azure setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) dalla console di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="07597-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="07597-144">script di azure setup.ps1 toorun hello, scaricarla ed eseguire hello `./azure-setup.ps1 setup` comando dalla console di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="07597-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="07597-145">Accedere quindi tooyour sottoscrizione di Azure con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="07597-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="07597-146">Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="07597-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="07597-147">Facoltativamente, scegliere una password complessa quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="07597-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="07597-148">Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.</span><span class="sxs-lookup"><span data-stu-id="07597-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="07597-149">Usare l'interfaccia della riga di comando di Azure 1.0 (per gli utenti Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="07597-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="07597-150">tooget avviato con Terraform nel computer Linux o Mac con Azure CLI 1.0, librerie di installazione hello appropriate nel computer.</span><span class="sxs-lookup"><span data-stu-id="07597-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="07597-151">Installare gli strumenti CLI di Azure xPlat seguendo procedure hello [installare Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07597-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="07597-152">Scaricare e installare un processore JSON seguendo le istruzioni hello [scaricare jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="07597-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="07597-153">Scaricare ed eseguire hello [script azure setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script dalla console hello.</span><span class="sxs-lookup"><span data-stu-id="07597-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="07597-154">script di azure setup.sh toorun hello, scaricarla ed eseguire hello `./azure-setup setup` comando dalla console hello.</span><span class="sxs-lookup"><span data-stu-id="07597-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="07597-155">Accedere quindi tooyour sottoscrizione di Azure con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="07597-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="07597-156">Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="07597-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="07597-157">Facoltativamente, scegliere una password complessa quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="07597-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="07597-158">Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.</span><span class="sxs-lookup"><span data-stu-id="07597-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="07597-159">Tutti gli script precedenti di hello creano un'applicazione Azure AD e il servizio principale.</span><span class="sxs-lookup"><span data-stu-id="07597-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="07597-160">entità servizio Hello Ottiene un collaboratore o l'accesso a livello di proprietario della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="07597-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="07597-161">A causa di hello elevato livello di accesso, è consigliabile proteggere sempre le informazioni di sicurezza hello generate da tali script.</span><span class="sxs-lookup"><span data-stu-id="07597-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="07597-162">Prendere nota di tutte e quattro le informazioni di sicurezza fornite da tali script: appId, password, subscription_id e tenant_id.</span><span class="sxs-lookup"><span data-stu-id="07597-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="07597-163">Impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="07597-163">Set environment variables</span></span>
<span data-ttu-id="07597-164">Dopo aver creato e configurare un'entità servizio di Azure AD, è necessario toolet Terraform conoscere hello tenant ID, ID sottoscrizione, ID client e client secret toouse.</span><span class="sxs-lookup"><span data-stu-id="07597-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="07597-165">A tale scopo, incorporare tali valori negli script Terraform, come descritto in [Creare un'infrastruttura di base usando Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="07597-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="07597-166">In alternativa, è possibile impostare hello seguenti variabili di ambiente (e pertanto evitare di archiviare accidentalmente o condividere le proprie credenziali):</span><span class="sxs-lookup"><span data-stu-id="07597-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="07597-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="07597-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="07597-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="07597-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="07597-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="07597-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="07597-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="07597-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="07597-171">È possibile utilizzare questo tooset script della shell di esempio di tali variabili:</span><span class="sxs-lookup"><span data-stu-id="07597-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="07597-172">Inoltre, se si utilizza Terraform con Azure in Cina o di Azure per enti pubblici o di Azure in Germania, è necessario variabile di ambiente tooset hello in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="07597-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07597-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07597-173">Next steps</span></span>
<span data-ttu-id="07597-174">Abbiamo installato Terraform e configurato le credenziali di Azure per avviare la distribuzione dell'infrastruttura nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="07597-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="07597-175">Per ulteriori informazioni come troppo[creare infrastruttura con Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="07597-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
