---
title: aaaMicrosoft tooProvide ITFM per i clienti dell'utilizzo di Azure e RateCard API abilitare Cloudyn | Documenti Microsoft
description: "Offre una prospettiva univoca dal partner fatturazione di Microsoft Azure Cloudyn, nella sua esperienza l'integrazione di hello Azure fatturazione API nel prodotto.  Ciò è particolarmente utile per i clienti di Azure e Cloudyn che sono interessati a utilizzare/provare Cloudyn per Servizi di Azure."
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
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Utilizzo di Microsoft Azure e RateCard API abilitare Cloudyn tooProvide ITFM per i clienti
Cloudyn, un partner di sviluppo di Microsoft e un fornitore leader di funzionalità di gestione di cloud, è stato scelto per l'anteprima privata di hello nuovo RateCard APIs e utilizzo delle risorse di Microsoft Azure.  Hello utilizzo API fornisce accesso ai dati di utilizzo di Azure tooestimated per una sottoscrizione. Hello RateCard API fornisce informazioni sui prezzi complete di tutti i servizi di Azure, per i clienti non - Enterprise Agreement EA. Insieme, queste API forniscono una base di informazioni complete da inserire negli strumenti ITFM, ad esempio quelli forniti da Cloudyn.

## <a name="introduction"></a>Introduzione
Hello cosiddetta "moltiplicazione" di dati da hello API di utilizzo con i dati di hello API RateCard (prezzo di utilizzo [unità] [$unit] = dettagliate sull'utilizzo e i costi) Crea hello più granulare, accurato e affidabile le informazioni di fatturazione disponibili per Azure oggi.

![Panoramica su ITFM][1]

Utilizzo di queste API fornisce informazioni chiave sull'utilizzo dei clienti e i costi, consentire gli account dei clienti tooanalyze Cloudyn in un modo semplice e a livello di codice e tooperform diverse attività ITFM per i propri clienti.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Integrazione di Cloudyn con hello RateCard e le API di utilizzo
Hello RateCard API richiede diversi parametri di input, come info di area, valuta e delle impostazioni locali, ma più importante è OfferDurableID, che specifica il tipo di hello del cliente di hello offerte Azure utilizzato (legacy, pagamento 6 e 12 mesi impegno hello i piani, MSDN, le offerte MPN offerte, offerte promozionali e altri). Hello OfferDurableID è reperibile in hello [dell'utilizzo di Azure e il portale di fatturazione](https://account.windowsazure.com/Subscriptions), in hello "Offrono ID" per hello sottoscrizione specificata.

Al momento della registrazione per [Cloudyn per Azure](https://www.cloudyn.com/microsoft-azure/) services, è possibile aggiungere il codice OfferDurableID, che consente di Cloudyn toopull le informazioni sui prezzi rilevanti tramite hello RateCard API.  Informazioni sui diversi tipi di hello delle offerte disponibili uno hello [dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) pagina.

![Panoramica sul motore ITFM di Cloudyn][2]

Reporting, costo Cloudyn utilizza che entrambi hello informazioni sull'utilizzo e APIs RateCard, in aggiunta toohello prestazioni API di Azure, toocreate livelli aggiuntivi di visualizzazione, analitica, avvisi, gestione e i suggerimenti pratici, fornendo un affidabile ai clienti di Azure strumento ITFM di Enterprise cloud.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Casi di utilizzo di ITFM Cloudyn abilitati mediante l’integrazione delle API di utilizzo e RateCard
I casi di utilizzo di ITFM Cloudyn comuni abilitati mediante l’integrazione delle API di utilizzo e RateCard includono quelli indicati di seguito:

* **Analisi dei costi** -consente di cloud costi toobe ripartiti tooany nativo identificazione dimensione (provider, servizi, account, regione e così via). Hello dell'utilizzo di Azure e RateCard APIs semplificano queste un compito facile, fornendo suddivisione più granulare di hello dei dati di utilizzo e i costi per ogni account, che viene quindi raggruppate e filtrati in base Cloudyn e presentati toohello utente, sotto forma di grafico o tabulare.

![Grafico a torta sull’analisi dei costi][3]

* **Costo di allocazione 360** -Abilita finance e hello di toouncover ai responsabili IT effettivo costo scomposizione, i driver e le tendenze della loro distribuzione cloud. Ulteriormente consente ai gestori delle spese di distribuzione associati tooeasily con business unit, reparti, aree e altre informazioni, fornendo informazioni approfondite precedenti in costi di cloud e agevolare chargeback enterprise e showbacks. Hello dell'utilizzo di Azure e RateCard APIs fungono da Costo allocazione del motore del input tooCloudyn, che integra hello API tramite la definizione di metodi e logica di business per l'allocazione delle risorse non contrassegnate o untaggable.

![Grafico dell’allocazione costi a 360°][4]

* **Ridimensionamento a costi contenuti** -vengono forniti suggerimenti di ridimensionamento per le macchine virtuali sottoutilizzate, riducendo in tal modo le spese del cliente hello nei computer di dimensioni eccessive o provisioning eccessivo. Ciò avviene mediante l'esame delle metriche della CPU e della RAM (tramite API di prestazioni) delle macchine virtuali, delle ore di runtime (tramite le API di utilizzo) e dei costi (tramite le API RateCard). Cloudyn fornisce indicazioni di ottimizzazione in base alle risorse sottoutilizzate CPU o di RAM (prestazioni) e viene calcolato il risparmio stimato moltiplicando il delta di prezzo hello (RateCard) tra le macchine virtuali hello da hello ora-utilizzo effettivo (utilizzo) di hello computer sottoutilizzati.

![Ridimensionamento conveniente][5]

* **Suggerimenti relativi alla portabilità del cloud** : fornisce consigli finanziari sulla portabilità del cloud. Esamina i costi correnti di un utente di risorse cloud che vengono distribuiti sui fornitori principali di cloud e confronta il costo di toohello di una distribuzione equivalente in Azure. Fornisce quindi granulare, per ogni risorsa, finanziario basato su porting tooAzure indicazioni. Dopo avere valutato distribuzione equivalente di hello necessaria in Azure (in base alle preferenze dell'utente e le metriche delle prestazioni), Cloudyn Usa hello API RateCard tooevaluate hello costo distribuzione equivalente hello in Azure.
* **Report di prestazioni** -abilitata per le prestazioni di Azure API, questi report forniscono una matrice di funzionalità dell'utilizzo della CPU e RAM toooptimization indicazioni. Di seguito viene fornito un esempio di report di utilizzo dell’istanza, che presenta la suddivisione dell’istanza in base all'utilizzo medio della CPU.

![Report di prestazioni][6]

* **Gestione di categoria** -una potente funzionalità Cloudyn che consente di risorse cloud toounorganized. Fornisce agli utenti hello libertà toocreate categorie proprie univoci (tag) per misurare e i report che è in linea con le procedure aziendali efficace. Inoltre, gli utenti possono regolare facilmente e classificare i tag non coerenti (ad esempio errori di digitazione e altre discrepanze) e rilevare automaticamente le risorse senza tag per un’attribuzione accurata dei costi.

![Gestione delle categorie][7]

## <a name="video"></a>Video
Di seguito è riportato un breve video che illustra come un cliente di Azure possa utilizzare Cloudyn per Azure e hello fatturazione API di Azure, le informazioni toogain dai relativi dati di utilizzo di Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Avviare una liberazione [Cloudyn per Azure](https://www.cloudyn.com/microsoft-azure/) toosee valutazione come è possibile ottenere costi trasparenza con analitica per la distribuzione di cloud di Microsoft Azure e di creazione di report personalizzati.
* Vedere [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure](billing-usage-rate-card-overview.md) per una panoramica dell'utilizzo delle risorse di Azure hello e RateCard APIs.
* Estrarre hello [Azure fatturazione riferimento all'API REST](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) per ulteriori informazioni su entrambe le API che fanno parte del set di hello delle API fornite da hello Azure Resource Manager.
* Se si desidera toodive direttamente nel codice di esempio hello, consultare il nostro Microsoft Azure fatturazione API esempi di codice in [esempi di codice di Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Ulteriori informazioni
* toolearn informazioni sulle offerte di Microsoft Azure Enterprise Agreement (EA), visitare [licenze di Azure per hello Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) toolearn articolo ulteriori informazioni sulla hello Azure Resource Manager.
* Per ulteriori informazioni su suite hello degli strumenti spesa toohelp necessarie ad la comprensione del cloud, fare riferimento troppo articolo Gartner [mercato Guida per gli strumenti di gestione finanziaria IT (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
