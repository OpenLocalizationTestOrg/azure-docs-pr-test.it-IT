---
title: aaaSet backup e utilizzare hello Machine Learning indicazioni API | Documenti Microsoft
description: API Recommendations Microsoft create con le domande frequenti su Azure Machine Learning
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
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
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Domande frequenti sulla configurazione e sull'uso dell'API Recommendations di Machine Learning
**Che cos'è RECOMMENDATIONS?**

> [!NOTE]
> È consigliabile iniziare utilizzando hello indicazioni API cognitivi servizio invece di questa versione. Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste. Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.
> Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate)
> 
> 

Per le organizzazioni e le aziende che si basano su toocross indicazioni offerte speciali e prodotti di offerte speciali e clienti tootheir servizi, indicazioni in Azure Machine Learning fornisce un motore indicazioni self-service. Si tratta di un'implementazione di "filtro collaborativo" che usa la fattorizzazione di matrice come algoritmo di base. Gli sviluppatori di applicazioni possono accedere a RECOMMENDATIONS tramite le API REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Quali funzionalità offre RECOMMENDATIONS?**

RECOMMENDATIONS accetta come input un elemento o un insieme di elementi e restituisce un elenco di raccomandazioni rilevanti. Ad esempio, un cliente di un rivenditore online fa clic su un prodotto. punto vendita online Hello invia tale prodotto come input tooRECOMMENDATIONS, ottiene un elenco di prodotti in cambio e decide quali di questi prodotti verranno visualizzati toohello cliente. Si desidera toouse indicazioni toooptimize negozio online oppure anche tooinform l'interno center chiamata o di reparto vendite.

**Sono previste limitazioni per l'utilizzo?**

Indicazioni è hello limitazioni di utilizzo seguenti:

* Numero massimo di modelli per sottoscrizione: 10
* Numero massimo di elementi che possono essere inclusi nel catalogo: 100.000
* numero massimo di Hello di punti di utilizzo che vengono conservati è ~ 5.000.000. Hello meno recente verrà eliminato verranno caricati o segnalati nuovi.
* La dimensione massima dei dati che possono essere inviati per posta elettronica (ad esempio, importazione dei dati del catalogo o dei dati di utilizzo) è di 200 MB.
* Il numero di transazioni al secondo (TPS) per una compilazione di un modello di raccomandazioni non attiva è di ~2 TPS. Una compilazione del modello indicazioni attivo può contenere fino too20 TPS.

## <a name="purchase-and-billing"></a>Acquisto e fatturazione
**Indicazioni costa durante il periodo di avvio hello?**

Recommendations è un servizio basato su sottoscrizione. Gli addebiti sono basati sul volume di transazioni al mese. È possibile controllare hello [offrono pagina](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace per informazioni sui prezzi.

**Sono previsti costi per la registrazione e l'archiviazione dell'attività utente tramite Recommendations?**

Non un determinato momento hello.

**È disponibile una versione di valutazione gratuita per Recommendations?**

Non vi è un itinerario gratuito che è limitato too10, 000 transazioni al mese.

**Quando verrà emessa la fattura per Recommendations?**

Una sottoscrizione a pagamento è una sottoscrizione per cui sono previste tariffe mensili. Quando si acquista una sottoscrizione a pagamento, riceve immediatamente l'addebito per hello primo utilizzo mese di. Si viene addebitato l'importo di hello associato hello offerta nella pagina di sottoscrizione hello (più le imposte applicabili). L'addebito mensile viene eseguita ogni mese in hello stesso calendario data di acquisto originale, fino a quando non si Annulla sottoscrizione hello. 

**Come eseguire l'aggiornamento del servizio di livello superiore tooa?**

È possibile acquistare o aggiornare la sottoscrizione da hello [offrono pagina](https://datamarket.azure.com/dataset/amla/recommendations) pagina in Microsoft Azure Marketplace.

Quando si aggiorna una sottoscrizione:

* Le transazioni rimanenti nella sottoscrizione precedente non vengono aggiunti tooyour nuova sottoscrizione. 
* Si paga il prezzo completo per la nuova sottoscrizione hello, anche se dispone di transazioni non usate nella sottoscrizione precedente.

Processo tooupgrade una sottoscrizione:

* Nevigate toohello [offrono pagina](https://datamarket.azure.com/dataset/amla/recommendations).
* Se non già effettuato l'accesso, accedi toohello Marketplace.
* Nel riquadro di destra hello, sono elencati tutti i piani disponibili hello. Fare clic su pulsante di opzione hello per piano di hello da tooupgrade per.
* Se si desidera tooupgrade, fare clic su **OK**. Se si desidera tooupgrade, fare clic su **Annulla**.

**Importante** la finestra di dialogo di hello leggere con attenzione prima di aggiornare poiché sono presenti le implicazioni di fatturazione e utilizzo.

**Quando terminerà tooRecommendations la sottoscrizione?**

La sottoscrizione avrà termine quando la si annulla. Se si desidera toocancel delle sottoscrizioni, vedere hello attenendosi alle istruzioni.

**Come si annulla la sottoscrizione a Recommendations?**

toocancel la sottoscrizione, utilizzare hello seguendo i passaggi. Se la sottoscrizione corrente è una sottoscrizione a pagamento, la sottoscrizione rimarrà attiva fino a fine di hello hello periodo di fatturazione corrente. Se è necessario hello toobe annullamento effettiva immediatamente, contattare Microsoft all'indirizzo [supporto Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Nota** non sono previsti rimborsi se annullare prima hello fine del periodo di fatturazione o per le transazioni inutilizzate in un periodo di fatturazione.

* Passare toohello [offrono pagina](https://datamarket.azure.com/dataset/amla/recommendations).
* Se non già effettuato l'accesso, accedi toohello Marketplace.
* Fare clic su **Annulla** toohello destra del nome di set di dati hello e lo stato. È possibile usare questa sottoscrizione fino al raggiungimento fine hello di hello fatturazione periodo o il limite della transazione corrente (a seconda del valore si verifica per primo).

Se si desidera toocancel la sottoscrizione immediatamente così è possibile acquistare una nuova sottoscrizione, creare un ticket al [supporto Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Introduzione a Recommendations
**Per quali utenti è consigliabile Recommendations?** 

Indicazioni in Machine Learning è per le organizzazioni e le aziende che si basano sui consigli toocross-selling e indirizzare i prodotti o servizi tootheir clienti. Se si ha un sito Web pubblico, una forza vendita, una forza vendita interna o un call center e se si offre un catalogo che include più di qualche decina di prodotti o servizi, l'uso di Recommendations può offrire molti vantaggi. 

Esperimenti con indicazioni è progettato toobe piuttosto semplice. versione di Hello corrente basate su API richiede competenze di programmazione di base. Se è necessaria assistenza, contattare il fornitore hello che ha sviluppato il sito Web. Se si dispone di un reparto IT interno o uno sviluppatore interno, dovrebbero essere in grado di tooget indicazioni toowork automaticamente. 

**Quali sono hello prerequisiti per la configurazione di suggerimenti?**

Raccomandazioni richiede la presenza di un log delle scelte dell'utente in relazione tooyour catalogo. Se il log non è disponibile e si usa un sito Web pubblico, si potrà usare Recommendations per raccogliere automaticamente informazioni sulle attività degli utenti. 

Recommendations richiede anche un catalogo di prodotti o servizi. Se non si dispone di catalogo hello, indicazioni possono utilizzare dati di utilizzo reali dei clienti hello e filtrare un catalogo. Un catalogo implicito non include elementi non segnalati come parte delle transazioni degli utenti.

**Come si impostano le indicazioni per hello prima volta?**

Dopo aver [sottoscrizione](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, è consigliabile utilizzare la documentazione di hello API hello [indicazioni di Azure Machine Learning - Guida introduttiva](machine-learning-recommendation-api-quick-start-guide.md) tooset servizio hello.

**Dove è possibile trovare la documentazione sulle API?** 

la documentazione dell'API Hello è [indicazioni di Azure Machine Learning-Guida introduttiva](machine-learning-recommendation-api-quick-start-guide.md).

**Che cosa opzioni ho tooRecommendations di dati di utilizzo e di catalogo tooupload?**

Sono disponibili due opzioni per il caricamento dei dati di utilizzo e di catalogo: È possibile esportare dati hello dal sistema CRM o altri registri e caricarlo tooRecommendations o per aggiungere un sito Web tooyour tag che tengano traccia attività dell'utente. Se si usa quest'ultimo metodo hello, dati hello verranno archiviati in Azure.

## <a name="maintenance-and-support"></a>Manutenzione e supporto
**Quali sono le dimensioni massime consentite per i set di dati?**

Ogni set di dati può contenere backup too100, gli elementi del catalogo 000 e backup too2048 MB di dati di utilizzo.
Inoltre, una sottoscrizione può contenere i set di dati too10 (modelli).

**Dove si può ottenere il supporto tecnico per Recommendations?**

Il supporto tecnico è disponibile in hello [Microsoft Azure supporta](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) sito.

**Dove trovare condizioni hello di utilizzo**

[Condizioni del servizio relative all'API Recommentazions di Microsoft Azure Machine Learning](https://datamarket.azure.com/dataset/amla/recommendations#terms).

