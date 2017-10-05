---
title: Gestire Azure Key Vault tramite l'interfaccia della riga di comando | Microsoft Docs
description: "Usare questa esercitazione per automatizzare le attività comuni nell'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="8cdb5-103">Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8cdb5-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="8cdb5-104">L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="8cdb5-105">Per altre informazioni, vedere la [pagina Insieme di credenziali delle chiavi - Prezzi](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="8cdb5-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8cdb5-106">Introduction</span></span>

<span data-ttu-id="8cdb5-107">Usare questa esercitazione per imparare a eseguire facilmente le attività iniziali dell'insieme di credenziali delle chiavi di Azure per creare un contenitore finalizzato (insieme di credenziali) in Azure, in cui archiviare e gestire chiavi crittografiche e segreti in Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="8cdb5-108">Verrà inoltre descritto come usare l'interfaccia della riga di comando multipiattaforma di Azure per creare un insieme di credenziali contenente una chiave o una password che sarà possibile usare con un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="8cdb5-109">L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="8cdb5-110">**Tempo previsto per il completamento:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="8cdb5-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="8cdb5-111">Questa esercitazione non include istruzioni su come scrivere l'applicazione Azure usata nel passaggio che spiega come autorizzare un'applicazione all'uso di una chiave o un segreto nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="8cdb5-112">Attualmente non è possibile configurare l'insieme di credenziali delle chiavi di Azure nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="8cdb5-113">Seguire invece le istruzioni relative all'interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="8cdb5-114">In alternativa, per le istruzioni relative ad Azure PowerShell, vedere [questa esercitazione equivalente](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="8cdb5-115">Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="8cdb5-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cdb5-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8cdb5-116">Prerequisites</span></span>

<span data-ttu-id="8cdb5-117">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8cdb5-118">Una sottoscrizione a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="8cdb5-119">Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="8cdb5-120">Interfaccia della riga di comando multipiattaforma versione 0.9.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="8cdb5-121">Per installare l'ultima versione e associarla alla sottoscrizione di Azure, vedere [Installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="8cdb5-122">Un'applicazione che verrà configurata per usare la chiave o la password creata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="8cdb5-123">Un'applicazione di esempio è disponibile nell'[Area download Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="8cdb5-124">Per istruzioni, vedere il file Readme associato.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="8cdb5-125">Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8cdb5-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="8cdb5-126">Questa esercitazione si presuppone che si abbia familiarità con l'interfaccia della riga di comando (Bash, terminal, prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="8cdb5-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="8cdb5-127">Il parametro --help o -h consente di visualizzare la Guida per specifici comandi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="8cdb5-128">In alternativa, è anche possibile utilizzare il formato azure help [comando] [opzioni] per ottenere le stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="8cdb5-129">Ad esempio, tutti i comandi seguenti restituiranno le stesse informazioni:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="8cdb5-130">In caso di dubbi sui parametri necessari per un comando, fare riferimento alla Guida utilizzando --help, -h o azure help [comando].</span><span class="sxs-lookup"><span data-stu-id="8cdb5-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="8cdb5-131">È consigliabile di leggere anche le seguenti esercitazioni per acquisire familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="8cdb5-132">Installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="8cdb5-133">Uso dell'interfaccia della riga di comando multipiattaforma di Azure con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8cdb5-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="8cdb5-134">Connettersi alle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="8cdb5-134">Connect to your subscriptions</span></span>

<span data-ttu-id="8cdb5-135">Per accedere utilizzando un account aziendale, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="8cdb5-136">Se invece si vuole accedere digitando in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="8cdb5-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="8cdb5-137">Il metodo di accesso funziona solo con l'account aziendale.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-137">The login method only works with organizational account.</span></span> <span data-ttu-id="8cdb5-138">L'account aziendale corrisponde a un utente gestito dall'organizzazione e definito nel tenant Azure Active Directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="8cdb5-139">Se non si dispone di un account aziendale e si usa un account Microsoft per accedere alla sottoscrizione di Azure, è possibile crearne facilmente uno utilizzando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="8cdb5-140">Accedere al [portale di gestione di Azure](https://manage.windowsazure.com/)e fare clic su Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="8cdb5-141">Se non esistono directory, selezionare Crea directory e fornire le informazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="8cdb5-142">Selezionare la directory e aggiungere un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-142">Select your directory and add a new user.</span></span> <span data-ttu-id="8cdb5-143">Questo nuovo utente corrisponde a un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-143">This new user is an organizational account.</span></span> <span data-ttu-id="8cdb5-144">Durante la creazione dell'utente, verranno forniti un indirizzo di posta elettronica e una password provvisoria.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="8cdb5-145">Salvare queste informazioni perché verranno utilizzate in un altro passaggio.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="8cdb5-146">Nel portale selezionare Impostazioni e quindi Amministratori.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="8cdb5-147">Selezionare Aggiungi e aggiungere il nuovo utente come co-amministratore.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="8cdb5-148">In questo modo l'account aziendale potrà gestire la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="8cdb5-149">Infine, disconnettersi dal portale Azure ed effettuare di nuovo l'accesso con il nuovo account aziendale.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="8cdb5-150">La prima volta che si accede con questo account verrà richiesto di cambiare la password.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="8cdb5-151">Per altre informazioni sull'uso dell'account aziendale con Microsoft Azure, vedere [Iscrizione ad Azure come organizzazione](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="8cdb5-152">Se si dispone di più sottoscrizioni e se ne vuole specificare una in particolare da usare per l'insieme di credenziali delle chiavi di Azure, digitare quanto segue per visualizzare le sottoscrizioni per il proprio account:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="8cdb5-153">Quindi, per specificare la sottoscrizione da usare, digitare.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="8cdb5-154">Per altre informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [Installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="8cdb5-155">Passare all'uso di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8cdb5-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="8cdb5-156">Poiché per l'insieme di credenziali delle chiavi è necessario Gestione risorse di Azure, digitare quanto segue per passare alla modalità Gestione risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="8cdb5-157">Creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8cdb5-157">Create a new resource group</span></span>
<span data-ttu-id="8cdb5-158">Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="8cdb5-159">Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="8cdb5-160">Il primo parametro è il nome del gruppo di risorse e il secondo è la posizione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="8cdb5-161">Per la posizione usare il comando `azure location list` per identificare come si specifica una posizione alternativa a quella di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="8cdb5-162">Se servono altre informazioni, digitare: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="8cdb5-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="8cdb5-163">Registrare il provider di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8cdb5-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="8cdb5-164">Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="8cdb5-165">Quest'operazione deve essere eseguita una volta sola per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="8cdb5-166">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8cdb5-166">Create a key vault</span></span>

<span data-ttu-id="8cdb5-167">Usare il comando `azure keyvault create` per creare un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="8cdb5-168">Questo script ha tre parametri obbligatori: un nome del gruppo di risorse, un nome dell'insieme di credenziali delle chiavi e la località geografica.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="8cdb5-169">Ad esempio, se si usa il nome dell'insieme di credenziali ContosoKeyVault, il nome del gruppo di risorse ContosoResourceGroup e la posizione East Asia, digitare:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="8cdb5-170">L'output di questo comando mostra le proprietà dell'insieme di credenziali delle chiavi appena creato.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="8cdb5-171">Le due proprietà più importanti sono:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-171">The two most important properties are:</span></span>

* <span data-ttu-id="8cdb5-172">**Name**: nell'esempio corrisponde a ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="8cdb5-173">Questo nome verrà usato per altri cmdlet di insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="8cdb5-174">**vaultUri**: nell'esempio corrisponde a https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="8cdb5-175">Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="8cdb5-176">L'account Azure ora è autorizzato a eseguire qualsiasi operazione su questo insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="8cdb5-177">Nessun altro lo è ancora.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="8cdb5-178">Aggiungere una chiave o un segreto all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8cdb5-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="8cdb5-179">Per usare l'insieme di credenziali delle chiavi di Azure per creare automaticamente una chiave protetta tramite software, eseguire il comando `azure key create` e digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="8cdb5-180">Tuttavia, se si ha una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si vuole caricare nell'insieme di credenziali delle chiavi di Azure, digitare il comando seguente per importare la chiave dal file PEM che protegge la chiave tramite software nel servizio dell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="8cdb5-181">A questo punto è possibile fare riferimento alla chiave creata o caricata nell'insieme di credenziali delle chiavi di Azure, usando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="8cdb5-182">Usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** per ottenere sempre la versione corrente e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** per ottenere questa versione specifica.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="8cdb5-183">Per aggiungere un segreto all'insieme di credenziali, ovvero una password denominata SQLPassword con il valore Pa$$w0rd per l'insieme di credenziali delle chiavi, digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="8cdb5-184">È ora possibile fare riferimento a questa password aggiunta nell'insieme di credenziali delle chiavi di Azure, usando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="8cdb5-185">Usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** per ottenere sempre la versione corrente e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** per ottenere questa versione specifica.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="8cdb5-186">Ora si può visualizzare la chiave o il segreto appena creato:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="8cdb5-187">Per visualizzare la chiave, digitare: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="8cdb5-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="8cdb5-188">Per visualizzare il segreto, digitare: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="8cdb5-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="8cdb5-189">Registrare un'applicazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cdb5-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="8cdb5-190">Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="8cdb5-191">Anche se non è specifico dell'insieme di credenziali delle chiavi di Azure, viene incluso qui per completezza.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cdb5-192">Per completare l'esercitazione, l'account, l'insieme di credenziali e l'applicazione in cui si registrerà questo passaggio devono essere tutti nella stessa directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="8cdb5-193">Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="8cdb5-194">A tale scopo, il proprietario dell'applicazione deve innanzitutto registrare l'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="8cdb5-195">Al termine della registrazione, il proprietario dell'applicazione ottiene i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="8cdb5-196">Un **ID applicazione** (chiamato anche ID client) e una **chiave di autenticazione** (chiamata anche segreto condiviso).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="8cdb5-197">L'applicazione deve presentare entrambi questi valori ad Azure Active Directory per ottenere un token.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="8cdb5-198">La configurazione dell'applicazione per eseguire questa operazione dipende dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="8cdb5-199">Per l'applicazione di esempio dell'insieme di credenziali delle chiavi, il proprietario dell'applicazione imposta questi valori nel file app.config.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="8cdb5-200">Per registrare l'applicazione in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="8cdb5-201">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="8cdb5-202">A sinistra fare clic su **Active Directory**e quindi selezionare la directory in cui si registrerà l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="8cdb5-203">È necessario selezionare la stessa directory che contiene la sottoscrizione di Azure con cui è stato creato l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="8cdb5-204">Se non si sa quale directory selezionare, fare clic su **Impostazioni**, identificare la sottoscrizione con cui si è creato l'insieme di credenziali chiave e prendere nota del nome della directory visualizzata nell'ultima colonna.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="8cdb5-205">Fare clic su **APPLICAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="8cdb5-206">Se nessuna app è stata aggiunta alla directory, in questa pagina sarà visualizzato solo il collegamento **Aggiungi un'app**.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="8cdb5-207">Fare clic sul collegamento. In alternativa, è possibile fare clic su **AGGIUNGI** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="8cdb5-208">Nella pagina **Come procedere** della procedura guidata **AGGIUNGI APPLICAZIONE** fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="8cdb5-209">Nella pagina **Informazioni sull'applicazione** specificare un nome per l'applicazione e selezionare **APPLICAZIONE WEB E/O API WEB** (opzione predefinita).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="8cdb5-210">Fare clic sull'icona Avanti.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-210">Click the Next icon.</span></span>
6. <span data-ttu-id="8cdb5-211">Nella pagina **Proprietà dell'app** specificare **URL ACCESSO** e **URI ID APP** per l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="8cdb5-212">Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="8cdb5-213">Non è importante se questi siti esistono. Ciò che conta è che ogni applicazione nella directory abbia un URI ID app diverso.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="8cdb5-214">La directory usa questa stringa per identificare l'app.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="8cdb5-215">Fare clic sull'icona Completa per salvare le modifiche nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="8cdb5-216">Nella pagina Avvio rapido fare clic su **CONFIGURA**.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="8cdb5-217">Scorrere fino alla sezione **chiavi**, selezionare la durata e quindi fare clic su **SALVA**.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="8cdb5-218">La pagina viene aggiornata e mostra un valore chiave.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="8cdb5-219">È necessario configurare l'applicazione con questo valore chiave e con il valore **ID CLIENT** .</span><span class="sxs-lookup"><span data-stu-id="8cdb5-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="8cdb5-220">Le istruzioni per questa configurazione saranno specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="8cdb5-221">Copiare da questa pagina il valore dell'ID client che si userà nel passaggio successivo per impostare le autorizzazioni per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="8cdb5-222">Autorizzare l'applicazione a usare la chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="8cdb5-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="8cdb5-223">Per autorizzare l'accesso da parte dell'applicazione alla chiave o al segreto nell'insieme di credenziali, usare il comando `azure keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="8cdb5-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="8cdb5-224">Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e l'applicazione che si desidera autorizzare ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si vuole autorizzare l'applicazione a decrittografare e firmare con le chiavi dell'insieme di credenziali, eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="8cdb5-225">Se si eseguono prompt dei comandi di Windows, sostituire le virgolette singole con virgolette doppie e aggiungere il carattere di escape prima delle virgolette doppie interne.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="8cdb5-226">Ad esempio: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="8cdb5-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="8cdb5-227">Se si desidera autorizzare la stessa applicazione per la lettura di tutti i segreti nell'insieme di credenziali, eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="8cdb5-228">Per usare un modulo di protezione hardware</span><span class="sxs-lookup"><span data-stu-id="8cdb5-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="8cdb5-229">Per una maggiore sicurezza, è possibile importare o generare le chiavi in moduli di protezione hardware (HSM) che rimangono sempre entro il limite HSM.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="8cdb5-230">I moduli di protezione hardware sono certificati per FIPS 140-2 livello 2.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="8cdb5-231">Se questo requisito non è applicabile, saltare questa sezione e andare a [Eliminare l'insieme di credenziali delle chiavi e le chiavi e i segreti associati](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="8cdb5-232">Per creare queste chiavi HSM protette, è necessaria una sottoscrizione all'insieme di credenziali che supporti le chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="8cdb5-233">Quando si crea l'insieme di credenziali, aggiungere il parametro 'sku':</span><span class="sxs-lookup"><span data-stu-id="8cdb5-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="8cdb5-234">È possibile aggiungere a questo insieme di credenziali chiavi protette tramite software (come illustrato in precedenza) e chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="8cdb5-235">Per creare una chiave HSM protetta, impostare il parametro Destination su 'HSM':</span><span class="sxs-lookup"><span data-stu-id="8cdb5-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="8cdb5-236">È possibile usare il comando seguente per importare una chiave da un file con estensione PEM nel computer.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="8cdb5-237">Questo comando importa la chiave nei moduli HSM nel servizio dell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="8cdb5-238">Il comando successivo importa un pacchetto "bring your own key" (BYOK).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="8cdb5-239">Ciò consente di generare la chiave nel modulo HSM locale e di trasferirlo in moduli HSM nel servizio dell'insieme di credenziali delle chiavi, senza che la chiave esca dal limite HSM:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="8cdb5-240">Per istruzioni più dettagliate su come generare questo pacchetto BYOK, vedere [Come usare chiavi HSM protette con l'insieme di credenziali delle chiavi di Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="8cdb5-241">Eliminare l'insieme di credenziali delle chiavi e le chiavi e i segreti associati</span><span class="sxs-lookup"><span data-stu-id="8cdb5-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="8cdb5-242">Se l'insieme di credenziali delle chiavi e la chiave o il segreto associato non sono più necessari, è possibile eliminare l'insieme di credenziali delle chiavi usando il comando azure keyvault delete:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="8cdb5-243">In alternativa, è possibile eliminare l'intero gruppo di risorse di Azure, che include l'insieme di credenziali delle chiavi e tutte le altre risorse incluse in quel gruppo:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="8cdb5-244">Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure</span><span class="sxs-lookup"><span data-stu-id="8cdb5-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="8cdb5-245">Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdb5-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="8cdb5-246">Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="8cdb5-247">Questo comando visualizza un elenco completo di proprietà per la chiave specificata:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="8cdb5-248">Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="8cdb5-249">Ecco un esempio di come rimuovere una chiave specifica:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="8cdb5-250">Ecco un esempio di come rimuovere un segreto specifico:</span><span class="sxs-lookup"><span data-stu-id="8cdb5-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="8cdb5-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8cdb5-251">Next steps</span></span>
<span data-ttu-id="8cdb5-252">Per i riferimenti alla programmazione, vedere [Guida per gli sviluppatori dell’insieme di credenziali chiave Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="8cdb5-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

