---
title: aaaManaging Azure risorse con Cloud Explorer | Documenti Microsoft
description: Informazioni su come toouse Cloud Explorer toobrowse e gestire le risorse di Azure in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="9ddc5-103">Gestire le risorse di hello associate agli account di Azure in Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9ddc5-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="9ddc5-104">Cloud Explorer consente si tooview le risorse di Azure e i gruppi di risorse, controllare le relative proprietà ed eseguire azioni di diagnostica chiave sviluppatore da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="9ddc5-105">Ad esempio hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer viene compilato nello stack di hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="9ddc5-106">Pertanto riconosce risorse, come i gruppi di risorse di Azure e i servizi di Azure, come le app per la logica e le app per le API. Supporta infine il [controllo degli accessi in base al ruolo](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="9ddc5-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9ddc5-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9ddc5-107">Prerequisites</span></span>
- <span data-ttu-id="9ddc5-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello **carico di lavoro Azure** selezionato, o una versione precedente di Visual Studio con hello [Microsoft Azure SDK per .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="9ddc5-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="9ddc5-109">Account di Microsoft Azure: se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="9ddc5-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="9ddc5-110">tooview Cloud Explorer, selezionare **vista** > **Cloud Explorer** sulla barra dei menu hello.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="9ddc5-111">Aggiungere un tooCloud account Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="9ddc5-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="9ddc5-112">risorse di hello tooview associate a un account Azure, è necessario prima aggiungere hello account tooCloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="9ddc5-113">In **Cloud Explorer**, selezionare **Impostazioni account Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="9ddc5-115">Selezionare **Aggiungi un nuovo account**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-115">Select **Add new account**.</span></span> 

    ![Collegamento per l'aggiunta dell'account di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="9ddc5-117">Accedi toohello account Azure con risorse di cui si desidera toobrowse.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="9ddc5-118">Una volta effettuato l'accesso tooan account Azure, visualizzare le sottoscrizioni di hello associate all'account.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="9ddc5-119">Selezionare hello per le sottoscrizioni degli account hello toobrowse desiderato e quindi selezionare le caselle di controllo **applica**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: selezionare le sottoscrizioni di Azure toodisplay](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="9ddc5-121">Dopo aver selezionato le sottoscrizioni di hello con risorse di cui si desidera toobrowse, tali sottoscrizioni e le risorse visualizzare hello Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Elenco delle risorse di Cloud Explorer per un account Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="9ddc5-123">Rimuovere un account di Azure da Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9ddc5-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="9ddc5-124">In **Cloud Explorer**, selezionare **Impostazioni account Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="9ddc5-126">Selezionare Avanti toohello account cui si vuole tooremove, **rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Icona delle impostazioni account di Azure di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="9ddc5-128">Visualizzare i tipi o i gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="9ddc5-128">View resource types or resource groups</span></span>
<span data-ttu-id="9ddc5-129">tooview le risorse di Azure, è possibile scegliere una **tipi di risorse** o **gruppi di risorse** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="9ddc5-130">In **Cloud Explorer**, selezionare hello a discesa di visualizzazione di risorse.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Visualizzazione di risorse hello desiderato tooselect elenco a discesa Esplora del cloud](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="9ddc5-132">Dal menu di scelta rapida hello, selezionare visualizzazione di hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="9ddc5-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="9ddc5-133">**Tipi di risorse** visualizzazione - hello comune utilizzato in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Mostra le risorse di Azure classificati in base al tipo, ad esempio applicazioni web, gli account di archiviazione e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="9ddc5-134">**Gruppi di risorse** visualizzazione - le risorse di Azure vengono suddivisi in categorie per il gruppo di risorse di Azure hello con cui si associato.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="9ddc5-135">Un gruppo di risorse è un bundle di risorse di Azure, in genere usate da un'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="9ddc5-136">toolearn altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di gestione risorse di Azure](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc5-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="9ddc5-137">Hello immagine seguente mostra un confronto di hello due viste di risorsa:</span><span class="sxs-lookup"><span data-stu-id="9ddc5-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Confronto tra visualizzazioni delle risorse di Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="9ddc5-139">Visualizzare ed esplorare le risorse in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9ddc5-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="9ddc5-140">toonavigate tooan risorse di Azure e visualizzare le informazioni in Cloud Explorer espandere tipo dell'elemento hello o un gruppo di risorse associati, quindi selezionare la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="9ddc5-141">Quando si seleziona una risorsa, vengono visualizzate informazioni nelle schede hello due - **azioni** e **proprietà** : nella parte inferiore di hello del Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="9ddc5-142">**Azioni** scheda - elenchi hello azioni eseguibili in Cloud Explorer per la risorsa hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="9ddc5-143">È inoltre possibile visualizzare queste opzioni facendo hello risorsa tooview menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="9ddc5-144">**Proprietà** scheda - Visualizza le proprietà di hello della risorsa hello, ad esempio il gruppo di tipo, delle impostazioni locali e delle risorse a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="9ddc5-145">Hello immagine seguente mostra un confronto di esempio di ciò che viene visualizzato in ogni scheda per un servizio App:</span><span class="sxs-lookup"><span data-stu-id="9ddc5-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="9ddc5-146">Ogni risorsa ha azione hello **Apri nel portale di**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="9ddc5-147">Quando si sceglie questa azione, Cloud Explorer consente di visualizzare risorse hello selezionato in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9ddc5-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="9ddc5-148">Hello **Apri nel portale** funzionalità è utile per spostarsi tra le risorse toodeeply annidati.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="9ddc5-149">Azioni aggiuntive e i valori delle proprietà possono essere visualizzata anche in base alle risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="9ddc5-150">Ad esempio, le applicazioni web e App per la logica anche avere azioni hello **Apri nel browser** e **collega debugger** inoltre troppo**Apri nel portale di**.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="9ddc5-151">Editor di azioni tooopen vengono visualizzati quando si sceglie un blob dell'account di archiviazione, una coda o una tabella.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="9ddc5-152">Per le app Azure sono disponibili le proprietà relative a **URL** e **stato**, mentre per le risorse di archiviazione sono disponibili le proprietà relative alle chiavi e alle stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="9ddc5-153">Cercare risorse in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9ddc5-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="9ddc5-154">risorse toolocate con un nome specifico in una delle sottoscrizioni di account di Azure, immettere il nome di hello in hello **ricerca** casella in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Ricerca di risorse in Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="9ddc5-156">Mentre si immettono caratteri in hello **ricerca** casella, solo le risorse che corrispondono a tali caratteri vengono visualizzati nell'albero di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9ddc5-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
