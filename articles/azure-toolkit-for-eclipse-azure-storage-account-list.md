---
title: Elenco di Account di archiviazione aaaAzure
description: Gestire le impostazioni dell'account di archiviazione utilizzando hello Azure Toolkit per Eclipse
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="8f164-103">Elenco di Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8f164-103">Azure Storage Account List</span></span>
<span data-ttu-id="8f164-104">Abilitare gli account di archiviazione Azure scaricare toobe percorsi utilizzati per il JDK, server applicazioni e componenti arbitrari, nonché per l'archiviazione dello stato quando si utilizza la memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="8f164-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="8f164-105">Eclipse gestisce un elenco di account di archiviazione conosciuti tooyour disponibili progetti nell'area di lavoro di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8f164-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="8f164-106">hello tooopen **gli account di archiviazione** finestra di dialogo che viene utilizzato toomanage l'elenco, in Eclipse, fare clic su **finestra**, fare clic su **preferenze**, espandere **Azure** , quindi fare clic su **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="8f164-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="8f164-107">Hello seguente illustra la hello **gli account di archiviazione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="8f164-108">Questa finestra di dialogo può anche essere aperta da un **account** collegamento nelle finestre di dialogo che utilizzano gli account di archiviazione, come illustrato di seguito hello:</span><span class="sxs-lookup"><span data-stu-id="8f164-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="8f164-109">Hello **JDK** scheda di hello **configurazione Server** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="8f164-110">Hello **Server** scheda di hello **configurazione Server** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="8f164-111">Hello **Add Component** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="8f164-112">Hello **la memorizzazione nella cache** finestra di dialogo proprietà.</span><span class="sxs-lookup"><span data-stu-id="8f164-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="8f164-113">tooimport lo spazio di archiviazione degli account con un file di impostazioni di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="8f164-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="8f164-114">All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Importa da file PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="8f164-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="8f164-115">(Ignorare questo passaggio se è già stato salvato un computer locale pubblica Impostazioni file tooyour). In hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su **Scarica File PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="8f164-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="8f164-116">Se non si è ancora connessi all'account Azure, sarà richiesta toolog in.</span><span class="sxs-lookup"><span data-stu-id="8f164-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="8f164-117">Quindi verrà chiesto di file di impostazioni di pubblicazione toosave di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f164-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="8f164-118">(È possibile ignorare istruzioni di hello risultanti visualizzate nelle pagine di accesso hello - sono forniti dal portale di Azure hello e sono destinate agli utenti di Visual Studio.) Salvare il file tooyour di computer locale.</span><span class="sxs-lookup"><span data-stu-id="8f164-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="8f164-119">Ancora in hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su hello **Sfoglia** pulsante, hello seleziona pubblicare file di impostazioni che è stato salvato in locale in precedenza e quindi fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="8f164-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="8f164-120">Fare clic su **OK** tooclose hello **Importa informazioni sottoscrizione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="8f164-121">toocreate un nuovo account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8f164-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="8f164-122">All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8f164-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="8f164-123">All'interno di hello **Add Storage Account** finestra di dialogo, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="8f164-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="8f164-124">All'interno di hello **nuovo Account di archiviazione** finestra di dialogo, specificare i valori per l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="8f164-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="8f164-125">Nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f164-125">Storage account name.</span></span>

   * <span data-ttu-id="8f164-126">Posizione dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f164-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="8f164-127">Descrizione dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f164-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="8f164-128">account di archiviazione di Hello sottoscrizione toowhich hello appartiene.</span><span class="sxs-lookup"><span data-stu-id="8f164-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="8f164-129">Fare clic su **OK** tooclose hello **nuovo Account di archiviazione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="8f164-130">Potrebbe richiedere alcuni minuti per il toobe di account di archiviazione creato.</span><span class="sxs-lookup"><span data-stu-id="8f164-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="8f164-131">Dopo averlo creato, fare clic su **OK** tooclose hello **Add Storage Account** finestra di dialogo e il nuovo account di archiviazione verrà aggiunto toohello elenco di account di archiviazione disponibile.</span><span class="sxs-lookup"><span data-stu-id="8f164-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="8f164-132">tooadd un elenco di toohello account di archiviazione esistente</span><span class="sxs-lookup"><span data-stu-id="8f164-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="8f164-133">Se non hai già una risorsa di archiviazione Azure account, crearlo hello passaggi elencati in hello **toocreate una nuova sezione di account di archiviazione** sopra.</span><span class="sxs-lookup"><span data-stu-id="8f164-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="8f164-134">(In alternativa, è possibile creare un nuovo account di archiviazione in hello [il portale di gestione di Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="8f164-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="8f164-135">All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8f164-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="8f164-136">All'interno di hello **Add Storage Account** finestra di dialogo, immettere i valori per **nome** e **tasto**.</span><span class="sxs-lookup"><span data-stu-id="8f164-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="8f164-137">chiave di accesso e sul nome di account Hello deve essere di un account di archiviazione di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="8f164-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="8f164-138">Hello utilizzare **archiviazione** sezione di hello [il portale di gestione di Azure] [ Azure Management Portal] tooview nomi account di archiviazione e delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8f164-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="8f164-139">Il **Add Storage Account** finestra di dialogo avrà un aspetto simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="8f164-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="8f164-140">Fare clic su **OK** tooclose hello **Add Storage Account** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="8f164-141">toomodify un toouse di account di archiviazione nuova chiave di accesso</span><span class="sxs-lookup"><span data-stu-id="8f164-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="8f164-142">All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su account di archiviazione hello che desidera tooedit e quindi fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="8f164-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="8f164-143">All'interno di hello **Edit Storage Account Access Key** finestra di dialogo, modificare hello **chiave di accesso** valore.</span><span class="sxs-lookup"><span data-stu-id="8f164-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="8f164-144">Fare clic su **OK** tooclose hello **Edit Storage Account Access Key** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8f164-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="8f164-145">tooremove un account di archiviazione dall'elenco di hello gestito in Eclipse</span><span class="sxs-lookup"><span data-stu-id="8f164-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="8f164-146">All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su account di archiviazione hello che desidera tooedit e quindi fare clic su **rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="8f164-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="8f164-147">Fare clic su **OK** quando richiesta tooremove hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f164-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="8f164-148">Rimozione di account di archiviazione hello tramite hello **gli account di archiviazione** finestra di dialogo verrà rimosso solo dall'elenco di hello degli account di archiviazione visualizzabile in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8f164-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="8f164-149">Non rimuove account di archiviazione hello dalla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f164-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="8f164-150">Inoltre, account di archiviazione hello venga visualizzato nuovamente nell'elenco dopo che Eclipse ricarica i dettagli di hello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8f164-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="8f164-151">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8f164-151">See Also</span></span>
<span data-ttu-id="8f164-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8f164-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="8f164-153">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8f164-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="8f164-154">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8f164-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="8f164-155">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="8f164-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
