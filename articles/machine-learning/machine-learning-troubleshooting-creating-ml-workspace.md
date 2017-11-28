---
title: 'Risolvere i problemi: Creare e collegare l''area di lavoro Machine Learning tooa | Documenti Microsoft'
description: Soluzioni ai problemi comuni per la creazione e la connessione dell'area di lavoro di tooan Azure Machine Learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="e62a6-103">Guida alla risoluzione dei problemi: creare e collegare l'area di lavoro Machine Learning tooan</span><span class="sxs-lookup"><span data-stu-id="e62a6-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="e62a6-104">Questa guida offre soluzioni per alcuni problemi frequenti relativi alla configurazione di aree di lavoro di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e62a6-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="e62a6-105">Proprietario dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="e62a6-105">Workspace owner</span></span>
<span data-ttu-id="e62a6-106">tooopen un'area di lavoro in Machine Learning Studio, è necessario essere connessi toohello Account Microsoft è stato usato area hello toocreate oppure è necessario un invito dall'area di lavoro di hello proprietario toojoin hello tooreceive.</span><span class="sxs-lookup"><span data-stu-id="e62a6-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="e62a6-107">Dal portale di Azure è possibile gestire hello hello area di lavoro che include l'accesso tooconfigure possibilità di hello.</span><span class="sxs-lookup"><span data-stu-id="e62a6-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="e62a6-108">Per altre informazioni sulla gestione di un'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="e62a6-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Gestire un'area di lavoro di Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="e62a6-110">Aree geografiche disponibili</span><span class="sxs-lookup"><span data-stu-id="e62a6-110">Allowed regions</span></span>
<span data-ttu-id="e62a6-111">Machine Learning è attualmente disponibile in un numero limitato di aree.</span><span class="sxs-lookup"><span data-stu-id="e62a6-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="e62a6-112">Se la sottoscrizione non include una di queste aree, verrà visualizzato il messaggio di errore hello, "Si sono presenti sottoscrizioni nelle consentiti aree hello."</span><span class="sxs-lookup"><span data-stu-id="e62a6-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="e62a6-113">toorequest da un'area aggiunto tooyour sottoscrizione, creare una nuova richiesta di supporto Microsoft dal portale di Azure hello scegliere **fatturazione** come tipo di problema hello e seguire hello richiede toosubmit la richiesta.</span><span class="sxs-lookup"><span data-stu-id="e62a6-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="e62a6-114">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e62a6-114">Storage account</span></span>
<span data-ttu-id="e62a6-115">Hello servizio Machine Learning è necessario un toostore dati dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e62a6-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="e62a6-116">È possibile utilizzare un account di archiviazione esistente o quando si crea l'area di lavoro Machine Learning nuovo hello (se si dispone di quota toocreate un nuovo account di archiviazione), è possibile creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e62a6-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="e62a6-117">Dopo aver creato l'area di lavoro Machine Learning nuovo hello, per accedere tooMachine Learning Studio usando account Microsoft hello che dell'area di lavoro di toocreate hello è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e62a6-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="e62a6-118">Se viene visualizzato il messaggio di errore hello, "Area di lavoro non trovato" (toohello simile seguente schermata), utilizzare hello seguendo i passaggi toodelete i cookie del browser.</span><span class="sxs-lookup"><span data-stu-id="e62a6-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Area di lavoro non trovata][screen3]

<span data-ttu-id="e62a6-120">**cookie del browser toodelete**</span><span class="sxs-lookup"><span data-stu-id="e62a6-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="e62a6-121">Se si utilizza Internet Explorer, fare clic su hello **strumenti** nell'angolo superiore destro hello e selezionare **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="e62a6-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Opzioni Internet][screen4]

2. <span data-ttu-id="e62a6-123">In hello **generale** scheda, fare clic su **eliminare...**</span><span class="sxs-lookup"><span data-stu-id="e62a6-123">Under hello **General** tab, click **Delete…**</span></span>

![Generale][screen5]

3. <span data-ttu-id="e62a6-125">In hello **Elimina cronologia esplorazioni** finestra di dialogo verificare **cookie e dati del sito Web** sia selezionata e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="e62a6-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Eliminare i cookie][screen6]

<span data-ttu-id="e62a6-127">Dopo l'eliminazione dei cookie hello, riavviare il browser hello e quindi passare toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) pagina.</span><span class="sxs-lookup"><span data-stu-id="e62a6-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="e62a6-128">Quando viene chiesto di immettere un nome utente e una password, hello stesso account Microsoft usato dell'area di lavoro di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e62a6-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="e62a6-129">Commenti</span><span class="sxs-lookup"><span data-stu-id="e62a6-129">Comments</span></span>

<span data-ttu-id="e62a6-130">L'obiettivo è toomake hello esperienza di Machine Learning più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="e62a6-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="e62a6-131">Inviare eventuali commenti e i problemi in hello [forum di Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp a un servizio migliore.</span><span class="sxs-lookup"><span data-stu-id="e62a6-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
