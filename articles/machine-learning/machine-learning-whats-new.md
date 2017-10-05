---
title: "Novità di Azure Machine Learning | Documentazione Microsoft"
description: "Nuove funzionalità disponibili in Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="c08f9-103">Novità in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c08f9-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="c08f9-104">La versione di marzo 2017 degli aggiornamenti di Microsoft Azure Machine Learning offre la funzionalità seguente:</span><span class="sxs-lookup"><span data-stu-id="c08f9-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="c08f9-105">Capacità dedicata per i processi BES di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c08f9-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="c08f9-106">L'elaborazione di pool Batch in Machine Learning usa il [servizio Azure Batch](../batch/batch-technical-overview.md) per fornire la scalabilità gestita dal cliente per il servizio di esecuzione Batch di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c08f9-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="c08f9-107">L'elaborazione di pool Batch consente di creare pool Azure Batch a cui è possibile inviare i processi batch e eseguirli in modo prevedibile.</span><span class="sxs-lookup"><span data-stu-id="c08f9-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="c08f9-108">Per altre informazioni, vedere [Servizio Azure Batch per i processi di Machine Learning](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="c08f9-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="c08f9-109">La versione di agosto 2016 degli aggiornamenti di Microsoft Azure Machine Learning offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="c08f9-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="c08f9-110">I servizi Web classici possono ora essere gestiti nel nuovo portale dei [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/), che consente di gestire tutti gli aspetti del servizio Web da un'unica posizione e:</span><span class="sxs-lookup"><span data-stu-id="c08f9-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="c08f9-111">Fornisce le [statistiche di uso](machine-learning-manage-new-webservice.md)del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c08f9-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="c08f9-112">Semplifica il test delle chiamate di richiesta remota di Azure Machine Learning tramite dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c08f9-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="c08f9-113">Offre una nuova pagina di test del servizio Esecuzione batch con la cronologia di invio di processi e dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c08f9-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="c08f9-114">Consente una gestione più semplice degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="c08f9-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="c08f9-115">La versione di luglio 2016 degli aggiornamenti di Microsoft Azure Machine Learning offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="c08f9-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="c08f9-116">I servizi Web vengono ora gestiti come risorse di Azure gestite tramite le interfacce di [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) consentendo i miglioramenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c08f9-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="c08f9-117">Sono disponibili nuove [API REST](https://msdn.microsoft.com/library/azure/Dn950030.aspx) per la distribuzione e la gestione dei servizi Web basati su Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c08f9-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="c08f9-118">Il nuovo portale dei [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/) consente di gestire tutti gli aspetti del servizio Web da un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="c08f9-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="c08f9-119">Incorpora un nuovo modello di distribuzione dei servizi Web basato sulla sottoscrizione, con più aree usando API basate su Resource Manager che si avvalgono del provider di risorse di Resource Manager per i servizi Web.</span><span class="sxs-lookup"><span data-stu-id="c08f9-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="c08f9-120">Introduce nuovi [piani tariffari](https://azure.microsoft.com/pricing/details/machine-learning/) e capacità di gestione dei piani avvalendosi del nuovo provider di risorse di Resource Manager per la fatturazione.</span><span class="sxs-lookup"><span data-stu-id="c08f9-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="c08f9-121">È ora possibile [distribuire il servizio Web in più aree](machine-learning-how-to-deploy-to-multiple-regions.md) senza dover creare una sottoscrizione in ogni area.</span><span class="sxs-lookup"><span data-stu-id="c08f9-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="c08f9-122">Fornisce le [statistiche di uso](machine-learning-manage-new-webservice.md)del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c08f9-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="c08f9-123">Semplifica il test delle chiamate di richiesta remota di Azure Machine Learning tramite dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c08f9-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="c08f9-124">Offre una nuova pagina di test del servizio Esecuzione batch con la cronologia di invio di processi e dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c08f9-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="c08f9-125">Inoltre, Machine Learning Studio è stato aggiornato in modo da consentire ancora la distribuzione del modello di servizio Web classico, oltre alla distribuzione del nuovo modello di servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c08f9-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

