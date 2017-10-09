---
title: scenari comuni di catalogo dati aaaAzure | Documenti Microsoft
description: Panoramica degli scenari comuni per Azure Data Catalog, tra cui registrazione hello e individuazione delle origini dati di alto valore, l'abilitazione di business intelligence self-service e conoscenze sulle origini dati e i processi di acquisizione.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Scenari comuni del Catalogo dati di Azure
In questo articolo vengono presentati scenari comuni in cui Azure Data Catalog può aiutare l'organizzazione a incrementare il valore delle origini dati esistenti.

## <a name="scenario-1-registration-of-central-data-sources"></a>Scenario 1: Registrazione delle origini dati centrali
Le organizzazioni hanno spesso molte origini dati di valore elevato. Queste origini dati includono sistemi di elaborazione di transazioni online (OLTP) line-of-business, data warehouse e database di business intelligence/analisi. diversi sistemi, Hello e hello sovrapposizione tra di essi, in genere aumenta nel tempo con l'evolversi delle esigenze e con l'evolversi tramite, ad esempio, fusioni e acquisizioni azienda hello stesso.

Può essere difficile per tooknow i membri dell'organizzazione in cui toolocate hello dati all'interno di queste origini dati. Domande seguente hello sono tutti troppo comune:

* Di hello HR tre sistemi usati all'interno di azienda hello, che è necessario utilizzare toocreate questo tipo di report?
* In cui è necessario passare tooget hello Certificate cifre relative alle vendite per anno fiscale hello appena interrotta?
* Che è necessario chiedere o Qual è il processo di hello consigliabile utilizzare tooget accesso toohello data warehouse?
* Se non si è certi che i numeri siano corretti, Che è possibile fare per ottenere informazioni su questi dati vengano presunto toobe utilizzata prima di condividere questo dashboard con il proprio team?

toothese e altre domande, Azure Data Catalog possono fornire risposte. Hello centrale, valore elevato, le origini dati gestita dal reparto IT che vengono usate tra le organizzazioni sono spesso hello logico punto di partenza per il popolamento del catalogo hello. Anche se tutti gli utenti possono registrare un'origine dati, con catalogo hello kick-started con origini dati hello che probabilmente tooprovide valore toohello più grande numero di utenti consente di guidare l'adozione e l'utilizzo del sistema hello. 

Se si inizia con Azure Data Catalog, l'identificazione e la registrazione delle origini di dati della chiave utilizzati per molti team di consumer di dati può essere il primo toosuccess passaggio.

Questo scenario presenta anche un toomake di origini dati di valore elevato di opportunità tooannotate hello li toounderstand più semplice e l'accesso. Un aspetto fondamentale di questa attività è tooinclude informazioni su come gli utenti possono richiedere l'origine dati di access toohello. Con Azure Data Catalog, è possibile fornire l'indirizzo di posta elettronica hello di utente hello team responsabile del controllo dell'accesso all'origine di dati, strumenti tooexisting collegamenti o documentazione o testo libero che descrive il processo di richiesta di accesso hello. Queste informazioni consente di membri che individuare le origini dati registrati ma che non dispongono ancora di autorizzazioni tooaccess hello dati tooeasily richiedere l'accesso tramite processi hello definiti e controllati dai proprietari di hello origine dati.

## <a name="scenario-2-self-service-business-intelligence"></a>Scenario 2: Business intelligence in modalità self-service
Anche se le tradizionali soluzioni di business intelligence aziendale continuare toobe paesaggi parte dei dati di molte organizzazioni, hello modifica in base alla velocità di business ha reso più importante di Business Intelligence self-service. Usando la BI in modalità self-service, gli information worker e gli analisti possono creare report, cartelle di lavoro e dashboard senza basarsi su un team IT centrale oppure senza limitazioni di pianificazione e disponibilità del team IT.

In scenari di business intelligence in modalità self-service gli utenti normalmente combinano dati da più origini, molte delle quali potrebbero non essere ancora state usate per analisi e business intelligence. Anche se alcune di queste origini dati potrebbero essere già note, può essere difficile toodiscover quali toolocate toodo e valutare i potenziali origini dati per una determinata attività.

In genere, questo processo di individuazione è manuale: analyst utilizzano loro tooidentify connessioni di rete peer con altri utenti che utilizzano dati hello cercati. Dopo che un'origine dati è stata trovata e utilizzata, hello processo viene ripetuto nuovamente per ogni successiva self-service BI sforzo, con più utenti che eseguono un processo manuale ridondante di individuazione.

Con Azure Data Catalog, l'organizzazione può interrompere questo ciclo di attività. Dopo aver individuato un'origine dati in modo tradizionale, un analista possibile registrarlo toomake è più facilmente individuabili da altri utenti nella hello future. Analista di hello possibile aggiungere più valore annotando hello registrato asset di dati, ma questa annotazione non è necessario tootake luogo a hello la stessa ora di registrazione. Gli utenti possono contribuire nel tempo, come consentire le pianificazioni, gradualmente aggiunta di origini dati di valore toohello registrate nel catalogo di hello.

Questa crescita strutturale del contenuto del catalogo hello è una complemento naturale toohello la registrazione iniziale delle origini dati centrale. Popolamento preliminare catalogo hello con i dati necessari molti utenti può essere un forte motivazione per uso iniziale e l'individuazione. Abilitazione degli utenti tooregister e annotare origini aggiuntive possono essere un tookeep modo coinvolti li e altri membri dell'organizzazione.

Vale la pena notare che anche se questo scenario si concentra in modo specifico su Business Intelligence self-service, hello stesso sfide e i modelli si applicano toolarge scala aziendali progetti BI anche. Usando Data Catalog, l'organizzazione può migliorare qualsiasi attività comporti un processo manuale di individuazione delle origini dati.

## <a name="scenario-3-capturing-tribal-knowledge"></a>Scenario 3: Acquisizione di conoscenze specifiche
Per sapere quali dati è necessario toodo il proprio lavoro e in cui toofind che i dati?

Se si ha una certa familiarità con il processo, probabilmente già si hanno le conoscenze necessarie. Si è effettuato tramite un processo di apprendimento di graduale e nel tempo state fornite informazioni sulle origini dati hello che sono chiavi tooyour quotidiane.

Quando si aggiunge un nuovo dipendente del team, qual è la persona sapere quali dati sono necessari per il processo di hello e in cui toofind è?

Probabilità sono nuova persona hello proviene tooyou con queste domande.

Il trasferimento in corso delle conoscenze fa parte del processo di individuazione dell'origine dati hello in piccole e grandi aziende. Membri del team più esperti e senior siano compilate le conoscenze negli anni hello e i membri del team più recenti imparato tooask quando hanno domande. informazioni più importanti di Hello spesso esistono solo in capi hello di alcuni utenti chiavi, e quando tali utenti sono in vacanza o lasciano il team di hello, organizzazione hello subisce.

Esperti di dati in genere verificare un toodocument sforzo le proprie conoscenze, condivisione tramite posta elettronica o in documenti di Word in un sito di SharePoint del team. Sebbene questo approccio può essere utile, introduce un nuovo problema di individuazione: come si persone sapere quali documentazione esiste e in cui toofind è?

Con Azure Data Catalog, l'organizzazione ha un'unica posizione centrale in cui archiviare e condividere queste informazioni specifiche, rendendole facilmente individuabili. Nel catalogo dati, gli esperti di dati possano annotare asset di dati direttamente e forniscono collegamenti tooexisting documentazione. Quando i membri dell'organizzazione utilizzano hello catalogo toodiscover un'origine dati, vi troveranno non solo l'origine hello stesso, ma anche knowledge hello che esisteva in precedenza solo in mente hello di esperti dell'organizzazione.
