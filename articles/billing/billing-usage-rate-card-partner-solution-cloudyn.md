---
title: L'API di utilizzo e l'API RateCard di Microsoft Azure consentono a Cloudyn di fornire ITFM ai clienti | Documentazione Microsoft
description: "Fornisce un punto di vista unico del partner di fatturazione di Microsoft Azure, Cloudyn, sulle esperienze di integrazione delle API di fatturazione di Azure nel prodotto.  Ciò è particolarmente utile per i clienti di Azure e Cloudyn che sono interessati a utilizzare/provare Cloudyn per Servizi di Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: fac0ee2e9cbc87c8b3d04675551bba61f7a532b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-to-provide-itfm-for-customers"></a>L’API di utilizzo e l’API RateCard di Microsoft Azure Usage consentono a Cloudyn di fornire ITFM ai clienti
Cloudyn, partner di sviluppo Microsoft e fornitore leader di funzionalità di gestione del cloud, è stato scelto per un'anteprima privata delle nuove API di utilizzo delle risorse e RateCard di Microsoft Azure.  L'API di utilizzo fornisce l'accesso alle stime dei dati di consumo di Azure relative a una sottoscrizione. L'API RateCard fornisce informazioni complete sui prezzi di tutti i servizi di Azure per i clienti non EA. Insieme, queste API forniscono una base di informazioni complete da inserire negli strumenti ITFM, ad esempio quelli forniti da Cloudyn.

## <a name="introduction"></a>Introduzione
La cosiddetta "moltiplicazione" dei dati dell'API di utilizzo con i dati dall'API RateCard ([unità] di utilizzo price[$unit] = uso e costi dettagliati) consente oggi di creare informazioni di fatturazione più granulari, accurate e affidabili per Azure.

![Panoramica su ITFM][1]

L’utilizzo di queste API fornisce informazioni chiave sull'utilizzo e sui costi dei clienti, consentendo a Cloudyn di analizzare gli account dei clienti in modo semplice e a livello di codice, e di eseguire varie attività ITFM per i clienti.

## <a name="integrating-cloudyn-with-the-ratecard-and-usage-apis"></a>Integrazione di Cloudyn con API RateCard e API di utilizzo
L'API RateCard richiede diversi parametri di input, come informazioni relative all’area, alla valuta e alle impostazioni locali, ma il più importante è OfferDurableID, che consente di specificare il tipo di offerta Azure utilizzato dal cliente (pagamento in base al consumo, piani di impegno legacy di 6 e 12 mesi, offerte MSDN, offerte MPN, offerte promozionali e altre). Il parametro OfferDurableID è disponibile nel [portale di utilizzo e di fatturazione di Azure](https://account.windowsazure.com/Subscriptions), in "ID offerta" per una determinata sottoscrizione.

Al momento della registrazione ai servizi [Cloudyn per Azure](https://www.cloudyn.com/microsoft-azure/) , è possibile aggiungere il codice OfferDurableID, che consente a Cloudyn di estrarre le informazioni rilevanti sui prezzi tramite l'API RateCard.  Informazioni sui diversi tipi di offerte sono disponibili nella pagina [Dettagli delle offerte per Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) .

![Panoramica sul motore ITFM di Cloudyn][2]

Cloudyn utilizza sia le API di utilizzo, sia le API RateCard API oltre alle API di prestazioni di Azure, per creare livelli aggiuntivi di visualizzazione, analisi, avviso, creazione di report, gestione dei costi e suggerimenti applicabili, offrendo ai clienti di Azure uno strumento ITFM per il cloud aziendale affidabile.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Casi di utilizzo di ITFM Cloudyn abilitati mediante l’integrazione delle API di utilizzo e RateCard
I casi di utilizzo di ITFM Cloudyn comuni abilitati mediante l’integrazione delle API di utilizzo e RateCard includono quelli indicati di seguito:

* **Analisi dei costi** : consente di ripartire l'analisi dei costi del cloud nelle dimensioni identificative di origine (provider, servizio, account, area e così via). Le API di utilizzo e RateCard di Azure semplificano questo compito, fornendo la suddivisione più granulare dei dati di utilizzo e di costo per ogni account, che vengono quindi raggruppati e filtrati da Cloudyn e presentati all'utente in forma grafica o tabulare.

![Grafico a torta sull’analisi dei costi][3]

* **Allocazione dei costi a 360°** : consente ai responsabili IT e finanziari di individuare la scomposizione dei costi effettivi, i fattori di spinta e le tendenze della distribuzione cloud. Consente, inoltre, ai responsabili di associare facilmente i costi di distribuzione a business unit, reparti, aree e altro, fornendo informazioni dettagliate senza precedenti sui costi del cloud e agevolando showback e chargeback aziendali. Le API di utilizzo e RateCard di Azure servono da input al motore per l’allocazione dei costi di Cloudyn, che le completa definendo metodi e logica business per l'allocazione delle risorse senza tag o alle quali non è possibile aggiungere un tag.

![Grafico dell’allocazione costi a 360°][4]

* **Ridimensionamento economico** : fornisce consigli per il corretto dimensionamento delle macchine virtuali sottoutilizzate, riducendo in tal modo le spese del cliente relative a computer troppo grandi oppure con provisioning eccessivo. Ciò avviene mediante l'esame delle metriche della CPU e della RAM (tramite API di prestazioni) delle macchine virtuali, delle ore di runtime (tramite le API di utilizzo) e dei costi (tramite le API RateCard). Cloudyn fornisce quindi i consigli per il corretto dimensionamento in base alle risorse CPU o RAM sottoutilizzate (Prestazioni), ed esegue una stima dei risparmi moltiplicando il prezzo delta (RateCard) tra le macchine virtuali per il tempo di utilizzo effettivo (Uso) dei computer sottoutilizzati.

![Ridimensionamento conveniente][5]

* **Suggerimenti relativi alla portabilità del cloud** : fornisce consigli finanziari sulla portabilità del cloud. Esamina i costi correnti delle risorse cloud di un utente distribuiti sui principali fornitori cloud e li confronta con il costo di una distribuzione equivalente in Azure. Fornisce, quindi ad Azure suggerimenti sulla portabilità granulari, per risorsa, su base finanziaria. Dopo avere valutato la distribuzione equivalente necessaria in Azure (in base alle metriche delle prestazioni e alle preferenze dell’utente), Cloudyn utilizza l'API RateCard per valutare il costo della distribuzione equivalente in Azure.
* **Report di prestazioni** : abilitati dall’API delle prestazioni di Azure, questi report forniscono una gamma di funzionalità dall’utilizzo della CPU e della RAM ai suggerimenti per l’ottimizzazione. Di seguito viene fornito un esempio di report di utilizzo dell’istanza, che presenta la suddivisione dell’istanza in base all'utilizzo medio della CPU.

![Report di prestazioni][6]

* **Gestione delle categorie** : una potente funzionalità di Cloudyn che introduce l'ordine nelle risorse cloud non organizzate. Tale funzionalità fornisce agli utenti la libertà di creare categorie univoche (tag) per la misurazione effettiva e la creazione di report in linea con le procedure aziendali. Inoltre, gli utenti possono regolare facilmente e classificare i tag non coerenti (ad esempio errori di digitazione e altre discrepanze) e rilevare automaticamente le risorse senza tag per un’attribuzione accurata dei costi.

![Gestione delle categorie][7]

## <a name="video"></a>Video
Di seguito viene fornito un breve video in cui viene mostrato come un cliente di Azure può utilizzare Cloudyn e le API di fatturazione di Azure per ottenere approfondimenti utili sui dati consumo di Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Avviare una versione di valutazione gratuita di [Cloudyn per Azure](https://www.cloudyn.com/microsoft-azure/) per scoprire come ottenere la trasparenza dei costi grazie alla creazione di report e all’analisi personalizzate per la distribuzione cloud di Microsoft Azure.
* Per una panoramica sulle API di utilizzo delle risorse e sulle API RateCard di Azure, vedere [Ottenere informazioni significative sul consumo di risorse di Microsoft Azure](billing-usage-rate-card-overview.md) .
* Per ulteriori informazioni su entrambe le API, appartenenti al set di API fornito da Gestione risorse di Azure, vedere il [riferimento all'API REST di fatturazione di Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) .
* Se si desidera approfondire il codice di esempio, vedere gli esempi di codice dell'API di fatturazione di Microsoft Azure in [Esempi di codice di Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Ulteriori informazioni
* Per ulteriori informazioni sulle offerte relative al contratto di Microsoft Azure Enterprise, visitare [Licenze di Azure per l’azienda](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Per ulteriori informazioni su Gestione risorse di Azure, vedere l'articolo [Panoramica su Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) .
* Per altre informazioni sulla suite di strumenti necessari per conoscere la spesa relativa al cloud, fare riferimento all'articolo di Gartner sulla [Guida di mercato agli strumenti ITFM](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
