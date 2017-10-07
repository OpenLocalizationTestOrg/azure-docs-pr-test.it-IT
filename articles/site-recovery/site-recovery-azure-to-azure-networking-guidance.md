---
title: Guida delle reti per la replica delle macchine virtuali dal tooAzure Azure Site Recovery aaaAzure | Documenti Microsoft
description: Materiale sussidiario del servizio di rete per la replica delle macchine virtuali di Azure
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
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Materiale sussidiario del servizio di rete per la replica delle macchine virtuali di Azure

>[!NOTE]
> La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.

Quando si ha la replica e il ripristino di macchine virtuali di Azure da una regione tooanother regione, i dettagli di questo articolo hello Guida delle reti di Azure Site Recovery. Per ulteriori informazioni sui requisiti di Azure Site Recovery, vedere hello [prerequisiti](site-recovery-prereq.md) articolo.

## <a name="site-recovery-architecture"></a>Architettura di Site Recovery

Il ripristino del sito fornisce un modo semplice di tooreplicate applicazioni in esecuzione su macchine virtuali di Azure tooanother area di Azure in modo che possano essere ripristinate se è presente un'interruzione nell'area primaria hello. Altre informazioni su [questo scenario e sull'architettura di Site Recovery](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Infrastruttura della rete in uso

Hello diagramma seguente illustra tipico ambiente Azure hello per un'applicazione in esecuzione in macchine virtuali di Azure:

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Se si utilizza Azure ExpressRoute o una connessione VPN da un tooAzure di rete locale, ambiente hello simile al seguente:

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

In genere, i clienti proteggono le proprie reti usando firewall e/o gruppi di sicurezza di rete. i firewall Hello è possono utilizzare basato su URL o basata su IP whitelist per controllare la connettività di rete. NSGs consentono le regole per l'utilizzo di connettività di rete toocontrol intervalli IP.

>[!IMPORTANT]
> Se si utilizza la connettività di rete toocontrol un proxy autenticato, non è supportata e non è possibile abilitare la replica di Site Recovery. 

Hello sezioni che seguono hello connettività in uscita modifiche che sono richiesti dalle macchine virtuali di Azure per il ripristino del sito toowork di replica.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Connettività in uscita per gli URL di Azure Site Recovery

Se si utilizza qualsiasi connettività in uscita di proxy toocontrol firewall basato su URL, essere toowhitelist che queste richieste di URL del servizio Azure Site Recovery:


**URL** | **Scopo**  
--- | ---
*.blob.core.windows.net | Obbligatorio in modo che i dati possono essere scritti toohello account di archiviazione della cache nell'area di origine hello da hello macchina virtuale.
login.microsoftonline.com | Obbligatorio per l'URL del servizio Site Recovery toohello autenticazione e autorizzazione.
*.hypervrecoverymanager.windowsazure.com | Necessarie per consentire la comunicazione dei servizi di ripristino del sito hello può verificarsi tra hello macchina virtuale.
*.servicebus.windows.net | Obbligatorio in modo che è possibile scrivere dati di monitoraggio e diagnostica di Site Recovery hello hello macchina virtuale.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Connettività in uscita per gli intervalli IP di Azure Site Recovery

>[!NOTE]
> tooautomatically creare regole NSG hello necessarie nel gruppo di sicurezza di rete hello, è possibile [scaricare e usare questo script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Si consiglia di creare le regole NSG hello necessario in un gruppo di sicurezza di rete di test e verificare che non siano presenti problemi prima di creare regole hello in un gruppo di sicurezza di rete di produzione.
> * numero di hello necessario toocreate delle regole di gruppo, verificare che la sottoscrizione è abilitata. Contattare il supporto tecnico tooincrease hello NSG regola limite nella sottoscrizione.

Se si utilizza qualsiasi proxy firewall basato su IP o la connettività in uscita di NSG regole toocontrol, hello seguenti intervalli IP necessario toobe consentito, a seconda di percorsi di origine e destinazione hello delle macchine virtuali di hello:

- Tutti gli intervalli IP che corrispondono toohello percorso di origine. (È possibile scaricare hello [intervalli IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) In modo che i dati possono essere scritti toohello account di archiviazione della cache di hello VM, è necessario Whitelist.

- Tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Se gli indirizzi IP di nuovo aggiunta intervalli IP 365 tooOffice in futuro hello occorre toocreate nuove regole del gruppo.
    
- IP dell'endpoint di servizio di Site Recovery ([disponibili in un file XML](https://aka.ms/site-recovery-public-ips)), che variano a seconda della posizione di destinazione: 

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

## <a name="sample-nsg-configuration"></a>Configurazione NSG di esempio
Questa sezione spiega le regole NSG hello passaggi tooconfigure in modo che la replica di Site Recovery può funzionare in una macchina virtuale. Se si utilizza la connettività in uscita di NSG regole toocontrol, utilizzare le regole "Consenti HTTPS in uscita" per tutti gli intervalli IP hello necessario.

>[!Note]
> tooautomatically creare regole NSG hello necessarie nel gruppo di sicurezza di rete hello, è possibile [scaricare e usare questo script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Ad esempio, se il percorso di origine della macchina virtuale è "Stati Uniti orientali" e il percorso di destinazione di replica è "Central US", procedura hello in hello nelle due sezioni successive.

>[!IMPORTANT]
> * Si consiglia di creare le regole NSG hello necessario in un gruppo di sicurezza di rete di test e verificare che non siano presenti problemi prima di creare regole hello in un gruppo di sicurezza di rete di produzione.
> * numero di hello necessario toocreate delle regole di gruppo, verificare che la sottoscrizione è abilitata. Contattare il supporto tecnico tooincrease hello NSG regola limite nella sottoscrizione. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Regole di gruppo nel gruppo di sicurezza di rete hello Stati Uniti orientali

* Creare regole che corrisponde alle[intervalli IP Stati Uniti orientali](https://www.microsoft.com/download/confirmation.aspx?id=41653). Ciò è necessario in modo che i dati possono essere scritti toohello account di archiviazione della cache di hello macchina virtuale.

* Creare regole per tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Creare regole che corrispondono toohello percorso di destinazione:

   **Posizione** | **IP del servizio Site Recovery** |  **IP di monitoraggio di Site Recovery**
    --- | --- | ---
   Stati Uniti centrali | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Regole di gruppo nel gruppo di sicurezza di rete centrale USA hello

Queste regole sono necessarie in modo che sia possibile abilitare la replica dal hello destinazione area toohello origine area dopo il failover:

* Le regole corrispondenti troppo[intervalli IP Usa centrale](https://www.microsoft.com/download/confirmation.aspx?id=41653). Sono necessarie in modo che i dati possono essere scritti toohello account di archiviazione della cache di hello macchina virtuale.

* Regole per tutti gli intervalli IP che corrispondono a 365 tooOffice [autenticazione e identità endpoint IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Le regole corrispondenti toohello percorso di origine:

   **Posizione** | **IP del servizio Site Recovery** |  **IP di monitoraggio di Site Recovery**
    --- | --- | ---
   Stati Uniti orientali | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Linee guida per la configurazione di ExpressRoute/VPN esistente da Azure in locale

Se si dispone di una connessione VPN o ExpressRoute tra sedi locali e hello in Azure percorso di origine, attenersi alle linee guida hello in questa sezione.

### <a name="forced-tunneling-configuration"></a>Configurazione del tunneling forzato

Una configurazione personalizzata comune è toodefine una route predefinita (0.0.0.0/0) che forza tooflow di traffico Internet in uscita tramite una sede locale hello. Ciò non è consigliabile. il traffico di replica Hello e la comunicazione dei servizi di ripristino del sito non lasciare hello Azure limite. Hello soluzione è tooadd route definite dall'utente (UDRs) per [questi intervalli IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) in modo che il traffico di replica hello non andare in locale.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Connettività tra il percorso di destinazione e locale hello

Seguire queste linee guida per le connessioni tra il percorso di destinazione hello e hello locale:
- Se l'applicazione deve tooconnect toohello alle macchine locali o se sono presenti client che si connettono toohello applicazione locale tramite VPN/ExpressRoute, assicurarsi di disporre di almeno un [connessione site-to-site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) tra i Data Center Azure hello e area locale di destinazione.

- Se si prevede di tooflow il traffico tra l'area di Azure di destinazione e il data center locale hello, è necessario creare un altro [connessione ExpressRoute](../expressroute/expressroute-introduction.md) tra Data Center di destinazione Azure hello e area locale hello.

- Se si vuole tooretain gli indirizzi IP per le macchine virtuali hello dopo che il failover, è possibile mantenere connessione sito a sito o ExpressRoute dell'area di destinazione hello in uno stato disconnesso. Si tratta di toomake che non vi sia alcun conflitto di intervallo tra gli intervalli IP dell'area di origine hello e intervalli IP dell'area di destinazione.

### <a name="best-practices-for-expressroute-configuration"></a>Procedure consigliate per la configurazione di ExpressRoute
Seguire queste procedure consigliate per la configurazione di ExpressRoute:

- È necessario un circuito ExpressRoute in entrambe le aree di origine e destinazione hello toocreate. È necessario toocreate una connessione tra:
  - rete virtuale di origine Hello e circuito ExpressRoute hello.
  - rete virtuale di destinazione Hello e circuito ExpressRoute hello.

- Come parte dello standard di ExpressRoute, è possibile creare circuiti in hello stessa regione di natura geopolitica. circuiti ExpressRoute di toocreate in diverse aree di natura geopolitiche, Azure ExpressRoute Premium è obbligatorio, che comporta un costo incrementale. (se si sta già usando ExpressRoute Premium, non sono previsti costi aggiuntivi). Per ulteriori informazioni, vedere hello [documento percorsi ExpressRoute](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e [ExpressRoute prezzi](https://azure.microsoft.com/pricing/details/expressroute/).

- È consigliabile usare diversi intervalli IP nelle aree di origine e di destinazione. Hello circuito ExpressRoute sarà in grado di intervalli di IP stesso tooconnect con reti virtuali di Azure due di hello in hello contemporaneamente.

- È possibile creare reti virtuali con hello stesso IP intervalli in entrambe le aree e quindi creare circuiti ExpressRoute in entrambe le aree. Nel caso di hello di un evento di failover, disconnettersi circuito hello dalla rete virtuale di origine hello e connettersi circuito hello nella rete virtuale di destinazione hello.

 >[!IMPORTANT]
 > Se l'area primaria hello è completamente verso il basso, hello disconnettere l'operazione può avere esito negativo. Rete virtuale di destinazione hello che, potrà ottenere la connettività di ExpressRoute.

## <a name="next-steps"></a>Passaggi successivi
Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).
