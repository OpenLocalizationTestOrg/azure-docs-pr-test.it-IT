---
title: Panoramica del processo di analisi scientifica dei dati di Team aaaAzure | Documenti Microsoft
description: Fornisce un analitica predittiva data science metodologia toodeliver soluzioni e le applicazioni intelligenti.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Panoramica del processo di data science per i team

Hello Team Data Science processo (TDSP) è un agile, soluzioni di dati iterativi scienza metodologia toodeliver analitica predittiva e applicazioni intelligenti in modo efficiente. Il TDSP consente di migliorare la collaborazione tra team e l'apprendimento. Contiene una distillazione consigliate hello e strutture di Microsoft e di altri utenti nel settore hello che semplificano la corretta implementazione di hello delle iniziative di analisi scientifica dei dati. obiettivo di Hello è toohelp aziende completamente che hello del programma analitica.

Questo articolo riporta una panoramica del TDSP e dei suoi componenti principali. È fornire una descrizione generica del processo di hello qui che può essere implementata con una varietà di strumenti. Ulteriori argomenti collegati, viene fornita una descrizione più dettagliata delle attività di progetto hello e ruoli coinvolti nel ciclo di vita di hello del processo di hello. Informazioni aggiuntive su come viene fornito anche hello tooimplement TDSP con un set specifico di infrastruttura che utilizziamo hello tooimplement TDSP i team e gli strumenti di Microsoft.

## <a name="key-components-of-hello-tdsp"></a>Componenti principali di hello TDSP

TDSP è costituito dai seguenti componenti chiave hello:

- Una definizione del **ciclo di vita del data science**
- Una **struttura di progetto standardizzata**
- **Infrastruttura e risorse** per i progetti di data science
- **Strumenti e utilità** per l'esecuzione dei progetti


## <a name="data-science-lifecycle"></a>Ciclo di vita del data science

Hello Team Data Science processo (TDSP) fornisce sviluppo hello toostructure del ciclo di vita dei progetti di analisi scientifica dei dati. ciclo di vita Hello descrive i passaggi di hello, dall'inizio toofinish, i progetti seguenti in genere quando vengono eseguiti.

Se si utilizza un altro del ciclo di analisi scientifica dei dati, ad esempio [metodologia](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) o un processo personalizzato dell'organizzazione, è comunque possibile usare hello TDSP basato su attività nel contesto di hello di tali sviluppo cicli di vita. In generale queste diverse metodologie hanno molto in comune. 

Questo ciclo di vita è stato messo a punto per i progetti di data science inclusi in applicazioni intelligenti. Queste applicazioni distribuiscono modelli di Machine Learning o intelligenza artificiale per l'analisi predittiva. Anche i progetti di data science esplorativi o i progetti analitici ad hoc possono trarre vantaggio dall'utilizzo di questo processo. Ma in questi casi alcuni dei passaggi di hello descritti può non essere necessaria.    

ciclo di vita TDSP Hello è costituito da cinque fasi principali che vengono eseguite in modo iterativo:

* **Informazioni commerciali**
* **Acquisizione e comprensione dei dati**
* **Modellazione**
* **Distribuzione**
* **Accettazione del cliente**

Ecco una rappresentazione visiva di hello **ciclo di vita del processo di analisi scientifica dei dati di Team**. 

![Ciclo di vita TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Hello obiettivi, attività e gli elementi di documentazione per ogni fase del ciclo di vita di hello in TDSP sono descritti in hello [ciclo di vita del processo di analisi scientifica dei dati di Team](data-science-process-lifecycle.md) argomento. Queste attività ed elementi sono associati a ruoli di progetto:

- Architetto di soluzioni
- Project manager
- Data scientist
- Responsabile di progetto 

Hello diagramma seguente offre una visualizzazione griglia di attività di hello (in blu) e gli elementi (in verde) associati a ogni fase del ciclo di vita di hello (su hello asse orizzontale) per questi ruoli (su hello asse verticale). 

![TDSP-roles-and-tasks](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Struttura di progetto standardizzata

Tutti i progetti condividono una struttura di directory e utilizzare i modelli per i documenti progetto contribuisce a semplificare per hello team membri toofind informazioni sui progetti. Tutto il codice e i documenti vengono archiviati in un sistema di controllo di versione (dei contenitori dei volumi) come la collaborazione tra team tooenable Subversion Git o TFS. Rilevamento di attività e funzionalità in un progetto agile rilevamento sistema come Jira, Rally, Visual Studio Team Services consente di codice hello per le singole funzionalità di rilevamento più vicino. Tale rilevamento consente inoltre di tooobtain team meglio stime dei costi. TDSP consigliabile creare un archivio separato per ogni progetto in hello dei contenitori dei volumi per il controllo delle versioni, la protezione delle informazioni e la collaborazione. Hello standardizzato struttura per tutti i progetti consente di compilazione knowledge istituzionale organizzazione hello.

Si forniscono modelli per la struttura di cartelle hello e documenti richiesti in posizioni standard. Questa struttura di cartelle consente di organizzare i file hello che contengono codice per l'esplorazione dei dati e di estrazione di funzioni e che registrano le iterazioni del modello. Questi modelli semplificano team membri toounderstand lavoro svolto da altri utenti e tooadd nuovi membri tooteams. È facili modelli di documento tooview e update in formato markdown. Utilizzare gli elenchi di controllo di modelli tooprovide con domande chiave per ogni progetto tooinsure che problema hello è ben definito e che i risultati finali soddisfino qualità hello previsto. Tra gli esempi sono inclusi:

- un problema aziendale di progetto fondatore toodocument hello e un ambito di progetto hello
- struttura hello toodocument report dei dati e le statistiche dei dati non elaborati hello
- hello toodocument di report modello derivato funzionalità
- metriche di prestazioni del modello come curve ROC o MSE


![TDSP-directories](./media/data-science-process-overview/tdsp-dir-structure.png)

struttura di directory Hello può essere clonato da [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infrastruttura e risorse per i progetti di data science

Il TDSP fornisce suggerimenti per la gestione dell'infrastruttura di analisi e archiviazione, ad esempio:

- file system su cloud per l'archiviazione dei set di dati, 
- database
- cluster Big Data (Hadoop o Spark) 
- servizi di Machine Learning. 

infrastruttura di archiviazione e analitica Hello può essere in locale o cloud hello. Si tratta della posizione in cui sono archiviati i set di dati non elaborati ed elaborati. Questa infrastruttura consente di eseguire analisi riproducibili. Inoltre, evita la duplicazione, che può causare tooinconsistencies e i costi di infrastruttura non necessari. Gli strumenti vengono forniti tooprovision hello risorse condivise, tenerne traccia e consentire a ogni tooconnect membro del team di risorse toothose in modo sicuro. È inoltre consigliabile che i membri del progetto creino un ambiente di calcolo coerente. Diversi membri del team possono quindi replicare e convalidare gli esperimenti.

Di seguito è riportato un esempio di un team che lavora su più progetti e condivide diversi componenti dell'infrastruttura di analisi su cloud.

![TDSP-infrastructure](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Strumenti e utilità per l'esecuzione dei progetti

Introdurre processi nella maggior parte delle organizzazioni è complesso. Gli strumenti forniti ciclo di vita e processo di analisi scientifica dei dati hello tooimplement aumentare inferiore hello barriere tooand coerenza hello dell'adozione. TDSP fornisce un set iniziale di strumenti e script di avvio toojump adozione di TDSP all'interno di un team. Consente inoltre di automatizzare alcune attività comuni di hello nel ciclo di vita di hello data science, ad esempio l'esplorazione dei dati e modellazione di base. È una struttura ben definita fornito per utenti singoli toocontribute condiviso strumenti e utilità nel repository di codice condiviso del team. Queste risorse possono quindi essere sfruttate da altri progetti all'interno del team di hello o organizzazione hello. TDSP prevede inoltre i contributi hello tooenable di strumenti e utilità toohello Comunità. utilità TDSP Hello possono essere clonate da [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Passaggi successivi

[Processo di analisi scientifica dei dati di team: Ruoli e attività](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) vengono descritti i ruoli del personale chiave hello e le relative attività associate per un team di analisi scientifica dei dati che consente di standardizzare su questo processo. 
