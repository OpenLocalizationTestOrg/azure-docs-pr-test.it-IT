---
title: toowork aaaHow con origini dati 'big data' | Documenti Microsoft
description: Modelli di evidenziazione come tooarticle per l'utilizzo di Azure Data Catalog con origini di dati 'big data', inclusi archiviazione Blob di Azure, Azure Data Lake e Hadoop HDFS.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Come origini di toowork dati di grandi dimensioni in Azure Data Catalog
## <a name="introduction"></a>Introduzione
**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. Si tratta di consentendo alle persone di individuare, comprendere e utilizzare origini dati e il supporto di maggior valore organizzazioni tooget dalle origini dati esistenti, inclusi i dati di grandi dimensioni.

**Azure Data Catalog** supporta hello registrazione del BLOB di archiviazione BLOB di Azure e le directory, nonché i file HDFS Hadoop e directory. Hello semistrutturati natura queste origini dati offre una notevole flessibilità. Tuttavia, tooget hello maggior valore tramite la registrazione con **Azure Data Catalog**, gli utenti devono considerare l'organizzazione delle origini dati hello.

## <a name="directories-as-logical-data-sets"></a>Directory come set di dati logici
Un modello comune per organizzare le origini dati di grandi dimensioni è tootreat directory come set di dati logico. Directory di primo livello sono toodefine utilizzato un set di dati, mentre le sottocartelle di definire le partizioni e hello che contengono dell'archivio dati hello stessi.

Ecco un esempio di questo schema:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

In questo esempio vehicle_maintenance_events e location_tracking_events rappresentano i set di dati logici. Ognuna di queste cartelle contiene file di dati organizzati in sottocartelle per anno e mese. Ogni cartella potrebbe contenere centinaia o migliaia di file.

In questo schema la registrazione di singoli file con **Catalogo dati di Azure** probabilmente non ha senso. In alternativa, registrare directory hello che rappresentano i set di dati di hello essere significativi toohello agli utenti che lavorano con dati hello.

## <a name="reference-data-files"></a>File di dati di riferimento
Un modello complementare è toostore set di dati di riferimento come singoli file. Questi set di dati può essere considerati come sul lato 'small' hello dei big data e sono spesso toodimensions simili in un modello di dati analitici. File di dati di riferimento contengono record di contesto utilizzate tooprovide per bulk hello hello dei file di dati archiviati in un' posizione nell'archivio dati hello.

Ecco un esempio di questo schema:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Quando un esperto di analista o dati funziona con dati hello contenuti in strutture di directory di dimensioni maggiori hello, dati hello in questi file di riferimento possono essere utilizzato tooprovide informazioni più dettagliate per le entità che sono definita tooonly per nome o ID in dati di dimensioni maggiori di hello set.

In questo modello, è consigliabile memorizzarlo file di dati di riferimento individuale tooregister hello con **Azure Data Catalog**. Ogni file rappresenta un set di dati e ognuno può essere annotato ed individuato singolarmente.

## <a name="alternate-patterns"></a>Schemi alternativi
modelli descritti nella precedente sezione hello Hello sono solo due possibili modalità che può essere organizzato in un archivio dati di grandi dimensioni, ma ogni implementazione è diverso. Indipendentemente dalla modalità le origini dati sono strutturate, durante la registrazione delle origini dati di grandi dimensioni con **Azure Data Catalog**, lo stato attivo sulla registrazione hello file e directory che rappresentano i set di dati hello di tooothers valore all'interno del organizzazione. Registrazione di tutti i file e directory possono creare confusione catalogo hello, rendendone più difficile per gli utenti toofind hanno bisogno.

## <a name="summary"></a>Riepilogo
La registrazione delle origini dati con **Azure Data Catalog** rende più semplice toodiscover e comprendere. Registrando e annotazione hello dati file e directory che rappresentano il set di dati logico, si consente agli utenti di trovare e utilizzare origini dati hello che hanno bisogno.
