---
title: un'area di lavoro di Machine Learning aaaCreate | Documenti Microsoft
description: Come toocreate un'area di lavoro per Azure Machine Learning Studio
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
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="f5a93-103">Creare e condividere un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f5a93-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="f5a93-104">Questo menu Collega tootopics che descrivono come tooset backup hello diversi ambienti di analisi scientifica dei dati utilizzata dal hello Cortana Analitica processo (CAP).</span><span class="sxs-lookup"><span data-stu-id="f5a93-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="f5a93-105">toouse Azure Machine Learning Studio, è necessario toohave un'area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f5a93-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="f5a93-106">L'area di lavoro contiene strumenti hello necessari toocreate, gestire e pubblicare esperimenti.</span><span class="sxs-lookup"><span data-stu-id="f5a93-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="f5a93-107">toocreate un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="f5a93-107">toocreate a workspace</span></span>
1. <span data-ttu-id="f5a93-108">Accedi toohello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f5a93-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5a93-109">toosign in e creare un'area di lavoro, è necessario toobe amministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a93-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="f5a93-110">Fare clic su **+Nuovo**</span><span class="sxs-lookup"><span data-stu-id="f5a93-110">Click **+New**</span></span>

3. <span data-ttu-id="f5a93-111">Selezionare **Intelligence e analisi**, fare clic su **Area di lavoro di Machine Learning** e quindi su **Crea**</span><span class="sxs-lookup"><span data-stu-id="f5a93-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="f5a93-112">Immettere le informazioni sull'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="f5a93-112">Enter your workspace information</span></span>

    - <span data-ttu-id="f5a93-113">Hello *nome area di lavoro* può essere up too260 caratteri, che non terminano in uno spazio.</span><span class="sxs-lookup"><span data-stu-id="f5a93-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="f5a93-114">nome di Hello non può includere i seguenti caratteri:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="f5a93-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="f5a93-115">Hello *il piano di servizio web* si sceglie (o creare), insieme a hello associata *tariffario* seleziona, verrà utilizzata se si distribuiscono servizi web dall'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f5a93-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Creazione di una nuova area di lavoro](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="f5a93-117">Fare clic su **Crea**</span><span class="sxs-lookup"><span data-stu-id="f5a93-117">Click **Create**</span></span>

<span data-ttu-id="f5a93-118">Dopo aver distribuito l'area di lavoro hello, è possibile aprirlo in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f5a93-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="f5a93-119">Sfoglia tooMachine Learning Studio a [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f5a93-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="f5a93-120">Selezionare l'area di lavoro nell'angolo superiore a destra di hello.</span><span class="sxs-lookup"><span data-stu-id="f5a93-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Selezionare l'area di lavoro](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="f5a93-122">Fare clic su **esperimenti personali**.</span><span class="sxs-lookup"><span data-stu-id="f5a93-122">Click **my experiments**.</span></span>

    ![Aprire gli esperimenti](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="f5a93-124">Per informazioni sulla gestione dell'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f5a93-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="f5a93-125">Se si verifica un problema durante la creazione dell'area di lavoro, vedere [Troubleshooting guide: creare e collegare l'area di lavoro Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f5a93-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="f5a93-126">Condivisione di un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f5a93-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="f5a93-127">Dopo aver creato un'area di lavoro di Machine Learning, è possibile invitare utenti tooyour dell'area di lavoro tooshare accesso tooyour dell'area di lavoro e tutti i relativi esperimenti, set di dati, blocchi appunti e così via. È possibile aggiungere gli utenti in due ruoli:</span><span class="sxs-lookup"><span data-stu-id="f5a93-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="f5a93-128">**Utente** -un utente dell'area di lavoro può creare, aprire, modificare ed eliminare gli esperimenti, set di dati, e così via. nell'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="f5a93-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="f5a93-129">**Proprietario** : possibile invitare un proprietario e rimuovere gli utenti nell'area di lavoro hello in toowhat inoltre un utente possono eseguire.</span><span class="sxs-lookup"><span data-stu-id="f5a93-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="f5a93-130">account amministratore Hello Crea area di lavoro hello viene automaticamente aggiunto toohello dell'area di lavoro come proprietario dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f5a93-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="f5a93-131">Tuttavia, altri amministratori o utenti in sottoscrizione non sono automaticamente concesso l'accesso toohello dell'area di lavoro, è necessario tooinvite loro in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="f5a93-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="f5a93-132">tooshare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="f5a93-132">tooshare a workspace</span></span>

1. <span data-ttu-id="f5a93-133">Accedi tooMachine Learning Studio a [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="f5a93-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="f5a93-134">Nel riquadro sinistro di hello, fare clic su **impostazioni**</span><span class="sxs-lookup"><span data-stu-id="f5a93-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="f5a93-135">Fare clic su hello **utenti** scheda</span><span class="sxs-lookup"><span data-stu-id="f5a93-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="f5a93-136">Fare clic su **INVITARE utenti più** nella parte inferiore di hello della pagina hello</span><span class="sxs-lookup"><span data-stu-id="f5a93-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Impostazioni di Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="f5a93-138">Immettere uno o più indirizzi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f5a93-138">Enter one or more email addresses.</span></span> <span data-ttu-id="f5a93-139">gli utenti di Hello è necessario un account Microsoft valido o un account aziendale (da Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f5a93-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="f5a93-140">Selezionare se si desidera che gli utenti di hello tooadd come proprietario o l'utente.</span><span class="sxs-lookup"><span data-stu-id="f5a93-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="f5a93-141">Fare clic su hello **OK** segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f5a93-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="f5a93-142">Ogni utente che si aggiunge un messaggio e-mail con le istruzioni su come area di lavoro è condivisa in toohello toosign.</span><span class="sxs-lookup"><span data-stu-id="f5a93-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="f5a93-143">Per gli utenti toobe in grado di toodeploy o gestire servizi web nell'area di lavoro, devono essere Collaboratore o amministratore di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a93-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



