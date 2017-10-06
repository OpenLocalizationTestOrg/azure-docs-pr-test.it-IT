---
title: "Convalidare la velocità effettiva VPN tooa rete virtuale di Microsoft Azure | Documenti Microsoft"
description: "scopo di questo documento Hello è toohelp velocità effettiva della rete hello da loro tooan risorse locali macchina virtuale di Azure di convalidare un utente."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>La rete virtuale tooa toovalidate VPN velocità effettiva

Una connessione gateway VPN consente connettività cross-premise sicura, tooestablish tra la rete virtuale in Azure e locale infrastruttura IT.

Questo articolo illustra come velocità effettiva della rete toovalidate da hello locale tooan risorse macchina virtuale di Azure. Fornisce inoltre informazioni aggiuntive sulla risoluzione dei problemi.

>[!NOTE]
>Questo articolo è dedicato toohelp diagnosticare e risolvere i problemi comuni. Se si problema hello toosolve Impossibile utilizzando le seguenti informazioni, hello [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Panoramica

connessione del gateway VPN Hello prevede hello seguenti componenti:

- Dispositivo VPN locale (visualizzare un elenco di [dispositivi VPN convalidati](vpn-gateway-about-vpn-devices.md#devicetable)).
- Internet pubblico
- Gateway VPN di Azure
- Macchina virtuale di Azure

Hello seguente diagramma mostra la connettività logico hello di un tooan di rete locale rete virtuale di Azure tramite VPN.

![Logica della connettività di rete del cliente tooMSFT rete tramite la VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Calcolare hello massimo previsto in ingresso e uscita

1.  Determinare i requisiti di velocità effettiva di base dell'applicazione.
2.  Determinare i limiti di velocità effettiva del gateway VPN di Azure. Per informazioni, vedere la sezione hello "velocità effettiva aggregata dal tipo SKU e VPN" di [pianificazione e progettazione per il Gateway VPN](vpn-gateway-plan-design.md).
3.  Determinare hello [indicazioni di velocità effettiva di macchina virtuale di Azure](../virtual-machines/virtual-machines-windows-sizes.md) per la dimensione della macchina virtuale.
4.  Determinare la larghezza di banda del provider di servizi Internet (ISP).
5.  Eseguire il calcolo di velocità effettiva prevista - larghezza di banda minima di (macchina virtuale, gateway, ISP) * 0,8.

Se la velocità effettiva di calcolato non soddisfa i requisiti di velocità effettiva della linea di base dell'applicazione, è necessario tooincrease della larghezza di banda hello della risorsa hello identificato come collo di bottiglia hello. tooresize un Gateway VPN di Azure, vedere [la modifica di un gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize una macchina virtuale, vedere [ridimensiona una macchina virtuale](../virtual-machines/virtual-machines-windows-resize-vm.md). Se non si verificano previsto della larghezza di banda Internet, è inoltre possibile toocontact provider di servizi Internet.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Convalidare la velocità effettiva della rete mediante gli strumenti di prestazioni

È consigliabile eseguire questa convalida al di fuori delle ore di punta, poiché la saturazione della velocità effettiva del tunnel VPN durante il test non fornisce risultati accurati.

lo strumento di Hello che viene usato per questo test è iPerf, che funziona in Windows e Linux e le modalità client e server. È limitato too3 Gbps per macchine virtuali di Windows.

Questo strumento non esegue qualsiasi toodisk di operazioni di lettura/scrittura. Produce solo il traffico TCP generato automaticamente da un fine toohello altri. Il metodo generato statistiche in base a sperimentazione che misura hello della larghezza di banda disponibile tra i nodi di client e server. Durante il test tra due nodi, uno funge da server hello e hello altri come client. Una volta completato il test, è consigliabile che non è invertire hello ruoli tootest entrambi caricare e scaricare la velocità effettiva in entrambi i nodi.

### <a name="download-iperf"></a>Scaricare iPerf
Eseguire il download di [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Per dettagli, vedere la [documentazione di iPerf](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >Hello terze parti citati in questo articolo prodotti da aziende indipendenti da Microsoft. Microsoft non fornisce alcuna garanzia, implicita o esplicita, sulle prestazioni di hello o all'affidabilità di questi prodotti.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Eseguire iPerf (iperf3.exe)
1. Abilitare una regola ACL di NSG/consenta il traffico di hello (per l'indirizzo IP pubblico test nella macchina virtuale di Azure).

2. In entrambi i nodi abilitare un'eccezione firewall per la porta 5001.

    **Windows:** comando che segue hello di Esegui come amministratore:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    regola di hello tooremove durante il test è stata completata, eseguire questo comando:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Linux di Azure**: le immagini Linux di Azure dispongono di firewall permissivi. Se è presente un'applicazione in attesa su una porta, è consentito il traffico hello attraverso. Per le immagini personalizzate protette potrebbero essere necessarie porte aperte in modo esplicito. Firewall a livello di sistema operativo Linux comuni includono `iptables`, `ufw` o `firewalld`.

3. Nel nodo server hello modificare toohello directory in cui viene estratto iperf3.exe. Quindi eseguire iPerf in modalità server e impostare toolisten sulla porta 5001 come hello seguenti comandi:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Nel nodo client hello, modificare toohello directory in cui iperf strumento verrà estratti e quindi eseguire hello comando seguente:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    client hello è la generazione di traffico in porta 5001 toohello server per 30 secondi. Hello flag '-P ' indicante che si sono usando 32 nodi server toohello di connessioni simultanee.

    Hello seguente schermata Mostra output di hello di questo esempio:

    ![Output](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (Facoltativo) toopreserve hello test risultati, eseguiti questo comando:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Dopo aver completato i passaggi precedenti hello, eseguire hello stessi passaggi con i ruoli di hello invertiti, in modo che hello nodo server sarà client hello e viceversa.

## <a name="address-slow-file-copy-issues"></a>Risolvere i problemi di esecuzione lenta della copia dei file
È possibile che la copia dei file venga eseguita lentamente quando si usa Esplora risorse o il trascinamento della selezione tramite una sessione RDP. Questo problema è in genere a causa di tooone o entrambi hello seguenti fattori:

- Le applicazioni di copia dei file, ad esempio Esplora risorse e RDP, non usano più thread durante la copia dei file. Per ottenere prestazioni migliori, utilizzare un'applicazione di copia di file a thread multipli, ad esempio [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) file toocopy con 16 o 32 thread. numero di thread hello toochange per la copia dei file in Richcopy, fare clic su **azione** > **opzioni Copia** > **copia del File**.<br><br>
![Problemi di esecuzione lenta della copia dei file](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Velocità di lettura/scrittura disco macchina virtuale insufficiente. Per altre informazioni, vedere [Risoluzione dei problemi di Archiviazione di Azure](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interfaccia con connessione rivolta all'esterno del dispositivo locale
Se hello in locale il dispositivo VPN indirizzo IP con connessione Internet è incluso in hello [rete locale](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definizione in Azure, potrebbero verificarsi toobring impossibilità hello disconnette VPN, sporadici errori o problemi di prestazioni.

## <a name="checking-latency"></a>Verifica della latenza
Utilizzare tracert tootrace tooMicrosoft bordo Azure dispositivo toodetermine se sono presenti eventuali ritardi superiore a 100 ms tra hop.

Esecuzione dalla rete locale hello, *tracert* toohello VIP di hello Azure Gateway o la macchina virtuale. Dopo aver visualizzato solo * restituito, si conosce è stato raggiunto hello Azure edge. Quando vengono visualizzati i nomi DNS che includono "MSN" restituito, si conosce che è stato raggiunto il backbone Microsoft hello.<br><br>
![Controllo della latenza](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni o assistenza, vedere hello seguenti collegamenti:

- [Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
