---
title: Comunicazione protetta con il proxy inverso di Azure Service Fabric | Microsoft Docs
description: Configurare il proxy inverso per abilitare la comunicazione end-to-end protetta.
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="c0177-103">Connettersi a un servizio protetto con il proxy inverso</span><span class="sxs-lookup"><span data-stu-id="c0177-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="c0177-104">In questo articolo viene spiegato come stabilire una connessione protetta tra il proxy inverso e i servizi, abilitando un canale protetto end-to-end.</span><span class="sxs-lookup"><span data-stu-id="c0177-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="c0177-105">La connessione ai servizi protetti è supportata solo quando il proxy inverso è configurato per l'ascolto su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0177-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="c0177-106">In questo documento si presuppone che questo sia il caso.</span><span class="sxs-lookup"><span data-stu-id="c0177-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="c0177-107">Fare riferimento a [Proxy inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) per configurare il proxy inverso in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0177-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="c0177-108">Stabilire una connessione protetta tra il proxy inverso e i servizi</span><span class="sxs-lookup"><span data-stu-id="c0177-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="c0177-109">Autenticazione del proxy inverso per i servizi:</span><span class="sxs-lookup"><span data-stu-id="c0177-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="c0177-110">Il proxy inverso si autoidentifica per i servizi usando il certificato, specificato con la proprietà ***reverseProxyCertificate*** nella [sezione relativa al tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md) del **cluster** .</span><span class="sxs-lookup"><span data-stu-id="c0177-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="c0177-111">I servizi possono implementare la logica per verificare il certificato presentato dal proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="c0177-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="c0177-112">I servizi possono specificare i dettagli del certificato client accettati come impostazioni di configurazione nel pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c0177-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="c0177-113">Questo può essere letto in fase di runtime e usato per convalidare il certificato presentato dal proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="c0177-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="c0177-114">Fare riferimento a [Gestire i parametri dell'applicazione](service-fabric-manage-multiple-environment-app-configuration.md) per aggiungere le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c0177-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="c0177-115">Verifica dell'identità del servizio da parte del proxy inverso tramite il certificato presentato dal servizio:</span><span class="sxs-lookup"><span data-stu-id="c0177-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="c0177-116">Per eseguire la convalida del certificato del server per i certificati presentati dai servizi, il proxy inverso supporta una delle opzioni seguenti: None, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="c0177-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="c0177-117">Per selezionare una di queste tre opzioni, specificare **ApplicationCertificateValidationPolicy** nella sezione dei parametri dell'elemento ApplicationGateway/Http in [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c0177-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="c0177-118">Fare riferimento alla sezione successiva per informazioni sulla configurazione aggiuntiva per ognuna di queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="c0177-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="c0177-119">Opzioni di convalida dei certificati del servizio</span><span class="sxs-lookup"><span data-stu-id="c0177-119">Service certificate validation options</span></span> 

- <span data-ttu-id="c0177-120">**None**: il proxy inverso ignora la verifica del certificato del servizio di proxy e stabilisce la connessione sicura.</span><span class="sxs-lookup"><span data-stu-id="c0177-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="c0177-121">Questo è il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="c0177-121">This is the default behavior.</span></span>
<span data-ttu-id="c0177-122">Specificare **ApplicationCertificateValidationPolicy** con il valore **None** nella sezione dei parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="c0177-123">**ServiceCommonNameAndIssuer**: il proxy inverso verifica il certificato presentato dal servizio in base al nome comune del certificato e all'identificazione personale immediata dell'autorità di certificazione: specificare **ApplicationCertificateValidationPolicy** con valore **ServiceCommonNameAndIssuer** nella sezione dei parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="c0177-124">Per specificare l'elenco del nome comune del servizio e l'identificazione personale dell'autorità di certificazione, aggiungere un elemento **ApplicationGateway/Http/ServiceCommonNameAndIssuer** in fabricsettings, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c0177-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="c0177-125">Nell'elemento della matrice di parametri è possibile aggiungere associazioni multiple del nome comune del certificato e dell'identificazione personale dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="c0177-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="c0177-126">Se il proxy inverso dell'endpoint si connette per presentare un certificato il cui nome comune e l'identificazione personale dell'autorità di certificazione corrisponde a uno qualsiasi dei valori specificati in questo caso, viene stabilito il canale SSL.</span><span class="sxs-lookup"><span data-stu-id="c0177-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="c0177-127">In caso di errore nella corrispondenza dei dettagli del certificato, il proxy inverso non esegue correttamente la richiesta del client e presenta un codice di stato 502, ovvero Gateway non valido.</span><span class="sxs-lookup"><span data-stu-id="c0177-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="c0177-128">La riga di stato HTTP conterrà anche la frase "Invalid SSL Certificate" (Certificato SSL non valido).</span><span class="sxs-lookup"><span data-stu-id="c0177-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="c0177-129">**ServiceCertificateThumbprints**: il proxy inverso consente di verificare il certificato del servizio del proxy in base all'identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="c0177-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="c0177-130">È possibile scegliere di intraprendere questa strada quando i servizi vengono configurati con certificati autofirmati : specificare **ApplicationCertificateValidationPolicy** con valore **ServiceCertificateThumbprints** nella sezione dei parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="c0177-131">Specificare anche le identificazioni personali con una voce **ServiceCertificateThumbprints** nella sezione parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="c0177-132">Nel campo del valore è possibile specificare più identificazioni personali come un elenco delimitato da virgole, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c0177-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="c0177-133">Se l'identificazione personale del certificato del server è elencata in questa voce di configurazione, il proxy inverso esegue correttamente la connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="c0177-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="c0177-134">In caso contrario, termina la connessione e non esegue correttamente la richiesta del client con un errore 502, ovvero Gateway non valido.</span><span class="sxs-lookup"><span data-stu-id="c0177-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="c0177-135">La riga di stato HTTP conterrà anche la frase "Invalid SSL Certificate" (Certificato SSL non valido).</span><span class="sxs-lookup"><span data-stu-id="c0177-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="c0177-136">Logica di scelta dell'endpoint quando i servizi espongono endpoint sicuri e non sicuri</span><span class="sxs-lookup"><span data-stu-id="c0177-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="c0177-137">Service Fabric supporta la configurazione di più endpoint per un servizio.</span><span class="sxs-lookup"><span data-stu-id="c0177-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="c0177-138">Vedere [Specificare le risorse in un manifesto del servizio](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c0177-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="c0177-139">Il proxy inverso consente di selezionare uno degli endpoint per inoltrare la richiesta in base al parametro di query **ListenerName**.</span><span class="sxs-lookup"><span data-stu-id="c0177-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="c0177-140">Se non viene specificato, viene scelto un endpoint qualsiasi nell'elenco degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="c0177-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="c0177-141">A questo punto potrebbe essere un endpoint HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0177-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="c0177-142">Potrebbero verificarsi situazioni in cui si desidera o è necessario che il proxy inverso funzioni "solo in modalità protetta",</span><span class="sxs-lookup"><span data-stu-id="c0177-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="c0177-143">per evitare che si inoltrino richieste agli endpoint non protetti.</span><span class="sxs-lookup"><span data-stu-id="c0177-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="c0177-144">A tale scopo è necessario impostare il valore della voce della configurazione **SecureOnlyMode** su **true** nella sezione dei parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="c0177-145">Quando si opera in **SecureOnlyMode**, se il client ha specificato un **ListenerName** corrispondente a un endpoint HTTP, non sicuro, il proxy inverso non esegue correttamente la richiesta con un codice di stato HTTP 404, ovvero Non trovato.</span><span class="sxs-lookup"><span data-stu-id="c0177-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="c0177-146">Configurazione dell'autenticazione del certificato client tramite il proxy inverso</span><span class="sxs-lookup"><span data-stu-id="c0177-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="c0177-147">La terminazione SSL si verifica sul proxy inverso e si perdono tutti i dati del certificato client.</span><span class="sxs-lookup"><span data-stu-id="c0177-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="c0177-148">Affinché i servizi eseguano l'autenticazione del certificato client, impostare l'impostazione **ForwardClientCertificate** nella sezione dei parametri dell'elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="c0177-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="c0177-149">Quando **ForwardClientCertificate** è impostato su **false**, il proxy inverso non richiederà il certificato del client durante l'handshake SSL con il client.</span><span class="sxs-lookup"><span data-stu-id="c0177-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="c0177-150">Questo è il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="c0177-150">This is the default behavior.</span></span>

2. <span data-ttu-id="c0177-151">Quando **ForwardClientCertificate** è impostato su **true**, il proxy inverso richiede il certificato del client durante l'handshake SSL con il client.</span><span class="sxs-lookup"><span data-stu-id="c0177-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="c0177-152">I dati del certificato client verranno quindi inviati in un'intestazione HTTP personalizzata denominata **X-Client-Certificate**.</span><span class="sxs-lookup"><span data-stu-id="c0177-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="c0177-153">Il valore dell'intestazione è la stringa in formato PEM con codifica base64 del certificato del client.</span><span class="sxs-lookup"><span data-stu-id="c0177-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="c0177-154">Il servizio può eseguire correttamente o meno la richiesta con il codice di stato appropriato dopo aver esaminato i dati del certificato.</span><span class="sxs-lookup"><span data-stu-id="c0177-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="c0177-155">Se il client non presenta un certificato, il proxy inverso inoltra un'intestazione vuota e il caso viene gestito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="c0177-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="c0177-156">Il proxy inverso è un semplice server d'inoltro,</span><span class="sxs-lookup"><span data-stu-id="c0177-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="c0177-157">pertanto non esegue alcuna convalida del certificato del client.</span><span class="sxs-lookup"><span data-stu-id="c0177-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0177-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0177-158">Next steps</span></span>
* <span data-ttu-id="c0177-159">Fare riferimento a [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) (Configurare il proxy inverso per la connessione ai servizi protetti) per il modello di Azure Resource Manager per configurare il proxy inverso protetto con le diverse opzioni di convalida del certificato del servizio .</span><span class="sxs-lookup"><span data-stu-id="c0177-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="c0177-160">Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c0177-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="c0177-161">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="c0177-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="c0177-162">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c0177-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c0177-163">Gestire i certificati cluster</span><span class="sxs-lookup"><span data-stu-id="c0177-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
