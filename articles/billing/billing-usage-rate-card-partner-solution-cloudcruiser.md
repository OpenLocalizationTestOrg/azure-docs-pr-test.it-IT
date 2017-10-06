---
title: aaaCloud Cruiser e integrazione di API di fatturazione di Microsoft Azure | Documenti Microsoft
description: "Offre una prospettiva univoca dal partner fatturazione di Microsoft Azure Cloud Cruiser, nella sua esperienza l'integrazione di hello Azure fatturazione API nel prodotto.  Ciò è particolarmente utile per i clienti di Azure e Cloud Cruiser che sono interessati a utilizzare/provare Cloud Cruiser per Microsoft Azure Pack."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Cloud Cruiser e integrazione delle API di fatturazione di Microsoft Azure
In questo articolo viene descritto come informazioni di hello raccolte da hello che fatturazione API di nuovo Microsoft Azure è utilizzabile nei Cloud Cruiser per flusso di lavoro costi simulazione e l'analisi.

## <a name="azure-ratecard-api"></a>API RateCard di Azure
Hello RateCard API fornisce informazioni sui tassi da Azure. Dopo l'autenticazione con credenziali appropriate hello, è possibile eseguire una query hello API toocollect metadati sui servizi hello disponibili in Azure, insieme ai tassi di hello associate con l'ID offerta.

Hello seguito è riportato un esempio di risposta dall'API di hello che mostra i prezzi di hello per hello A0 (Windows) istanza:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>Cloud tooAzure interfaccia del Cruiser API RateCard
Cloud Cruiser possono sfruttare informazioni RateCard API hello in modi diversi. Per questo articolo viene illustrato come può essere utilizzato toomake IaaS del carico di lavoro costo simulazione e analisi.

toodemonstrate in questo caso d'uso, si supponga un carico di lavoro di più istanze in esecuzione in Microsoft Azure Pack (WAP). obiettivo di Hello è toosimulate questo stesso carico di lavoro in Azure e stima dei costi di hello di eseguendo tale migrazione. In ordine toocreate la simulazione, esistono due toobe attività principali eseguite:

1. **Importazione e processo hello servizio informazioni raccolte da hello RateCard API.** Questa attività viene eseguita anche nelle cartelle di lavoro hello, in cui estratto hello hello RateCard API viene trasformato e pubblicati tooa nuovo piano di frequenza. Questo nuovo piano tariffario sarà utilizzato sui hello simulazioni tooestimate hello prezzi di Azure.
2. **Normalizzare i servizi WAP e i servizi di Azure per IaaS.** Per impostazione predefinita, i servizi WAP sono basati sulle singole risorse, come CPU, dimensioni della memoria, dimensioni del disco e così via, mentre i servizi di Azure si basano sulle dimensioni dell'istanza, come A0, A1, A2 e così via. Questa prima attività possono essere eseguite dal motore ETL del Cloud Cruiser, chiamato a cartelle di lavoro, in cui queste risorse possono essere combinate sulle dimensioni dell'istanza, analoga tooAzure istanza services.

### <a name="import-data-from-hello-ratecard-api"></a>Importare dati da hello RateCard API
Le cartelle di lavoro di cloud Cruiser informazioni un modo automatico toocollect e processo da hello RateCard API.  Le cartelle di lavoro ETL (extract-transform-load) consentono di raccolta hello tooconfigure, trasformazione e pubblicazione dei dati nel database Cloud Cruiser hello.

Ogni cartella di lavoro può avere uno o più raccolte, consentendo toocorrelate informazioni da origini diverse toocomplement o aumentare i dati di utilizzo hello. Hello seguenti due schermate Mostra come toocreate un nuovo *raccolta* in una cartella di lavoro e l'importazione di informazioni in hello *raccolta* da hello RateCard API:

![Figura 1 - Creazione di una nuova raccolta][1]

![Figura 2 - importazione dei dati dal nuovo insieme di hello][2]

Dopo aver importato dati hello nella cartella di lavoro hello, è possibile toocreate più passaggi e i processi di trasformazione, toomodify e modello di dati di hello. Per questo esempio, poiché si intende solo infrastructure-as-a-Service (IaaS), è possibile utilizzare hello trasformazione passaggi tooremove le righe non necessarie o record, correlate tooservices diverso da IaaS.

Hello schermata seguente mostra i passaggi di trasformazione hello utilizzati dati hello tooprocess raccolti dall'API RateCard:

![Figura 3 - trasformazione passaggi tooprocess raccolti dati dall'API RateCard][3]

### <a name="defining-new-services-and-rate-plans"></a>Definizione di nuovi servizi e piani tariffari
Nel Cloud Cruiser sono servizi toodefine modi diversi. Una delle opzioni di hello è servizi hello tooimport dai dati di utilizzo di hello. Questo metodo viene in genere utilizzato quando si lavora con i cloud pubblici, in servizi di hello sono già definiti dal provider di hello.

Un piano tariffario è un set di frequenze o prezzi che possono essere applicati toodifferent services, in base alle date di validità, o un gruppo di clienti, tra le altre opzioni. Piani tariffari possono anche essere usati in simulazione toocreate Cloud Cruiser o "" scenari di simulazione, toounderstand come modifiche apportate ai servizi possono influire sul costo totale di hello di un carico di lavoro.

In questo esempio, si utilizzerà le informazioni sui servizi hello da nuovi servizi toodefine RateCard API hello nel Cloud Cruiser. In hello stesso modo, è possibile utilizzare i tassi di hello associati toohello toocreate un nuovo piano tariffario nel Cloud Cruiser dei servizi.

Alla fine di hello del processo di trasformazione hello, è possibile toocreate un nuovo passaggio e pubblicare i dati di hello di hello RateCard API come tariffe e nuovi servizi.

![Figura 4 - pubblicano i dati di hello di hello RateCard API come nuovi servizi e velocità][4]

### <a name="verify-azure-services-and-rates"></a>Verificare i servizi e i costi di Azure
Dopo la pubblicazione di servizi di hello e di tariffe, è possibile verificare l'elenco di hello dei servizi del Cloud Cruiser importati *servizi* scheda:

![Figura 5 - verifica hello nuovi servizi][5]

In hello *frequenza piani* scheda, è possibile controllare piano tariffario nuovo hello chiamato "AzureSimulation" con frequenze di hello importati da hello RateCard API.

![Figura 6 - verifica hello frequenza nuovo piano e tariffe associati][6]

### <a name="normalize-wap-and-azure-services"></a>Normalizzare i servizi WAP e Azure
Per impostazione predefinita, WAP fornisce informazioni sull'utilizzo in base all'utilizzo di hello di calcolo, memoria e risorse di rete. Nel Cloud Cruiser, è possibile definire l'allocazione hello direttamente su servizi in base o a consumo dell'utilizzo di queste risorse. Ad esempio, è possibile impostare una frequenza di base per ogni ora di utilizzo della CPU o addebito hello GB di memoria allocata tooan istanza.

Per questo esempio, i costi di toocompare ordine tra WAP e Azure, è necessario tooaggregate hello utilizzo delle risorse WAP in bundle, che possono essere mappate tooAzure servizi. Questa trasformazione può essere implementata facilmente nelle cartelle di lavoro hello:

![Figura 7 - trasformazione dei servizi di toonormalize dati WAP][7]

ultimo passaggio di Hello nella cartella di lavoro hello è dati hello toopublish nel database Cloud Cruiser hello. Durante questo passaggio, i dati di utilizzo di hello vengano ora inseriti in servizi (che eseguono il mapping toohello servizi di Azure) e gli addebiti di hello toodefault tariffe toocreate associato.

Dopo la cartella di lavoro hello completamento, è possibile automatizzare l'elaborazione di hello dei dati di hello, aggiunta di un'attività nell'utilità di pianificazione hello e specificando la frequenza di hello e l'ora di hello toorun di cartella di lavoro.

![Figura 8 - Pianificazione della cartella di lavoro][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Creare report per l'analisi di simulazione dei costi del carico di lavoro
Dopo l'utilizzo di hello raccolte e gli addebiti vengono caricati nel database Cloud Cruiser hello, è possibile sfruttare tutte hello Cloud Cruiser Insights modulo toocreate hello del carico di lavoro costo simulazione che si desidera.

Negli ordini toodemonstrate questo scenario, sono stati creati hello seguenti report:

![Confronto dei costi][9]

Hello superiore mostra un confronto tra costi dai servizi, il confronto dei prezzi di hello del carico di lavoro hello in esecuzione per ogni servizio specifico tra WAP (blu scuro) e Azure (celeste).

grafico relativo alla parte inferiore Hello Mostra hello stessi dati ma suddiviso in base al reparto. Mostra i costi per ogni reparto di toorun hello relativo carico di lavoro WAP sia in Azure, insieme a differenza di hello tra di esse nella barra di risparmio hello (verde).

## <a name="azure-usage-api"></a>API di utilizzo di Azure
### <a name="introduction"></a>Introduzione
Microsoft ha introdotto di recente hello API di utilizzo di Azure, consentire ai sottoscrittori pull tooprogrammatically nell'utilizzo dei dati toogain approfondite consumo. Questa è una notizia eccezionale per i clienti di Cloud Cruiser che possono sfruttare hello più set di dati disponibili tramite questa API.

Cloud Cruiser può sfruttare l'integrazione di hello con hello API di utilizzo in diversi modi. granularità di Hello (informazioni sull'utilizzo di ogni ora) e informazioni sui metadati delle risorse disponibili tramite l'API fornisce hello hello set di dati necessarie toosupport flessibile Showback o Chargeback modelli. 

In questa esercitazione verrà presentata un esempio di come Cloud Cruiser possibile trarre vantaggio da hello informazioni sull'utilizzo API. In particolare, si verrà crea un gruppo di risorse in Azure, associare tag per la struttura dei conti hello, quindi descrivere hello processo di estrazione e l'elaborazione delle informazioni di tag hello in Cloud Cruiser.

obiettivo finale Hello è toobe toocreate in grado di report come segue quello hello e tooanalyze in grado di costo e consumo basati sulla struttura di account hello compilato da tag hello.

![Figura 10 - Report con suddivisioni usando i tag][10]

### <a name="microsoft-azure-tags"></a>Tag di Microsoft Azure
dati Hello disponibili tramite l'API di utilizzo di Azure hello includono non solo informazioni sul consumo, ma anche dei metadati delle risorse tra i tag associati. Tag forniscono tooorganize un modo semplice le risorse, ma in ordine toobe efficace, è necessario tooensure che:

* I tag sono risorse toohello correttamente applicati in fase di provisioning
* Tag correttamente vengono utilizzati nella struttura dei conti hello Showback/Chargeback processo tootie hello utilizzo toohello dell'organizzazione.

Entrambi questi requisiti può essere complessa, soprattutto quando un processo manuale nel provisioning hello o ad addebitare i costi collaterali. Tag errate, anche mancante o non corretto risultano segnalazioni più comuni dei clienti utilizzando tag e questi errori può semplificare su hello ad addebitare i costi collaterali molto difficile.

Con hello nuova API di utilizzo di Azure, Cloud Cruiser può estrarre informazioni di tag di risorse e tramite uno strumento ETL avanzato chiamato le cartelle di lavoro, correggere questi errori comuni di tag. Tramite la trasformazione utilizzando espressioni regolari e la correlazione dei dati, Cloud Cruiser può identificare risorse contrassegnate in modo non corretto e applicare tag corretta hello, assicurando l'associazione corretta delle risorse di hello hello con consumer hello.

Hello lato ad addebitare i costi, Cloud Cruiser automatizza hello Showback/Chargeback processo e può sfruttare hello tag informazioni tootie hello utilizzo toohello consumer appropriato (reparto, divisione, progetto e così via). Questa automazione offre un notevole miglioramento e può assicurare un processo di addebito coerente e controllabile.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Creazione di un gruppo di risorse con tag in Microsoft Azure
Hello primo passaggio in questa esercitazione è di un gruppo di risorse nel portale di Azure hello toocreate, quindi creare nuovi tag tooassociate toohello risorse. Per questo esempio, si creeranno hello tag seguenti: reparto, ambiente, proprietario, progetto.

Hello schermata riportata di seguito viene illustrato un esempio di che tag associate al gruppo di risorse con hello.

![Figura 11 - Gruppo di risorse con tag associati nel portale di Azure][11]

passaggio successivo Hello è toopull hello in informazioni provenienti da hello API utilizzo Cloud Cruiser. attualmente, Hello utilizzo API fornisce le risposte in formato JSON. Di seguito è riportato un esempio di hello dati recuperati:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Importare dati da hello utilizzo API in Cloud Cruiser
Le cartelle di lavoro di cloud Cruiser informazioni un modo automatico toocollect e processo da hello API di utilizzo. Una cartella di lavoro ETL (extract-transform-load) consente di raccolta hello tooconfigure, trasformazione e pubblicazione dei dati nel database Cloud Cruiser hello.

Ogni cartella di lavoro può contenere una o più raccolte. In questo modo toocorrelate informazioni da origini diverse toocomplement o estendere hello dati di utilizzo. Per questo esempio, si creerà un nuovo foglio nella cartella di lavoro modello Azure hello (*UsageAPI)* e impostare un nuovo *raccolta* tooimport informazioni da hello API di utilizzo.

![Figura 3 - i dati di utilizzo API importati nel foglio UsageAPI hello][12]

Si noti che questa cartella di lavoro già dispone di altri fogli tooimport servizi di Azure (*ImportServices*) ed elaborare le informazioni di utilizzo hello dall'API di fatturazione hello (*PublishData*).

Viene quindi utilizzata hello toopopulate API di utilizzo di hello *UsageAPI* foglio e correlare hello con i dati di utilizzo hello hello fatturazione API su hello *PublishData* foglio.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>L'elaborazione delle informazioni di tag hello da hello API di utilizzo
Dopo aver importato dati hello nella cartella di lavoro hello, verrà creata passaggi di trasformazione in hello *UsageAPI* foglio in tooprocess hello le informazioni sugli ordini hello API. Primo passaggio consiste toouse un hello tooextract di processore "Suddivisione JSON" tag da un singolo campo, quindi creare i campi per ognuno di essi (reparto, progetto, proprietario e ambiente).

![Figura 4: creare nuovi campi per informazioni sui tag hello][13]

Hello avviso "Rete" servizio mancano le informazioni di tag hello (casella di colore giallo), ma è possibile verificare che sia parte di hello stesso gruppo di risorse osservando hello *ResourceGroupName* campo. Poiché vi sono tag hello per hello altre risorse da questo gruppo di risorse, è possibile usare questo hello tooapply informazioni tag toothis risorsa in un secondo momento nel processo di hello mancante.

passaggio successivo Hello è toocreate una ricerca associazione hello informazioni sulla tabella da hello tag toohello *ResourceGroupName*. Questa tabella di ricerca verrà utilizzata in hello successivo passaggio tooenrich hello dati relativi al consumo con informazioni sui tag.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Aggiunta di dati di utilizzo di hello tag informazioni toohello
Ora verrà osservato toohello *PublishData* foglio, quali processi hello informazioni sul consumo di hello fatturazione API e aggiungono campi hello estratti dai tag hello. Questo processo viene eseguito analizzando hello tabella di ricerca creata nel passaggio precedente hello, utilizzando hello *ResourceGroupName* come chiave hello per le ricerche di hello.

![Figura 5 - popolando hello account struttura con le informazioni di hello di ricerche hello][14]

Si noti che sono stati applicati i campi di struttura hello account appropriato per il servizio "Rete" hello, correzione problema di hello con hello tag mancanti. È inoltre popolati i campi struttura degli account hello per le risorse diverso da questo gruppo di risorse di destinazione con "Altro", nell'ordine toodifferentiate su hello report.

Ora è sufficiente tooadd dati di utilizzo un passaggio toopublish hello. Durante questo passaggio, tassi di hello appropriati per ogni servizio definito in questo piano tariffario sarà applicato toohello informazioni sull'utilizzo con addebito di hello risultante caricato nel database di hello.

parte migliore Hello è che è sufficiente toogo tramite questo processo una volta. Al termine di cartella di lavoro hello, è sufficiente tooadd è toohello dell'utilità di pianificazione che verrà eseguito ogni ora o ogni giorno all'indirizzo hello ora pianificata. È quindi sufficiente di creazione di nuovi report o la personalizzazione di quelli esistenti, in ordine tooanalyze hello dati tooget informazioni significative dall'utilizzo del cloud.

### <a name="next-steps"></a>Passaggi successivi
* Per istruzioni dettagliate sulla creazione di cartelle di lavoro di Cloud Cruiser e i report, vedere tooCloud Cruiser del online [documentazione](http://docs.cloudcruiser.com/) (account di accesso valido richiesto).  Per altre informazioni su Cloud Cruiser, contattare [info@cloudcruiser.com](mailto:info@cloudcruiser.com).
* Vedere [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure](billing-usage-rate-card-overview.md) per una panoramica dell'utilizzo delle risorse di Azure hello e RateCard APIs.
* Estrarre hello [Azure fatturazione riferimento all'API REST](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) per ulteriori informazioni su entrambe le API che fanno parte del set di hello delle API fornite da hello Azure Resource Manager.
* Se si desidera toodive direttamente nel codice di esempio hello, consultare il nostro Microsoft Azure fatturazione API esempi di codice in [esempi di codice di Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Ulteriori informazioni
* Vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) toolearn articolo ulteriori informazioni sulla hello Azure Resource Manager.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figura 1 - Creazione di una nuova raccolta"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figura 2 - importazione dei dati dal nuovo insieme di hello"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figura 3 - trasformazione passaggi tooprocess raccolti dati dall'API RateCard"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figura 4 - pubblicano i dati di hello di hello RateCard API come nuovi servizi e velocità"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figura 5 - verifica hello nuovi servizi"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figura 6 - verifica hello frequenza nuovo piano e tariffe associati"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figura 7 - trasformazione dei servizi di toonormalize dati WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figura 8 - Pianificazione della cartella di lavoro"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figura 9 - Report di esempio per uno scenario di confronto dei costi di hello del carico di lavoro"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figura 10 - Report con suddivisioni usando i tag"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figura 11 - Gruppo di risorse con tag associati nel portale di Azure"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figura 12 - i dati di utilizzo API importati nel foglio UsageAPI hello"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figura 13 - creare nuovi campi per informazioni sui tag hello"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Nella figura 14 - popolando hello account struttura con le informazioni di hello di ricerche hello"
