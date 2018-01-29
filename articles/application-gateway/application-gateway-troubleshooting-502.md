---
title: Risolvere gli errori di gateway non valido (502) nel gateway applicazione di Azure | Microsoft Docs
description: Informazioni su come risolvere gli errori 502 del gateway applicazione
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: e0099734a81cd8b1edf5cf80cb56b5c322a5feee
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Risoluzione degli errori del gateway non valido nel gateway applicazione

Informazioni su come risolvere gli errori di gateway non valido (502) ricevuti durante l'uso di un gateway applicazione.

## <a name="overview"></a>Panoramica

Dopo aver configurato un gateway applicazione, uno degli errori che gli utenti possono riscontrare è "Errore del server: 502 - Risposta non valida ricevuta dal server Web in funzione come server proxy o gateway". Questo errore può verificarsi a causa dei principali motivi seguenti:

* Un gruppo di sicurezza di rete, una route definita dall'utente o un DNS personalizzato sta bloccando l'accesso ai membri del pool back-end.
* Le macchine virtuali back-end o le istanze del set di scalabilità di macchine virtuali [non rispondono al probe di integrità predefinito](#problems-with-default-health-probe.md).
* [Configurazione dei probe di integrità personalizzati](#problems-with-custom-health-probe.md) non valida o inappropriata.
* Il [pool back-end del gateway applicazione di Azure non è configurato o è vuoto](#empty-backendaddresspool).
* Nessuna delle macchine virtuali o delle istanze nel [set di scalabilità di macchine virtuali è integra](#unhealthy-instances-in-backendaddresspool).
* [Problemi di timeout della richiesta o di connettività](#request-time-out) con le richieste degli utenti.

## <a name="network-security-group-user-defined-route-or-custom-dns-issue"></a>Problema di gruppo di sicurezza di rete, route definita dall'utente o DNS personalizzato

### <a name="cause"></a>Causa

Se l'accesso al back-end è bloccato a causa della presenza di un gruppo di sicurezza di rete, di una route definita dall'utente o di un DNS personalizzato, le istanze del gateway applicazione non saranno in grado di raggiungere il pool back-end e daranno origine a problemi di probe, causando errori 502. Si noti che possono essere presenti gruppi di sicurezza di rete/route definite dall'utente sia nella subnet del gateway applicazione, sia nella subnet in cui vengono distribuite le macchine virtuali delle applicazioni. In modo analogo, anche la presenza di un DNS personalizzato nella rete virtuale potrebbe causare problemi se si usa un nome di dominio completo per i membri del pool back-end e tale nome non viene risolto correttamente dal server DNS configurato dall'utente per la rete virtuale.

### <a name="solution"></a>Soluzione

Convalidare la configurazione di gruppo di sicurezza di rete, route definita dall'utente o DNS personalizzato tramite i passaggi seguenti:
* Controllare i gruppi di sicurezza di rete associati alla subnet del gateway applicazione. Verificare che la comunicazione con il back-end non sia bloccata.
* Controllare la route definita dall'utente associata alla subnet del gateway applicazione. Assicurarsi che la route definita dall'utente non indirizzi il traffico fuori dalla subnet del back-end. Controllare, ad esempio, che il routing verso appliance virtuali di rete o route predefinite venga annunciato alla subnet del gateway applicazione tramite ExpressRoute/VPN.

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name vnetName -ResourceGroupName rgName
Get-AzureRmVirtualNetworkSubnetConfig -Name appGwSubnet -VirtualNetwork $vnet
```

* Controllare il gruppo di sicurezza di rete e la route effettivi nella macchina virtuale back-end

```powershell
Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName nic1 -ResourceGroupName testrg
Get-AzureRmEffectiveRouteTable -NetworkInterfaceName nic1 -ResourceGroupName testrg
```

* Controllare se è presente un DNS personalizzato nella rete virtuale. È possibile eseguire questo controllo esaminando i dettagli delle proprietà della rete virtuale nell'output.

```json
Get-AzureRmVirtualNetwork -Name vnetName -ResourceGroupName rgName 
DhcpOptions            : {
                           "DnsServers": [
                             "x.x.x.x"
                           ]
                         }
```
Se presente, assicurarsi che il server DNS sia in grado di risolvere correttamente il nome di dominio completo del membro del pool back-end.

## <a name="problems-with-default-health-probe"></a>Problemi con il probe di integrità predefinito

### <a name="cause"></a>Causa

Gli errori 502 possono anche indicare frequentemente che il probe di integrità predefinito non riesce a raggiungere le VM back-end. Quando viene eseguito il provisioning di un'istanza del gateway applicazione, viene automaticamente configurato il probe di integrità predefinito per ogni BackendAddressPool tramite le proprietà del BackendHttpSetting. Per impostare il probe non è necessaria alcuna azione da parte dell'utente. In particolare, quando viene configurata una regola di bilanciamento del carico, viene creata un'associazione tra BackendHttpSetting e BackendAddressPool. Il probe predefinito viene configurato per ognuna di queste associazioni e il gateway applicazione avvia una connessione di controllo di integrità periodica su ogni istanza nel BackendAddressPool, sulla porta specificata nell'elemento BackendHttpSetting. La tabella seguente elenca i valori associati al probe di integrità predefinito.

| Proprietà probe | Valore | Descrizione |
| --- | --- | --- |
| URL probe |http://127.0.0.1/ |Percorso URL |
| Interval |30 |Intervallo di probe in secondi |
| Timeout |30 |Timeout di probe in secondi |
| Soglia non integra |3 |Numero di tentativi di probe. Il server back-end viene contrassegnato come inattivo dopo che il numero di errori di probe consecutivi ha raggiunto una soglia non integra. |

### <a name="solution"></a>Soluzione

* Verificare che sia stato configurato un sito predefinito e che sia in ascolto su 127.0.0.1.
* Se BackendHttpSetting specifica una porta diversa da 80, il sito predefinito deve essere configurato per ascoltare tale porta.
* La chiamata a http://127.0.0.1:port deve restituire un codice risultato HTTP di 200. Questo valore deve essere restituito entro il periodo di timeout di 30 secondi.
* Verificare che la porta configurata sia aperta e che non esistano regole del firewall o gruppi di sicurezza di rete di Azure che bloccano il traffico in ingresso o in uscita sulla porta configurata.
* Se le macchine virtuali classiche di Azure o il servizio cloud vengono usati con indirizzi FQDN o IP pubblici, verificare che l' [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) corrispondente sia aperto.
* Se la macchina virtuale è stata configurata tramite Azure Resource Manager e si trova all'esterno della rete virtuale in cui è distribuito il gateway applicazione, è necessario configurare un [Gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) per consentire l'accesso alla porta desiderata.

## <a name="problems-with-custom-health-probe"></a>Problemi con il probe di integrità personalizzato

### <a name="cause"></a>Causa

Il probe di integrità personalizzato consente una maggiore flessibilità per la ricerca di comportamenti predefiniti del probe. Quando si usano probe personalizzati, gli utenti possono configurare l'intervallo di probe, l'URL e il percorso da testare, nonché il numero di risposte non riuscite da accettare prima di contrassegnare l'istanza del pool back-end come non integra. Vengono aggiunte le seguenti proprietà aggiuntive.

| Proprietà probe | Descrizione |
| --- | --- |
| Nome |Nome del probe. Questo nome viene usato per fare riferimento al probe nelle impostazioni HTTP back-end |
| Protocollo |Protocollo usato per inviare il probe. Il probe usa il protocollo definito nelle impostazioni HTTP del back-end. |
| Host |Nome host per inviare il probe. Applicabile solo quando vengono configurati più siti nel gateway applicazione. Questo nome è diverso dal nome host della macchina virtuale. |
| Percorso |Percorso relativo del probe. Il percorso valido inizia da "/". Il probe viene inviato a \<protocollo\>://\<host\>:\<porta\>\<percorso\> |
| Interval |Intervallo di probe in secondi. Si tratta dell'intervallo di tempo tra due probe consecutivi. |
| Timeout |Timeout del probe in secondi. Se non viene ricevuta una risposta valida entro questo periodo di timeout, il probe viene contrassegnato come non riuscito. |
| Soglia non integra |Numero di tentativi di probe. Il server back-end viene contrassegnato come inattivo dopo che il numero di errori di probe consecutivi ha raggiunto una soglia non integra. |

### <a name="solution"></a>Soluzione

Verificare che il probe di integrità personalizzato sia configurato correttamente in base alla tabella precedente. In aggiunta alle procedure di risoluzione dei problemi precedenti, verificare anche quanto segue:

* Verificare che il probe sia specificato correttamente secondo le istruzioni della [guida](application-gateway-create-probe-ps.md).
* Se il gateway applicazione è configurato per un singolo sito, per impostazione predefinita il nome dell'host deve essere specificato come "127.0.0.1", se non diversamente configurato nel probe personalizzato.
* Verificare che la chiamata a http://\<host\>:\<porta\>\<percorso\> restituisca un codice risultato HTTP di 200.
* Assicurarsi che Intervallo, Timeout e Soglia non integra siano compresi in intervalli accettabili.
* Se si usa un probe HTTPS, assicurarsi che il server back-end non richieda SNI configurando un certificato di fallback nello stesso server back-end.

## <a name="request-time-out"></a>Timeout della richiesta

### <a name="cause"></a>Causa

Quando viene ricevuta una richiesta dell'utente, il gateway applicazione applica le regole configurate alla richiesta e la instrada a un'istanza del pool back-end. Attende quindi la risposta dall'istanza back-end per un intervallo di tempo configurabile. Per impostazione predefinita, l'intervallo è impostato su **30 secondi**. Se il gateway applicazione non riceve una risposta dall'applicazione back-end in questo intervallo, alla richiesta dell'utente viene assegnato un errore 502.

### <a name="solution"></a>Soluzione

Il gateway applicazione consente agli utenti di configurare questa impostazione tramite BackendHttpSetting, applicabile a pool diversi. I diversi pool back-end possono avere BackendHttpSetting differenti e quindi una diversa configurazione del timeout della richiesta.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="empty-backendaddresspool"></a>BackendAddressPool vuoto

### <a name="cause"></a>Causa

Se nel pool di indirizzi back-end non sono presenti macchine virtuali o set di scalabilità di macchine virtuali configurati, il gateway applicazione non può instradare le richieste del cliente e genera un errore di gateway non valido.

### <a name="solution"></a>Soluzione

Verificare che il pool di indirizzi back-end non sia vuoto. A tale scopo è possibile usare PowerShell, l'interfaccia della riga di comando o il portale.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

L'output del cmdlet precedente dovrebbe contenere un pool di indirizzi back-end non vuoto. Di seguito è riportato un esempio in cui vengono restituiti due pool configurati con indirizzi IP o FQDN (nome di dominio completo) per le macchine virtuali back-end. Lo stato del provisioning di BackendAddressPool deve essere "Succeeded".

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Istanze non integre in BackendAddressPool

### <a name="cause"></a>Causa

Se tutte le istanze di BackendAddressPool non sono integre, il gateway applicazione non avrà back-end a cui instradare la richiesta dell'utente. Questo potrebbe anche verificarsi quando le istanze back-end sono integre ma non è stata distribuita l'applicazione necessaria.

### <a name="solution"></a>Soluzione

Verificare che le istanze siano integre e che l'applicazione sia configurata correttamente. Controllare se le istanze back-end riescono a rispondere a un ping da un'altra VM nella stessa rete virtuale. Se configurato con un endpoint pubblico, verificare che sia valida la richiesta del browser per l'applicazione Web.

## <a name="next-steps"></a>Passaggi successivi

Se i passaggi precedenti non risolvono il problema, aprire un [ticket di supporto](https://azure.microsoft.com/support/options/).

