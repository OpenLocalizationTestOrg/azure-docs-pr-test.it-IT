---
title: Cenni preliminari sul Runtime di funzioni aaaAzure | Documenti Microsoft
description: Panoramica di hello anteprima di Azure funzioni di Runtime
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
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="37cb9-103">Panoramica di Runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="37cb9-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="37cb9-104">Hello Azure funzioni di Runtime fornisce un nuovo modo per si tootake vantaggio della semplicità hello e la flessibilità di hello Azure funzioni di programmazione del modello locale.</span><span class="sxs-lookup"><span data-stu-id="37cb9-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="37cb9-105">Basato su hello stesso aprire radici di origine come funzioni di Azure, Azure funzioni di Runtime è quasi identica per lo sviluppo esperienza come servizio cloud hello tooprovide di distribuiti in locale.</span><span class="sxs-lookup"><span data-stu-id="37cb9-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Anteprima del runtime di Funzioni di Azure - Portale][1]

<span data-ttu-id="37cb9-107">Hello Azure funzioni Runtime fornisce un modo per si tooexperience le funzioni di Azure prima del commit toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="37cb9-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="37cb9-108">In questo modo, risorse di codice hello che compili quindi è possibile portare toohello cloud quando esegue la migrazione.</span><span class="sxs-lookup"><span data-stu-id="37cb9-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="37cb9-109">runtime Hello apre anche nuove opzioni per l'utente, ad esempio l'utilizzo di potenza di calcolo riserva hello dei processi batch toorun computer locale durante la notte.</span><span class="sxs-lookup"><span data-stu-id="37cb9-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="37cb9-110">È anche possibile utilizzare i dispositivi all'interno dell'organizzazione tooconditionally trasmissione dati tooother sistemi, sia in locale e nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="37cb9-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="37cb9-111">Hello Azure funzioni di Runtime è costituito da due parti:</span><span class="sxs-lookup"><span data-stu-id="37cb9-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="37cb9-112">Il ruolo di gestione del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="37cb9-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="37cb9-113">Il ruolo di lavoro del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="37cb9-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="37cb9-114">Il ruolo di gestione di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="37cb9-114">Azure Functions Management Role</span></span>

<span data-ttu-id="37cb9-115">Ruolo di gestione di Azure funzioni Hello fornisce un host per la gestione di hello di funzioni locali.</span><span class="sxs-lookup"><span data-stu-id="37cb9-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="37cb9-116">Questo ruolo esegue hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="37cb9-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="37cb9-117">Hosting del portale di gestione di Azure funzioni, hello è hello hello stesso viene visualizzato in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37cb9-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="37cb9-118">Questo consente di sviluppare le funzioni in hello stesso modo come si farebbe in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37cb9-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="37cb9-119">La distribuzione di funzioni tra più ruoli di lavoro di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="37cb9-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="37cb9-120">La garanzia di un endpoint di pubblicazione in modo che sia possibile pubblicare direttamente le funzioni da Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37cb9-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="37cb9-121">Ruolo di lavoro di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="37cb9-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="37cb9-122">i ruoli di lavoro funzioni Hello Azure vengono distribuiti nei contenitori di Windows e si tratta in cui viene eseguito il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="37cb9-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="37cb9-123">È possibile distribuire più ruoli di lavoro in tutta l'organizzazione e i clienti possono quindi sfruttare potenza di calcolo di riserva.</span><span class="sxs-lookup"><span data-stu-id="37cb9-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="37cb9-124">Requisiti minimi</span><span class="sxs-lookup"><span data-stu-id="37cb9-124">Minimum Requirements</span></span>

<span data-ttu-id="37cb9-125">tooget introduttiva hello Azure funzioni di Runtime è necessario disporre di un computer con **Windows Server 2016 o Windows 10 creatori Update** con accesso tooa **SQL Server** istanza.</span><span class="sxs-lookup"><span data-stu-id="37cb9-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37cb9-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37cb9-126">Next Steps</span></span>

<span data-ttu-id="37cb9-127">Installare hello [anteprima di Azure funzioni Runtime](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="37cb9-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
