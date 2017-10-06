---
title: per la replica tooAzure VMware con il ripristino del sito di rete aaaPlan | Documenti Microsoft
description: Questo articolo illustra la pianificazione di rete necessaria per la replica di macchine virtuali di Azure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Passaggio 3: Pianificare la rete per la replica di macchine virtuali di Azure

Dopo aver verificato hello [prerequisiti di distribuzione](azure-to-azure-walkthrough-prerequisites.md), leggere questo hello toounderstand articolo considerazioni relative alla replica e il ripristino delle macchine virtuali di Azure (VM) da un'area di Azure tooanother, di rete utilizzando hello Servizio di Azure Site Recovery. 

- Dopo aver articolo hello, è necessario un clear comprensione delle modalità tooset backup in uscita di accesso per le macchine virtuali di Azure si desidera tooreplicate e le macchine virtuali toothose dei siti tooconnect da locale.
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> La replica di macchine virtuali di Azure con il servizio Site Recovery è attualmente disponibile in anteprima.



## <a name="network-overview"></a>Panoramica della rete

In genere le macchine virtuali di Azure si trovano in una rete/subnet virtuale Azure ed è una connessione tra il tooAzure sito locale con Azure ExpressRoute o una connessione VPN.

Le reti sono in genere protette tramite firewall e/o gruppi di sicurezza rete. Firewall consente URL basato su elenchi basato su IP, la connettività di rete toocontrol. I gruppi di sicurezza di rete fanno uso di regole basate su intervalli IP. 


Per il ripristino del sito toowork previsto, è necessario toomake alcune modifiche della connettività di rete in uscita, da macchine virtuali che si desidera tooreplicate. Il ripristino del sito non supporta l'utilizzo di un'autenticazione proxy toocontrol della connettività di rete. Se si usa un proxy di autenticazione, non è possibile abilitare la replica. 


Hello diagramma seguente illustra un tipico ambiente per un'applicazione in esecuzione in macchine virtuali di Azure.

![customer-environment](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Ambiente di macchine virtuali di Azure**

Può inoltre essere un tooAzure connessione imposta da sito locale con Azure ExpressRoute o una connessione VPN. 

![customer-environment](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure connessione locale**



## <a name="outbound-connectivity-for-urls"></a>Connettività in uscita per gli URL

Se si utilizza una connettività di firewall basato su URL proxy toocontrol in uscita, assicurarsi che si consente a questi URL utilizzati per il ripristino del sito

**URL** | **Dettagli**  
--- | ---
*.blob.core.windows.net | Consente di toobe dati scritti da hello macchina virtuale, l'account di archiviazione toohello cache nell'area di origine hello.
login.microsoftonline.com | Fornisce autenticazione e autorizzazione tooSite gli URL del servizio di ripristino.
*.hypervrecoverymanager.windowsazure.com | Consente la comunicazione con il servizio di ripristino del sito da hello VM hello.
*.servicebus.windows.net | Obbligatorio in modo che è possibile scrivere dati di monitoraggio e diagnostica di Site Recovery hello hello macchina virtuale.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Connettività in uscita per gli intervalli di indirizzi IP

- È possibile creare automaticamente le regole di hello necessario su hello NSG, scaricare ed eseguire [questo script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- È consigliabile creare le regole NSG hello necessario in un gruppo di test e verificare che non siano presenti problemi, prima di creare regole hello in un gruppo di produzione.
- numero di hello necessario toocreate delle regole di gruppo, verificare che la sottoscrizione è abilitata. Contattare il supporto tecnico tooincrease hello NSG regola limite nella sottoscrizione.
Se si utilizza qualsiasi proxy firewall basato su IP o la connettività in uscita di NSG regole toocontrol, hello seguenti intervalli IP necessario toobe consentito, a seconda di percorsi di origine e destinazione hello delle macchine virtuali di hello:

    - Tutti gli intervalli di indirizzi IP che corrispondono a percorso di origine toohello. Download hello [intervalli](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Whitelist è necessaria, in modo che i dati possono essere scritti toohello account di archiviazione della cache di hello macchina virtuale.
    - Tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Se gli intervalli IP 365 tooOffice aggiunta nuovi indirizzi IP, è necessario toocreate nuove regole del gruppo.
-     Indirizzi IP dell'endpoint di servizio di Site Recovery, [disponibili in un file XML](https://aka.ms/site-recovery-public-ips), che variano a seconda della località di destinazione: 

   **Posizione di destinazione** | **IP del servizio Site Recovery** |  **IP di monitoraggio di Site Recovery**
   --- | --- | ---
   Asia orientale | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Asia sudorientale | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   India centrale | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   India meridionale | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Stati Uniti centro-settentrionali | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Europa settentrionale | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europa occidentale | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Stati Uniti orientali | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Stati Uniti occidentali | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Stati Uniti centro-meridionali | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Stati Uniti centrali | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Stati Uniti orientali 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Giappone orientale | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Giappone occidentale | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Brasile meridionale | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Australia orientale | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Australia sudorientale | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Canada centrale | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Canada orientale | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Stati Uniti centro-occidentali | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Stati Uniti occidentali 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Regno Unito occidentale | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Regno Unito meridionale | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="example-nsg-configuration"></a>Esempio di configurazione del gruppo di sicurezza di rete

In questa sezione viene illustrato come tooconfigure NSG regole, in modo che le repliche funziona per una macchina virtuale. Se si utilizza la connettività in uscita di NSG regole toocontrol, utilizzare le regole "Consenti HTTPS in uscita" per tutti gli intervalli IP hello necessario.

In questo esempio, il percorso di origine VM hello è "Stati Uniti orientali". percorso di destinazione di replica Hello è Central US.


### <a name="example"></a>Esempio

#### <a name="east-us"></a>Stati Uniti Orientali

1. Creare regole che corrisponde alle[intervalli IP Stati Uniti orientali](https://www.microsoft.com/download/confirmation.aspx?id=41653). Ciò è necessario in modo che i dati possono essere scritti toohello account di archiviazione della cache di hello macchina virtuale.
2. Creare regole per tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Creare regole che corrispondono toohello percorso di destinazione:

   **Posizione** | **IP del servizio Site Recovery** |  **IP di monitoraggio di Site Recovery**
    --- | --- | ---
   Stati Uniti centrali | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Stati Uniti centrali

Queste regole sono necessarie in modo che sia possibile abilitare la replica dal hello destinazione toohello origine paese, dopo il failover.

1. Creare regole che corrisponde alle[intervalli IP Usa centrale](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Creare regole per tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Creare regole che corrispondono toohello percorso di origine:

   **Posizione** | **IP del servizio Site Recovery** |  **IP di monitoraggio di Site Recovery**
    --- | --- | ---
   Stati Uniti orientali | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Connessione locale esistente

Se si dispone di una connessione VPN o ExpressRoute tra il sito locale e il percorso di origine hello in Azure, seguire queste linee guida:

**Configurazione** | **Dettagli**
--- | ---
**Tunneling forzato** | In genere una route predefinita (0.0.0.0/0) impone tooflow di traffico internet in uscita tramite una sede locale hello. ma non è una scelta consigliata. Il traffico di replica e le comunicazioni di Site Recovery devono rimanere all'interno di Azure.<br/><br/> Come soluzione, aggiungere le route definite dall'utente (UDRs) per [questi intervalli IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), in modo che il traffico di hello non passa in locale.
**Connettività** | Se le app devono essere presenti tooconnect tooon locale macchine o client locali connettono toohello app locale tramite VPN/ExpressRoute, accertarsi di avere almeno un [connessione site-to-site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), tra la destinazione hello regione di Azure e Hello nel sito locale.<br/><br/> Se i volumi di traffico sono elevati tra sito locale hello e di destinazione di hello regione di Azure, creare un altro [connessione ExpressRoute](../expressroute/expressroute-introduction.md), tra l'area di destinazione hello e locale.<br/><br/> Se si desidera tooretain gli indirizzi IP per le macchine virtuali dopo il failover, è possibile mantenere connessione sito a sito o ExpressRoute dell'area di destinazione hello in uno stato disconnesso. In questo modo nessun intervallo di conflitti tra hello origine e destinazione intervalli di indirizzi IP.
**ExpressRoute** | Creare un circuito ExpressRoute hello aree di origine e destinazione.<br/><br/> Creare una connessione tra la rete di origine hello e circuito ExpressRoute hello e tra la rete di destinazione hello e circuito hello.<br/><br/> È consigliabile usare diversi intervalli IP nelle aree di origine e di destinazione. Hello circuito non sarà in grado di tooconnect toomore rispetto a reti di uno Azure con hello stesso intervalli IP in hello contemporaneamente.<br/><br/> È possibile creare reti virtuali con hello stesso IP intervalli in entrambe le aree e quindi creare circuiti ExpressRoute in entrambe le aree. Per il failover, disconnettere il circuito hello dalla rete virtuale di origine hello e connettersi circuito hello nella rete virtuale di destinazione hello.<br/><br/> Se l'area primaria hello è completamente verso il basso, hello disconnettere l'operazione potrebbe non riuscire. In questo caso, rete virtuale di destinazione hello otterranno la connettività di ExpressRoute.
**ExpressRoute Premium** | È possibile creare circuiti in hello stessa regione di natura geopolitica.<br/><br/> circuiti toocreate nelle diverse aree geografiche geopolitici, è necessario Azure ExpressRoute Premium.<br/><br/> Con Premium, il costo di hello è incrementale. Per coloro che la usano già non sono previsti costi aggiuntivi.<br/><br/> Altre informazioni sulle [località](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e i [prezzi](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 4: creare un insieme di credenziali](azure-to-azure-walkthrough-vault.md)

