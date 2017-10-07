---
title: sicurezza aaaIntegrate in progettazioni dell'architettura Azure | Documenti Microsoft
description: " In questo articolo consentono di comprendere l'architettura di servizi e l'applicazione hello in Azure toomake è più semplice della sicurezza di toointegrate nella progettazione e implementazione. "
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
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="e1c2a-103">Architettura delle applicazioni in Azure</span><span class="sxs-lookup"><span data-stu-id="e1c2a-103">Application architecture on Azure</span></span>
<span data-ttu-id="e1c2a-104">toohelp proteggere le soluzioni basate su cloud in Microsoft Azure, una solida architettura è fondamentale.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="e1c2a-105">Architetti, progettisti e responsabili dell'implementazione beneficiano di una conoscenza avanzata dell'architettura di applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="e1c2a-106">Questa knowledge base conoscenza di comprendere tutti i componenti di hello delle soluzioni basate su cloud e rendono più semplice toointegrate protezione in tutti gli aspetti della progettazione e implementazione.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="e1c2a-107">È stata hello seguenti toohelp si con l'analisi dell'architettura e progettazione:</span><span class="sxs-lookup"><span data-stu-id="e1c2a-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="e1c2a-108">Infografici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="e1c2a-108">Architectural infographics</span></span>
* <span data-ttu-id="e1c2a-109">Progetti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="e1c2a-109">Architectural blueprints</span></span>
* <span data-ttu-id="e1c2a-110">Set di simboli per Cloud ed Enterprise</span><span class="sxs-lookup"><span data-stu-id="e1c2a-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="e1c2a-111">Modello di progetto Visio 3D</span><span class="sxs-lookup"><span data-stu-id="e1c2a-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="e1c2a-112">Infografici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="e1c2a-112">Architectural infographics</span></span>
<span data-ttu-id="e1c2a-113">Microsoft pubblica vari poster/infografici relativi all'architettura,</span><span class="sxs-lookup"><span data-stu-id="e1c2a-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="e1c2a-114">tra cui:</span><span class="sxs-lookup"><span data-stu-id="e1c2a-114">They include:</span></span>

* [<span data-ttu-id="e1c2a-115">Creazione di app reali per il cloud</span><span class="sxs-lookup"><span data-stu-id="e1c2a-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="e1c2a-116">Scalabilità delle applicazioni con Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="e1c2a-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="e1c2a-117">Progetti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="e1c2a-117">Architectural blueprints</span></span>
<span data-ttu-id="e1c2a-118">Microsoft pubblica un set di alto livello [disegni architetturali](http://aka.ms/azblueprints) che mostra come toobuild tipi specifici di sistemi che utilizzano i prodotti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="e1c2a-119">Ogni progetto include:</span><span class="sxs-lookup"><span data-stu-id="e1c2a-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="e1c2a-120">File flat 2D basato su Visio 2003 che è possibile scaricare e modificare</span><span class="sxs-lookup"><span data-stu-id="e1c2a-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="e1c2a-121">File di prospettiva 3D colorato PDF personale tecnico tooless toointroduce hello progetto iniziale</span><span class="sxs-lookup"><span data-stu-id="e1c2a-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="e1c2a-122">Video che illustra fino alla versione di hello 3D</span><span class="sxs-lookup"><span data-stu-id="e1c2a-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="e1c2a-123">Set di simboli per Cloud ed Enterprise</span><span class="sxs-lookup"><span data-stu-id="e1c2a-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="e1c2a-124">[Visualizzare hello Visio e i simboli di formazione video](http://aka.ms/CnESymbolsVideo) e quindi [scaricare il set di Cloud e il simbolo Enterprise hello](http://aka.ms/CnESymbols) toohelp creare materiale tecnici che descrivono Azure, Windows Server, SQL Server e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="e1c2a-125">È possibile utilizzare i simboli di hello nei diagrammi dell'architettura, materiali di formazione, presentazioni, fogli dati, infografiche, white paper e documentazione di terze parti anche se hello libro treni persone toouse i prodotti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="e1c2a-126">Tuttavia non possono essere usati nelle interfacce utente.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="e1c2a-127">Modello di progetto Visio 3D</span><span class="sxs-lookup"><span data-stu-id="e1c2a-127">3D blueprint Visio template</span></span>
<span data-ttu-id="e1c2a-128">Hello versioni 3D di hello [progetti sull'architettura Microsoft](http://aka.ms/azblueprints) creati inizialmente in uno strumento non Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="e1c2a-129">Il modello Visio 2013 (e versioni successive) è arrivato il 5 agosto 2015 come parte di un [Corso di certificazione per Microsoft Architecture](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course)distribuito su EDX.ORG.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="e1c2a-130">modello di Hello è anche disponibile di fuori del corso hello.</span><span class="sxs-lookup"><span data-stu-id="e1c2a-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="e1c2a-131">[Visualizzare il video di formazione hello](http://aka.ms/3dBlueprintTemplateVideo) prima per sapere cosa può fare</span><span class="sxs-lookup"><span data-stu-id="e1c2a-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="e1c2a-132">Scaricare hello [Microsoft 3d modello di progetto iniziale di Visio](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="e1c2a-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="e1c2a-133">Scaricare hello [Cloud e i simboli Enterprise](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse con modello 3D hello</span><span class="sxs-lookup"><span data-stu-id="e1c2a-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
