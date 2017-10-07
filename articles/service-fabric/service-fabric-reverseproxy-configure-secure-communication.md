---
title: aaaAzure Service Fabric invertire una comunicazione protetta proxy | Documenti Microsoft
description: Configurare la comunicazione di proxy inverso tooenable protezione end-to-end.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Connettere il servizio sicura tooa con proxy inverso hello

Questo articolo spiega come tooestablish connessione sicura tra proxy inverso hello e servizi, consentendo un canale sicuro tooend di fine.

La connessione di servizi toosecure è supportata solo quando proxy inverso toolisten configurato su HTTPS. Resto del documento hello presuppone che Hello caso.
Fare riferimento troppo[inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverso di hello tooconfigure nell'infrastruttura del servizio.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Stabilire una connessione sicura tra proxy inverso hello e servizi 

### <a name="reverse-proxy-authenticating-tooservices"></a>L'autenticazione tooservices inverso:
Hello proxy inverso identifica tooservices utilizzando il certificato, specificato con ***reverseProxyCertificate*** proprietà hello **Cluster** [sezione tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md). I servizi possono implementare hello logica tooverify hello del certificato utilizzato da proxy inverso hello. servizi di Hello è possibile specificare dettagli del certificato client hello accettato come impostazioni di configurazione nel pacchetto di configurazione hello. Questo può essere letta in fase di esecuzione e usato toovalidate hello certificato presentato dal proxy inverso hello. Fare riferimento troppo[gestire parametri dell'applicazione](service-fabric-manage-multiple-environment-app-configuration.md) tooadd le impostazioni di configurazione hello. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Verifica dell'identità del servizio hello tramite hello certificato presentato dal servizio hello inverso:
convalida del certificato server tooperform dei certificati hello presentati dai servizi hello, proxy inverso supporta una delle seguenti opzioni hello: None, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.
tooselect una di queste tre opzioni, specificare hello **ApplicationCertificateValidationPolicy** nella sezione parametri hello sotto l'elemento ApplicationGateway/Http [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Per dettagli sulla configurazione aggiuntiva per ognuna di queste opzioni, vedere la sezione successiva toohello.

### <a name="service-certificate-validation-options"></a>Opzioni di convalida dei certificati del servizio 

- **Nessuna**: Ignora verifica del certificato del servizio proxy hello e stabilisce una connessione sicura hello di proxy inverso. Questo è il comportamento predefinito di hello.
Specificare hello **ApplicationCertificateValidationPolicy** con valore **Nessuno** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.

- **ServiceCommonNameAndIssuer**: verifica di proxy inverso hello certificato presentato dal servizio hello in base a nome comune del certificato e l'identificazione personale dell'emittente immediato: specificare hello **ApplicationCertificateValidationPolicy**  con valore **ServiceCommonNameAndIssuer** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

elenco di hello toospecify di nome comune del servizio e le identificazioni personali dell'autorità di certificazione, aggiungere un **Http/ApplicationGateway/ServiceCommonNameAndIssuer** elemento sotto fabricSettings, come illustrato di seguito. È possibile aggiungere più nome comune del certificato e coppie di identificazione personale dell'autorità di certificazione nell'elemento di matrice di parametri hello. 

Se si sta connettendo proxy inverso di hello endpoint toopresents un certificato che è comune identificazione personale del nome e l'emittente corrisponde a uno dei valori di hello specificati qui, viene stabilito il canale SSL. Al momento di dettagli del certificato errore toomatch hello, proxy inverso ha esito negativo di richiesta del client hello con un codice di stato 502 (Gateway non valido). riga di stato HTTP Hello conterrà anche la frase hello "Certificato SSL non valido". 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: proxy inverso consentirà di verificare il certificato di servizio proxy hello in base all'identificazione personale. È possibile scegliere toogo questa route quando hello servizi sono configurati con certificati autofirmati: specificare hello **ApplicationCertificateValidationPolicy** con valore **ServiceCertificateThumbprints**nella sezione parametri hello dell'elemento di ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Specificare anche le identificazioni personali hello con un **ServiceCertificateThumbprints** voce nella sezione parametri di un elemento di ApplicationGateway/Http. Identificazioni personali più possono essere specificate come un elenco delimitato da virgole nel campo valore hello, come illustrato di seguito:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Se l'identificazione personale hello hello del certificato del server è elencato in questa voce di configurazione, proxy inverso ha esito positivo di connessione SSL hello. In caso contrario, termina la connessione hello e ha esito negativo hello richiesta del client con un 502 (Gateway non valido). riga di stato HTTP Hello conterrà anche la frase hello "Certificato SSL non valido".

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Logica di scelta dell'endpoint quando i servizi espongono endpoint sicuri e non sicuri
Service Fabric supporta la configurazione di più endpoint per un servizio. Vedere [Specificare le risorse in un manifesto del servizio](service-fabric-service-manifest-resources.md).

Proxy inverso consente di selezionare una richiesta hello endpoint tooforward hello in base a hello **ListenerName** parametro di query. Se non viene specificato, è possibile selezionare qualsiasi endpoint dall'elenco di endpoint hello. A questo punto potrebbe essere un endpoint HTTP o HTTPS. Potrebbero esserci/requisiti di scenari in cui si desidera toooperate di proxy inverso hello in "sola modalità di protezione", ovvero non si desidera hello sicura proxy inverso tooforward richieste toounsecured endpoint. È possibile specificando hello **SecureOnlyMode** voce di configurazione con valore **true** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> Quando si opera in **SecureOnlyMode**, se il client è stato specificato un **ListenerName** corrispondente tooan HTTP(unsecured) endpoint, proxy inverso richiesta hello con un codice di stato 404 (non trovato) HTTP non riesce.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Configurare l'autenticazione del certificato client tramite proxy inverso hello
Si verifica la terminazione SSL proxy inverso hello e tutti i dati del certificato client hello viene perso. Per l'autenticazione del certificato client tooperform servizi hello, impostare hello **ForwardClientCertificate** impostazione nella sezione parametri hello dell'elemento di ApplicationGateway/Http.

1. Quando **ForwardClientCertificate** è troppo**false**, inversa proxy non verrà richiesta per il certificato client hello relativo handshake SSL con client hello.
Questo è il comportamento predefinito di hello.

2. Quando **ForwardClientCertificate** è troppo**true**, richieste di proxy per il certificato del client hello inversa relativo handshake SSL con client hello.
Verrà quindi inoltra client hello dati del certificato in un'intestazione HTTP personalizzata denominata **X-Client-certificato**. valore dell'intestazione Hello è hello di stringa di formato con codificata base64 PEM del certificato hello del client. servizio Hello può avere esito positivo/non superato richiesta hello con codice di stato appropriato dopo aver esaminato i dati del certificato hello.
Se il client di hello non è presente un certificato, proxy inverso inoltra un'intestazione vuota e consentire i case di hello handle servizio hello.

> Il proxy inverso è un semplice server d'inoltro, Non esegue alcuna convalida del certificato hello del client.


## <a name="next-steps"></a>Passaggi successivi
* Fare riferimento troppo[configurare servizi di proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) per Gestione risorse di Azure tooconfigure proxy inverso sicuro con le opzioni di convalida certificato di servizio diverso hello esempi di modello.
* Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Chiamate di procedura remota con i Reliable Services remoti](service-fabric-reliable-services-communication-remoting.md)
* [Web API che usa OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Gestire i certificati cluster](service-fabric-cluster-security-update-certs-azure.md)
