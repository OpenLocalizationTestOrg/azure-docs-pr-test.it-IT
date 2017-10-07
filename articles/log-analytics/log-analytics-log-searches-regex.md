---
title: espressioni aaaRegular in OMS Log Analitica log ricerche | Documenti Microsoft
description: "È possibile utilizzare una parola chiave RegEx hello nei Log Analitica log ricerche toohello hello risultati filtro in base a espressioni regolari tooa.  In questo articolo fornisce sintassi hello per le espressioni con alcuni esempi."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Utilizza toofilter di espressioni regolari consente di cercare di log nel Log Analitica

[Log delle ricerche](log-analytics-log-searches.md) consentono tooextract informazioni dal repository di hello Analitica di Log.  [Espressioni di filtro](log-analytics-search-reference.md#filter-expressions) consentono risultati hello toofilter della ricerca hello in base a criteri toospecific.  Hello **RegEx** la parola chiave consente toospecify un'espressione regolare per il filtro.  

In questo articolo vengono fornite informazioni dettagliate sulla sintassi di espressione regolare hello utilizzata dal Log Analitica.

> [!NOTE]
> È possibile usare solo RegEx con i campi ricercabili.  Per altre informazioni sui campi ricercabili, vedere **Tipi di campo** in [Trovare dati con ricerche nei log in Log Analytics](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Parola chiave RegEx

Hello utilizzare seguente hello toouse sintassi **RegEx** parola chiave in una ricerca di log.  È possibile utilizzare hello altre sezioni incluse in questa sintassi di hello toodetermine articolo di espressione regolare di hello stesso.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Ad esempio, un avviso di espressione regolare tooreturn toouse registra con un tipo di *avviso* o *errore*, si utilizzerebbe hello ricerca nei log seguente.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Corrispondenze parziali
Si noti che l'espressione regolare hello deve corrispondere testo intero hello della proprietà hello.  Le corrispondenze parziali non restituiranno alcun record.  Ad esempio, se si sta tentando di tooreturn record da un computer denominato srv01.contoso.com, hello ricerca nei log seguente sarà **non** restituito alcun record.

    Computer=RegEx("srv..")

Questo avviene perché solo hello prima parte del nome hello corrispondente espressione regolare di hello.  Hello ricerche nei log due seguenti restituisce i record da questo computer perché corrispondano nome intero hello.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Caratteri
Specificare caratteri diversi.

| Character | Descrizione | Esempio | Corrispondenze di esempio |
|:--|:--|:--|:--|
| a | Un'occorrenza del carattere hello. | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| . | Qualsiasi carattere singolo. | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Zero o una occorrenza del carattere hello. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Zero o più occorrenze del carattere hello. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Una o più occorrenze del carattere hello. | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Corrisponde a qualsiasi carattere singolo tra parentesi quadre hello | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Corrisponde a un carattere singolo nell'intervallo di hello.  Può includere più intervalli. | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Nessuno dei caratteri di hello tra parentesi quadre hello | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Nessuno dei caratteri hello nell'intervallo di hello. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Corrispondenza di un intervallo di caratteri numerici. | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | Qualsiasi stringa di caratteri. | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Più occorrenze del carattere
Specificare più occorrenze di un carattere specifico.

| Character | Descrizione | Esempio | Corrispondenze di esempio |
|:--|:--|:--|:--|
| a{n} |  *n*occorrenze del carattere hello. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*o più occorrenze del carattere hello. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*troppo*m* le occorrenze del carattere hello. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Espressioni logiche
Selezionare più valori.

| Character | Descrizione | Esempio | Corrispondenze di esempio |
|:--|:--|:--|:--|
| &#124; | OR logico.  Restituisce un risultato se corrisponde a una delle espressioni. | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | Avviso<br>Errore |
| & | AND logico.  Restituisce un risultato se corrisponde a entrambe le espressioni | EventData=regex("(Security.\*&.\*success.\*)") | Controllo della sicurezza eseguito correttamente |


## <a name="literals"></a>Valori letterali
Convertire i caratteri speciali tooliteral caratteri.  Sono inclusi i caratteri che offrono funzionalità quali espressioni tooregular?-\*^\[\]{}\(\)+\|. &.

| Character | Descrizione | Esempio | Corrispondenze di esempio |
|:--|:--|:--|:--|
| \\ | Converte un valore letterale di tooa carattere speciale. | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [Error]File non trovato.<br>Errore-File non trovato. |


## <a name="next-steps"></a>Passaggi successivi

* Acquisire familiarità con [log ricerche](log-analytics-log-searches.md) tooview e analizzare i dati nel repository di hello Analitica di Log.
