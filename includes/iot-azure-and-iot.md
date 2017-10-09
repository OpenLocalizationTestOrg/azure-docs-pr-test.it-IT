
# <a name="azure-and-internet-of-things"></a>Azure e Internet delle cose

Benvenuti tooMicrosoft Azure e hello Internet delle cose (IoT). Questo articolo descrive un'architettura della soluzione IoT che descrive le caratteristiche comuni di hello di una soluzione IoT che è possibile distribuire servizi di Azure. Soluzioni di IoT richiedono sicura, la comunicazione bidirezionale tra i dispositivi, probabilmente la numerazione hello milioni e una soluzione di back-end. Ad esempio, una soluzione di back-end potrebbe utilizzare insights toouncover analitica predittiva, automatizzati dal flusso di eventi da dispositivo a cloud.

Azure IoT Hub è un componente essenziale quando si implementa questa architettura della soluzione IoT usando i servizi Azure. IoT Suite mette a disposizione implementazioni complete ed end-to-end di questa architettura per scenari IoT specifici. ad esempio:

* Hello *monitoraggio remoto* soluzione consente di stato di hello toomonitor dei dispositivi, ad esempio i distributori.
* Hello *manutenzione predittiva* soluzione consente di tooanticipate esigenze di manutenzione dei dispositivi, ad esempio pump stazioni di distribuzione remote e i tempi di inattività non pianificati tooavoid.
* Hello *factory connesso* soluzione consente di tooconnect e monitorare i dispositivi industriali.

## <a name="iot-solution-architecture"></a>Architettura della soluzione IoT

Hello seguente diagramma viene illustrato una tipico architettura della soluzione IoT. diagramma di Hello non include nomi di hello di servizi di Azure specifici, ma vengono descritti gli elementi chiave hello in un'architettura della soluzione IoT generico. In questa architettura, i dispositivi IoT raccolgono i dati che inviano tooa gateway del cloud. gateway del cloud Hello hello dati sono disponibili per l'elaborazione da altri servizi back-end in cui i dati vengono recapitati applicazioni line-of-business tooother o operatori toohuman tramite un dashboard o altro dispositivo di presentazione.

![Architettura della soluzione IoT][img-solution-architecture]

> [!NOTE]
> Per un'analisi approfondita dell'architettura di IoT, vedere hello [architettura di riferimento di Microsoft Azure IoT][lnk-refarch].

### <a name="device-connectivity"></a>Connettività dei dispositivi

In questa architettura della soluzione IoT, i dispositivi le inviano dati di telemetria, ad esempio la lettura dei sensori da una stazione di distribuzione, di un endpoint di cloud tooa per l'archiviazione e l'elaborazione. In uno scenario di manutenzione predittiva back-end di hello soluzione utile flusso hello del sensore dati toodetermine quando una specifica pump richiede attività di manutenzione. Dispositivi possono anche ricevere e rispondere messaggi toocloud nel dispositivo da cui leggere i messaggi da un endpoint di cloud. Ad esempio, nella soluzione di hello hello manutenzione predittiva scenario back-end potrebbe inviare messaggi pump tooother in hello distribuzione toobegin stazione reindirizzamento dei flussi, appena prima della scadenza manutenzione toostart. Questa procedura sarebbe assicurarsi tecnico della manutenzione hello potrebbe iniziare subito dopo aver raggiunto.

Una delle maggiori sfide hello affiancate IoT progetti come tooreliably e connettersi in modo sicuro i dispositivi toohello soluzione back-end. I dispositivi IoT hanno caratteristiche diverse, come client tooother confrontati, ad esempio i browser e App per dispositivi mobili. Dispositivi IoT:

* Sono spesso sistemi incorporati senza operatore umano.
* Possono essere distribuiti in località remote, dove l'accesso fisico è costoso.
* Può essere solo raggiungibile tramite hello soluzione back-end. Non vi è alcun altro toointeract modo con dispositivo hello.
* Possono avere risorse di alimentazione e di elaborazione limitate.
* Possono disporre di una connettività di rete intermittente, lenta o costosa.
* Potrebbe essere necessario toouse protocolli di applicazioni proprietarie, personalizzati o specifici del settore.
* Possono essere create utilizzando un'ampia gamma di piattaforme hardware e software molto comuni.

Inoltre toohello requisiti sopra riportati, qualsiasi soluzione IoT deve inoltre offrire scalabilità, sicurezza e affidabilità. Hello set risultante dei requisiti di connettività è difficile e lunga tooimplement utilizzando tecnologie tradizionali, ad esempio contenitori web e Broker di messaggistica. IoT Hub Azure e hello Azure IoT dispositivo SDK rendono più semplice soluzioni tooimplement che soddisfano questi requisiti.

Un dispositivo può comunicare direttamente con un endpoint di gateway del cloud o se il dispositivo hello è possibile utilizzare uno dei protocolli di comunicazione hello hello cloud gateway supporta, è possibile connettersi tramite un gateway intermedio. Ad esempio, hello [gateway del protocollo Azure IoT] [ lnk-protocol-gateway] possono eseguire conversione di protocollo, se i dispositivi non è possibile utilizzare uno dei protocolli hello che supporta l'IoT Hub.

### <a name="data-processing-and-analytics"></a>e analisi dei dati

Nel cloud hello, una soluzione di IoT back-end è in cui si verifica la maggior parte hello dell'elaborazione dei dati, ad esempio il filtro e l'aggregazione di dati di telemetria e del relativo routing tooother servizi. Hello IoT soluzione back-end:

* Riceve i dati di telemetria su larga scala dai dispositivi e determina la modalità tooprocess e archiviare i dati. 
* Può consentire i comandi toosend dal dispositivo di toospecific hello cloud.
* Fornisce funzionalità di registrazione dei dispositivi che consentono di tooprovision dispositivi e i dispositivi che sono consentiti infrastruttura tooyour tooconnect toocontrol.
* Abilita si tootrack hello lo stato dei dispositivi e monitorare le relative attività.

In caso di manutenzione predittiva hello, back-end di hello soluzione archivia i dati di telemetria cronologici. back-end di Hello soluzione è possibile utilizzare questo pattern tooidentify toouse di dati che indicano la manutenzione è su una data pump specifico.

Le soluzioni IoT possono includere cicli di feedback automatici. Ad esempio, un modulo analitica nel back-end di hello soluzione può identificare l'origine dati di telemetria di temperatura hello di un dispositivo specifico sopra normali livelli operativi. soluzione Hello può quindi inviare un dispositivo toohello comando, indicando l'azione correttiva tootake.

### <a name="presentation-and-business-connectivity"></a>Connettività aziendale e di presentazione

livello di connettività di presentazione e business Hello consente agli utenti finali di dispositivi di hello e toointeract con hello soluzione IoT. Consente gli utenti tooview e analizzare dati hello raccolti dai propri dispositivi. Queste viste possono richiedere modulo hello del dashboard o report di Business Intelligence che è possibile visualizzare sia i dati cronologici o in prossimità di dati in tempo reale. Ad esempio, un operatore può controllare hello stato della stazione di distribuzione specifico e vedere tutti gli avvisi generati dal sistema hello. Questo livello consente inoltre l'integrazione di hello IoT soluzione back-end con tootie applicazioni line-of-business esistenti in processi di business dell'organizzazione o flussi di lavoro. Ad esempio, soluzione manutenzione predittiva hello possibile integrare con un sistema di programmazione tale documentazione un toovisit engineer una stazione di distribuzione quando la soluzione hello identifica un pump che necessita di manutenzione.

![Dashboard della soluzione IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
