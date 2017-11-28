---
title: Panoramica dell'istanza del servizio metadati aaaAzure | Documenti Microsoft
description: Interfaccia REST tooget informazioni della macchina virtuale calcolo, rete e gli eventi di manutenzione programmata.
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
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="b3124-103">Servizio metadati dell'istanza di Azure</span><span class="sxs-lookup"><span data-stu-id="b3124-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="b3124-104">Hello Azure servizio metadati dell'istanza vengono fornite informazioni sull'esecuzione di istanze di macchine virtuali che possono essere utilizzati toomanage e configurare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b3124-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="b3124-105">Le informazioni includono ad esempio SKU, configurazione di rete ed eventi di manutenzione previsti.</span><span class="sxs-lookup"><span data-stu-id="b3124-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="b3124-106">Per altre informazioni sul tipo di informazioni disponibili, vedere le [categorie di metadati](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="b3124-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="b3124-107">Servizio metadati dell'istanza di Azure è un Endpoint REST accessibile tooall le macchine virtuali IaaS creati tramite hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="b3124-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="b3124-108">endpoint Hello è disponibile all'indirizzo IP non instradabile ben noto (`169.254.169.254`) che sono accessibili solo da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b3124-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="b3124-109">Informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="b3124-109">Important information</span></span>

<span data-ttu-id="b3124-110">Questo servizio è **disponibile a livello generale** nelle aree globali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3124-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="b3124-111">È in anteprima pubblica per il cloud di Azure Germania, per la Cina e per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="b3124-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="b3124-112">Riceve regolarmente gli aggiornamenti tooexpose nuove informazioni sulle istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b3124-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="b3124-113">Questa pagina riflette hello aggiornata [categorie di dati](#instance-metadata-data-categories) disponibili.</span><span class="sxs-lookup"><span data-stu-id="b3124-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="b3124-114">Disponibilità del servizio</span><span class="sxs-lookup"><span data-stu-id="b3124-114">Service Availability</span></span>
<span data-ttu-id="b3124-115">servizio di Hello è disponibile in tutte le aree di Azure globale disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="b3124-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="b3124-116">servizio Hello è in anteprima pubblica in aree di hello per enti pubblici, Cina o Germania.</span><span class="sxs-lookup"><span data-stu-id="b3124-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="b3124-117">Regioni</span><span class="sxs-lookup"><span data-stu-id="b3124-117">Regions</span></span>                                        | <span data-ttu-id="b3124-118">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="b3124-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="b3124-119">Tutte le aree globali di Azure con disponibilità a livello generale</span><span class="sxs-lookup"><span data-stu-id="b3124-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="b3124-120">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="b3124-120">Generally Available</span></span> 
[<span data-ttu-id="b3124-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="b3124-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="b3124-122">In anteprima</span><span class="sxs-lookup"><span data-stu-id="b3124-122">In Preview</span></span> 
[<span data-ttu-id="b3124-123">Azure per la Cina</span><span class="sxs-lookup"><span data-stu-id="b3124-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="b3124-124">In anteprima</span><span class="sxs-lookup"><span data-stu-id="b3124-124">In Preview</span></span>
[<span data-ttu-id="b3124-125">Azure Germania</span><span class="sxs-lookup"><span data-stu-id="b3124-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="b3124-126">In anteprima</span><span class="sxs-lookup"><span data-stu-id="b3124-126">In Preview</span></span>

<span data-ttu-id="b3124-127">Questa tabella viene aggiornata quando diventa disponibile il servizio hello in altri cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3124-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="b3124-128">tootry out hello servizio metadati dell'istanza, creare una macchina virtuale da [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portale di Azure](http://portal.azure.com) in hello sopra le aree e seguire hello esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b3124-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="b3124-129">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b3124-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="b3124-130">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="b3124-130">Versioning</span></span>
<span data-ttu-id="b3124-131">Hello servizio metadati dell'istanza viene creata.</span><span class="sxs-lookup"><span data-stu-id="b3124-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="b3124-132">Le versioni sono obbligatorie e la versione corrente di hello è `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="b3124-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-133">Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="b3124-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="b3124-134">Questo formato non è più supportato e verrà rimossa in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="b3124-135">Quando si aggiungono versioni più recenti, quelle precedenti sono comunque accessibili per la compatibilità, se gli script presentano dipendenze in formati di dati specifici.</span><span class="sxs-lookup"><span data-stu-id="b3124-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="b3124-136">Si noti tuttavia che version(2017-03-01) anteprima corrente hello potrebbe non essere disponibile quando il servizio di hello è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="b3124-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="b3124-137">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="b3124-137">Using Headers</span></span>
<span data-ttu-id="b3124-138">Quando si eseguono query hello servizio metadati dell'istanza, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="b3124-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="b3124-139">Recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="b3124-139">Retrieving metadata</span></span>

<span data-ttu-id="b3124-140">I metadati dell'istanza sono disponibili per l'esecuzione di macchine virtuali create e gestite tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="b3124-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="b3124-141">Accedere a tutte le categorie di dati per un'istanza di macchina virtuale utilizzando hello seguito richiesta:</span><span class="sxs-lookup"><span data-stu-id="b3124-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="b3124-142">Tutte le query dei metadati dell'istanza fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b3124-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="b3124-143">Output dei dati</span><span class="sxs-lookup"><span data-stu-id="b3124-143">Data output</span></span>
<span data-ttu-id="b3124-144">Per impostazione predefinita, servizio metadati dell'istanza di hello restituisce i dati in formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="b3124-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="b3124-145">Tuttavia, API diverse possono restituire dati in formati diversi se necessario.</span><span class="sxs-lookup"><span data-stu-id="b3124-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="b3124-146">Hello nella tabella seguente è un riferimento di altri formati di dati che potrebbero supportare le API.</span><span class="sxs-lookup"><span data-stu-id="b3124-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="b3124-147">API</span><span class="sxs-lookup"><span data-stu-id="b3124-147">API</span></span> | <span data-ttu-id="b3124-148">Formato dati predefinito</span><span class="sxs-lookup"><span data-stu-id="b3124-148">Default Data Format</span></span> | <span data-ttu-id="b3124-149">Altri formati</span><span class="sxs-lookup"><span data-stu-id="b3124-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="b3124-150">/instance</span><span class="sxs-lookup"><span data-stu-id="b3124-150">/instance</span></span> | <span data-ttu-id="b3124-151">json</span><span class="sxs-lookup"><span data-stu-id="b3124-151">json</span></span> | <span data-ttu-id="b3124-152">text</span><span class="sxs-lookup"><span data-stu-id="b3124-152">text</span></span>
<span data-ttu-id="b3124-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="b3124-153">/scheduledevents</span></span> | <span data-ttu-id="b3124-154">json</span><span class="sxs-lookup"><span data-stu-id="b3124-154">json</span></span> | <span data-ttu-id="b3124-155">Nessuno</span><span class="sxs-lookup"><span data-stu-id="b3124-155">none</span></span>

<span data-ttu-id="b3124-156">tooaccess un formato di risposta non predefinito, specificare il formato richiesto di hello come parametro querystring nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="b3124-157">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b3124-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="b3124-158">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="b3124-158">Security</span></span>
<span data-ttu-id="b3124-159">endpoint di servizio metadati dell'istanza di Hello è accessibile solo dall'interno hello esegue l'istanza di macchina virtuale in un indirizzo IP non è instradabile.</span><span class="sxs-lookup"><span data-stu-id="b3124-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="b3124-160">Inoltre, qualsiasi richiesta con un `X-Forwarded-For` intestazione viene rifiutata dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="b3124-161">È inoltre necessario richieste toocontain un `Metadata: true` tooensure intestazione che hello richiesta effettiva è stata direttamente previsto e che non fa parte di reindirizzamento non intenzionale.</span><span class="sxs-lookup"><span data-stu-id="b3124-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="b3124-162">Errore</span><span class="sxs-lookup"><span data-stu-id="b3124-162">Error</span></span>
<span data-ttu-id="b3124-163">Se è presente un elemento di dati non trovato o una richiesta in formato non corretto, hello servizio metadati dell'istanza restituisce errori HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="b3124-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="b3124-164">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b3124-164">For example:</span></span>

<span data-ttu-id="b3124-165">Codice di stato HTTP</span><span class="sxs-lookup"><span data-stu-id="b3124-165">HTTP Status Code</span></span> | <span data-ttu-id="b3124-166">Motivo</span><span class="sxs-lookup"><span data-stu-id="b3124-166">Reason</span></span>
----------------|-------
<span data-ttu-id="b3124-167">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b3124-167">200 OK</span></span> |
<span data-ttu-id="b3124-168">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="b3124-168">400 Bad Request</span></span> | <span data-ttu-id="b3124-169">Intestazione `Metadata: true` mancante</span><span class="sxs-lookup"><span data-stu-id="b3124-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="b3124-170">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="b3124-170">404 Not Found</span></span> | <span data-ttu-id="b3124-171">esistere Hello quando elemento richiesto</span><span class="sxs-lookup"><span data-stu-id="b3124-171">hello requested element does't exist</span></span> 
<span data-ttu-id="b3124-172">405 - Metodo non consentito</span><span class="sxs-lookup"><span data-stu-id="b3124-172">405 Method Not Allowed</span></span> | <span data-ttu-id="b3124-173">Sono supportate solo le richieste `GET` e `POST`</span><span class="sxs-lookup"><span data-stu-id="b3124-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="b3124-174">429 - Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="b3124-174">429 Too Many Requests</span></span> | <span data-ttu-id="b3124-175">l'API di Hello attualmente supporta un massimo di 5 query al secondo</span><span class="sxs-lookup"><span data-stu-id="b3124-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="b3124-176">500 - Errore del servizio</span><span class="sxs-lookup"><span data-stu-id="b3124-176">500 Service Error</span></span>     | <span data-ttu-id="b3124-177">Ripetere l'operazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="b3124-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="b3124-178">esempi</span><span class="sxs-lookup"><span data-stu-id="b3124-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-179">Tutte le risposte delle API sono stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="b3124-179">All API responses are JSON strings.</span></span> <span data-ttu-id="b3124-180">Tutte le risposte di esempio che seguono sono di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="b3124-181">Recupero delle informazioni di rete</span><span class="sxs-lookup"><span data-stu-id="b3124-181">Retrieving network information</span></span>

<span data-ttu-id="b3124-182">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="b3124-183">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-184">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="b3124-184">hello response is a JSON string.</span></span> <span data-ttu-id="b3124-185">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-185">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="b3124-186">Recupero dell'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="b3124-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="b3124-187">Recupero di tutti i metadati per un'istanza</span><span class="sxs-lookup"><span data-stu-id="b3124-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="b3124-188">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="b3124-189">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-190">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="b3124-190">hello response is a JSON string.</span></span> <span data-ttu-id="b3124-191">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-191">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="b3124-192">Recupero dei metadati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="b3124-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="b3124-193">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-193">**Request**</span></span>

<span data-ttu-id="b3124-194">I metadati dell'istanza possono essere recuperati in Windows tramite l'utilità di PowerShell hello `curl`:</span><span class="sxs-lookup"><span data-stu-id="b3124-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="b3124-195">O tramite hello `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b3124-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="b3124-196">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-197">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="b3124-197">hello response is a JSON string.</span></span> <span data-ttu-id="b3124-198">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-198">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="b3124-199">Categorie di dati dei metadati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="b3124-199">Instance metadata data categories</span></span>
<span data-ttu-id="b3124-200">Hello seguenti categorie di dati sono disponibile tramite hello servizio metadati dell'istanza:</span><span class="sxs-lookup"><span data-stu-id="b3124-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="b3124-201">Dati</span><span class="sxs-lookup"><span data-stu-id="b3124-201">Data</span></span> | <span data-ttu-id="b3124-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b3124-202">Description</span></span>
-----|------------
<span data-ttu-id="b3124-203">location</span><span class="sxs-lookup"><span data-stu-id="b3124-203">location</span></span> | <span data-ttu-id="b3124-204">Hello area Azure VM è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="b3124-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="b3124-205">name</span><span class="sxs-lookup"><span data-stu-id="b3124-205">name</span></span> | <span data-ttu-id="b3124-206">Nome della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="b3124-206">Name of hello VM</span></span> 
<span data-ttu-id="b3124-207">offer</span><span class="sxs-lookup"><span data-stu-id="b3124-207">offer</span></span> | <span data-ttu-id="b3124-208">Offrono informazioni per l'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-208">Offer information for hello VM image.</span></span> <span data-ttu-id="b3124-209">Questo valore è presente solo per le immagini distribuite dalla raccolta di immagini di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3124-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="b3124-210">publisher</span><span class="sxs-lookup"><span data-stu-id="b3124-210">publisher</span></span> | <span data-ttu-id="b3124-211">Server di pubblicazione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="b3124-211">Publisher of hello VM image</span></span>
<span data-ttu-id="b3124-212">sku</span><span class="sxs-lookup"><span data-stu-id="b3124-212">sku</span></span> | <span data-ttu-id="b3124-213">SKU specifico per l'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="b3124-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="b3124-214">version</span><span class="sxs-lookup"><span data-stu-id="b3124-214">version</span></span> | <span data-ttu-id="b3124-215">Versione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="b3124-215">Version of hello VM image</span></span> 
<span data-ttu-id="b3124-216">osType</span><span class="sxs-lookup"><span data-stu-id="b3124-216">osType</span></span> | <span data-ttu-id="b3124-217">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="b3124-217">Linux or Windows</span></span> 
<span data-ttu-id="b3124-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="b3124-218">platformUpdateDomain</span></span> |  <span data-ttu-id="b3124-219">[Dominio di aggiornamento](virtual-machines-windows-manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="b3124-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="b3124-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="b3124-220">platformFaultDomain</span></span> | <span data-ttu-id="b3124-221">[Dominio di errore](virtual-machines-windows-manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="b3124-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="b3124-222">vmId</span><span class="sxs-lookup"><span data-stu-id="b3124-222">vmId</span></span> | <span data-ttu-id="b3124-223">[Identificatore univoco](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) per hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="b3124-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="b3124-224">vmSize</span></span> | [<span data-ttu-id="b3124-225">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b3124-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="b3124-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="b3124-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="b3124-227">Indirizzo IPv4 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="b3124-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b3124-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="b3124-229">Indirizzo IPv4 pubblico di hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="b3124-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="b3124-230">subnet/address</span></span> | <span data-ttu-id="b3124-231">Indirizzo di subnet di hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-231">Subnet address of hello VM</span></span>
<span data-ttu-id="b3124-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="b3124-232">subnet/prefix</span></span> | <span data-ttu-id="b3124-233">Prefisso della subnet, ad esempio 24</span><span class="sxs-lookup"><span data-stu-id="b3124-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="b3124-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="b3124-234">ipv6/ipAddress</span></span> | <span data-ttu-id="b3124-235">Indirizzo IPv6 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="b3124-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="b3124-236">macAddress</span></span> | <span data-ttu-id="b3124-237">Indirizzo mac della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b3124-237">VM mac address</span></span> 
<span data-ttu-id="b3124-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="b3124-238">scheduledevents</span></span> | <span data-ttu-id="b3124-239">Attualmente in anteprima pubblica. Vedere [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="b3124-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="b3124-240">Scenari di uso di esempio</span><span class="sxs-lookup"><span data-stu-id="b3124-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="b3124-241">Rilevamento della macchina virtuale in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="b3124-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="b3124-242">Come provider di servizi, potrebbe essere necessario numero hello tootrack delle macchine virtuali in esecuzione il software o gli agenti necessari tootrack l'univocità di hello VM.</span><span class="sxs-lookup"><span data-stu-id="b3124-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="b3124-243">toobe in grado di tooget un ID univoco per una macchina virtuale, utilizzare hello `vmId` campo servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b3124-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="b3124-244">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="b3124-245">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="b3124-246">Posizionamento di contenitori, dominio di aggiornamento/errore basato su partizioni dati</span><span class="sxs-lookup"><span data-stu-id="b3124-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="b3124-247">Per alcuni scenari, il posizionamento di repliche dati diverse è di importanza primaria.</span><span class="sxs-lookup"><span data-stu-id="b3124-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="b3124-248">Ad esempio, [posizionamento delle repliche HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la selezione host contenitore tramite un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) richieda è hello tooknow `platformFaultDomain` e `platformUpdateDomain` hello macchina virtuale è in esecuzione in.</span><span class="sxs-lookup"><span data-stu-id="b3124-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="b3124-249">È possibile ottenere i dati direttamente tramite hello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b3124-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="b3124-250">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="b3124-251">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="b3124-252">Ulteriori informazioni su hello VM durante il caso di supporto</span><span class="sxs-lookup"><span data-stu-id="b3124-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="b3124-253">Come provider di servizi, si potrebbero ottenere una chiamata al supporto in cui si desidera tooknow ulteriori informazioni sulla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="b3124-254">Porre hello cliente tooshare hello calcolo metadati possono fornire informazioni di base per hello supporto professionale tooknow su tipo hello della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="b3124-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="b3124-255">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="b3124-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="b3124-256">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="b3124-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="b3124-257">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="b3124-257">hello response is a JSON string.</span></span> <span data-ttu-id="b3124-258">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-258">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="b3124-259">Esempi di chiamate del servizio di metadati utilizzando diversi linguaggi all'interno di hello VM</span><span class="sxs-lookup"><span data-stu-id="b3124-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="b3124-260">Lingua</span><span class="sxs-lookup"><span data-stu-id="b3124-260">Language</span></span> | <span data-ttu-id="b3124-261">Esempio</span><span class="sxs-lookup"><span data-stu-id="b3124-261">Example</span></span> 
---------|----------------
<span data-ttu-id="b3124-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="b3124-262">Ruby</span></span>     | <span data-ttu-id="b3124-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="b3124-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="b3124-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="b3124-264">Go Lan</span></span>   | <span data-ttu-id="b3124-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="b3124-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="b3124-266">python</span><span class="sxs-lookup"><span data-stu-id="b3124-266">python</span></span>   | <span data-ttu-id="b3124-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="b3124-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="b3124-268">C++</span><span class="sxs-lookup"><span data-stu-id="b3124-268">C++</span></span>      | <span data-ttu-id="b3124-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="b3124-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="b3124-270">C#</span><span class="sxs-lookup"><span data-stu-id="b3124-270">C#</span></span>       | <span data-ttu-id="b3124-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="b3124-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="b3124-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b3124-272">Javascript</span></span> | <span data-ttu-id="b3124-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="b3124-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="b3124-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3124-274">Powershell</span></span> | <span data-ttu-id="b3124-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="b3124-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="b3124-276">Bash</span><span class="sxs-lookup"><span data-stu-id="b3124-276">Bash</span></span>       | <span data-ttu-id="b3124-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="b3124-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="b3124-278">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="b3124-278">FAQ</span></span>
1. <span data-ttu-id="b3124-279">Viene visualizzato l'errore hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="b3124-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="b3124-280">Che cosa significa?</span><span class="sxs-lookup"><span data-stu-id="b3124-280">What does this mean?</span></span>
   * <span data-ttu-id="b3124-281">Servizio metadati dell'istanza di Hello richiede intestazione hello `Metadata: true` toobe passato nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="b3124-282">Il passaggio di questa intestazione nella chiamata REST hello consente accesso toohello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b3124-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="b3124-283">Perché non riesco a ottenere le informazioni di calcolo per la macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="b3124-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="b3124-284">Hello servizio metadati dell'istanza supporta attualmente solo le istanze create con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3124-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="b3124-285">In hello future, si potrebbe aggiungere supporto per le macchine virtuali del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="b3124-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="b3124-286">Ho creato la mia macchina virtuale tramite Azure Resource Manager tempo fa.</span><span class="sxs-lookup"><span data-stu-id="b3124-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="b3124-287">Perché non riesco a vedere le informazioni sui metadati di calcolo?</span><span class="sxs-lookup"><span data-stu-id="b3124-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="b3124-288">Per tutte le macchine virtuali create dopo settembre 2016, aggiungere un [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart vedere calcolo metadati.</span><span class="sxs-lookup"><span data-stu-id="b3124-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="b3124-289">Per macchine virtuali meno recenti (Create prima di settembre 2016), aggiungere o rimuovere estensioni o dati dischi toohello VM toorefresh metadati.</span><span class="sxs-lookup"><span data-stu-id="b3124-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="b3124-290">Perché viene visualizzato errore hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="b3124-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="b3124-291">Inviare di nuovo la richiesta basata sul sistema di backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="b3124-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="b3124-292">Se il problema di hello persiste, contattare il supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3124-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="b3124-293">Dove posso condividere domande o commenti aggiuntivi?</span><span class="sxs-lookup"><span data-stu-id="b3124-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="b3124-294">Inviare i propri commenti accedendo alla pagina http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b3124-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="b3124-295">Il servizio funziona per l'istanza del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="b3124-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="b3124-296">Sì, il Servizio metadati è disponibile per le istanze del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3124-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="b3124-297">Come ottenere supporto per il servizio hello?</span><span class="sxs-lookup"><span data-stu-id="b3124-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="b3124-298">supporto tooget per il servizio di hello, creare un problema di supporto nel portale di Azure per la macchina virtuale in cui non si risposta dei metadati in grado di tooget dopo tentativi lunghi hello</span><span class="sxs-lookup"><span data-stu-id="b3124-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Supporto per i metadati dell'istanza](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="b3124-300">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3124-300">Next Steps</span></span>

- <span data-ttu-id="b3124-301">Altre informazioni su hello [scheduledevents](virtual-machines-scheduled-events.md) API **In anteprima pubblica** fornita da servizio metadati dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="b3124-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
