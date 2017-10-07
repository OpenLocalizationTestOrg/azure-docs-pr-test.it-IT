---
title: Glossario di IoT Hub aaaAzure | Documenti Microsoft
description: Guida per sviluppatori - un glossario dei termini comuni relativi tooAzure IoT Hub.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Glossario dei termini relativi all'hub IoT
Questo articolo vengono elencati alcuni dei termini comuni di hello usati in hello articoli IoT Hub.

## <a name="advanced-message-queueing-protocol"></a>Advanced Message Queueing Protocol
[Advanced Message Queuing Protocol (AMQP)](https://www.amqp.org/) è uno dei messaggi hello protocolli che [IoT Hub](#iot-hub) supporta per comunicare con dispositivi. Per ulteriori informazioni su hello IoT Hub supporta i protocolli di messaggistica, vedere [inviare e ricevere messaggi con l'IoT Hub](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
Hello [CLI di Azure](../cli-install-nodejs.md) è uno strumento di comando multipiattaforma, open source, basata su shell per la creazione e la gestione delle risorse in Microsoft Azure. Questa versione di hello CLI viene implementata con Node.js.

## <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0
Hello [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) è uno strumento di comando multipiattaforma, open source, basata su shell per la creazione e la gestione delle risorse in Microsoft Azure. Questa versione di anteprima di hello CLI viene implementata usando Python.


## <a name="azure-iot-device-sdks"></a>SDK dispositivo IoT Azure
Esistono _dispositivo SDK_ disponibile per più lingue che consentono di toocreate [App per dispositivi](#device-app) che interagiscono con un hub IoT. Hello IoT Hub le esercitazioni illustrano come toouse questi SDK di dispositivo. È possibile trovare il codice sorgente hello e altre informazioni sul dispositivo hello SDK in questa GitHub [repository](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
Bordo IoT consente applicazioni toowrite che consentono di dispositivi connessi al gateway toocommunicate con [IoT Hub](#iot-hub). Hello IoT Edge le esercitazioni illustrano come toouse questo servizio. È possibile trovare il codice sorgente hello e ulteriori informazioni su Azure IoT bordo in questo GitHub [repository](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>Azure IoT SDK per servizi
Esistono _service SDK_ disponibile per più lingue che consentono di toocreate [back-end app](#back-end-app) che interagiscono con un hub IoT. Hello IoT Hub le esercitazioni illustrano come questi toouse service SDK. È possibile trovare il codice sorgente hello e altre informazioni sul servizio hello SDK in questa GitHub [repository](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Portale di Azure
Hello [portale Microsoft Azure](https://portal.azure.com) è una posizione centrale in cui è possibile eseguire il provisioning e gestire le risorse di Azure. Organizza il contenuto usando i _pannelli_. In alcune delle esercitazioni di Hub IoT hello, potrebbe essere necessario hello toouse [portale di Azure classico](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) è una raccolta di cmdlet, è possibile utilizzare toomanage Azure con Windows PowerShell. Utilizzare toocreate cmdlet hello, testare, distribuire e gestire soluzioni e servizi messi a disposizione hello piattaforma Azure.

## <a name="azure-resource-manager"></a>Gestione risorse di Azure
[Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) consente toowork con risorse hello nella soluzione come gruppo. È possibile distribuire, aggiornare o eliminare le risorse di hello per la soluzione in un'operazione singola, coordinata.

## <a name="azure-service-bus"></a>Bus di servizio di Azure
[Bus di servizio](../service-bus/index.md) fornisce abilitata per il cloud di comunicazione con servizi di messaggistica aziendale e inoltrata la comunicazione che consente di connettersi soluzioni locali al cloud hello. Alcune esercitazioni sull'hub IoT usano le [code](../service-bus-messaging/service-bus-messaging-overview.md) del bus di servizio.

## <a name="azure-storage"></a>Archiviazione di Azure
[Archiviazione di Azure](../storage/common/storage-introduction.md) è una soluzione di archiviazione cloud. Include il servizio di archiviazione Blob hello che è possibile utilizzare toostore non strutturati dati dell'oggetto. Alcune esercitazioni su Hub IoT usano l'archivio BLOB.

## <a name="back-end-app"></a>App back-end
Nel contesto di hello di [IoT Hub](#iot-hub), un'applicazione back-end è un'app che si connette tooone di endpoint di servizio orientati hello in un hub IoT. Ad esempio, è possibile recuperare un'applicazione back-end [da dispositivo a cloud](#device-to-cloud)messaggi o gestire hello [Registro di sistema di identità](#identity-registry). In genere, un'applicazione back-end viene eseguito nel cloud di hello, ma in molti delle esercitazioni di hello hello back-end App sono applicazioni console in esecuzione nel computer di sviluppo locale.

## <a name="built-in-endpoints"></a>Endpoint predefiniti
Ogni hub IoT include un [endpoint](iot-hub-devguide-endpoints.md) predefinito compatibile con l'Hub eventi. È possibile utilizzare qualsiasi meccanismo che funziona con i messaggi da dispositivo a cloud tooread di hub eventi da questo endpoint.

## <a name="cloud-gateway"></a>Gateway cloud
Un gateway del cloud consente la connettività per i dispositivi che non è possibile connettersi direttamente troppo[IoT Hub](#iot-hub). Un gateway del cloud è ospitato nel cloud hello in contrasto tooa [gateway campo](#field-gateway) che esegue i dispositivi tooyour locale. Un caso di utilizzo tipico per un gateway del cloud è la conversione di protocollo tooimplement per i dispositivi.

## <a name="cloud-to-device"></a>Da cloud a dispositivo
Si riferisce toomessages inviati da un dispositivo di IoT hub tooa connesso. Spesso, questi messaggi sono comandi che comunicano hello dispositivo tootake un'azione. Per altre informazioni, vedere [Inviare e ricevere messaggi con l'hub IoT](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Stringa di connessione
Utilizzare le stringhe di connessione dell'app codice tooencapsulate hello informazioni necessarie tooconnect tooan endpoint. Una stringa di connessione include in genere indirizzo hello di endpoint hello e informazioni di sicurezza, ma la stringa di connessione formati possono variare tra servizi. Esistono due tipi di stringa di connessione associato al servizio IoT Hub hello:
- *Stringhe di connessione al dispositivo* abilitare gli endpoint che utilizzano il dispositivo di dispositivi tooconnect toohello in un hub IoT.
- *Le stringhe di connessione IoT Hub* abilitare gli endpoint orientati ai servizi di back-end App tooconnect toohello in un hub IoT.

## <a name="custom-endpoints"></a>Endpoint personalizzati
È possibile creare personalizzato [endpoint](iot-hub-devguide-endpoints.md) su un toodeliver hub IoT i messaggi inviati da un [regola di routing](#routing-rules). Endpoint personalizzati connettono direttamente tooan hub di eventi, una coda del Bus di servizio o un argomento del Bus di servizio.

## <a name="custom-gateway"></a>Gateway personalizzato
Un gateway consente la connettività per i dispositivi che non è possibile connettersi direttamente troppo[IoT Hub](#iot-hub). È possibile utilizzare [Azure IoT Edge](#azure-iot-edge) toobuild i gateway personalizzati che implementano la logica personalizzata toohandle messaggi, le conversioni di protocollo personalizzato e altri tipi di elaborazione su hello edge.

## <a name="data-point-message"></a>Messaggio di punto dati
Un messaggio di punto dati è un messaggio da [dispositivo a cloud](#device-to-cloud) contenente dati di [telemetria](#telemetry) come temperatura o velocità del vento.

## <a name="desired-configuration"></a>Configurazione desiderata
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), desired configuration fa riferimento toohello set completo di proprietà e metadati in un doppio dispositivo hello che deve essere sincronizzato con il dispositivo hello.

## <a name="desired-properties"></a>Proprietà desiderate
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), desiderato proprietà è una sottosezione di due dispositivi hello utilizzata con [segnalati proprietà](#reported-properties) toosynchronize configurazione del dispositivo o una condizione. Proprietà desiderate può essere impostata solo un [app back-end](#back-end-app) e vengono rispettate dalla hello [dispositivo app](#device-app).

## <a name="device-to-cloud"></a>Da dispositivo a cloud
Fa riferimento toomessages inviato da un dispositivo connesso[IoT Hub](#iot-hub). Questi messaggi potrebbero essere di [punto dati](#data-point-message) o [interattivi](#interactive-message). Per altre informazioni, vedere [Inviare e ricevere messaggi con l'hub IoT](iot-hub-devguide-messaging.md).

## <a name="device"></a>Dispositivo
Nel contesto di hello di IoT, un dispositivo è in genere un dispositivo di elaborazione autonomo su scala ridotta, che potrebbe raccogliere dati o per controllare altri dispositivi. Ad esempio, un dispositivo potrebbe essere un dispositivo di monitoraggio dell'ambiente o un controller per i sistemi nutrirli e ventilazione hello in un greenhouse. Hello [catalogo dispositivo](https://catalog.azureiotsuite.com/) fornisce un elenco di hardware toowork certificate di dispositivi con [IoT Hub](#iot-hub).

## <a name="device-app"></a>App per dispositivi
Un'app del dispositivo alimentato il [dispositivo](#device) e gli handle di hello la comunicazione con il [hub IoT](#iot-hub). In genere, si utilizza uno di hello [dispositivo IoT di Azure SDK](#azure-iot-device-sdks) quando si implementa un'app del dispositivo. In molte delle esercitazioni di IoT hello, utilizzare un [dispositivo simulato](#simulated-device) per motivi di praticità.

## <a name="device-condition"></a>Condizione del dispositivo
Fa riferimento a informazioni sullo stato toodevice, ad esempio il metodo di connettività hello attualmente in uso, come riportato da un [dispositivo app](#device-app). Le [app per dispositivi](#device-app) possono anche segnalare le loro stesse funzionalità. È possibile cercare le informazioni sulla condizione e sulle funzionalità usando i dispositivi gemelli.

## <a name="device-data"></a>Dati del dispositivo
I dati del dispositivo fa riferimento a dati per ogni dispositivo toohello archiviati in hello IoT Hub [Registro di sistema di identità](#identity-registry). È possibile tooimport ed esportare i dati.

## <a name="device-explorer"></a>Esplora dispositivi
Hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) è uno strumento che viene eseguito in Windows e consente di toomanage i dispositivi in hello [Registro di sistema di identità](#identity-registry).hello strumento può inoltre inviare e ricevere i dispositivi tooyour messaggi.

## <a name="device-identities-rest-api"></a>API REST per le identità dei dispositivi
Hello [API REST di identità dispositivo](https://docs.microsoft.com/rest/api/iothub/iothubresource) consente i dispositivi registrati in hello toomanage [Registro di sistema di identità](#identity-registry) utilizzando un'API REST. In genere, è necessario utilizzare uno di livello superiore di hello [service SDK](#azure-iot-service-sdks) come illustrato nell'hello esercitazioni IoT Hub.

## <a name="device-identity"></a>Identità del dispositivo
identità del dispositivo Hello è hello identificatore univoco assegnato tooevery dispositivo registrato in hello [Registro di sistema di identità](#identity-registry).

## <a name="device-management"></a>Gestione dei dispositivi
Gestione dei dispositivi include hello intero ciclo di vita associato alla gestione dei dispositivi hello nella soluzione IoT inclusi pianificazione, provisioning, la configurazione, monitoraggio e disattivato.

## <a name="device-management-patterns"></a>Modelli di gestione dei dispositivi
L'[hub IoT](#iot-hub) abilita modelli di gestione dei dispositivi comuni, inclusi riavvio, esecuzione di ripristini delle impostazioni predefinite ed esecuzione di aggiornamenti del firmware nei dispositivi.

## <a name="device-messaging-rest-api"></a>API REST per la messaggistica dei dispositivi
È possibile utilizzare hello [dell'API REST di messaggistica dispositivo](https://docs.microsoft.com/rest/api/iothub/httpruntime) da un dispositivo messaggi hub IoT tooan toosend dispositivo a cloud e di ricezione [cloud a dispositivo](#cloud-to-device) messaggi da un hub IoT. In genere, è necessario utilizzare uno di livello superiore di hello [dispositivo SDK](#azure-iot-device-sdks) come illustrato nell'hello esercitazioni IoT Hub.

## <a name="device-provisioning"></a>Provisioning di dispositivi
Provisioning del dispositivo è il processo di hello di aggiunta iniziale hello [i dati del dispositivo](#device-data) toohello archivia nella soluzione. tooenable un nuovo hub tooyour tooconnect di dispositivo, è necessario aggiungere un dispositivo ID e le chiavi toohello IoT Hub [Registro di sistema di identità](#identity-registry). Come parte del processo di provisioning hello, potrebbe essere necessario tooinitialize di dati specifico del dispositivo in altri archivi di soluzione.

## <a name="device-twin"></a>Dispositivo gemello
Un [dispositivo gemello](iot-hub-devguide-device-twins.md) è un documento JSON nel quali vengono archiviate informazioni sullo stato dei dispositivi, ad esempio metadati, configurazioni e condizioni. [Hub IoT](#iot-hub) rende permanente un dispositivo gemello per ogni dispositivo di cui viene effettuato il provisioning nell'hub IoT. Gemelli di dispositivo consentono di toosynchronize [condizioni dispositivo](#device-condition) e delle configurazioni tra il dispositivo di hello e soluzione hello back-end. È possibile eseguire query gemelli toolocate specifici dispositivi e query sullo stato di hello di operazioni a esecuzione prolungata.

## <a name="device-twin-queries"></a>Query del dispositivo gemello
[Le query doppi dispositivo](iot-hub-devguide-query-language.md) hello IoT Hub simile a SQL query language tooretrieve da utilizzare le informazioni gemelli del dispositivo. È possibile utilizzare hello stessa IoT Hub query informazioni relative alla lingua tooretrieve su [processi](#job) in esecuzione nell'hub IoT.

## <a name="device-twin-rest-api"></a>API REST dei dispositivi gemelli
È possibile utilizzare hello [API REST di dispositivo doppi](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) dalla soluzione hello back-end toomanage gemelli del dispositivo. Hello API consente di aggiornamento e tooretrieve [doppi dispositivo](#device-twin) proprietà e richiamare [diretta metodi](#direct-method). In genere, è necessario utilizzare uno di livello superiore di hello [service SDK](#azure-iot-service-sdks) come illustrato nell'hello esercitazioni IoT Hub.

## <a name="device-twin-synchronization"></a>Sincronizzazione dei dispositivi gemelli
La sincronizzazione del dispositivo doppi utilizza hello [le proprietà desiderate](#desired-properties) nel tooconfigure gemelli dispositivo i dispositivi e recuperare [segnalati proprietà](#reported-properties) da toostore i dispositivi in un doppio dispositivo hello.

## <a name="direct-method"></a>Metodo diretto
Oggetto [metodo diretto](iot-hub-devguide-direct-methods.md) è un modo per si tootrigger tooexecute un metodo in un dispositivo chiamando un'API l'hub IoT.

## <a name="endpoint"></a>Endpoint
Un hub IoT espone più [endpoint](iot-hub-devguide-endpoints.md) che abilitano l'hub IoT toohello tooconnect l'app. Endpoint che utilizzano il dispositivo che consentono operazioni tooperform dispositivi, ad esempio l'invio di [da dispositivo a cloud](#device-to-cloud) messaggi e la ricezione [cloud a dispositivo](#cloud-to-device) messaggi. Sono disponibili endpoint di Gestione servizio Web che consentono di [back-end app](#back-end-app) tooperform operazioni, ad esempio [identità del dispositivo](#device-identity) gestione e la gestione dei dispositivi doppi. Esistono [endpoint incorporati](#built-in-endpoints) del servizio per leggere i messaggi da dispositivo a cloud. È possibile creare [endpoint personalizzati](#custom-endpoints) messaggi da dispositivo a cloud tooreceive inviati da un [regola di routing](#routing-rules).

## <a name="event-hubs-service"></a>Servizio Hub eventi
[Hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md) è un servizio altamente scalabile di ingresso dei dati tale che può inserire milioni di eventi al secondo. servizio Hello permette tooprocess e analizzare hello enormi quantità di dati prodotti da applicazioni e dispositivi connessi. Per un confronto con hello servizio IoT Hub, vedere [hub eventi di Azure e di confronto di IoT Hub Azure](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Endpoint compatibile con Hub eventi
tooread [da dispositivo a cloud](#device-to-cloud) i messaggi inviati tooyour IoT hub, è possibile connettersi endpoint tooan l'hub e utilizzare qualsiasi tooread metodo Hub eventi compatibile con i messaggi. I metodi compatibili con Hub eventi includono l'utilizzo di hello [SDK hub eventi](../event-hubs/event-hubs-programming-guide.md) e [Azure flusso Analitica](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Gateway sul campo
Un gateway campo consente la connettività per i dispositivi che non è possibile connettersi direttamente troppo[IoT Hub](#iot-hub) e viene in genere distribuito in locale con i dispositivi. Per altre informazioni, vedere [Che cos'è l'hub IoT di Azure?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Account gratuito
È possibile creare un [libero account Azure](https://azure.microsoft.com/pricing/free-trial/) toocomplete hello esercitazioni IoT Hub e sperimentare hello servizio IoT Hub (e altri servizi di Azure).

## <a name="gateway"></a>Gateway
Un gateway consente la connettività per i dispositivi che non è possibile connettersi direttamente troppo[IoT Hub](#iot-hub). Vedere anche [Gateway sul campo](#field-gateway), [Gateway cloud](#cloud-gateway) e [Gateway personalizzato](#custom-gateway).

## <a name="identity-registry"></a>Registro delle identità
Hello [Registro di sistema di identità](iot-hub-devguide-identity-registry.md) è consentito, componente incorporato di hello di un hub IoT che archivia le informazioni sui singoli dispositivi hello tooconnect tooan IoT hub.

## <a name="interactive-message"></a>Messaggio interattivo
Un messaggio interattivo è un [cloud a dispositivo](#cloud-to-device) messaggio che attiva un'azione immediata in hello soluzione back-end. Ad esempio, un dispositivo potrebbe inviare un avviso relativo a un errore che deve essere registrato automaticamente nel sistema CRM tooa.

## <a name="iot-hub"></a>Hub IoT
Hub IoT è un servizio completamente gestito di Azure che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Per altre informazioni, vedere [Che cos'è l'hub IoT di Azure?](iot-hub-what-is-iot-hub.md) Utilizzando il [sottoscrizione di Azure](#subscription), è possibile creare il IoT carichi di lavoro di messaggistica toohandle hub IoT.

## <a name="iot-hub-metrics"></a>Metriche di Hub IoT
[Le metriche di IoT Hub](iot-hub-metrics.md) fornisce i dati sullo stato di hello dell'hub IoT hello nel [sottoscrizione di Azure](#subscription). Abilitazione di metriche IoT Hub è tooassess hello integrità complessiva del servizio di hello e dispositivi hello connesso tooit. Le metriche di IoT Hub consentono di vedere cosa succede con l'hub IoT e analizzare i problemi di causa principale senza la necessità di toocontact supporto tecnico di Azure.

## <a name="iot-hub-query-language"></a>Linguaggio di query di Hub IoT
Hello [il linguaggio di query di IoT Hub](iot-hub-devguide-query-language.md) è un linguaggio simile a SQL che consente di tooquery il [processi](#job) e gemelli di dispositivo.

## <a name="iot-hub-resource-provider-rest-api"></a>API REST del provider di risorse dell'hub IoT
È possibile utilizzare hello [API REST del Provider di risorse Hub IoT](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage hello l'hub IoT consente nel [sottoscrizione di Azure](#subscription) eseguendo operazioni come la creazione, aggiornamento ed eliminazione di hub.

## <a name="iot-suite"></a>IoT Suite
Azure IoT Suite riunisce diversi servizi di Azure e soluzioni preconfigurate. Queste soluzioni preconfigurate abilitare tooget iniziare rapidamente con le implementazioni di end-to-end di scenari comuni di IoT. Per altre informazioni, vedere [Che cos'è Azure IoT Suite?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>iothub-explorer
Hello [l'hub IOT Esplora](https://github.com/azure/iothub-explorer) è uno strumento da riga di comando multipiattaforma. lo strumento Hello consente si toomanage i dispositivi in hello [Registro di sistema di identità](#identity-registry), inviare e ricevere messaggi e file dai dispositivi e monitorare le operazioni di hub IoT.

## <a name="job"></a>Job
La soluzione di back-end è possibile utilizzare [processi](iot-hub-devguide-jobs.md) tooschedule e tenere traccia di attività in un set di dispositivi registrati con l'hub IoT. Le attività includono l'aggiornamento delle [proprietà desiderate](#desired-properties) di un dispositivo gemello, l'aggiornamento dei [tag](#tags) di un dispositivo gemello e la chiamata di [metodi diretti](#direct-method). [IoT Hub](#iot-hub) Usa anche i processi troppo[importare esportazione tooand](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) da hello [Registro di sistema di identità](#identity-registry).

## <a name="jobs-rest-api"></a>API REST dei processi
Hello [API REST di processi](https://docs.microsoft.com/rest/api/iothub/jobapi) consente toomanage [processi](#job) in esecuzione nell'hub IoT.

## <a name="module"></a>Modulo
In [Azure IoT Edge](iot-hub-linux-iot-edge-get-started.md) un [modulo](iot-hub-linux-iot-edge-get-started.md) è un componente che esegue un'attività specifica. Attività includono l'inserimento di un messaggio da un dispositivo, la trasformazione di un messaggio o l'invio di un hub IoT tooan di messaggio. Un broker è responsabile dell'inoltro dei messaggi tra i moduli. Azure IoT Edge include un set di moduli di esempio. È anche possibile creare moduli personalizzati.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) è uno dei messaggi hello protocolli che [IoT Hub](#iot-hub) supporta per comunicare con dispositivi. Per ulteriori informazioni su hello IoT Hub supporta i protocolli di messaggistica, vedere [inviare e ricevere messaggi con l'IoT Hub](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Monitoraggio delle operazioni
IoT Hub [monitoraggio delle operazioni](iot-hub-operations-monitoring.md) consente lo stato di hello toomonitor delle operazioni l'hub IoT in tempo reale. L'[hub IoT](#iot-hub) tiene traccia degli eventi nelle diverse categorie di operazioni. È possibile scegliere di inviare gli eventi da uno o più categorie tooan endpoint IoT Hub per l'elaborazione. È possibile controllare i dati di hello per errori o impostare un'elaborazione più complessa basata su modelli di dati.

## <a name="physical-device"></a>Dispositivo fisico
Un dispositivo fisico è un dispositivo reale, ad esempio una Pi Raspberry che si connette tooan IoT hub. Per praticità, molte delle esercitazioni di Hub IoT hello utilizzare [simulato dispositivi](#simulated-device) tooenable si toorun esempi sul computer locale.

## <a name="primary-and-secondary-keys"></a>Chiavi primarie e secondarie
Quando ci si connette tooa che utilizzano il dispositivo o di un endpoint di servizio Web in un hub IoT, il [stringa di connessione](#connection-string) include toogrant chiave accesso. Quando si aggiunge un dispositivo toohello [Registro di sistema di identità](#identity-registry) o aggiungere un [criterio di accesso condiviso](#shared-access-policy) tooyour hub, servizio hello genera una chiave primaria e secondaria. Con due chiavi consente tooroll su da uno tooanother chiave quando si aggiorna una chiave senza perdere l'hub IoT toohello di accesso.

## <a name="protocol-gateway"></a>Gateway di protocollo
Un gateway di protocollo viene in genere distribuito nel cloud hello e fornisce servizi di traduzione per i dispositivi connessi troppo di protocollo[IoT Hub](#iot-hub). Per altre informazioni, vedere [Che cos'è l'hub IoT di Azure?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Quote e limitazioni
Esistono vari [quote](iot-hub-devguide-quotas-throttling.md) che si applicano tooyour ricorso [IoT Hub](#iot-hub), molti dei hello quote variano in base a livello di hello dell'hub IoT hello. [IoT Hub](#iot-hub) si applica anche [limita](iot-hub-devguide-quotas-throttling.md) tooyour utilizzo del servizio hello in fase di esecuzione.

## <a name="reported-configuration"></a>Configurazione segnalata
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), segnalati configurazione fa riferimento toohello l'intero set di proprietà e metadati in un doppio dispositivo hello che deve essere segnalati toohello soluzione back-end.

## <a name="reported-properties"></a>Proprietà segnalate
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), segnalato una sottosezione di hello gemelli di dispositivo utilizzato con proprietà [le proprietà desiderate](#desired-properties) toosynchronize configurazione del dispositivo o una condizione. Segnalato proprietà può essere impostata solo tramite hello [dispositivo app](#device-app) e può essere letto e verrà eseguita una query da un [app back-end](#back-end-app).

## <a name="resource-group"></a>Gruppo di risorse
[Gestione risorse di Azure](#azure-resource-manager) toogroup gruppi di risorse utilizza le risorse correlate. È possibile utilizzare contemporaneamente un operazioni tooperform gruppo di risorse in tutte le risorse hello nel gruppo di hello.

## <a name="retry-policy"></a>Criteri di ripetizione
Si utilizza un toohandle di criteri di ripetizione [errori temporanei](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) quando ci si connette il servizio di cloud tooa.

## <a name="routing-rules"></a>Regole di routing
Configurare [regole di routing](iot-hub-devguide-messages-read-custom.md) nei messaggi da dispositivo a cloud tooa di IoT hub tooroute [endpoint predefinito](#built-in-endpoints) o troppo[endpoint personalizzati](#custom-endpoints) per l'elaborazione da backup soluzione fine.

## <a name="sasl-plain"></a>SASL PLAIN
SASL normale è un protocollo che hello [AMQP](#advanced-message-queue-protocol) protocollo Usa il token di sicurezza di tootransfer.

## <a name="shared-access-signature"></a>Firma di accesso condiviso
Le firme di accesso condiviso sono un meccanismo di autenticazione basato su hash sicuri SHA-256 o URI. L'autenticazione della firma di accesso condiviso presenta due componenti: i _criteri di accesso condiviso_ e una _firma di accesso condiviso_, che viene spesso chiamata token. Un dispositivo usa tooauthenticate SAS con un hub IoT. [Le applicazioni back-end](#back-end-app) inoltre utilizzare tooauthenticate SAS con gli endpoint di servizio orientati hello su un hub IoT. In genere, si includono i token di firma di accesso condiviso hello hello [stringa di connessione](#connection-string) che un'app Usa tooestablish un hub IoT tooan di connessione.

## <a name="shared-access-policy"></a>Criteri di accesso condiviso
Criteri di accesso condiviso definiscono autorizzazioni hello tooanyone che ha una validità [chiave primaria o secondaria](#primary-and-secondary-keys) associata a tale criterio. È possibile gestire i criteri di accesso condiviso hello e le chiavi per l'hub hello [portale](#azure-portal).

## <a name="simulated-device"></a>Dispositivo simulato
Per praticità, molte delle esercitazioni IoT Hub utilizzano hello simulati tooenable dispositivi si toorun esempi sul computer locale. Al contrario, un [dispositivo fisico](#physical-device) è un dispositivo reale, ad esempio una Pi Raspberry che si connette tooan IoT hub.

## <a name="solution"></a>Soluzione
Oggetto _soluzione_ può fare riferimento tooa soluzione di Visual Studio che include uno o più progetti. A _soluzione_ può indicare anche tooan IoT soluzione che include elementi quali i dispositivi, [App per dispositivi](#device-app), un hub IoT, gli altri servizi Azure e [back-end app](#back-end-app).

## <a name="subscription"></a>Sottoscrizione
In una sottoscrizione di Azure viene eseguita la fatturazione. Ogni risorsa di Azure creata o ogni servizio di Azure usato è associato a una singola sottoscrizione. Molte quote si applicano anche a livello di hello di una sottoscrizione.

## <a name="system-properties"></a>Proprietà di sistema
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), le proprietà di sistema sono di sola lettura e includono informazioni sull'utilizzo di dispositivi hello, ad esempio lo stato di connessione e l'ora di ultima attività.

## <a name="tags"></a>Tag
Nel contesto di hello di un [doppi dispositivo](iot-hub-devguide-device-twins.md), i tag sono i metadati archiviati e recuperati dal back-end soluzione hello sotto forma di hello di un documento JSON. Tag non sono visibili tooapps in un dispositivo.

## <a name="telemetry"></a>Telemetria
Dispositivi raccogliere dati di telemetria, ad esempio velocità del vento o temperatura, e utilizzare [coordinata messaggi](#data-point-messages) toosend l'hub IoT tooan hello telemetria.

## <a name="token-service"></a>Servizio token
È possibile utilizzare un tooimplement token servizio un meccanismo di autenticazione per i dispositivi. Usa un IoT Hub [criterio di accesso condiviso](#shared-access-policy) con **DeviceConnect** autorizzazioni toocreate *con ambito dispositivo* token. Questi token abilitare l'hub IoT tooyour tooconnect un dispositivo. Un dispositivo usa una tooauthenticate meccanismo di autenticazione personalizzato con il servizio token di hello. Se il dispositivo hello viene autenticato correttamente, il servizio token di hello rilascia un token di firma di accesso condiviso per hello dispositivo toouse tooaccess l'hub IoT.

## <a name="x509-client-certificate"></a>Certificato client X.509
Un dispositivo può usare un tooauthenticate certificato x. 509 con [IoT Hub](#iot-hub). Utilizza un certificato x. 509 è un'alternativa toousing un [token SAS](#shared-access-signature).
