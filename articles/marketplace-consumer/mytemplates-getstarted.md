---
title: Introduzione ai modelli privati | Documentazione Microsoft
description: Aggiungere, gestire e condividere modelli privati usando il portale di Azure, l'interfaccia della riga di comando di Azure o PowerShell.
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
ms.openlocfilehash: 01657619cbe579c6818a790cc3ab95a33936a565
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-private-templates-on-the-azure-portal"></a><span data-ttu-id="759a1-103">Introduzione ai modelli privati nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="759a1-103">Get started with private Templates on the Azure Portal</span></span>
<span data-ttu-id="759a1-104">Un modello di [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) è un modello dichiarativo usato per definire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="759a1-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span></span> <span data-ttu-id="759a1-105">Permette di definire le risorse da distribuire per una soluzione e di specificare i parametri e le variabili che consentono di immettere valori per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="759a1-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="759a1-106">Il modello è composto da JSON ed espressioni che è possibile usare per creare valori per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="759a1-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span></span>

<span data-ttu-id="759a1-107">È possibile usare la nuova funzionalità **Modelli** nel [portale di Azure](https://portal.azure.com) insieme al provider di risorse **Microsoft.Gallery** come estensione di [Azure Marketplace](https://azure.microsoft.com/marketplace/), per consentire agli utenti di creare, gestire e distribuire modelli privati da una raccolta personale.</span><span class="sxs-lookup"><span data-stu-id="759a1-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="759a1-108">Questo documento descrive come aggiungere, gestire e condividere un **modello** privato con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="759a1-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="759a1-109">Indicazioni</span><span class="sxs-lookup"><span data-stu-id="759a1-109">Guidance</span></span>
<span data-ttu-id="759a1-110">I suggerimenti riportati di seguito permettono di sfruttare al meglio i **modelli** per l'uso delle soluzioni:</span><span class="sxs-lookup"><span data-stu-id="759a1-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="759a1-111">Un **modello** è una risorsa di incapsulamento contenente un modello di Resource Manager e metadati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="759a1-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="759a1-112">Si comporta in modo molto simile a un elemento di Marketplace.</span><span class="sxs-lookup"><span data-stu-id="759a1-112">It behaves very similarly to an item in the Marketplace.</span></span> <span data-ttu-id="759a1-113">La differenza principale è che si tratta di un elemento privato, mentre gli elementi di Marketplace sono pubblici.</span><span class="sxs-lookup"><span data-stu-id="759a1-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span></span>
* <span data-ttu-id="759a1-114">La raccolta **Modelli** è efficace per gli utenti che vogliono personalizzare le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="759a1-114">The **Templates** library works well for users who need to customize their deployments.</span></span>
* <span data-ttu-id="759a1-115">**modelli** permettono di usare un repository semplice all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="759a1-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="759a1-116">Iniziare con un modello di Resource Manager esistente.</span><span class="sxs-lookup"><span data-stu-id="759a1-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="759a1-117">In [GitHub](https://github.com/Azure/azure-quickstart-templates) o nel post di blog relativo all'[esportazione modelli](../azure-resource-manager/resource-manager-export-template.md) è possibile trovare modelli a partire da un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="759a1-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="759a1-118">**modelli** sono legati all'utente che li pubblica.</span><span class="sxs-lookup"><span data-stu-id="759a1-118">**Templates** are tied to the user who publishes them.</span></span> <span data-ttu-id="759a1-119">Il nome dell'autore è visibile a chiunque abbia accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="759a1-119">The publisher name is visible to everyone who has read access to it.</span></span>
* <span data-ttu-id="759a1-120">**modelli** sono risorse di Resource Manager e non possono essere rinominati dopo la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="759a1-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="759a1-121">Aggiungere una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="759a1-121">Add a Template resource</span></span>
<span data-ttu-id="759a1-122">Per creare una risorsa **modello** nel portale di Azure è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="759a1-122">There are two ways to create a **Template** resource in the Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="759a1-123">Metodo 1: creare una nuova risorsa modello da un gruppo di risorse in esecuzione</span><span class="sxs-lookup"><span data-stu-id="759a1-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="759a1-124">Passare a un gruppo di risorse esistente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="759a1-124">Navigate to an existing resource group on the Azure Portal.</span></span> <span data-ttu-id="759a1-125">In **Impostazioni** selezionare **Esporta modello**.</span><span class="sxs-lookup"><span data-stu-id="759a1-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="759a1-126">Dopo aver esportato il modello di Resource Manager, fare clic sul pulsante **Salva modello** per salvarlo nel repository **Modelli**.</span><span class="sxs-lookup"><span data-stu-id="759a1-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span></span> <span data-ttu-id="759a1-127">Per informazioni dettagliate sull'esportazione di modelli, vedere questa [pagina](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="759a1-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="759a1-128">
   ![Esportazione di un gruppo di risorse](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="759a1-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="759a1-129">Fare clic sul pulsante di comando **Salva modello** .</span><span class="sxs-lookup"><span data-stu-id="759a1-129">Select the **Save to Template** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="759a1-130">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="759a1-130">Enter the following information:</span></span>
   
   * <span data-ttu-id="759a1-131">Nome: nome dell'oggetto modello. Nota: il nome è basato su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="759a1-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="759a1-132">È soggetto a tutte le limitazioni relative all'assegnazione dei nomi non può essere modificato dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="759a1-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="759a1-133">Descrizione: breve descrizione del modello.</span><span class="sxs-lookup"><span data-stu-id="759a1-133">Description – Quick summary about the template.</span></span>
     
     ![Salva modello](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="759a1-135">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="759a1-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="759a1-136">In caso di errori del modello di Resource Manager esportato, le notifiche vengono visualizzate nel pannello Esporta modello. Sarà comunque possibile salvare il modello di Resource Manager nei modelli.</span><span class="sxs-lookup"><span data-stu-id="759a1-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span></span> <span data-ttu-id="759a1-137">Assicurarsi di controllare e correggere eventuali problemi del modello di Resource Manager prima di ridistribuire il modello di Resource Manager esportato.</span><span class="sxs-lookup"><span data-stu-id="759a1-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="759a1-138">Metodo 2: aggiungere una nuova risorsa modello dall'esplorazione</span><span class="sxs-lookup"><span data-stu-id="759a1-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="759a1-139">È anche possibile aggiungere un nuovo **modello** da zero usando il pulsante di comando +Aggiungi in **Esplora > Modelli**.</span><span class="sxs-lookup"><span data-stu-id="759a1-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="759a1-140">È necessario specificare un nome, una descrizione e il file JSON del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="759a1-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span></span>

![Aggiungi modello](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="759a1-142">Microsoft.Gallery è un provider di risorse di Azure basato su tenant.</span><span class="sxs-lookup"><span data-stu-id="759a1-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="759a1-143">La risorsa modello è associata all'utente che l'ha creata.</span><span class="sxs-lookup"><span data-stu-id="759a1-143">The Template resource is tied to the user who created it.</span></span> <span data-ttu-id="759a1-144">Non è associata a una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="759a1-144">It is not tied to any specific subscription.</span></span> <span data-ttu-id="759a1-145">È necessario scegliere una sottoscrizione solo quando si distribuisce un modello.</span><span class="sxs-lookup"><span data-stu-id="759a1-145">A subscription needs to be chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="759a1-146">Visualizzare le risorse modello</span><span class="sxs-lookup"><span data-stu-id="759a1-146">View Template resources</span></span>
<span data-ttu-id="759a1-147">È possibile visualizzare tutti i **modelli** disponibili in **Esplora > Modelli**.</span><span class="sxs-lookup"><span data-stu-id="759a1-147">All **Templates** available to you can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="759a1-148">Sono inclusi i **modelli** creati dall'utente e quelli condivisi con l'utente a vari livelli di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="759a1-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="759a1-149">Per altre informazioni sul [controllo di accesso](#access-control-for-a-tenant-resource-provider) , vedere la relativa sezione più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="759a1-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Visualizza modello](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="759a1-151">Per visualizzare i dettagli di un **modello** è possibile fare clic su un elemento nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="759a1-151">You can view the details of a **Template** by clicking into an item in the list.</span></span>

![Visualizza modello](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="759a1-153">Modificare una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="759a1-153">Edit a Template resource</span></span>
<span data-ttu-id="759a1-154">Per avviare il flusso di modifica per un **modello** , fare clic con il pulsante destro del mouse sull'elemento nell'elenco di ricerca o scegliere il pulsante di comando Modifica.</span><span class="sxs-lookup"><span data-stu-id="759a1-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span></span>

![Modifica modello](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="759a1-156">È possibile modificare la descrizione o il testo del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="759a1-156">You can edit the description or Resource Manager template text.</span></span> <span data-ttu-id="759a1-157">Dato che si tratta di un nome di risorsa di Resource Manager, non è possibile modificare il nome.</span><span class="sxs-lookup"><span data-stu-id="759a1-157">You cannot edit the name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="759a1-158">Quando si modifica il file JSON del modello di Resource Manager, viene eseguita la convalida per verificare che si tratti di un file JSON valido.</span><span class="sxs-lookup"><span data-stu-id="759a1-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span></span> <span data-ttu-id="759a1-159">Scegliere **OK** e quindi **Salva** per salvare il modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="759a1-159">Choose **OK** and then **Save** to save your updated template.</span></span>

![Modifica modello](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="759a1-161">Verrà visualizzata una notifica che conferma il salvataggio del **modello** .</span><span class="sxs-lookup"><span data-stu-id="759a1-161">Once the **Template** is saved you will see a confirmation notification.</span></span>

![Modifica modello](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="759a1-163">Distribuire una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="759a1-163">Deploy a Template resource</span></span>
<span data-ttu-id="759a1-164">È possibile distribuire qualsiasi **modello** per cui si hanno autorizzazioni di **lettura**.</span><span class="sxs-lookup"><span data-stu-id="759a1-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="759a1-165">Il flusso di distribuzione consente di avviare il pannello di distribuzione del modello di Azure standard.</span><span class="sxs-lookup"><span data-stu-id="759a1-165">The deployment flow launches the standard Azure Template deployment blade.</span></span> <span data-ttu-id="759a1-166">Compilare i valori per i parametri del modello di Resource Manager per procedere con la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="759a1-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span></span>

![Modello di distribuzione](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="759a1-168">Condividere una risorsa modello</span><span class="sxs-lookup"><span data-stu-id="759a1-168">Share a Template resource</span></span>
<span data-ttu-id="759a1-169">È possibile condividere le risorse **modello** con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="759a1-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="759a1-170">La condivisione funziona in modo simile all' [assegnazione di ruoli per qualsiasi risorsa di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="759a1-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="759a1-171">Il proprietario del **modello** fornisce le autorizzazioni ad altri utenti, che possono interagire con la risorsa modello.</span><span class="sxs-lookup"><span data-stu-id="759a1-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span></span> <span data-ttu-id="759a1-172">L'utente o il gruppo di utenti con cui viene condiviso il **modello** può visualizzare il modello di Resource Manager e le relative proprietà della raccolta.</span><span class="sxs-lookup"><span data-stu-id="759a1-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-the-microsoftgallery-resources"></a><span data-ttu-id="759a1-173">Controllo di accesso per le risorse Microsoft.Gallery</span><span class="sxs-lookup"><span data-stu-id="759a1-173">Access control for the Microsoft.Gallery resources</span></span>
| <span data-ttu-id="759a1-174">Ruolo</span><span class="sxs-lookup"><span data-stu-id="759a1-174">Role</span></span> | <span data-ttu-id="759a1-175">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="759a1-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="759a1-176">Proprietario</span><span class="sxs-lookup"><span data-stu-id="759a1-176">Owner</span></span> |<span data-ttu-id="759a1-177">Consente il controllo completo sulla risorsa modello, inclusa la condivisione.</span><span class="sxs-lookup"><span data-stu-id="759a1-177">Allows full control on the Template resource including Share</span></span> |
| <span data-ttu-id="759a1-178">Lettore</span><span class="sxs-lookup"><span data-stu-id="759a1-178">Reader</span></span> |<span data-ttu-id="759a1-179">Consente l'autorizzazione di lettura ed esecuzione o distribuzione sulla risorsa modello.</span><span class="sxs-lookup"><span data-stu-id="759a1-179">Allows Read and Execute(Deploy) on the Template resource</span></span> |
| <span data-ttu-id="759a1-180">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="759a1-180">Contributor</span></span> |<span data-ttu-id="759a1-181">Consente l'autorizzazione di modifica ed eliminazione sulla risorsa modello.</span><span class="sxs-lookup"><span data-stu-id="759a1-181">Allows Edit and Delete permission on the Template resource.</span></span> <span data-ttu-id="759a1-182">L'utente non può condividere il modello con altri.</span><span class="sxs-lookup"><span data-stu-id="759a1-182">User cannot Share the Template with others</span></span> |

<span data-ttu-id="759a1-183">Fare clic con il pulsante destro del mouse sul pannello di visualizzazione di un elemento specifico e selezionare **Condividi** .</span><span class="sxs-lookup"><span data-stu-id="759a1-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span></span> <span data-ttu-id="759a1-184">Verrà avviata la condivisione.</span><span class="sxs-lookup"><span data-stu-id="759a1-184">This launches a Share experience.</span></span>

![Condividi modello](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="759a1-186">È possibile scegliere un ruolo e un utente o un gruppo a cui fornire l'accesso a un **modello**specifico.</span><span class="sxs-lookup"><span data-stu-id="759a1-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span></span> <span data-ttu-id="759a1-187">I ruoli disponibili sono Proprietario, Lettore e Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="759a1-187">The available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="759a1-188">Per altre informazioni sul [controllo di accesso](#access-control-for-a-tenant-resource-provider) , vedere la relativa sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="759a1-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Condividi modello](media/share-template-portal2b.png)  <br />

![Condividi modello](media/share-template-portal3b.png)  <br />

<span data-ttu-id="759a1-191">Fare clic su **Seleziona** e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="759a1-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="759a1-192">Ora è possibile visualizzare gli utenti o i gruppi aggiunti alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="759a1-192">You can now see the users or groups you added to the resource.</span></span>

![Condividi modello](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="759a1-194">Un modello può essere condiviso solo con utenti e gruppi nello stesso tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="759a1-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span></span> <span data-ttu-id="759a1-195">Se si condivide un modello con un indirizzo di posta elettronica che non è incluso nel tenant, viene inviato un invito a entrare nel tenant come guest.</span><span class="sxs-lookup"><span data-stu-id="759a1-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="759a1-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="759a1-196">Next steps</span></span>
* <span data-ttu-id="759a1-197">Per informazioni sulla creazione di modelli di Resource Manager, vedere [Creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="759a1-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="759a1-198">Per informazioni sulle funzioni disponibili in un modello di Resource Manager, vedere [Funzioni del modello](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="759a1-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="759a1-199">Per informazioni aggiuntive sulla progettazione di modelli, vedere [Procedure consigliate per la progettazione di modelli di Gestione risorse di Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="759a1-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

