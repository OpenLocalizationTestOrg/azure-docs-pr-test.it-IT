---
title: 'Risoluzione dei problemi: Creare e connettersi a un''area di lavoro di Machine Learning | Microsoft Docs'
description: Soluzioni per problemi comuni di creazione e connessione a un'area di lavoro di Azure Machine Learning
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="7bb96-103">Guida per la risoluzione dei problemi: Creazione e connessione a un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7bb96-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="7bb96-104">Questa guida offre soluzioni per alcuni problemi frequenti relativi alla configurazione di aree di lavoro di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7bb96-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="7bb96-105">Proprietario dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="7bb96-105">Workspace owner</span></span>
<span data-ttu-id="7bb96-106">Per aprire un'area di lavoro in Machine Learning Studio, è necessario essere connessi con l'account Microsoft usato per creare l'area di lavoro oppure ricevere un invito dal proprietario per partecipare all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bb96-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="7bb96-107">Dal portale di Azure è possibile gestire l'area di lavoro e anche configurare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7bb96-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="7bb96-108">Per altre informazioni sulla gestione di un'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="7bb96-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="7bb96-109">[Gestire un'area di lavoro di Azure Machine Learning]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="7bb96-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="7bb96-110">Aree geografiche disponibili</span><span class="sxs-lookup"><span data-stu-id="7bb96-110">Allowed regions</span></span>
<span data-ttu-id="7bb96-111">Machine Learning è attualmente disponibile in un numero limitato di aree.</span><span class="sxs-lookup"><span data-stu-id="7bb96-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="7bb96-112">Se la sottoscrizione non include una di queste aree, è possibile che venga visualizzato l'errore "Non sono presenti sottoscrizioni nelle aree consentite".</span><span class="sxs-lookup"><span data-stu-id="7bb96-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="7bb96-113">Per richiedere l'aggiunta di un'area alla sottoscrizione, creare una nuova richiesta al supporto tecnico Microsoft dal portale di Azure, scegliere **Fatturazione** come tipo di problema, quindi seguire le istruzioni per inviare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bb96-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="7bb96-114">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7bb96-114">Storage account</span></span>
<span data-ttu-id="7bb96-115">Il servizio Machine Learning necessita di un account di archiviazione per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="7bb96-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="7bb96-116">È possibile usare un account di archiviazione esistente oppure creare un nuovo account di archiviazione quando si crea la nuova area di lavoro di Machine Learning, se la quota disponibile è sufficiente per la creazione di un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bb96-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="7bb96-117">Dopo aver creato una nuova area di lavoro di Machine Learning, è possibile accedere a Machine Learning Studio usando l'account Microsoft specificato per creare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bb96-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="7bb96-118">Se viene visualizzato il messaggio di errore relativo all'area di lavoro non trovata, analogo a quanto mostrato nella schermata sottostante, usare la procedura seguente per eliminare i cookie dal browser.</span><span class="sxs-lookup"><span data-stu-id="7bb96-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Area di lavoro non trovata][screen3]

<span data-ttu-id="7bb96-120">**Per eliminare i cookie dal browser**</span><span class="sxs-lookup"><span data-stu-id="7bb96-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="7bb96-121">Se si usa Internet Explorer, fare clic sul pulsante **Strumenti** nell'angolo superiore destro, quindi selezionare **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="7bb96-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Opzioni Internet][screen4]

2. <span data-ttu-id="7bb96-123">Nella scheda **Generale** fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="7bb96-123">Under the **General** tab, click **Delete…**</span></span>

![Generale][screen5]

3. <span data-ttu-id="7bb96-125">Nella finestra di dialogo **Elimina cronologia esplorazioni** assicurarsi che l'opzione **Cookie e dati di siti Web** sia selezionata, quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="7bb96-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Eliminare i cookie][screen6]

<span data-ttu-id="7bb96-127">Dopo l'eliminazione dei cookie, riavviare il browser e quindi passare alla pagina [Microsoft Azure Machine Learning](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="7bb96-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="7bb96-128">Quando vengono richiesti nome utente e password, immettere lo stesso account Microsoft usato per creare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bb96-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="7bb96-129">Commenti</span><span class="sxs-lookup"><span data-stu-id="7bb96-129">Comments</span></span>

<span data-ttu-id="7bb96-130">L'obiettivo consiste nel semplificare al massimo l'esperienza di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7bb96-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="7bb96-131">Inserire eventuali commenti e problemi nel [forum su Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) per contribuire al miglioramento del prodotto.</span><span class="sxs-lookup"><span data-stu-id="7bb96-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
