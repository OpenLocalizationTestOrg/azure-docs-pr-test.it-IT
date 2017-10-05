---
title: Installare e configurare Terraform per eseguire il provisioning di macchine virtuali e altra infrastruttura in Azure | Microsoft Docs
description: Informazioni su come installare e configurare Terraform per la creazione di risorse di Azure
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
ms.openlocfilehash: 1f26bccf279ebb61fbf77767186d0435e4f4ba40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="b6724-103">Installare e configurare Terraform per eseguire il provisioning di macchine virtuali e altra infrastruttura in Azure</span><span class="sxs-lookup"><span data-stu-id="b6724-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="b6724-104">In questo articolo vengono illustrati i passaggi necessari per installare e configurare Terraform al fine di eseguire il provisioning di risorse, ad esempio macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="b6724-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="b6724-105">Verrà anche spiegato come creare e usare le credenziali di Azure per abilitare Terraform al provisioning di risorse cloud in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="b6724-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="b6724-106">HashiCorp Terraform offre un modo semplice per definire e distribuire l'infrastruttura cloud usando un linguaggio di modelli personalizzato, denominato linguaggio di configurazione HashiCorp (HCL).</span><span class="sxs-lookup"><span data-stu-id="b6724-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="b6724-107">Questo linguaggio personalizzato è [facile da scrivere e capire](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b6724-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="b6724-108">Inoltre, tramite il comando `terraform plan` è possibile visualizzare le modifiche all'infrastruttura prima del commit.</span><span class="sxs-lookup"><span data-stu-id="b6724-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="b6724-109">Seguire questi passaggi per iniziare a usare Terraform con Azure.</span><span class="sxs-lookup"><span data-stu-id="b6724-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="b6724-110">Installazione di Terraform</span><span class="sxs-lookup"><span data-stu-id="b6724-110">Install Terraform</span></span>
<span data-ttu-id="b6724-111">Per installare Terraform, [scaricare](https://www.terraform.io/downloads.html) il pacchetto appropriato per il sistema operativo in uso in una directory di installazione distinta.</span><span class="sxs-lookup"><span data-stu-id="b6724-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="b6724-112">Il download contiene un singolo file eseguibile, per cui è anche necessario definire un percorso globale.</span><span class="sxs-lookup"><span data-stu-id="b6724-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="b6724-113">Per istruzioni su come impostare il percorso in Mac e Linux, vedere [questa pagina Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="b6724-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="b6724-114">Per istruzioni su come impostare il percorso in Windows, vedere [questa pagina Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="b6724-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="b6724-115">Per verificare l'installazione, eseguire il comando `terraform`.</span><span class="sxs-lookup"><span data-stu-id="b6724-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="b6724-116">Si dovrebbe vedere un elenco di opzioni Terraform disponibili come output.</span><span class="sxs-lookup"><span data-stu-id="b6724-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="b6724-117">Successivamente, sarà necessario consentire l'accesso di Terraform alla sottoscrizione di Azure per eseguire il provisioning dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="b6724-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="b6724-118">Impostazione dell'accesso di Terraform in Azure</span><span class="sxs-lookup"><span data-stu-id="b6724-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="b6724-119">Per abilitare Terraform al provisioning delle risorse in Azure, è necessario creare due entità in Azure Active Directory (AAD): un'applicazione Azure AD e un'entità servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6724-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="b6724-120">Gli identificatori di queste entità verranno usati negli script Terraform.</span><span class="sxs-lookup"><span data-stu-id="b6724-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="b6724-121">L'entità servizio è un'istanza locale di un'applicazione Azure AD globale.</span><span class="sxs-lookup"><span data-stu-id="b6724-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="b6724-122">Un'entità servizio consente il controllo di accesso locale granulare a risorse globali.</span><span class="sxs-lookup"><span data-stu-id="b6724-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="b6724-123">Esistono diversi modi per creare un'applicazione Azure AD e un'entità servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6724-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="b6724-124">Il modo più semplice e rapido oggi consiste nell'usare l'interfaccia della riga di comando di Azure 2.0, che [è possibile scaricare e installare in Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6724-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="b6724-125">È anche possibile usare PowerShell o l'interfaccia della riga di comando di Azure 1.0 per creare l'infrastruttura di sicurezza necessaria.</span><span class="sxs-lookup"><span data-stu-id="b6724-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="b6724-126">Le istruzioni riportate di seguito illustrano come configurare Terraform per Azure usando tutti questi approcci.</span><span class="sxs-lookup"><span data-stu-id="b6724-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="b6724-127">Usare l'interfaccia della riga di comando di Azure 2.0 (per gli utenti di Windows, Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="b6724-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="b6724-128">Dopo avere scaricato e installato [l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), eseguire l'accesso per amministrare la sottoscrizione di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b6724-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="b6724-129">Se si usa il cloud di Azure Cina, Azure Germania o Azure per enti pubblici, è necessario innanzitutto configurare l'interfaccia della riga di comando di Azure per garantirne la compatibilità con il cloud specifico.</span><span class="sxs-lookup"><span data-stu-id="b6724-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="b6724-130">Per completare questa operazione, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="b6724-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="b6724-131">Se si dispone di più sottoscrizioni di Azure, i relativi dettagli vengono restituiti dal comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="b6724-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="b6724-132">Impostare la variabile di ambiente `SUBSCRIPTION_ID` che conterrà il valore del campo `id` restituito dalla sottoscrizione che si intende usare.</span><span class="sxs-lookup"><span data-stu-id="b6724-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="b6724-133">Selezionare la sottoscrizione da usare per la sessione.</span><span class="sxs-lookup"><span data-stu-id="b6724-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="b6724-134">Eseguire una query dell'account per ottenere i valori di ID sottoscrizione e tenant.</span><span class="sxs-lookup"><span data-stu-id="b6724-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="b6724-135">Successivamente, creare credenziali separate per Terraform.</span><span class="sxs-lookup"><span data-stu-id="b6724-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="b6724-136">Vengono restituiti appId, password, sp_name e tenant.</span><span class="sxs-lookup"><span data-stu-id="b6724-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="b6724-137">Prendere nota di appId e password.</span><span class="sxs-lookup"><span data-stu-id="b6724-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="b6724-138">Confermare le proprie credenziali (entità servizio) aprendo una nuova shell ed eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6724-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="b6724-139">Sostituire i valori restituiti per sp_name, password e tenant:</span><span class="sxs-lookup"><span data-stu-id="b6724-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="b6724-140">Uso di PowerShell (per gli utenti di Windows)</span><span class="sxs-lookup"><span data-stu-id="b6724-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="b6724-141">Per usare un computer Windows per scrivere ed eseguire gli script Terraform e usare PowerShell per attività di configurazione, è necessario configurare il computer con gli strumenti PowerShell appropriati.</span><span class="sxs-lookup"><span data-stu-id="b6724-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="b6724-142">Installare gli strumenti di PowerShell seguendo i passaggi descritti in [Installare e configurare Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b6724-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="b6724-143">Scaricare ed eseguire lo [script azure-setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) dalla console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6724-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="b6724-144">Per eseguire lo script azure-setup.ps1, scaricarlo ed eseguire il comando `./azure-setup.ps1 setup` dalla console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6724-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="b6724-145">Accedere quindi alla sottoscrizione di Azure con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="b6724-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="b6724-146">Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="b6724-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="b6724-147">Facoltativamente, scegliere una password complessa quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="b6724-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="b6724-148">Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.</span><span class="sxs-lookup"><span data-stu-id="b6724-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="b6724-149">Usare l'interfaccia della riga di comando di Azure 1.0 (per gli utenti Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="b6724-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="b6724-150">Per iniziare a usare Terraform su computer Linux o Mac con l'interfaccia della riga di comando di Azure 1.0, è necessario che nel computer siano installate le librerie appropriate.</span><span class="sxs-lookup"><span data-stu-id="b6724-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="b6724-151">Installare gli strumenti dell'interfaccia della riga di comando di Azure xPlat seguendo i passaggi descritti in [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6724-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="b6724-152">Scaricare e installare un processore JSON seguendo le istruzioni in [Download jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="b6724-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="b6724-153">Scaricare ed eseguire il [bash script azure-setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) dalla console.</span><span class="sxs-lookup"><span data-stu-id="b6724-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="b6724-154">Per eseguire lo script azure-setup.sh, scaricarlo ed eseguire il comando `./azure-setup setup` dalla console.</span><span class="sxs-lookup"><span data-stu-id="b6724-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="b6724-155">Accedere quindi alla sottoscrizione di Azure con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="b6724-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="b6724-156">Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="b6724-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="b6724-157">Facoltativamente, scegliere una password complessa quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="b6724-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="b6724-158">Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.</span><span class="sxs-lookup"><span data-stu-id="b6724-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="b6724-159">Tutti gli script precedenti creano un'applicazione e un'entità servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6724-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="b6724-160">L'entità servizio ottiene un collaboratore o l'accesso a livello di proprietario nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b6724-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="b6724-161">Per via del livello elevato di accesso concesso, è consigliabile proteggere sempre le informazioni di sicurezza generate da tali script.</span><span class="sxs-lookup"><span data-stu-id="b6724-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="b6724-162">Prendere nota di tutte e quattro le informazioni di sicurezza fornite da tali script: appId, password, subscription_id e tenant_id.</span><span class="sxs-lookup"><span data-stu-id="b6724-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="b6724-163">Impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="b6724-163">Set environment variables</span></span>
<span data-ttu-id="b6724-164">Dopo aver creato e configurato un'entità servizio Azure AD, è necessario comunicare a Terraform l'ID tenant, l'ID sottoscrizione, l'ID client e il segreto client da usare.</span><span class="sxs-lookup"><span data-stu-id="b6724-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="b6724-165">A tale scopo, incorporare tali valori negli script Terraform, come descritto in [Creare un'infrastruttura di base usando Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b6724-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="b6724-166">In alternativa, è possibile impostare le variabili di ambiente seguenti (e pertanto evitare di archiviare o condividere accidentalmente le credenziali):</span><span class="sxs-lookup"><span data-stu-id="b6724-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="b6724-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="b6724-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="b6724-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="b6724-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="b6724-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="b6724-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="b6724-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="b6724-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="b6724-171">Di seguito è riportato uno script della shell di esempio che è possibile usare per impostare tali variabili:</span><span class="sxs-lookup"><span data-stu-id="b6724-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="b6724-172">Se si usa Terraform con Azure per enti pubblici, Azure Germania o Azure Cina, è anche necessario impostare la variabile di ambiente in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="b6724-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6724-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6724-173">Next steps</span></span>
<span data-ttu-id="b6724-174">Abbiamo installato Terraform e configurato le credenziali di Azure per avviare la distribuzione dell'infrastruttura nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6724-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="b6724-175">Vediamo ora come [creare l'infrastruttura con Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b6724-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
