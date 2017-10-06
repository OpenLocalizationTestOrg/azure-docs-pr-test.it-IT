---
title: operazioni aaaCommon in Machine Learning indicazioni API hello | Documenti Microsoft
description: Recommendations di Azure ML - Applicazione di esempio
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Applicazione di esempio dell'API Recommendations
> [!NOTE]
> È consigliabile iniziare utilizzando hello indicazioni API cognitivi servizio invece di questa versione. Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste. Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.
> Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Scopo
Questo documento illustra l'utilizzo di hello di hello Azure Machine Learning indicazioni API tramite un [applicazione di esempio](https://code.msdn.microsoft.com/Recommendations-144df403).

L'applicazione non è previsto tooinclude le funzionalità complete, né utilizza hello tutte le API. Vengono illustrate alcune tooperform operazioni comuni quando si desidera innanzitutto tooplay con il servizio di suggerimenti di Machine Learning hello. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Introduzione tooMachine il servizio di suggerimenti di apprendimento
Suggerimenti tramite il servizio di suggerimenti di Machine Learning hello sono abilitati quando si compila un modello di raccomandazione basato su hello dati seguenti:

* Un repository di elementi di hello da toorecommend, noto anche come un catalogo
* Rappresentazione dell'uso di hello di elementi per ogni utente o sessione (ciò può essere acquisito nel tempo tramite l'acquisizione dei dati, non come parte di app di esempio hello) di dati

Una volta creato un modello di raccomandazione, è possibile utilizzarlo toopredict elementi che un utente potrebbe essere interessato, in base a tooa Seleziona utente hello di set di elementi (o un singolo elemento).

tooenable hello scenario precedente, si segue hello in hello servizio indicazione di Machine Learning:

* Creare un modello: si tratta di un contenitore logico che contiene i dati di hello (catalogo e utilizzo) e i modelli di stima hello. Il contenitore di ogni modello è identificato da un ID univoco allocato al momento della creazione. Questo ID viene chiamato l'ID modello hello e viene utilizzato per la maggior parte delle API hello. 
* Caricare toocatalog: quando viene creato un contenitore del modello, è possibile associare tooit un catalogo.

**Nota**: creazione di un modello e il caricamento di catalogo tooa vengono in genere eseguite una volta per ciclo di vita del modello hello.

* Utilizzo di caricare: aggiunge contenitore del modello toohello dati sull'utilizzo.
* Compilare un modello di raccomandazione: dopo avere dati sufficienti, è possibile compilare il modello di raccomandazione hello. Questa operazione utilizza hello superiore Machine Learning algoritmi toocreate un modello di raccomandazione. A ogni compilazione è associato un ID univoco, È necessario un record di questo ID tookeep perché è necessario per la funzionalità di hello di alcune API.
* Hello monitoraggio processo di compilazione: una compilazione del modello di raccomandazione è un'operazione asincrona e può richiedere da diverse ore tooseveral minuti, a seconda della quantità di hello di dati (catalogo e utilizzo) e hello parametri di compilazione. Pertanto, è necessario compilazione hello toomonitor. Un modello di raccomandazione viene creato solo se la compilazione associata riesce.
* (Facoltativo) Scegliere una compilazione del modello di raccomandazione attivo: questo passaggio è necessario solo se nel contenitore del modello è disponibile più di una compilazione del modello di raccomandazione. Raccomandazioni tooget richiesta senza indicare il modello di raccomandazione active di hello viene reindirizzata automaticamente da compilazione active di hello sistema toohello predefinito. 

**Nota**: un modello di raccomandazione attivo è pronto per la produzione e viene compilato per i carichi di lavoro di produzione. Differisce da un modello di raccomandazione non attivo che rimane in un ambiente di tipo test, definito a volte gestione temporanea.

* Ottenere raccomandazioni: dopo avere ottenuto un modello di raccomandazione, è possibile attivare le raccomandazioni per un singolo elemento o un elenco di elementi selezionati. 

In genere si richiama Get Recommendation per un certo periodo di tempo. Durante tale periodo di tempo, è possibile reindirizzare i dati di utilizzo toohello sistema di raccomandazione Machine Learning, che aggiunge questo contenitore del modello specificato toohello dati. Quando si dispone di sufficienti dati di utilizzo, è possibile creare un nuovo modello di raccomandazione che incorpora dati di utilizzo aggiuntivo hello. 

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2013 o versioni successive
* Accesso a Internet 
* Sottoscrizione toohello indicazioni API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Soluzione di app di esempio di Azure Machine Learning
Questa soluzione contiene codice sorgente hello, esempio di utilizzo, i file di catalogo e direttive toodownload hello pacchetti che sono necessari per la compilazione.

## <a name="hello-apis-used"></a>le API usate Hello
un'applicazione Hello utilizza la funzionalità di indicazione di Machine Learning tramite un sottoinsieme delle API disponibile. Hello che API seguenti vengono illustrate in un'applicazione hello:

* Creazione di modelli: creare un contenitore logico di toohold i modelli di data e l'indicazione. Un modello è identificato da un nome e non è possibile creare più di un modello con hello stesso nome.
* Caricare il file di catalogo: usare i dati del catalogo tooupload.
* Caricare il file di utilizzo: dati di utilizzo tooupload utilizzati.
* Attivare compilazione: utilizzare un modello di raccomandazione toocreate.
* Monitorare l'esecuzione della compilazione: utilizzare toomonitor hello stato di una compilazione del modello di raccomandazione.
* Scegliere un modello predefinito per il suggerimento: usare tooindicate quali toouse modello di raccomandazione per impostazione predefinita per un determinato contenitore del modello. Questo passaggio è necessario solo se si dispone di più di un modello di raccomandazione e si desidera tooactivate non attivo di compilazione del modello di raccomandazione active hello.
* Ottenere l'indicazione: utilizzare tooretrieve elementi in base tooa dato singolo elemento o un set di elementi consigliati. 

Per una descrizione completa di hello API, vedere la documentazione di Microsoft Azure Marketplace hello. 

**Nota**: con il tempo, un modello può avere diverse compilazioni (non contemporaneamente). Ogni compilazione è stata creata con hello stesso o un aggiornamento del catalogo e i dati di utilizzo aggiuntive.

## <a name="common-pitfalls"></a>Inconvenienti comuni
* È necessario tooprovide il nome utente e le app di esempio hello toorun chiave account principale di Microsoft Azure Marketplace.
* App di esempio in esecuzione hello consecutivamente avrà esito negativo. il flusso dell'applicazione Hello include creazione, caricamento, il monitoraggio di hello e ottenere indicazioni da un modello predefinito. Pertanto, non funziona sull'esecuzione consecutivi se non si modifica il nome modello hello tra le chiamate.
* La raccomandazione potrebbe essere restituita senza dati. app di esempio Hello utilizza un file di catalogo e di utilizzo molto piccolo. Pertanto, alcuni elementi dal catalogo hello non saranno necessario alcun elementi consigliati.

## <a name="disclaimer"></a>Dichiarazione di non responsabilità
app di esempio Hello non è previsto toobe eseguito in un ambiente di produzione. dati Hello forniti nel catalogo di hello sono molto piccoli e non fornisce un modello di raccomandazione significativo. dati Hello viene forniti una dimostrazione. 

