---
title: Panoramica del Servizio metadati dell'istanza di Azure | Microsoft Docs
description: Interfaccia RESTful per ottenere informazioni sugli eventi di calcolo, di rete e di manutenzione previsti della macchina virtuale.
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="0c302-103">Servizio metadati dell'istanza di Azure</span><span class="sxs-lookup"><span data-stu-id="0c302-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="0c302-104">Il Servizio metadati dell'istanza di Azure fornisce informazioni sull'esecuzione delle istanze di macchine virtuali che possono essere utilizzate per gestire e configurare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0c302-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="0c302-105">Le informazioni includono ad esempio SKU, configurazione di rete ed eventi di manutenzione previsti.</span><span class="sxs-lookup"><span data-stu-id="0c302-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="0c302-106">Per altre informazioni sul tipo di informazioni disponibili, vedere le [categorie di metadati](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="0c302-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="0c302-107">Il Servizio metadati dell'istanza di Azure è un endpoint REST accessibile a tutte le macchine virtuali IaaS create tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0c302-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0c302-108">L'endpoint è disponibile a un indirizzo IP non instradabile noto (`169.254.169.254`) a cui è possibile accedere solo dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c302-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="0c302-109">Informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="0c302-109">Important information</span></span>

<span data-ttu-id="0c302-110">Questo servizio è **disponibile a livello generale** nelle aree globali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="0c302-111">È in anteprima pubblica per il cloud di Azure Germania, per la Cina e per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="0c302-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="0c302-112">Il servizio riceve regolarmente aggiornamenti per esporre nuove informazioni sulle istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0c302-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="0c302-113">Questa pagina riporta le [categorie di dati](#instance-metadata-data-categories) attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="0c302-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="0c302-114">Disponibilità del servizio</span><span class="sxs-lookup"><span data-stu-id="0c302-114">Service Availability</span></span>
<span data-ttu-id="0c302-115">Il servizio è disponibile a livello generale in tutte le aree globali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="0c302-116">È in anteprima pubblica nelle aree Germania, Cina  ed enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="0c302-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="0c302-117">Regioni</span><span class="sxs-lookup"><span data-stu-id="0c302-117">Regions</span></span>                                        | <span data-ttu-id="0c302-118">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="0c302-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="0c302-119">Tutte le aree globali di Azure con disponibilità a livello generale</span><span class="sxs-lookup"><span data-stu-id="0c302-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="0c302-120">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="0c302-120">Generally Available</span></span> 
[<span data-ttu-id="0c302-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="0c302-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="0c302-122">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0c302-122">In Preview</span></span> 
[<span data-ttu-id="0c302-123">Azure per la Cina</span><span class="sxs-lookup"><span data-stu-id="0c302-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="0c302-124">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0c302-124">In Preview</span></span>
[<span data-ttu-id="0c302-125">Azure Germania</span><span class="sxs-lookup"><span data-stu-id="0c302-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="0c302-126">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0c302-126">In Preview</span></span>

<span data-ttu-id="0c302-127">Questa tabella viene aggiornata quando il servizio viene reso disponibile in altri cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="0c302-128">Per provare il Servizio metadati dell'istanza, creare una macchina virtuale da [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o dal [portale di Azure](http://portal.azure.com) nelle aree di cui sopra e seguire gli esempi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="0c302-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="0c302-129">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="0c302-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="0c302-130">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="0c302-130">Versioning</span></span>
<span data-ttu-id="0c302-131">Il Servizio metadati dell'istanza è con versione.</span><span class="sxs-lookup"><span data-stu-id="0c302-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0c302-132">Le versioni sono obbligatorie e la versione corrente è `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="0c302-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-133">Le versioni precedenti di anteprima di eventi pianificati {ultima} sono supportate come versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="0c302-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="0c302-134">Questo formato non è più supportato e verrà rimosso in futuro.</span><span class="sxs-lookup"><span data-stu-id="0c302-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="0c302-135">Quando si aggiungono versioni più recenti, quelle precedenti sono comunque accessibili per la compatibilità, se gli script presentano dipendenze in formati di dati specifici.</span><span class="sxs-lookup"><span data-stu-id="0c302-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="0c302-136">Si noti però che la versione di anteprima corrente (2017-03-01) potrebbe non essere disponibile quando il servizio è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="0c302-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0c302-137">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="0c302-137">Using Headers</span></span>
<span data-ttu-id="0c302-138">Quando si eseguono query sul Servizio metadati dell'istanza, è necessario specificare l'intestazione `Metadata: true` per garantire che la richiesta non sia stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="0c302-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="0c302-139">Recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="0c302-139">Retrieving metadata</span></span>

<span data-ttu-id="0c302-140">I metadati dell'istanza sono disponibili per l'esecuzione di macchine virtuali create e gestite tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0c302-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0c302-141">Accedere a tutte le categorie di dati per un'istanza di macchina virtuale utilizzando la richiesta seguente:</span><span class="sxs-lookup"><span data-stu-id="0c302-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="0c302-142">Tutte le query dei metadati dell'istanza fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="0c302-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="0c302-143">Output dei dati</span><span class="sxs-lookup"><span data-stu-id="0c302-143">Data output</span></span>
<span data-ttu-id="0c302-144">Per impostazione predefinita, il Servizio metadati dell'istanza restituisce i dati in formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="0c302-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="0c302-145">Tuttavia, API diverse possono restituire dati in formati diversi se necessario.</span><span class="sxs-lookup"><span data-stu-id="0c302-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="0c302-146">La tabella seguente costituisce un riferimento per gli altri formati di dati che le API possono supportare.</span><span class="sxs-lookup"><span data-stu-id="0c302-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="0c302-147">API</span><span class="sxs-lookup"><span data-stu-id="0c302-147">API</span></span> | <span data-ttu-id="0c302-148">Formato dati predefinito</span><span class="sxs-lookup"><span data-stu-id="0c302-148">Default Data Format</span></span> | <span data-ttu-id="0c302-149">Altri formati</span><span class="sxs-lookup"><span data-stu-id="0c302-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="0c302-150">/instance</span><span class="sxs-lookup"><span data-stu-id="0c302-150">/instance</span></span> | <span data-ttu-id="0c302-151">json</span><span class="sxs-lookup"><span data-stu-id="0c302-151">json</span></span> | <span data-ttu-id="0c302-152">text</span><span class="sxs-lookup"><span data-stu-id="0c302-152">text</span></span>
<span data-ttu-id="0c302-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0c302-153">/scheduledevents</span></span> | <span data-ttu-id="0c302-154">json</span><span class="sxs-lookup"><span data-stu-id="0c302-154">json</span></span> | <span data-ttu-id="0c302-155">Nessuno</span><span class="sxs-lookup"><span data-stu-id="0c302-155">none</span></span>

<span data-ttu-id="0c302-156">Per accedere a un formato di risposta non predefinito, specificare il formato richiesto come parametro di stringa di query nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="0c302-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="0c302-157">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0c302-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="0c302-158">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="0c302-158">Security</span></span>
<span data-ttu-id="0c302-159">L'endpoint del Servizio metadati dell'istanza è accessibile solo dall'istanza della macchina virtuale in esecuzione su un indirizzo IP non instradabile.</span><span class="sxs-lookup"><span data-stu-id="0c302-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="0c302-160">Inoltre, qualsiasi richiesta con intestazione `X-Forwarded-For` viene rifiutata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="0c302-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="0c302-161">È necessario anche che le richieste includano l'intestazione `Metadata: true` per garantire che la richiesta sia stata destinata direttamente e non faccia parte di un reindirizzamento non intenzionale.</span><span class="sxs-lookup"><span data-stu-id="0c302-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="0c302-162">Tipi di errore</span><span class="sxs-lookup"><span data-stu-id="0c302-162">Error</span></span>
<span data-ttu-id="0c302-163">In caso di elementi dati non trovati o di richiesta non valida, il Servizio metadati dell'istanza restituisce errori HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="0c302-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="0c302-164">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0c302-164">For example:</span></span>

<span data-ttu-id="0c302-165">Codice di stato HTTP</span><span class="sxs-lookup"><span data-stu-id="0c302-165">HTTP Status Code</span></span> | <span data-ttu-id="0c302-166">Motivo</span><span class="sxs-lookup"><span data-stu-id="0c302-166">Reason</span></span>
----------------|-------
<span data-ttu-id="0c302-167">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0c302-167">200 OK</span></span> |
<span data-ttu-id="0c302-168">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="0c302-168">400 Bad Request</span></span> | <span data-ttu-id="0c302-169">Intestazione `Metadata: true` mancante</span><span class="sxs-lookup"><span data-stu-id="0c302-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="0c302-170">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="0c302-170">404 Not Found</span></span> | <span data-ttu-id="0c302-171">L'elemento richiesto non esiste</span><span class="sxs-lookup"><span data-stu-id="0c302-171">The requested element does't exist</span></span> 
<span data-ttu-id="0c302-172">405 - Metodo non consentito</span><span class="sxs-lookup"><span data-stu-id="0c302-172">405 Method Not Allowed</span></span> | <span data-ttu-id="0c302-173">Sono supportate solo le richieste `GET` e `POST`</span><span class="sxs-lookup"><span data-stu-id="0c302-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="0c302-174">429 - Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="0c302-174">429 Too Many Requests</span></span> | <span data-ttu-id="0c302-175">L'API supporta attualmente un massimo di 5 query al secondo</span><span class="sxs-lookup"><span data-stu-id="0c302-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="0c302-176">500 - Errore del servizio</span><span class="sxs-lookup"><span data-stu-id="0c302-176">500 Service Error</span></span>     | <span data-ttu-id="0c302-177">Ripetere l'operazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="0c302-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="0c302-178">esempi</span><span class="sxs-lookup"><span data-stu-id="0c302-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-179">Tutte le risposte delle API sono stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="0c302-179">All API responses are JSON strings.</span></span> <span data-ttu-id="0c302-180">Tutte le risposte di esempio che seguono sono di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="0c302-181">Recupero delle informazioni di rete</span><span class="sxs-lookup"><span data-stu-id="0c302-181">Retrieving network information</span></span>

<span data-ttu-id="0c302-182">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="0c302-183">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-184">La risposta è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0c302-184">The response is a JSON string.</span></span> <span data-ttu-id="0c302-185">La risposta di esempio che segue è di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-185">The following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="0c302-186">Recupero dell'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="0c302-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="0c302-187">Recupero di tutti i metadati per un'istanza</span><span class="sxs-lookup"><span data-stu-id="0c302-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="0c302-188">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="0c302-189">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-190">La risposta è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0c302-190">The response is a JSON string.</span></span> <span data-ttu-id="0c302-191">La risposta di esempio che segue è di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-191">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="0c302-192">Recupero dei metadati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="0c302-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="0c302-193">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-193">**Request**</span></span>

<span data-ttu-id="0c302-194">I metadati dell'istanza possono essere recuperati in Windows tramite l'utilità PowerShell `curl`:</span><span class="sxs-lookup"><span data-stu-id="0c302-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="0c302-195">Oppure tramite il cmdlet `Invoke-RestMethod`:</span><span class="sxs-lookup"><span data-stu-id="0c302-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="0c302-196">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-197">La risposta è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0c302-197">The response is a JSON string.</span></span> <span data-ttu-id="0c302-198">La risposta di esempio che segue è di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-198">The following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="0c302-199">Categorie di dati dei metadati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="0c302-199">Instance metadata data categories</span></span>
<span data-ttu-id="0c302-200">Tramite il Servizio metadati dell'istanza sono disponibili le categorie di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c302-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="0c302-201">Dati</span><span class="sxs-lookup"><span data-stu-id="0c302-201">Data</span></span> | <span data-ttu-id="0c302-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0c302-202">Description</span></span>
-----|------------
<span data-ttu-id="0c302-203">location</span><span class="sxs-lookup"><span data-stu-id="0c302-203">location</span></span> | <span data-ttu-id="0c302-204">Area di Azure in cui la macchina virtuale è in esecuzione</span><span class="sxs-lookup"><span data-stu-id="0c302-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="0c302-205">name</span><span class="sxs-lookup"><span data-stu-id="0c302-205">name</span></span> | <span data-ttu-id="0c302-206">Nome della VM</span><span class="sxs-lookup"><span data-stu-id="0c302-206">Name of the VM</span></span> 
<span data-ttu-id="0c302-207">offer</span><span class="sxs-lookup"><span data-stu-id="0c302-207">offer</span></span> | <span data-ttu-id="0c302-208">Offre informazioni per l'immagine della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c302-208">Offer information for the VM image.</span></span> <span data-ttu-id="0c302-209">Questo valore è presente solo per le immagini distribuite dalla raccolta di immagini di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="0c302-210">publisher</span><span class="sxs-lookup"><span data-stu-id="0c302-210">publisher</span></span> | <span data-ttu-id="0c302-211">Autore dell'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-211">Publisher of the VM image</span></span>
<span data-ttu-id="0c302-212">sku</span><span class="sxs-lookup"><span data-stu-id="0c302-212">sku</span></span> | <span data-ttu-id="0c302-213">SKU specifica per l'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="0c302-214">version</span><span class="sxs-lookup"><span data-stu-id="0c302-214">version</span></span> | <span data-ttu-id="0c302-215">Versione dell'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-215">Version of the VM image</span></span> 
<span data-ttu-id="0c302-216">osType</span><span class="sxs-lookup"><span data-stu-id="0c302-216">osType</span></span> | <span data-ttu-id="0c302-217">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="0c302-217">Linux or Windows</span></span> 
<span data-ttu-id="0c302-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="0c302-218">platformUpdateDomain</span></span> |  <span data-ttu-id="0c302-219">[Dominio di aggiornamento](virtual-machines-windows-manage-availability.md) in cui è in esecuzione la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="0c302-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="0c302-220">platformFaultDomain</span></span> | <span data-ttu-id="0c302-221">[Dominio di errore](virtual-machines-windows-manage-availability.md) in cui è in esecuzione la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="0c302-222">vmId</span><span class="sxs-lookup"><span data-stu-id="0c302-222">vmId</span></span> | <span data-ttu-id="0c302-223">[Identificatore univoco](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="0c302-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="0c302-224">vmSize</span></span> | [<span data-ttu-id="0c302-225">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="0c302-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="0c302-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="0c302-227">Indirizzo IPv4 locale della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="0c302-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0c302-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="0c302-229">Indirizzo IPv4 pubblico della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="0c302-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="0c302-230">subnet/address</span></span> | <span data-ttu-id="0c302-231">Indirizzo della subnet della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-231">Subnet address of the VM</span></span>
<span data-ttu-id="0c302-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="0c302-232">subnet/prefix</span></span> | <span data-ttu-id="0c302-233">Prefisso della subnet, ad esempio 24</span><span class="sxs-lookup"><span data-stu-id="0c302-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="0c302-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="0c302-234">ipv6/ipAddress</span></span> | <span data-ttu-id="0c302-235">Indirizzo IPv6 locale della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="0c302-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="0c302-236">macAddress</span></span> | <span data-ttu-id="0c302-237">Indirizzo mac della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-237">VM mac address</span></span> 
<span data-ttu-id="0c302-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0c302-238">scheduledevents</span></span> | <span data-ttu-id="0c302-239">Attualmente in anteprima pubblica. Vedere [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="0c302-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="0c302-240">Scenari di uso di esempio</span><span class="sxs-lookup"><span data-stu-id="0c302-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="0c302-241">Rilevamento della macchina virtuale in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="0c302-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="0c302-242">Come provider di servizi, potrebbe essere necessario tenere traccia del numero di macchine virtuali che eseguono il proprio software o avere agenti che devono verificare l'univocità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c302-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="0c302-243">Per poter ottenere un ID univoco per una macchina virtuale, usare il campo `vmId` dal Servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0c302-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="0c302-244">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="0c302-245">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="0c302-246">Posizionamento di contenitori, dominio di aggiornamento/errore basato su partizioni dati</span><span class="sxs-lookup"><span data-stu-id="0c302-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="0c302-247">Per alcuni scenari, il posizionamento di repliche dati diverse è di importanza primaria.</span><span class="sxs-lookup"><span data-stu-id="0c302-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="0c302-248">Ad esempio per il [posizionamento delle repliche HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o per il posizionamento di contenitori tramite un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) è necessario conoscere il `platformFaultDomain` e il `platformUpdateDomain` in cui la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0c302-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="0c302-249">È possibile eseguire query su questi dati direttamente tramite il Servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0c302-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="0c302-250">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="0c302-251">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="0c302-252">Ottenere altre informazioni sulla macchina virtuale durante la richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="0c302-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="0c302-253">Come provider di servizi è possibile ricevere una chiamata di supporto per la quale occorre sapere altre informazioni sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c302-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="0c302-254">Chiedere al cliente di condividere i metadati di calcolo può risultare utile per avere informazioni di base che consentano al personale del supporto tecnico di conoscere il tipo di macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="0c302-255">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0c302-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="0c302-256">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0c302-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c302-257">La risposta è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0c302-257">The response is a JSON string.</span></span> <span data-ttu-id="0c302-258">La risposta di esempio che segue è di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-258">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="0c302-259">Esempi di chiamate del Servizio metadati con diversi linguaggi all'interno della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c302-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="0c302-260">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="0c302-260">Language</span></span> | <span data-ttu-id="0c302-261">Esempio</span><span class="sxs-lookup"><span data-stu-id="0c302-261">Example</span></span> 
---------|----------------
<span data-ttu-id="0c302-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="0c302-262">Ruby</span></span>     | <span data-ttu-id="0c302-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="0c302-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="0c302-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="0c302-264">Go Lan</span></span>   | <span data-ttu-id="0c302-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="0c302-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="0c302-266">python</span><span class="sxs-lookup"><span data-stu-id="0c302-266">python</span></span>   | <span data-ttu-id="0c302-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="0c302-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="0c302-268">C++</span><span class="sxs-lookup"><span data-stu-id="0c302-268">C++</span></span>      | <span data-ttu-id="0c302-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="0c302-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="0c302-270">C#</span><span class="sxs-lookup"><span data-stu-id="0c302-270">C#</span></span>       | <span data-ttu-id="0c302-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="0c302-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="0c302-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c302-272">Javascript</span></span> | <span data-ttu-id="0c302-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="0c302-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="0c302-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c302-274">Powershell</span></span> | <span data-ttu-id="0c302-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="0c302-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="0c302-276">Bash</span><span class="sxs-lookup"><span data-stu-id="0c302-276">Bash</span></span>       | <span data-ttu-id="0c302-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="0c302-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="0c302-278">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0c302-278">FAQ</span></span>
1. <span data-ttu-id="0c302-279">Viene visualizzato l'errore `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="0c302-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="0c302-280">Che cosa significa?</span><span class="sxs-lookup"><span data-stu-id="0c302-280">What does this mean?</span></span>
   * <span data-ttu-id="0c302-281">Il Servizio metadati dell'istanza richiede che nella richiesta venga passata l'intestazione `Metadata: true`.</span><span class="sxs-lookup"><span data-stu-id="0c302-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="0c302-282">Il passaggio di questa intestazione nella chiamata REST consente l'accesso al Servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0c302-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="0c302-283">Perché non riesco a ottenere le informazioni di calcolo per la macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="0c302-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="0c302-284">Attualmente il Servizio metadati dell'istanza supporta solo le istanze create con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0c302-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="0c302-285">È possibile che in futuro venga aggiunto il supporto per le macchine virtuali del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0c302-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="0c302-286">Ho creato la mia macchina virtuale tramite Azure Resource Manager tempo fa.</span><span class="sxs-lookup"><span data-stu-id="0c302-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="0c302-287">Perché non riesco a vedere le informazioni sui metadati di calcolo?</span><span class="sxs-lookup"><span data-stu-id="0c302-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="0c302-288">Per tutte le macchine virtuali create dopo settembre 2016, è necessario aggiungere un [Tag](../azure-resource-manager/resource-group-using-tags.md) per iniziare a essere visualizzare i metadati di calcolo.</span><span class="sxs-lookup"><span data-stu-id="0c302-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="0c302-289">Per le macchine virtuale precedenti (create prima di settembre 2016), è necessario aggiungere o rimuovere estensioni o dischi di dati dalla macchina virtuale per aggiornare i metadati.</span><span class="sxs-lookup"><span data-stu-id="0c302-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="0c302-290">Perché viene visualizzato l'errore `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="0c302-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="0c302-291">Inviare di nuovo la richiesta basata sul sistema di backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="0c302-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="0c302-292">Se il problema persiste, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c302-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="0c302-293">Dove posso condividere domande o commenti aggiuntivi?</span><span class="sxs-lookup"><span data-stu-id="0c302-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="0c302-294">Inviare i propri commenti accedendo alla pagina http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="0c302-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="0c302-295">Il servizio funziona per l'istanza del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="0c302-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="0c302-296">Sì, il Servizio metadati è disponibile per le istanze del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="0c302-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="0c302-297">Come si ottiene assistenza per il servizio?</span><span class="sxs-lookup"><span data-stu-id="0c302-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="0c302-298">Per ottenere assistenza per il servizio, è necessario creare una richiesta di supporto nel portale di Azure per la macchina virtuale per la quale non si riesce a ottenere la risposta dei metadati dopo lunghi tentativi</span><span class="sxs-lookup"><span data-stu-id="0c302-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Supporto per i metadati dell'istanza](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="0c302-300">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c302-300">Next Steps</span></span>

- <span data-ttu-id="0c302-301">Altre informazioni sull'API [scheduledevents](virtual-machines-scheduled-events.md) **in anteprima pubblica** fornita dal Servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0c302-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
