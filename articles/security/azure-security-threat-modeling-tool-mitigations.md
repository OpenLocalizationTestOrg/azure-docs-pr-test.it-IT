---
title: aaaMitigations - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
description: "Pagina le misure di attenuazione per hello dello strumento Microsoft Threat modellazione evidenziazione possibili soluzioni toohello più esposta generato minacce."
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Mitigazioni di Microsoft Threat Modeling Tool

Strumento di modellazione delle minacce Hello è un elemento principale di hello Microsoft Security Development Lifecycle (SDL). Consente di software progettisti tooidentify e attenuare i potenziali problemi di sicurezza in anticipo, quando sono tooresolve relativamente semplice e conveniente. Di conseguenza, riduce notevolmente il costo totale di hello di sviluppo. Inoltre, è progettato strumento hello con gli esperti di protezione non presente, semplificando la modellazione delle minacce per tutti gli sviluppatori fornendo indicazioni precise sulla creazione e l'analisi dei modelli di rischio.

Visitare hello  **[strumento di modellazione delle minacce](./azure-security-threat-modeling-tool.md)**  tooget subito!

## <a name="mitigation-categories"></a>Categorie di mitigazione

le misure di attenuazione strumento di modellazione delle minacce Hello sono suddivisi in base toohello Frame di sicurezza dell'applicazione Web, costituito dai seguenti hello:

| Categoria | Descrizione |
| -------- | ----------- |
| **[Controllo e registrazione](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Chi ha fatto cosa e quando? Il controllo e registrazione, vedere toohow l'applicazione registra gli eventi di sicurezza |
| **[Autenticazione](./azure-security-threat-modeling-tool-authentication.md)** | Chi si sta autenticando? L'autenticazione è il processo di hello in cui un'entità verifica identità hello di un'altra entità, in genere tramite le credenziali, ad esempio un nome utente e password |
| **[Autorizzazione](./azure-security-threat-modeling-tool-authorization.md)** | Cosa fare L'autorizzazione è il modo in cui l'applicazione fornisce controlli sull'accesso per risorse e operazioni |
| **[Sicurezza delle comunicazioni](./azure-security-threat-modeling-tool-communication-security.md)** | Con si sta parlando? La protezione delle comunicazioni garantisce che tutte le comunicazioni siano eseguite nel modo più sicuro possibile |
| **[Gestione della configurazione](./azure-security-threat-modeling-tool-configuration-management.md)** | A nome di chi è eseguita l'applicazione? A quale database si connette? Come viene amministrata l'applicazione? Come vengono protette queste impostazioni? Gestione della configurazione fa riferimento toohow l'applicazione gestisce questi problemi operativi |
| **[Crittografia](./azure-security-threat-modeling-tool-cryptography.md)** | Come si mantengono i segreti (la riservatezza)? Come si mettono a prova di manomissione i dati o le librerie (integrità)? Come vengono creati i valori di inizializzazione casuali che devono essere crittograficamente sicuri? Crittografia si intende toohow l'applicazione impone la riservatezza e integrità |
| **[Gestione delle eccezioni](./azure-security-threat-modeling-tool-exception-management.md)** | Quando una chiamata del metodo nell'applicazione ha esito negativo, che cosa fa l'applicazione? Quanto viene rivelato? Si restituiscono errore brevi informazioni tooend gli utenti? Si passa chiamante toohello indietro di eccezione importanti informazioni? L'applicazione ha esito negativo correttamente? |
| **[Convalida dell'input](./azure-security-threat-modeling-tool-input-validation.md)** | Come si capisce che l'applicazione riceve input di hello è valido e sicuro? Convalida dell'input fa riferimento toohow l'applicazione filtra, Annulla o rifiuta di input prima di un'ulteriore elaborazione. Considerare la limitazione dell'input tramite punti di ingresso e la codifica dell'output tramite punti di uscita. Ci si fida dei dati dalle fonti come i database e la condivisione di file? |
| **[Dati sensibili](./azure-security-threat-modeling-tool-sensitive-data.md)** | In che modo l'applicazione gestisce dati sensibili? I dati sensibili fa riferimento l'applicazione gestisce i dati che devono essere protetti in memoria, rete hello o negli archivi permanenti toohow |
| **[Gestione delle sessioni](./azure-security-threat-modeling-tool-session-management.md)** | In che modo l'applicazione gestisce e protegge le sessioni utente? Una sessione si riferisce tooa serie di interazioni correlate tra un utente e l'applicazione Web |

Ciò consente di identificare:

* Dove è hello errori più comuni
* Dove è hello miglioramenti più utilizzabili

Di conseguenza, utilizzare toofocus queste categorie e classificare il lavoro di protezione, in modo che se si conoscono i problemi di sicurezza più prevalenti hello si verificano nelle categorie di autorizzazione, autenticazione e la convalida inpue hello, è possibile partire da qui. Per altre informazioni, visitare **[questo collegamento al brevetto](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Passaggi successivi

Visitare  **[minacce dello strumento di modellazione minaccia](./azure-security-threat-modeling-tool-threats.md)**  toolearn ulteriori informazioni sugli hello minaccia strumento hello categorie utilizza toogenerate minacce di progettazione.
