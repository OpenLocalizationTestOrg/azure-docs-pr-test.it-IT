---
title: le funzioni finestra Analitica di aaaIntroduction tooStream | Documenti Microsoft
description: Informazioni sui tre funzioni finestra hello in flusso Analitica (a cascata, di salto, scorrimento).
keywords: finestra a cascata, finestra temporale scorrevole, finestra di salto
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Funzioni finestra Analitica tooStream di introduzione
È necessario tooperform operazioni solo sui dati di hello contenuti nelle finestre temporali in tempo reale molti gli scenari di flusso. Il supporto nativo per funzioni di windowing è una funzionalità chiave di Analitica di flusso di Azure che consente di spostare lancetta hello sulla produttività da sviluppatore per la creazione di processi di elaborazione di flusso complessi. Flusso Analitica consente agli sviluppatori toouse [ **a cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **estendibile** ](https://msdn.microsoft.com/library/dn835051.aspx) operazioni temporali tooperform di windows nel flusso di dati. Vale la pena notare che tutti i [finestra](https://msdn.microsoft.com/library/dn835019.aspx) operazioni di output risultati hello **fine** della finestra hello. output di Hello di finestra hello sarà singolo evento basato sulla funzione di aggregazione hello utilizzato. evento Hello avrà timestamp hello della fine hello finestra hello e tutte le funzioni finestra sono definite con una lunghezza fissa. Infine è importante toonote che tutte le funzioni finestra devono essere utilizzate in un [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) clausola.

![Concetti delle funzioni finestra di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Finestra a cascata
Le funzioni finestra a cascata sono toosegment usato un flusso di dati in segmenti di tempo specifico ed eseguono una funzione su di essi, ad esempio esempio hello riportato di seguito. principali differenze di Hello di una finestra a cascata sono che ripetono, non si sovrappongano e un evento non può appartenere toomore rispetto a una finestra a cascata.

![Introduzione alle funzioni finestra a cascata di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Finestra di salto
Le funzioni finestra di salto consentono di avanzare nel tempo di un periodo fisso. Potrebbe essere facile toothink di essi come finestre a cascata che può essere sovrapposta, quindi gli eventi possono appartenere toomore rispetto a un set di risultati Hopping finestra. una finestra Hopping toomake hello stesso come una finestra a cascata semplicemente uno specificherà toobe di dimensioni hop hello hello stesso come dimensione della finestra hello. 

![Introduzione alle funzioni finestra di salto di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Finestra temporale scorrevole
Le funzioni finestra temporale scorrevole, diversamente dalle finestre a cascata o di salto, generano un output **solo** quando si verifica un evento. Ogni finestra sarà necessario almeno un evento e finestra hello continuamente sposta in avanti un € (epsilon). Ad esempio finestre di salto, gli eventi possono appartenere toomore rispetto a una finestra temporale scorrevole.

![Introduzione alle funzioni finestra temporale scorrevole di Analisi di flusso](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Risorse della Guida per le funzioni finestra
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

