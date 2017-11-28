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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="d0c23-103">Connettere il servizio sicura tooa con proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="d0c23-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="d0c23-104">Questo articolo spiega come tooestablish connessione sicura tra proxy inverso hello e servizi, consentendo un canale sicuro tooend di fine.</span><span class="sxs-lookup"><span data-stu-id="d0c23-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="d0c23-105">La connessione di servizi toosecure è supportata solo quando proxy inverso toolisten configurato su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0c23-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="d0c23-106">Resto del documento hello presuppone che Hello caso.</span><span class="sxs-lookup"><span data-stu-id="d0c23-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="d0c23-107">Fare riferimento troppo[inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverso di hello tooconfigure nell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="d0c23-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="d0c23-108">Stabilire una connessione sicura tra proxy inverso hello e servizi</span><span class="sxs-lookup"><span data-stu-id="d0c23-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="d0c23-109">L'autenticazione tooservices inverso:</span><span class="sxs-lookup"><span data-stu-id="d0c23-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="d0c23-110">Hello proxy inverso identifica tooservices utilizzando il certificato, specificato con ***reverseProxyCertificate*** proprietà hello **Cluster** [sezione tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d0c23-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="d0c23-111">I servizi possono implementare hello logica tooverify hello del certificato utilizzato da proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="d0c23-112">servizi di Hello è possibile specificare dettagli del certificato client hello accettato come impostazioni di configurazione nel pacchetto di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="d0c23-113">Questo può essere letta in fase di esecuzione e usato toovalidate hello certificato presentato dal proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="d0c23-114">Fare riferimento troppo[gestire parametri dell'applicazione](service-fabric-manage-multiple-environment-app-configuration.md) tooadd le impostazioni di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="d0c23-115">Verifica dell'identità del servizio hello tramite hello certificato presentato dal servizio hello inverso:</span><span class="sxs-lookup"><span data-stu-id="d0c23-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="d0c23-116">convalida del certificato server tooperform dei certificati hello presentati dai servizi hello, proxy inverso supporta una delle seguenti opzioni hello: None, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="d0c23-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="d0c23-117">tooselect una di queste tre opzioni, specificare hello **ApplicationCertificateValidationPolicy** nella sezione parametri hello sotto l'elemento ApplicationGateway/Http [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d0c23-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="d0c23-118">Per dettagli sulla configurazione aggiuntiva per ognuna di queste opzioni, vedere la sezione successiva toohello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="d0c23-119">Opzioni di convalida dei certificati del servizio</span><span class="sxs-lookup"><span data-stu-id="d0c23-119">Service certificate validation options</span></span> 

- <span data-ttu-id="d0c23-120">**Nessuna**: Ignora verifica del certificato del servizio proxy hello e stabilisce una connessione sicura hello di proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="d0c23-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="d0c23-121">Questo è il comportamento predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-121">This is hello default behavior.</span></span>
<span data-ttu-id="d0c23-122">Specificare hello **ApplicationCertificateValidationPolicy** con valore **Nessuno** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="d0c23-123">**ServiceCommonNameAndIssuer**: verifica di proxy inverso hello certificato presentato dal servizio hello in base a nome comune del certificato e l'identificazione personale dell'emittente immediato: specificare hello **ApplicationCertificateValidationPolicy**  con valore **ServiceCommonNameAndIssuer** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="d0c23-124">elenco di hello toospecify di nome comune del servizio e le identificazioni personali dell'autorità di certificazione, aggiungere un **Http/ApplicationGateway/ServiceCommonNameAndIssuer** elemento sotto fabricSettings, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d0c23-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="d0c23-125">È possibile aggiungere più nome comune del certificato e coppie di identificazione personale dell'autorità di certificazione nell'elemento di matrice di parametri hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="d0c23-126">Se si sta connettendo proxy inverso di hello endpoint toopresents un certificato che è comune identificazione personale del nome e l'emittente corrisponde a uno dei valori di hello specificati qui, viene stabilito il canale SSL.</span><span class="sxs-lookup"><span data-stu-id="d0c23-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="d0c23-127">Al momento di dettagli del certificato errore toomatch hello, proxy inverso ha esito negativo di richiesta del client hello con un codice di stato 502 (Gateway non valido).</span><span class="sxs-lookup"><span data-stu-id="d0c23-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="d0c23-128">riga di stato HTTP Hello conterrà anche la frase hello "Certificato SSL non valido".</span><span class="sxs-lookup"><span data-stu-id="d0c23-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="d0c23-129">**ServiceCertificateThumbprints**: proxy inverso consentirà di verificare il certificato di servizio proxy hello in base all'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="d0c23-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="d0c23-130">È possibile scegliere toogo questa route quando hello servizi sono configurati con certificati autofirmati: specificare hello **ApplicationCertificateValidationPolicy** con valore **ServiceCertificateThumbprints**nella sezione parametri hello dell'elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="d0c23-131">Specificare anche le identificazioni personali hello con un **ServiceCertificateThumbprints** voce nella sezione parametri di un elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="d0c23-132">Identificazioni personali più possono essere specificate come un elenco delimitato da virgole nel campo valore hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0c23-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

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

<span data-ttu-id="d0c23-133">Se l'identificazione personale hello hello del certificato del server è elencato in questa voce di configurazione, proxy inverso ha esito positivo di connessione SSL hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="d0c23-134">In caso contrario, termina la connessione hello e ha esito negativo hello richiesta del client con un 502 (Gateway non valido).</span><span class="sxs-lookup"><span data-stu-id="d0c23-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="d0c23-135">riga di stato HTTP Hello conterrà anche la frase hello "Certificato SSL non valido".</span><span class="sxs-lookup"><span data-stu-id="d0c23-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="d0c23-136">Logica di scelta dell'endpoint quando i servizi espongono endpoint sicuri e non sicuri</span><span class="sxs-lookup"><span data-stu-id="d0c23-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="d0c23-137">Service Fabric supporta la configurazione di più endpoint per un servizio.</span><span class="sxs-lookup"><span data-stu-id="d0c23-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="d0c23-138">Vedere [Specificare le risorse in un manifesto del servizio](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d0c23-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="d0c23-139">Proxy inverso consente di selezionare una richiesta hello endpoint tooforward hello in base a hello **ListenerName** parametro di query.</span><span class="sxs-lookup"><span data-stu-id="d0c23-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="d0c23-140">Se non viene specificato, è possibile selezionare qualsiasi endpoint dall'elenco di endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="d0c23-141">A questo punto potrebbe essere un endpoint HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0c23-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="d0c23-142">Potrebbero esserci/requisiti di scenari in cui si desidera toooperate di proxy inverso hello in "sola modalità di protezione", ovvero</span><span class="sxs-lookup"><span data-stu-id="d0c23-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="d0c23-143">non si desidera hello sicura proxy inverso tooforward richieste toounsecured endpoint.</span><span class="sxs-lookup"><span data-stu-id="d0c23-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="d0c23-144">È possibile specificando hello **SecureOnlyMode** voce di configurazione con valore **true** nella sezione parametri hello dell'elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="d0c23-145">Quando si opera in **SecureOnlyMode**, se il client è stato specificato un **ListenerName** corrispondente tooan HTTP(unsecured) endpoint, proxy inverso richiesta hello con un codice di stato 404 (non trovato) HTTP non riesce.</span><span class="sxs-lookup"><span data-stu-id="d0c23-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="d0c23-146">Configurare l'autenticazione del certificato client tramite proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="d0c23-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="d0c23-147">Si verifica la terminazione SSL proxy inverso hello e tutti i dati del certificato client hello viene perso.</span><span class="sxs-lookup"><span data-stu-id="d0c23-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="d0c23-148">Per l'autenticazione del certificato client tooperform servizi hello, impostare hello **ForwardClientCertificate** impostazione nella sezione parametri hello dell'elemento di ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="d0c23-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="d0c23-149">Quando **ForwardClientCertificate** è troppo**false**, inversa proxy non verrà richiesta per il certificato client hello relativo handshake SSL con client hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="d0c23-150">Questo è il comportamento predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="d0c23-151">Quando **ForwardClientCertificate** è troppo**true**, richieste di proxy per il certificato del client hello inversa relativo handshake SSL con client hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="d0c23-152">Verrà quindi inoltra client hello dati del certificato in un'intestazione HTTP personalizzata denominata **X-Client-certificato**.</span><span class="sxs-lookup"><span data-stu-id="d0c23-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="d0c23-153">valore dell'intestazione Hello è hello di stringa di formato con codificata base64 PEM del certificato hello del client.</span><span class="sxs-lookup"><span data-stu-id="d0c23-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="d0c23-154">servizio Hello può avere esito positivo/non superato richiesta hello con codice di stato appropriato dopo aver esaminato i dati del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="d0c23-155">Se il client di hello non è presente un certificato, proxy inverso inoltra un'intestazione vuota e consentire i case di hello handle servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="d0c23-156">Il proxy inverso è un semplice server d'inoltro,</span><span class="sxs-lookup"><span data-stu-id="d0c23-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="d0c23-157">Non esegue alcuna convalida del certificato hello del client.</span><span class="sxs-lookup"><span data-stu-id="d0c23-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d0c23-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0c23-158">Next steps</span></span>
* <span data-ttu-id="d0c23-159">Fare riferimento troppo[configurare servizi di proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) per Gestione risorse di Azure tooconfigure proxy inverso sicuro con le opzioni di convalida certificato di servizio diverso hello esempi di modello.</span><span class="sxs-lookup"><span data-stu-id="d0c23-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="d0c23-160">Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d0c23-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="d0c23-161">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="d0c23-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d0c23-162">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d0c23-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d0c23-163">Gestire i certificati cluster</span><span class="sxs-lookup"><span data-stu-id="d0c23-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
