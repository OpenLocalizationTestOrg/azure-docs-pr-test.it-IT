---
title: sicurezza di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: "Le istruzioni per sviluppatori - modalità toocontrol accesso tooIoT Hub per le app di dispositivo e back-end. Include informazioni sui token di sicurezza e sul supporto per i certificati x.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Controllo accesso tooIoT Hub

Questo articolo descrive le opzioni di hello per proteggere l'hub IoT. Usa IoT Hub *autorizzazioni* endpoint hub IoT di toogrant accesso tooeach. Le autorizzazioni di limitano l'hub IoT tooan accesso hello in base alle funzionalità.

L'articolo illustra:

* Hello diverse autorizzazioni che è possibile concedere tooa dispositivo o app back-end tooaccess l'hub IoT.
* Hello processo e hello i token di autenticazione usa tooverify autorizzazioni.
* Come tooscope credenziali toospecific toolimit accedere alle risorse.
* Supporto dell'hub IoT per i certificati x.509.
* Meccanismo di autenticazione personalizzata del dispositivo che usa gli schemi di autenticazione o i registri di identità del dispositivo esistenti.

### <a name="when-toouse"></a>Quando toouse

È necessario disporre delle autorizzazioni appropriate tooaccess qualsiasi endpoint Hub IoT hello. Ad esempio, un dispositivo deve includere un token contenente le credenziali di sicurezza con ogni messaggio inviato tooIoT Hub.

## <a name="access-control-and-permissions"></a>Controllo dell'accesso e autorizzazioni

È possibile concedere [autorizzazioni](#iot-hub-permissions) in hello seguenti modi:

* **Criteri di accesso condivisi a livello di hub IoT**. I criteri di accesso condiviso possono concedere qualsiasi combinazione di [autorizzazioni](#iot-hub-permissions). È possibile definire i criteri in hello [portale di Azure][lnk-management-portal], o a livello di programmazione utilizzando hello [il provider di risorse IoT Hub API REST][lnk-resource-provider-apis]. Un hub IoT appena creato è hello criteri predefiniti seguenti:

  * **iothubowner**: criteri con tutte le autorizzazioni.
  * **service**: criteri con autorizzazione **ServiceConnect**.
  * **device**: criteri con autorizzazione **DeviceConnect**.
  * **registryRead**: criteri con autorizzazione **RegistryRead**.
  * **registryReadWrite**: criteri con autorizzazioni **RegistryRead** e RegistryWrite.
  * **Credenziali di sicurezza specifiche del dispositivo**. Ogni hub IoT contiene un [registro delle identità][lnk-identity-registry]. Per ogni dispositivo in questo registro di sistema di identità, è possibile configurare le credenziali di sicurezza che concedono **DeviceConnect** autorizzazioni con ambito toohello gli endpoint di periferica corrispondente.

Ad esempio, in una soluzione IoT tipica:

* componente di Gestione periferiche Hello utilizza hello *registryReadWrite* criteri.
* componente elaboratore eventi di Hello utilizza hello *servizio* criteri.
* componente della logica di business in fase di esecuzione dispositivo Hello utilizza hello *servizio* criteri.
* I singoli dispositivi di connetteranno utilizzando le credenziali archiviate nel Registro di sistema dell'hub IoT hello identità.

> [!NOTE]
> Per informazioni dettagliate, vedere [Autorizzazioni](#iot-hub-permissions).

## <a name="authentication"></a>Autenticazione

IoT Hub Azure concede accesso tooendpoints verificando un token con i criteri di accesso condiviso hello e credenziali di sicurezza del Registro di sistema di identità.

Le credenziali di sicurezza, ad esempio le chiavi simmetriche, non vengono mai inviate in transito hello.

> [!NOTE]
> Hello provider di risorse IoT Hub di Azure è protetto tramite una sottoscrizione di Azure, sono tutti i provider di hello [Azure Resource Manager][lnk-azure-resource-manager].

Per ulteriori informazioni su come tooconstruct e l'utilizzo di token di sicurezza, vedere [i token di sicurezza di IoT Hub][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Specifiche del protocollo

Ogni protocollo supportato, ad esempio MQTT, AMQP e HTTP, trasporta i token in modo diverso.

Quando si utilizza MQTT, pacchetto CONNETTI hello ha hello deviceId hello ClientId, {iothubhostname} / {deviceId} nel campo nome utente hello e un token di firma di accesso condiviso nel campo Password hello. {iothubhostname} deve essere hello CName completo dell'hub IoT hello (ad esempio, contoso.azure devices.net).

Quando si usa [AMQP][lnk-amqp], l'hub IoT supporta [SASL PLAIN][lnk-sasl-plain] e la [sicurezza basata sulle attestazioni AMQP][lnk-cbs].

Se si usa AMQP attestazioni in base a sicurezza, specifica hello standard come tootransmit questi token.

Per il normale SASL, hello **username** può essere:

* `{policyName}@sas.root.{iothubName}` nel caso di token a livello di hub IoT.
* `{deviceId}@sas.{iothubname}` ne caso di token con ambito relativo al dispositivo.

In entrambi i casi, il campo di password hello contiene token hello, come descritto in [i token di sicurezza di IoT Hub][lnk-sas-tokens].

HTTP implementa l'autenticazione con l'inclusione di un token valido in hello **autorizzazione** intestazione della richiesta.

#### <a name="example"></a>Esempio

Nome utente (per DeviceId viene fatta distinzione tra maiuscole e minuscole): `iothubname.azure-devices.net/DeviceId`

Password (token di firma di accesso condiviso generato con hello [Esplora dispositivo] [ lnk-device-explorer] strumento):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Hello [Azure IoT SDK] [ lnk-sdks] generare automaticamente i token durante la connessione del servizio toohello. In alcuni casi, hello Azure IoT SDK non supportano tutti i protocolli di hello o tutti i metodi di autenticazione hello.

### <a name="special-considerations-for-sasl-plain"></a>Considerazioni speciali su SASL PLAIN

Quando si utilizza SASL normale con AMQP, un client che si connette l'hub IoT tooan è possibile utilizzare un token singolo per ogni connessione TCP. Quando il token hello scade, hello connessione TCP disconnette dal servizio hello e viene attivata una riconnessione. Questo comportamento, mentre non problematico per un'applicazione back-end, danneggiare per un'applicazione di dispositivo per hello seguenti motivi:

* I gateway si connettono in genere per conto di molti dispositivi. Quando si utilizza SASL normale, hanno il toocreate una connessione TCP distinta per ogni dispositivo di connessione hub IoT tooan. Questo scenario notevolmente aumenta al consumo di energia e le risorse di rete hello e aumenta la latenza di hello di ogni connessione del dispositivo.
* Dispositivi con risorse limitate possono essere influenzati negativamente mediante l'utilizzo di hello aumentato di risorse tooreconnect dopo ogni scadenza del token.

## <a name="scope-iot-hub-level-credentials"></a>Definire l'ambito delle credenziali a livello di hub IoT

È possibile definire l'ambito dei criteri di sicurezza a livello di hub IoT creando token con URI di risorsa con limitazioni. Ad esempio, i messaggi da dispositivo a cloud di hello endpoint toosend da un dispositivo è **/devices/ {deviceId} / messaggi/eventi**. È inoltre possibile utilizzare un criterio di accesso condiviso a livello di hub IoT con **DeviceConnect** toosign autorizzazioni un token di cui resourceURI **/devices/ {deviceId}**. Questo approccio consente di creare un token solo messaggi toosend utilizzabile per conto di dispositivo **deviceId**.

Questo meccanismo è simile toohello [criteri dell'editore hub eventi][lnk-event-hubs-publisher-policy]ed è possibile tooimplement metodi di autenticazione personalizzati.

## <a name="security-tokens"></a>Token di sicurezza

IoT Hub utilizza la protezione del token tooauthenticate dispositivi e servizi tooavoid l'invio delle chiavi durante la trasmissione hello. Inoltre, i token di sicurezza hanno una validità limitata in termini di tempo e portata. Gli [Azure IoT SDK][lnk-sdks] generano automaticamente i token senza richiedere una configurazione speciale. Alcuni scenari richiedono toogenerate e utilizzare direttamente i token di sicurezza. Tali scenari includono:

* utilizzo diretto di Hello superfici hello MQTT, AMQP o HTTP.
* Hello implementazione del modello di servizio token di hello, come illustrato in [l'autenticazione del dispositivo personalizzato][lnk-custom-auth].

IoT Hub consente inoltre alle periferiche tooauthenticate con l'IoT Hub utilizzando [certificati x. 509][lnk-x509].

### <a name="security-token-structure"></a>Formato del token di sicurezza

Si utilizza protezione token toogrant accesso limitato al tempo toodevices e servizi toospecific funzionalità nell'IoT Hub. tooget autorizzazione tooconnect tooIoT Hub, dispositivi e servizi devono inviare i token di sicurezza firmati con un accesso condiviso o della chiave simmetrica. Tali chiavi vengono archiviate con un'identità del dispositivo nel Registro di sistema di hello identità.

Un token firmato con un'accesso condiviso chiave concede accesso tooall hello funzionalità associate le autorizzazioni di criteri di accesso condiviso hello. Un token firmato con hello simmetrica chiave concede solo dell'identità del dispositivo **DeviceConnect** l'autorizzazione per hello è associata l'identità del dispositivo.

token di sicurezza Hello è hello seguente formato:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Di seguito sono i valori previsti hello:

| Valore | Descrizione |
| --- | --- |
| {signature} |Una stringa di firma del modulo hello HMAC-SHA256: `{URL-encoded-resourceURI} + "\n" + expiry`. **Importante**: chiave hello è decodificare da base64 e utilizzato come chiave tooperform calcolo di hello HMAC-SHA256. |
| {resourceURI} |Prefisso URI (per segmento) di endpoint hello che è possibile accedere con questo token, a partire da nome host dell'hub IoT hello (nessun protocol). Ad esempio, `myHub.azure-devices.net/devices/device1` |
| {expiry} |Stringhe UTF8 per il numero di secondi trascorsi hello epoch 00:00:00 UTC del 1 ° gennaio 1970. |
| {URL-encoded-resourceURI} |Più basso caso la codifica URL della risorsa di lettere minuscole hello URI |
| {policyName} |nome di Hello di hello condiviso toowhich di criteri di accesso che fa riferimento il token. Assente se il token hello fa riferimento credenziali toodevice Registro di sistema. |

**Nota sul prefisso**: prefisso URI hello viene calcolato dal segmento e non dai caratteri. Ad esempio `/a/b` è un prefisso per `/a/b/c` ma non per `/a/bc`.

Hello frammento Node.js seguente viene illustrata una funzione denominata **generateSasToken** che calcola hello token dagli input hello `resourceUri, signingKey, policyName, expiresInMins`. Nelle sezioni successive di Hello in dettaglio come i diversi input hello tooinitialize per token diverso hello casi d'uso.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Come un confronto, hello equivalente toogenerate di codice Python che è un token di sicurezza:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Poiché hello tempo di validità delle token hello viene convalidato in computer IoT Hub, deviazione hello su clock hello del computer di hello che genera token hello deve essere minimo.

### <a name="use-sas-tokens-in-a-device-app"></a>Usare i token di firma di accesso condiviso in un dispositivo client

Esistono due modi tooobtain **DeviceConnect** autorizzazioni con l'IoT Hub con i token di sicurezza: utilizzare un [chiave simmetrica dispositivo dal Registro di sistema identità hello](#use-a-symmetric-key-in-the-identity-registry), oppure utilizzare un [chiavediaccessocondiviso](#use-a-shared-access-policy).

Tenere presente che, per impostazione predefinita, tutte le funzionalità accessibili dai dispositivi vengono esposte negli endpoint con il prefisso `/devices/{deviceId}`.

> [!IMPORTANT]
> chiave simmetrica identità del dispositivo hello utilizza Hello unico modo che l'IoT Hub autentica un dispositivo specifico. Quando un criterio di accesso condiviso viene usato tooaccess funzionalità del dispositivo, soluzione hello deve considerare la possibilità componente hello emissione di token di sicurezza hello come sottocomponente attendibile.

gli endpoint che utilizzano il dispositivo di Hello sono (indipendentemente dal protocollo hello):

| Endpoint | Funzionalità |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Invio di messaggi da dispositivo a cloud. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Ricezione di messaggi da cloud a dispositivo. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Utilizzare una chiave simmetrica nel Registro di sistema di hello identità

Quando si utilizza toogenerate chiave simmetrica un token dell'identità del dispositivo, hello policyName (`skn`) elemento di token hello viene omesso.

Ad esempio, un token creato tooaccess tutte le funzionalità di dispositivo deve avere hello seguenti parametri:

* URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* chiave di firma: qualsiasi chiave simmetrica per hello `{device id}` identità,
* Nessun nome di criterio,
* Qualsiasi ora di scadenza.

Un esempio di utilizzo hello precedente Node.js funzione sarà:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

risultato Hello, che concede l'accesso tooall funzionalità per la periferica 1, sarà:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> È possibile toogenerate un token di firma di accesso condiviso usando .NET hello [Esplora dispositivo] [ lnk-device-explorer] degli strumenti o hello multipiattaforma, basato su nodi [l'hub IOT Esplora] [ lnk-iothub-explorer] utilità della riga di comando.

### <a name="use-a-shared-access-policy"></a>Usare criteri di accesso condiviso

Quando si crea un token da un criterio di accesso condiviso, impostare hello `skn` toohello nome dei criteri di hello. Questo criterio deve concedere hello **DeviceConnect** autorizzazione.

Hello due scenari principali per l'utilizzo di funzionalità della periferica di tooaccess criteri di accesso condiviso sono:

* [gateway del protocollo cloud][lnk-endpoints],
* [servizi token] [ lnk-custom-auth] utilizzato tooimplement schemi di autenticazione personalizzati.

Poiché hello criteri di accesso condiviso possono potenzialmente concedere accesso tooconnect qualsiasi dispositivo, che è importante toouse hello corretto URI della risorsa durante la creazione di token di sicurezza. Questa impostazione è particolarmente importante per i servizi token, che hanno tooscope hello tooa token dispositivo specifico utilizzando l'URI della risorsa hello. Questo punto è meno importante per i gateway di protocollo, in quanto già filtrano il traffico per tutti i dispositivi.

Ad esempio, un servizio token utilizzando hello creato in precedenza condivise criterio di accesso denominato **dispositivo** creerebbe un token con hello seguenti parametri:

* URI della risorsa: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* chiave di firma: una delle chiavi di hello di hello `device` criteri,
* nome criterio: `device`,
* Qualsiasi ora di scadenza.

Un esempio di utilizzo hello precedente Node.js funzione sarà:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

risultato Hello, che concede l'accesso tooall funzionalità per la periferica 1, sarà:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Un gateway di protocollo Impossibile usare hello stesso token per tutti i dispositivi semplicemente impostazione hello URI risorsa troppo`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Usare token di sicurezza da componenti del servizio

Componenti del servizio possono solo generare token di sicurezza usando i criteri di accesso condiviso concessione delle autorizzazioni appropriate di hello come descritto in precedenza.

Ecco funzioni hello del servizio esposte su endpoint hello:

| Endpoint | Funzionalità |
| --- | --- |
| `{iot hub host name}/devices` |Creazione, aggiornamento, recupero ed eliminazione delle identità dispositivo. |
| `{iot hub host name}/messages/events` |Ricezione di messaggi da dispositivo a cloud. |
| `{iot hub host name}/servicebound/feedback` |Ricezione di feedback per messaggi da cloud a dispositivo. |
| `{iot hub host name}/devicebound` |Invio di messaggi da cloud a dispositivo. |

Ad esempio, un servizio di generazione utilizzando hello creato in precedenza condivise criterio di accesso denominato **registryRead** creerebbe un token con hello seguenti parametri:

* URI della risorsa: `{IoT hub name}.azure-devices.net/devices`,
* chiave di firma: una delle chiavi di hello di hello `registryRead` criteri,
* nome criterio: `registryRead`,
* Qualsiasi ora di scadenza.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

risultato Hello, che viene concesso l'accesso tooread tutte le identità del dispositivo, sarà:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Certificati X.509 supportati

È possibile utilizzare qualsiasi tooauthenticate certificato x. 509 un dispositivo con l'IoT Hub. I certificati inclusi sono i seguenti:

* **Un certificato X.509 esistente**. Un dispositivo potrebbe già avere un certificato X.509 associato. dispositivo Hello è possibile utilizzare questo tooauthenticate certificato con l'IoT Hub.
* **Un certificato X-509 auto-generato e auto-firmato**. Un produttore del dispositivo o i distributori interne possono generare questi certificati e archiviare la chiave privata corrispondente di hello (e certificato) su dispositivo hello. È possibile usare strumenti come [OpenSSL][lnk-openssl] e l'utilità [Windows SelfSignedCertificate][lnk-selfsigned] per questo scopo.
* **Certificato X.509 firmato da un'autorità di certificazione**. tooidentify un dispositivo e l'autenticazione con l'IoT Hub, è possibile usare un certificato x. 509 generato e firmato da un'autorità di certificazione (CA). IoT Hub verifica solo tale identificazione digitale hello presentati corrispondente identificazione personale hello configurato. L'hub IOT non viene convalidata la catena di certificati hello.

Un dispositivo può usare un certificato X.509 o un token di sicurezza per l'autenticazione, ma non per entrambi.

### <a name="register-an-x509-certificate-for-a-device"></a>Registrare un certificato X.509 per un dispositivo

Hello [SDK di servizi IoT di Azure per c#] [ lnk-service-sdk] (versione 1.0.8+) supporta la registrazione di un dispositivo che usa un certificato x. 509 per l'autenticazione. Anche altre API come quelle per l'importazione e l'esportazione dei dispositivi supportano i certificati X.509.

### <a name="c-support"></a>Supporto per C\#

Hello **RegistryManager** classe fornisce un modo programmatico di tooregister un dispositivo. In particolare, hello **AddDeviceAsync** e **UpdateDeviceAsync** metodi consentono di tooregister e aggiornare un dispositivo in hello del Registro di sistema di IoT Hub identità. Questi due metodi accettano un'istanza **Device** come input. Hello **dispositivo** classe include un **autenticazione** proprietà che è possibile toospecify primarie e secondarie x. 509 identificazioni personali del certificato. identificazione personale Hello rappresenta un hash SHA-1 del certificato x. 509 hello (archiviato utilizzando la codifica DER binaria). È possibile hello che specifica un'identificazione personale del primaria o un'identificazione personale del secondario o entrambi. Identificazioni personali primarie e secondarie sono toohandle supportati scenari di rollover dei certificati.

> [!NOTE]
> IoT Hub non è necessario né archiviare il certificato x. 509 intera hello, solo identificazione personale hello.

Di seguito è riportato un esempio C\# tooregister frammento di codice un dispositivo utilizzando un certificato x. 509:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Usare un certificato X.509 durante le operazioni di runtime

Hello [dispositivo IoT di Azure SDK per .NET] [ lnk-client-sdk] (versione 1.0.11+) supporta l'utilizzo di hello di certificati x. 509.

### <a name="c-support"></a>Supporto per C\#

classe Hello **DeviceAuthenticationWithX509Certificate** supporta hello creazione di **DeviceClient** istanze tramite un certificato x. 509. certificato x. 509 Hello deve essere nel formato PFX (denominato anche PKCS #12) hello che include la chiave privata di hello.

Di seguito è riportato un frammento di codice di esempio:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Autenticazione personalizzata del dispositivo

È possibile usare l'IoT Hub hello [Registro di sistema di identità] [ lnk-identity-registry] tooconfigure le credenziali di sicurezza per ogni dispositivo e controllo dell'accesso tramite [token] [ lnk-sas-tokens] . Se una soluzione IoT dispone già di una combinazione di identità personalizzato del Registro di sistema e/o l'autenticazione, è consigliabile creare un *servizio token* toointegrate questa infrastruttura con l'IoT Hub. In questo modo, è possibile usare altre funzionalità IoT nella soluzione.

Un servizio token è un servizio cloud personalizzato. Usa un IoT Hub *criterio di accesso condiviso* con **DeviceConnect** autorizzazioni toocreate *con ambito dispositivo* token. Questi token abilitare l'hub IoT tooyour tooconnect un dispositivo.

![Passaggi del modello di servizio token di hello][img-tokenservice]

Ecco i passaggi principali hello del modello di servizio token di hello:

1. Creare i criteri di accesso condiviso dell'hub IoT con autorizzazioni **DeviceConnect** per l'hub IoT. È possibile creare questo criterio in hello [portale di Azure] [ lnk-management-portal] o a livello di codice. il servizio token di Hello utilizza i token di hello toosign questo criterio viene creato.
1. Quando un dispositivo deve tooaccess l'hub IoT, richiede un token firmato dal servizio token. Hello dispositivo può eseguire l'autenticazione con l'identità del dispositivo identità personalizzato del Registro di sistema o di autenticazione schema toodetermine hello che il servizio token di hello utilizza token hello toocreate.
1. il servizio token di Hello restituisce un token. Hello token viene creato utilizzando `/devices/{deviceId}` come `resourceURI`, con `deviceId` come dispositivo hello da autenticare. il servizio token di Hello utilizza il token hello tooconstruct di hello accesso condiviso dei criteri.
1. dispositivo di Hello Usa token hello direttamente con l'hub IoT hello.

> [!NOTE]
> È possibile utilizzare una classe .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] o hello classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un token nel servizio di token.

il servizio token di Hello è possibile impostare scadenza del token hello in base alle esigenze. Quando il token hello scade, l'hub IoT hello server connessione dispositivo hello. Quindi, dispositivo hello deve richiedere un nuovo token dal servizio token di hello. Una scadenza breve aumenta il carico di hello sul dispositivo hello e servizio token di hello.

Per un hub di tooyour tooconnect dispositivo, è necessario comunque aggiungerla toohello del Registro di sistema di IoT Hub identità, anche se hello dispositivo usa un token e non una chiave tooconnect di dispositivo. Pertanto, è possibile continuare controllo di accesso per ogni dispositivo toouse abilitando o disabilitando le identità del dispositivo in hello [Registro di sistema di identità][lnk-identity-registry]. Questo approccio consente di ridurre i rischi di hello di utilizzo di token con ore di scadenza lunga.

### <a name="comparison-with-a-custom-gateway"></a>Confronto con un gateway personalizzato

modello di servizio token di Hello è hello consigliato in modo tooimplement una combinazione di identità personalizzato del Registro di sistema o di autenticazione con l'IoT Hub. Questo modello è consigliato perché l'IoT Hub continua toohandle la maggior parte del traffico di soluzione hello. Tuttavia, se lo schema di autenticazione personalizzato hello è così interconnesse con protocollo hello, potrebbe essere necessario un *gateway personalizzato* tooprocess tutti hello traffico. Un esempio di tale scenario prevede l'uso del [protocollo TLS (Transport Layer Security) e di chiavi precondivise][lnk-tls-psk]. Per ulteriori informazioni, vedere hello [gateway del protocollo] [ lnk-protocols] argomento.

## <a name="reference-topics"></a>Argomenti di riferimento:

Hello argomenti di riferimento seguenti offrono ulteriori informazioni su controllo hub IoT tooyour di accesso.

## <a name="iot-hub-permissions"></a>Autorizzazioni per l'hub IoT

Hello nella tabella seguente elenca le autorizzazioni di hello è possibile usare l'hub IoT accesso tooyour toocontrol.

| Autorizzazione | Note |
| --- | --- |
| **RegistryRead** |Concede l'accesso in lettura toohello identità Registro di sistema. Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry]. <br/>Questa autorizzazione viene usata dai servizi cloud back-end. |
| **RegistryReadWrite** |Concede l'accesso in lettura e scrittura toohello identità Registro di sistema. Per altre informazioni, vedere [Registro delle identità][lnk-identity-registry]. <br/>Questa autorizzazione viene usata dai servizi cloud back-end. |
| **ServiceConnect** |Concede l'accesso toocloud orientati ai servizi comunicazione e gli endpoint di monitoraggio. <br/>Concede l'autorizzazione i messaggi da dispositivo a cloud tooreceive, inviare messaggi da cloud a dispositivo e recuperare hello corrispondente conferma di recapito. <br/>Concede l'autorizzazione tooretrieve recapito riconoscimenti per il file caricato. <br/>Concede l'autorizzazione tooaccess dispositivo gemelli tooupdate tag e le proprietà desiderate, recuperare le proprietà segnalate ed eseguire query. <br/>Questa autorizzazione viene usata dai servizi cloud back-end. |
| **DeviceConnect** |Concede l'accesso gli endpoint orientati toodevice. <br/>Concede l'autorizzazione toosend dispositivo a cloud dei messaggi e ricevere messaggi da cloud a dispositivo. <br/>Concede l'autorizzazione tooperform il caricamento di file da un dispositivo. <br/>Concede l'autorizzazione tooreceive doppi desiderato proprietà notifiche e aggiornamento dispositivo doppio proprietà segnalate. <br/>Carica file di tooperform concede l'autorizzazione. <br/>Questa autorizzazione viene usata dai dispositivi. |

## <a name="additional-reference-material"></a>Materiale di riferimento

Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* [Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* [Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello e la limitazione di comportamenti che si applicano toohello servizio IoT Hub.
* [Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* [Il linguaggio di query di IoT Hub] [ lnk-query] descrive il linguaggio di query hello è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.
* [Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi

Ora si è appreso come toocontrol accedere IoT Hub, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:

* [Utilizzare lo stato del dispositivo gemelli toosynchronize e configurazioni][lnk-devguide-device-twins]
* [Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello seguenti esercitazioni IoT Hub:

* [Introduzione all'hub IoT di Azure][lnk-getstarted-tutorial]
* [La modalità toosend cloud a dispositivo dei messaggi con l'IoT Hub][lnk-c2d-tutorial]
* [Come tooprocess messaggi da dispositivo a cloud IoT Hub][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
