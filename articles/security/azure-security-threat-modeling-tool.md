---
title: aaaMicrosoft dello strumento di modellazione minaccia, Azure | Documenti Microsoft
description: pagina principale per hello Microsoft Threat strumento di modellazione, che contiene informazioni introduttive sull'utilizzo dello strumento hello, tra cui il processo di modellazione delle minacce hello
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="70d7c-103">Microsoft Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="70d7c-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="70d7c-104">Strumento di modellazione delle minacce Hello è un elemento principale di hello Microsoft Security Development Lifecycle (SDL).</span><span class="sxs-lookup"><span data-stu-id="70d7c-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="70d7c-105">Consente di software progettisti tooidentify e attenuare i potenziali problemi di sicurezza in anticipo, quando sono tooresolve relativamente semplice e conveniente.</span><span class="sxs-lookup"><span data-stu-id="70d7c-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="70d7c-106">Di conseguenza, riduce notevolmente il costo totale di hello di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="70d7c-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="70d7c-107">Inoltre, è progettato strumento hello con gli esperti di protezione non presente, semplificando la modellazione delle minacce per tutti gli sviluppatori fornendo indicazioni precise sulla creazione e l'analisi dei modelli di rischio.</span><span class="sxs-lookup"><span data-stu-id="70d7c-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="70d7c-108">strumento Hello consente a tutti gli utenti:</span><span class="sxs-lookup"><span data-stu-id="70d7c-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="70d7c-109">Comunicare sulla progettazione di sicurezza hello dei sistemi</span><span class="sxs-lookup"><span data-stu-id="70d7c-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="70d7c-110">Analizzare le progettazioni per individuare potenziali problemi di sicurezza usando una metodologia comprovata</span><span class="sxs-lookup"><span data-stu-id="70d7c-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="70d7c-111">Suggerire e gestire soluzioni di prevenzione per problemi di protezione</span><span class="sxs-lookup"><span data-stu-id="70d7c-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="70d7c-112">Ecco alcune funzionalità di strumenti e le innovazioni, tooname solo alcuni:</span><span class="sxs-lookup"><span data-stu-id="70d7c-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="70d7c-113">**Automazione:** linee guida e feedback sulla definizione di un modello</span><span class="sxs-lookup"><span data-stu-id="70d7c-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="70d7c-114">**STRIDE per ogni elemento:** analisi guidata di minacce e soluzioni di prevenzione</span><span class="sxs-lookup"><span data-stu-id="70d7c-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="70d7c-115">**Creazione di report:** le attività di protezione e il test in fase di verifica hello</span><span class="sxs-lookup"><span data-stu-id="70d7c-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="70d7c-116">**Metodologia univoco:** toobetter utenti consente di visualizzare e comprendere le minacce</span><span class="sxs-lookup"><span data-stu-id="70d7c-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="70d7c-117">**Progettato per gli sviluppatori e incentrato sul software:** molti approcci sono incentrati su risorse o utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="70d7c-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="70d7c-118">Noi ci siamo concentrati sul software.</span><span class="sxs-lookup"><span data-stu-id="70d7c-118">We are centered on software.</span></span> <span data-ttu-id="70d7c-119">Facciamo leva sulle attività con cui tutti gli sviluppatori di software e i progettisti hanno familiarità, ad esempio il disegno di immagini per l'architettura software</span><span class="sxs-lookup"><span data-stu-id="70d7c-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="70d7c-120">**Esegue l'analisi della progettazione:** hello termine "modellazione delle minacce" può fare riferimento tooeither un requisito o una tecnica di analisi di progettazione.</span><span class="sxs-lookup"><span data-stu-id="70d7c-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="70d7c-121">In alcuni casi, si riferisce tooa blend complessi di hello due.</span><span class="sxs-lookup"><span data-stu-id="70d7c-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="70d7c-122">Hello Microsoft SDL approccio toothreat modellazione è una tecnica di analisi di progettazione con lo stato attivo</span><span class="sxs-lookup"><span data-stu-id="70d7c-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="70d7c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70d7c-123">Next steps</span></span>

<span data-ttu-id="70d7c-124">tabella Hello seguente contiene collegamenti importanti tooget che si è partiti hello strumento di modellazione delle minacce:</span><span class="sxs-lookup"><span data-stu-id="70d7c-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="70d7c-125">Passaggio</span><span class="sxs-lookup"><span data-stu-id="70d7c-125">Step</span></span>  | <span data-ttu-id="70d7c-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="70d7c-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="70d7c-127">**1**</span><span class="sxs-lookup"><span data-stu-id="70d7c-127">**1**</span></span> | [<span data-ttu-id="70d7c-128">Scaricare hello strumento di modellazione delle minacce</span><span class="sxs-lookup"><span data-stu-id="70d7c-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="70d7c-129">**2**</span><span class="sxs-lookup"><span data-stu-id="70d7c-129">**2**</span></span> | [<span data-ttu-id="70d7c-130">Vedere la Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="70d7c-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="70d7c-131">**3**</span><span class="sxs-lookup"><span data-stu-id="70d7c-131">**3**</span></span> | [<span data-ttu-id="70d7c-132">Acquisire familiarità con le funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="70d7c-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="70d7c-133">**4**</span><span class="sxs-lookup"><span data-stu-id="70d7c-133">**4**</span></span> | [<span data-ttu-id="70d7c-134">Informazioni sulle categorie di minacce generate</span><span class="sxs-lookup"><span data-stu-id="70d7c-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="70d7c-135">**5**</span><span class="sxs-lookup"><span data-stu-id="70d7c-135">**5**</span></span> | [<span data-ttu-id="70d7c-136">Trovare le misure di attenuazione di minacce toogenerated</span><span class="sxs-lookup"><span data-stu-id="70d7c-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="70d7c-137">Risorse</span><span class="sxs-lookup"><span data-stu-id="70d7c-137">Resources</span></span>

<span data-ttu-id="70d7c-138">Ecco alcuni precedenti articoli toothreat ancora rilevanti modellazione oggi:</span><span class="sxs-lookup"><span data-stu-id="70d7c-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="70d7c-139">Articolo su hello importanza della modellazione delle minacce</span><span class="sxs-lookup"><span data-stu-id="70d7c-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="70d7c-140">Training pubblicato da Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="70d7c-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="70d7c-141">Controllare quello che hanno fatto alcuni esperti di Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="70d7c-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="70d7c-142">Gestione delle minacce</span><span class="sxs-lookup"><span data-stu-id="70d7c-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="70d7c-143">Blog sulla protezione di Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="70d7c-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)