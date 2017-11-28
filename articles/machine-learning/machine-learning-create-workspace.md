---
title: Creare un'area di lavoro di Machine Learning | Microsoft Docs
description: Come creare un'area di lavoro per Azure Machine Learning Studio.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="9e8e7-103">Creare e condividere un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9e8e7-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="9e8e7-104">Questo menu si collega ad argomenti che descrivono come configurare i diversi ambienti di scienza dei dati usati da Cortana Analytics Process (CAP).</span><span class="sxs-lookup"><span data-stu-id="9e8e7-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="9e8e7-105">Per usare Azure Machine Learning Studio, è necessario disporre di un'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="9e8e7-106">Quest'area di lavoro contiene tutti gli strumenti necessari per la creazione, la gestione e la pubblicazione di esperimenti.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="9e8e7-107">Per creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="9e8e7-107">To create a workspace</span></span>
1. <span data-ttu-id="9e8e7-108">Accedere al [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9e8e7-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e8e7-109">Per eseguire l'accesso e creare un'area di lavoro è necessario essere amministratore di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="9e8e7-110">Fare clic su **+Nuovo**</span><span class="sxs-lookup"><span data-stu-id="9e8e7-110">Click **+New**</span></span>

3. <span data-ttu-id="9e8e7-111">Selezionare **Intelligence e analisi**, fare clic su **Area di lavoro di Machine Learning** e quindi su **Crea**</span><span class="sxs-lookup"><span data-stu-id="9e8e7-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="9e8e7-112">Immettere le informazioni sull'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="9e8e7-112">Enter your workspace information</span></span>

    - <span data-ttu-id="9e8e7-113">Il *nome dell'area di lavoro* può contenere al massimo 260 caratteri e non può terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="9e8e7-114">Il nome non può includere questi caratteri: `< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="9e8e7-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="9e8e7-115">Se si distribuiscono i servizi Web da quest'area di lavoro, vengono usati il *piano di servizio Web* che si sceglie (o si crea) e il *piano tariffario* selezionato.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Creazione di una nuova area di lavoro](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="9e8e7-117">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="9e8e7-117">Click **Create**</span></span>

<span data-ttu-id="9e8e7-118">Dopo aver distribuito l'area di lavoro è possibile aprirla in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="9e8e7-119">Passare a Machine Learning Studio all'indirizzo [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9e8e7-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="9e8e7-120">Selezionare l'area di lavoro nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Selezionare l'area di lavoro](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="9e8e7-122">Fare clic su **esperimenti personali**.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-122">Click **my experiments**.</span></span>

    ![Aprire gli esperimenti](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="9e8e7-124">Per informazioni sulla gestione dell'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e7-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="9e8e7-125">Se si verifica un problema durante la creazione dell'area di lavoro, vedere [Guida per la risoluzione dei problemi: Creare un'area di lavoro di Machine Learning e connettersi a essa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e7-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="9e8e7-126">Condivisione di un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9e8e7-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="9e8e7-127">Dopo la creazione di un'area di lavoro di Machine Learning, è possibile invitare utenti all'area di lavoro per condividere l'accesso all'area di lavoro e a tutti i rispettivi esperimenti, dataset, notebook e così via. È possibile aggiungere gli utenti in due ruoli:</span><span class="sxs-lookup"><span data-stu-id="9e8e7-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="9e8e7-128">**Utente**: un utente dell'area di lavoro può creare, aprire, modificare ed eliminare esperimenti, dataset e così via nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="9e8e7-129">**Proprietario**: un proprietario può invitare e rimuovere gli utenti dell'area di lavoro in aggiunta alle operazioni consentite a un utente.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="9e8e7-130">L'account amministratore che crea l'area di lavoro viene aggiunto automaticamente all'area di lavoro come proprietario.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="9e8e7-131">Agli altri amministratori o utenti della sottoscrizione non viene invece concesso automaticamente l'accesso all'area di lavoro, ma è necessario inviare loro un invito in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="9e8e7-132">Per condividere un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="9e8e7-132">To share a workspace</span></span>

1. <span data-ttu-id="9e8e7-133">Accedere a Machine Learning Studio all'indirizzo [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="9e8e7-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="9e8e7-134">Nel pannello sinistro fare clic su **IMPOSTAZIONI**</span><span class="sxs-lookup"><span data-stu-id="9e8e7-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="9e8e7-135">Fare clic sulla scheda **UTENTI**</span><span class="sxs-lookup"><span data-stu-id="9e8e7-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="9e8e7-136">Fare clic su **INVITE MORE USERS (INVITA ALTRI UTENTI)** in fondo alla pagina</span><span class="sxs-lookup"><span data-stu-id="9e8e7-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Impostazioni di Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="9e8e7-138">Immettere uno o più indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-138">Enter one or more email addresses.</span></span> <span data-ttu-id="9e8e7-139">L'utente ha bisogno di un account Microsoft o di un account aziendale valido (da Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9e8e7-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="9e8e7-140">Scegliere se si desidera aggiungere l'utente come proprietario o utente.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="9e8e7-141">Fare clic sul segno di spunta **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="9e8e7-142">Ogni utente aggiunto riceverà un messaggio di posta elettronica con istruzioni per l'accesso all'area di lavoro condivisa.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="9e8e7-143">Per poter distribuire o gestire i servizi Web nell'area di lavoro, l'utente deve essere un collaboratore o un amministratore nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e8e7-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



