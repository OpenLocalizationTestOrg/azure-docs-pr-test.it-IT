---
title: aaaThreats - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
description: Pagina di categoria di minaccia per lo strumento Microsoft Threat modellazione hello, che contiene le categorie per tutti esposti generato minacce.
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
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Minacce di Microsoft Threat Modeling Tool

Strumento di modellazione delle minacce Hello è un elemento principale di hello Microsoft Security Development Lifecycle (SDL). Consente di software progettisti tooidentify e attenuare i potenziali problemi di sicurezza in anticipo, quando sono tooresolve relativamente semplice e conveniente. Di conseguenza, riduce notevolmente il costo totale di hello di sviluppo. Inoltre, è progettato strumento hello con gli esperti di protezione non presente, semplificando la modellazione delle minacce per tutti gli sviluppatori fornendo indicazioni precise sulla creazione e l'analisi dei modelli di rischio.

> Visitare hello  **[strumento di modellazione delle minacce](./azure-security-threat-modeling-tool.md)**  tooget subito!

Strumento di modellazione delle minacce Hello contribuisce di rispondere a domande specifiche, ad esempio hello quelli indicati di seguito:

* Come un utente malintenzionato può modificare i dati di autenticazione hello?
* Che cos'è l'impatto di hello se un utente malintenzionato può leggere i dati del profilo utente hello?
* Cosa accade se toohello database di profilo utente viene negato l'accesso?

## <a name="stride-model"></a>Modello STRIDE

Guida toobetter formulazione di questi tipi di domande puntare, Microsoft utilizza hello modello STRIDE, che classifica i diversi tipi di minacce e semplifica hello conversazioni sicurezza complessiva.

| Categoria | Descrizione |
| -------- | ----------- |
| **Spoofing** | Implica l'accesso in modo illegale e l'uso delle informazioni di autenticazione di un altro utente, ad esempio nome utente e password |
| **Manomissione** | Implica hello modifica non autorizzata dei dati. Esempi di modifiche non autorizzate toopersistent dati, ad esempio quelle contenute in un database e la modifica dei dati hello mentre passano tra due computer in una rete aperta, ad esempio hello Internet |
| **Ripudio** | Associata a impedire l'esecuzione di un'azione le altre parti non tooprove qualsiasi modo, in caso contrario gli utenti, ad esempio, un utente esegue un'operazione non valida in un sistema che non dispone di operazioni di hello possibilità tootrace hello non consentito. Il non ripudio fa riferimento il possibilità toohello delle minacce di ripudio toocounter sistema. Ad esempio, un utente che acquista un articolo potrebbe essere toosign per elemento hello al momento della ricezione. fornitore Hello potrà quindi utilizzare hello firmato ricevuta come prova che l'utente hello ha ricevuto il pacchetto di hello |
| **Divulgazione di informazioni** | Comporta l'esposizione di hello di tooindividuals informazioni che non dovrebbero toohave tooit di accesso, ad esempio, il possibilità hello di utenti tooread un file che non erano concesso l'accesso a o hello capacità dei dati di tooread intruso in transito tra due computer |
| **Denial of Service** | Attacchi Denial of service (DoS) negare agli utenti di toovalid di servizio, ad esempio, rendendo un server Web temporaneamente non disponibile o inutilizzabile. È necessario proteggersi da determinati tipi di DoS minacce semplicemente tooimprove sistema disponibilità e affidabilità |
| **Elevazione dei privilegi** | Un utente senza privilegi ottenga l'accesso con privilegi e in tal modo è sufficiente accedere toocompromise o distruggere hello intero sistema. Elevazione delle minacce privilegio includere nelle situazioni in cui un utente malintenzionato ha effettivamente attraversate tutte le difese di sistema e diventano parte del sistema hello trusted stesso, effettivamente una situazione pericolosa |

## <a name="next-steps"></a>Passaggi successivi

Procedere troppo**[riduzioni dello strumento di modellazione delle minacce](./azure-security-threat-modeling-tool-mitigations.md)**  diversi modi hello toolearn tali minacce con Azure.
