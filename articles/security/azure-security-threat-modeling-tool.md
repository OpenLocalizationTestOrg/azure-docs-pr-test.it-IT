---
title: Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: pagina principale per il Microsoft Threat Modeling Tool, contenente informazioni per iniziare a usare lo strumento, incluso il processo di modellazione delle minacce
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
ms.openlocfilehash: 6e26b0af2a16a872c8e02b736e24019b47ed5780
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="41bc1-103">Microsoft Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="41bc1-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="41bc1-104">Microsoft Threat Modeling Tool è un elemento principale di Microsoft Security Development Lifecycle (SDL).</span><span class="sxs-lookup"><span data-stu-id="41bc1-104">The Threat Modeling Tool is a core element of the Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="41bc1-105">Consente ai progettisti di software di identificare e ridurre tempestivamente i potenziali problemi di sicurezza, quando sono relativamente semplici e convenienti da risolvere.</span><span class="sxs-lookup"><span data-stu-id="41bc1-105">It allows software architects to identify and mitigate potential security issues early, when they are relatively easy and cost-effective to resolve.</span></span> <span data-ttu-id="41bc1-106">Di conseguenza, riduce notevolmente i costi totali di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="41bc1-106">As a result, it greatly reduces the total cost of development.</span></span> <span data-ttu-id="41bc1-107">Inoltre, lo strumento è progettato pensando agli esperti non relativi alla sicurezza, poiché semplifica la modellazione delle minacce per tutti gli sviluppatori fornendo istruzioni chiare sulla creazione e sull'analisi dei modelli di rischio.</span><span class="sxs-lookup"><span data-stu-id="41bc1-107">Also, we designed the tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="41bc1-108">Lo strumento consente a tutti gli utenti di:</span><span class="sxs-lookup"><span data-stu-id="41bc1-108">The tool enables anyone to:</span></span>

* <span data-ttu-id="41bc1-109">Parlare della progettazione della protezione dei sistemi</span><span class="sxs-lookup"><span data-stu-id="41bc1-109">Communicate about the security design of their systems</span></span>
* <span data-ttu-id="41bc1-110">Analizzare le progettazioni per individuare potenziali problemi di sicurezza usando una metodologia comprovata</span><span class="sxs-lookup"><span data-stu-id="41bc1-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="41bc1-111">Suggerire e gestire soluzioni di prevenzione per problemi di protezione</span><span class="sxs-lookup"><span data-stu-id="41bc1-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="41bc1-112">Ecco alcune funzionalità degli strumenti e innovazioni, solo per citarne alcune:</span><span class="sxs-lookup"><span data-stu-id="41bc1-112">Here are some tooling capabilities and innovations, just to name a few:</span></span>

* <span data-ttu-id="41bc1-113">**Automazione:** linee guida e feedback sulla definizione di un modello</span><span class="sxs-lookup"><span data-stu-id="41bc1-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="41bc1-114">**STRIDE per ogni elemento:** analisi guidata di minacce e soluzioni di prevenzione</span><span class="sxs-lookup"><span data-stu-id="41bc1-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="41bc1-115">**Creazione di report:** attività di protezione e test in fase di verifica</span><span class="sxs-lookup"><span data-stu-id="41bc1-115">**Reporting:** Security activities and testing in the verification phase</span></span>
* <span data-ttu-id="41bc1-116">**Metodologia univoca:** consente agli utenti di visualizzare meglio e conoscere le minacce</span><span class="sxs-lookup"><span data-stu-id="41bc1-116">**Unique Methodology:** Enables users to better visualize and understand threats</span></span>
* <span data-ttu-id="41bc1-117">**Progettato per gli sviluppatori e incentrato sul software:** molti approcci sono incentrati su risorse o utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="41bc1-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="41bc1-118">Noi ci siamo concentrati sul software.</span><span class="sxs-lookup"><span data-stu-id="41bc1-118">We are centered on software.</span></span> <span data-ttu-id="41bc1-119">Facciamo leva sulle attività con cui tutti gli sviluppatori di software e i progettisti hanno familiarità, ad esempio il disegno di immagini per l'architettura software</span><span class="sxs-lookup"><span data-stu-id="41bc1-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="41bc1-120">**Concentrazione sull'analisi della progettazione:** il termine "modellazione delle minacce" può fare riferimento a un requisito o una tecnica di analisi della progettazione.</span><span class="sxs-lookup"><span data-stu-id="41bc1-120">**Focused on Design Analysis:** The term "threat modeling" can refer to either a requirements or a design analysis technique.</span></span> <span data-ttu-id="41bc1-121">In alcuni casi, si riferisce a una combinazione complessa dei due.</span><span class="sxs-lookup"><span data-stu-id="41bc1-121">Sometimes, it refers to a complex blend of the two.</span></span> <span data-ttu-id="41bc1-122">L'approccio Microsoft SDL alla modellazione delle minacce è una tecnica di analisi di progettazione focalizzata</span><span class="sxs-lookup"><span data-stu-id="41bc1-122">The Microsoft SDL approach to threat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="41bc1-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41bc1-123">Next steps</span></span>

<span data-ttu-id="41bc1-124">La tabella seguente contiene collegamenti importanti per iniziare a usare Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="41bc1-124">The table below contains important links to get you started with the Threat Modeling Tool:</span></span>

| <span data-ttu-id="41bc1-125">Passaggio</span><span class="sxs-lookup"><span data-stu-id="41bc1-125">Step</span></span>  | <span data-ttu-id="41bc1-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="41bc1-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="41bc1-127">**1**</span><span class="sxs-lookup"><span data-stu-id="41bc1-127">**1**</span></span> | [<span data-ttu-id="41bc1-128">Scaricare Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="41bc1-128">Download the Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="41bc1-129">**2**</span><span class="sxs-lookup"><span data-stu-id="41bc1-129">**2**</span></span> | [<span data-ttu-id="41bc1-130">Vedere la Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="41bc1-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="41bc1-131">**3**</span><span class="sxs-lookup"><span data-stu-id="41bc1-131">**3**</span></span> | [<span data-ttu-id="41bc1-132">Acquisire familiarità con le funzionalità</span><span class="sxs-lookup"><span data-stu-id="41bc1-132">Get familiar with the features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="41bc1-133">**4**</span><span class="sxs-lookup"><span data-stu-id="41bc1-133">**4**</span></span> | [<span data-ttu-id="41bc1-134">Informazioni sulle categorie di minacce generate</span><span class="sxs-lookup"><span data-stu-id="41bc1-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="41bc1-135">**5**</span><span class="sxs-lookup"><span data-stu-id="41bc1-135">**5**</span></span> | [<span data-ttu-id="41bc1-136">Trovare soluzioni di prevenzione per le minacce generate</span><span class="sxs-lookup"><span data-stu-id="41bc1-136">Find mitigations to generated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="41bc1-137">Risorse</span><span class="sxs-lookup"><span data-stu-id="41bc1-137">Resources</span></span>

<span data-ttu-id="41bc1-138">Di seguito sono illustrati alcuni articoli più datati ancora rilevanti per la modellazione delle minacce:</span><span class="sxs-lookup"><span data-stu-id="41bc1-138">Here are a few older articles still relevant to threat modeling today:</span></span>

* [<span data-ttu-id="41bc1-139">Articolo sull'importanza della modellazione delle minacce</span><span class="sxs-lookup"><span data-stu-id="41bc1-139">Article on the Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="41bc1-140">Training pubblicato da Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="41bc1-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="41bc1-141">Controllare quello che hanno fatto alcuni esperti di Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="41bc1-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="41bc1-142">Gestione delle minacce</span><span class="sxs-lookup"><span data-stu-id="41bc1-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="41bc1-143">Blog sulla protezione di Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="41bc1-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)