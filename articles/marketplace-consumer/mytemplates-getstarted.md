---
title: aaaGet un'introduzione ai modelli privati | Documenti Microsoft
description: Aggiungere, gestire e condividere i modelli privati utilizzando hello portale di Azure, hello CLI di Azure o PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="ff8e5-103">Introduzione a modelli privati su hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ff8e5-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="ff8e5-104">Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modello è un modello dichiarativo utilizzato toodefine la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="ff8e5-105">È possibile definire hello toodeploy di risorse per una soluzione e specificare i parametri e variabili che consentono valori tooinput per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="ff8e5-106">Hello costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="ff8e5-107">È possibile usare hello nuovo **modelli** funzionalità hello [portale Azure](https://portal.azure.com) insieme hello **Microsoft.Gallery** provider di risorse come estensione di hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable utenti toocreate, gestire e distribuire modelli privati da una libreria personale.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="ff8e5-108">Questo documento illustra la procedura aggiunta, la gestione e condivisione privata **modello** utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="ff8e5-109">Indicazioni</span><span class="sxs-lookup"><span data-stu-id="ff8e5-109">Guidance</span></span>
<span data-ttu-id="ff8e5-110">Hello suggerimenti seguenti consentono di sfruttare appieno **modelli** quando si lavora con le soluzioni:</span><span class="sxs-lookup"><span data-stu-id="ff8e5-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="ff8e5-111">Un **modello** è una risorsa di incapsulamento contenente un modello di Resource Manager e metadati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="ff8e5-112">Si comporta in modo molto simile elemento tooan hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="ff8e5-113">la differenza principale Hello è che è un elemento privato come elementi del Marketplace pubblici toohello anziché.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="ff8e5-114">Hello **modelli** libreria funziona anche per gli utenti che richiedono toocustomize le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="ff8e5-115">**modelli** permettono di usare un repository semplice all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="ff8e5-116">Iniziare con un modello di Resource Manager esistente.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="ff8e5-117">In [GitHub](https://github.com/Azure/azure-quickstart-templates) o nel post di blog relativo all'[esportazione modelli](../azure-resource-manager/resource-manager-export-template.md) è possibile trovare modelli a partire da un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="ff8e5-118">**Modelli** toohello collegati gli utenti che li pubblica.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="ff8e5-119">nome del server di pubblicazione Hello è visibile tooeveryone che dispone di accesso in lettura tooit.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="ff8e5-120">**modelli** sono risorse di Resource Manager e non possono essere rinominati dopo la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="ff8e5-121">Aggiungere una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-121">Add a Template resource</span></span>
<span data-ttu-id="ff8e5-122">Esistono due modi toocreate un **modello** risorsa nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="ff8e5-123">Metodo 1: creare una nuova risorsa modello da un gruppo di risorse in esecuzione</span><span class="sxs-lookup"><span data-stu-id="ff8e5-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="ff8e5-124">Passare tooan gruppo di risorse esistente nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="ff8e5-125">In **Impostazioni** selezionare **Esporta modello**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="ff8e5-126">Dopo aver esportato il modello di gestione risorse di hello, utilizzare hello **Salva modello** toosave pulsante è toohello **modelli** repository.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="ff8e5-127">Per informazioni dettagliate sull'esportazione di modelli, vedere questa [pagina](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="ff8e5-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="ff8e5-128">
   ![Esportazione di un gruppo di risorse](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="ff8e5-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="ff8e5-129">Seleziona hello **salvare tooTemplate** pulsante di comando.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="ff8e5-130">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="ff8e5-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="ff8e5-131">Name: nome dell'oggetto modello hello (Nota: questo è un nome di base di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="ff8e5-132">È soggetto a tutte le limitazioni relative all'assegnazione dei nomi non può essere modificato dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="ff8e5-133">Descrizione: riepilogo rapido sul modello hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-133">Description – Quick summary about hello template.</span></span>
     
     ![Salva modello](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="ff8e5-135">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ff8e5-136">Hello pannello modello esportazione Mostra notifiche quando il modello di gestione delle risorse esportato hello presenta errori, ma sarà comunque in grado di toosave questo toohello modello di gestione risorse modelli.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="ff8e5-137">Assicurarsi di controllare e correggere problemi nel modello un gestore delle risorse prima di ridistribuzione hello esportata modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="ff8e5-138">Metodo 2: aggiungere una nuova risorsa modello dall'esplorazione</span><span class="sxs-lookup"><span data-stu-id="ff8e5-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="ff8e5-139">È inoltre possibile aggiungere un nuovo **modello** da zero utilizzando hello + Aggiungi pulsante di comando in **Sfoglia > modelli**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="ff8e5-140">Tooprovide sarà necessario un nome, descrizione e il modello di gestione risorse JSON hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Aggiungi modello](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="ff8e5-142">Microsoft.Gallery è un provider di risorse di Azure basato su tenant.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="ff8e5-143">Hello risorsa modello è abbinato toohello utente che lo ha creato.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="ff8e5-144">Non è vincolata tooany specifica sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="ff8e5-145">Una sottoscrizione deve toobe scelte solo durante la distribuzione di un modello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="ff8e5-146">Visualizzare le risorse modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-146">View Template resources</span></span>
<span data-ttu-id="ff8e5-147">Tutti **modelli** tooyou disponibili possono essere visualizzati in **Sfoglia > modelli**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="ff8e5-148">Sono inclusi i **modelli** creati dall'utente e quelli condivisi con l'utente a vari livelli di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="ff8e5-149">Altre informazioni, vedere hello [il controllo degli accessi](#access-control-for-a-tenant-resource-provider) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Visualizza modello](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="ff8e5-151">È possibile visualizzare i dettagli di hello di un **modello** facendo clic in un elemento nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Visualizza modello](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="ff8e5-153">Modificare una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-153">Edit a Template resource</span></span>
<span data-ttu-id="ff8e5-154">È possibile avviare il flusso di modifica hello per un **modello** dall'elemento di hello facendo clic su elenco hello o scegliendo pulsante di comando di modifica hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Modifica modello](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="ff8e5-156">È possibile modificare la descrizione hello o il testo del modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="ff8e5-157">È possibile modificare il nome di hello perché è un nome di risorsa di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="ff8e5-158">Quando si modifica il modello di gestione risorse di hello JSON è convaliderà tooensure è costituito da un oggetto JSON valido.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="ff8e5-159">Scegliere **OK** e quindi **salvare** toosave il modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Modifica modello](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="ff8e5-161">Una volta hello **modello** viene salvato verrà visualizzata una notifica di conferma.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Modifica modello](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="ff8e5-163">Distribuire una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-163">Deploy a Template resource</span></span>
<span data-ttu-id="ff8e5-164">È possibile distribuire qualsiasi **modello** per cui si hanno autorizzazioni di **lettura**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="ff8e5-165">flusso di distribuzione Hello avvia pannello distribuzione il modello di Azure standard di hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="ff8e5-166">Compilare i valori hello per hello tooproceed parametri modello di gestione delle risorse con la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Modello di distribuzione](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="ff8e5-168">Condividere una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-168">Share a Template resource</span></span>
<span data-ttu-id="ff8e5-169">È possibile condividere le risorse **modello** con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="ff8e5-170">Condivisione presenta un comportamento simile troppo[assegnazione di ruolo per qualsiasi risorsa di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ff8e5-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="ff8e5-171">Hello **modello** proprietario fornisce le autorizzazioni tooother gli utenti possono interagire con una risorsa di modello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="ff8e5-172">Hello persona o il gruppo di utenti condividere hello **modello** sarà in grado di toosee modello di gestione risorse di hello e le relative proprietà di raccolta.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="ff8e5-173">Controllo di accesso per le risorse Microsoft.Gallery hello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="ff8e5-174">Ruolo</span><span class="sxs-lookup"><span data-stu-id="ff8e5-174">Role</span></span> | <span data-ttu-id="ff8e5-175">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="ff8e5-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="ff8e5-176">Proprietario</span><span class="sxs-lookup"><span data-stu-id="ff8e5-176">Owner</span></span> |<span data-ttu-id="ff8e5-177">Consente il controllo completo su una risorsa modello di hello inclusi condivisione</span><span class="sxs-lookup"><span data-stu-id="ff8e5-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="ff8e5-178">Reader</span><span class="sxs-lookup"><span data-stu-id="ff8e5-178">Reader</span></span> |<span data-ttu-id="ff8e5-179">Consente di lettura ed Execute(Deploy) su hello risorsa modello</span><span class="sxs-lookup"><span data-stu-id="ff8e5-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="ff8e5-180">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="ff8e5-180">Contributor</span></span> |<span data-ttu-id="ff8e5-181">Consente l'autorizzazione per modificare ed eliminare hello risorse modello.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="ff8e5-182">Utente non può condividere hello modello con altri utenti</span><span class="sxs-lookup"><span data-stu-id="ff8e5-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="ff8e5-183">Selezionare **condivisione** sull'elemento di visualizzazione hello facendo clic o nel Pannello di visualizzazione hello di un elemento specifico.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="ff8e5-184">Verrà avviata la condivisione.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-184">This launches a Share experience.</span></span>

![Condividi modello](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="ff8e5-186">È ora possibile scegliere un ruolo e un utente o gruppo tooprovide accesso tooa particolare **modello**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="ff8e5-187">i ruoli disponibili Hello sono proprietario, il lettore e collaboratore.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="ff8e5-188">Altre informazioni, vedere hello [il controllo degli accessi](#access-control-for-a-tenant-resource-provider) sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Condividi modello](media/share-template-portal2b.png)  <br />

![Condividi modello](media/share-template-portal3b.png)  <br />

<span data-ttu-id="ff8e5-191">Fare clic su **Seleziona** e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="ff8e5-192">È ora possibile visualizzare hello utenti o gruppi aggiunti toohello risorse.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-192">You can now see hello users or groups you added toohello resource.</span></span>

![Condividi modello](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="ff8e5-194">Un modello può essere condiviso solo con utenti e gruppi in hello stesso tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="ff8e5-195">Se si condivide un modello con un indirizzo di posta elettronica che non è nel tenant, verrà inviato un invito porre tenant di hello utente toojoin hello come guest.</span><span class="sxs-lookup"><span data-stu-id="ff8e5-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ff8e5-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff8e5-196">Next steps</span></span>
* <span data-ttu-id="ff8e5-197">toolearn sulla creazione di modelli di gestione delle risorse, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="ff8e5-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="ff8e5-198">le funzioni hello toounderstand è possibile utilizzare in un modello di gestione delle risorse, vedere [funzioni di modello](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="ff8e5-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="ff8e5-199">Per informazioni aggiuntive sulla progettazione di modelli, vedere [Procedure consigliate per la progettazione di modelli di Gestione risorse di Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="ff8e5-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

