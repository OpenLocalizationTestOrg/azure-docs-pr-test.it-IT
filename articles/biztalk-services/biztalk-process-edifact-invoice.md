---
title: 'Esercitazione: Elaborare fatture EDIFACT con Servizi BizTalk di Azure | Documentazione Microsoft'
description: Come toocreate e configurare app casella connettore o l'API di hello e utilizzarlo in un'app di logica nel servizio App di Azure
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Esercitazione: Elaborare fatture EDIFACT con Servizi BizTalk di Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

È possibile utilizzare tooconfigure portale dei servizi BizTalk di hello e distribuire accordi X12 ed EDIFACT. In questa esercitazione, verranno esaminate come toocreate un accordo EDIFACT per lo scambio di fatture tra partner commerciali. L'esercitazione è relativa a una soluzione aziendale end-to-end che coinvolge due partner commerciali, Northwind e Contoso, che si scambiano messaggi EDIFAC.  

## <a name="sample-based-on-this-tutorial"></a>Esempio basato su questa esercitazione
Questa esercitazione è stata scritta su un esempio, **invio EDIFACT fatture mediante servizi BizTalk**, ovvero toodownload disponibile da hello [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005). È possibile utilizzare l'esempio hello e scorrere questa esercitazione toounderstand come hello è stato creato. O, è possibile usare questa esercitazione toocreate soluzione zero. In questa esercitazione è mirata secondo approccio hello in modo da comprendere come è stata compilata la soluzione. Inoltre, per quanto possibile, hello esercitazione è coerente con l'esempio hello e utilizza hello stessi nomi di elementi (ad esempio, schemi, trasformazioni) usati nell'esempio hello.  

> [!NOTE]
> Poiché questa soluzione prevede l'invio di un messaggio da un bridge EDI tooan bridge EAI, Riutilizza hello [esempio di concatenamento di Bridge di servizi di BizTalk](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) esempio.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Qual è la soluzione hello?
In questa soluzione Northwind riceve da Contoso fatture EDIFACT che non sono in un formato EDI standard. In tal caso, prima di inviare hello fattura tooNorthwind, deve essere trasformato tooan EDIFACT (nota anche come INVOIC) fattura. Al momento della ricezione, Northwind deve elaborare una fattura EDIFACT hello e restituire un tooContoso di messaggi (noto anche come CONTRL) del controllo.

![][1]  

tooachieve in questo scenario di business, Contoso Usa le funzionalità di hello fornite con i servizi BizTalk di Microsoft Azure.

* Contoso utilizza EAI Bridge tootransform hello originale fattura tooEDIFACT INVOIC.
* bridge EAI Hello invia quindi tooan messaggio hello di trasmissione EDI bridge distribuito come parte di un accordo configurato nel portale dei servizi BizTalk di hello.
* bridge di trasmissione EDI Hello elabora hello INVOIC EDIFACT e lo indirizza tooNorthwind.
* Dopo aver ricevuto la fattura hello, Northwind restituisce un toohello messaggio CONTRL di ricezione EDI distribuito come parte dell'accordo hello bridge.  

> [!NOTE]
> Facoltativamente, questa soluzione illustra anche come toouse batch toosend hello fatture in batch, anziché inviare separatamente ogni fattura.  
> 
> 

scenario di hello toocomplete, utilizziamo code del Bus di servizio toosend fattura da Contoso tooNorthwind o ricevere un acknowledgement da Northwind. Queste code possono essere create utilizzando un'applicazione client, che è disponibile come download ed è inclusa nel pacchetto di esempio hello che è disponibile come parte di questa esercitazione.  

## <a name="prerequisites"></a>Prerequisiti
* È necessario disporre di uno spazio dei nomi di bus di servizio. Per istruzioni sulla creazione di uno spazio dei nomi, vedere [Procedura: Creare o modificare uno spazio dei nomi del servizio del bus di servizio](https://msdn.microsoft.com/library/azure/hh674478.aspx). Si supponga di aver già effettuato il provisioning di uno spazio dei nomi di bus di servizio, denominato **edifactbts**.
* È necessario disporre di una sottoscrizione a Servizi BizTalk. Per le istruzioni, vedere [Creazione di servizi BizTalk tramite il portale di Azure](http://go.microsoft.com/fwlink/?LinkID=302280). Per questa esercitazione, si supponga di avere una sottoscrizione a Servizi BizTalk, denominata **contosowabs**.
* Registrare la sottoscrizione di servizi BizTalk nel portale dei servizi BizTalk di hello. Per istruzioni, vedere [la registrazione di una distribuzione del servizio BizTalk nel portale dei servizi BizTalk di hello](https://msdn.microsoft.com/library/hh689837.aspx)
* È necessario aver installato Visual Studio.
* È necessario aver installato BizTalk Services SDK. È possibile scaricare hello SDK da [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Passaggio 1: Creare hello code del Bus di servizio
Questa soluzione Usa il Bus di servizio accoda tooexchange i messaggi tra partner commerciali. Contoso e Northwind inviano messaggi toohello code da dove i bridge EAI e/o EDI hello li utilizzano. Per questa soluzione, sono necessarie tre code del bus di servizio:

* **northwindreceive** : Northwind riceve la fattura hello da Contoso tramite questa coda.
* **ContosoReceive** : Contoso riceve l'acknowledgement hello da Northwind tramite questa coda.
* **sospeso** – tutti i messaggi sospesi vengono indirizzati toothis coda. I messaggi vengono sospesi se presentano errori durante l'elaborazione.

È possibile creare le code del Bus di servizio tramite un'applicazione client inclusa nel pacchetto di esempio hello.  

1. Dal percorso di hello in cui è stato scaricato l'esempio hello, aprire **esercitazione l'invio di fatture utilizzando BizTalk Services EDI Bridges.sln**.
2. Premere **F5** toobuild e avviare hello **Tutorial Client** dell'applicazione.
3. Nella schermata di hello, immettere lo spazio dei nomi ACS di Bus di servizio di hello, nome dell'autorità emittente e chiave dell'autorità emittente.
   
   ![][2]  
4. Un messaggio informa che verranno create tre code nello spazio dei nomi del bus di servizio. Fare clic su **OK**.
5. Lasciare hello Tutorial Client è in esecuzione. Aprire hello, fare clic su **Bus di servizio** > ***lo spazio dei nomi del Bus di servizio*** > **code**e verificare che hello tre code siano state create.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Passaggio 2: creare e distribuire un contratto tra partner commerciali
Creare un accordo tra partner commerciali tra Contoso e Northwind. Un accordo tra partner commerciali definisce un contratto commerciale tra partner commerciali hello due, ad esempio quali toouse dello schema di messaggio, quali la messaggistica protocollo toouse e così via. Un accordo tra partner commerciali include due Bridge EDI, uno toosend messaggi tootrading partner (chiamato hello **bridge di invio EDI**) e uno tooreceive messaggi dai partner commerciali (denominato hello **bridge di ricezione EDI**).

Nel contesto di hello di questa soluzione, il bridge di trasmissione EDI hello corrisponde toohello lato invio dell'accordo hello e toosend utilizzati hello EDIFACT fattura da Contoso tooNorthwind. Analogamente, bridge di ricezione EDI hello corrisponde toohello sul lato di ricezione dell'accordo hello e viene utilizzato tooreceive acknowledgement da Northwind.  

### <a name="create-hello-trading-partners"></a>Creare i partner commerciali hello
toostart, creare i partner commerciali per Contoso e Northwind.  

1. Nel portale dei servizi BizTalk, di hello in hello **partner** scheda, fare clic su **Aggiungi**.
2. In hello pagina nuovo partner immettere **Contoso** come nome del partner e quindi fare clic su **salvare**.
3. Hello ripetere il passaggio toocreate hello secondo partner, **Northwind**.  

### <a name="create-hello-agreement"></a>Creare il contratto di hello
Gli accordi tra partner commerciali vengono creati tra i profili di business dei partner coinvolti. Questa soluzione Usa i profili di partner hello predefiniti che vengono creati automaticamente quando abbiamo creato i partner hello.  

1. Nel portale dei servizi BizTalk di hello, fare clic su **contratti** > **Aggiungi**.
2. In hello del nuovo accordo **impostazioni generali** pagina specificare i valori hello come illustrato nell'immagine di hello seguente e quindi fare clic su **continua**.
   
   ![][3]  
   
   Dopo avere fatto clic su **Continua**, diventano disponibili due schede, **Impostazioni di ricezione** e **Impostazioni di invio**.
3. Creare il contratto di invio hello tra Contoso e Northwind. Questo accordo definisce il modo in cui Contoso invia tooNorthwind di fattura EDIFACT hello.
   
   1. Fare clic su **Send Settings**.
   2. Mantenere i valori predefiniti di hello in hello **URL in ingresso**, **trasformare**, e **batch** schede.
   3. In hello **protocollo** scheda hello **schemi** sezione, caricare hello **EFACT_D93A_INVOIC.xsd** dello schema. Questo schema è disponibile con il pacchetto di esempio hello.
      
      ![][4]  
   4. In hello **trasporto** scheda, specificare i dettagli di hello per le code del Bus di servizio hello. Per contratto lato invio hello, utilizziamo hello **northwindreceive** coda toosend hello EDIFACT fattura tooNorthwind e hello **sospeso** coda di messaggi non riusciti durante l'elaborazione e vengono tooroute sospeso. È stato creato queste code in **passaggio 1: creare le code del Bus di servizio di hello** (in questo argomento).
      
      ![][5]  
      
      In **le impostazioni di trasporto > tipo di trasporto** e **impostazioni sospensione messaggi > tipo di trasporto**, selezionare il Bus di servizio di Azure e fornire i valori hello come illustrato nella figura hello.
4. Creare hello accordo tra Contoso e Northwind per la ricezione. Questo accordo definisce come Contoso riceve l'acknowledgement di hello da Northwind.
   
   1. Fare clic su **Receive Settings**.
   2. Mantenere i valori predefiniti di hello in hello **trasporto** e **trasformare** schede.
   3. In hello **protocollo** scheda hello **schemi** sezione, caricare hello **EFACT_4.1_CONTRL.xsd** dello schema. Questo schema è disponibile con il pacchetto di esempio hello.
   4. In hello **Route** scheda, creare un filtro tooensure che solo gli acknowledgement di Northwind sono tooContoso indirizzato. In **impostazioni Route**, fare clic su **Aggiungi** toocreate hello filtro di routing.
      
      ![][6]  
      
      1. Specificare i valori per **nome regola**, **regola Route**, e **destinazione Route** come illustrato nella figura hello.
      2. Fare clic su **Salva**.
   5. In hello **Route** nuovamente, specificare quale vengono instradati gli acknowledgement sospesi (riconoscimenti con esito negativo durante l'elaborazione). Impostare tooAzure tipo di trasporto hello Bus di servizio, tipo di destinazione route troppo**coda**, il tipo di autenticazione è troppo**firma di accesso condiviso** (SAS), specificare relativa stringa di connessione hello per hello Bus di servizio spazio dei nomi, quindi immettere come nome della coda hello **sospeso**.
5. Infine, fare clic su **Distribuisci** contratto hello toodeploy. Gli endpoint di hello nota in cui hello inviare e ricevere i contratti vengono distribuiti.
   
   * In hello **impostazioni di invio** scheda **URL in ingresso**, notare hello endpoint. toosend un messaggio da Contoso tooNorthwind utilizzando hello bridge di trasmissione EDI, è necessario inviare un endpoint toothis del messaggio.
   * In hello **impostazioni di ricezione** scheda **trasporto**, notare hello endpoint. bridge di ricezione toosend un messaggio da Northwind tooContoso utilizzando hello EDI, è necessario inviare un endpoint toothis del messaggio.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Passaggio 3: Creare e distribuire il progetto di servizi BizTalk di hello
Nel passaggio precedente hello è distribuito hello EDI inviare e ricevere le fatture EDIFACT tooprocess di contratti e riconoscimenti. Questi accordi possono elaborare solo messaggi conformi toohello schema del messaggio EDIFACT standard. Tuttavia, per ogni scenario hello per questa soluzione, Contoso invia un tooNorthwind fattura in uno schema proprietario interno. In tal caso, prima che il messaggio hello viene inviato toohello bridge di trasmissione EDI, devono essere trasformato da hello schema interne toohello schema EDIFACT standard fattura. progetto EAI servizi BizTalk di Hello vengono eseguite.

progetto di servizi BizTalk di Hello, **InvoiceProcessingBridge**, che le trasformazioni hello messaggio è anche inclusa come parte dell'esempio hello è stato scaricato. progetto Hello include hello seguenti elementi:

* **INHOUSEINVOICE. XSD** : Schema della fattura interna hello inviato tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** : Schema della fattura EDIFACT standard hello.
* **EFACT_4.1_CONTRL. XSD** : Schema di riconoscimento EDIFACT hello che Northwind invia tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** : hello trasformazione che esegue il mapping hello in-House invoice schema toohello schema EDIFACT standard fattura.  

### <a name="create-hello-biztalk-services-project"></a>Creare il progetto di servizi BizTalk di hello
1. In hello soluzione di Visual Studio, espandere progetto InvoiceProcessingBridge hello e quindi aprire hello **MessageFlowItinerary.bcs** file.
2. Fare clic in un punto qualsiasi nell'area di disegno hello e impostare hello **URL del servizio BizTalk** hello toospecify casella proprietà il nome della sottoscrizione dei servizi BizTalk. ad esempio `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Dalla casella degli strumenti hello, trascinare un **Bridge Xml unidirezionale** toohello area di disegno. Set hello **nome entità** e **indirizzo relativo** le proprietà di hello bridge troppo**ProcessInvoiceBridge**. Fare doppio clic su **ProcessInvoiceBridge** tooopen superficie di configurazione del bridge hello.
4. All'interno di hello **tipi di messaggio** fare clic su hello segno più (**+**) dello schema di hello toospecify pulsante del messaggio in ingresso. Poiché il messaggio in ingresso hello per hello bridge EAI è sempre in-House invoice hello, impostare questo troppo**INHOUSEINVOICE**.
   
   ![][8]  
5. Fare clic su hello **Xml Transform** forma, hello proprietà e nella casella per hello **mappe** proprietà, fare clic sui puntini di sospensione hello (**...** ) pulsante. In hello **selezione mappe** la finestra di dialogo, seleziona hello **INHOUSEINVOICE_to_D93AINVOIC** trasformare il file e quindi fare clic su **OK**.
   
   ![][9]  
6. Tornare indietro troppo**MessageFlowItinerary.bcs**, trascinarlo dalla casella degli strumenti hello, un **Endpoint di servizio esterno bidirezionale** toohello diritto di hello **ProcessInvoiceBridge**. Impostare il relativo **nome entità** proprietà troppo**EDIBridge**.
7. In Esplora soluzioni hello, espandere hello **MessageFlowItinerary.bcs** fare doppio clic su hello **Edibridge** file. Sostituire il contenuto di hello hello **Edibridge** con seguenti hello.
   
   > [!NOTE]
   > Motivo per cui sono file con estensione config tooedit hello? endpoint del servizio esterno Hello che abbiamo aggiunto toohello canvas di progettazione bridge rappresenta i bridge EDI hello distribuiti in precedenza. I bridge EDI sono bidirezionali, con un lato invio e un lato ricezione. Tuttavia, hello bridge EAI, che è stato aggiunto di progettazione del bridge toohello è un bridge unidirezionale. In tal caso, toohandle hello diversi modelli di scambio messaggi di due Bridge hello, utilizziamo un comportamento di bridge personalizzato includendo la configurazione nel file hello. config. Inoltre, un comportamento personalizzato hello gestisce inoltre l'endpoint del bridge trasmissione EDI toohello autenticazione hello. Questo comportamento personalizzato è disponibile come esempio separato in [esempio - tooEDI EAI di concatenamento di Bridge di servizi di BizTalk](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Questa soluzione riusa l'esempio hello.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Aggiornare i dettagli di configurazione tooinclude file Edibridge hello
   
   * In  *<behaviors>* , fornire hello spazio dei nomi ACS e chiave associata a hello sottoscrizione dei servizi BizTalk.
   * In  *<client>* , forniscono hello endpoint in cui viene distribuito l'accordo di trasmissione EDI hello.
   
   Salvare le modifiche e chiudere il file di configurazione di hello.
9. Dalla casella degli strumenti hello, fare clic su hello **connettore** e hello join **ProcessInvoiceBridge** e **EDIBridge** componenti. Selezionare il connettore hello e nella finestra Proprietà impostare **condizione di filtro** troppo**trova tutte le corrispondenze**. In questo modo si garantisce che tutti i messaggi elaborati da hello bridge EAI vengono instradati bridge EDI toohello.
   
   ![][10]  
10. Salvare le modifiche toohello soluzione.  

### <a name="deploy-hello-project"></a>Distribuire il progetto hello
1. Nel computer in cui è stato creato il progetto di servizi BizTalk di hello hello scaricare e installare il certificato SSL hello per la sottoscrizione di servizi BizTalk. Da , in Servizi BizTalk fare clic su **Dashboard**, quindi su **Scarica certificato SSL**. Fare doppio clic sul certificato hello e seguire l'installazione di hello hello toocomplete prompt dei comandi. Assicurarsi di installare il certificato di hello in **autorità di certificazione radice attendibili** archivio certificati.
2. In Esplora soluzioni di Visual Studio, fare clic sul hello **InvoiceProcessingBridge** del progetto e quindi fare clic su **Distribuisci**.
3. Specificare i valori di hello, come illustrato nella figura hello e quindi fare clic su **Distribuisci**. È possibile ottenere le credenziali di hello ACS per i servizi BizTalk facendo **informazioni di connessione** dal dashboard servizi BizTalk di hello.
   
   ![][11]  
   
   Dal riquadro di output di hello, copiare hello endpoint in cui hello bridge EAI è distribuito, ad esempio, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. L'URL di questo endpoint sarà necessario più avanti.  

## <a name="step-4-test-hello-solution"></a>Passaggio 4: Testare la soluzione hello
In questo argomento, viene analizzato in che modo tootest hello soluzione utilizzando hello **Tutorial Client** applicazione fornito come parte dell'esempio hello.  

1. In Visual Studio, premere F5 toostart hello **Tutorial Client**.
2. schermata di Hello deve avere i valori di hello inseriti passaggio hello a cui è stato creato hello code del Bus di servizio. Fare clic su **Avanti**.
3. Nella finestra successiva hello, fornire le credenziali ACS per sottoscrizione dei servizi BizTalk e hello endpoint in cui EAI ed EDI (ricezione) sono distribuiti i Bridge.
   
   Endpoint del bridge EAI hello era stato copiato nel passaggio precedente hello. Per l'endpoint del bridge, di ricezione EDI nel portale dei servizi BizTalk di hello, passare toohello accordo > Impostazioni di ricezione > trasporto > Endpoint.
   
   ![][12]  
4. Nella finestra successiva hello in Contoso, fare clic su hello **invio fattura interna** pulsante. Nel File hello aprire la finestra di dialogo, aprire il file INHOUSEINVOICE.txt hello. Esaminare il contenuto di hello del file hello e quindi fare clic su **OK** fattura hello toosend.
   
   ![][13]  
5. In alcuni hello secondi Northwind riceve fatture. Fare clic su hello **Visualizza messaggio** fattura di hello toosee collegamento ricevuta da Northwind. Si noti come fattura hello ricevuta da Northwind è nello schema EDIFACT standard durante hello quello inviato da Contoso sono uno schema interno.
   
   ![][14]  
6. Selezionare la fattura hello e quindi fare clic su **Send Acknowledgement**. In hello della finestra di dialogo visualizzata notare interscambio hello che ID è lo stesso in hello ricevuto fattura e hello acknowledgement inviato. Fare clic su OK in hello **Send Acknowledgement** la finestra di dialogo.
   
   ![][15]  
7. In pochi secondi, acknowledgement hello è Contoso riceve correttamente.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Passaggio 5 (facoltativo): inviare le fatture EDIFACT in batch
I bridge EDI di Servizi BizTalk supportano anche l'invio in batch dei messaggi in uscita. Questa funzionalità è utile per i partner destinatari che preferiscono tooreceive un batch di messaggi (soddisfa un determinato criterio) anziché messaggi singoli.

l'aspetto più importante Hello quando si utilizzano batch è effettivo rilascio di hello del batch di hello, detto anche i criteri di rilascio hello. criteri di rilascio Hello possono basarsi su come partner di destinazione hello vuole tooreceive messaggi. Se è abilitato l'invio in batch, hello bridge EDI non invia toohello messaggio in uscita hello ricezione partner fino a quando non hello criteri di rilascio viene soddisfatto. Ad esempio, se si impostano criteri di invio in batch basati sul numero di messaggi, viene inviato un batch solo quando vengono raggruppati 'n' messaggi. I criteri di batch possono anche essere basati sul tempo e in questo caso un batch può ad esempio essere inviato ogni giorno a una determinata ora. In questa soluzione è provare il criterio basato sul numero di messaggi hello.

1. Nel portale dei servizi BizTalk di hello, fare clic su accordo hello creato in precedenza. Fare clic su Send Settings > Batch > Add Batch.
2. Come nome del batch immettere **InvoiceBatch**, specificare una descrizione, quindi fare clic su **Avanti**.
3. Specificare criteri di batch che definiscano quali messaggi devono essere raggruppati. In questa soluzione vengono raggruppati tutti i messaggi. In tal caso, selezionare l'opzione Usa definizioni avanzate hello e immettere **1 = 1**. Questa è una condizione che sarà sempre vera, quindi tutti i messaggi verranno raggruppati in un batch. Fare clic su **Avanti**.
   
   ![][17]  
4. Specificare criteri di rilascio del batch. Hello-elenco a discesa selezionare **MessageCountBased**e per **conteggio**, specificare **3**. Ciò significa che un batch di tre messaggi verrà inviato tooNorthwind. Fare clic su **Avanti**.
   
   ![][18]  
5. Rivedere il riepilogo di hello e quindi fare clic su **salvare**. Fare clic su **Distribuisci** contratto hello tooredeploy.
6. Tornare indietro toohello **Tutorial Client**, fare clic su **invio fattura interna**e seguire hello richieste toosend hello fattura. Si noterà che non riceve alcuna fattura su Northwind perché la dimensione del batch hello non viene soddisfatta. Ripetere questo passaggio altre due volte, in modo da avere tre messaggi di fattura inviati tooNorthwind. Ciò soddisfa i criteri di rilascio batch di 3 messaggi hello e dovrebbe essere una fattura presso Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

