---
title: archiviazione tooconnectivity aaaIntroduction Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello capacità di connessione Watcher di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Introduzione tooconnectivity archiviazione Watcher di rete di Azure

Hello funzionalità di connettività di rete Watcher fornisce hello funzionalità toocheck una connessione TCP diretta da una macchina virtuale tooa macchina virtuale (VM), il nome di dominio completo (FQDN), un URI o l'indirizzo IPv4. Gli scenari di rete sono complessi e vengono implementati mediante l'uso di gruppi di sicurezza di rete, firewall, route definite dall'utente e risorse fornite da Azure. La risoluzione dei problemi di connettività nella configurazioni complesse è un compito impegnativo. Watcher di rete consente di ridurre hello quantità di tempo toofind e rilevare i problemi di connettività. risultati Hello restituiti forniscono informazioni dettagliate in sia un problema di connettività di scadenza tooa piattaforma o un problema di configurazione utente. È possibile controllare la connettività con [PowerShell](network-watcher-connectivity-powershell.md), l'[interfaccia della riga di comando di Azure](network-watcher-connectivity-cli.md) e l'[API REST](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`. Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Response

Hello nella tabella seguente mostra le proprietà di hello restituite quando una verifica della connettività ha completato l'esecuzione.

|Proprietà  |Descrizione  |
|---------|---------|
|ConnectionStatus     | stato Hello di verifica della connettività hello. I risultati possibili sono **Reachable** e **Unreachable**.        |
|AvgLatencyInMs     | Latenza media durante la verifica della connettività hello in millisecondi. Visualizzata solo se lo stato del controllo è reachable.        |
|MinLatencyInMs     | La latenza minima durante connettività hello controllare in millisecondi. Visualizzata solo se lo stato del controllo è reachable.        |
|MaxLatencyInMs     | La latenza massima di connettività hello durante la verifica in millisecondi. Visualizzata solo se lo stato del controllo è reachable.        |
|ProbesSent     | Numero di probe inviato durante il controllo hello. Il valore massimo è 100.        |
|ProbesFailed     | Numero di probe che non è riuscita durante il controllo hello. Il valore massimo è 100.        |
|Hops     | Hop dal percorso di hop dall'origine toodestination.        |
|Hops[].Type     | Tipo di risorsa. I valori possibili sono **Source**, **VirtualAppliance**, **VnetLocal** e **Internet**.        |
|Hops[].Id | Identificatore univoco dell'hop hello.|
|Hops[].Address | Indirizzo IP dell'hop hello.|
|Hops[].ResourceId | ResourceID dell'hop hello se hop hello è una risorsa di Azure. Se si tratta di una risorsa Internet, l'ID risorsa è **Internet**. |
|Hops[].NextHopIds | Identificatore univoco di Hello dell'hop successivo di hello eseguita.|
|Hops[].Issues | Raccolta di problemi che si sono verificati durante il controllo hello tale hop. Se sono non stati problemi, il valore di hello è vuoto.|
|Hops[].Issues[].Origin | Hop di corrente di hello, in cui si è verificato problema. I valori possibili sono:<br/> **Connessioni in entrata** -problema è collegamento hello hello precedente hop toohello corrente dell'hop<br/>**In uscita** -problema è collegamento hello hello corrente hop toohello dell'hop successivo<br/>**Locale** -problema è hop corrente hello.|
|Hops[].Issues[].Severity | gravità Hello di hello problema rilevato. I valori possibili sono **Error** e **Warning**. |
|Hops[].Issues[].Type |tipo di Hello del problema rilevato. I valori possibili sono: <br/>**CPU**<br/>**Memoria**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |Dettagli relativi hello problema rilevato.|
|Hops[].Issues[].Context[].key |La chiave di hello coppia chiave / valore restituito.|
|Hops[].Issues[].Context[].value |Valore di hello coppia chiave / valore restituito.|

Hello Ecco un esempio di un problema rilevato su un hop.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Tipi di errore

verifica della connettività Hello restituisce i tipi di errore relativi alla connessione hello. Hello nella tabella seguente fornisce un elenco di hello corrente tipi di errore restituito.

|Tipo  |Descrizione  |
|---------|---------|
|CPU     | Utilizzo elevato della CPU.       |
|Memoria     | Uso intensivo della memoria.       |
|GuestFirewall     | Il traffico viene bloccato a causa di configurazione del firewall tooa macchina virtuale.        |
|DNSResolution     | Risoluzione DNS non riuscita per l'indirizzo di destinazione hello.        |
|NetworkSecurityRule    | Traffico bloccato da una regola NSG. La regola viene restituita.        |
|UserDefinedRoute|Il traffico viene eliminato a causa di definito dall'utente tooa o di sistema. |

### <a name="next-steps"></a>Passaggi successivi

Informazioni su come risorsa di tooa tooverify connettività visitando: [verificare la connettività con il Watcher di rete di Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

