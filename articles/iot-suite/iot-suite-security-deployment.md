---
title: Proteggere la distribuzione di IoT (Internet delle cose) | Documentazione Microsoft
description: Questo articolo illustra come proteggere la distribuzione di IoT
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
ms.openlocfilehash: d752dd13b138cdae80dac5c0b2f84a19fe0aa670
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="secure-your-iot-deployment"></a>Proteggere la distribuzione di IoT
L'articolo fornisce una serie di informazioni avanzate per proteggere l'infrastruttura Azure IoT e fornisce i collegamenti ai dettagli a livello di implementazione per configurare e distribuire ciascun componente. Offre anche una serie di confronti e scelte tra i vari metodi concorrenti.

La protezione della distribuzione di Azure IoT può essere divisa nelle tre aree di sicurezza seguenti:

* **Sicurezza del dispositivo**: proteggere il dispositivo IoT mentre viene distribuito in circostanze normali.
* **Sicurezza delle connessioni**: garantire che tuti i dati trasmessi tra il dispositivo IoT e l'hub IoT siano riservati e a prova di manomissione.
* **Sicurezza del cloud**: fornire un mezzo per proteggere i dati duranti il trasferimento e l'archiviazione nel cloud.

![Tre aree di sicurezza][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Proteggere il provisioning dei dispositivi e l'autenticazione
Azure IoT Suite protegge dispositivi IoT mediante i due metodi seguenti:

* Fornendo una chiave di identità univoca (token di sicurezza) per ogni dispositivo, che può essere utilizzata dal dispositivo per comunicare con l'hub IoT.
* Usando un [certificato X.509 ][lnk-x509] su dispositivo e la chiave privata come mezzo per autenticare il dispositivo nell'hub IoT. Questo metodo di autenticazione assicura che la chiave privata sul dispositivo non sia mai nota all'esterno del dispositivo, garantendo un livello di sicurezza più elevato.

Il metodo basato sul token di sicurezza fornisce l'autenticazione per ogni chiamata effettuata dal dispositivo all'hub IoT associando la chiave simmetrica a ciascuna chiamata. L'autenticazione basata sul certificato x.509 consente di autenticare un dispositivo IoT a livello fisico come parte del processo di creazione della connessione TLS. Il metodo basato sul token di sicurezza può essere utilizzato senza l'autenticazione tramite certificato x.509, che rappresenta un modello meno sicuro. La scelta tra i due metodi dipende principalmente dal livello di protezione richiesto dall'autenticazione del dispositivo e dalla disponibilità di spazio di archiviazione sicura sul dispositivo (per archiviare la chiave privata in modo sicuro).

## <a name="iot-hub-security-tokens"></a>Token di sicurezza dell'hub IoT
Hub IoT usa i token di sicurezza per autenticare i dispositivi e i servizi ed evitare l'invio in rete delle chiavi. Inoltre, i token di sicurezza hanno una validità limitata in termini di tempo e portata. Gli Azure IoT SDK generano automaticamente i token senza richiedere una configurazione speciale. In alcuni scenari, tuttavia, è necessario che l'utente generi e usi direttamente i token di sicurezza. Questi scenari includono l'uso diretto delle superfici MQTT, AMQP o HTTP o l'implementazione del modello di servizio token.

Maggiori dettagli sulla struttura del token di sicurezza e il relativo utilizzo sono forniti all'interno degli articoli seguenti:

* [Struttura dei token di sicurezza][lnk-security-tokens]
* [Uso dei token SAS come dispositivo][lnk-sas-tokens]

Ogni hub IoT ha un [registro di identità][lnk-identity-registry] che può essere usato per creare risorse per dispositivo nel servizio, ad esempio una coda che contiene messaggi cloud a dispositivo in elaborazione, e per consentire l'accesso agli endpoint per dispositivi. Il Registro delle identità dell'hub IoT offre l'archiviazione protetta delle identità e delle chiavi di protezione del dispositivo per una soluzione. Le identità dei dispositivi, singolarmente o in gruppo, possono essere aggiunte a un elenco Consenti o Blocca, favorendo il controllo completo dell'accesso al dispositivo. Gli articoli seguenti illustrano altri dettagli sulla struttura del registro di identità e sulle operazioni supportate.

[L'hub IoT supporta protocolli quali MQTT, AMQP e HTTP][lnk-protocols]. Ognuno di questi protocolli utilizza i token di sicurezza dal dispositivo all'hub IoT in modo diverso:

* AMQP: sicurezza basata su attestazioni AMQP e SASL PLAIN ({policyName}@sas.root.{iothubName} nel caso di token a livello di hub IoT; {deviceId} nel caso di token con ambito dispositivo).
* MQTT: il pacchetto CONNECT usa {deviceId} come {ClientId}, {IoThubhostname}/{deviceId} nel campo **Nome utente** e un token di firma di accesso condiviso nel campo **Password**.
* HTTP: il token valido è contenuto nell'intestazione della richiesta di autorizzazione.

Il registro di identità dell'hub IoT può essere usato per configurare il controllo dell'accesso e le credenziali di sicurezza per dispositivo. Se tuttavia una soluzione IoT presenta già un investimento significativo in un [registro personalizzato di identità dei dispositivi e/o in uno schema di autenticazione][lnk-custom-auth], è possibile integrarla nell'infrastruttura esistente con l'hub IoT creando un servizio token.

### <a name="x509-certificate-based-device-authentication"></a>Autenticazione del dispositivo basata sul certificato x.509
L'uso di un [certificato x.509 basato su dispositivo][lnk-protocols] e la coppia di chiavi pubblica e privata associata consente un'autenticazione aggiuntiva a livello fisico. La chiave privata viene archiviata in modo sicuro nel dispositivo e non può essere individuata all'esterno del dispositivo. Il certificato x.509 contiene informazioni sul dispositivo (ad esempio l'ID dispositivo) e altri dettagli dell'organizzazione. Una firma del certificato viene generata utilizzando la chiave privata.

Flusso di provisioning di dispositivi di alto livello:

* Associare un identificatore a un dispositivo fisico: associazione dell'identità del dispositivo e/o del certificato x.509 al dispositivo durante la produzione e la messa in funzione del dispositivo.
* Creare una voce di identità corrispondente nell'hub IoT: l'identità del dispositivo e le informazioni sul dispositivo associato nel registro di identità dell'hub IoT.
* Archiviare in modo sicuro l'identificazione personale del certificato x.509 nel registro di identità dell'hub IoT.

### <a name="root-certificate-on-device"></a>Certificato principale nel dispositivo
Durante il tentativo di stabilire una connessione TLS sicura con l'hub IoT, il dispositivo IoT autentica l'hub IoT usando un certificato principale che fa parte dell'SDK per dispositivi. Per l'SDK client dell'unità C, il certificato si trova nella cartella "\\c\\certs" nella radice del repository. Anche se questi certificati sono di lunga durata, possono comunque scadere o essere revocati. Se non esiste alcun modo di aggiornare il certificato sul dispositivo, il dispositivo potrebbe successivamente non essere in grado di connettersi all'hub IoT (o qualsiasi altro servizio cloud). Questo rischio si riduce efficacemente se si dispone di un mezzo per aggiornare il certificato principale dopo aver distribuito il dispositivo IoT.

## <a name="securing-the-connection"></a>Proteggere la connessione
La connessione Internet tra il dispositivo IoT e l'hub IoT è protetta mediante lo standard TLS (Transport Layer Security). IoT di Azure supporta gli standard[TLS 1.2][lnk-tls12], TLS 1.1 e TLS 1.0, in questo ordine. Il supporto per lo standard TLS 1.0 viene fornito soltanto per la compatibilità con le versioni precedenti. Si consiglia di usare lo standard TLS 1.2, che fornisce un livello di protezione superiore.

Azure IoT Suite supporta, nell'ordine, i pacchetti di crittografia seguenti:

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

## <a name="securing-the-cloud"></a>Proteggere il cloud
L'hub IoT di Azure consente la definizione dei [criteri di controllo di accesso][lnk-protocols] per ogni chiave di sicurezza, usando il set di autorizzazioni seguente per concedere l'accesso agli endpoint dell'hub IoT. Le autorizzazioni limitano l'accesso a un hub IoT in base alla funzionalità.

* **RegistryRead**. Concede l'accesso di sola lettura al registro di identità. Per altre informazioni, vedere [Registro di identità][lnk-identity-registry].
* **RegistryReadWrite**. Concede l'accesso di lettura e scrittura al registro di identità. Per altre informazioni, vedere [Registro di identità][lnk-identity-registry].
* **ServiceConnect**. Concede l'accesso alle comunicazioni per il servizio cloud e al monitoraggio degli endpoint. Ad esempio, concede ai servizi cloud back-end l'autorizzazione per la ricezione di messaggi da dispositivo a cloud, l'invio di messaggi da cloud a dispositivo e il recupero degli acknowledgment di recapito corrispondenti.
* **DeviceConnect**. Concede l'accesso agli endpoint per il dispositivo. Ad esempio, concede l'autorizzazione per l'invio di messaggi da dispositivo a cloud e la ricezione di messaggi da cloud a dispositivo. Questa autorizzazione viene usata dai dispositivi.

Ci sono due modi per ottenere le autorizzazioni **DeviceConnect** su hub IoT con i [token di sicurezza][lnk-sas-tokens]: tramite una chiave di identità dispositivo o tramite una chiave di accesso condiviso. Inoltre, è importante notare che tutte le funzionalità accessibili dai dispositivi vengono esposte, per impostazione predefinita, sugli endpoint con prefisso `/devices/{deviceId}`.

[I componenti del servizio possono generare token di sicurezza][lnk-service-tokens] solo tramite criteri di accesso condiviso che concedono le autorizzazioni appropriate.

L'hub IoT di Azure e altri servizi che possono essere parte della soluzione consentono la gestione degli utenti mediante l'Azure Active Directory.

I dati inseriti dall'Hub IoT di Azure possono essere usati da una serie di servizi, ad esempio Analisi di flusso di Azure, Archiviazione BLOB e così via. Questi servizi consentono l'accesso di gestione. Ulteriori informazioni su questi servizi e sulle opzioni disponibili riportate di seguito:

* [Azure Cosmos DB][lnk-docdb]: un servizio di database scalabile e completamente indicizzato per i dati semistrutturati che gestiscono metadati per i dispositivi di cui si effettua il provisioning, ad esempio attributi, configurazione e proprietà di sicurezza. Cosmos DB offre l'elaborazione ad alte prestazioni e velocità effettiva elevata, indicizzazione dei dati senza schema e una ricca interfaccia di query SQL.
* [Analisi di flusso di Azure][lnk-asa]: elaborazione del flusso in tempo reale nel cloud per sviluppare e distribuire rapidamente una soluzione di analisi a basso costo che consenta di rilevare informazioni approfondite in tempo reale da dispositivi, sensori, infrastruttura e applicazioni. I dati di questo servizio completamente gestito possono raggiungere qualsiasi volume anche in condizioni di velocità effettiva elevata, bassa latenza e resilienza.
* [Servizi app di Azure][lnk-appservices]: piattaforma cloud per compilare efficaci app mobili e Web che si connettono ai dati ovunque si trovino: nel cloud o localmente. Creare app per dispositivi mobili coinvolgenti per iOS, Android e Windows. Eseguire l'integrazione con applicazioni Software as a Service (SaaS) e aziendali, grazie a connettività integrata a dozzine di applicazioni aziendali e servizi basati sul cloud. Scrivere codice usando IDE e il linguaggio preferito, .NET, Node.js, PHP, Python o Java, per creare app Web e API più rapidamente che mai.
* [App per la logica][lnk-logicapps]: la funzionalità App per la logica del servizio app di Azure consente di integrare la soluzione IoT con i sistemi line-of-business esistenti e automatizzare i processi del flusso di lavoro. App per la logica consente agli sviluppatori di progettare flussi di lavoro che vengono avviati da un trigger e quindi di eseguire una serie di passaggi, regole e azioni che usano potenti connettori per l'integrazione con i processi aziendali. App per la logica offre connettività integrata per un vasto ecosistema di applicazioni SaaS, basate sul cloud e locali.
* [Archiviazione BLOB di Azure][lnk-blob]: archiviazione cloud affidabile ed economica per i dati che i dispositivi inviano al cloud.

## <a name="conclusion"></a>Conclusione
Questo articolo fornisce una panoramica a livello di implementazione per progettare e distribuire un'infrastruttura mediante Azure IoT. Per una protezione complessiva dell'infrastruttura IoT è fondamentale configurare la sicurezza di ciascun componente. Le scelte di progettazione disponibili in Azure IoT forniscono un certo livello di flessibilità e scelta; tuttavia, ogni scelta può avere determinate implicazioni di sicurezza. Si consiglia di vagliare entrambe le opzioni secondo il criterio di una valutazione dei costi e del rischio.

## <a name="see-also"></a>Vedere anche
È anche possibile esplorare alcune altre funzionalità delle soluzioni preconfigurate di IoT Suite:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su IoT Suite][lnk-faq]

Informazioni sulla protezione dell'hub IoT sono disponibili in [Controllare l'accesso all'hub IoT][lnk-devguide-security] nella guida per gli sviluppatori dell'hub IoT.


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
