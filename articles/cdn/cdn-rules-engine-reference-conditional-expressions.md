---
title: espressioni condizionali motore regole di aaaAzure CDN | Documenti Microsoft
description: "Documentazione di riferimento per le funzionalità e condizioni di corrispondenza del motore regole della rete CDN di Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="254e8-103">Espressioni condizionali del motore regole della rete CDN</span><span class="sxs-lookup"><span data-stu-id="254e8-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="254e8-104">In questo argomento elenca le descrizioni dettagliate di hello espressioni condizionali per Azure rete CDN (Content Delivery) [motore regole di business](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="254e8-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="254e8-105">Hello prima parte di una regola è hello espressione condizionale.</span><span class="sxs-lookup"><span data-stu-id="254e8-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="254e8-106">Espressione condizionale</span><span class="sxs-lookup"><span data-stu-id="254e8-106">Conditional Expression</span></span> | <span data-ttu-id="254e8-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="254e8-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="254e8-108">IF</span><span class="sxs-lookup"><span data-stu-id="254e8-108">IF</span></span> | <span data-ttu-id="254e8-109">Un'espressione IF è sempre una parte di hello prima istruzione di una regola.</span><span class="sxs-lookup"><span data-stu-id="254e8-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="254e8-110">Come tutte le altre espressioni condizionali, l'istruzione IF deve essere associata a una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="254e8-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="254e8-111">Se non sono definite alcun espressioni condizionali aggiuntive, questa corrispondenza determina criterio hello che deve essere soddisfatte prima di un set di funzionalità può essere applicato tooa richiesta.</span><span class="sxs-lookup"><span data-stu-id="254e8-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="254e8-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="254e8-112">AND IF</span></span> | <span data-ttu-id="254e8-113">Un'espressione e se può essere aggiunti solo dopo i seguenti tipi di espressioni: se condizionale, e se hello.</span><span class="sxs-lookup"><span data-stu-id="254e8-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="254e8-114">Indica che è presente un'altra condizione che deve essere soddisfatte per l'istruzione IF iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="254e8-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="254e8-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="254e8-115">ELSE IF</span></span>| <span data-ttu-id="254e8-116">Un'espressione ELSE IF specifica una condizione alternativa che deve essere soddisfatte prima che un set di funzionalità specifiche toothis istruzione ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="254e8-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="254e8-117">presenza di Hello di un'istruzione ELSE IF indica fine hello dell'istruzione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="254e8-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="254e8-118">espressione condizionale solo Hello che può essere inserito dopo un'istruzione ELSE IF è un'altra istruzione ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="254e8-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="254e8-119">Ciò significa che un'istruzione IF ELSE può essere solo toospecify usato una sola condizione aggiuntiva con toobe soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="254e8-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="254e8-120">**Esempio**: ![condizione di corrispondenza della rete CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="254e8-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="254e8-121">Una regola successive può eseguire l'override di azioni hello specificate da una regola precedente.</span><span class="sxs-lookup"><span data-stu-id="254e8-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="254e8-122">Esempio: una regola di catch-all protegge tutte le richieste tramite l'autenticazione basata su token.</span><span class="sxs-lookup"><span data-stu-id="254e8-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="254e8-123">Un'altra regola può essere creata direttamente di sotto toomake un'eccezione per alcuni tipi di richieste.</span><span class="sxs-lookup"><span data-stu-id="254e8-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="254e8-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="254e8-124">Next steps</span></span>
* [<span data-ttu-id="254e8-125">Panoramica della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="254e8-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="254e8-126">Informazioni di riferimento sul motore regole</span><span class="sxs-lookup"><span data-stu-id="254e8-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="254e8-127">Condizioni di corrispondenza del motore regole</span><span class="sxs-lookup"><span data-stu-id="254e8-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="254e8-128">Funzionalità del motore regole</span><span class="sxs-lookup"><span data-stu-id="254e8-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="254e8-129">Override del comportamento HTTP predefinito utilizzando il motore regole di hello</span><span class="sxs-lookup"><span data-stu-id="254e8-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
