---
title: aaaInternet di procedure consigliate di sicurezza operazioni | Documenti Microsoft
description: articolo Hello fornisce un elenco curato di Microsoft Internet delle cose Security Best Practices e i suggerimenti generali.
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Procedure consigliate per la sicurezza di Internet delle cose
Protezione dell'infrastruttura di Internet delle cose (IoT) hello è un'impresa critica per tutti i membri con soluzioni di IoT. A causa di hello e numero di hello di dispositivi coinvolti natura distribuita di questi dispositivi, impatto hello un evento di sicurezza correlati toocompromise di milioni di dispositivi IoT non è semplice e può avere un impatto esteso.

Per questo motivo, la sicurezza IoT richiede un approccio approfondito. Dati esigenze toobe sicuro nel cloud hello e si sposta su reti pubbliche e private. È necessario toobe in luogo toosecurely provisioning hello IoT dispositivi stessi metodi. Ogni livello, dal dispositivo, toonetwork, toocloud back-end deve garanzie di sicurezza sicuro.

Procedure consigliate di IoT possono essere suddivise in hello seguente modo:

* Produttore o integratore di hardware IoT
* Sviluppatore di soluzioni IoT
* Distributore di soluzioni IoT
* Operatore di soluzioni IoT

Questo articolo riepiloga le [procedure consigliate per la sicurezza di Internet delle cose](../iot-suite/iot-security-best-practices.md). Per informazioni più dettagliate, vedere l'articolo toothat.

## <a name="iot-hardware-manufacturer-or-integrator"></a>Produttore o integratore di hardware IoT
Se si è un produttore dell'hardware IoT o un integratore di hardware, seguire hello le procedure consigliate seguenti:

* **Ambito i requisiti hardware toominimum**: progettazione hardware hello deve includere le funzionalità minime necessarie per l'operazione di hardware hello e nient'altro. 
* **Rendere hardware manomissione**: compilare in meccanismi toodetect fisico manomissione di hardware, ad esempio l'apertura di una copertura hello dispositivo, la rimozione di una parte del dispositivo hello e così via. 
* **Creare un hardware sicuro**: se il [costo del venduto](https://en.wikipedia.org/wiki/Cost_of_goods_sold) lo consente, creare funzionalità di sicurezza, ad esempio l'archiviazione protetta e crittografata e la funzionalità di avvio basata sul modulo TPM (Trusted Platform Module).
* **Proteggere gli aggiornamenti**: l'aggiornamento del firmware nel corso della durata del dispositivo hello è inevitabile.

## <a name="iot-solution-developer"></a>Sviluppatore di soluzioni IoT
Se uno sviluppatore di soluzioni IoT, seguire hello le procedure consigliate seguenti:

* **Seguire la metodologia di sviluppo software protetto**: sviluppo di software protetto richiede interamente progettato pensando di sicurezza dall'inizio di hello del progetto hello implementazione tooits modo di hello, test e distribuzione.
* **Scegliere software open source con cautela**: software open source offre l'opportunità tooquickly lo sviluppo di soluzioni.
* **Integrazione con cautela**: molti dei problemi di protezione software hello esiste confine hello di librerie e API. 

## <a name="iot-solution-deployer"></a>Distributore di soluzioni IoT
In caso di un distributore soluzione IoT, seguire hello le procedure consigliate seguenti:

* **Distribuzione protetta hardware**: le distribuzioni di IoT possono richiedere hardware toobe distribuite nei percorsi non sicuri, ad esempio spazi pubblici o non supervisionato le impostazioni locali.
* **Proteggere le chiavi di autenticazione**: durante la distribuzione, ogni dispositivo richiede l'ID dispositivo e chiavi di autenticazione generate dal servizio cloud hello associata. Conservare queste chiavi fisicamente sicuro anche dopo la distribuzione di hello. Un tasto qualsiasi compromesso è utilizzabile da un toomasquerade dispositivo dannoso come un dispositivo esistente.

## <a name="iot-solution-operator"></a>Operatore di soluzioni IoT
Se si è un operatore di soluzione IoT, seguire hello le procedure consigliate seguenti:

* **Mantenere i sistemi di toodate**: assicurarsi di sistemi operativi dei dispositivi e tutti i driver di dispositivo sono versioni più recenti toohello aggiornato. 
* **Proteggersi da attività dannose**: se consentito dal sistema operativo hello, inserire funzionalità antivirus e anti-malware più recenti hello in ogni sistema operativo del dispositivo. 
* **Controllare spesso**: IoT infrastruttura di controllo per problemi è chiave quando si risponde a eventi imprevisti toosecurity relativi alla protezione.
* **Proteggere fisicamente infrastruttura IoT hello**: hello attacchi alla protezione contro IoT infrastruttura vengono avviati con accesso fisico toodevices peggiore.
* **Proteggere le credenziali di cloud**: le credenziali di autenticazione cloud utilizzate per la configurazione e il funzionamento di una distribuzione IoT sono probabilmente accesso toogain modo più semplice di hello e compromettere un sistema IoT. 

