---
title: Configurare e usare l'API Recommendations di Machine Learning | Documentazione Microsoft
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
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Domande frequenti sulla configurazione e sull'uso dell'API Recommendations di Machine Learning
**Che cos'è RECOMMENDATIONS?**

> [!NOTE]
> È consigliabile iniziare usando l'API Recommendations di Servizi cognitivi invece di questa versione. Il Servizio cognitivo di Recommendations sostituirà questo servizio e verranno sviluppate nuove funzionalità. Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.
> Per altre informazioni, vedere [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)
> 
> 

RECOMMENDATIONS in Azure Machine Learning è un motore di raccomandazioni self-service in esecuzione in Azure, ideale per le organizzazioni e le attività che si basano sulle raccomandazioni per il cross-selling e l'upselling ai clienti. Si tratta di un'implementazione di "filtro collaborativo" che usa la fattorizzazione di matrice come algoritmo di base. Gli sviluppatori di applicazioni possono accedere a RECOMMENDATIONS tramite le API REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Quali funzionalità offre RECOMMENDATIONS?**

RECOMMENDATIONS accetta come input un elemento o un insieme di elementi e restituisce un elenco di raccomandazioni rilevanti. Ad esempio, un cliente di un rivenditore online fa clic su un prodotto. Il rivenditore online invia il prodotto specifico come input a RECOMMENDATIONS, ottiene un elenco di prodotti e decide quale prodotto verrà visualizzato al cliente. È consigliabile usare RECOMMENDATIONS per ottimizzare il negozio online o per fornire informazioni al reparto vendite o al call center interno.

**Sono previste limitazioni per l'utilizzo?**

L'utilizzo di Recommendations ha le limitazioni seguenti:

* Numero massimo di modelli per sottoscrizione: 10
* Numero massimo di elementi che possono essere inclusi nel catalogo: 100.000
* Il numero massimo di punti di utilizzo mantenuti è ~5.000.000. I meno recenti saranno eliminati se ne vengono caricati o segnalati di nuovi.
* La dimensione massima dei dati che possono essere inviati per posta elettronica (ad esempio, importazione dei dati del catalogo o dei dati di utilizzo) è di 200 MB.
* Il numero di transazioni al secondo (TPS) per una compilazione di un modello di raccomandazioni non attiva è di ~2 TPS. Una compilazione del modello di raccomandazioni attiva può includere un massimo di 20 TPS.

## <a name="purchase-and-billing"></a>Acquisto e fatturazione
**Qual è il costo di Recommendations durante il periodo di lancio?**

Recommendations è un servizio basato su sottoscrizione. Gli addebiti sono basati sul volume di transazioni al mese. Per informazioni sui prezzi, è possibile vedere la [pagina delle offerte](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace.

**Sono previsti costi per la registrazione e l'archiviazione dell'attività utente tramite Recommendations?**

Al momento no.

**È disponibile una versione di valutazione gratuita per Recommendations?**

La versione di valutazione gratuita disponibile è limitata a 10.000 transazioni al mese.

**Quando verrà emessa la fattura per Recommendations?**

Una sottoscrizione a pagamento è una sottoscrizione per cui sono previste tariffe mensili. Quando si acquista una sottoscrizione a pagamento, si riceve immediatamente l'addebito per il primo mese d'uso. Viene addebitato l'importo indicato accanto all'offerta nella pagina di sottoscrizione, con l'aggiunta di eventuali imposte applicabili. L'addebito mensile viene effettuato ogni mese nello stesso giorno di calendario in cui è stato effettuato l'acquisto originale, fino all'annullamento della sottoscrizione. 

**Come si esegue l'aggiornamento a servizi di livello superiore?**

È possibile acquistare o aggiornare la sottoscrizione dalla [pagina delle offerte](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace.

Quando si aggiorna una sottoscrizione:

* Le transazioni rimanenti nella sottoscrizione precedente non verranno aggiunte alla nuova sottoscrizione. 
* Sarà necessario pagare il prezzo completo per la nuova sottoscrizione, anche se nella sottoscrizione precedente sono presenti transazioni non usate.

Processo per aggiornare una sottoscrizione:

* Passare alla [pagina delle offerte](https://datamarket.azure.com/dataset/amla/recommendations).
* Accedere al Marketplace se non è già stato fatto.
* Nel riquadro a sinistra sono elencati tutti i piani disponibili. Fare clic sul pulsante di opzione del piano da aggiornare.
* Per eseguire l'aggiornamento, fare clic su **OK**nella finestra di dialogo. Se non si vuole eseguire l'aggiornamento, fare clic su **Annulla**.

**Importante** : esaminare attentamente la finestra di dialogo prima di eseguire l'aggiornamento, perché sono previste implicazioni a livello di fatturazione e uso.

**Quando scade la sottoscrizione a Recommendations?**

La sottoscrizione avrà termine quando la si annulla. Per annullare le sottoscrizioni, vedere le istruzioni seguenti.

**Come si annulla la sottoscrizione a Recommendations?**

Per annullare la sottoscrizione, eseguire la procedura seguente. Se la sottoscrizione attuale è una sottoscrizione a pagamento, rimarrà attiva fino al termine del periodo di fatturazione corrente. Se è necessario annullarla con effetto immediato, contattare il [Supporto tecnico Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Nota** : non sono previsti rimborsi in caso di annullamento prima della fine di un periodo di fatturazione o per le transazioni non usate in un periodo di fatturazione.

* Passare alla [pagina delle offerte](https://datamarket.azure.com/dataset/amla/recommendations).
* Accedere al Marketplace se non è già stato fatto.
* Fare clic su **Annulla** a destra del nome e dello stato del set di dati. È possibile usare questa sottoscrizione fino al termine del periodo di fatturazione corrente o fino al raggiungimento del limite di transazioni, a seconda di quale evento si verifica per primo.

Per annullare immediatamente la sottoscrizione e acquistarne una nuova, inviare un ticket al [Supporto tecnico Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Introduzione a Recommendations
**Per quali utenti è consigliabile Recommendations?** 

Recommendations in Machine Learning è ideale per le organizzazioni e le attività che si basano sulle raccomandazioni per il cross-selling e l'upselling di prodotti e servizi ai clienti. Se si ha un sito Web pubblico, una forza vendita, una forza vendita interna o un call center e se si offre un catalogo che include più di qualche decina di prodotti o servizi, l'uso di Recommendations può offrire molti vantaggi. 

Sperimentare l'uso di Recommendations è abbastanza semplice. La versione attuale basata su API richiede competenze di programmazione di base. Se è necessaria assistenza, rivolgersi al fornitore che ha sviluppato il sito Web. Se nell'organizzazione è disponibile un reparto IT o è presente uno sviluppatore interno, dovrebbe essere in grado di configurare Recommendations per l'uso nell'organizzazione. 

**Quali sono i prerequisiti per la configurazione di Recommendations?**

Recommendations richiede la disponibilità di un log di scelte utente in relazione al catalogo. Se il log non è disponibile e si usa un sito Web pubblico, si potrà usare Recommendations per raccogliere automaticamente informazioni sulle attività degli utenti. 

Recommendations richiede anche un catalogo di prodotti o servizi. Se il catalogo non è disponibile, Recommendations può usare i dati di uso effettivi dei clienti per estrarre un catalogo. Un catalogo implicito non include elementi non segnalati come parte delle transazioni degli utenti.

**Come si configura Recommendations per la prima volta?**

Dopo la [sottoscrizione](https://datamarket.azure.com/dataset/amla/recommendations) a Recommendations, è necessario usare la documentazione dell'API disponibile nella [Guida introduttiva per l'API Recommendations di Azure Machine Learning](machine-learning-recommendation-api-quick-start-guide.md) per configurare il dispositivo.

**Dove è possibile trovare la documentazione sulle API?** 

La documentazione sulle API è disponibile nella [Guida introduttiva per l'API Recommendations di Azure Machine Learning](machine-learning-recommendation-api-quick-start-guide.md).

**Quali sono le opzioni disponibili per caricare i dati relativi al catalogo e all'utilizzo in Recommendations?**

Per caricare i dati relativi al catalogo e all'utilizzo sono disponibili due opzioni: è possibile esportare questi dati dal sistema CRM o da altri log e caricarli in Recommendations oppure aggiungere tag al sito Web, in modo da tenere traccia delle attività degli utenti. Se si usa il secondo metodo, i dati saranno archiviati in Azure.

## <a name="maintenance-and-support"></a>Manutenzione e supporto
**Quali sono le dimensioni massime consentite per i set di dati?**

Ogni set di dati può includere al massimo 100.000 elementi del catalogo e fino a 2048 MB di dati di utilizzo.
Una sottoscrizione può anche includere un massimo di 10 set di dati (modelli).

**Dove si può ottenere il supporto tecnico per Recommendations?**

Il supporto tecnico è disponibile tramite il sito del [supporto tecnico di Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) .

**Dove si trovano le condizioni per l'utilizzo?**

[Condizioni del servizio relative all'API Recommentazions di Microsoft Azure Machine Learning](https://datamarket.azure.com/dataset/amla/recommendations#terms).

