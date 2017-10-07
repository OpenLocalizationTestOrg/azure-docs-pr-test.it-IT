---
title: la maschera dati dinamica del Database SQL aaaAzure | Documenti Microsoft
description: La maschera dati dinamica del Database SQL limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Maschera dati dinamica del database SQL

La maschera dati dinamica del Database SQL limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon. 

Maschera dati dinamica aiuta a impedire che i dati di accesso non autorizzato toosensitive abilitando i clienti toodesignate la quantità di hello dati sensibili tooreveal con un impatto minimo sul livello di applicazione hello. È una funzionalità basata su criteri di sicurezza che consente di nascondere i dati sensibili hello nel set di risultati hello di una query su campi di database designati, senza dati hello hello database non viene modificati.

Ad esempio, un rappresentante del servizio a un call center può identificare i chiamanti da diverse cifre del loro numero di carta di credito, ma tali dati in cui gli elementi non devono essere completamente esposti toohello rappresentante del servizio. Può definire una regola di maschera che tutte le maschere ma hello ultime quattro cifre di qualsiasi numero di carta di credito nel set di risultati hello delle query. Ad esempio, una maschera dati appropriata può essere definito tooprotect informazioni identificabili personalmente (PII) dati, uno sviluppatore può eseguire query su ambienti di produzione per la risoluzione dei problemi senza violare la regolamentazione di conformità.

## <a name="sql-database-dynamic-data-masking-basics"></a>Nozioni fondamentali sulla funzione Maschera dati dinamica del database SQL
Impostare un criterio di hello di maschera dati dinamica portale di Azure selezionando l'operazione nel Pannello di configurazione Database SQL o nel pannello delle impostazioni di maschera dati dinamica di hello.

### <a name="dynamic-data-masking-permissions"></a>Autorizzazioni per il mascheramento dei dati dinamici
La maschera dati dinamica può essere configurata Database Azure salve, amministratore del server o ruoli di sicurezza responsabile della.

### <a name="dynamic-data-masking-policy"></a>Criteri di mascheramento dei dati dinamici
* **Utenti SQL esclusi dalla maschera** - set di utenti SQL o le identità di Azure ad che ottengono dati senza mascherati in hello SQL risultati della query. Gli utenti con privilegi di amministratore sono sempre esclusi dalla maschera e visualizzare i dati originali di hello senza qualsiasi maschera.
* **Le regole di maschera** -un set di regole che definiscono hello designato toobe campi mascherato e hello funzione che viene usata la maschera. è possibile definire Hello designato campi utilizzando un nome dello schema di database, un nome di tabella e un nome di colonna.
* **Funzioni di maschera** -un set di metodi che consentono di controllare l'esposizione di hello dei dati per scenari diversi.

| Funzione di mascheramento | Logica di mascheramento |
| --- | --- |
| **Default** |**Maschera completa in base toohello dati tipi di hello designato campi**<br/><br/>• Usare XXXX o x minori se dimensioni hello del campo hello sono minore di 4 caratteri per i tipi di dati string (nchar, ntext, nvarchar).<br/>• Usare un valore pari a zero per i tipi di dati numerici (bigint, bit, decimal, int, money, numeric, smallint, smallmoney, tinyint, float, real).<br/>• Usare 01-01-1900 per i tipi di dati data/ora (date, datetime2, datetime, datetimeoffset, smalldatetime, time).<br/>• SQL variant, hello come valore predefinito del tipo corrente hello viene utilizzato.<br/>• Per documento hello XML <masked/> viene utilizzato.<br/>• Usare un valore vuoto per i tipi di dati speciali (timestamp table, hierarchyid, GUID, binary, image, varbinary spatial types). |
| **Carta di credito** |**Metodo di maschera, che espone hello ultime quattro cifre di hello designato campi** e aggiunge una stringa costante come prefisso sotto forma di hello di una carta di credito.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Indirizzo di posta elettronica** |**Metodo di maschera, che espone prima lettera hello e sostituisce il dominio hello con XXX.com** mediante un prefisso stringa costante in forma di hello di un indirizzo di posta elettronica.<br/><br/>aXX@XXXX.com |
| **Numero casuale** |**Metodo di maschera, che genera un numero casuale** in base toohello selezionati i limiti e i tipi di dati effettivi. Se hello designato limiti sono uguale, funzione di maschera hello è un numero costante.<br/><br/>![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Testo personalizzato** |**Metodo, che espone hello prima e ultima caratteri di maschera** e aggiunge una stringa di riempimento personalizzata hello centro. Se la stringa originale hello è minore di suffisso e prefisso hello esposto, viene utilizzato solo hello stringa di riempimento. <br/>prefisso[riempimento]suffisso<br/><br/>![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>I campi obbligatori toomask
Hello motore indicazioni DDM, flag di determinati campi dal database come i campi potrebbero contenere informazioni riservati, che possono essere utili candidati per la maschera. Nel pannello maschera dati dinamica hello nel portale di hello, si noterà hello consigliato colonne per il database. È sufficiente toodo fare clic su **Aggiungi maschera** per una o più colonne e quindi **salvare** tooapply una maschera per questi campi.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Configurare il mascheramento dei dati dinamici per il database usando i cmdlet di PowerShell.
Vedere [Cmdlet del database SQL di Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Configurare il mascheramento dei dati dinamici per il database usando l'API REST
Vedere [Operazioni per i database SQL di Azure](https://msdn.microsoft.com/library/dn505719.aspx).

