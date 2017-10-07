---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Guida alla pubblicazione dei dati del servizio per hello Azure Marketplace
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners). Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Dopo aver completato il passaggio di hello 1, [la creazione di Account e la registrazione](marketplace-publishing-accounts-creation-registration.md), si è illustrate hello [generale tecnici](marketplace-publishing-pre-requisites.md) e [requisiti tecnici](marketplace-publishing-data-service-creation-prerequisites.md) di un servizio dati offrono in Azure Marketplace. Ora è verranno illustrati i passaggi di hello per la creazione di un'offerta di servizio dati su hello [portale pubblicazione] [ link-pubportal] per hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Account di accesso toohello portale di pubblicazione.
Andare troppo[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Per prima tooPublishing di account di accesso a tempo portale, utilizzare hello stesso account con cui profilo venditore della società è stato registrato nel centro per sviluppatori.**  (In un secondo momento è possibile aggiungere qualsiasi dipendente della società come co-amministratore in hello portale di pubblicazione).

Fare clic su hello **pubblicare un servizi dati** espansa se si tratta di account di accesso prima hello nel portale di pubblicazione hello.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Scegliere **Data Services** nel menu di navigazione hello sul lato sinistro hello.
  ![disegno](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Creare un nuovo servizio dati
Compilare per il nuovo servizio dati offrono titolo hello e fare clic su "+" su hello destra.

  ![disegno](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Sottomenu hello revisione in hello appena creata servizio dati in menu di navigazione hello.
Fare clic su hello **procedura dettagliata** scheda e di esaminare tutti i passaggi necessari esigenze toopublish hello correttamente il servizio dati su hello Azure Marketplace.

> [!TIP]
> È sempre possibile fare clic sui collegamenti hello nella pagina "Procedura dettagliata" hello o utilizzare schede di sottomenu dell'offerta di servizio dati hello sul lato sinistro di hello.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Creare un nuovo piano.
### <a name="offers-plans-transactions"></a>Offerte, piani, transazioni.
Ciascuna offerta può contenere più piani, tuttavia è necessario disporre di almeno un (1) piano. Quando gli utenti finali di eseguire la sottoscrizione tooyour offerta sottoscrivono un piano dell'offerta hello. Ogni piano definisce come gli utenti finali potrà essere in grado di toouse il servizio.

Attualmente Azure Marketplace supporta solo modello basato su transazioni di sottoscrizione mensile per i servizi dati, ad esempio gli utenti finali pagamento mensile in base a prezzo toohello del piano di hello specifico hanno eseguito la sottoscrizione tooand sarà in grado di tooconsume ogni numero di mese di transazione definito dal piano hello.

Ogni transazione, in genere definita come numero di record, che verrà restituito il servizio dati basato su query di hello inviato toohello servizio. valore predefinito di Hello è 100. Numero di transazioni restituiti tooeach query verrà numero di record diviso per 100 e arrotondato per eccesso toohello numero intero più vicino.

Si tratta del servizio di Azure Marketplace livello responsabilità toomonitor (misuratore) numero di transazioni utilizzato da ogni query.

> [!IMPORTANT]
> Gli utenti finali che ha raggiunto il limite di transazione hello durante il mese di hello non potranno continuare servizio hello toouse fino al termine del loro ciclo di sottoscrizione mensile.
> 
> Hello piano o uno dei piani di hello possibile (ma non necessario) includono un numero illimitato di transazioni.
> 
> 

### <a name="create-a-plan"></a>Creare un piano.
1. Fare clic su **"+"** toohello successivo "aggiungere un nuovo piano".
2. Scegliere una delle opzioni di hello: **Unlimited** o **limitato** utilizzo per questo piano.  Se Limited quindi fornire il numero di hello del piano di hello transazione consentirà tooconsume in un mese.
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Portale di pubblicazione verrà inoltre indicare "Identificatore del piano", che sarà utilizzato toocommunicate toohello gli utenti finali hello nome di piano hello hello dell'interfaccia utente e anche usato dai hello tooidentify di mercato servizio hello piano. Se si desidera, è possibile modificare hello "Identificatore del piano".
   
   > [!NOTE]
   > Hello "Identificatore del piano" deve essere univoco nell'ambito di hello di ogni offerta. Come molti altri identificatori nell'hello pubblicazione portale pianificare identificatore sarà bloccato dopo hello prima tooproduction di pubblicazione e non saranno più in grado di toochange questo identificatore.
   > 
   > 
3. Fare clic su tooaccept prescelto.
4. Verranno quindi poste alcune domande aggiuntive circa il piano appena creato.
   
    ![disegno](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Domanda | Significato |
| --- | --- |
| **Il piano è gratuito e disponibile tutto il mondo?** |È possibile creare un piano completamente gratuito. Se è hello prevede solo per questa offerta – significa che si sta pubblicando "Offrono libero" in hello Marketplace. Se è solo per un (numero) piano, hello consente di definire un toolearn gli utenti finali toooffer opzione ulteriori informazioni sul servizio con un numero relativamente ridotto di transazioni al mese.  Se la risposta hello è "Sì", non verranno richiesto alcun ulteriori domande. |

> [!NOTE]
> Gli utenti finali possono aggiornare sempre toohello a pagamento di piani.
> 
> 

| Domanda | Significato |
| --- | --- |
| **È disponibile una versione di prova gratuita?** |È possibile scegliere tra "Nessuna versione di valutazione" affatto o assegnare toouse un'opzione il piano per "Un mese". I server di pubblicazione, ad esempio toouse questa opzione tooprovide gli utenti finali hello possibilità toounderstand hello vantaggi di hello offrono gratuitamente per un mese. |

> [!IMPORTANT]
> Gli utenti finali saranno in grado di toopurchase una valutazione gratuita solo se hanno stabilito di pagamento, ad esempio carta di credito, contratto enterprise agreement.
> 
> Dopo un mese di valutazione gratuita di hello, Azure Marketplace inizierà ad addebitare i costi clienti prezzo hello data hello di sottoscrizione hello, a meno che il cliente hello avviata annullamento sottoscrizione hello. Non verranno fornito agli utenti finali toohello alcuna notifica speciale.
> 
> 

| Domanda | Significato |
| --- | --- |
| **Il piano è richiesto un toopurchase codice promozione?** |I server di pubblicazione hanno un tootheir di accesso toolimit opzione piani di servizio, fornendo un codice speciale, denominato "Un codice promozione" toospecific clienti. Solo gli utenti finali che conterrà il codice promozione sarà in grado di toosubscribe toohello piano. Se si sceglie "No", quindi si accetta che tutti gli utenti dall'area hello in hello offerta è disponibili (vedere [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) per altri dettagli) sarà in grado di toosubscribe toothis piano. Non verranno poste ulteriori domande. |
| **Nascondere anche il piano a tutti gli utenti che non dispongono di un codice di promozione valido?** |Se hello risposta toohello precedente domanda "Yes" hello, server di pubblicazione contiene toocompletely un'opzione rimuovere questo piano venga visualizzato nell'interfaccia utente di hello Marketplace hello. Significa che, i clienti non visualizzeranno il piano nella pagina dei dettagli dell'offerta hello. Gli utenti finali che riceveranno toopurchase un codice promozione, sarà in grado di toosubscribe tooit tramite questo codice promozione. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Creare contenuti di marketing di Marketplace
Per modalità tooprovide informazioni necessarie **Marketing, prezzi, supporto e le categorie** schede, visitare [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) che è comune tooall gli elementi pubblicati in hello Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Connettere il tooyour offerta di servizio (SQL Azure basato su o il servizio Web basato su).
Fare clic su hello **Data Services** sottomenu.

Nella parte superiore hello pagina hello verrà chiesto di offerta di hello tooprovide **Namespace**.  

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.png)

Hello seguito domanda definirà hello Publisher modalità tooexpose appena creati offerta tooAzure Marketplace. (Per ulteriori informazioni, vedere hello [Guida prerequisiti tecniche di Data Services](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Pubblicazione hello Database basato su servizio**

Fare clic su **Database**. verrà visualizzata la seguente pagina Hello:

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate un mapping di CSDL per hello set di dati in base hello database SQL di Azure:

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.4.png)

E quindi per ciascuna tabella

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.6.png)

Se il servizio Web

  ![disegno](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Lettura [Mapping esistente web servizio tooOData tramite CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) per istruzioni dettagliate ed esempi sulla creazione di un servizio Web di CSDL.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato l'offerta di servizio dati, assicurarsi di aver completato le istruzioni di hello in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) prima di spostare in avanti troppo[test il servizio dati in gestione temporanea](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: Come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)
* Se si è interessati alla comprensione hello l'intero processo di mapping di OData e lo scopo, leggere questo articolo [Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definizioni, strutture e le istruzioni.
* Se è interessati a learning e informazioni sui nodi specifici di hello e i relativi parametri, leggere questo articolo [nodi Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni, esempi e il contesto casi di utilizzo.
* Se si è interessati a esaminare alcuni esempi, leggere questo articolo [esempi di Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee codice di esempio e comprendere la sintassi di codice e il contesto.

[link-pubportal]:https://publish.windowsazure.com
