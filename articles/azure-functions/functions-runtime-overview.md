---
title: Panoramica del runtime di Funzioni di Azure | Documentazione Microsoft
description: Panoramica di anteprima del runtime di Funzioni di Azure
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="4c503-103">Panoramica di Runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4c503-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="4c503-104">Il runtime di Funzioni di Azure offre un nuovo modo per sfruttare la semplicità e la flessibilità del modello di programmazione di Funzioni di Azure in locale.</span><span class="sxs-lookup"><span data-stu-id="4c503-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="4c503-105">Con la stessa base open source di Funzioni di Azure, il runtime di Funzioni di Azure viene distribuito in locale per fornire un'esperienza di sviluppo quasi identica al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4c503-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Anteprima del runtime di Funzioni di Azure - Portale][1]

<span data-ttu-id="4c503-107">Il runtime di Funzioni di Azure offre un modo per sfruttare Funzioni di Azure prima di eseguire il commit nel cloud.</span><span class="sxs-lookup"><span data-stu-id="4c503-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="4c503-108">In questo modo, è possibile portare gli asset di codice compilati nel cloud quando si esegue la migrazione.</span><span class="sxs-lookup"><span data-stu-id="4c503-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="4c503-109">Il runtime offre anche nuove opzioni, ad esempio l'uso di potenza di calcolo di riserva dei computer locali per l'esecuzione di processi batch durante la notte.</span><span class="sxs-lookup"><span data-stu-id="4c503-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="4c503-110">È possibile anche usare i dispositivi all'interno dell'organizzazione per inviare dati in modo condizionale ad altri sistemi, sia in locale sia nel cloud.</span><span class="sxs-lookup"><span data-stu-id="4c503-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="4c503-111">Il runtime di Funzioni di Azure è composto da due parti:</span><span class="sxs-lookup"><span data-stu-id="4c503-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="4c503-112">Il ruolo di gestione del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4c503-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="4c503-113">Il ruolo di lavoro del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4c503-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="4c503-114">Il ruolo di gestione di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4c503-114">Azure Functions Management Role</span></span>

<span data-ttu-id="4c503-115">Il ruolo di gestione di Funzioni di Azure fornisce un host per la gestione di Funzioni in locale.</span><span class="sxs-lookup"><span data-stu-id="4c503-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="4c503-116">Questo ruolo esegue le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c503-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="4c503-117">L'hosting del portale di gestione di Funzioni di Azure, corrispondente a quello nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c503-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4c503-118">Ciò consente di sviluppare funzioni come si farebbe nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c503-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="4c503-119">La distribuzione di funzioni tra più ruoli di lavoro di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="4c503-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="4c503-120">La garanzia di un endpoint di pubblicazione in modo che sia possibile pubblicare direttamente le funzioni da Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c503-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="4c503-121">Ruolo di lavoro di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4c503-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="4c503-122">I ruoli di lavoro di Funzioni di Azure vengono distribuiti nei contenitori Windows e qui viene eseguito il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="4c503-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="4c503-123">È possibile distribuire più ruoli di lavoro in tutta l'organizzazione e i clienti possono quindi sfruttare potenza di calcolo di riserva.</span><span class="sxs-lookup"><span data-stu-id="4c503-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="4c503-124">Requisiti minimi</span><span class="sxs-lookup"><span data-stu-id="4c503-124">Minimum Requirements</span></span>

<span data-ttu-id="4c503-125">Per iniziare a usare il runtime di Funzioni di Azure è necessario disporre di un computer con **Windows Server 2016 o Windows 10 Creators Update** con accesso a un'istanza di **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4c503-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c503-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c503-126">Next Steps</span></span>

<span data-ttu-id="4c503-127">Installare l'[anteprima del runtime di Funzioni di Azure](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="4c503-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
