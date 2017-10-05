---
title: Introduzione al playbook PoC di Azure Active Directory | Microsoft Docs
description: "Esplorare e implementare rapidamente gli scenari di Gestione delle identità e degli accessi"
services: active-directory
keywords: azure active directory, playbook, modello di verifica, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="c1c03-104">Playbook dei modelli di verifica di Azure Active Directory: introduzione</span><span class="sxs-lookup"><span data-stu-id="c1c03-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="c1c03-105">In questo articolo vengono fornite linee guida per l'esplorazione di diverse funzionalità di Azure AD in un Proof of Concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="c1c03-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="c1c03-106">I destinatari di questo documento sono gli architetti di identità, i professionisti IT e gli integratori di sistemi</span><span class="sxs-lookup"><span data-stu-id="c1c03-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="c1c03-107">Come usare questo playbook</span><span class="sxs-lookup"><span data-stu-id="c1c03-107">How to use this Playbook</span></span>

1. <span data-ttu-id="c1c03-108">Usare la sezione [Tema](active-directory-playbook-ingredients.md#theme) e selezionare le aree di interesse in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c1c03-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="c1c03-109">Definire l'ambito del PoC scegliendo gli scenari in linea con gli obiettivi aziendali.</span><span class="sxs-lookup"><span data-stu-id="c1c03-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="c1c03-110">L'ambito deve essere il più ristretto possibile.</span><span class="sxs-lookup"><span data-stu-id="c1c03-110">The shorter the better.</span></span> <span data-ttu-id="c1c03-111">Si consiglia di definire un ambito il più breve e conciso possibile in modo da veicolarne il valore alle parti interessate, riducendone al minimo la complessità di realizzazione.</span><span class="sxs-lookup"><span data-stu-id="c1c03-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="c1c03-112">Usare la sezione [Implementazione](active-directory-playbook-implementation.md) per comprendere gli scenari e il relativo significato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="c1c03-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="c1c03-113">In ogni scenario viene descritto come eseguire la configurazione (i cosiddetti [blocchi predefiniti](active-directory-playbook-building-blocks.md)) e come passare da uno scenario all'altro.</span><span class="sxs-lookup"><span data-stu-id="c1c03-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="c1c03-114">In ogni blocco predefinito vengono illustrati i prerequisiti necessari, nonché il tempo approssimativo necessario per il completamento.</span><span class="sxs-lookup"><span data-stu-id="c1c03-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="c1c03-115">Ciò costituisce un valido supporto durante il processo di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="c1c03-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="c1c03-116">In base ai passaggi da 1 a 3 sopra riportati, definire l'[ambiente](active-directory-playbook-ingredients.md#environment) in cui si desidera eseguire le operazioni.</span><span class="sxs-lookup"><span data-stu-id="c1c03-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="c1c03-117">Si consiglia di creare un ambiente di produzione che offra la migliore esperienza possibile per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c1c03-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="c1c03-118">In presenza di requisiti in conflitto, utilizzare questa utile matrice per trovare un compromesso</span><span class="sxs-lookup"><span data-stu-id="c1c03-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="c1c03-119">Visualizzazione incentrata sul tema del valore</span><span class="sxs-lookup"><span data-stu-id="c1c03-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="c1c03-120">Precisione nella preparazione, configurazione ed esecuzione degli scenari</span><span class="sxs-lookup"><span data-stu-id="c1c03-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="c1c03-121">Tempo minimo richiesto per eseguire gli scenari di destinazione</span><span class="sxs-lookup"><span data-stu-id="c1c03-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="c1c03-122">Esecuzione in linea il più possibile alla produzione all'interno dei vincoli</span><span class="sxs-lookup"><span data-stu-id="c1c03-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="c1c03-123">In questo articolo, verranno mostrate alcune applicazioni e prodotti di terze parti specifici citati a titolo esemplificativo per comodità.</span><span class="sxs-lookup"><span data-stu-id="c1c03-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="c1c03-124">Azure AD supporta migliaia di applicazioni incluse nella [raccolta delle applicazioni](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) che è possibile utilizzare in base alle esigenze e all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="c1c03-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]