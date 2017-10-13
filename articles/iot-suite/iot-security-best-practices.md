---
title: Procedure consigliate per la sicurezza IoT | Documentazione Microsoft
description: Procedure consigliate per la protezione dell'infrastruttura IoT
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 24e7bda2-5f7b-44e3-b8af-761abd3276ff
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: dcab91856bcebb8f3bfab8cc69b63fad487f8ace
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="internet-of-things-security-best-practices"></a>Procedure consigliate per la sicurezza di Internet of Things
Per proteggere un'infrastruttura Internet of Things (IoT) è richiesta una strategia di sicurezza rigorosa e approfondita. Questa strategia richiede la protezione dei dati nel cloud, dell'integrità dei dati in transito sulla rete internet pubblica e il provisioning sicuro dei dispositivi. Ogni livello crea maggiori garanzie di sicurezza dell'infrastruttura complessiva.

## <a name="secure-an-iot-infrastructure"></a>Proteggere un'infrastruttura IoT
Questa strategia di sicurezza può essere sviluppata e implementata con la partecipazione attiva dei vari attori coinvolti nella produzione, nello sviluppo e nella distribuzione di dispositivi e infrastrutture IoT. Di seguito è riportata una descrizione dettagliata degli attori.  

* **Produttore/integratore di hardware IoT**: in genere si tratta dei produttori dell'hardware IoT da distribuire, integratori che si occupano dell'assemblaggio di hardware da produttori diversi, oppure di fornitori per la distribuzione IoT prodotta o integrata da altri fornitori.
* **Sviluppatore di soluzioni IoT**: lo sviluppo di una soluzione IoT viene in genere effettuato da uno sviluppatore di soluzioni. Uno sviluppatore può far parte di un team interno o un integratore di sistemi (SI) specializzato in questa attività. Lo sviluppatore di soluzioni IoT può sviluppare vari componenti della soluzione IoT partendo da zero, integrare vari componenti predefiniti o open source, oppure adottare soluzioni preconfigurate che necessitano di un adattamento minore.
* **Distributore di soluzioni IoT**: una volta sviluppata, la soluzione IoT deve essere distribuita nell'ambiente. Ciò implica la distribuzione dell'hardware, l'interconnessione dei dispositivi e la distribuzione di soluzioni su dispositivi hardware o nel cloud.
* **Operatore di soluzioni IoT**: una volta distribuita, la soluzione IoT richiede operazioni, monitoraggio, aggiornamenti e manutenzione a lungo termine. Questa operazione può essere eseguita da un team interno che comprende esperti di tecnologie informatiche, team per le operazioni hardware e team di manutenzione, nonché specialisti di dominio che monitorano il corretto funzionamento dell'intera infrastruttura IoT.

Le sezioni che seguono descrivono le procedure consigliate per ognuno di questi attori per aiutare a sviluppare, distribuire e gestire un'infrastruttura IoT protetta.

## <a name="iot-hardware-manufacturerintegrator"></a>Produttore/integratore di hardware IoT
Di seguito sono riportate le pratiche ottimali per i produttori di hardware IoT e gli integratori di hardware.

* **Impostare l'hardware sui requisiti minimi**: la progettazione dell'hardware deve includere esclusivamente le funzionalità minime necessarie per il funzionamento. Ad esempio, è possibile includere porte USB solo se necessario al funzionamento del dispositivo. Queste funzionalità aggiuntive espongono il dispositivo a vettori di attacchi indesiderati, che sarebbe opportuno evitare.
* **Realizzare hardware a prova di manomissione**: meccanismi integrati per il rilevamento di manomissioni fisiche, ad esempio l'apertura del coperchio del dispositivo o la rimozione di una parte del dispositivo. Questi segnali di manomissione possono essere inseriti nel flusso dei dati caricati nel cloud, al fine di segnalare tali eventi agli operatori.
* **Creare un hardware sicuro**: se il costo del venduto lo consente, creare funzionalità di sicurezza, ad esempio l'archiviazione protetta e crittografata o la funzionalità di avvio basata sul modulo TPM (Trusted Platform Module). Queste funzionalità rendono i dispositivi più sicuri e aiutano a proteggere l'intera infrastruttura IoT.
* **Implementare aggiornamenti sicuri**: gli aggiornamenti del firmware durante il ciclo di vita del dispositivo non possono essere evitati. La creazione di dispositivi con percorsi protetti per gli aggiornamenti e crittografia protetta delle versioni del firmware consentirà al dispositivo di rimanere protetto durante e dopo gli aggiornamenti.

## <a name="iot-solution-developer"></a>Sviluppatore di soluzioni IoT
Di seguito sono riportate le pratiche ottimali per gli sviluppatori di soluzioni IoT:

* **Applicare una metodologia di sviluppo software protetta**: lo sviluppo di software protetti richiede una riflessione totale riguardo alla sicurezza dall'inizio del progetto fino all'implementazione, al test e alla distribuzione. Le scelte di piattaforme, linguaggi e strumenti è influenzata dalla metodologia. Microsoft Security Development Lifecycle fornisce un approccio dettagliato per la creazione di software protetti.
* **Scegliere software open source con attenzione**: il software open source consente di sviluppare soluzioni in modo rapido. Quando si sceglie il software open source, valutare il livello di attività della community per ogni componente open source. Una community attiva garantisce il supporto del software e la possibilità di rilevare e risolvere i problemi. Al contrario, un software open source incomprensibile e inattivo non verrebbe supportato e i problemi non verranno probabilmente rilevati.
* **Eseguire l'integrazione con attenzione**: molti dei problemi di sicurezza del software intervengono al confine tra librerie e API. Le funzionalità non necessarie per la distribuzione in corso potrebbero essere ancora disponibili tramite un livello di API. Per garantire la sicurezza complessiva, assicurarsi di controllare tutte le interfacce dei componenti integrati per rilevare eventuali difetti di protezione.      

## <a name="iot-solution-deployer"></a>Distributore di soluzioni IoT
Di seguito sono riportate le pratiche ottimali per i distributori di soluzioni IoT:

* **Distribuire l'hardware in modo sicuro**: le distribuzioni IoT potrebbero richiedere che l'hardware da distribuire si trovi in posizioni non protette, ad esempio spazi pubblici o posizioni non controllate. In questi casi, assicurarsi che la distribuzione dell'hardware garantisca la massima protezione dalle manomissioni. Se l'hardware dispone di porte USB o di altro tipo, assicurarsi che questi elementi siano protetti. Molti vettori di attacco possono usarle come punto di ingresso.
* **Proteggere le chiavi di autenticazione**: durante la distribuzione, ogni dispositivo richiede gli ID dei dispositivi e le chiavi di autenticazione associate generate dal servizio cloud. Conservare fisicamente queste chiavi al sicuro anche dopo la distribuzione. Qualsiasi chiave compromessa può essere usata da un dispositivo non autorizzato per passare come dispositivo esistente.

## <a name="iot-solution-operator"></a>Operatore di soluzioni IoT
Di seguito sono riportate le pratiche ottimali per gli operatori di soluzioni IoT:

* **Aggiornare il sistema regolarmente**: assicurarsi che tutti i sistemi operativi e i driver dei dispositivi vengano aggiornati alle versioni più recenti. Se si attiva la funzionalità di aggiornamento automatico su Windows 10 (IoT o altri SKU), Microsoft mantiene il sistema aggiornato, garantendo un sistema operativo protetto per i dispositivi IoT. Mantenere aggiornati gli altri sistemi operativi (ad esempio Linux) aiuta a garantirne la protezione anche dagli attacchi dannosi.
* **Proteggere i sistemi da attività dannose**: se il sistema operativo lo consente, installare le più recenti funzionalità antivirus e anti-malware su ogni sistema operativo del dispositivo. In questo modo è possibile mitigare le minacce più esterne. È possibile proteggere i sistemi operativi più recenti dalle minacce eseguendo i passaggi appropriati.
* **Effettuare controlli regolari**: controllare la presenza di problemi di sicurezza all'infrastruttura IoT è un fattore chiave durante la risposta agli incidenti di sicurezza. La maggior parte dei sistemi operativi offre la registrazione integrata degli eventi che è opportuno esaminare frequentemente per assicurarsi che non si verifichino violazioni della protezione. Le informazioni di controllo possono essere inviate come flusso dati di telemetria separati al servizio cloud per l'analisi.
* **Proteggere fisicamente l'infrastruttura IoT**: gli attacchi più dannosi per la sicurezza dell'infrastruttura IoT vengono lanciati tramite l'accesso fisico ai dispositivi. Un'importante procedura di sicurezza è la protezione contro l'uso non autorizzato di porte USB e altri accessi fisici. Un'operazione fondamentale per rilevare eventuali violazioni è la registrazione degli accessi fisici, come l'uso delle porte USB. Anche in questo caso, Windows 10 (IoT e altri SKU) offre la registrazione dettagliata di questi eventi.
* **Proteggere le credenziali del cloud**: le credenziali per l'autenticazione nel cloud usate per la configurazione e il funzionamento di una distribuzione IoT costituiscono probabilmente il modo più semplice per accedere e compromettere un sistema IoT. Proteggere le credenziali modificando frequentemente la password ed evitare di usarle sui computer pubblici.

Le capacità dei vari dispositivi IoT variano. Alcuni dispositivi potrebbero essere computer dotati di sistemi operativi desktop tradizionali, mentre altri dispositivi potrebbero disporre di sistemi operativi molto leggeri. Le migliori pratiche per la protezione descritte in precedenza possono essere applicate a questi dispositivi in modo diverso. Se specificato, è necessario attenersi alle procedure aggiuntive per la sicurezza e la distribuzione fornite dai produttori dei dispositivi.

Alcuni dispositivi legacy e limitati potrebbero non essere stati progettati in modo specifico per la distribuzione IoT. Questi dispositivi potrebbero non essere in grado di crittografare i dati, stabilire connessioni a Internet, o fornire un controllo avanzato. In questi casi, l'uso di un gateway moderno e sicuro sul campo può aggregare i dati dai dispositivi legacy al fine di garantire la protezione necessaria per la connessione di questi dispositivi a Internet. I gateway sul campo offrono l'autenticazione protetta, la negoziazione per le sessioni crittografate, la ricezione di comandi dal cloud e molte altre funzionalità di sicurezza.

## <a name="see-also"></a>Vedere anche
Per altre informazioni sulla protezione della soluzione IoT, vedere:

* [Architettura della sicurezza IoT][lnk-security-architecture]
* [Proteggere la distribuzione di IoT][lnk-security-deployment]

È anche possibile esplorare alcune altre funzionalità delle soluzioni preconfigurate di IoT Suite:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su Azure IoT Suite][lnk-faq]

Informazioni sulla protezione dell'hub IoT sono disponibili in [Controllare l'accesso all'hub IoT][lnk-devguide-security] nella guida per gli sviluppatori dell'hub IoT.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
