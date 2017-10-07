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
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Registrazione tooflow introduzione per gruppi di sicurezza di rete

I registri del flusso di gruppo di sicurezza di rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete. Questi registri di flusso sono scritti in formato json e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.

![Panoramica dei log di flusso][1]

Mentre il flusso di log di gruppi di sicurezza di rete di destinazione, non vengono visualizzati hello stesso come hello altri log. I log di flusso vengono archiviati solo all'interno di un account di archiviazione e il percorso di registrazione hello seguente come illustrato nell'esempio seguente hello:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hello stesso log tooflow di applicare i criteri di conservazione in altri log. Registri di disporre di criteri di conservazione che possono essere impostato da giorni too365 1 giorno. Se non è impostato un criterio di conservazione, hello registri vengono mantenuti sempre.

## <a name="log-file"></a>File di log

I log dei flussi hanno più proprietà. Hello elenco riportato di seguito è riportato un elenco di proprietà hello che vengono restituiti all'interno del Registro di flusso NSG hello:

* **tempo** - tempo quando è stato registrato l'evento hello
* **systemId**: ID risorsa del gruppo di sicurezza di rete.
* **categoria** -categoria di hello dell'evento hello, questo è sempre possibile NetworkSecurityGroupFlowEvent
* **ResourceID** -hello Id risorsa di hello NSG
* **operationName**: sempre NetworkSecurityGroupFlowEvents.
* **proprietà** -una raccolta di proprietà del flusso di hello
    * **Versione** -numero di versione dello schema di eventi di flusso di Log hello
    * **flows**: raccolta di flussi. Questa proprietà ha più voci per regole diverse.
        * **regola** -regola per cui hello sono elencati i flussi
            * **flows**: raccolta di flussi.
                * **Mac** -hello indirizzo MAC di hello NIC per la macchina virtuale in cui vengono raccolti flusso hello hello
                * **flowTuples** -stringa che contiene più proprietà per hello flusso tupla in formato delimitato da virgole
                    * **Data e ora** -questo valore è timestamp hello di quando si è verificato il flusso di hello in formato epoca UNIX
                    * **IP di origine** : hello IP di origine
                    * **Destinazione IP** -hello IP di destinazione
                    * **Porta di origine** : hello porta di origine
                    * **Porta di destinazione** -hello porta di destinazione
                    * **Protocollo** -hello protocollo del flusso di hello. I valori validi sono **T** per TCP e **U** per UDP.
                    * **Traffico** -hello direzione del flusso di traffico hello. I valori validi sono **I** per traffico in ingresso e **O** per il traffico in uscita.
                    * **Traffic**: indica se il traffico è stato consentito o negato. I valori validi sono **A** per il traffico consentito e **D** per il traffico negato.


Hello Ecco un esempio di un flusso di log. Come si può notare, sono presenti più record che seguono l'elenco di proprietà hello descritto nella precedente sezione hello. 

> [!NOTE]
> I valori nella proprietà flowTuples hello sono un elenco delimitato da virgole.
 
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

## <a name="next-steps"></a>Passaggi successivi

Informazioni su modalità di registrazione tooenable flusso visitando [registrazione abilitazione flusso](network-watcher-nsg-flow-logging-portal.md).

Per informazioni sulla registrazione dei Gruppi di sicurezza di rete, vedere [Analisi dei log per i gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-manage-log.md).

Per sapere se il traffico è consentito o negato in una VM, vedere [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare il traffico con la verifica del flusso IP)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

