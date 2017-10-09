---
title: aaaAzure servizio metadati dell'istanza per Windows | Documenti Microsoft
description: Interfaccia REST tooget informazioni della macchina virtuale Windows calcolo, rete e gli eventi di manutenzione programmata.
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a><span data-ttu-id="19311-103">Servizio metadati dell'istanza di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="19311-103">Azure Instance Metadata service for Windows VMs</span></span>


<span data-ttu-id="19311-104">Hello Azure servizio metadati dell'istanza vengono fornite informazioni sull'esecuzione di istanze di macchine virtuali che possono essere utilizzati toomanage e configurare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19311-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="19311-105">Le informazioni includono ad esempio SKU, configurazione di rete ed eventi di manutenzione previsti.</span><span class="sxs-lookup"><span data-stu-id="19311-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="19311-106">Per altre informazioni sul tipo di informazioni disponibili, vedere le [categorie di metadati](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="19311-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="19311-107">Servizio metadati dell'istanza di Azure è un Endpoint REST accessibile tooall le macchine virtuali IaaS creati tramite hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="19311-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="19311-108">endpoint Hello è disponibile all'indirizzo IP non instradabile ben noto (`169.254.169.254`) che sono accessibili solo da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="19311-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>



> [!IMPORTANT]
> <span data-ttu-id="19311-109">Questo servizio è **disponibile a livello generale** nelle aree globali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19311-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="19311-110">È in anteprima pubblica per il cloud di Azure Germania, per la Cina e per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="19311-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="19311-111">Riceve regolarmente gli aggiornamenti tooexpose nuove informazioni sulle istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="19311-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="19311-112">Questa pagina riflette hello aggiornata [categorie di dati](#instance-metadata-data-categories) disponibili.</span><span class="sxs-lookup"><span data-stu-id="19311-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>



## <a name="service-availability"></a><span data-ttu-id="19311-113">Disponibilità del servizio</span><span class="sxs-lookup"><span data-stu-id="19311-113">Service Availability</span></span>
<span data-ttu-id="19311-114">servizio di Hello è disponibile in tutte le aree di Azure globale disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="19311-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="19311-115">servizio Hello è in anteprima pubblica in aree di hello per enti pubblici, Cina o Germania.</span><span class="sxs-lookup"><span data-stu-id="19311-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="19311-116">Regioni</span><span class="sxs-lookup"><span data-stu-id="19311-116">Regions</span></span>                                        | <span data-ttu-id="19311-117">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="19311-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="19311-118">Tutte le aree globali di Azure con disponibilità a livello generale</span><span class="sxs-lookup"><span data-stu-id="19311-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="19311-119">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="19311-119">Generally Available</span></span> 
[<span data-ttu-id="19311-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="19311-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="19311-121">In anteprima</span><span class="sxs-lookup"><span data-stu-id="19311-121">In Preview</span></span> 
[<span data-ttu-id="19311-122">Azure per la Cina</span><span class="sxs-lookup"><span data-stu-id="19311-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="19311-123">In anteprima</span><span class="sxs-lookup"><span data-stu-id="19311-123">In Preview</span></span>
[<span data-ttu-id="19311-124">Azure Germania</span><span class="sxs-lookup"><span data-stu-id="19311-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="19311-125">In anteprima</span><span class="sxs-lookup"><span data-stu-id="19311-125">In Preview</span></span>

<span data-ttu-id="19311-126">Questa tabella viene aggiornata quando diventa disponibile il servizio hello in altri cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="19311-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="19311-127">tootry out hello servizio metadati dell'istanza, creare una macchina virtuale da [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portale di Azure](http://portal.azure.com) in hello sopra le aree e seguire hello esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="19311-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="19311-128">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="19311-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="19311-129">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="19311-129">Versioning</span></span>
<span data-ttu-id="19311-130">Hello servizio metadati dell'istanza viene creata.</span><span class="sxs-lookup"><span data-stu-id="19311-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="19311-131">Le versioni sono obbligatorie e la versione corrente di hello è `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="19311-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-132">Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="19311-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="19311-133">Questo formato non è più supportato e verrà rimossa in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="19311-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="19311-134">Quando si aggiungono versioni più recenti, quelle precedenti sono comunque accessibili per la compatibilità, se gli script presentano dipendenze in formati di dati specifici.</span><span class="sxs-lookup"><span data-stu-id="19311-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="19311-135">Si noti tuttavia che version(2017-03-01) anteprima corrente hello potrebbe non essere disponibile quando il servizio di hello è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="19311-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="19311-136">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="19311-136">Using headers</span></span>
<span data-ttu-id="19311-137">Quando si eseguono query hello servizio metadati dell'istanza, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="19311-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="19311-138">Recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="19311-138">Retrieving metadata</span></span>

<span data-ttu-id="19311-139">I metadati dell'istanza sono disponibili per l'esecuzione di macchine virtuali create e gestite tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="19311-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="19311-140">Accedere a tutte le categorie di dati per un'istanza di macchina virtuale utilizzando hello seguito richiesta:</span><span class="sxs-lookup"><span data-stu-id="19311-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="19311-141">Tutte le query dei metadati dell'istanza fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="19311-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="19311-142">Output dei dati</span><span class="sxs-lookup"><span data-stu-id="19311-142">Data output</span></span>
<span data-ttu-id="19311-143">Per impostazione predefinita, servizio metadati dell'istanza di hello restituisce i dati in formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="19311-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="19311-144">Tuttavia, API diverse possono restituire dati in formati diversi se necessario.</span><span class="sxs-lookup"><span data-stu-id="19311-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="19311-145">Hello nella tabella seguente è un riferimento di altri formati di dati che potrebbero supportare le API.</span><span class="sxs-lookup"><span data-stu-id="19311-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="19311-146">API</span><span class="sxs-lookup"><span data-stu-id="19311-146">API</span></span> | <span data-ttu-id="19311-147">Formato dati predefinito</span><span class="sxs-lookup"><span data-stu-id="19311-147">Default Data Format</span></span> | <span data-ttu-id="19311-148">Altri formati</span><span class="sxs-lookup"><span data-stu-id="19311-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="19311-149">/instance</span><span class="sxs-lookup"><span data-stu-id="19311-149">/instance</span></span> | <span data-ttu-id="19311-150">json</span><span class="sxs-lookup"><span data-stu-id="19311-150">json</span></span> | <span data-ttu-id="19311-151">text</span><span class="sxs-lookup"><span data-stu-id="19311-151">text</span></span>
<span data-ttu-id="19311-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="19311-152">/scheduledevents</span></span> | <span data-ttu-id="19311-153">json</span><span class="sxs-lookup"><span data-stu-id="19311-153">json</span></span> | <span data-ttu-id="19311-154">Nessuno</span><span class="sxs-lookup"><span data-stu-id="19311-154">none</span></span>

<span data-ttu-id="19311-155">tooaccess un formato di risposta non predefinito, specificare il formato richiesto di hello come parametro querystring nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="19311-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="19311-156">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="19311-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="19311-157">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="19311-157">Security</span></span>
<span data-ttu-id="19311-158">endpoint di servizio metadati dell'istanza di Hello è accessibile solo dall'interno hello esegue l'istanza di macchina virtuale in un indirizzo IP non è instradabile.</span><span class="sxs-lookup"><span data-stu-id="19311-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="19311-159">Inoltre, qualsiasi richiesta con un `X-Forwarded-For` intestazione viene rifiutata dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="19311-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="19311-160">È inoltre necessario richieste toocontain un `Metadata: true` tooensure intestazione che hello richiesta effettiva è stata direttamente previsto e che non fa parte di reindirizzamento non intenzionale.</span><span class="sxs-lookup"><span data-stu-id="19311-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="19311-161">Errore</span><span class="sxs-lookup"><span data-stu-id="19311-161">Error</span></span>
<span data-ttu-id="19311-162">Se è presente un elemento di dati non trovato o una richiesta in formato non corretto, hello servizio metadati dell'istanza restituisce errori HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="19311-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="19311-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="19311-163">For example:</span></span>

<span data-ttu-id="19311-164">Codice di stato HTTP</span><span class="sxs-lookup"><span data-stu-id="19311-164">HTTP Status Code</span></span> | <span data-ttu-id="19311-165">Motivo</span><span class="sxs-lookup"><span data-stu-id="19311-165">Reason</span></span>
----------------|-------
<span data-ttu-id="19311-166">200 - OK</span><span class="sxs-lookup"><span data-stu-id="19311-166">200 OK</span></span> |
<span data-ttu-id="19311-167">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="19311-167">400 Bad Request</span></span> | <span data-ttu-id="19311-168">Intestazione `Metadata: true` mancante</span><span class="sxs-lookup"><span data-stu-id="19311-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="19311-169">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="19311-169">404 Not Found</span></span> | <span data-ttu-id="19311-170">esistere Hello quando elemento richiesto</span><span class="sxs-lookup"><span data-stu-id="19311-170">hello requested element does't exist</span></span> 
<span data-ttu-id="19311-171">405 - Metodo non consentito</span><span class="sxs-lookup"><span data-stu-id="19311-171">405 Method Not Allowed</span></span> | <span data-ttu-id="19311-172">Sono supportate solo le richieste `GET` e `POST`</span><span class="sxs-lookup"><span data-stu-id="19311-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="19311-173">429 - Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="19311-173">429 Too Many Requests</span></span> | <span data-ttu-id="19311-174">l'API di Hello attualmente supporta un massimo di 5 query al secondo</span><span class="sxs-lookup"><span data-stu-id="19311-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="19311-175">500 - Errore del servizio</span><span class="sxs-lookup"><span data-stu-id="19311-175">500 Service Error</span></span>     | <span data-ttu-id="19311-176">Ripetere l'operazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="19311-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="19311-177">esempi</span><span class="sxs-lookup"><span data-stu-id="19311-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-178">Tutte le risposte delle API sono stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="19311-178">All API responses are JSON strings.</span></span> <span data-ttu-id="19311-179">Tutte le risposte di esempio che seguono sono di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="19311-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="19311-180">Recupero delle informazioni di rete</span><span class="sxs-lookup"><span data-stu-id="19311-180">Retrieving network information</span></span>

<span data-ttu-id="19311-181">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="19311-182">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-183">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="19311-183">hello response is a JSON string.</span></span> <span data-ttu-id="19311-184">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="19311-184">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="19311-185">Recupero dell'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="19311-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="19311-186">Recupero di tutti i metadati per un'istanza</span><span class="sxs-lookup"><span data-stu-id="19311-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="19311-187">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="19311-188">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-189">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="19311-189">hello response is a JSON string.</span></span> <span data-ttu-id="19311-190">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="19311-190">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="19311-191">Recupero dei metadati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="19311-191">Retrieving metadata in Windows virtual machine</span></span>

<span data-ttu-id="19311-192">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-192">**Request**</span></span>

<span data-ttu-id="19311-193">I metadati dell'istanza possono essere recuperati in Windows tramite l'utilità di PowerShell hello `curl`:</span><span class="sxs-lookup"><span data-stu-id="19311-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="19311-194">O tramite hello `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="19311-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="19311-195">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-196">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="19311-196">hello response is a JSON string.</span></span> <span data-ttu-id="19311-197">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="19311-197">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="19311-198">Categorie di dati dei metadati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="19311-198">Instance metadata data categories</span></span>
<span data-ttu-id="19311-199">Hello seguenti categorie di dati sono disponibile tramite hello servizio metadati dell'istanza:</span><span class="sxs-lookup"><span data-stu-id="19311-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="19311-200">Dati</span><span class="sxs-lookup"><span data-stu-id="19311-200">Data</span></span> | <span data-ttu-id="19311-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="19311-201">Description</span></span>
-----|------------
<span data-ttu-id="19311-202">location</span><span class="sxs-lookup"><span data-stu-id="19311-202">location</span></span> | <span data-ttu-id="19311-203">Hello area Azure VM è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="19311-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="19311-204">name</span><span class="sxs-lookup"><span data-stu-id="19311-204">name</span></span> | <span data-ttu-id="19311-205">Nome della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="19311-205">Name of hello VM</span></span> 
<span data-ttu-id="19311-206">offer</span><span class="sxs-lookup"><span data-stu-id="19311-206">offer</span></span> | <span data-ttu-id="19311-207">Offrono informazioni per l'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="19311-207">Offer information for hello VM image.</span></span> <span data-ttu-id="19311-208">Questo valore è presente solo per le immagini distribuite dalla raccolta di immagini di Azure.</span><span class="sxs-lookup"><span data-stu-id="19311-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="19311-209">publisher</span><span class="sxs-lookup"><span data-stu-id="19311-209">publisher</span></span> | <span data-ttu-id="19311-210">Server di pubblicazione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="19311-210">Publisher of hello VM image</span></span>
<span data-ttu-id="19311-211">sku</span><span class="sxs-lookup"><span data-stu-id="19311-211">sku</span></span> | <span data-ttu-id="19311-212">SKU specifico per l'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="19311-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="19311-213">version</span><span class="sxs-lookup"><span data-stu-id="19311-213">version</span></span> | <span data-ttu-id="19311-214">Versione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="19311-214">Version of hello VM image</span></span> 
<span data-ttu-id="19311-215">osType</span><span class="sxs-lookup"><span data-stu-id="19311-215">osType</span></span> | <span data-ttu-id="19311-216">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="19311-216">Linux or Windows</span></span> 
<span data-ttu-id="19311-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="19311-217">platformUpdateDomain</span></span> |  <span data-ttu-id="19311-218">[Dominio di aggiornamento](manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="19311-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="19311-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="19311-219">platformFaultDomain</span></span> | <span data-ttu-id="19311-220">[Dominio di errore](manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="19311-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="19311-221">vmId</span><span class="sxs-lookup"><span data-stu-id="19311-221">vmId</span></span> | <span data-ttu-id="19311-222">[Identificatore univoco](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) per hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="19311-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="19311-223">vmSize</span></span> | [<span data-ttu-id="19311-224">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19311-224">VM size</span></span>](sizes.md)
<span data-ttu-id="19311-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="19311-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="19311-226">Indirizzo IPv4 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="19311-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="19311-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="19311-228">Indirizzo IPv4 pubblico di hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="19311-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="19311-229">subnet/address</span></span> | <span data-ttu-id="19311-230">Indirizzo di subnet di hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-230">Subnet address of hello VM</span></span>
<span data-ttu-id="19311-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="19311-231">subnet/prefix</span></span> | <span data-ttu-id="19311-232">Prefisso della subnet, ad esempio 24</span><span class="sxs-lookup"><span data-stu-id="19311-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="19311-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="19311-233">ipv6/ipAddress</span></span> | <span data-ttu-id="19311-234">Indirizzo IPv6 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="19311-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="19311-235">macAddress</span></span> | <span data-ttu-id="19311-236">Indirizzo mac della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="19311-236">VM mac address</span></span> 
<span data-ttu-id="19311-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="19311-237">scheduledevents</span></span> | <span data-ttu-id="19311-238">Attualmente in anteprima pubblica. Vedere [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="19311-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="19311-239">Scenari di utilizzo di esempio</span><span class="sxs-lookup"><span data-stu-id="19311-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="19311-240">Rilevamento della macchina virtuale in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="19311-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="19311-241">Come provider di servizi, potrebbe essere necessario numero hello tootrack delle macchine virtuali in esecuzione il software o gli agenti necessari tootrack l'univocità di hello VM.</span><span class="sxs-lookup"><span data-stu-id="19311-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="19311-242">toobe in grado di tooget un ID univoco per una macchina virtuale, utilizzare hello `vmId` campo servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="19311-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="19311-243">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="19311-244">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="19311-245">Posizionamento di contenitori, dominio di aggiornamento/errore basato su partizioni dati</span><span class="sxs-lookup"><span data-stu-id="19311-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="19311-246">Per alcuni scenari, il posizionamento di repliche dati diverse è di importanza primaria.</span><span class="sxs-lookup"><span data-stu-id="19311-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="19311-247">Ad esempio, [posizionamento delle repliche HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la selezione host contenitore tramite un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) richieda è hello tooknow `platformFaultDomain` e `platformUpdateDomain` hello macchina virtuale è in esecuzione in.</span><span class="sxs-lookup"><span data-stu-id="19311-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="19311-248">È possibile ottenere i dati direttamente tramite hello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="19311-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="19311-249">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="19311-250">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="19311-251">Ulteriori informazioni su hello VM durante il caso di supporto</span><span class="sxs-lookup"><span data-stu-id="19311-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="19311-252">Come provider di servizi, si potrebbero ottenere una chiamata al supporto in cui si desidera tooknow ulteriori informazioni sulla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="19311-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="19311-253">Porre hello cliente tooshare hello calcolo metadati possono fornire informazioni di base per hello supporto professionale tooknow su tipo hello della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="19311-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="19311-254">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="19311-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="19311-255">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="19311-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="19311-256">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="19311-256">hello response is a JSON string.</span></span> <span data-ttu-id="19311-257">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="19311-257">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="19311-258">Esempi di chiamate del servizio di metadati utilizzando diversi linguaggi all'interno di hello VM</span><span class="sxs-lookup"><span data-stu-id="19311-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="19311-259">Lingua</span><span class="sxs-lookup"><span data-stu-id="19311-259">Language</span></span> | <span data-ttu-id="19311-260">Esempio</span><span class="sxs-lookup"><span data-stu-id="19311-260">Example</span></span> 
---------|----------------
<span data-ttu-id="19311-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="19311-261">Ruby</span></span>     | <span data-ttu-id="19311-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="19311-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="19311-263">Go Lan</span><span class="sxs-lookup"><span data-stu-id="19311-263">Go Lan</span></span>   | <span data-ttu-id="19311-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="19311-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="19311-265">python</span><span class="sxs-lookup"><span data-stu-id="19311-265">python</span></span>   | <span data-ttu-id="19311-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="19311-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="19311-267">C++</span><span class="sxs-lookup"><span data-stu-id="19311-267">C++</span></span>      | <span data-ttu-id="19311-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="19311-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="19311-269">C#</span><span class="sxs-lookup"><span data-stu-id="19311-269">C#</span></span>       | <span data-ttu-id="19311-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="19311-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="19311-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="19311-271">Javascript</span></span> | <span data-ttu-id="19311-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="19311-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="19311-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19311-273">Powershell</span></span> | <span data-ttu-id="19311-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="19311-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="19311-275">Bash</span><span class="sxs-lookup"><span data-stu-id="19311-275">Bash</span></span>       | <span data-ttu-id="19311-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="19311-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="19311-277">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="19311-277">FAQ</span></span>
1. <span data-ttu-id="19311-278">Viene visualizzato l'errore hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="19311-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="19311-279">Che cosa significa?</span><span class="sxs-lookup"><span data-stu-id="19311-279">What does this mean?</span></span>
   * <span data-ttu-id="19311-280">Servizio metadati dell'istanza di Hello richiede intestazione hello `Metadata: true` toobe passato nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="19311-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="19311-281">Il passaggio di questa intestazione nella chiamata REST hello consente accesso toohello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="19311-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="19311-282">Perché non riesco a ottenere le informazioni di calcolo per la macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="19311-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="19311-283">Hello servizio metadati dell'istanza supporta attualmente solo le istanze create con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19311-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="19311-284">In hello future, si potrebbe aggiungere supporto per le macchine virtuali del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="19311-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="19311-285">Ho creato la mia macchina virtuale tramite Azure Resource Manager tempo fa.</span><span class="sxs-lookup"><span data-stu-id="19311-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="19311-286">Perché non riesco a vedere le informazioni sui metadati di calcolo?</span><span class="sxs-lookup"><span data-stu-id="19311-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="19311-287">Per tutte le macchine virtuali create dopo settembre 2016, aggiungere un [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart vedere calcolo metadati.</span><span class="sxs-lookup"><span data-stu-id="19311-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="19311-288">Per macchine virtuali meno recenti (Create prima di settembre 2016), aggiungere o rimuovere estensioni o dati dischi toohello VM toorefresh metadati.</span><span class="sxs-lookup"><span data-stu-id="19311-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="19311-289">Perché viene visualizzato errore hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="19311-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="19311-290">Inviare di nuovo la richiesta basata sul sistema di backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="19311-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="19311-291">Se il problema di hello persiste, contattare il supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="19311-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="19311-292">Dove posso condividere domande o commenti aggiuntivi?</span><span class="sxs-lookup"><span data-stu-id="19311-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="19311-293">Inviare i propri commenti accedendo alla pagina http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="19311-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="19311-294">Il servizio funziona per l'istanza del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="19311-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="19311-295">Sì, il Servizio metadati è disponibile per le istanze del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="19311-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="19311-296">Come ottenere supporto per il servizio hello?</span><span class="sxs-lookup"><span data-stu-id="19311-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="19311-297">supporto tooget per il servizio di hello, creare un problema di supporto nel portale di Azure per la macchina virtuale in cui non si risposta dei metadati in grado di tooget dopo tentativi lunghi hello</span><span class="sxs-lookup"><span data-stu-id="19311-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Supporto per i metadati dell'istanza](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="19311-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19311-299">Next steps</span></span>

- <span data-ttu-id="19311-300">Altre informazioni su hello [agli eventi pianificati](scheduled-events.md) API **in anteprima pubblica** fornita da servizio metadati dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="19311-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
