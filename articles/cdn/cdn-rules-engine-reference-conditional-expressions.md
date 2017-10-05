---
title: Espressioni condizionali del motore regole della rete CDN di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="4514f-103">Espressioni condizionali del motore regole della rete CDN</span><span class="sxs-lookup"><span data-stu-id="4514f-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="4514f-104">Questo argomento offre descrizioni dettagliate delle espressioni condizionali disponibili per il [motore regole](cdn-rules-engine.md) della rete per la distribuzione di contenuti (CDN, Content Delivery Network) di Azure.</span><span class="sxs-lookup"><span data-stu-id="4514f-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="4514f-105">La prima parte di una regola è l'espressione condizionale.</span><span class="sxs-lookup"><span data-stu-id="4514f-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="4514f-106">Espressione condizionale</span><span class="sxs-lookup"><span data-stu-id="4514f-106">Conditional Expression</span></span> | <span data-ttu-id="4514f-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4514f-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="4514f-108">IF</span><span class="sxs-lookup"><span data-stu-id="4514f-108">IF</span></span> | <span data-ttu-id="4514f-109">Un'espressione IF è sempre una parte della prima istruzione in una regola.</span><span class="sxs-lookup"><span data-stu-id="4514f-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="4514f-110">Come tutte le altre espressioni condizionali, l'istruzione IF deve essere associata a una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="4514f-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="4514f-111">Se non sono definite altre espressioni condizionali, questa corrispondenza determina il criterio che deve essere soddisfatto prima che sia possibile applicare un set di funzionalità a una richiesta.</span><span class="sxs-lookup"><span data-stu-id="4514f-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="4514f-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="4514f-112">AND IF</span></span> | <span data-ttu-id="4514f-113">Un'espressione AND IF può essere aggiunta solo dopo i tipi di espressioni condizionali seguenti: IF e AND IF.</span><span class="sxs-lookup"><span data-stu-id="4514f-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="4514f-114">Indica che esiste un'altra condizione che deve essere soddisfatta per l'istruzione IF iniziale.</span><span class="sxs-lookup"><span data-stu-id="4514f-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="4514f-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="4514f-115">ELSE IF</span></span>| <span data-ttu-id="4514f-116">Un'espressione ELSE IF specifica una condizione alternativa che deve essere soddisfatta prima che venga eseguita una serie di funzionalità specifiche di questa istruzione ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="4514f-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="4514f-117">La presenza di un'istruzione ELSE IF indica la fine dell'istruzione precedente.</span><span class="sxs-lookup"><span data-stu-id="4514f-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="4514f-118">L'unica espressione condizionale che può essere inserita dopo un'istruzione ELSE IF è un'altra istruzione ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="4514f-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="4514f-119">Ciò significa che un'istruzione ELSE IF può essere usata solo per specificare una sola condizione aggiuntiva da soddisfare.</span><span class="sxs-lookup"><span data-stu-id="4514f-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="4514f-120">**Esempio**: ![condizione di corrispondenza della rete CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="4514f-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="4514f-121">Una regola successiva potrebbe seguire l'override delle azioni specificate da una regola precedente.</span><span class="sxs-lookup"><span data-stu-id="4514f-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="4514f-122">Esempio: una regola di catch-all protegge tutte le richieste tramite l'autenticazione basata su token.</span><span class="sxs-lookup"><span data-stu-id="4514f-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="4514f-123">È possibile creare un'altra regola direttamente sotto questa per creare un'eccezione per alcuni tipi di richieste.</span><span class="sxs-lookup"><span data-stu-id="4514f-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4514f-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4514f-124">Next steps</span></span>
* [<span data-ttu-id="4514f-125">Panoramica della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="4514f-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="4514f-126">Informazioni di riferimento sul motore regole</span><span class="sxs-lookup"><span data-stu-id="4514f-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="4514f-127">Condizioni di corrispondenza del motore regole</span><span class="sxs-lookup"><span data-stu-id="4514f-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="4514f-128">Funzionalità del motore regole</span><span class="sxs-lookup"><span data-stu-id="4514f-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="4514f-129">Override del comportamento HTTP predefinito mediante il motore regole</span><span class="sxs-lookup"><span data-stu-id="4514f-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
