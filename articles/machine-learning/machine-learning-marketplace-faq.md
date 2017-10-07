---
title: domande frequenti - AAA(deprecated) pubblicare e usare le app di Machine Learning in Azure Marketplace | Documenti Microsoft
description: (obsoleto) Domande frequenti sulla pubblicazione delle app di Machine Learning in hello Azure Marketplace
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(obsoleto) La pubblicazione e si usano app di Machine Learning in Azure Marketplace hello: domande frequenti

> [!NOTE]
> DataMarket e Servizi dati verranno ritirati e le sottoscrizioni esistenti verranno ritirate e annullate a partire dal 31/3/2017. Di conseguenza, questo articolo è deprecato. 
> 
> In alternativa, è possibile pubblicare il toohello esperimenti di Machine Learning [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) benefit hello della community di analisi scientifica dei dati hello. Per ulteriori informazioni, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Domande sull'utilizzo da Marketplace
**1. Perché viene visualizzato hello seguente messaggio di errore dopo immettere per il servizio web hello:**

**richiesta di Hello ha restituito un timeout di back-end o back-end. il team di Hello sta analizzando problema hello. Siamo spiacenti per eventuali inconvenienti hello. (500)**

I parametri di input potrebbero non essere conforme toohello formato richiesto per il servizio web specifico hello. Per i parametri di input e le limitazioni di hello di questo servizio web, vedere toohello corrispondente documentazione collegamento toofind hello formato corretto.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Se Copia collegamento hello API per il servizio web hello che viene visualizzato nella pagina "Esplora set di dati" hello e incollarlo in un'altra finestra del browser, le credenziali, è necessario è possibile utilizzare tooaccess hello risultati e come viene visualizzato?**

È necessario utilizzare l'account di Marketplace come nome utente hello e una chiave account primaria hello come password hello. chiave account primaria Hello è reperibile in hello **esplorare il set di dati** pagina Descrizione hello del servizio web hello (fare clic su hello **Mostra** pulsante). risultato Hello potrebbe essere visualizzato in browser hello o potrebbe essere disponibile troppo download, a seconda del browser in uso.

**3. Perché viene visualizzato hello seguente messaggio di errore dopo avere immesso input hello per il servizio web hello nella pagina "Esplora set di dati" hello:** 

**Si è verificato un errore imprevisto durante l'elaborazione della richiesta. Riprovare più tardi.**

Uno o più parametri di input del servizio web potrebbero essere superato il limite di lunghezza hello durante l'utilizzo del servizio web hello in marketplace hello **esplorare il set di dati** pagina. servizi Hello possono essere chiamati con una lunghezza di input più utilizzando i metodi HTTP POST. Per esempi, vedere [l'uso di R in Machine Learning e pubblicati tooMarketplace soluzioni di esempio](machine-learning-r-csharp-web-service-examples.md).

**4. Perché non riesco a visualizzare tutti gli elementi hello "Esplora API" scheda int hello archivio nel portale di Azure classico hello?** 

Si tratta di un problema noto con hello Azure Marketplace portale classico. il team di Hello sta tooresolve questo problema. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Domande sulla pubblicazione da Azure Machine Learning nel Marketplace
**1. Perché i logo, le immagini e il numero di transazioni non vengono aggiornati per il servizio Web?** 

Logo e immagini vengono memorizzati nella cache nel portale di pubblicazione hello e potrebbe richiedere fino a too10 giorni per il nuovo logo hello o tooupdate immagine nel portale di hello.

**2. Perché è una scheda di "Dettagli" hello del servizio web in Marketplace che mostra un messaggio di errore?**

È presente un problema noto di Marketplace quando ci si connette tooAzure Machine Learning per i dettagli del servizio. il team di Hello sta tooresolve questo problema.

**3. Perché il codice di esempio R nei servizi web di Azure Machine Learning hello hello non funziona per i servizi web di hello dispendiosa in termini di mercato?**

sistemi di autenticazione Hello sono diversi, la connessione a servizi web di Machine Learning tooAzure diretta rispetto a servizi web di toothese tooconnecting tramite hello Marketplace. servizi di Hello in Marketplace sono servizi OData, e possono essere chiamati con i metodi GET o POST. 

**4. Perché sono collegamenti per il supporto di hello del servizio web offre l'aggiornamento non correttamente per alcune delle mie proposte?**

collegamenti per il supporto di Hello sono globali per ogni server di pubblicazione, non per l'offerta. 

**5. Come si pubblica un servizio Web con modalità di input batch nel Marketplace?**

modalità di input di Hello batch non è attualmente supportata nei servizi web Marketplace.

**6. Chi contattare Guida tooget domande su come diventare un editore di dati o se verificano problemi durante la pubblicazione?**

Contattare il team di Azure Marketplace hello < mailto:datamarketbd@microsoft.com > per ulteriori informazioni.

