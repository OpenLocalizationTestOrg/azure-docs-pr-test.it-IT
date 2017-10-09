---
title: insieme di credenziali chiave di Azure usa CLI aaaManage | Documenti Microsoft
description: "Utilizzare questa attività comuni di esercitazione tooautomate nell'insieme di credenziali chiave usando hello CLI"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="f729f-103">Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="f729f-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="f729f-104">L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree.</span><span class="sxs-lookup"><span data-stu-id="f729f-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="f729f-105">Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="f729f-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="f729f-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f729f-106">Introduction</span></span>

<span data-ttu-id="f729f-107">Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato (un insieme di credenziali) in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="f729f-108">Illustra hello processo di toocreate interfaccia della riga di comando multipiattaforma di Azure utilizzando un insieme di credenziali che contiene una chiave o una password che è quindi possibile utilizzare con un'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="f729f-109">L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.</span><span class="sxs-lookup"><span data-stu-id="f729f-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="f729f-110">**Toocomplete tempo stimato:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="f729f-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="f729f-111">In questa esercitazione non include istruzioni su come toowrite hello applicazione Azure che uno dei passaggi di hello include, che mostra come tooauthorize un toouse applicazione una chiave o la chiave privata della chiave hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f729f-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="f729f-112">Attualmente, non è possibile configurare l'insieme di credenziali chiave di Azure nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="f729f-113">Seguire invece le istruzioni relative all'interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="f729f-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="f729f-114">In alternativa, per le istruzioni relative ad Azure PowerShell, vedere [questa esercitazione equivalente](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="f729f-115">Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f729f-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f729f-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f729f-116">Prerequisites</span></span>

<span data-ttu-id="f729f-117">toocomplete questa esercitazione, è necessario disporre di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f729f-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f729f-118">TooMicrosoft una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="f729f-119">Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="f729f-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="f729f-120">Interfaccia della riga di comando multipiattaforma versione 0.9.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f729f-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="f729f-121">tooinstall hello versione più recente e connettersi tooyour sottoscrizione di Azure, vedere [installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f729f-122">Un'applicazione che verrà configurato toouse hello chiave o password creati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f729f-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="f729f-123">Un'applicazione di esempio è disponibile da hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="f729f-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="f729f-124">Per istruzioni, vedere il file Leggimi di accompagnamento hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="f729f-125">Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f729f-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="f729f-126">In questa esercitazione si presuppone che si ha familiarità con l'interfaccia della riga di comando hello (Bash, Terminal, prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="f729f-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="f729f-127">Hello - Guida o -h parametro può essere utilizzato tooview della Guida in linea per i comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="f729f-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="f729f-128">In alternativa, help hello azure [comando] [opzioni] formato può essere anche usato tooreturn hello stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="f729f-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="f729f-129">Ad esempio, i comandi tutte restituito seguente hello hello stesse informazioni:</span><span class="sxs-lookup"><span data-stu-id="f729f-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="f729f-130">In caso di dubbi sui parametri hello necessari da un comando, fare riferimento tramite toohelp - help, -h o azure help [comando].</span><span class="sxs-lookup"><span data-stu-id="f729f-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="f729f-131">È inoltre possibile leggere hello seguenti esercitazioni tooget familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:</span><span class="sxs-lookup"><span data-stu-id="f729f-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="f729f-132">Come tooinstall e configurare l'interfaccia riga di comando multipiattaforma di Azure</span><span class="sxs-lookup"><span data-stu-id="f729f-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="f729f-133">Uso dell'interfaccia della riga di comando multipiattaforma di Azure con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f729f-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="f729f-134">Connettersi tooyour sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="f729f-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="f729f-135">toolog con un account aziendale, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f729f-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="f729f-136">o se si desidera toolog digitando in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="f729f-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="f729f-137">metodo di accesso Hello funziona solo con account aziendale.</span><span class="sxs-lookup"><span data-stu-id="f729f-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="f729f-138">L'account aziendale corrisponde a un utente gestito dall'organizzazione e definito nel tenant Azure Active Directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f729f-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="f729f-139">Se si dispone attualmente di un account aziendale e si utilizza un toolog account Microsoft in tooyour sottoscrizione di Azure, è possibile creare facilmente tramite hello i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f729f-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="f729f-140">Account di accesso toohello accesso toohello [il portale di gestione di Azure](https://manage.windowsazure.com/)e fare clic su Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f729f-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="f729f-141">Se è presente alcuna directory, selezionare la directory di creare e fornire hello informazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="f729f-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="f729f-142">Selezionare la directory e aggiungere un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="f729f-142">Select your directory and add a new user.</span></span> <span data-ttu-id="f729f-143">Questo nuovo utente corrisponde a un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="f729f-143">This new user is an organizational account.</span></span> <span data-ttu-id="f729f-144">Durante la creazione dell'utente hello hello verrà fornito con un indirizzo di posta elettronica per l'utente hello e una password temporanea.</span><span class="sxs-lookup"><span data-stu-id="f729f-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="f729f-145">Salvare queste informazioni perché verranno utilizzate in un altro passaggio.</span><span class="sxs-lookup"><span data-stu-id="f729f-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="f729f-146">Dal portale di hello, selezionare le impostazioni e quindi selezionare gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="f729f-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="f729f-147">Selezionare Aggiungi e aggiungere hello nuovo utente come coamministratore.</span><span class="sxs-lookup"><span data-stu-id="f729f-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="f729f-148">In questo modo hello account aziendale toomanage la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="f729f-149">Infine, disconnettersi hello portale di Azure e quindi accedere di nuovo utilizzando hello nuovo account aziendale.</span><span class="sxs-lookup"><span data-stu-id="f729f-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="f729f-150">Se si tratta di hello prima registrazione in tempo con questo account, sarà password hello toochange richiesta.</span><span class="sxs-lookup"><span data-stu-id="f729f-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="f729f-151">Per altre informazioni sull'uso dell'account aziendale con Microsoft Azure, vedere [Iscrizione ad Azure come organizzazione](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="f729f-152">Se si dispone di più sottoscrizioni e si desidera toospecify un uno toouse specifico per l'insieme di credenziali chiave di Azure, digitare hello sottoscrizioni hello toosee per l'account di seguito:</span><span class="sxs-lookup"><span data-stu-id="f729f-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="f729f-153">Quindi, toospecify hello sottoscrizione toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="f729f-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="f729f-154">Per ulteriori informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [come tooInstall e l'interfaccia della riga di comando multipiattaforma di Azure configurare](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="f729f-155">Opzione toousing Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f729f-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="f729f-156">insieme di credenziali chiave Hello richiede Gestione risorse di Azure, quindi digitare hello seguenti modalità di gestione risorse tooAzure tooswitch:</span><span class="sxs-lookup"><span data-stu-id="f729f-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="f729f-157">Creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f729f-157">Create a new resource group</span></span>
<span data-ttu-id="f729f-158">Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f729f-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="f729f-159">Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.</span><span class="sxs-lookup"><span data-stu-id="f729f-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="f729f-160">primo parametro Hello è il nome di gruppo di risorse e hello secondo parametro è il percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="f729f-161">Per il percorso, utilizzare il comando di hello `azure location list` tooidentify come toospecify toohello un percorso alternativo uno in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="f729f-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="f729f-162">Se servono altre informazioni, digitare: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="f729f-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="f729f-163">Registrazione provider di risorse hello insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="f729f-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="f729f-164">Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="f729f-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="f729f-165">Questa operazione deve solo toobe eseguito una volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f729f-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="f729f-166">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="f729f-166">Create a key vault</span></span>

<span data-ttu-id="f729f-167">Hello utilizzare `azure keyvault create` comando toocreate un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f729f-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="f729f-168">Questo script ha tre parametri obbligatori: il nome di un gruppo di risorse, un insieme di credenziali delle chiavi e la posizione geografica di hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="f729f-169">Ad esempio, se si utilizza il nome dell'insieme di credenziali hello di ContosoKeyVault, nome gruppo di risorse hello di ContosoResourceGroup e il percorso di hello dell'Asia orientale, digitare:</span><span class="sxs-lookup"><span data-stu-id="f729f-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="f729f-170">output di Hello di questo comando Mostra le proprietà dell'insieme di credenziali chiave hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="f729f-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="f729f-171">proprietà di Hello due più importanti sono:</span><span class="sxs-lookup"><span data-stu-id="f729f-171">hello two most important properties are:</span></span>

* <span data-ttu-id="f729f-172">**Nome**: nell'esempio hello tratta ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="f729f-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="f729f-173">Questo nome verrà usato per altri cmdlet di insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="f729f-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="f729f-174">**vaultUri**: nell'esempio hello tratta https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="f729f-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="f729f-175">Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.</span><span class="sxs-lookup"><span data-stu-id="f729f-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="f729f-176">L'account di Azure è ora autorizzato tooperform insieme di credenziali di qualsiasi operazione su questa chiave.</span><span class="sxs-lookup"><span data-stu-id="f729f-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="f729f-177">Nessun altro lo è ancora.</span><span class="sxs-lookup"><span data-stu-id="f729f-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="f729f-178">Aggiungere una chiave o un insieme di credenziali chiave segreta toohello</span><span class="sxs-lookup"><span data-stu-id="f729f-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="f729f-179">Se si desidera toocreate insieme credenziali chiavi Azure una chiave protetta tramite software per l'utente, utilizzare hello `azure key create` comandi e digitare il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="f729f-180">Tuttavia, se si dispone di una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si desidera tooupload tooAzure insieme di credenziali chiave, digitare hello seguenti chiave hello tooimport dagli hello. File con estensione PEM, che protegge hello chiave tramite software nel servizio insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="f729f-181">È ora possibile fare riferimento chiave hello creati o caricati tooAzure insieme di credenziali chiave utilizzando il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="f729f-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="f729f-182">Utilizzare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways ottenere la versione corrente di hello e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tale versione.</span><span class="sxs-lookup"><span data-stu-id="f729f-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="f729f-183">tooadd un insieme di credenziali toohello segreto, che è una password denominata SQLPassword e con valore hello Pa$ $w0rd tooAzure insieme di credenziali chiave hello tipo seguente:</span><span class="sxs-lookup"><span data-stu-id="f729f-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="f729f-184">È ora possibile fare riferimento a questa password che sono state aggiunte tooAzure insieme di credenziali chiave, tramite il relativo URI.</span><span class="sxs-lookup"><span data-stu-id="f729f-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="f729f-185">Utilizzare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways ottenere la versione corrente di hello e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tale versione.</span><span class="sxs-lookup"><span data-stu-id="f729f-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="f729f-186">Si considerino hello chiave o il segreto appena creato:</span><span class="sxs-lookup"><span data-stu-id="f729f-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="f729f-187">tooview il tipo di chiave,:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f729f-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="f729f-188">tooview segreto, tipo:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f729f-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="f729f-189">Registrare un'applicazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f729f-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="f729f-190">Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato.</span><span class="sxs-lookup"><span data-stu-id="f729f-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="f729f-191">Non è tooAzure specifico insieme di credenziali chiave ma è incluso in questo caso, per motivi di completezza.</span><span class="sxs-lookup"><span data-stu-id="f729f-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f729f-192">esercitazione hello toocomplete, l'account, insieme di credenziali hello e un'applicazione hello che verrà registrato in questo passaggio deve essere in hello stessa directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="f729f-193">Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f729f-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="f729f-194">toodo, hello proprietario di un'applicazione hello deve innanzitutto registrare l'applicazione hello in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f729f-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="f729f-195">Alla fine di hello della registrazione, proprietario dell'applicazione hello Ottiene hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="f729f-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="f729f-196">Un **ID applicazione** (noto anche come un ID Client) e **chiave di autenticazione** (noto anche come hello segreto condiviso).</span><span class="sxs-lookup"><span data-stu-id="f729f-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="f729f-197">un'applicazione Hello deve presentare entrambi questi tooAzure valori tooget un token di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f729f-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="f729f-198">Come un'applicazione hello viene configurato toodo che ciò dipende dall'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="f729f-199">Per l'applicazione di esempio insieme di credenziali chiave hello, proprietario dell'applicazione hello imposta questi valori nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="f729f-200">applicazione hello tooregister in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="f729f-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="f729f-201">Accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="f729f-202">A sinistra di hello, fare clic su **Active Directory**, quindi selezionare hello directory in cui è necessario registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f729f-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="f729f-203">È necessario selezionare hello stessa directory che contiene hello sottoscrizione di Azure con cui è stato creato l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f729f-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="f729f-204">Non si conosce la directory in questo caso, fare clic su **impostazioni**, identificare hello sottoscrizione con cui è stato creato l'insieme di credenziali chiave e il nome di hello nota della directory hello visualizzato nell'ultima colonna hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="f729f-205">Fare clic su **APPLICAZIONI**.</span><span class="sxs-lookup"><span data-stu-id="f729f-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="f729f-206">Se nessuna App è stati aggiunti tooyour directory, questa pagina mostrerà solo hello **aggiungere un'App** collegamento.</span><span class="sxs-lookup"><span data-stu-id="f729f-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="f729f-207">Fare clic sul collegamento hello o in alternativa, è possibile fare clic su hello **aggiungere** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f729f-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="f729f-208">In hello **Aggiungi applicazione** procedura guidata hello **cosa si desidera toodo?** pagina, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="f729f-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="f729f-209">In hello **informazioni sull'applicazione** pagina, specificare un nome per l'applicazione e selezionare **applicazione WEB, e/o API WEB** (hello predefinito).</span><span class="sxs-lookup"><span data-stu-id="f729f-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="f729f-210">Fare clic sull'icona Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="f729f-211">In hello **proprietà App** specificare hello **URL accesso** e **URI ID APP** per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="f729f-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="f729f-212">Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle).</span><span class="sxs-lookup"><span data-stu-id="f729f-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="f729f-213">Non è importante se esistono di questi siti. aspetto importante è che URI ID app hello per ogni applicazione è diverso per ogni applicazione nella directory.</span><span class="sxs-lookup"><span data-stu-id="f729f-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="f729f-214">directory Hello usato tooidentify questa stringa l'app.</span><span class="sxs-lookup"><span data-stu-id="f729f-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="f729f-215">Fare clic su hello icona completata toosave le modifiche apportate nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="f729f-216">Nella pagina introduttiva hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="f729f-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="f729f-217">Scorrere toohello **chiavi** sezione, selezionare la durata hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f729f-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="f729f-218">pagina Hello viene aggiornato e verrà visualizzato un valore di chiave.</span><span class="sxs-lookup"><span data-stu-id="f729f-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="f729f-219">È necessario configurare l'applicazione con questo valore di chiave e hello **ID CLIENT** valore.</span><span class="sxs-lookup"><span data-stu-id="f729f-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="f729f-220">Le istruzioni per questa configurazione saranno specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f729f-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="f729f-221">Copiare valore dell'ID di hello client dalla pagina, che verrà utilizzato in hello successivo passaggio tooset le autorizzazioni per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f729f-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="f729f-222">Autorizzare hello applicazione toouse hello chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="f729f-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="f729f-223">tooauthorize hello applicazione tooaccess hello chiave o al segreto nell'insieme di credenziali hello, utilizzare hello `azure keyvault set-policy` comando.</span><span class="sxs-lookup"><span data-stu-id="f729f-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="f729f-224">Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e hello applicazione cui si desidera tooauthorize ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si desidera tooauthorize hello applicazione toodecrypt e accedere con le chiavi nell'insieme di credenziali, quindi eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f729f-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="f729f-225">Se si esegue nel prompt dei comandi di Windows, si devono sostituire le virgolette singole con le virgolette doppie e anche di escape doppie interno hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="f729f-226">Ad esempio: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="f729f-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="f729f-227">Se si desiderano che stessi segreti tooread applicazione tooauthorize nell'insieme di credenziali, eseguire hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="f729f-228">Se si desidera toouse un modulo di protezione hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="f729f-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="f729f-229">Per maggiore sicurezza, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello.</span><span class="sxs-lookup"><span data-stu-id="f729f-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="f729f-230">Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato.</span><span class="sxs-lookup"><span data-stu-id="f729f-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="f729f-231">Se questo requisito non si applica a tooyou, ignorare questa sezione e passare troppo[Elimina insieme di credenziali chiave hello e le chiavi associate e i segreti](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="f729f-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="f729f-232">toocreate queste chiavi HSM protette, è necessario avere una sottoscrizione di insieme di credenziali che supporta chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="f729f-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="f729f-233">Quando si crea keyvault hello, aggiungere il parametro 'sku' hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="f729f-234">È possibile aggiungere le chiavi protette tramite software (come illustrato in precedenza) e l'insieme di credenziali delle chiavi HSM protette toothis.</span><span class="sxs-lookup"><span data-stu-id="f729f-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="f729f-235">toocreate una chiave HSM protetta, set hello destinazione parametro too'HSM':</span><span class="sxs-lookup"><span data-stu-id="f729f-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="f729f-236">È possibile utilizzare hello successivo comando tooimport una chiave da un file con estensione PEM nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f729f-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="f729f-237">Questo comando consente di importare chiave hello in hello servizio insieme di credenziali chiave HSM:</span><span class="sxs-lookup"><span data-stu-id="f729f-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="f729f-238">comando successivo Hello Importa un "bring your own key" pacchetto (BYOK).</span><span class="sxs-lookup"><span data-stu-id="f729f-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="f729f-239">Ciò consente di generare la chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="f729f-240">Per ulteriori istruzioni su come toogenerate il pacchetto BYOK, vedere [come toouse HSM-Protected chiavi insieme di credenziali chiave di Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="f729f-241">Eliminare l'insieme di credenziali chiave hello e le chiavi associate e i segreti</span><span class="sxs-lookup"><span data-stu-id="f729f-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="f729f-242">Se non è più necessario insieme di credenziali chiave hello e hello chiave o il segreto in esso contenuti, è possibile eliminare l'insieme di credenziali chiave hello tramite comando di eliminazione keyvault hello azure:</span><span class="sxs-lookup"><span data-stu-id="f729f-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="f729f-243">In alternativa, è possibile eliminare un gruppo di risorse di Azure intero, che include l'insieme di credenziali chiave di hello e altre risorse che incluso in tale gruppo:</span><span class="sxs-lookup"><span data-stu-id="f729f-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="f729f-244">Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure</span><span class="sxs-lookup"><span data-stu-id="f729f-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="f729f-245">Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f729f-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="f729f-246">Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="f729f-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="f729f-247">Questo comando Visualizza un elenco completo delle proprietà per la chiave specificata hello:</span><span class="sxs-lookup"><span data-stu-id="f729f-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="f729f-248">Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:</span><span class="sxs-lookup"><span data-stu-id="f729f-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="f729f-249">Di seguito è riportato un esempio di come tooremove una chiave specifica:</span><span class="sxs-lookup"><span data-stu-id="f729f-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="f729f-250">Di seguito è riportato un esempio di come tooremove un segreto specifico:</span><span class="sxs-lookup"><span data-stu-id="f729f-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="f729f-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f729f-251">Next steps</span></span>
<span data-ttu-id="f729f-252">Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f729f-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

