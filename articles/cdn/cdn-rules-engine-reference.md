---
title: riferimento al modulo di regole aaaAzure CDN | Documenti Microsoft
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Motore regole della rete CDN di Azure
In questo argomento elenca le descrizioni dettagliate delle funzionalità e le condizioni di corrispondenza disponibili di hello per Azure rete CDN (Content Delivery) [motore regole di business](cdn-rules-engine.md).

Hello HTTP motore regole di business è progettato toobe hello finale autorità specifica tipi di richieste vengono elaborate hello CDN.

**Usi comuni**:

- Eseguire l'override o definire un criterio della cache personalizzato.
- Proteggere o negare le richieste di contenuti sensibili.
- Reindirizzare le richieste.
- Archiviare i dati di log personalizzati.

## <a name="terminology"></a>Terminologia
Una regola è definita tramite l'utilizzo di hello di [ **espressioni condizionali**](cdn-rules-engine-reference-conditional-expressions.md), [ **corrisponde**](cdn-rules-engine-reference-match-conditions.md), e [  **funzionalità**](cdn-rules-engine-reference-features.md). Questi elementi vengono evidenziati in hello seguente illustrazione.

 ![Condizione di corrispondenza della rete CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Sintassi

modo Hello in cui verranno considerati caratteri speciali varia in base toohow una condizione di corrispondenza o valori di testo di handle di funzionalità. Una condizione di corrispondenza o la funzionalità potrebbe interpretare il testo in uno dei seguenti modi hello:

1. [**Valori letterali**](#literal-values) 
2. [**Valori caratteri jolly**](#wildcard-values)
3. [**Espressioni regolari**](#regular-expressions)

### <a name="literal-values"></a>Valori letterali
Testo che viene interpretato come un valore letterale considererà tutti i caratteri speciali, con l'eccezione di hello del simbolo % hello, come parte del valore di hello che deve corrispondere. In altre parole, un valore letterale corrisponde condizione impostata troppo`\'*'\` verrà soddisfatta solo quando il cui valore esatto (ad esempio, `\'*'\`) è stato trovato.
 
Un simbolo di percentuale è l'URL utilizzato tooindicate codifica (ad esempio, `%20`).

### <a name="wildcard-values"></a>Valori caratteri jolly
Testo che viene interpretato come valore di carattere jolly assegnerà caratteri toospecial significato aggiuntivo. Hello nella tabella seguente descrive come verrà interpretato hello seguente set di caratteri.

Character | Descrizione
----------|------------
\ | Una barra rovesciata è usato tooescape hello caratteri specificato in questa tabella. Una barra rovesciata deve essere specificata direttamente prima di un carattere speciale hello che deve essere sottoposto a escape.<br/>Ad esempio, la seguente sintassi hello ignora un asterisco:`\*`
% | Un simbolo di percentuale è l'URL utilizzato tooindicate codifica (ad esempio, `%20`).
* | L'asterisco è un carattere jolly che rappresenta uno o più caratteri.
Spazio | Un carattere di spazio indica che una condizione di corrispondenza può essere soddisfatto mediante hello specificato valori o i modelli.
"value" | Una virgoletta singola non ha un significato speciale. Tuttavia, in cui viene utilizzato un set di virgolette tooindicate che un valore deve essere considerato come un valore letterale. E può essere utilizzato in hello seguenti modi:<br><br/>-Consente un toobe di condizione di corrispondenza soddisfatta ogni volta che hello specificato valore corrisponde a qualsiasi parte del valore di confronto hello.  Ad esempio, `'ma'` corrisponderebbe a una delle seguenti stringhe hello: <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-Consente a un carattere speciale di toobe specificato come carattere letterale. Ad esempio, è possibile specificare un carattere di spazio letterale racchiudendo un carattere di spazio all'interno di un set di virgolette singole (ad esempio, `' '` o `'sample value'`).<br/>-Consente un valore vuoto di toobe specificato. Specificare un valore vuoto indicando un set di virgolette singole (ad esempio '').<br /><br/>**Importante:**<br/>-Se hello è specificato il valore non contiene un carattere jolly, quindi si verrà automaticamente considerato un valore letterale. Ciò significa che non è necessario toospecify un set di virgolette singole.<br/>- Se una barra rovesciata non effettua l'escape di un altro carattere in questa tabella, questo verrà ignorato se specificato all'interno di un set di virgolette singole.<br/>-Un altro modo toospecify un carattere speciale come carattere letterale è tooescape con una barra rovesciata (ad esempio, `\`).

### <a name="regular-expressions"></a>Espressioni regolari

Le espressioni regolari definiscono un modello che verrà cercato all'interno di un valore di testo. Notazione delle espressioni regolari definisce simboli svariati tooa un significato specifico. Nella tabella seguente Hello indica i caratteri speciali come vengono gestiti dalle condizioni di corrispondenza e le funzionalità che supportano le espressioni regolari.

Carattere speciale | Descrizione
------------------|------------
\ | Segue un hello carattere di barra rovesciata di escape hello. In questo modo toobe tale carattere considerato come un valore letterale anziché in modo semplice il significato di espressione regolare. Ad esempio, la seguente sintassi hello ignora un asterisco:`\*`
% | il significato di Hello di un simbolo di percentuale dipende dal relativo utilizzo.<br/><br/> `%{HTTPVariable}`: questa sintassi identifica una variabile HTTP.<br/>`%{HTTPVariable%Pattern}`: Questa sintassi utilizza un tooidentify simbolo di percentuale HTTP variabile e come delimitatore.<br />`\%`: Un simbolo di percentuale di escape consente toobe utilizzato come valore letterale o codifica URL tooindicate (ad esempio, `\%20`).
* | Un asterisco consente hello precedente toobe carattere corrispondenza zero o più volte. 
Spazio | Un carattere di spazio in genere è considerato come un carattere letterale. 
"value" | Le virgolette singole vengono trattate come caratteri letterali. Un set di virgolette singole non ha un significato speciale.


## <a name="next-steps"></a>Passaggi successivi
* [Condizioni di corrispondenza del motore regole](cdn-rules-engine-reference-match-conditions.md)
* [Espressioni condizionali del motore regole](cdn-rules-engine-reference-conditional-expressions.md)
* [Funzionalità del motore regole](cdn-rules-engine-reference-features.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
* [Panoramica della rete CDN di Azure](cdn-overview.md)
