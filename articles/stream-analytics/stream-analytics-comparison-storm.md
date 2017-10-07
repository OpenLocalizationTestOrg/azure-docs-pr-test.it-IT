---
title: 'Piattaforme Analitica: Apache Storm confronto tooStream Analitica | Documenti Microsoft'
description: "Scelta di una piattaforma di cloud analitica utilizzando un tooStream confronto Apache Storm Analitica indicazioni. Comprendere le funzionalità e le differenze."
keywords: piattaforma di analisi, piattaforme di analisi, piattaforma di analisi cloud, confronto con Storm
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a>Scegliere una piattaforma di analisi di flusso: confronto tra Apache Storm e Analisi di flusso di Azure
Azure offre diverse soluzioni per l'analisi dei flussi di dati: [Analisi di flusso di Azure](https://docs.microsoft.com/azure/stream-analytics/) e [Apache Storm in Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/). Entrambe le piattaforme analitica hello vantaggi di una soluzione PaaS. Ma piattaforme hello presentano alcune differenze significative anche le funzionalità come illustrato come configurare e gestirli. 

Questo articolo fornisce un confronto side-by-side di funzionalità toohelp che si sceglie tra Apache Storm e Analitica di flusso di Azure come piattaforma cloud analitica. 

## <a name="general-features"></a>Funzionalità generali

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Analisi di flusso di Azure</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm in HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Open source?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
No. Analisi di flusso di Azure è un'offerta proprietaria Microsoft.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sì. Apache Storm è una tecnologia concessa in licenza da Apache.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Supporto tecnico Microsoft?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Sì </p>
            </td>
            <td width="246" valign="top">
                <p>
Sì </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Requisiti hardware</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Nessuno. Analisi di flusso di Azure è un servizio di Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Nessuno. Apache Storm è un servizio di Azure.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Unità di livello superiore</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gli utenti distribuiscono e monitorano i processi di streaming.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli utenti distribuiscono e monitorano un intero cluster, che può ospitare più processi di Storm nonché altri carichi di lavoro (incluso il batch).
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Prezzi</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Prezzo al volume dei dati elaborati e hello numero di unità di streaming necessarie per ogni ora che hello processo è in esecuzione. 
                </p>
                    <p>Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Prezzi di Analisi di flusso</a>.</p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
unità di Hello di acquisto è basata su cluster e viene addebitato in base a ora hello hello cluster è in esecuzione, indipendente da processi di distribuzione.
                </p>
                <p>
Per altre informazioni, vedere <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Prezzi di HDInsight</a>.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a>Creazione

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Analisi di flusso di Azure</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm in HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Funzionalità: DSL SQL?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Sì. Analisi di flusso di Azure fornisce un linguaggio simile a SQL per la creazione di trasformazioni.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
No. Gli utenti devono scrivere il codice in Java o C# o usare le API Trident.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Funzionalità: operatori temporali?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Per impostazione predefinita sono supportati i join temporali e le aggregazioni finestra.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli operatori temporali devono essere implementati da utente hello.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Esperienza di sviluppo</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gli utenti possono creare, eseguire il debug e monitorare i processi tramite il portale di Azure, hello utilizzando dati di esempio derivati da un flusso in tempo reale.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli utenti che utilizzano .NET possono sviluppare, eseguire il debug e monitorare tramite Visual Studio. Gli utenti utilizzando Java o in altri linguaggi possono utilizzare hello IDE di propria scelta.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Supporto per il debug</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
I registri di stato e le operazioni di processo di base sono disponibili toohelp debug. Flusso Analitica attualmente non consentire agli utenti di specificare il tipo di contenuto o la quantità di contenuto è incluso nei registri hello (ad esempio, la modalità dettagliata).
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sono disponibili log dettagliati. Gli utenti possono accedere i log in Visual Studio o dal cluster toohello accesso a registri hello direttamente.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Estensibilità tramite codice personalizzato?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Supporto parziale con UDF JavaScript. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integrazione UDF di JavaScript</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sì. Gli utenti possono scrivere codice personalizzato in C#, Java o qualsiasi altro linguaggio supportato in Storm.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a>Origini dati (input) e output ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Analisi di flusso di Azure</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm in HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                 <strong>Origini dati di input</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>Hub eventi di Azure e Archiviazione BLOB di Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
I connettori sono disponibili per l'Hub eventi di Azure, Bus di servizio di Microsoft Azure, Kafka e altro ancora. Gli utenti possono creare connettori aggiuntivi con codice personalizzato.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formati di dati di input</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Avro, JSON, CSV </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli utenti possono implementare tutti i formati utilizzando codice personalizzato.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Output</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Un processo di streaming può avere più output. Output supportati: Hub eventi di Azure, Archiviazione BLOB di Azure, Archiviazione tabelle di Azure, Azure SQL DB e Power BI.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm supporta più output in una topologia e ogni output può avere una logica personalizzata per l'elaborazione downstream. Storm include connettori predefiniti per Power BI, Hub eventi di Azure, Archiviazione BLOB di Azure, Azure Cosmos DB, SQL e HBase. Gli utenti possono creare connettori aggiuntivi con codice personalizzato.    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formati di codifica dei dati</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Dati devono essere formattati usando UTF-8.
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
Gli utenti possono implementare tutti i formati di codifica dei dati usando codice personalizzato.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a>Gestione e operazioni ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Analisi di flusso di Azure</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm in HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Modello di distribuzione dei processi</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Portale di Azure, PowerShell e API REST.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Portale di Azure, PowerShell, Visual Studio e API REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Monitoraggio (statistiche, contatori e così via)</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Il monitoraggio viene implementato tramite il portale di Azure e le API REST. Gli utenti possono inoltre configurare gli avvisi di Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Il monitoraggio viene implementato tramite hello Storm UI e le API REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Scalabilità</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
La scalabilità è determinata dal numero di hello di unità di Streaming (SUs) per ogni processo. Ogni unità di Streaming elabora backup too1 MB al secondo, con un massimo di 50 unità. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">velocità effettiva di scala tooincrease</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
La scalabilità è determinata dal numero di hello di nodi nel cluster HDInsight Storm hello. limite superiore di Hello numero hello di nodi è definito dalla quota di Azure dell'utente hello.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Limiti di elaborazione dei dati</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Gli utenti possono aumentare l'elaborazione dati o ottimizzare i costi aumentando o diminuendo hello numero di unità di Streaming, con un limite superiore di 1 GB al secondo.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli utenti possono scalare le dimensioni cluster per aumentarle o diminuirle.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Arresto/ripresa</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Arrestare e riprendere dall'ultimo punto di arresto.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Arrestare e riprendere dall'ultimo punto di arresto in base al limite.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Aggiornamento del servizio e del framework</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Applicazione di patch automatica senza tempi di inattività.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Applicazione di patch automatica senza tempi di inattività.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Continuità aziendale grazie a un servizio a disponibilità elevata con contratti di servizio garantiti</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li>Tempo di attività per il contratto di servizio del 99,9%</li>
                <li>Ripristino automatico in caso di errori</li>
                <li>Ripristino predefinito degli operatori temporali con stato</li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
Contratto di servizio del 99,9% tempo di attività del cluster Storm hello. 
                </p>
                <p>
Apache Storm è una piattaforma di streaming a tolleranza di errore. Tuttavia, è tooensure responsabilità dell'utente hello che il flusso di esecuzione dei processi senza interruzioni.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a>Funzionalità avanzate ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong> </strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Analisi di flusso di Azure</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm in HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Gestione di eventi di arrivo in ritardo e con ordine non corretto</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Criteri configurabili predefiniti per riordinare e rilasciare gli eventi o modificare l'ora degli eventi.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Gli utenti devono implementare logica toohandle questo scenario.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Dati di riferimento</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Dati di riferimento sono disponibili dall'archiviazione BLOB di Azure con un massimo di 100 MB di cache in memoria. Dati di riferimento viene aggiornati dal servizio hello.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Nessun limite alle dimensioni dei dati. I connettori sono disponibili per HBase, Azure Cosmos DB, SQL Server e Azure. Gli utenti possono creare connettori aggiuntivi con codice personalizzato. I dati di riferimento devono essere aggiornati con un codice personalizzato.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Integrazione con Machine Learning</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
I modelli di Azure Machine Learning pubblicati possono essere configurati come funzioni durante la creazione dei processi. Per altre informazioni, vedere <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scalabilità per le funzioni di Machine Learning</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Disponibile tramite i bolt di Storm.
                </p>
            </td>
        </tr>
    </tbody>
</table>
