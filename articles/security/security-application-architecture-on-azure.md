---
title: Integrare la sicurezza nei progetti di architettura di Azure | Documentazione Microsoft
description: " In questo articolo consente di comprendere l'architettura di applicazioni e servizi in Azure per semplificare l'integrazione della sicurezza nella progettazione e nell'implementazione. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="f9d8d-103">Architettura delle applicazioni in Azure</span><span class="sxs-lookup"><span data-stu-id="f9d8d-103">Application architecture on Azure</span></span>
<span data-ttu-id="f9d8d-104">Per proteggere le soluzioni basate sul cloud in Microsoft Azure, è fondamentale avere un'architettura affidabile.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="f9d8d-105">Architetti, progettisti e responsabili dell'implementazione beneficiano di una conoscenza avanzata dell'architettura di applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="f9d8d-106">Queste informazioni fondamentali permettono di comprendere tutti i componenti delle soluzioni basate sul cloud e semplificano l'integrazione della sicurezza in tutti gli aspetti della progettazione e dell'implementazione.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="f9d8d-107">Per semplificare l'analisi dell'architettura e la progettazione, sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="f9d8d-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="f9d8d-108">Infografici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="f9d8d-108">Architectural infographics</span></span>
* <span data-ttu-id="f9d8d-109">Progetti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="f9d8d-109">Architectural blueprints</span></span>
* <span data-ttu-id="f9d8d-110">Set di simboli per Cloud ed Enterprise</span><span class="sxs-lookup"><span data-stu-id="f9d8d-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="f9d8d-111">Modello di progetto Visio 3D</span><span class="sxs-lookup"><span data-stu-id="f9d8d-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="f9d8d-112">Infografici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="f9d8d-112">Architectural infographics</span></span>
<span data-ttu-id="f9d8d-113">Microsoft pubblica vari poster/infografici relativi all'architettura,</span><span class="sxs-lookup"><span data-stu-id="f9d8d-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="f9d8d-114">tra cui:</span><span class="sxs-lookup"><span data-stu-id="f9d8d-114">They include:</span></span>

* [<span data-ttu-id="f9d8d-115">Creazione di app reali per il cloud</span><span class="sxs-lookup"><span data-stu-id="f9d8d-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="f9d8d-116">Scalabilità delle applicazioni con Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="f9d8d-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="f9d8d-117">Progetti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="f9d8d-117">Architectural blueprints</span></span>
<span data-ttu-id="f9d8d-118">Microsoft pubblica un set di [Progetti dell'architettura](http://aka.ms/azblueprints) generali che illustrano come creare tipi specifici di sistemi usando prodotti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="f9d8d-119">Ogni progetto include:</span><span class="sxs-lookup"><span data-stu-id="f9d8d-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="f9d8d-120">File flat 2D basato su Visio 2003 che è possibile scaricare e modificare</span><span class="sxs-lookup"><span data-stu-id="f9d8d-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="f9d8d-121">File PDF in prospettiva 3D a colori per presentare il progetto a destinatari con minori competenze tecniche</span><span class="sxs-lookup"><span data-stu-id="f9d8d-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="f9d8d-122">Video che illustra la versione 3D</span><span class="sxs-lookup"><span data-stu-id="f9d8d-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="f9d8d-123">Set di simboli per Cloud ed Enterprise</span><span class="sxs-lookup"><span data-stu-id="f9d8d-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="f9d8d-124">[Guardare il video di training su simboli e Visio](http://aka.ms/CnESymbolsVideo) e quindi [scaricare il set di simboli per Cloud ed Enterprise](http://aka.ms/CnESymbols) per creare materiali tecnici che illustrano Azure, Windows Server, SQL Server e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="f9d8d-125">È possibile usarli in diagrammi di architettura, materiale didattico, presentazioni, fogli dati, infografica, white paper e anche in manuali di terze parti, se sono destinati alla formazione sull'uso di prodotti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="f9d8d-126">Tuttavia non possono essere usati nelle interfacce utente.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="f9d8d-127">Modello di progetto Visio 3D</span><span class="sxs-lookup"><span data-stu-id="f9d8d-127">3D blueprint Visio template</span></span>
<span data-ttu-id="f9d8d-128">Le versioni 3D dei [Progetti di Microsoft Architecture](http://aka.ms/azblueprints) sono stati creati inizialmente in uno strumento non Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="f9d8d-129">Il modello Visio 2013 (e versioni successive) è arrivato il 5 agosto 2015 come parte di un [Corso di certificazione per Microsoft Architecture](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course)distribuito su EDX.ORG.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="f9d8d-130">Il modello è anche disponibile al di fuori del corso.</span><span class="sxs-lookup"><span data-stu-id="f9d8d-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="f9d8d-131">[Visualizzare prima il video di training](http://aka.ms/3dBlueprintTemplateVideo) in modo da sapere quali operazione eseguire</span><span class="sxs-lookup"><span data-stu-id="f9d8d-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="f9d8d-132">Scaricare [Microsoft 3D Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="f9d8d-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="f9d8d-133">Scaricare i [simboli di Cloud ed Enterprise](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) da usare con il modello 3D</span><span class="sxs-lookup"><span data-stu-id="f9d8d-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
