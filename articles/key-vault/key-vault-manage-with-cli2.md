---
title: Gestire Azure Key Vault tramite l'interfaccia della riga di comando | Microsoft Docs
description: "Usare questa esercitazione per automatizzare le attività comuni in Key Vault tramite l'interfaccia della riga di comando 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="ccb56-103">Gestire Key Vault tramite l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="ccb56-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="ccb56-104">L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree.</span><span class="sxs-lookup"><span data-stu-id="ccb56-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="ccb56-105">Per altre informazioni, vedere la [pagina Insieme di credenziali delle chiavi - Prezzi](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="ccb56-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="ccb56-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="ccb56-106">Introduction</span></span>
<span data-ttu-id="ccb56-107">Usare questa esercitazione per imparare a eseguire facilmente le attività iniziali dell'insieme di credenziali delle chiavi di Azure per creare un contenitore finalizzato (insieme di credenziali) in Azure, in cui archiviare e gestire chiavi crittografiche e segreti in Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="ccb56-108">Verrà inoltre descritto come usare l'interfaccia della riga di comando multipiattaforma di Azure per creare un insieme di credenziali contenente una chiave o una password che sarà possibile usare con un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="ccb56-109">L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.</span><span class="sxs-lookup"><span data-stu-id="ccb56-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="ccb56-110">**Tempo previsto per il completamento:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="ccb56-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="ccb56-111">Questa esercitazione non include istruzioni su come scrivere l'applicazione Azure usata nel passaggio che spiega come autorizzare un'applicazione all'uso di una chiave o un segreto nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="ccb56-112">Questa esercitazione usa l'interfaccia della riga di comando 2.0 di Azure più recente.</span><span class="sxs-lookup"><span data-stu-id="ccb56-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="ccb56-113">Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="ccb56-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccb56-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ccb56-114">Prerequisites</span></span>
<span data-ttu-id="ccb56-115">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccb56-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ccb56-116">Una sottoscrizione a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="ccb56-117">Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="ccb56-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="ccb56-118">Interfaccia della riga di comando versione 2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="ccb56-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="ccb56-119">Per installare l'ultima versione e associarla alla sottoscrizione di Azure, vedere [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli) (Installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="ccb56-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="ccb56-120">Un'applicazione che verrà configurata per usare la chiave o la password creata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="ccb56-121">Un'applicazione di esempio è disponibile nell'[Area download Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="ccb56-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="ccb56-122">Per istruzioni, vedere il file Readme associato.</span><span class="sxs-lookup"><span data-stu-id="ccb56-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="ccb56-123">Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ccb56-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="ccb56-124">Questa esercitazione si presuppone che si abbia familiarità con l'interfaccia della riga di comando (Bash, terminal, prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="ccb56-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="ccb56-125">Il parametro --help o -h consente di visualizzare la Guida per specifici comandi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="ccb56-126">In alternativa, è anche possibile utilizzare il formato azure help [comando] [opzioni] per ottenere le stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="ccb56-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="ccb56-127">Ad esempio, tutti i comandi seguenti restituiranno le stesse informazioni:</span><span class="sxs-lookup"><span data-stu-id="ccb56-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="ccb56-128">In caso di dubbi sui parametri necessari per un comando, fare riferimento alla Guida usando --help, -h o az help [comando].</span><span class="sxs-lookup"><span data-stu-id="ccb56-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="ccb56-129">È consigliabile di leggere anche le seguenti esercitazioni per acquisire familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:</span><span class="sxs-lookup"><span data-stu-id="ccb56-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="ccb56-130">Installare l'interfaccia da riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ccb56-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="ccb56-131">Introduzione all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ccb56-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="ccb56-132">Connettersi alle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="ccb56-132">Connect to your subscriptions</span></span>
<span data-ttu-id="ccb56-133">Per accedere utilizzando un account aziendale, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ccb56-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="ccb56-134">Se invece si vuole accedere digitando in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="ccb56-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="ccb56-135">Se si dispone di più sottoscrizioni e se ne vuole specificare una in particolare da usare per l'insieme di credenziali delle chiavi di Azure, digitare quanto segue per visualizzare le sottoscrizioni per il proprio account:</span><span class="sxs-lookup"><span data-stu-id="ccb56-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="ccb56-136">Quindi, per specificare la sottoscrizione da usare, digitare.</span><span class="sxs-lookup"><span data-stu-id="ccb56-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="ccb56-137">Per ulteriori informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ccb56-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="ccb56-138">Creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ccb56-138">Create a new resource group</span></span>
<span data-ttu-id="ccb56-139">Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ccb56-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="ccb56-140">Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="ccb56-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="ccb56-141">Il primo parametro è il nome del gruppo di risorse e il secondo è la posizione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="ccb56-142">Per la posizione usare il comando `az account list-locations` per identificare come si specifica una posizione alternativa a quella di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ccb56-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="ccb56-143">Se servono altre informazioni, digitare: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="ccb56-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="ccb56-144">Registrare il provider di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ccb56-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="ccb56-145">Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="ccb56-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="ccb56-146">Quest'operazione deve essere eseguita una volta sola per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="ccb56-147">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ccb56-147">Create a key vault</span></span>
<span data-ttu-id="ccb56-148">Usare il comando `az keyvault create` per creare un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="ccb56-149">Questo script ha tre parametri obbligatori: un nome del gruppo di risorse, un nome dell'insieme di credenziali delle chiavi e la località geografica.</span><span class="sxs-lookup"><span data-stu-id="ccb56-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="ccb56-150">Ad esempio, se si usa il nome dell'insieme di credenziali ContosoKeyVault, il nome del gruppo di risorse ContosoResourceGroup e la posizione East Asia, digitare:</span><span class="sxs-lookup"><span data-stu-id="ccb56-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="ccb56-151">L'output di questo comando mostra le proprietà dell'insieme di credenziali delle chiavi appena creato.</span><span class="sxs-lookup"><span data-stu-id="ccb56-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="ccb56-152">Le due proprietà più importanti sono:</span><span class="sxs-lookup"><span data-stu-id="ccb56-152">The two most important properties are:</span></span>

* <span data-ttu-id="ccb56-153">**name**: nell'esempio corrisponde a ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="ccb56-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="ccb56-154">Questo nome verrà usato per altri comandi di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ccb56-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="ccb56-155">**vaultUri**: nell'esempio corrisponde a https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="ccb56-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="ccb56-156">Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.</span><span class="sxs-lookup"><span data-stu-id="ccb56-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="ccb56-157">L'account Azure ora è autorizzato a eseguire qualsiasi operazione su questo insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="ccb56-158">Nessun altro lo è ancora.</span><span class="sxs-lookup"><span data-stu-id="ccb56-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="ccb56-159">Aggiungere una chiave o un segreto all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ccb56-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="ccb56-160">Per usare l'insieme di credenziali delle chiavi di Azure per creare automaticamente una chiave protetta tramite software, eseguire il comando `az key create` e digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ccb56-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="ccb56-161">Tuttavia, se si ha una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si vuole caricare nell'insieme di credenziali delle chiavi di Azure, digitare il comando seguente per importare la chiave dal file PEM che protegge la chiave tramite software nel servizio dell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="ccb56-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="ccb56-162">A questo punto è possibile fare riferimento alla chiave creata o caricata nell'insieme di credenziali delle chiavi di Azure, usando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="ccb56-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="ccb56-163">Usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** per ottenere sempre la versione corrente e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** per ottenere questa versione specifica.</span><span class="sxs-lookup"><span data-stu-id="ccb56-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="ccb56-164">Per aggiungere un segreto all'insieme di credenziali, ovvero una password denominata SQLPassword con il valore Pa$$w0rd per l'insieme di credenziali delle chiavi, digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ccb56-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="ccb56-165">È ora possibile fare riferimento a questa password aggiunta nell'insieme di credenziali delle chiavi di Azure, usando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="ccb56-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="ccb56-166">Usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** per ottenere sempre la versione corrente e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** per ottenere questa versione specifica.</span><span class="sxs-lookup"><span data-stu-id="ccb56-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="ccb56-167">Ora si può visualizzare la chiave o il segreto appena creato:</span><span class="sxs-lookup"><span data-stu-id="ccb56-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="ccb56-168">Per visualizzare la chiave, digitare: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="ccb56-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="ccb56-169">Per visualizzare il segreto, digitare: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="ccb56-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="ccb56-170">Registrare un'applicazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccb56-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="ccb56-171">Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato.</span><span class="sxs-lookup"><span data-stu-id="ccb56-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="ccb56-172">Anche se non è specifico dell'insieme di credenziali delle chiavi di Azure, viene incluso qui per completezza.</span><span class="sxs-lookup"><span data-stu-id="ccb56-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccb56-173">Per completare l'esercitazione, l'account, l'insieme di credenziali e l'applicazione in cui si registrerà questo passaggio devono essere tutti nella stessa directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="ccb56-174">Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccb56-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="ccb56-175">A tale scopo, il proprietario dell'applicazione deve innanzitutto registrare l'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccb56-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="ccb56-176">Al termine della registrazione, il proprietario dell'applicazione ottiene i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccb56-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="ccb56-177">Un **ID applicazione** (chiamato anche ID client) e una **chiave di autenticazione** (chiamata anche segreto condiviso).</span><span class="sxs-lookup"><span data-stu-id="ccb56-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="ccb56-178">L'applicazione deve presentare entrambi questi valori ad Azure Active Directory per ottenere un token.</span><span class="sxs-lookup"><span data-stu-id="ccb56-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="ccb56-179">La configurazione dell'applicazione per eseguire questa operazione dipende dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="ccb56-180">Per l'applicazione di esempio dell'insieme di credenziali delle chiavi, il proprietario dell'applicazione imposta questi valori nel file app.config.</span><span class="sxs-lookup"><span data-stu-id="ccb56-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="ccb56-181">Per registrare l'applicazione in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="ccb56-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="ccb56-182">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="ccb56-183">A sinistra fare clic su **Azure Active Directory** e quindi selezionare la directory in cui si registrerà l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="ccb56-184">È necessario selezionare la stessa directory che contiene la sottoscrizione di Azure con cui è stato creato l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="ccb56-185">Se non si sa quale directory selezionare, fare clic su **Impostazioni**, identificare la sottoscrizione con cui si è creato l'insieme di credenziali chiave e prendere nota del nome della directory visualizzata nell'ultima colonna.</span><span class="sxs-lookup"><span data-stu-id="ccb56-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="ccb56-186">Fare clic su **APPLICAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="ccb56-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="ccb56-187">Se nessuna app è stata aggiunta alla directory, in questa pagina sarà visualizzato solo il collegamento **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="ccb56-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="ccb56-188">Fare clic sul collegamento. In alternativa, è possibile fare clic su **AGGIUNGI** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="ccb56-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="ccb56-189">Nella pagina **Come procedere** della procedura guidata **AGGIUNGI APPLICAZIONE** fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="ccb56-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="ccb56-190">Nella pagina **Informazioni sull'applicazione** specificare un nome per l'applicazione e selezionare **APPLICAZIONE WEB E/O API WEB** (opzione predefinita).</span><span class="sxs-lookup"><span data-stu-id="ccb56-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="ccb56-191">Fare clic sull'icona Avanti.</span><span class="sxs-lookup"><span data-stu-id="ccb56-191">Click the Next icon.</span></span>
6. <span data-ttu-id="ccb56-192">Nella pagina **Proprietà dell'app** specificare **URL ACCESSO** e **URI ID APP** per l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="ccb56-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="ccb56-193">Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle).</span><span class="sxs-lookup"><span data-stu-id="ccb56-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="ccb56-194">Non è importante se questi siti esistono. Ciò che conta è che ogni applicazione nella directory abbia un URI ID app diverso.</span><span class="sxs-lookup"><span data-stu-id="ccb56-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="ccb56-195">La directory usa questa stringa per identificare l'app.</span><span class="sxs-lookup"><span data-stu-id="ccb56-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="ccb56-196">Fare clic sull'icona Completa per salvare le modifiche nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="ccb56-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="ccb56-197">Nella pagina Avvio rapido fare clic su **CONFIGURA**.</span><span class="sxs-lookup"><span data-stu-id="ccb56-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="ccb56-198">Scorrere fino alla sezione **chiavi**, selezionare la durata e quindi fare clic su **SALVA**.</span><span class="sxs-lookup"><span data-stu-id="ccb56-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="ccb56-199">La pagina viene aggiornata e mostra un valore chiave.</span><span class="sxs-lookup"><span data-stu-id="ccb56-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="ccb56-200">È necessario configurare l'applicazione con questo valore chiave e con il valore **ID CLIENT** .</span><span class="sxs-lookup"><span data-stu-id="ccb56-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="ccb56-201">Le istruzioni per questa configurazione saranno specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ccb56-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="ccb56-202">Copiare da questa pagina il valore dell'ID client che si userà nel passaggio successivo per impostare le autorizzazioni per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ccb56-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="ccb56-203">Autorizzare l'applicazione a usare la chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="ccb56-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="ccb56-204">Per autorizzare l'accesso da parte dell'applicazione alla chiave o al segreto nell'insieme di credenziali, usare il comando `az keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="ccb56-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="ccb56-205">Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e l'applicazione che si desidera autorizzare ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si vuole autorizzare l'applicazione a decrittografare e firmare con le chiavi dell'insieme di credenziali, eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ccb56-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="ccb56-206">Se si desidera autorizzare la stessa applicazione per la lettura di tutti i segreti nell'insieme di credenziali, eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="ccb56-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="ccb56-207">Per usare un modulo di protezione hardware</span><span class="sxs-lookup"><span data-stu-id="ccb56-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="ccb56-208">Per una maggiore sicurezza, è possibile importare o generare le chiavi in moduli di protezione hardware (HSM) che rimangono sempre entro il limite HSM.</span><span class="sxs-lookup"><span data-stu-id="ccb56-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="ccb56-209">I moduli di protezione hardware sono certificati per FIPS 140-2 livello 2.</span><span class="sxs-lookup"><span data-stu-id="ccb56-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="ccb56-210">Se questo requisito non è applicabile, saltare questa sezione e andare a [Eliminare l'insieme di credenziali delle chiavi e le chiavi e i segreti associati](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="ccb56-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="ccb56-211">Per creare queste chiavi HSM protette, è necessaria una sottoscrizione all'insieme di credenziali che supporti le chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="ccb56-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="ccb56-212">Quando si crea l'insieme di credenziali, aggiungere il parametro 'sku':</span><span class="sxs-lookup"><span data-stu-id="ccb56-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="ccb56-213">È possibile aggiungere a questo insieme di credenziali chiavi protette tramite software (come illustrato in precedenza) e chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="ccb56-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="ccb56-214">Per creare una chiave HSM protetta, impostare il parametro Destination su 'HSM':</span><span class="sxs-lookup"><span data-stu-id="ccb56-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="ccb56-215">È possibile usare il comando seguente per importare una chiave da un file con estensione PEM nel computer.</span><span class="sxs-lookup"><span data-stu-id="ccb56-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="ccb56-216">Questo comando importa la chiave nei moduli HSM nel servizio dell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="ccb56-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="ccb56-217">Il comando successivo importa un pacchetto "bring your own key" (BYOK).</span><span class="sxs-lookup"><span data-stu-id="ccb56-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="ccb56-218">Ciò consente di generare la chiave nel modulo HSM locale e di trasferirlo in moduli HSM nel servizio dell'insieme di credenziali delle chiavi, senza che la chiave esca dal limite HSM:</span><span class="sxs-lookup"><span data-stu-id="ccb56-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="ccb56-219">Per istruzioni più dettagliate su come generare questo pacchetto BYOK, vedere [Come usare chiavi HSM protette con l'insieme di credenziali delle chiavi di Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="ccb56-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="ccb56-220">Eliminare l'insieme di credenziali delle chiavi e le chiavi e i segreti associati</span><span class="sxs-lookup"><span data-stu-id="ccb56-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="ccb56-221">Se l'insieme di credenziali delle chiavi e la chiave o il segreto associato non sono più necessari, è possibile eliminare l'insieme di credenziali delle chiavi usando il comando `az keyvault delete`:</span><span class="sxs-lookup"><span data-stu-id="ccb56-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="ccb56-222">In alternativa, è possibile eliminare l'intero gruppo di risorse di Azure, che include l'insieme di credenziali delle chiavi e tutte le altre risorse incluse in quel gruppo:</span><span class="sxs-lookup"><span data-stu-id="ccb56-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="ccb56-223">Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure</span><span class="sxs-lookup"><span data-stu-id="ccb56-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="ccb56-224">Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb56-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="ccb56-225">Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="ccb56-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="ccb56-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="ccb56-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="ccb56-227">Questo comando visualizza un elenco completo di proprietà per la chiave specificata:</span><span class="sxs-lookup"><span data-stu-id="ccb56-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="ccb56-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="ccb56-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="ccb56-229">Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="ccb56-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="ccb56-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="ccb56-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="ccb56-231">Ecco un esempio di come rimuovere una chiave specifica:</span><span class="sxs-lookup"><span data-stu-id="ccb56-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="ccb56-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="ccb56-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="ccb56-233">Ecco un esempio di come rimuovere un segreto specifico:</span><span class="sxs-lookup"><span data-stu-id="ccb56-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="ccb56-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="ccb56-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="ccb56-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccb56-235">Next steps</span></span>
<span data-ttu-id="ccb56-236">Per riferimenti sull'interfaccia della riga di comando di Azure per i comandi delle credenziali delle chiavi, vedere [Key Vault CLI reference](/cli/azure/keyvault) (Riferimento dell'interfaccia della riga di comando di Key Vault)</span><span class="sxs-lookup"><span data-stu-id="ccb56-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="ccb56-237">Per i riferimenti alla programmazione, vedere [Guida per gli sviluppatori dell'insieme di credenziali chiave Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ccb56-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
