---
title: registrazione di tooflow aaaIntroduction per gruppi di sicurezza di rete con il Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene illustrato come flusso NSG toouse registra una funzionalità del controllo di rete di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="d17bf-103">Registrazione tooflow introduzione per gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="d17bf-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="d17bf-104">I registri del flusso di gruppo di sicurezza di rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d17bf-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="d17bf-105">Questi registri di flusso sono scritti in formato json e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="d17bf-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![Panoramica dei log di flusso][1]

<span data-ttu-id="d17bf-107">Mentre il flusso di log di gruppi di sicurezza di rete di destinazione, non vengono visualizzati hello stesso come hello altri log.</span><span class="sxs-lookup"><span data-stu-id="d17bf-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="d17bf-108">I log di flusso vengono archiviati solo all'interno di un account di archiviazione e il percorso di registrazione hello seguente come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d17bf-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="d17bf-109">Hello stesso log tooflow di applicare i criteri di conservazione in altri log.</span><span class="sxs-lookup"><span data-stu-id="d17bf-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="d17bf-110">Registri di disporre di criteri di conservazione che possono essere impostato da giorni too365 1 giorno.</span><span class="sxs-lookup"><span data-stu-id="d17bf-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="d17bf-111">Se non è impostato un criterio di conservazione, hello registri vengono mantenuti sempre.</span><span class="sxs-lookup"><span data-stu-id="d17bf-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="d17bf-112">File di log</span><span class="sxs-lookup"><span data-stu-id="d17bf-112">Log file</span></span>

<span data-ttu-id="d17bf-113">I log dei flussi hanno più proprietà.</span><span class="sxs-lookup"><span data-stu-id="d17bf-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="d17bf-114">Hello elenco riportato di seguito è riportato un elenco di proprietà hello che vengono restituiti all'interno del Registro di flusso NSG hello:</span><span class="sxs-lookup"><span data-stu-id="d17bf-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="d17bf-115">**tempo** - tempo quando è stato registrato l'evento hello</span><span class="sxs-lookup"><span data-stu-id="d17bf-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="d17bf-116">**systemId**: ID risorsa del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d17bf-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="d17bf-117">**categoria** -categoria di hello dell'evento hello, questo è sempre possibile NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="d17bf-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="d17bf-118">**ResourceID** -hello Id risorsa di hello NSG</span><span class="sxs-lookup"><span data-stu-id="d17bf-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="d17bf-119">**operationName**: sempre NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="d17bf-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="d17bf-120">**proprietà** -una raccolta di proprietà del flusso di hello</span><span class="sxs-lookup"><span data-stu-id="d17bf-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="d17bf-121">**Versione** -numero di versione dello schema di eventi di flusso di Log hello</span><span class="sxs-lookup"><span data-stu-id="d17bf-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="d17bf-122">**flows**: raccolta di flussi.</span><span class="sxs-lookup"><span data-stu-id="d17bf-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="d17bf-123">Questa proprietà ha più voci per regole diverse.</span><span class="sxs-lookup"><span data-stu-id="d17bf-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="d17bf-124">**regola** -regola per cui hello sono elencati i flussi</span><span class="sxs-lookup"><span data-stu-id="d17bf-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="d17bf-125">**flows**: raccolta di flussi.</span><span class="sxs-lookup"><span data-stu-id="d17bf-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="d17bf-126">**Mac** -hello indirizzo MAC di hello NIC per la macchina virtuale in cui vengono raccolti flusso hello hello</span><span class="sxs-lookup"><span data-stu-id="d17bf-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="d17bf-127">**flowTuples** -stringa che contiene più proprietà per hello flusso tupla in formato delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="d17bf-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="d17bf-128">**Data e ora** -questo valore è timestamp hello di quando si è verificato il flusso di hello in formato epoca UNIX</span><span class="sxs-lookup"><span data-stu-id="d17bf-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="d17bf-129">**IP di origine** : hello IP di origine</span><span class="sxs-lookup"><span data-stu-id="d17bf-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="d17bf-130">**Destinazione IP** -hello IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="d17bf-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="d17bf-131">**Porta di origine** : hello porta di origine</span><span class="sxs-lookup"><span data-stu-id="d17bf-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="d17bf-132">**Porta di destinazione** -hello porta di destinazione</span><span class="sxs-lookup"><span data-stu-id="d17bf-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="d17bf-133">**Protocollo** -hello protocollo del flusso di hello.</span><span class="sxs-lookup"><span data-stu-id="d17bf-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="d17bf-134">I valori validi sono **T** per TCP e **U** per UDP.</span><span class="sxs-lookup"><span data-stu-id="d17bf-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="d17bf-135">**Traffico** -hello direzione del flusso di traffico hello.</span><span class="sxs-lookup"><span data-stu-id="d17bf-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="d17bf-136">I valori validi sono **I** per traffico in ingresso e **O** per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="d17bf-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="d17bf-137">**Traffic**: indica se il traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="d17bf-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="d17bf-138">I valori validi sono **A** per il traffico consentito e **D** per il traffico negato.</span><span class="sxs-lookup"><span data-stu-id="d17bf-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="d17bf-139">Hello Ecco un esempio di un flusso di log.</span><span class="sxs-lookup"><span data-stu-id="d17bf-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="d17bf-140">Come si può notare, sono presenti più record che seguono l'elenco di proprietà hello descritto nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="d17bf-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="d17bf-141">I valori nella proprietà flowTuples hello sono un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="d17bf-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="d17bf-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d17bf-142">Next steps</span></span>

<span data-ttu-id="d17bf-143">Informazioni su modalità di registrazione tooenable flusso visitando [registrazione abilitazione flusso](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d17bf-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="d17bf-144">Per informazioni sulla registrazione dei Gruppi di sicurezza di rete, vedere [Analisi dei log per i gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="d17bf-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="d17bf-145">Per sapere se il traffico è consentito o negato in una VM, vedere [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare il traffico con la verifica del flusso IP)</span><span class="sxs-lookup"><span data-stu-id="d17bf-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

