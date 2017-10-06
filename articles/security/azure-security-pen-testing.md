---
title: aaaPen test | Documenti Microsoft
description: articolo Hello viene fornita una panoramica del processo (pentest) di test di penetrazione di hello e come eseguire pentest contro le App in esecuzione nell'infrastruttura di Azure.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Test di penetrazione
Uno dei vantaggi hello sull'utilizzo di Microsoft Azure per la distribuzione e test dell'applicazione è che non è necessario tooput insieme un toodevelop infrastruttura on-premise, testare e distribuire le applicazioni. Tutta l'infrastruttura hello viene preso in considerazione dai servizi della piattaforma Microsoft Azure hello. Non è tooworry su richiesta approvvigionamento, l'acquisizione e "su rack e sovrapposizione" proprio hardware locale.

Questo è molto utile, ma è comunque necessario toomake che si esegue la normale protezione diligente. Una delle operazioni di hello è necessario toodo è nelle applicazioni hello test di penetrazione distribuiti in Azure.

Forse si è già a conoscenza del fatto che Microsoft esegue [il test di penetrazione dell'ambiente di Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e), che consente di ottimizzare la piattaforma e di determinare le azioni mirate a migliorare i controlli di sicurezza, introdurre nuovi controlli di sicurezza e perfezionare i processi di sicurezza.

È non penna testare l'applicazione, ma è comprendere che verrà che desideri tooperform penna test sulle proprie applicazioni. È utile perché quando è migliorare la sicurezza hello delle applicazioni, consente di rendere più sicura ecosistema Azure intera hello.

Quando si penna testano le applicazioni, può sembrare un attacco toous. I modelli di attacco vengono [continuamente monitorati](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) e, se necessario, verrà avviato un processo di risposta agli eventi imprevisti, Non consente di e non consente di ci se è attiva una risposta agli eventi imprevisti scadenza tooyour proprio a causa di test penna molta attenzione.

Quali toodo?

Quando si è pronti toopen testare le applicazioni ospitate da Azure, è disponibile un'opzione troppo[segnalarlo](https://portal.msrc.microsoft.com/en-us/engage/pentest). Una volta che si sa che si userà toobe l'esecuzione di test specifico, viene inavvertitamente non è stato chiuso (ad esempio indirizzo IP hello che si sta testando da), purché i test conformi toohello Azure penna termini e le condizioni descritte in test[Cloud Microsoft Unified penetrazione regole di comportamento](https://technet.microsoft.com/en-us/mt784683).
I test standard che è possibile eseguire includono:

* I test eseguiti sul hello toouncover endpoint [aprire Web applicazione sicurezza progetto (OWASP) le prime 10 vulnerabilità](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Test con dati casuali](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) degli endpoint
* [Port scanning](https://en.wikipedia.org/wiki/Port_scanner) degli endpoint

Tra i tipi di test che non è possibile eseguire sono incluse tutte le tipologie di attacco [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack), tra cui l'avvio di un attacco DoS vero e proprio o l'esecuzione di test correlati che possono determinare, dimostrare o simulare tutti i tipi di attacco DoS.

Si che pronti tooget introduttiva penna test le applicazioni ospitate in Microsoft Azure? Se in tal caso, head su toohello [Cenni preliminari sul Test di penetrazione](https://technet.microsoft.com/library/mt784683.aspx) pagina (e fare clic su Crea un pulsante di richiesta di test nella parte inferiore di hello della pagina hello hello. Sono inoltre disponibili ulteriori informazioni sulla penna hello test termini e condizioni e collegamenti utili su come è possibile segnalare tooAzure correlati difetti di sicurezza o altri servizi Microsoft.
