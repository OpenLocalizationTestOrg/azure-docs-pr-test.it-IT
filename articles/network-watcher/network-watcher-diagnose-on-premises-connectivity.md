---
title: "connettività locale aaaDiagnose tramite gateway VPN con il Watcher di rete di Azure | Documenti Microsoft"
description: "In questo articolo viene descritto come toodiagnose locale connettività tramite il gateway VPN con la risoluzione dei problemi di risorse Watcher di rete di Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnosticare la connettività locale tramite i gateway VPN

Gateway VPN di Azure permette di soluzione ibrida toocreate che consentono di risolvere hello sia necessaria una connessione sicura tra la rete locale e la rete virtuale di Azure. Perché i requisiti sono univoci, pertanto viene scelta hello del dispositivo VPN locale. Azure supporta attualmente [diversi dispositivi VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) costantemente che vengono convalidati in collaborazione con fornitori di dispositivi hello. Esaminare le impostazioni di configurazione specifiche del dispositivo hello prima di configurare il dispositivo VPN locale. Analogamente, il gateway VPN di Azure viene configurato con un set di [parametri IPsec supportati](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) che vengono usati per stabilire le connessioni. Attualmente non è alcun modo toospecify o selezionare una combinazione specifica di parametri IPsec da Gateway VPN di Azure hello. Per stabilire una connessione tra sedi locali e Azure, hello locale impostazioni del dispositivo VPN devono essere in base ai parametri IPsec hello prescritti dal Gateway VPN di Azure. Se hello impostazioni sono corrette, si verifica una perdita di connettività e fino ad ora risoluzione di questi problemi, non è semplice e in genere richiesto ore tooidentify e correzione problema hello.

Risolvere i problemi funzionalità con hello Watcher di rete di Azure, si sono in grado di toodiagnose eventuali problemi con il Gateway e connessioni e in pochi minuti toomake sufficienti informazioni un problema di hello toorectify decisione informata in merito.

## <a name="scenario"></a>Scenario

Si desidera che la connessione tooconfigure un sito a sito tra Azure e locali utilizzando FortiGate come hello VPN del Gateway locale. tooachieve questo scenario, si richiede hello dopo l'installazione:

1. Gateway di rete virtuale - hello Gateway VPN in Azure
1. Gateway di rete locale - hello [(FortiGate) del Gateway VPN locale](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) rappresentazione nel cloud di Azure
1. Connessione da sito a sito (criteri di base) - [connessione tra Gateway VPN hello e hello locale router](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configurazione di FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Sono disponibili istruzioni passo passo dettagliate per la configurazione di una configurazione da sito a sito, visitare il sito: [creare una rete virtuale con una connessione da sito a sito usando il portale di Azure hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Uno dei passaggi di configurazione critiche hello consiste nella configurazione di parametri di comunicazione IPsec hello, qualsiasi errore di configurazione comporta tooloss di connettività tra Azure e di rete locale hello. Gateway VPN di Azure non sono attualmente configurato toosupport hello seguenti parametri di IPsec per la fase 1. Come indicato in precedenza, non è possibile modificare queste impostazioni.  Come vede nella tabella hello riportata di seguito, gli algoritmi di crittografia hello supportati dal Gateway VPN di Azure sono AES256 AES128 e 3DES.

### <a name="ike-phase-1-setup"></a>Configurazione fase 1 IKE

| **Proprietà** | **PolicyBased** | **Gateway VPN RouteBased e con prestazioni elevate o standard** |
| --- | --- | --- |
| Versione IKE |IKEv1 |IKEv2 |
| Diffie-Hellman Group |Gruppo 2 (1024 bit) |Gruppo 2 (1024 bit) |
| Metodo di autenticazione |Chiave precondivisa |Chiave precondivisa |
| Algoritmi di crittografia |AES256 AES128 3DES |AES256 3DES |
| Algoritmo di hash |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Durata (tempo) associazione di sicurezza (SA) fase 1 |28.800 secondi |10.800 secondi |

Come un utente, sarà necessario tooconfigure il FortiGate, un esempio di configurazione è reperibile in [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Inavvertitamente come è stata configurata la toouse FortiGate SHA-512 hello algoritmo hash. Questo algoritmo non è supportato per le connessioni basate su criteri, quindi la connessione VPN non funziona.

Questi problemi sono tootroubleshoot disco rigido e cause principali sono spesso non intuitivi. In questo caso, è possibile aprire un ticket di supporto tooget assistenza nella risoluzione problema hello. Con l'API di risoluzione dei problemi di Azure Network Watcher è tuttavia possibile identificare questi problemi autonomamente.

## <a name="troubleshooting-using-azure-network-watcher"></a>Risoluzione dei problemi tramite Azure Network Watcher

toodiagnose la connessione, connettersi tooAzure PowerShell e avviare hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. È possibile trovare i dettagli di hello sull'utilizzo di questo cmdlet nel [connessioni - PowerShell e risolvere i problemi di Gateway di rete virtuale](network-watcher-troubleshoot-manage-powershell.md). Questo cmdlet potrebbe richiedere toofew minuti toocomplete.

Una volta completata la hello cmdlet, è possibile passare il percorso di archiviazione toohello specificato nel cmdlet hello tooget informazioni dettagliate sul problema hello sui registri. Watcher di rete di Azure crea una cartella di zip che contiene i seguenti file di log hello:

![1][1]

File aperti hello chiamato IKEErrors.txt e Visualizza seguente hello errore, che indica un problema con una configurazione errata impostazione IKE in locale.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

È possibile ottenere informazioni dettagliate da hello Scrubbed wfpdiag.txt errore hello, come in questo caso viene indicato che si è verificato `ERROR_IPSEC_IKE_POLICY_MATCH` che tooconnection lead non funziona correttamente.

Un altro errore di configurazione comune è hello specificando le chiavi condivise non corrette. In caso di hello sopra riportato è stato specificato diverse chiavi condivise, hello IKEErrors.txt Mostra hello il seguente errore: `Error: Authentication failed. Check shared key`.

Watcher di rete di Azure risolvere i problemi di funzionalità consente toodiagnose e risolvere i problemi del Gateway VPN e una connessione con facilità hello di un semplice cmdlet di PowerShell. Attualmente è supportare la diagnosi hello seguenti condizioni e funzionino verso altre condizioni aggiunte.

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
| ConnectionsNotConnected | Nessuna delle connessioni hello connessi. Questo è solo un avviso.| Sì|
| GatewayCPUUsageExceeded | utilizzo del Gateway corrente Hello l'utilizzo della CPU è > 95%. | Sì |

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

## <a name="next-steps"></a>Passaggi successivi

Informazioni di connettività Gateway VPN toocheck con PowerShell e automazione di Azure, visitare il sito [gateway VPN di monitoraggio di risoluzione dei problemi di controllo di rete di Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
