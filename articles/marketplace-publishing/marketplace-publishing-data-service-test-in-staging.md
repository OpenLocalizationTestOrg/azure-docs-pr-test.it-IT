---
title: aaaTesting offrono il servizio dati per hello Marketplace | Documenti Microsoft
description: Comprendere in che modo tootest offrono il servizio dati per hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Test dell'offerta del servizio dati in gestione temporanea
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners). Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Dopo aver completato i primi due passaggi di hello di [creazione dell'account di Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [creazione l'offerta di servizio dati nel portale di pubblicazione](marketplace-publishing-data-service-creation.md) si è pronti per rendere disponibili in hello l'offerta Azure Marketplace. In questo argomento verrà illustrati hello prima, intermedia, passaggio denominato "gestione temporanea"

Indica l'offerta in una "sandbox" in cui è possibile testare e verificare le funzionalità prima di pubblicarlo tooproduction privata di distribuzione di gestione temporanea. offerta Hello apparirà come avverrebbe tooa cliente che ha distribuito di gestione temporanea.

## <a name="step-1-pushing-your-offer-toostaging"></a>Passaggio 1. Push toostaging l'offerta
Inserendo l'offerta toostaging consente offerta hello tootest prima che diventi disponibile toofuture sottoscrittori.  È possibile visualizzare come l'offerta la corretta visualizzazione e per quelli tooyour dati di sottoscrizione.  

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Account di accesso in hello [portale di pubblicazione](https://publish.windowsazure.com)
2. Selezionare **Data Services** nella finestra di navigazione a sinistra di hello
3. Selezionare l'offerta desiderata toopush toostaging. Si noterà hello schermata.
4. Fare clic su **Push tooStaging** pulsante.  
5. Se si verificano problemi con hello offerta necessari toobe completato toostaging toopushing precedente, verrà visualizzato un elenco visualizzato.  Correggere questi elementi facendo clic su ogni elemento nell'elenco di hello. Quando tutte le correzioni apportate, fare clic su **Push tooStaging** nuovamente clic sul pulsante.

Se non esistono problemi con l'offerta finestra popup hello seguente verrà visualizzato.  

Se non si pianificazione/non approvato toosurface l'offerta nel portale di Azure (attualmente dispone di capacità limitata), quindi finestra popup hello appena Chiudi.

tootest i dati del servizio nel portale di Azure (nel portale di DataMarket toohello di addizione), sarà necessario tootest un ID sottoscrizione di Azure con.  L'ID sottoscrizione identificherà account hello che verrà consentito tootest l'offerta.  

Tagliare e incollare l'ID sottoscrizione e fare clic su hello toocontinue di segno di spunta.

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Questi ID le sottoscrizioni di Azure sono necessari per il testing e di gestione temporanea in hello [il portale di gestione di Azure](https://manage.windowsazure.com). Non sono necessari tootest in Azure Marketplace.
> 
> 

Hello che viene visualizzato nella schermata successiva che la pubblicazione viene eseguita mediante la visualizzazione di hello "In corso" icona evidenziata giallo riportata di seguito. Push toostaging accetta tra 10 minuti too15.  Se richiede più tempo, prima di aggiornare il browser (premere F5 in Internet Explorer).  In casi rari hello in cui l'offerta viene comunque eseguita toostaging dopo un'ora, fare clic su contatto hello ci toolet inviarci che si verifica un problema di collegamento.

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Al termine di hello Push tooStaging hello "In corso" icona verrà interrotta lo spostamento e verrà aggiornato lo stato di hello troppo "staging".  Si sono ora pronti tootest l'offerta.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Passaggio 2. Testare l'offerta in gestione temporanea in DataMarket
Fare clic sul collegamento hello dopo il testo hello **"vedere il servizio di offerta...."** schermata di hello toodisplay hello sottoscrittore verrà visualizzato quando l'offerta passa tooproduction e verrà visualizzato in DataMarket.

  ![disegno](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Testare o verificare tutti gli elementi 12 hello contrassegnato sopra tooensure tutti i logo, prezzi/transazioni, testo, immagini, documentazione e collegamenti siano corrette e funzionino correttamente.  Si tratta di un tooensure tempestivamente eventuali valori di test che immessi durante la creazione dell'offerta sono stati sostituiti con i valori effettivi.

1. Logo offerta
2. Nome offerta
3. Sito Web della società tooyour/collegamento del relativo nome di server di pubblicazione
4. Categorie di ricerca per l'offerta
5. Sottoscrittori tooassist collegamento di supporto dell'offerta
6. Descrizione contestuale dell'offerta
7. Piano dell’offerta che descrive i dettagli di fatturazione
8. Collegamento tooimplementation codice
9. Immagini di esempio che illustrano l'utilizzo dei dati dell’offerta
10. Metadati di Input/Output per ogni servizio all'interno di offerta hello
11. Condizioni di utilizzo dell'offerta
12. Anteprima dei dati dell'offerta hello

Infine, controllare il servizio hello funzionerà tramite hello Datamarket facendo clic sul collegamento hello "Esplora set di dati".  Verrà aperta una nuova finestra dello strumento hello è chiamare "Service Explorer" in modo che è possibile visualizzare l'anteprima risultati hello di una query per il servizio.  In questa finestra, è possibile immettere hello parametri necessari e visualizzare i risultati di hello visualizzati da una query sul servizio.   Inoltre, visualizzato è hello URL per la Query.  

> [!NOTE]
> Impossibile verificare tooreview hello descrizione testuale del servizio hello visualizzato nella parte superiore di hello.  E se l'offerta è costituito da più di un servizio di chiamata, fare clic sulle schede hello in hello inferiore tooswitch toohello successivo servizio tooreview e al test.
> 
> 

## <a name="next-step"></a>Passaggio successivo
Se si riscontrano problemi e serve assistenza per risolverli, contattare il [Supporto di pubblicazione di Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Se si è soddisfatti e toopublish pronto l'offerta leggere hello [richiesta approvazione tooPush tooProduction](marketplace-publishing-push-to-production.md) documentazione.

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: Come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)

