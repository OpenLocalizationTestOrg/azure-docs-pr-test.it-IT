---
title: tooresource aaaIntroduction risoluzione dei problemi in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di risoluzione dei problemi di hello Watcher di rete risorsa"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Introduzione tooresource risoluzione dei problemi in Watcher di rete di Azure

I gateway di rete virtuale forniscono la connettività tra le risorse locali e altre reti virtuali in Azure. Monitoraggio di questi gateway e le relative connessioni è fondamentale tooensuring comunicazione non viene interrotta. Watcher di rete fornisce hello funzionalità tootroubleshoot gateway di rete virtuale e le connessioni. Questo può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST. Quando viene chiamato, Watcher di rete individua integrità hello di gateway di rete virtuale hello o connessione e risultati appropriati hello restituito. Questa richiesta è una transazione con esecuzione prolungata, vengono restituiti risultati hello una volta completata la diagnosi di hello.

![portal][2]

## <a name="results"></a>Risultati

Hello preliminare risultati assegnano un'immagine complessiva dell'integrità di hello della risorsa hello. È possibile fornire informazioni più approfondite per le risorse come illustrato nella seguente sezione hello:

Hello elenco seguente include i valori hello restituiti con hello risolvere API:

* **startTime** -questo valore è ora hello hello risolvere chiamata API avviato.
* **endTime** -questo valore è ora hello quando la risoluzione dei problemi di hello è terminata.
* **code**: questo valore è UnHealthy in caso di singolo errore di diagnosi.
* **risultati** -risultati è una raccolta di risultati restituito nel gateway di rete virtuale di connessione o hello hello.
    * **ID** -questo valore è il tipo di errore hello.
    * **riepilogo** -questo valore è riportato un riepilogo dell'errore hello.
    * **dettagliate** -questo valore fornisce una descrizione dettagliata dell'errore hello.
    * **recommendedActions** -questa proprietà è una raccolta di tootake le azioni consigliate.
      * **actionText** -questo valore contiene testo hello che descrive quale tootake di azione.
      * **actionUri** -questo valore fornisce hello URI toodocumentation sulla tooact.
      * **actionUriText** -questo valore è una breve descrizione di testo dell'azione hello.

Hello seguenti tabelle Mostra hello diversi tipi di errore (id in risultati da hello precede elenco) che sono disponibili e, se l'errore hello Crea registri.

### <a name="gateway"></a>Gateway

| Tipo di errore | Motivo | Log|
|---|---|---|
| NoFault | Non viene rilevato alcun errore. |Sì|
| GatewayNotFound | Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning. |No|
| PlannedMaintenance |  L'istanza del gateway è in fase di manutenzione.  |No|
| UserDrivenUpdate | È in corso l'aggiornamento utente. Potrebbe trattarsi di un'operazione di ridimensionamento. | No |
| VipUnResponsive | Impossibile raggiungere l'istanza primaria di hello di hello Gateway. Ciò accade quando hello probe di integrità non riesce. | No |
| PlatformInActive | Si verifica un problema con la piattaforma di hello. | No|
| ServiceNotRunning | servizio di Hello sottostante non è in esecuzione. | No|
| NoConnectionsFoundForGateway | Nessuna connessione esista nel gateway hello. Questo è solo un avviso.| No|
| ConnectionsNotConnected | Le connessioni non sono connesse. Questo è solo un avviso.| Sì|
| GatewayCPUUsageExceeded | utilizzo della CPU Gateway corrente Hello è > 95%. | Sì |

### <a name="connection"></a>Connessione

| Tipo di errore | Motivo | Log|
|---|---|---|
| NoFault | Non viene rilevato alcun errore. |Sì|
| GatewayNotFound | Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning. |No|
| PlannedMaintenance | L'istanza del gateway è in fase di manutenzione.  |No|
| UserDrivenUpdate | È in corso l'aggiornamento utente. Potrebbe trattarsi di un'operazione di ridimensionamento.  | No |
| VipUnResponsive | Impossibile raggiungere l'istanza primaria di hello di hello Gateway. Verifica quando hello probe di integrità non riesce. | No |
| ConnectionEntityNotFound | La configurazione della connessione non è presente. | No |
| ConnectionIsMarkedDisconnected | Connessione Hello è contrassegnato come "disconnessa". |No|
| ConnectionNotConfiguredOnGateway | servizio sottostante Hello non dispone di hello che connessione configurata. | Sì |
| ConnectionMarkedStandy | Hello servizio sottostante viene contrassegnato come standby.| Sì|
| Autenticazione | Mancata corrispondenza della chiave precondivisa. | Sì|
| PeerReachability | gateway di Hello peer non è raggiungibile. | Sì|
| IkePolicyMismatch | gateway peer Hello dispone di criteri di IKE che non sono supportati da Azure. | Sì|
| WfpParse Error | Errore durante l'analisi dei log di piattaforma filtro Windows hello. |Sì|

## <a name="supported-gateway-types"></a>Tipi di gateway supportati

Hello elenco riportato di seguito viene illustrato il supporto di hello Mostra quali i gateway e le connessioni sono supportate con la risoluzione dei problemi di controllo di rete.
|  |  |
|---------|---------|
|**Tipi di gateway**   |         |
|VPN      | Supportato        |
|ExpressRoute | Non supportato |
|Hypernet | Non supportato|
|**Tipi di VPN** | |
|Basato su route | Supportato|
|Basata su criteri | Non supportato|
|**Tipi di connessione**||
|IPsec| Supportato|
|Vnet2Vnet| Supportato|
|ExpressRoute| Non supportato|
|Hypernet| Non supportato|
|VPNClient| Non supportato|

## <a name="log-files"></a>File di log

file di log sulla risoluzione dei problemi di Hello risorse vengono archiviati in un account di archiviazione dopo la risoluzione dei problemi di risorse completata. Hello immagine seguente mostra contenuto di esempio hello di una chiamata che ha restituito un errore.

![File ZIP][1]

> [!NOTE]
> In alcuni casi, solo un subset hello di file di log viene scritto toostorage.

Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Un altro strumento che può essere usato è Storage Explorer. Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Hello **ConnectionStats.txt** file contiene statistiche generali di hello connessione, inclusi i byte in ingresso e in uscita, lo stato di connessione e hello ora hello è stata stabilita una connessione.

> [!NOTE]
> Se hello chiamata toohello risoluzione dei problemi di API restituisce integro, unica hello restituito nel file zip hello è un **ConnectionStats.txt** file.

contenuto Hello di questo file è simile toohello esempio seguente:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Hello **CPUStats.txt** file contiene l'utilizzo della CPU e memoria disponibile in fase di hello del test.  contenuto Hello di questo file è simile toohello esempio seguente:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Hello **IKEErrors.txt** file contiene gli eventuali errori di IKE che sono stati trovati durante il monitoraggio.

Hello esempio seguente viene illustrato il contenuto di hello di un file IKEErrors.txt. Gli errori potrebbero essere diversi in base al problema hello.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

Hello **Scrubbed wfpdiag.txt** file di log contiene il log di piattaforma filtro Windows hello. Questo log contiene la registrazione del pacchetto ignorato e degli errori IKE/AuthIP.

Hello esempio seguente viene illustrato il contenuto di hello del file di Scrubbed wfpdiag.txt hello. In questo esempio, hello la chiave condivisa di una connessione non è corretta come si può notare dalla riga di 3 hello dal basso hello. Hello di esempio seguente è semplicemente un frammento di codice dell'intero log hello, come log hello può risultare lungo in base al problema hello.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

Hello **wfpdiag.txt.sum** file è un registro contenente i buffer hello e gli eventi elaborati.

Hello esempio seguente è contenuto hello di un file di wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come gateway VPN toodiagnose e le connessioni tramite hello portale visitando [risoluzione dei problemi Gateway - portale di Azure](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
