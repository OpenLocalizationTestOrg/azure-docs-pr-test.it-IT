---
title: Introduzione di Active Directory PoC Playbook aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="67a77-104">Playbook dei modelli di verifica di Azure Active Directory: introduzione</span><span class="sxs-lookup"><span data-stu-id="67a77-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="67a77-105">In questo articolo vengono fornite linee guida tooexplore Azure AD diverse funzionalità in un modello di verifica (PoC).</span><span class="sxs-lookup"><span data-stu-id="67a77-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="67a77-106">Hello destinato a destinatari di questo documento sono gli architetti di identità, i professionisti IT e integratori di sistemi</span><span class="sxs-lookup"><span data-stu-id="67a77-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="67a77-107">Come toouse questo Playbook</span><span class="sxs-lookup"><span data-stu-id="67a77-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="67a77-108">Hello utilizzare [tema](active-directory-playbook-ingredients.md#theme) sezione e selezionare hello aree di interesse in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="67a77-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="67a77-109">Definire l'ambito hello PoC scegliendo scenari hello allineati con gli obiettivi aziendali.</span><span class="sxs-lookup"><span data-stu-id="67a77-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="67a77-110">hello più breve Hello migliorato.</span><span class="sxs-lookup"><span data-stu-id="67a77-110">hello shorter hello better.</span></span> <span data-ttu-id="67a77-111">Si consiglia di eseguire l'operazione come short e conciso come valore di hello tooconvey possibili le parti interessate toohello riducendo al contempo hello toorealize complessità è.</span><span class="sxs-lookup"><span data-stu-id="67a77-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="67a77-112">Hello utilizzare [implementazione](active-directory-playbook-implementation.md) sezione toounderstand hello scenari e verrà loro significato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="67a77-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="67a77-113">In ogni scenario viene descritto come tooset, configurarlo (la cosiddetta [blocchi](active-directory-playbook-building-blocks.md)), e come toonavigate hello scenari.</span><span class="sxs-lookup"><span data-stu-id="67a77-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="67a77-114">Ogni blocco viene prerequisiti hello necessari, nonché un toocomplete approssimativamente il tempo previsto.</span><span class="sxs-lookup"><span data-stu-id="67a77-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="67a77-115">Questo può aiutare a durante il processo di pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="67a77-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="67a77-116">In base 1 a 3 sopra riportati, definire hello [ambiente](active-directory-playbook-ingredients.md#environment) in cui tooexecute.</span><span class="sxs-lookup"><span data-stu-id="67a77-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="67a77-117">Che incoraggia la collaborazione toostrive per un tooget ambiente di produzione una buona sensazione di esperienza hello per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="67a77-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="67a77-118">In presenza di requisiti in conflitto, utilizzare questa utile matrice per trovare un compromesso</span><span class="sxs-lookup"><span data-stu-id="67a77-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="67a77-119">Visualizzazione incentrata sul tema del valore</span><span class="sxs-lookup"><span data-stu-id="67a77-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="67a77-120">Scenari di hello tooprepare tooset backup e tooexecute Smoothness</span><span class="sxs-lookup"><span data-stu-id="67a77-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="67a77-121">Scenari di destinazione in tempi minimi tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="67a77-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="67a77-122">Come chiudere tooproduction come fattibile all'interno i vincoli</span><span class="sxs-lookup"><span data-stu-id="67a77-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="67a77-123">In questo articolo, verranno mostrate alcune applicazioni e prodotti di terze parti specifici citati a titolo esemplificativo per comodità.</span><span class="sxs-lookup"><span data-stu-id="67a77-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="67a77-124">Azure AD supporta migliaia di applicazioni incluse nella [raccolta delle applicazioni](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) che è possibile utilizzare in base alle esigenze e all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="67a77-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]