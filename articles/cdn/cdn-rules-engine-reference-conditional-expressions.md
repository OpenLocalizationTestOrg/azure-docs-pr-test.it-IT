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
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Espressioni condizionali del motore regole della rete CDN
In questo argomento elenca le descrizioni dettagliate di hello espressioni condizionali per Azure rete CDN (Content Delivery) [motore regole di business](cdn-rules-engine.md).

Hello prima parte di una regola è hello espressione condizionale.

Espressione condizionale | Descrizione
-----------------------|-------------
IF | Un'espressione IF è sempre una parte di hello prima istruzione di una regola. Come tutte le altre espressioni condizionali, l'istruzione IF deve essere associata a una corrispondenza. Se non sono definite alcun espressioni condizionali aggiuntive, questa corrispondenza determina criterio hello che deve essere soddisfatte prima di un set di funzionalità può essere applicato tooa richiesta.
AND IF | Un'espressione e se può essere aggiunti solo dopo i seguenti tipi di espressioni: se condizionale, e se hello. Indica che è presente un'altra condizione che deve essere soddisfatte per l'istruzione IF iniziale hello.
ELSE IF| Un'espressione ELSE IF specifica una condizione alternativa che deve essere soddisfatte prima che un set di funzionalità specifiche toothis istruzione ELSE IF. presenza di Hello di un'istruzione ELSE IF indica fine hello dell'istruzione precedente hello. espressione condizionale solo Hello che può essere inserito dopo un'istruzione ELSE IF è un'altra istruzione ELSE IF. Ciò significa che un'istruzione IF ELSE può essere solo toospecify usato una sola condizione aggiuntiva con toobe soddisfatti.

**Esempio**: ![condizione di corrispondenza della rete CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Una regola successive può eseguire l'override di azioni hello specificate da una regola precedente. Esempio: una regola di catch-all protegge tutte le richieste tramite l'autenticazione basata su token. Un'altra regola può essere creata direttamente di sotto toomake un'eccezione per alcuni tipi di richieste.

### <a name="next-steps"></a>Passaggi successivi
* [Panoramica della rete CDN di Azure](cdn-overview.md)
* [Informazioni di riferimento sul motore regole](cdn-rules-engine-reference.md)
* [Condizioni di corrispondenza del motore regole](cdn-rules-engine-reference-match-conditions.md)
* [Funzionalità del motore regole](cdn-rules-engine-reference-features.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
