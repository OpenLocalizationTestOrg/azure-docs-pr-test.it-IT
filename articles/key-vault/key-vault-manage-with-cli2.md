---
title: insieme di credenziali chiave di Azure usa CLI aaaManage | Documenti Microsoft
description: "Utilizzare questa attività comuni di esercitazione tooautomate nell'insieme di credenziali chiave usando hello CLI 2.0"
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
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="0d72b-103">Gestire Key Vault tramite l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="0d72b-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="0d72b-104">L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree.</span><span class="sxs-lookup"><span data-stu-id="0d72b-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="0d72b-105">Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0d72b-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="0d72b-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="0d72b-106">Introduction</span></span>
<span data-ttu-id="0d72b-107">Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato (un insieme di credenziali) in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="0d72b-108">Illustra hello processo di toocreate interfaccia della riga di comando multipiattaforma di Azure utilizzando un insieme di credenziali che contiene una chiave o una password che è quindi possibile utilizzare con un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="0d72b-109">L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.</span><span class="sxs-lookup"><span data-stu-id="0d72b-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="0d72b-110">**Toocomplete tempo stimato:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="0d72b-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="0d72b-111">In questa esercitazione non include istruzioni su come toowrite hello applicazione Azure che uno dei passaggi di hello include, che mostra come tooauthorize un toouse applicazione una chiave o la chiave privata della chiave hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="0d72b-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="0d72b-112">Questa esercitazione viene utilizzato hello 2.0 CLI di Azure più recenti.</span><span class="sxs-lookup"><span data-stu-id="0d72b-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="0d72b-113">Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0d72b-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d72b-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d72b-114">Prerequisites</span></span>
<span data-ttu-id="0d72b-115">toocomplete questa esercitazione, è necessario disporre di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d72b-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="0d72b-116">TooMicrosoft una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="0d72b-117">Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="0d72b-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="0d72b-118">Interfaccia della riga di comando versione 2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="0d72b-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="0d72b-119">tooinstall hello versione più recente e connettersi tooyour sottoscrizione di Azure, vedere [installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure 2.0 hello](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0d72b-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="0d72b-120">Un'applicazione che verrà configurato toouse hello chiave o password creati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="0d72b-121">Un'applicazione di esempio è disponibile da hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="0d72b-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="0d72b-122">Per istruzioni, vedere il file Leggimi di accompagnamento hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="0d72b-123">Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0d72b-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="0d72b-124">In questa esercitazione si presuppone che si ha familiarità con l'interfaccia della riga di comando hello (Bash, Terminal, prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="0d72b-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="0d72b-125">Hello - Guida o -h parametro può essere utilizzato tooview della Guida in linea per i comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="0d72b-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="0d72b-126">In alternativa, help hello azure [comando] [opzioni] formato può essere anche usato tooreturn hello stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="0d72b-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="0d72b-127">Ad esempio, i comandi tutte restituito seguente hello hello stesse informazioni:</span><span class="sxs-lookup"><span data-stu-id="0d72b-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="0d72b-128">In caso di dubbi sui parametri hello necessari da un comando, fare riferimento tramite toohelp - help, -h o az help [comando].</span><span class="sxs-lookup"><span data-stu-id="0d72b-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="0d72b-129">È inoltre possibile leggere hello seguenti esercitazioni tooget familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:</span><span class="sxs-lookup"><span data-stu-id="0d72b-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="0d72b-130">Installare l'interfaccia da riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0d72b-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="0d72b-131">Introduzione all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="0d72b-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="0d72b-132">Connettersi tooyour sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="0d72b-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="0d72b-133">toolog con un account aziendale, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d72b-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="0d72b-134">o se si desidera toolog digitando in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="0d72b-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="0d72b-135">Se si dispone di più sottoscrizioni e si desidera toospecify un uno toouse specifico per l'insieme di credenziali chiave di Azure, digitare hello sottoscrizioni hello toosee per l'account di seguito:</span><span class="sxs-lookup"><span data-stu-id="0d72b-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="0d72b-136">Quindi, toospecify hello sottoscrizione toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="0d72b-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="0d72b-137">Per ulteriori informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0d72b-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="0d72b-138">Creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d72b-138">Create a new resource group</span></span>
<span data-ttu-id="0d72b-139">Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0d72b-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="0d72b-140">Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="0d72b-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="0d72b-141">primo parametro Hello è il nome di gruppo di risorse e hello secondo parametro è il percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="0d72b-142">Per il percorso, utilizzare il comando di hello `az account list-locations` tooidentify come toospecify toohello un percorso alternativo uno in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="0d72b-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="0d72b-143">Se servono altre informazioni, digitare: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="0d72b-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="0d72b-144">Registrazione provider di risorse hello insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="0d72b-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="0d72b-145">Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="0d72b-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="0d72b-146">Questa operazione deve solo toobe eseguito una volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="0d72b-147">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="0d72b-147">Create a key vault</span></span>
<span data-ttu-id="0d72b-148">Hello utilizzare `az keyvault create` comando toocreate un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="0d72b-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="0d72b-149">Questo script ha tre parametri obbligatori: il nome di un gruppo di risorse, un insieme di credenziali delle chiavi e la posizione geografica di hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="0d72b-150">Ad esempio, se si utilizza il nome dell'insieme di credenziali hello di ContosoKeyVault, nome gruppo di risorse hello di ContosoResourceGroup e il percorso di hello dell'Asia orientale, digitare:</span><span class="sxs-lookup"><span data-stu-id="0d72b-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="0d72b-151">output di Hello di questo comando Mostra le proprietà dell'insieme di credenziali chiave hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="0d72b-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="0d72b-152">proprietà di Hello due più importanti sono:</span><span class="sxs-lookup"><span data-stu-id="0d72b-152">hello two most important properties are:</span></span>

* <span data-ttu-id="0d72b-153">**nome**: nell'esempio hello tratta ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="0d72b-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="0d72b-154">Questo nome verrà usato per altri comandi di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0d72b-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="0d72b-155">**vaultUri**: nell'esempio hello tratta https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="0d72b-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="0d72b-156">Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.</span><span class="sxs-lookup"><span data-stu-id="0d72b-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="0d72b-157">L'account di Azure è ora autorizzato tooperform insieme di credenziali di qualsiasi operazione su questa chiave.</span><span class="sxs-lookup"><span data-stu-id="0d72b-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="0d72b-158">Nessun altro lo è ancora.</span><span class="sxs-lookup"><span data-stu-id="0d72b-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="0d72b-159">Aggiungere una chiave o un insieme di credenziali chiave segreta toohello</span><span class="sxs-lookup"><span data-stu-id="0d72b-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="0d72b-160">Se si desidera toocreate insieme credenziali chiavi Azure una chiave protetta tramite software per l'utente, utilizzare hello `az key create` comandi e digitare il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="0d72b-161">Tuttavia, se si dispone di una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si desidera tooupload tooAzure insieme di credenziali chiave, digitare hello seguenti chiave hello tooimport dagli hello. File con estensione PEM, che protegge hello chiave tramite software nel servizio insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="0d72b-162">È ora possibile fare riferimento chiave hello creati o caricati tooAzure insieme di credenziali chiave utilizzando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="0d72b-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="0d72b-163">Utilizzare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways ottenere la versione corrente di hello e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tale versione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="0d72b-164">tooadd un insieme di credenziali toohello segreto, che è una password denominata SQLPassword e con valore hello Pa$ $w0rd tooAzure insieme di credenziali chiave hello tipo seguente:</span><span class="sxs-lookup"><span data-stu-id="0d72b-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="0d72b-165">È ora possibile fare riferimento a questa password che sono state aggiunte tooAzure insieme di credenziali chiave, tramite il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="0d72b-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="0d72b-166">Utilizzare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways ottenere la versione corrente di hello e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tale versione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="0d72b-167">Si considerino hello chiave o il segreto appena creato:</span><span class="sxs-lookup"><span data-stu-id="0d72b-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="0d72b-168">tooview il tipo di chiave,:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="0d72b-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="0d72b-169">tooview segreto, tipo:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="0d72b-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="0d72b-170">Registrare un'applicazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d72b-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="0d72b-171">Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato.</span><span class="sxs-lookup"><span data-stu-id="0d72b-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="0d72b-172">Non è tooAzure specifico insieme di credenziali chiave ma è incluso in questo caso, per motivi di completezza.</span><span class="sxs-lookup"><span data-stu-id="0d72b-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d72b-173">esercitazione hello toocomplete, l'account, insieme di credenziali hello e un'applicazione hello che verrà registrato in questo passaggio deve essere in hello stessa directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="0d72b-174">Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d72b-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="0d72b-175">toodo, hello proprietario di un'applicazione hello deve innanzitutto registrare l'applicazione hello in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d72b-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="0d72b-176">Alla fine di hello della registrazione, proprietario dell'applicazione hello Ottiene hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="0d72b-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="0d72b-177">Un **ID applicazione** (noto anche come un ID Client) e **chiave di autenticazione** (noto anche come hello segreto condiviso).</span><span class="sxs-lookup"><span data-stu-id="0d72b-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="0d72b-178">un'applicazione Hello deve presentare entrambi questi tooAzure valori tooget un token di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d72b-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="0d72b-179">Come un'applicazione hello viene configurato toodo che ciò dipende dall'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="0d72b-180">Per l'applicazione di esempio insieme di credenziali chiave hello, proprietario dell'applicazione hello imposta questi valori nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="0d72b-181">applicazione hello tooregister in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="0d72b-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="0d72b-182">Accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="0d72b-183">A sinistra di hello, fare clic su **Azure Active Directory**, quindi selezionare hello directory in cui è necessario registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="0d72b-184">È necessario selezionare hello stessa directory che contiene hello sottoscrizione di Azure con cui è stato creato l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="0d72b-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="0d72b-185">Non si conosce la directory in questo caso, fare clic su **impostazioni**, identificare hello sottoscrizione con cui è stato creato l'insieme di credenziali chiave e il nome di hello nota della directory hello visualizzato nell'ultima colonna hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="0d72b-186">Fare clic su **APPLICAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="0d72b-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="0d72b-187">Se nessuna App è stati aggiunti tooyour directory, questa pagina mostrerà solo hello **aggiungere un'App** collegamento.</span><span class="sxs-lookup"><span data-stu-id="0d72b-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="0d72b-188">Fare clic sul collegamento hello o in alternativa, è possibile fare clic su hello **aggiungere** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0d72b-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="0d72b-189">In hello **Aggiungi applicazione** procedura guidata hello **cosa si desidera toodo?** pagina, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="0d72b-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="0d72b-190">In hello **informazioni sull'applicazione** pagina, specificare un nome per l'applicazione e selezionare **applicazione WEB, e/o API WEB** (hello predefinito).</span><span class="sxs-lookup"><span data-stu-id="0d72b-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="0d72b-191">Fare clic sull'icona Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="0d72b-192">In hello **proprietà App** specificare hello **URL accesso** e **URI ID APP** per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="0d72b-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="0d72b-193">Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle).</span><span class="sxs-lookup"><span data-stu-id="0d72b-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="0d72b-194">Non è importante se esistono di questi siti. aspetto importante è che URI ID app hello per ogni applicazione è diverso per ogni applicazione nella directory.</span><span class="sxs-lookup"><span data-stu-id="0d72b-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="0d72b-195">directory Hello usato tooidentify questa stringa l'app.</span><span class="sxs-lookup"><span data-stu-id="0d72b-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="0d72b-196">Fare clic su hello icona completata toosave le modifiche apportate nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="0d72b-197">Nella pagina introduttiva hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="0d72b-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="0d72b-198">Scorrere toohello **chiavi** sezione, selezionare la durata hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="0d72b-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="0d72b-199">pagina Hello viene aggiornato e verrà visualizzato un valore di chiave.</span><span class="sxs-lookup"><span data-stu-id="0d72b-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="0d72b-200">È necessario configurare l'applicazione con questo valore di chiave e hello **ID CLIENT** valore.</span><span class="sxs-lookup"><span data-stu-id="0d72b-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="0d72b-201">Le istruzioni per questa configurazione saranno specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d72b-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="0d72b-202">Copiare valore dell'ID di hello client dalla pagina, che verrà utilizzato in hello successivo passaggio tooset le autorizzazioni per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="0d72b-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="0d72b-203">Autorizzare hello applicazione toouse hello chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="0d72b-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="0d72b-204">tooauthorize hello applicazione tooaccess hello chiave o al segreto nell'insieme di credenziali hello, utilizzare hello `az keyvault set-policy` comando.</span><span class="sxs-lookup"><span data-stu-id="0d72b-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="0d72b-205">Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e hello applicazione cui si desidera tooauthorize ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si desidera tooauthorize hello applicazione toodecrypt e accedere con le chiavi nell'insieme di credenziali, quindi eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d72b-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="0d72b-206">Se si desiderano che stessi segreti tooread applicazione tooauthorize nell'insieme di credenziali, eseguire hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="0d72b-207">Se si desidera toouse un modulo di protezione hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="0d72b-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="0d72b-208">Per maggiore sicurezza, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello.</span><span class="sxs-lookup"><span data-stu-id="0d72b-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="0d72b-209">Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato.</span><span class="sxs-lookup"><span data-stu-id="0d72b-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="0d72b-210">Se questo requisito non si applica a tooyou, ignorare questa sezione e passare troppo[Elimina insieme di credenziali chiave hello e le chiavi associate e i segreti](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="0d72b-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="0d72b-211">toocreate queste chiavi HSM protette, è necessario avere una sottoscrizione di insieme di credenziali che supporta chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="0d72b-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="0d72b-212">Quando si crea keyvault hello, aggiungere il parametro 'sku' hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="0d72b-213">È possibile aggiungere le chiavi protette tramite software (come illustrato in precedenza) e l'insieme di credenziali delle chiavi HSM protette toothis.</span><span class="sxs-lookup"><span data-stu-id="0d72b-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="0d72b-214">toocreate una chiave HSM protetta, set hello destinazione parametro too'HSM':</span><span class="sxs-lookup"><span data-stu-id="0d72b-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="0d72b-215">È possibile utilizzare hello successivo comando tooimport una chiave da un file con estensione PEM nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0d72b-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="0d72b-216">Questo comando consente di importare chiave hello in hello servizio insieme di credenziali chiave HSM:</span><span class="sxs-lookup"><span data-stu-id="0d72b-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="0d72b-217">comando successivo Hello Importa un "bring your own key" pacchetto (BYOK).</span><span class="sxs-lookup"><span data-stu-id="0d72b-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="0d72b-218">Ciò consente di generare la chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="0d72b-219">Per ulteriori istruzioni su come toogenerate il pacchetto BYOK, vedere [come toouse HSM-Protected chiavi insieme di credenziali chiave di Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0d72b-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="0d72b-220">Eliminare l'insieme di credenziali chiave hello e le chiavi associate e i segreti</span><span class="sxs-lookup"><span data-stu-id="0d72b-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="0d72b-221">Se non è più necessario insieme di credenziali chiave hello e hello chiave o il segreto in esso contenuti, è possibile eliminare l'insieme di credenziali chiave hello utilizzando hello `az keyvault delete` comando:</span><span class="sxs-lookup"><span data-stu-id="0d72b-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="0d72b-222">In alternativa, è possibile eliminare un gruppo di risorse di Azure intero, che include l'insieme di credenziali chiave di hello e altre risorse che incluso in tale gruppo:</span><span class="sxs-lookup"><span data-stu-id="0d72b-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="0d72b-223">Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure</span><span class="sxs-lookup"><span data-stu-id="0d72b-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="0d72b-224">Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d72b-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="0d72b-225">Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="0d72b-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="0d72b-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="0d72b-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="0d72b-227">Questo comando Visualizza un elenco completo delle proprietà per la chiave specificata hello:</span><span class="sxs-lookup"><span data-stu-id="0d72b-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="0d72b-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="0d72b-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="0d72b-229">Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="0d72b-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="0d72b-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="0d72b-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="0d72b-231">Di seguito è riportato un esempio di come tooremove una chiave specifica:</span><span class="sxs-lookup"><span data-stu-id="0d72b-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="0d72b-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="0d72b-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="0d72b-233">Di seguito è riportato un esempio di come tooremove un segreto specifico:</span><span class="sxs-lookup"><span data-stu-id="0d72b-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="0d72b-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="0d72b-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="0d72b-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d72b-235">Next steps</span></span>
<span data-ttu-id="0d72b-236">Per riferimenti sull'interfaccia della riga di comando di Azure per i comandi delle credenziali delle chiavi, vedere [Key Vault CLI reference](/cli/azure/keyvault) (Riferimento dell'interfaccia della riga di comando di Key Vault)</span><span class="sxs-lookup"><span data-stu-id="0d72b-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="0d72b-237">Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0d72b-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
