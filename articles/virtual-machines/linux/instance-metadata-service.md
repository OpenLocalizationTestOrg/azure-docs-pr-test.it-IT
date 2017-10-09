---
title: aaaAzure servizio metadati dell'istanza per le macchine virtuali Linux | Documenti Microsoft
description: Interfaccia REST tooget informazioni di Linux VM calcolo, rete e gli eventi di manutenzione programmata.
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="0b559-103">Servizio metadati dell'istanza di Azure per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="0b559-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="0b559-104">Hello Azure servizio metadati dell'istanza vengono fornite informazioni sull'esecuzione di istanze di macchine virtuali che possono essere utilizzati toomanage e configurare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0b559-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="0b559-105">Le informazioni includono ad esempio SKU, configurazione di rete ed eventi di manutenzione previsti.</span><span class="sxs-lookup"><span data-stu-id="0b559-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="0b559-106">Per altre informazioni sul tipo di informazioni disponibili, vedere le [categorie di metadati](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="0b559-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="0b559-107">Servizio metadati dell'istanza di Azure è un Endpoint REST accessibile tooall le macchine virtuali IaaS creati tramite hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0b559-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0b559-108">endpoint Hello è disponibile all'indirizzo IP non instradabile ben noto (`169.254.169.254`) che sono accessibili solo da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0b559-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b559-109">Questo servizio è **disponibile a livello generale** nelle aree globali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b559-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="0b559-110">È in anteprima pubblica per il cloud di Azure Germania, per la Cina e per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="0b559-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="0b559-111">Riceve regolarmente gli aggiornamenti tooexpose nuove informazioni sulle istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0b559-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="0b559-112">Questa pagina riflette hello aggiornata [categorie di dati](#instance-metadata-data-categories) disponibili.</span><span class="sxs-lookup"><span data-stu-id="0b559-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="0b559-113">Disponibilità del servizio</span><span class="sxs-lookup"><span data-stu-id="0b559-113">Service availability</span></span>
<span data-ttu-id="0b559-114">servizio di Hello è disponibile in tutte le aree di Azure globale disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="0b559-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="0b559-115">servizio Hello è in anteprima pubblica in aree di hello per enti pubblici, Cina o Germania.</span><span class="sxs-lookup"><span data-stu-id="0b559-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="0b559-116">Regioni</span><span class="sxs-lookup"><span data-stu-id="0b559-116">Regions</span></span>                                        | <span data-ttu-id="0b559-117">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="0b559-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="0b559-118">Tutte le aree globali di Azure con disponibilità a livello generale</span><span class="sxs-lookup"><span data-stu-id="0b559-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="0b559-119">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="0b559-119">Generally Available</span></span> 
[<span data-ttu-id="0b559-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="0b559-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="0b559-121">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0b559-121">In Preview</span></span> 
[<span data-ttu-id="0b559-122">Azure per la Cina</span><span class="sxs-lookup"><span data-stu-id="0b559-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="0b559-123">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0b559-123">In Preview</span></span>
[<span data-ttu-id="0b559-124">Azure Germania</span><span class="sxs-lookup"><span data-stu-id="0b559-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="0b559-125">In anteprima</span><span class="sxs-lookup"><span data-stu-id="0b559-125">In Preview</span></span>

<span data-ttu-id="0b559-126">Questa tabella viene aggiornata quando diventa disponibile il servizio hello in altri cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b559-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="0b559-127">tootry out hello servizio metadati dell'istanza, creare una macchina virtuale da [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portale di Azure](http://portal.azure.com) in hello sopra le aree e seguire hello esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0b559-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="0b559-128">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="0b559-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="0b559-129">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="0b559-129">Versioning</span></span>
<span data-ttu-id="0b559-130">Hello servizio metadati dell'istanza viene creata.</span><span class="sxs-lookup"><span data-stu-id="0b559-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0b559-131">Le versioni sono obbligatorie e la versione corrente di hello è `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="0b559-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-132">Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="0b559-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="0b559-133">Questo formato non è più supportato e verrà rimossa in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="0b559-134">Quando si aggiungono versioni più recenti, quelle precedenti sono comunque accessibili per la compatibilità, se gli script presentano dipendenze in formati di dati specifici.</span><span class="sxs-lookup"><span data-stu-id="0b559-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="0b559-135">Si noti tuttavia che version(2017-03-01) anteprima corrente hello potrebbe non essere disponibile quando il servizio di hello è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="0b559-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0b559-136">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="0b559-136">Using headers</span></span>
<span data-ttu-id="0b559-137">Quando si eseguono query hello servizio metadati dell'istanza, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="0b559-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="0b559-138">Recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="0b559-138">Retrieving metadata</span></span>

<span data-ttu-id="0b559-139">I metadati dell'istanza sono disponibili per l'esecuzione di macchine virtuali create e gestite tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0b559-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0b559-140">Accedere a tutte le categorie di dati per un'istanza di macchina virtuale utilizzando hello seguito richiesta:</span><span class="sxs-lookup"><span data-stu-id="0b559-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="0b559-141">Tutte le query dei metadati dell'istanza fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="0b559-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="0b559-142">Output dei dati</span><span class="sxs-lookup"><span data-stu-id="0b559-142">Data output</span></span>
<span data-ttu-id="0b559-143">Per impostazione predefinita, servizio metadati dell'istanza di hello restituisce i dati in formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="0b559-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="0b559-144">Tuttavia, API diverse possono restituire dati in formati diversi se necessario.</span><span class="sxs-lookup"><span data-stu-id="0b559-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="0b559-145">Hello nella tabella seguente è un riferimento di altri formati di dati che potrebbero supportare le API.</span><span class="sxs-lookup"><span data-stu-id="0b559-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="0b559-146">API</span><span class="sxs-lookup"><span data-stu-id="0b559-146">API</span></span> | <span data-ttu-id="0b559-147">Formato dati predefinito</span><span class="sxs-lookup"><span data-stu-id="0b559-147">Default Data Format</span></span> | <span data-ttu-id="0b559-148">Altri formati</span><span class="sxs-lookup"><span data-stu-id="0b559-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="0b559-149">/instance</span><span class="sxs-lookup"><span data-stu-id="0b559-149">/instance</span></span> | <span data-ttu-id="0b559-150">json</span><span class="sxs-lookup"><span data-stu-id="0b559-150">json</span></span> | <span data-ttu-id="0b559-151">text</span><span class="sxs-lookup"><span data-stu-id="0b559-151">text</span></span>
<span data-ttu-id="0b559-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0b559-152">/scheduledevents</span></span> | <span data-ttu-id="0b559-153">json</span><span class="sxs-lookup"><span data-stu-id="0b559-153">json</span></span> | <span data-ttu-id="0b559-154">Nessuno</span><span class="sxs-lookup"><span data-stu-id="0b559-154">none</span></span>

<span data-ttu-id="0b559-155">tooaccess un formato di risposta non predefinito, specificare il formato richiesto di hello come parametro querystring nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="0b559-156">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0b559-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="0b559-157">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="0b559-157">Security</span></span>
<span data-ttu-id="0b559-158">endpoint di servizio metadati dell'istanza di Hello è accessibile solo dall'interno hello esegue l'istanza di macchina virtuale in un indirizzo IP non è instradabile.</span><span class="sxs-lookup"><span data-stu-id="0b559-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="0b559-159">Inoltre, qualsiasi richiesta con un `X-Forwarded-For` intestazione viene rifiutata dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="0b559-160">È inoltre necessario richieste toocontain un `Metadata: true` tooensure intestazione che hello richiesta effettiva è stata direttamente previsto e che non fa parte di reindirizzamento non intenzionale.</span><span class="sxs-lookup"><span data-stu-id="0b559-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="0b559-161">Errore</span><span class="sxs-lookup"><span data-stu-id="0b559-161">Error</span></span>
<span data-ttu-id="0b559-162">Se è presente un elemento di dati non trovato o una richiesta in formato non corretto, hello servizio metadati dell'istanza restituisce errori HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="0b559-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="0b559-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0b559-163">For example:</span></span>

<span data-ttu-id="0b559-164">Codice di stato HTTP</span><span class="sxs-lookup"><span data-stu-id="0b559-164">HTTP Status Code</span></span> | <span data-ttu-id="0b559-165">Motivo</span><span class="sxs-lookup"><span data-stu-id="0b559-165">Reason</span></span>
----------------|-------
<span data-ttu-id="0b559-166">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0b559-166">200 OK</span></span> |
<span data-ttu-id="0b559-167">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="0b559-167">400 Bad Request</span></span> | <span data-ttu-id="0b559-168">Intestazione `Metadata: true` mancante</span><span class="sxs-lookup"><span data-stu-id="0b559-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="0b559-169">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="0b559-169">404 Not Found</span></span> | <span data-ttu-id="0b559-170">esistere Hello quando elemento richiesto</span><span class="sxs-lookup"><span data-stu-id="0b559-170">hello requested element does't exist</span></span> 
<span data-ttu-id="0b559-171">405 - Metodo non consentito</span><span class="sxs-lookup"><span data-stu-id="0b559-171">405 Method Not Allowed</span></span> | <span data-ttu-id="0b559-172">Sono supportate solo le richieste `GET` e `POST`</span><span class="sxs-lookup"><span data-stu-id="0b559-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="0b559-173">429 - Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="0b559-173">429 Too Many Requests</span></span> | <span data-ttu-id="0b559-174">l'API di Hello attualmente supporta un massimo di 5 query al secondo</span><span class="sxs-lookup"><span data-stu-id="0b559-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="0b559-175">500 - Errore del servizio</span><span class="sxs-lookup"><span data-stu-id="0b559-175">500 Service Error</span></span>     | <span data-ttu-id="0b559-176">Ripetere l'operazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="0b559-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="0b559-177">esempi</span><span class="sxs-lookup"><span data-stu-id="0b559-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-178">Tutte le risposte delle API sono stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="0b559-178">All API responses are JSON strings.</span></span> <span data-ttu-id="0b559-179">Tutte le risposte di esempio che seguono sono di tipo pretty-print per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="0b559-180">Recupero delle informazioni di rete</span><span class="sxs-lookup"><span data-stu-id="0b559-180">Retrieving network information</span></span>

<span data-ttu-id="0b559-181">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="0b559-182">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-183">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0b559-183">hello response is a JSON string.</span></span> <span data-ttu-id="0b559-184">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-184">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="0b559-185">Recupero dell'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="0b559-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="0b559-186">Recupero di tutti i metadati per un'istanza</span><span class="sxs-lookup"><span data-stu-id="0b559-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="0b559-187">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="0b559-188">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-189">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0b559-189">hello response is a JSON string.</span></span> <span data-ttu-id="0b559-190">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-190">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="0b559-191">Recupero dei metadati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="0b559-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="0b559-192">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-192">**Request**</span></span>

<span data-ttu-id="0b559-193">I metadati dell'istanza possono essere recuperati in Windows tramite l'utilità di PowerShell hello `curl`:</span><span class="sxs-lookup"><span data-stu-id="0b559-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="0b559-194">O tramite hello `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0b559-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="0b559-195">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-196">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0b559-196">hello response is a JSON string.</span></span> <span data-ttu-id="0b559-197">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-197">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="0b559-198">Categorie di dati dei metadati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="0b559-198">Instance metadata data categories</span></span>
<span data-ttu-id="0b559-199">Hello seguenti categorie di dati sono disponibile tramite hello servizio metadati dell'istanza:</span><span class="sxs-lookup"><span data-stu-id="0b559-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="0b559-200">Dati</span><span class="sxs-lookup"><span data-stu-id="0b559-200">Data</span></span> | <span data-ttu-id="0b559-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b559-201">Description</span></span>
-----|------------
<span data-ttu-id="0b559-202">location</span><span class="sxs-lookup"><span data-stu-id="0b559-202">location</span></span> | <span data-ttu-id="0b559-203">Hello area Azure VM è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="0b559-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="0b559-204">name</span><span class="sxs-lookup"><span data-stu-id="0b559-204">name</span></span> | <span data-ttu-id="0b559-205">Nome della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0b559-205">Name of hello VM</span></span> 
<span data-ttu-id="0b559-206">offer</span><span class="sxs-lookup"><span data-stu-id="0b559-206">offer</span></span> | <span data-ttu-id="0b559-207">Offrono informazioni per l'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-207">Offer information for hello VM image.</span></span> <span data-ttu-id="0b559-208">Questo valore è presente solo per le immagini distribuite dalla raccolta di immagini di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b559-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="0b559-209">publisher</span><span class="sxs-lookup"><span data-stu-id="0b559-209">publisher</span></span> | <span data-ttu-id="0b559-210">Server di pubblicazione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0b559-210">Publisher of hello VM image</span></span>
<span data-ttu-id="0b559-211">sku</span><span class="sxs-lookup"><span data-stu-id="0b559-211">sku</span></span> | <span data-ttu-id="0b559-212">SKU specifico per l'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0b559-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="0b559-213">version</span><span class="sxs-lookup"><span data-stu-id="0b559-213">version</span></span> | <span data-ttu-id="0b559-214">Versione dell'immagine di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0b559-214">Version of hello VM image</span></span> 
<span data-ttu-id="0b559-215">osType</span><span class="sxs-lookup"><span data-stu-id="0b559-215">osType</span></span> | <span data-ttu-id="0b559-216">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="0b559-216">Linux or Windows</span></span> 
<span data-ttu-id="0b559-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="0b559-217">platformUpdateDomain</span></span> |  <span data-ttu-id="0b559-218">[Dominio di aggiornamento](manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="0b559-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="0b559-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="0b559-219">platformFaultDomain</span></span> | <span data-ttu-id="0b559-220">[Dominio di errore](manage-availability.md) hello macchina virtuale è in esecuzione in</span><span class="sxs-lookup"><span data-stu-id="0b559-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="0b559-221">vmId</span><span class="sxs-lookup"><span data-stu-id="0b559-221">vmId</span></span> | <span data-ttu-id="0b559-222">[Identificatore univoco](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) per hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="0b559-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="0b559-223">vmSize</span></span> | [<span data-ttu-id="0b559-224">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0b559-224">VM size</span></span>](sizes.md)
<span data-ttu-id="0b559-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="0b559-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="0b559-226">Indirizzo IPv4 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="0b559-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0b559-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="0b559-228">Indirizzo IPv4 pubblico di hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="0b559-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="0b559-229">subnet/address</span></span> | <span data-ttu-id="0b559-230">Indirizzo di subnet di hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-230">Subnet address of hello VM</span></span>
<span data-ttu-id="0b559-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="0b559-231">subnet/prefix</span></span> | <span data-ttu-id="0b559-232">Prefisso della subnet, ad esempio 24</span><span class="sxs-lookup"><span data-stu-id="0b559-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="0b559-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="0b559-233">ipv6/ipAddress</span></span> | <span data-ttu-id="0b559-234">Indirizzo IPv6 locale di hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="0b559-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="0b559-235">macAddress</span></span> | <span data-ttu-id="0b559-236">Indirizzo mac della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0b559-236">VM mac address</span></span> 
<span data-ttu-id="0b559-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0b559-237">scheduledevents</span></span> | <span data-ttu-id="0b559-238">Attualmente in anteprima pubblica. Vedere [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="0b559-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="0b559-239">Scenari di utilizzo di esempio</span><span class="sxs-lookup"><span data-stu-id="0b559-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="0b559-240">Rilevamento della macchina virtuale in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="0b559-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="0b559-241">Come provider di servizi, potrebbe essere necessario numero hello tootrack delle macchine virtuali in esecuzione il software o gli agenti necessari tootrack l'univocità di hello VM.</span><span class="sxs-lookup"><span data-stu-id="0b559-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="0b559-242">toobe in grado di tooget un ID univoco per una macchina virtuale, utilizzare hello `vmId` campo servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0b559-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="0b559-243">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="0b559-244">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="0b559-245">Posizionamento di contenitori, dominio di aggiornamento/errore basato su partizioni dati</span><span class="sxs-lookup"><span data-stu-id="0b559-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="0b559-246">Per alcuni scenari, il posizionamento di repliche dati diverse è di importanza primaria.</span><span class="sxs-lookup"><span data-stu-id="0b559-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="0b559-247">Ad esempio, [posizionamento delle repliche HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la selezione host contenitore tramite un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) richieda è hello tooknow `platformFaultDomain` e `platformUpdateDomain` hello macchina virtuale è in esecuzione in.</span><span class="sxs-lookup"><span data-stu-id="0b559-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="0b559-248">È possibile ottenere i dati direttamente tramite hello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0b559-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="0b559-249">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="0b559-250">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="0b559-251">Ulteriori informazioni su hello VM durante il caso di supporto</span><span class="sxs-lookup"><span data-stu-id="0b559-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="0b559-252">Come provider di servizi, si potrebbero ottenere una chiamata al supporto in cui si desidera tooknow ulteriori informazioni sulla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="0b559-253">Porre hello cliente tooshare hello calcolo metadati possono fornire informazioni di base per hello supporto professionale tooknow su tipo hello della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="0b559-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="0b559-254">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0b559-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="0b559-255">**Risposta**</span><span class="sxs-lookup"><span data-stu-id="0b559-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0b559-256">risposta Hello è una stringa JSON.</span><span class="sxs-lookup"><span data-stu-id="0b559-256">hello response is a JSON string.</span></span> <span data-ttu-id="0b559-257">Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-257">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="0b559-258">Esempi di chiamate del servizio di metadati utilizzando diversi linguaggi all'interno di hello VM</span><span class="sxs-lookup"><span data-stu-id="0b559-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="0b559-259">Lingua</span><span class="sxs-lookup"><span data-stu-id="0b559-259">Language</span></span> | <span data-ttu-id="0b559-260">Esempio</span><span class="sxs-lookup"><span data-stu-id="0b559-260">Example</span></span> 
---------|----------------
<span data-ttu-id="0b559-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="0b559-261">Ruby</span></span>     | <span data-ttu-id="0b559-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="0b559-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="0b559-263">Go Lan</span><span class="sxs-lookup"><span data-stu-id="0b559-263">Go Lan</span></span>   | <span data-ttu-id="0b559-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="0b559-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="0b559-265">python</span><span class="sxs-lookup"><span data-stu-id="0b559-265">python</span></span>   | <span data-ttu-id="0b559-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="0b559-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="0b559-267">C++</span><span class="sxs-lookup"><span data-stu-id="0b559-267">C++</span></span>      | <span data-ttu-id="0b559-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="0b559-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="0b559-269">C#</span><span class="sxs-lookup"><span data-stu-id="0b559-269">C#</span></span>       | <span data-ttu-id="0b559-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="0b559-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="0b559-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0b559-271">Javascript</span></span> | <span data-ttu-id="0b559-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="0b559-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="0b559-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b559-273">Powershell</span></span> | <span data-ttu-id="0b559-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="0b559-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="0b559-275">Bash</span><span class="sxs-lookup"><span data-stu-id="0b559-275">Bash</span></span>       | <span data-ttu-id="0b559-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="0b559-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="0b559-277">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0b559-277">FAQ</span></span>
1. <span data-ttu-id="0b559-278">Viene visualizzato l'errore hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="0b559-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="0b559-279">Che cosa significa?</span><span class="sxs-lookup"><span data-stu-id="0b559-279">What does this mean?</span></span>
   * <span data-ttu-id="0b559-280">Servizio metadati dell'istanza di Hello richiede intestazione hello `Metadata: true` toobe passato nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="0b559-281">Il passaggio di questa intestazione nella chiamata REST hello consente accesso toohello servizio metadati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="0b559-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="0b559-282">Perché non riesco a ottenere le informazioni di calcolo per la macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="0b559-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="0b559-283">Hello servizio metadati dell'istanza supporta attualmente solo le istanze create con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b559-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="0b559-284">In hello future, si potrebbe aggiungere supporto per le macchine virtuali del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="0b559-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="0b559-285">Ho creato la mia macchina virtuale tramite Azure Resource Manager tempo fa.</span><span class="sxs-lookup"><span data-stu-id="0b559-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="0b559-286">Perché non riesco a vedere le informazioni sui metadati di calcolo?</span><span class="sxs-lookup"><span data-stu-id="0b559-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="0b559-287">Per tutte le macchine virtuali create dopo settembre 2016, aggiungere un [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart vedere calcolo metadati.</span><span class="sxs-lookup"><span data-stu-id="0b559-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="0b559-288">Per macchine virtuali meno recenti (Create prima di settembre 2016), aggiungere o rimuovere estensioni o dati dischi toohello VM toorefresh metadati.</span><span class="sxs-lookup"><span data-stu-id="0b559-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="0b559-289">Perché viene visualizzato errore hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="0b559-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="0b559-290">Inviare di nuovo la richiesta basata sul sistema di backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="0b559-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="0b559-291">Se il problema di hello persiste, contattare il supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b559-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="0b559-292">Dove posso condividere domande o commenti aggiuntivi?</span><span class="sxs-lookup"><span data-stu-id="0b559-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="0b559-293">Inviare i propri commenti accedendo alla pagina http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="0b559-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="0b559-294">Il servizio funziona per l'istanza del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="0b559-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="0b559-295">Sì, il Servizio metadati è disponibile per le istanze del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="0b559-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="0b559-296">Come ottenere supporto per il servizio hello?</span><span class="sxs-lookup"><span data-stu-id="0b559-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="0b559-297">supporto tooget per il servizio di hello, creare un problema di supporto nel portale di Azure per la macchina virtuale in cui non si risposta dei metadati in grado di tooget dopo tentativi lunghi hello</span><span class="sxs-lookup"><span data-stu-id="0b559-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Supporto per i metadati dell'istanza](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="0b559-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b559-299">Next steps</span></span>

- <span data-ttu-id="0b559-300">Altre informazioni su hello [agli eventi pianificati](scheduled-events.md) API **in anteprima pubblica** fornita da servizio metadati dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="0b559-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
