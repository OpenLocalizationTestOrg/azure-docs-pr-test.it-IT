---
title: errori del Gateway non valido di Gateway applicazione Azure (502) aaaTroubleshoot | Documenti Microsoft
description: Informazioni su come errori tootroubleshoot 502 Gateway applicazione
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
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Risoluzione degli errori del gateway non valido nel gateway applicazione

Informazioni su come errori (502) gateway non valido di tootroubleshoot ricevuto quando si usa il gateway applicazione.

## <a name="overview"></a>Panoramica

Dopo aver configurato un gateway applicazione, uno degli errori di hello che gli utenti possono incontrare è "Errore del Server: 502 - server Web ha ricevuto una risposta non valida che agisce come gateway o proxy server". Questo errore può verificarsi a causa di toohello seguenti motivi:

* Il [pool back-end del gateway applicazione di Azure non è configurato o è vuoto](#empty-backendaddresspool).
* Nessuna delle macchine virtuali hello o le istanze in [Set di scalabilità della macchina virtuale sono integri](#unhealthy-instances-in-backendaddresspool).
* Macchine virtuali o le istanze di Set di scalabilità della macchina virtuale back-end sono [non risponde probe di integrità predefinito toohello](#problems-with-default-health-probe.md).
* [Configurazione dei probe di integrità personalizzati](#problems-with-custom-health-probe.md) non valida o inappropriata.
* [Problemi di timeout della richiesta o di connettività](#request-time-out) con le richieste degli utenti.

## <a name="empty-backendaddresspool"></a>BackendAddressPool vuoto

### <a name="cause"></a>Causa

Se hello Gateway applicazione non dispone di nessuna macchina virtuale o il Set di scalabilità della macchina virtuale è configurato nel pool di indirizzi back-end di hello, grado di instradare le richieste del cliente e genera un errore di gateway non valido.

### <a name="solution"></a>Soluzione

Verificare che il pool di indirizzi back-end di hello non sia vuoto. A tale scopo è possibile usare PowerShell, l'interfaccia della riga di comando o il portale.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

output di Hello dalla precedente cmdlet hello deve contenere i pool di indirizzi back-end non vuoto. Di seguito è riportato un esempio in cui vengono restituiti due pool configurati con indirizzi IP o FQDN (nome di dominio completo) per le macchine virtuali back-end. stato di hello BackendAddressPool provisioning Hello deve essere 'completato'.

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

Se tutte le istanze di hello di BackendAddressPool sono integri, Gateway applicazione non avrebbero qualsiasi richiesta utente tooroute back-end. Potrebbe anche trattarsi case hello quando le istanze di back-end sono integri, ma non dispone di un'applicazione hello necessario distribuita.

### <a name="solution"></a>Soluzione

Verificare che le istanze di hello siano integri e un'applicazione hello sia configurata correttamente. Controllare se le istanze di back-end hello sono in grado di toorespond tooa ping da un'altra macchina virtuale nella stessa rete virtuale hello. Se configurato con un punto di fine pubblico, assicurarsi che un'applicazione di web browser toohello richiesta è utilizzabile dai servizi.

## <a name="problems-with-default-health-probe"></a>Problemi con il probe di integrità predefinito

### <a name="cause"></a>Causa

502 errori possono anche essere indicative che hello probe di integrità predefinito è tooreach non in grado di macchine virtuali di back-end. Quando viene eseguito il provisioning di un'istanza di Gateway applicazione, viene configurato automaticamente un tooeach probe di integrità predefinito BackendAddressPool utilizzando le proprietà di hello BackendHttpSetting. Input dell'utente è obbligatorio tooset questo probe. In particolare, quando viene configurata una regola di bilanciamento del carico, viene creata un'associazione tra BackendHttpSetting e BackendAddressPool. Un probe predefinito viene configurato per ognuna di queste associazioni e un'istanza di integrità periodici controllo connessione tooeach in hello BackendAddressPool hello porta specificata nell'elemento BackendHttpSetting hello avvia di Gateway applicazione. Nella tabella seguente sono elencati i valori di hello associati probe di integrità hello predefinito.

| Proprietà probe | Valore | Descrizione |
| --- | --- | --- |
| URL probe |http://127.0.0.1/ |Percorso URL |
| Interval |30 |Intervallo di probe in secondi |
| Timeout |30 |Timeout di probe in secondi |
| Soglia non integra |3 |Numero di tentativi di probe. server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello. |

### <a name="solution"></a>Soluzione

* Verificare che sia stato configurato un sito predefinito e che sia in ascolto su 127.0.0.1.
* Se BackendHttpSetting specifica una porta diversa dalla 80, sito predefinito hello deve essere configurato toolisten su tale porta.
* Hello toohttp://127.0.0.1:port chiamata deve restituire un codice di risultato HTTP 200. Questo metodo deve essere restituito nel periodo di timeout di 30 secondi hello.
* Verificare che la porta configurata è aperta e che non esistono regole del firewall o i gruppi di sicurezza rete di Azure, che blocca il traffico in ingresso o in uscita sulla porta hello configurato.
* Se un servizio Cloud o macchine virtuali di Azure classiche è usato con FQDN o indirizzo IP pubblico, assicurarsi di hello corrispondenti [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) viene aperto.
* Se hello VM è configurato con Azure Resource Manager e non è compreso tra reti virtuali in cui viene distribuito il Gateway applicazione, hello [Network Security Group](../virtual-network/virtual-networks-nsg.md) deve essere configurato tooallow accesso hello desiderato porta.

## <a name="problems-with-custom-health-probe"></a>Problemi con il probe di integrità personalizzato

### <a name="cause"></a>Causa

Probe di integrità personalizzato consentono una maggiore flessibilità toohello di ricerca predefinite comportamento. Quando si utilizzano probe personalizzati, gli utenti possono configurare intervallo probe "hello", l'URL di hello e percorso tootest e quanti tooaccept risposte non riuscito prima di contrassegnare l'istanza del pool back-end di hello come non integro. Hello seguenti proprietà aggiuntive viene aggiunte.

| Proprietà probe | Descrizione |
| --- | --- |
| Nome |Nome del probe hello. Questo nome è di tipo probe toohello toorefer utilizzati nelle impostazioni HTTP back-end. |
| Protocol |Protocollo utilizzato probe hello toosend. probe Hello hello protocollo definito nelle impostazioni HTTP back-end di hello |
| Host |Probe di hello toosend nome host. Applicabile solo quando vengono configurati più siti nel gateway applicazione. Questo nome è diverso dal nome host della macchina virtuale. |
| Path |Percorso relativo del probe hello. path valido Hello inizia con '/'. probe Hello viene inviato troppo\<protocollo\>://\<host\>:\<porta\>\<percorso\> |
| Interval |Intervallo di probe in secondi. Questo è l'intervallo di tempo hello tra due probe consecutivi. |
| Timeout |Timeout del probe in secondi. Se una risposta valida non viene ricevuta entro questo periodo di timeout, probe hello è contrassegnato come non riuscito. |
| Soglia non integra |Numero di tentativi di probe. server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello. |

### <a name="solution"></a>Soluzione

Convalidare tale hello che probe di integrità personalizzato sia configurato correttamente come hello tabella precedente. Inoltre, toohello precedente risoluzione dei problemi, anche verificare hello segue:

* Verificare che probe hello sia specificato correttamente in base alle hello [Guida](application-gateway-create-probe-ps.md).
* Se il Gateway applicazione è configurato per un singolo sito, da hello predefinito Host nome deve essere specificato come '127.0.0.1', se non diversamente configurato in probe personalizzato.
* Verificare che una chiamata toohttp: / /\<host\>:\<porta\>\<percorso\> restituisce un codice di risultato HTTP 200.
* Verificare che siano all'interno di intervalli accettabili hello intervallo, timeout e UnhealtyThreshold.
* Se tramite HTTPS probe, assicurarsi che il server back-end hello non richiede SNI tramite la configurazione di un certificato di fallback sul server back-end di hello stesso. 
* Verificare che siano all'interno di intervalli accettabili hello intervallo, timeout e UnhealtyThreshold.

## <a name="request-time-out"></a>Timeout della richiesta

### <a name="cause"></a>Causa

Quando viene ricevuta una richiesta dell'utente, Gateway applicazione applica hello configurata regole toohello richiesta e lo indirizza tooa istanza del pool di back-end. È in attesa per un intervallo di tempo per una risposta dall'istanza di back-end hello configurabile. Per impostazione predefinita, l'intervallo è impostato su **30 secondi**. Se il gateway applicazione non riceve una risposta dall'applicazione back-end in questo intervallo, alla richiesta dell'utente viene assegnato un errore 502.

### <a name="solution"></a>Soluzione

Gateway applicazione consente agli utenti tooconfigure questa impostazione tramite BackendHttpSetting, che può essere quindi applicati toodifferent pool. I diversi pool back-end possono avere BackendHttpSetting differenti e quindi una diversa configurazione del timeout della richiesta.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Passaggi successivi

Se hello passaggi precedenti non risolvono il problema di hello, aprire un [ticket di supporto](https://azure.microsoft.com/support/options/).

