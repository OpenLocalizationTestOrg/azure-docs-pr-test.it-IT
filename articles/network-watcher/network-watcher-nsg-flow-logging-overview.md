---
title: Introduzione alla registrazione dei flussi per i gruppi di sicurezza di rete con Network Watcher | Microsoft Docs
description: "Questa pagina illustra come usare i log dei flussi dei gruppi di sicurezza di rete, una funzionalità di Azure Network Watcher"
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
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="94887-103">Introduzione alla registrazione dei flussi per i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="94887-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="94887-104">I log di flusso del gruppo di sicurezza di rete sono una funzionalità di Network Watcher che consente di visualizzare le informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="94887-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="94887-105">Sono scritti in formato JSON e mostrano i flussi in ingresso e in uscita in base a regole, scheda di rete a cui si applica il flusso, informazioni su 5 tuple relative al flusso (IP di origine/destinazione, porta di origine/destinazione, protocollo), e se il traffico è consentito o meno.</span><span class="sxs-lookup"><span data-stu-id="94887-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![Panoramica dei log dei flussi][1]

<span data-ttu-id="94887-107">Anche se i log dei flussi specificano come destinazione gruppi di sicurezza di rete, non vengono visualizzati come gli altri log.</span><span class="sxs-lookup"><span data-stu-id="94887-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="94887-108">I log dei flussi vengono archiviati solo in un account di archiviazione e hanno un percorso di registrazione come quello dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="94887-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="94887-109">Ai log dei flussi si applicano gli stessi criteri di conservazione degli altri log.</span><span class="sxs-lookup"><span data-stu-id="94887-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="94887-110">Il criterio di conservazione dei log può essere impostato su un valore compreso tra 1 giorno e 365 giorni.</span><span class="sxs-lookup"><span data-stu-id="94887-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="94887-111">Se non viene impostato alcun criterio di conservazione, i log vengono conservati per sempre.</span><span class="sxs-lookup"><span data-stu-id="94887-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="94887-112">File di log</span><span class="sxs-lookup"><span data-stu-id="94887-112">Log file</span></span>

<span data-ttu-id="94887-113">I log dei flussi hanno più proprietà.</span><span class="sxs-lookup"><span data-stu-id="94887-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="94887-114">L'elenco seguente indica le proprietà restituite nel log del flusso del gruppo di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="94887-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="94887-115">**time**: ora in cui l'evento è stato registrato.</span><span class="sxs-lookup"><span data-stu-id="94887-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="94887-116">**systemId**: ID risorsa del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="94887-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="94887-117">**category**: categoria dell'evento, che è sempre NetworkSecurityGroupFlowEvent.</span><span class="sxs-lookup"><span data-stu-id="94887-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="94887-118">**resourceid**: ID risorsa del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="94887-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="94887-119">**operationName**: sempre NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="94887-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="94887-120">**properties**: raccolta di proprietà del flusso.</span><span class="sxs-lookup"><span data-stu-id="94887-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="94887-121">**Version**: numero di versione dello schema di eventi del log dei flussi.</span><span class="sxs-lookup"><span data-stu-id="94887-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="94887-122">**flows**: raccolta di flussi.</span><span class="sxs-lookup"><span data-stu-id="94887-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="94887-123">Questa proprietà ha più voci per regole diverse.</span><span class="sxs-lookup"><span data-stu-id="94887-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="94887-124">**rule**: regola per cui vengono elencati i flussi.</span><span class="sxs-lookup"><span data-stu-id="94887-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="94887-125">**flows**: raccolta di flussi.</span><span class="sxs-lookup"><span data-stu-id="94887-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="94887-126">**mac**: indirizzo MAC della scheda di interfaccia di rete per la VM in cui è stato raccolto il flusso.</span><span class="sxs-lookup"><span data-stu-id="94887-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="94887-127">**flowTuples**: stringa che contiene più proprietà per la tupla del flusso nel formato con valori separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="94887-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="94887-128">**Time Stamp**: questo valore è il timestamp di quando si è verificato il flusso in formato UNIX EPOCH.</span><span class="sxs-lookup"><span data-stu-id="94887-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="94887-129">**Source IP**: IP di origine.</span><span class="sxs-lookup"><span data-stu-id="94887-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="94887-130">**Destination IP**: IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94887-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="94887-131">**Source Port**: porta di origine.</span><span class="sxs-lookup"><span data-stu-id="94887-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="94887-132">**Destination Port**: porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94887-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="94887-133">**Protocol**: protocollo del flusso.</span><span class="sxs-lookup"><span data-stu-id="94887-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="94887-134">I valori validi sono **T** per TCP e **U** per UDP.</span><span class="sxs-lookup"><span data-stu-id="94887-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="94887-135">**Traffic Flow**: direzione del flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="94887-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="94887-136">I valori validi sono **I** per traffico in ingresso e **O** per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="94887-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="94887-137">**Traffic**: indica se il traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="94887-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="94887-138">I valori validi sono **A** per il traffico consentito e **D** per il traffico negato.</span><span class="sxs-lookup"><span data-stu-id="94887-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="94887-139">Di seguito è riportato un esempio di log dei flussi.</span><span class="sxs-lookup"><span data-stu-id="94887-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="94887-140">Come si può osservare, più record seguono l'elenco di proprietà descritto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="94887-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="94887-141">I valori della proprietà flowTuples sono un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="94887-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="94887-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94887-142">Next steps</span></span>

<span data-ttu-id="94887-143">Per informazioni su come abilitare i log dei flussi, vedere [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md) (Abilitazione della registrazione dei flussi).</span><span class="sxs-lookup"><span data-stu-id="94887-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="94887-144">Per informazioni sulla registrazione dei Gruppi di sicurezza di rete, vedere [Analisi dei log per i gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="94887-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="94887-145">Per sapere se il traffico è consentito o negato in una VM, vedere [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare il traffico con la verifica del flusso IP)</span><span class="sxs-lookup"><span data-stu-id="94887-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

