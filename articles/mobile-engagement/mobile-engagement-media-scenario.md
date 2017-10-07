---
title: implementazione di Mobile Engagement aaaAzure per un'App multimediale
description: Supporto app scenario tooimplement Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Implementare Mobile Engagement con app multimediali
## <a name="overview"></a>Overview
Mattia è un project manager impegnato in progetti per dispositivi mobili per una grande società di servizi multimediali. Ha recentemente lanciato una nuova app che sta registrando un numero molto elevato di download. Ha raggiunto i suoi obiettivi di download, ma il ritorno sugli investimenti (ROI) per utente non soddisfa ancora i requisiti stabiliti. 

Mattia ha già scoperto perché il ritorno sugli investimenti è troppo basso. Molti degli utenti smettono di usare la sua app dopo sole due settimane e la maggior parte di essi non riprende più a usarla. Conservazione di hello tooincrease del suo app desidera.

Dopo alcuni test iniziale, che ha appreso esercizio quando gli utenti con le notifiche push sono in genere toocontinue utilizzando il suo app. Anche gli utenti che erano inattivi spesso restituirà app toohello a seconda che li invia notifiche. Giorgio decide tooinvest in un tipo di programma di Engagement per le app che utilizza destinazioni avanzate alle notifiche push.

Giorgio ha letto recentemente hello [Azure Mobile Engagement - Guida introduttiva alle procedure consigliate](mobile-engagement-getting-started-best-practices.md) e ha deciso di indicazioni hello tooimplement dalla Guida hello.

## <a name="objectives-and-kpis"></a>Obiettivi e indicatori KPI
Le principali parti interessate si incontrano per discutere dell'app di Mattia. Il fatturato è generato dagli annunci pubblicitari visualizzati dagli utenti durante l'uso dei contenuti multimediali. Aumentando l'uso di contenuti per utente, Mattia potrà aumentare i ricavi. Tutti concordano un obiettivo principale: vendite tooincrease annunci del 25%. Vengono creati unità e toomeasure Business indicatori di prestazioni chiave (KPI), questo obiettivo

* Numero di annunci scelti per utente
* Numero di pagine di articoli visitate (per utente, per sessione, alla settimana, al mese)
* Categorie preferite

Sulla base della riunione tenuta con le principali parti interessate, Mattia ha definito i suoi KPI aziendali. Parte 1 di hello segue [Azure Mobile Engagement - Guida introduttiva alle procedure consigliate](mobile-engagement-getting-started-best-practices.md). 

Successivamente, Davide crea hello tooensure indicatori KPI di coinvolgimento che si raggiungono gli obiettivi seguenti:

* Monitorare memorizzazione attraverso hello seguenti intervalli: giornaliera, settimanale, quindicinale e mensili.
* Conteggio degli utenti attivi
* classificazione app Hello in app hello archivia

In base alle raccomandazioni del team IT hello, hello seguenti tecniche gli indicatori KPI sono state aggiunte hello tooanswer seguenti domande:

* Percorso utente (pagina visitata e tempo dedicato alla pagina dall'utente)
* Numero di arresti anomali o bug rilevati per sessione
* Versione del sistema operativo degli utenti
* Che cos'è di dimensioni medie di hello dello schermo per gli utenti?
* Tipo di connessione Internet degli utenti

Per ogni indicatore KPI, egli classifica dati hello necessari e quindi Registra nella posizione corretta di hello del suo playbook.

## <a name="engagement-program-and-integration"></a>Programma di engagement e integrazione
Dopo aver definito gli indicatori KPI, Mattia inizia la fase della strategia di engagement stabilendo quattro programmi di engagement e i relativi obiettivi: ![][1]

Mattia crea notifiche push dettagliate per ogni programma. Le notifiche push sono definite da cinque elementi:

1. Obiettivo: che cos'è l'obiettivo di hello della notifica hello
2. Come verrà raggiunto obiettivo hello
3. Destinazione: gli utenti che riceveranno la notifica hello?
4. Il contenuto: Che cos'è il testo hello e il formato di hello della notifica hello (In App/Out di App)
5. Quando: che cos'è hello toosend momento migliore questa notifica push
   
    ![][2]

Per ulteriori informazioni consultare toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

In base toohello parte 2 di hello white paper che Giorgio utilizza destinazione sezione toodefine quali dati ha toocollect e scrive il Tag pianificare insieme con una soluzione di hello tooimplement team IT. Dopo una settimana di implementazione e test di accettazione utente, Mattia è finalmente pronto per lanciare i suoi programmi.

## <a name="program-results"></a>Risultati del programma
Quattro mesi dopo, Mattia verifica le prestazioni dei programmi. Programma iniziale Hello e settimanale programma hello sono gli obiettivi il suo. Consente di ridurre il numero di Hello dell'utente con una sola sessione, vengono utilizzate più funzionalità dell'applicazione hello e numero hello di connessioni per ogni settimana è raddoppiato.

Hello **programma inattivo** aiuta Giorgio comprensione delle tendenze di utente. Sembra che il 15% di utenti inattivi hello tornare toohello app. La maggior parte di essi, tuttavia, non rimane attiva per più di un mese. Mattia pensa di poter ottimizzare ulteriormente questa sequenza aggiungendo altre notifiche ed espandendo la scelta di contenuti.

Hello **individuare programma** non funziona correttamente. Aumenta tra vendite, ma non è sufficiente tooreach il suo obiettivi. Giorgio identifica che ha non dispone di sufficienti dati toomake rilevanti targeting e proporre contenuto appropriato. Elimina questo programma e si concentra sull'invio di "notifiche push editoriali" con Azure Mobile Engagement. Il suo giornalisti dispone già di notifiche push toosend soluzione CMS e che non vogliono toochange.

Giorgio decide toouse hello API Reach che è un'API REST HTTP che consente la gestione delle campagne di copertura senza interfaccia Web AZME toouse. Con questo approccio Giorgio possibile raccogliere dati di hello egli deve e consentire il suo writer tookeep utilizzando una soluzione CMS hello.

tooensure che funziona correttamente, John chiede toobe team IT prestare attenzione in hello seguenti punti:

1. **Sistemi operativi** : tutti hanno le proprie regole tooadministrate le notifiche push, John decide toolist tutti i controlli e casi se hello API gestirla.
   Ad esempio: Sistema Android push consente un quadro generale che non è il caso hello con iOS.
2. **Intervallo di tempo**: John richiede un'API, il quale impostare l'intervallo di tempo hello e impostare un toocampaigns di fine. Desidera che gli utenti toopreserve da qualsiasi notifica di arresto improvviso saturazione.
3. **Categorie**: il team di marketing prepara un modello per ogni tipo di avviso. John richiede le categorie di tooset team IT all'interno di hello API.

Dopo alcuni test, Mattia si ritiene soddisfatto. API toothis grazie, giornalisti possono comunque inviare notifiche push con loro CMS e Azure Mobile Engagement raccoglie tutti i dati di comportamento per tali

Dopo questi primi quattro mesi, i risultati riflettono buone prestazioni generali e rassicurano Mattia e il consiglio di amministrazione, il ROI per utente è aumentato del 15% e le vendite da dispositivi mobili rappresentano il 17,5% delle vendite totali. Un aumento del 7,5% in soli quattro mesi.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
