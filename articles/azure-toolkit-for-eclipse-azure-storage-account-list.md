---
title: Elenco di Account di archiviazione di Azure
description: Gestire le impostazioni dell'account di archiviazione tramite il Toolkit di Azure per Eclipse
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="3c86c-103">Elenco di Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3c86c-103">Azure Storage Account List</span></span>
<span data-ttu-id="3c86c-104">Gli account di archiviazione di Azure abilitano dei percorsi di download da usare per il JDK, per il server dell’applicazione e per i componenti arbitrari, nonché per lo stato di archiviazione quando si utilizza la memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="3c86c-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="3c86c-105">Eclipse mantiene un elenco di account di archiviazione noti disponibili per i progetti nell'area di lavoro di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c86c-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="3c86c-106">Per aprire la finestra di dialogo **Account di archiviazione** che viene usata per gestire tale elenco, in Eclipse, fare clic su **Finestra**, **Preferenze**, espandere **Azure**, quindi fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="3c86c-107">Di seguito viene visualizzata la finestra di dialogo **Account di archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="3c86c-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="3c86c-108">Questa finestra di dialogo può anche essere aperta da un collegamento **Account** nelle finestre di dialogo che utilizzano gli account di archiviazione, come ad esempio le gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c86c-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="3c86c-109">La scheda **JDK** della finestra di dialogo **Configurazione Server**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="3c86c-110">La scheda **Server** della finestra di dialogo **Configurazione Server**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="3c86c-111">La finestra di dialogo **Aggiungi componente** .</span><span class="sxs-lookup"><span data-stu-id="3c86c-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="3c86c-112">La finestra di dialogo delle proprietà di **Memorizzazione nella cache**</span><span class="sxs-lookup"><span data-stu-id="3c86c-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="3c86c-113">Per importare gli account di archiviazione usando un file di impostazioni di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3c86c-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="3c86c-114">All'interno della finestra di dialogo **Account di archiviazione** fare clic su **Importa da file IMPOSTAZIONI DI PUBBLICAZIONE**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="3c86c-115">(Saltare questo passaggio se è già stato salvato un file di impostazioni di pubblicazione nel computer locale). Nella finestra di dialogo **Import Subscription Information** (Importa informazioni sottoscrizione) fare clic su **Download PUBLISH-SETTINGS File** (Download del file PUBLISH-SETTINGS).</span><span class="sxs-lookup"><span data-stu-id="3c86c-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="3c86c-116">Se non ci si è ancora connessi al proprio account Azure, verrà richiesto di farlo.</span><span class="sxs-lookup"><span data-stu-id="3c86c-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="3c86c-117">Quindi verrà richiesto di salvare un file di impostazioni di pubblicazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c86c-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="3c86c-118">(È possibile ignorare le istruzioni risultanti visualizzate nelle pagine di accesso, sono fornite dal portale di Azure e sono destinate agli utenti di Visual Studio.) Salvarlo nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="3c86c-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="3c86c-119">Sempre nella finestra di dialogo **Import Subscription Information** (Importa informazioni sottoscrizione) fare clic sul pulsante **Browse** (Sfoglia), selezionare il file di impostazioni di pubblicazione precedentemente salvato in locale e quindi fare clic su **Open** (Apri).</span><span class="sxs-lookup"><span data-stu-id="3c86c-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="3c86c-120">Fare clic su **OK** per chiudere la finestra di dialogo **Import Subscription Information** (Importa informazioni sottoscrizione).</span><span class="sxs-lookup"><span data-stu-id="3c86c-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="3c86c-121">Per creare un nuovo account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3c86c-121">To create a new storage account</span></span>
1. <span data-ttu-id="3c86c-122">Nella finestra di dialogo **Account di archiviazione** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="3c86c-123">Nella finestra di dialogo **Aggiungi account di archiviazione** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="3c86c-124">All'interno della finestra di dialogo **Nuovo Account di archiviazione** , specificare i valori per le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c86c-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="3c86c-125">Nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-125">Storage account name.</span></span>

   * <span data-ttu-id="3c86c-126">Posizione dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-126">Location of the storage account.</span></span>

   * <span data-ttu-id="3c86c-127">Descrizione dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-127">Description of the storage account.</span></span>

   * <span data-ttu-id="3c86c-128">Sottoscrizione a cui appartiene l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="3c86c-129">Fare clic su **OK** per chiudere la finestra di dialogo **Nuovo Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="3c86c-130">Potrebbero volerci alcuni minuti per creare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="3c86c-131">Dopo averlo creato, fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi Account di archiviazione** e il nuovo account di archiviazione verrà aggiunto all'elenco di account di archiviazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="3c86c-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="3c86c-132">Aggiungere un account di archiviazione esistente all’elenco</span><span class="sxs-lookup"><span data-stu-id="3c86c-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="3c86c-133">Se non si dispone ancora di un account di archiviazione di Azure, crearne uno seguendo i passaggi elencati in **Creare una nuova sezione di account di archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="3c86c-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="3c86c-134">In alternativa, è possibile creare un nuovo account di archiviazione nel [portale di gestione di Azure][Azure Management Portal].</span><span class="sxs-lookup"><span data-stu-id="3c86c-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="3c86c-135">Nella finestra di dialogo **Account di archiviazione** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="3c86c-136">Nella finestra di dialogo **Aggiungi Account di archiviazione** immettere i valori per **Nome** e **Chiave di accesso**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="3c86c-137">Ci devono essere la chiave dell'account e la chiave di accesso per un account di archiviazione di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="3c86c-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="3c86c-138">Utilizzare la sezione **Archiviazione** del [Portale di gestione di Azure][Azure Management Portal] per visualizzare i nomi degli account di archiviazione e le chiavi.</span><span class="sxs-lookup"><span data-stu-id="3c86c-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="3c86c-139">la finestra di dialogo **Aggiungi Account di archiviazione** sarà simile a quella seguente.</span><span class="sxs-lookup"><span data-stu-id="3c86c-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="3c86c-140">Fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="3c86c-141">Modificare un account di archiviazione per l'utilizzo di una nuova chiave di accesso</span><span class="sxs-lookup"><span data-stu-id="3c86c-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="3c86c-142">Nella finestra di dialogo **Account di archiviazione** scegliere l'account di archiviazione da modificare e quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="3c86c-143">Nella finestra di dialogo di modifica della **chiave di accesso dell'account di archiviazione**, modificare il valore della **chiave di accesso**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="3c86c-144">Fare clic su **OK** per chiudere la finestra di dialogo di modifica della **chiave di accesso dell'account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="3c86c-145">Per rimuovere un account di archiviazione dall'elenco gestito in Eclipse</span><span class="sxs-lookup"><span data-stu-id="3c86c-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="3c86c-146">Nella finestra di dialogo **Account di archiviazione** fare clic sull'account di archiviazione da modificare e quindi fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="3c86c-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="3c86c-147">Fare clic su **OK** quando viene richiesto di rimuovere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="3c86c-148">Rimuovendolo tramite la finestra di dialogo **Account di archiviazione**, l'account verrà rimosso solo dall'elenco di account di archiviazione visualizzabili in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c86c-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="3c86c-149">L'account di archiviazione non viene rimosso dalla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="3c86c-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="3c86c-150">e potrebbe essere nuovamente visualizzato nell'elenco dopo che Eclipse ricarica i dettagli della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3c86c-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="3c86c-151">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3c86c-151">See Also</span></span>
<span data-ttu-id="3c86c-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c86c-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="3c86c-153">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c86c-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="3c86c-154">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c86c-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="3c86c-155">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3c86c-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
