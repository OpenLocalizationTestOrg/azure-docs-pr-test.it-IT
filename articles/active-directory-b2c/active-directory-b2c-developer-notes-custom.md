---
title: 'Azure Active Directory B2C: note per gli sviluppatori sull''uso dei criteri personalizzati | Microsoft Docs'
description: Note per gli sviluppatori sulla configurazione e la gestione di Azure AD B2C con criteri personalizzati
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Note sulla versione di anteprima pubblica dei criteri personalizzati di Azure Active Directory B2C
Hello criterio personalizzato per il set di funzionalità è ora disponibile per la valutazione in un'anteprima pubblica di Azure tutti, B2C Active Directory (Azure AD B2C) clienti. Questo set di funzionalità è rivolto agli sviluppatori di identità avanzate la creazione di soluzioni di identità più complesse hello.  

Oggi per questo set di funzionalità necessari agli sviluppatori tooconfigure hello identità esperienza Framework direttamente tramite la modifica di file XML. Si tratta di un metodo di configurazione avanzato e complesso. Agli sviluppatori di identità usando hello avanzati identità esperienza Framework consigliabile tooinvest del tempo di completamento delle procedure e la lettura dei documenti di riferimento. 

## <a name="features-included-in-this-public-preview"></a>Funzionalità incluse nell'anteprima pubblica
Con hello nuove funzionalità introdotte in anteprima pubblica di hello, gli sviluppatori possono eseguire hello seguenti attività:<br>

* Creare e caricare percorsi utente di autenticazione personalizzati usando criteri personalizzati. 
   * Descrivere in modo dettagliato i percorsi utente come scambi tra provider di attestazioni. 
   * Definire la diramazione condizionale nei percorsi utente. 
* Integrare servizi abilitati per API REST nei percorsi utente di autenticazione personalizzati.  
* Aggiungere la federazione con provider di identità che sono conformi a hello OpenIDConnect standard. <br>
* Aggiungere la federazione con provider di identità che rispettano protocollo toohello SAML 2.0. 

## <a name="terms-of-hello-public-preview"></a>Condizioni per l'anteprima pubblica di hello

* Si consiglia di nuove funzionalità hello toouse solo a fini di valutazione.<br>
* Le nuove funzionalità non sono destinate all'uso in un ambiente di produzione.<br>
* Contratti di servizio (SLA) si applicano toohello nuove funzionalità. <br>
* È possibile inviare richieste di supporto tramite i normali canali del supporto. <br>
* Non è stata fissata una data per la disponibilità generale.<br>
* Discrezione e per qualsiasi motivo, Microsoft può flag e rifiutare o limitare gli scenari e i percorsi di utente che superano l'ambito di hello di hello Azure Active Directory B2C prodotto fondatore tooserve come una piattaforma di gestione (CIAM) cliente identità e accessi.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Responsabilità degli sviluppatori che usano il set di funzionalità dei criteri personalizzati
Configurazione manuale dei criteri concede l'accesso di livello inferiore toohello sottostante piattaforma di Azure Active Directory B2C e comporta hello creazione di un framework di trust completamente personalizzabile univoco. Le combinazioni possibili di provider di identità personalizzati, le relazioni di trust, integrazioni con servizi esterni e i flussi di lavoro dettagliate inserire le richieste di maggiore su hello avanzate gli sviluppatori che li usano.

toofully vantaggio dalla versione di anteprima pubblica hello, è consigliabile che gli sviluppatori che usano set di funzionalità di criteri personalizzata hello osservate toohello alle linee guida:
* Acquisire familiarità con il linguaggio di configurazione hello di hello del motore di analisi di identità e la gestione di chiave/i segreti.
* Assumere la proprietà degli scenari e delle integrazioni personalizzate.
* Eseguire test metodici degli scenari.
* Seguire le procedure consigliate di staging e sviluppo software con almeno un ambiente di sviluppo e testing e un ambiente di produzione.
* Essere informati sugli ultimi sviluppi dal provider di identità hello e si integra con servizi. Ad esempio, tenere traccia delle modifiche nei segreti e del servizio toohello pianificati e le modifiche.
* Impostare il monitoraggio attivo e monitorare i tempi di risposta hello degli ambienti di produzione.
* Mantenere aggiornati gli indirizzi di posta elettronica di contatto e rimanere messaggi di posta elettronica sito live team Microsoft toohello reattiva.
* Intervento tempestivo quando toodo consigliato in modo che una hello team live-sito Microsoft. 


>[!NOTE]
>Queste funzionalità potrebbero essere incluso in criteri predefiniti di Azure AD, rendendoli più accessibile agli sviluppatori di tooall.

## <a name="next-steps"></a>Passaggi successivi
[Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md)
