---
title: Servizi BizTalk tooAzure App per la logica delle App aaaMove | Documenti Microsoft
description: Spostare o eseguire la migrazione di Azure BizTalk Services MABS tooLogic App
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Spostare da servizi BizTalk tooLogic App

Servizi BizTalk di Microsoft Azure (MABS) verrà ritirato. Utilizzare il tooAzure di soluzioni di integrazione MABS App per la logica di toomove in questo argomento. 

## <a name="overview"></a>Panoramica

Servizi BizTalk è costituito da due servizi secondari:

1.  Connessioni ibride di Servizi BizTalk di Microsoft
2.  Integrazione basata su bridge di EAI ed EDI

Se si sta cercando le connessioni ibride toomove, quindi [le connessioni ibride di servizio App di Azure](../app-service/app-service-hybrid-connections.md) descrive hello modifiche e funzionalità di questo servizio. Connessioni ibride di Azure sostituisce Connessioni ibride di Servizi BizTalk. Le connessioni ibride di Azure è disponibile con il servizio App di Azure e viene offerto con hello portale di Azure. Le connessioni ibride Azure fornisce anche un nuovo toomanage Hybrid Connection Manager esistente connessioni ibride di servizi BizTalk e hello di nuove connessioni ibride creati nel portale. Connessioni ibride di Servizio app di Azure è disponibile a livello generale.

Per EAI ed EDI basato su bridge l'integrazione, App per la logica è una sostituzione hello. Logica App offre che tutti hello stesse funzionalità di servizi BizTalk e altro ancora. Logica App disponibili a livello di cloud in base al consumo del flusso di lavoro e l'orchestrazione caratteristiche che consentono di tooquickly e compilare facilmente le soluzioni di integrazione complessi con un browser, oppure tramite strumenti in Visual Studio.

Hello nella tabella seguente fornisce un mapping di funzionalità di servizi BizTalk tooLogic app.

| Servizi BizTalk   | App per la logica            | Scopo                  |
| ------------------ | --------------------- | ---------------------------- |
| Connettore          | Connettore             | Invio e ricezione di dati   |
| Bridge             | App per la logica             | Processore di pipeline           |
| Fase di convalida     | Operazione di convalida XML      | Convalidare un documento XML rispetto a uno schema             |
| Fase di miglioramento       | Token dei dati      | Alzare di livello delle proprietà nei messaggi o per decisioni di routing             |
| Fase di trasformazione    | Operazione di trasformazione      | Convertire i messaggi XML da un formato tooanother             |
| Fase di decodifica       | Operazione di decodifica di file flat      | Eseguire la conversione da file flat tooXML             |
| Fase di codifica       |  Operazione di codifica di file flat      | Eseguire la conversione da file tooflat XML             |
| Controllo messaggi       |  Funzioni di Azure o App per le API      | Eseguire il codice personalizzato nelle integrazioni             |
| Azione di routing      |  Condizione o switch      | Route messaggi tooone di hello specificato connettori             |

Esistono diversi tipi di elementi in Servizi BizTalk.

## <a name="connectors"></a>Connettori
Connettori nei servizi BizTalk consentono toosend Bridge e ricevano dati, inclusi i bridge bidirezionali che abilitato le interazioni basate su HTTP richiesta/risposta. Nella logica di App, hello viene utilizzata la stessa terminologia. I connettori App per la logica servono hello stesso scopo e includere anche più di 140 in grado di connettersi tooa vasta gamma di tecnologie e servizi, sia in locale con hello Gateway dati locale (sostituendo hello servizio Adapter BizTalk utilizzato dai servizi di BizTalk) e nel cloud servizi SaaS e PaaS, ad esempio OneDrive, Office 365, Dynamics CRM e molto altro ancora.

Origini nei servizi BizTalk sono limitate tooFTP, SFTP e coda di Service Bus o sottoscrizione dell'argomento.

![](media/logic-apps-move-from-mabs/sources.png)

Ogni bridge dispone di un endpoint HTTP per impostazione predefinita, che è configurato con hello indirizzo di Runtime e le proprietà di hello indirizzo relativo del bridge hello. tooachieve hello stessa logica App utilizzare hello [richiesta e risposta](../connectors/connectors-native-reqres.md) azioni.

## <a name="xml-processing-and-bridges"></a>Bridge ed elaborazione XML
Un bridge nei servizi BizTalk è analoga tooa pipeline di elaborazione. Un bridge può richiedere i dati ricevuti da un connettore ed eseguire altre operazioni con i dati di hello, quindi inviarlo tooanother sistema. Logica App hello stesso supportando hello stessa interazione pipeline basato su schemi come servizi BizTalk e fornisce inoltre una serie di altri modelli di integrazione. Hello [Bridge XML di richiesta-risposta](https://msdn.microsoft.com/library/azure/hh689781.aspx) nei servizi BizTalk è noto come pipeline VETER composta da fasi che può essere:

* Convalidare
* Migliorare
* Trasformare
* Migliorare
* Indirizzare

Come mostrato nella seguente immagine hello, l'elaborazione di hello viene suddiviso tra richiesta e risposta e consente di controllare la richiesta hello e hello percorsi di risposta separatamente (ad esempio, con le mappe diverse per ogni):

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Inoltre, un bridge unidirezionale XML aggiunge le fasi di decodifica e codifica all'inizio di hello e alla fine dell'elaborazione e hello bridge pass-through contiene un'unica fase Enrich.

### <a name="message-processing-and-decodingencoding"></a>Elaborazione e codifica/decodifica del messaggio
Nei servizi BizTalk, ricevere i messaggi XML di tipi diversi e determinare hello schema corrispondente per il messaggio hello ricevuto. Questa operazione viene eseguita in hello **tipi di messaggio** fase di hello pipeline di elaborazione di ricezione. Quindi, hello fase decodifica Usa toodecode tipo di messaggio hello rilevato in base allo schema hello fornito. Se lo schema di hello è uno schema file flat, converte hello in arrivo flatfile tooXML. 

App per la logica offre funzionalità simili. Ricevere un file flat tramite una vasta gamma di protocolli diversi, utilizzando i trigger di connettore diversi hello (File System, FTP, HTTP e così via) e utilizzare hello [decodificare File Flat](../logic-apps/logic-apps-enterprise-integration-flatfile.md) azione tooconvert hello in arrivo dati tooXML. È possibile spostare gli schemi file flat esistenti direttamente toologic App senza richiedere una modifica e quindi caricare schemi tooyour Account di integrazione.

### <a name="validation"></a>Convalida
Dopo aver hello dati in entrata tooXML convertito (o se XML è stato ricevuto formato di messaggio hello), la convalida viene eseguita toodetermine se il messaggio hello rispetti tooyour uno schema XSD. toodo in App per la logica, utilizzare hello [convalida XML](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) azione. È possibile usare nuovamente hello stessi schemi dai servizi di BizTalk senza apportare modifiche.

### <a name="transform-messages"></a>Trasformare i messaggi
Nei servizi BizTalk, fase Transform hello converte un messaggio basato su XML formato tooanother. Questa operazione viene eseguita applicando una mappa, utilizzando BizTalk mapper basato su TRFM hello. Nella logica di App, il processo di hello è simile. azione di trasformazione Hello esegue una mappa dall'Account di integrazione. la differenza principale Hello è che mappe nella logica App sono in formato XSLT. XSLT include hello possibilità tooreuse esistente è già presente, incluse le mappe create per BizTalk Server che contengono i functoid XSLT. 

### <a name="routing-rules"></a>Regole di routing
Servizi BizTalk rende una decisione di routing su quali endpoint/connettore toosend dati in arrivo messaggi /. Hello possibilità tooselect uno di un numero di endpoint preconfigurati, è possibile utilizzare l'opzione di filtro di routing hello:

![](media/logic-apps-move-from-mabs/route-filter.png)

App per la logica offre funzionalità di logica più sofisticate grazie alla [condizione](../logic-apps/logic-apps-use-logic-app-features.md) e allo [switch](../logic-apps/logic-apps-switch-case.md), attivando il flusso di controllo e routing avanzato. La conversione dei filtri di routing in Servizi BizTalk si ottiene al meglio usando una **condizione** *se* ci sono solo due opzioni. Se ci sono più di due opzioni, usare uno **switch**.

### <a name="enrich"></a>Miglioramento
fase Enrich nei servizi BizTalk di elaborazione Hello aggiunge proprietà toohello il contesto del messaggio associato a dati hello ricevuti. Innalzamento di livello, ad esempio, un toouse di proprietà per il routing (illustrato di seguito) da una ricerca nel database o mediante l'estrazione di un valore utilizzando un'espressione XPath. Logica App offre accesso tooall dati contestuali output dai precedenti azioni, rendendo semplice tooreplicate hello stesso comportamento. Ad esempio, usando hello `Get Row` azione di connessione SQL, si restituisce i dati da un database di SQL Server e utilizzare i dati hello in un'azione di decisione per il routing. Analogamente, le proprietà nel Bus di servizio in ingresso dei messaggi in coda da un trigger sono indirizzabile, nonché tramite hello xpath del flusso di lavoro definition language espressione XPath.

### <a name="use-custom-code"></a>Usare il codice personalizzato
Servizi BizTalk fornisce il possibilità hello troppo[eseguire codice personalizzato](https://msdn.microsoft.com/library/azure/dn232389.aspx) caricati in assembly personalizzati. Questa funzione è implementata hello [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interfaccia. Ogni fase del bridge hello include due proprietà (On Enter Inspector e On Exit Inspector) che forniscono tipo .net hello creato che implementa questa interfaccia. Codice personalizzato consente tooperform più complesso l'elaborazione in dati hello, nonché il riutilizzo del codice esistente nell'assembly che eseguono la logica di business comuni. 

Logica App offre due metodi principali codice personalizzato tooexecute: le funzioni di Azure e App per le API. È possibile creare le funzioni di Azure e richiamarle dalle app per la logica. Vedere [Aggiungere ed eseguire un codice personalizzato per le app per la logica di Azure tramite Funzioni di Azure](../logic-apps/logic-apps-azure-functions.md). Usare l'App per le API, parte del servizio App di Azure, toocreate trigger e azioni personalizzati. Altre informazioni, vedere [la creazione di un esempio di API personalizzata toouse con logica app](../logic-apps/logic-apps-create-api-app.md). 

Se si dispone di codice personalizzato in assmeblies che chiamano dai servizi di BizTalk, è possibile spostare questo codice tooAzure funzioni o creare API personalizzate con l'API app. a seconda di ciò che si sta implementando. Ad esempio, se si dispone di codice che esegue il wrapping di un altro servizio che la logica App non dispone di un connettore, quindi creare un'App per le API e utilizzare le azioni di hello che App per le API disponibili in un'app di logica. Se si dispone di funzioni di supporto o raccolte, le funzioni di Azure è probabilmente hello adatta.

### <a name="edi-processing-and-trading-partner-management"></a>Gestione del partner commerciale e dell'elaborazione di EDI
Servizi BizTalk include l'elaborazione EDI e B2B con supporto per AS2 (Applicability Statement 2), X12 ed EDIFACT. Lo stesso avviene per App per la logica. Nei servizi BizTalk, la creazione di Bridge EDI e creare o gestire i partner commerciali e contratti nel portale di gestione e rilevamento dedicato hello.

Nelle app di logica, questa funzionalità è inclusa in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). Si tratta di azioni di Account di integrazione e B2B hello per l'elaborazione EDI e B2B. Hello [Account integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) è toocreate utilizzato e gestire [i partner commerciali](../logic-apps/logic-apps-enterprise-integration-partners.md) e [contratti](../logic-apps/logic-apps-enterprise-integration-agreements.md). Dopo aver creato un Account di integrazione, è possibile associare uno o più account toohello apps di logica. Una volta associato, è possibile utilizzare hello B2B azioni tooaccess informazioni all'interno dell'app logica tra partner commerciali. viene fornita le seguenti azioni Hello:

* Codifica AS2
* Decodifica AS2
* Codifica X12
* Decodifica X12
* Codifica EDIFACT
* Decodifica EDIFACT

A differenza dei servizi BizTalk, queste azioni sono separate dai protocolli di trasporto hello. Quando si crea la logica App, è necessario maggiore flessibilità su quali connettori utilizzare toosend e ricevere dati. Ad esempio, è possibile tooreceive X12 file come allegati di posta elettronica e quindi elaborare questi file in un'app di logica. 

## <a name="manage-and-monitor"></a>Gestire e monitorare
Oltre alla gestione dei partner commerciali, hello dedicato portale per i servizi BizTalk fornito toomonitor funzionalità di rilevamento e risoluzione dei problemi. 

Logica App offre avanzati di rilevamento e monitoraggio delle funzionalità di hello [portale di Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md)e con hello [soluzione B2B Operations Management Suite](../logic-apps/logic-apps-monitor-b2b-message.md), ad esempio un'app per dispositivi mobili per tenere sotto controllo sugli elementi Quando ci si trova hello spostare.

## <a name="high-availability"></a>Disponibilità elevata
tooachieve disponibilità elevata (HA) nei servizi BizTalk, utilizzare più di un'istanza in un hello tooshare area determinato carico di elaborazione. Con le app per la logica, la disponibilità elevata in un'area è incorporata senza alcun costo aggiuntivo. Per il ripristino di emergenza al di fuori dell'area per l'elaborazione B2B in Servizi BizTalk, è necessario un processo di backup e ripristino. Nelle app di logica, un tra aree attiva/passiva [funzionalità di ripristino di emergenza](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) è fornito; che consente la sincronizzazione di hello dei dati B2B tra account di integrazione in aree diverse per la continuità aziendale.

## <a name="next"></a>Avanti
* [Informazioni sulle app per la logica](logic-apps-what-are-logic-apps.md)
* [Creare la prima app per la logica](logic-apps-create-a-logic-app.md), oppure iniziare rapidamente usando un [modello predefinito](logic-apps-use-logic-app-templates.md)  
* [Visualizza tutti i connettori disponibili di hello](../connectors/apis-list.md) è possibile utilizzare in un'app di logica
