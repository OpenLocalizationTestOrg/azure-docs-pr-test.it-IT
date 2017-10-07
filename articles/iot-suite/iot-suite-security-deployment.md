---
title: aaaSecure la distribuzione di Internet delle cose | Documenti Microsoft
description: Questo articolo come dettagli toosecure distribuzione IoT
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: befba8f2009279c2217dcd3496d529139134ec01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-iot-deployment"></a>Proteggere la distribuzione di IoT
Livello di dettaglio successivo hello fornite per la protezione dell'infrastruttura di hello basato su Azure IoT Internet delle cose (IoT). I dettagli per la configurazione e distribuzione di ogni componente di livello tooimplementation vengono collegati. Offre anche una serie di confronti e scelte tra i vari metodi concorrenti.

Proteggere la distribuzione di Azure IoT hello può essere suddivisi in tre aree di sicurezza seguente hello:

* **Sicurezza del dispositivo**: protezione mentre è distribuita in hello wild di dispositivo IoT hello.
* **Sicurezza della connessione**: assicurandosi di tutti i dati trasmessi tra l'IoT Hub e il dispositivo IoT hello è riservato e da eventuali alterazioni.
* **Protezione del cloud**: fornendo una modalità toosecure dati mentre vengono spostati e viene archiviato nel cloud hello.

![Tre aree di sicurezza][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Proteggere il provisioning dei dispositivi e l'autenticazione
Hello Azure IoT Suite consente di proteggere i dispositivi IoT da hello due metodi seguenti:

* Fornendo una chiave di identità univoco (token di sicurezza) per ogni dispositivo, che può essere usato dall'hello dispositivo toocommunicate con hello IoT Hub.
* Tramite un dispositivo [certificato x. 509] [ lnk-x509] e la chiave privata come un toohello di mezzo tooauthenticate hello dispositivo IoT Hub. Questo metodo di autenticazione assicura che hello chiave privata nel dispositivo hello non è noto all'esterno di dispositivo hello in qualsiasi momento, fornendo un livello di sicurezza.

metodo token di sicurezza Hello fornisce l'autenticazione per ogni chiamata effettuata da hello dispositivo tooIoT Hub associando la chiamata di hello tooeach chiave simmetrica. L'autenticazione basata su certificati x. 509 consente l'autenticazione di un dispositivo IoT a livello fisico di hello come parte di stabilire la connessione TLS hello. il metodo basato su token di sicurezza Hello è utilizzabile senza l'autenticazione di x. 509 hello, che è un modello meno sicura. Hello scelta tra metodi hello due principalmente dipende da come proteggere hello l'autenticazione del dispositivo deve toobe e la disponibilità di archiviazione protetta nel dispositivo hello (toostore hello chiave privata in modo sicuro).

## <a name="iot-hub-security-tokens"></a>Token di sicurezza dell'hub IoT
IoT Hub Usa sicurezza token tooauthenticate dispositivi e servizi tooavoid l'invio delle chiavi nella rete hello. Inoltre, i token di sicurezza hanno una validità limitata in termini di tempo e portata. Gli Azure IoT SDK generano automaticamente i token senza richiedere una configurazione speciale. Alcuni scenari, tuttavia, richiedono toogenerate utente hello e utilizzano direttamente i token di sicurezza. Sono inclusi l'uso diretto hello superfici hello MQTT, AMQP o HTTP, o implementazione hello del modello di servizio token di hello.

Ulteriori informazioni sulla struttura di hello del token di sicurezza hello e sul relativo utilizzo, vedere hello seguenti articoli:

* [Struttura dei token di sicurezza][lnk-security-tokens]
* [Uso dei token SAS come dispositivo][lnk-sas-tokens]

Ogni IoT Hub è un [Registro di sistema di identità] [ lnk-identity-registry] che può essere utilizzato toocreate per ogni dispositivo risorse nel servizio di hello, ad esempio una coda contenente messaggi da cloud a dispositivo in transito e tooallow accesso toohello endpoint che utilizzano il dispositivo. Hello del Registro di sistema di IoT Hub identità fornisce l'archiviazione sicura di identità di dispositivi e le chiavi di sicurezza per una soluzione. È possono aggiungere singoli o gruppi di identità dispositivo tooan consente di elenco o un elenco di blocco, abilitare il controllo completo sul dispositivo l'accesso. Hello articoli seguenti offrono ulteriori informazioni sulla struttura di hello del Registro di identità hello e operazioni supportate.

[L'hub IoT supporta protocolli quali MQTT, AMQP e HTTP][lnk-protocols]. Ognuno di questi protocolli utilizzare token di sicurezza da hello IoT dispositivo tooIoT Hub in modo diverso:

* AMQP: Sicurezza di semplice e basata sulle attestazioni AMQP SASL ({policyName}@sas.root. { iothubName} nel caso di hello di token a livello di hub IoT; {deviceId} in caso di token con ambito dispositivo).
* MQTT: La connessione utilizza pacchetto {deviceId} come hello {ClientId}, {IoThubhostname} / {deviceId} in hello **Username** token di campo e una firma di accesso condiviso in hello **Password** campo.
* HTTP: Token valido è nell'intestazione di richiesta di autorizzazione hello.

Registro di sistema di IoT Hub identità può essere tooconfigure utilizzate le credenziali di sicurezza per ogni dispositivo e il controllo degli accessi. Se tuttavia una soluzione IoT presenta già un investimento significativo in un [registro personalizzato di identità dei dispositivi e/o in uno schema di autenticazione][lnk-custom-auth], è possibile integrarla nell'infrastruttura esistente con l'hub IoT creando un servizio token.

### <a name="x509-certificate-based-device-authentication"></a>Autenticazione del dispositivo basata sul certificato x.509
utilizzo di Hello un [basato su dispositivi certificato x. 509] [ lnk-protocols] e la coppia di chiavi pubblica e privata associata consente l'autenticazione aggiuntiva a livello fisico hello. la chiave privata di Hello viene archiviata in modo sicuro nel dispositivo hello e non è individuabile esterno hello dispositivo. certificato x. 509 Hello contiene informazioni sul dispositivo hello, ad esempio, un ID dispositivo e altri dettagli dell'organizzazione. La firma del certificato hello viene generata utilizzando la chiave privata di hello.

Flusso di provisioning di dispositivi di alto livello:

* Associare un identificatore tooa dispositivo fisico: identità del dispositivo e/o dispositivo toohello associato di certificato x. 509 durante la periferica di produzione o la messa in funzione.
* Creare una voce di identità corrispondente nell'IoT Hub: identità del dispositivo e le informazioni di dispositivo associati nel Registro di identità IoT Hub hello.
* Archiviare in modo sicuro l'identificazione personale del certificato x.509 nel registro di identità dell'hub IoT.

### <a name="root-certificate-on-device"></a>Certificato principale nel dispositivo
Il tentativo di stabilire una connessione sicura TLS con l'IoT Hub, dispositivi IoT hello autentica IoT Hub utilizzando un certificato radice che fa parte del dispositivo hello SDK. Per client hello C SDK certificato hello si trova nella cartella hello "\\c\\certificati" nella radice hello repository hello. Anche se questi certificati sono di lunga durata, possono comunque scadere o essere revocati. Se non esiste alcun modo di aggiornamento del certificato hello sul dispositivo hello, hello dispositivo potrebbe non essere in grado di toosubsequently connettersi toohello IoT Hub (o qualsiasi altro servizio cloud). Con un certificato radice di mezzo tooupdate hello dopo aver distribuito dispositivo IoT hello in modo efficace sarà possibile limitare questo rischio.

## <a name="securing-hello-connection"></a>Protezione hello connessione
Connessione Internet tra dispositivo IoT hello e IoT Hub è protetto tramite hello Transport Layer Security (TLS) standard. IoT di Azure supporta gli standard[TLS 1.2][lnk-tls12], TLS 1.1 e TLS 1.0, in questo ordine. Il supporto per lo standard TLS 1.0 viene fornito soltanto per la compatibilità con le versioni precedenti. È consigliabile toouse TLS 1.2 in quanto fornisce hello maggiore protezione.

Azure IoT Suite supporta hello seguenti pacchetti di crittografia, in questo ordine.

| Pacchetto di crittografia | Length |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (uguale a RSA a 7680 bit) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (uguale a RSA a 3072 bit) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (uguale a RSA a 7680 bit) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (uguale a RSA a 3072 bit) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>La protezione cloud hello
L'hub IoT di Azure consente la definizione dei [criteri di controllo di accesso][lnk-protocols] per ogni chiave di sicurezza, Usa hello seguente set di autorizzazioni toogrant accesso tooeach degli endpoint dell'IoT Hub. Le autorizzazioni limitano hello accesso tooan che hub IoT in base alle funzionalità.

* **RegistryRead**. Concede l'accesso in lettura toohello identità Registro di sistema. Per altre informazioni, vedere [Registro di identità][lnk-identity-registry].
* **RegistryReadWrite**. Concede l'accesso in lettura e scrittura toohello identità Registro di sistema. Per altre informazioni, vedere [Registro di identità][lnk-identity-registry].
* **ServiceConnect**. Concede l'accesso toocloud orientati ai servizi comunicazione e gli endpoint di monitoraggio. Ad esempio, concede autorizzazioni tooback-end cloud services tooreceive da dispositivo a cloud messaggi, invio di messaggi da cloud a dispositivo e recuperare hello corrispondente conferma di recapito.
* **DeviceConnect**. Concede l'accesso gli endpoint orientati toodevice. Ad esempio, concede l'autorizzazione di messaggi da dispositivo a cloud toosend e ricevere messaggi da cloud a dispositivo. Questa autorizzazione viene usata dai dispositivi.

Esistono due modi tooobtain **DeviceConnect** autorizzazioni con l'IoT Hub con [i token di sicurezza][lnk-sas-tokens]: usando una chiave di identità del dispositivo o una chiave di accesso condiviso. Inoltre, è importante toonote tutte le funzionalità accessibili dai dispositivi esposto dalla progettazione sugli endpoint con prefisso `/devices/{deviceId}`.

[Componenti del servizio possono solo generare token di sicurezza] [ lnk-service-tokens] utilizza la concessione delle autorizzazioni appropriate di hello i criteri di accesso condivisa.

IoT Hub Azure e altri servizi che possono far parte della soluzione hello consentono la gestione di utenti che usano hello Azure Active Directory.

I dati inseriti dall'Hub IoT di Azure possono essere usati da una serie di servizi, ad esempio Analisi di flusso di Azure, Archiviazione BLOB e così via. Questi servizi consentono l'accesso di gestione. Ulteriori informazioni su questi servizi e sulle opzioni disponibili riportate di seguito:

* [Azure DB Cosmos][lnk-docdb]: un servizio di database scalabile e completamente indicizzato per dati semistrutturati che gestisce i metadati per i dispositivi hello viene effettuato il provisioning, ad esempio gli attributi, la configurazione e le proprietà di sicurezza. Cosmos DB offre l'elaborazione ad alte prestazioni e velocità effettiva elevata, indicizzazione dei dati senza schema e una ricca interfaccia di query SQL.
* [Azure Analitica flusso][lnk-asa]: flusso in tempo reale di elaborazione nel cloud hello che consente di toorapidly sviluppare e distribuire informazioni in tempo reale di basso costo analitica soluzione toouncover dai dispositivi, sensori, infrastruttura e le applicazioni. dati Hello da questo servizio completamente gestito possono essere ridimensionati volume tooany comunque una velocità effettiva elevata, bassa latenza e resilienza.
* [Servizi App Azure][lnk-appservices]: web potente toobuild piattaforma cloud e App per dispositivi mobili che si connettono toodata in qualsiasi punto; nel cloud hello o in locale. Creare app per dispositivi mobili coinvolgenti per iOS, Android e Windows. Integrazione con il Software come servizio (SaaS) ed enterprise nelle applicazioni con connettività di casella toodozens di servizi basati su cloud e applicazioni aziendali. Codice nell'IDE e linguaggio preferito toobuild web App (.NET, Node.js, PHP, Python o Java) e le API più veloce che mai.
* [Logica app][lnk-logicapps]: hello logica App funzionalità di servizio App di Azure consente di integrare i sistemi di line-of-business esistenti IoT soluzione tooyour e automatizzare i processi del flusso di lavoro. Logica App consente agli sviluppatori toodesign i flussi di lavoro che iniziano da un trigger e quindi eseguire una serie di passaggi, regole e le azioni che utilizzano i connettori potente toointegrate con i processi di business. La logica App offre vasto ecosistema tooa connettività della casella di SaaS, basati su cloud e applicazioni locali.
* [Archiviazione blob di Azure][lnk-blob]: archiviazione cloud affidabile ed economico per i dati di hello che i dispositivi inviano toohello cloud.

## <a name="conclusion"></a>Conclusioni
Questo articolo fornisce una panoramica a livello di implementazione per progettare e distribuire un'infrastruttura mediante Azure IoT. Configurazione di ogni componente toobe sicura è chiave nella protezione hello intera infrastruttura di IoT. scelte di progettazione Hello disponibili in Azure IoT offrono un certo livello di flessibilità e scelta; Tuttavia, ogni opzione può comportare implicazioni di sicurezza. Si consiglia di vagliare entrambe le opzioni secondo il criterio di una valutazione dei costi e del rischio.

## <a name="see-also"></a>Vedere anche
È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su IoT Suite][lnk-faq]

È possibile leggere sulla sicurezza di IoT Hub in [tooIoT accesso controllo Hub] [ lnk-devguide-security] nella Guida per sviluppatori di IoT Hub hello.


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
