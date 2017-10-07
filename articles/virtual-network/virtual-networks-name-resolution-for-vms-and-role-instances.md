---
title: aaaResolution per le macchine virtuali e istanze del ruolo
description: 'Scenari di risoluzione dei nomi per Azure IaaS, soluzioni ibride, tra diversi servizi cloud, Active Directory e utilizzando il proprio server DNS  '
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo
A seconda di come si utilizza Azure toohost IaaS, PaaS e soluzioni ibride, potrebbe essere necessario tooallow hello macchine virtuali e istanze del ruolo create toocommunicate tra loro. Sebbene questa comunicazione può essere eseguita utilizzando gli indirizzi IP, è molto più semplice toouse i nomi facili da ricordare e non cambiano. 

Quando le istanze del ruolo e le macchine virtuali ospitate in Azure devono gli indirizzi IP di tooresolve dominio nomi toointernal, possono utilizzare uno dei due metodi:

* [Risoluzione dei nomi fornita da Azure](#azure-provided-name-resolution)
* [Risoluzione dei nomi utilizzando il proprio server DNS](#name-resolution-using-your-own-dns-server) (che può inoltrare query toohello i server DNS fornito da Azure) 

tipo di Hello di risoluzione dei nomi che è utilizzare dipende in che modo le macchine virtuali e istanze del ruolo necessario toocommunicate tra loro.

**Hello nella tabella seguente sono illustrati gli scenari e soluzioni di risoluzione nome corrispondente:**

| **Scenario** | **Soluzione** | **Suffisso** |
| --- | --- | --- |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali presenti in hello stesso servizio cloud o rete virtuale |[Risoluzione dei nomi fornita da Azure](#azure-provided-name-resolution) |nome host o nome di dominio completo |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali situate in diverse reti virtuali |Server DNS gestiti dal cliente che inoltrano query tra reti virtuali per la risoluzione da parte di Azure (proxy DNS).  Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| Risoluzione dei nomi servizi e computer locali da istanze del ruolo o macchine virtuali in Azure |Server DNS gestiti dal cliente, ad esempio controller di dominio locale, controller di dominio di sola lettura locale o server DNS secondario sincronizzati tramite trasferimenti di zona.  Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| Risoluzione di nomi host di Azure da computer locali |Inoltro delle query tooa gestita dal cliente proxy server DNS nella rete virtuale corrispondente hello, server proxy hello inoltra tooAzure query per la risoluzione. Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| DNS inversi per indirizzi IP interni |[Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |n/d |
| Risoluzione dei nomi tra macchine virtuali o istanze del ruolo situate in servizi cloud diversi e non in una rete virtuale |Non applicabile Connettività tra macchine virtuali e istanze del ruolo in servizi cloud diversi non è supportata esternamente a una rete virtuale. |n/d |

## <a name="azure-provided-name-resolution"></a>Risoluzione dei nomi fornita da Azure
Oltre alla risoluzione dei nomi DNS pubblici, Azure fornisce la risoluzione dei nomi interna per le macchine virtuali e istanze del ruolo che si trovano nello stesso servizio cloud o di rete virtuale di hello.  Macchine virtuali o le istanze in un servizio cloud condividono hello DNS stesso suffisso (quindi solo il nome host hello è sufficiente), ma in servizi cloud diversi di reti virtuali classiche può avere diversi suffissi DNS hello FQDN è tooresolve necessari nomi tra servizi cloud diversi.  Nelle reti virtuali nel modello di distribuzione di gestione risorse di hello, hello suffisso DNS non è coerenza attraverso la rete virtuale hello (pertanto hello FQDN non è necessario) e i nomi DNS possono essere assegnati tooboth NIC e le macchine virtuali. Anche se la risoluzione dei nomi fornita da Azure non richiede alcuna configurazione, non è adatta hello per tutti gli scenari di distribuzione, come illustrato nella tabella hello precedente.

> [!NOTE]
> Nel caso di hello di ruoli web e di lavoro, è possibile accedere anche hello gli indirizzi IP interni delle istanze del ruolo in base a hello ruolo nome e numero di istanza utilizzando l'API REST di gestione Azure hello. Per altre informazioni, vedere [Riferimento all'API REST di gestione dei servizi](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Funzionalità e considerazioni
**Funzionalità**

* Facilità di utilizzo: in ordine toouse la risoluzione dei nomi fornita da Azure è necessaria alcuna configurazione.
* Hello Azure nome servizio di risoluzione è a disponibilità elevata, salvataggio hello è necessario toocreate e gestire i cluster di server DNS.
* Può essere utilizzato in combinazione con la propria tooresolve server DNS sia in locale e i nomi host di Azure.
* Risoluzione dei nomi viene fornita tra le istanze ruolo macchine virtuali all'interno di hello servizio senza necessità di un FQDN stesso cloud.
* Risoluzione dei nomi viene fornita tra le macchine virtuali in reti virtuali che utilizzano modelli di distribuzione di gestione delle risorse di hello, senza necessità di hello FQDN. La risoluzione dei nomi in diversi servizi cloud, reti virtuali nel modello di distribuzione classica hello richiedono hello FQDN. 
* È possibile usare nomi host personalizzati in grado di descrivere in modo più adeguato le distribuzioni, anziché usare nomi generati automaticamente.

**Considerazioni:**

* suffisso DNS creato da Azure Hello non può essere modificato.
* Non è possibile registrare manualmente i propri record.
* WINS e NetBIOS non sono supportati. Non è possibile visualizzare le macchine virtuali in Esplora risorse.
* I nomi host devono essere compatibili con DNS (devono utilizzare solo 0-9, a-z e '-' e non possono iniziare o terminare con un '-'. Vedere RFC 3696 sezione 2).
* Il traffico di query DNS è limitato per ogni VM. Questo in genere non comporta alcun impatto sulla maggior parte delle applicazioni.  Se viene osservata la limitazione delle richieste, assicurarsi che la memorizzazione nella cache sul lato client sia abilitata.  Per ulteriori informazioni, vedere [ottenere la maggior parte dalla risoluzione dei nomi fornita da Azure hello](#Getting-the-most-from-Azure-provided-name-resolution).
* Solo le macchine virtuali in hello primi 180 servizi cloud sono registrate per ogni rete virtuale in un modello di distribuzione classica. Non è applicabile reti toovirtual nei modelli di distribuzione di gestione risorse.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Ottenere la maggior parte dalla risoluzione dei nomi fornita da Azure hello
**Memorizzazione nella cache sul lato client:**

Non tutte le query DNS deve toobe inviati attraverso la rete hello.  Memorizzazione nella cache sul lato client consente di ridurre la latenza e migliorare blips toonetwork resilienza risolvendo ricorrente query DNS da una cache locale.  I record DNS contengono un Time-To-Live (TTL) che consente di record toostore hello della cache di hello per maggior tempo possibile senza influire sull'aggiornamento record, pertanto la cache lato client è adatta per la maggior parte dei casi.

predefinito Hello Client DNS di Windows è disponibile una cache DNS predefinita.  Alcuni Linux le distribuzioni non includono la memorizzazione nella cache per impostazione predefinita, è consigliabile che uno aggiunto tooeach VM Linux (dopo aver verificato che non vi è una cache locale già).

Esistono una serie di diversi DNS memorizzazione nella cache pacchetti disponibili, ad esempio dnsmasq, ecco hello passaggi tooinstall dnsmasq in distribuzioni di hello più comuni:

* **Ubuntu (usa resolvconf)**:
  * è sufficiente installare il pacchetto di dnsmasq hello ("sudo installazione apt get dnsmasq").
* **SUSE (usa netconf)**:
  * installare il pacchetto dnsmasq hello ("sudo zypper installazione dnsmasq") 
  * abilitare il servizio dnsmasq hello ("systemctl enable dnsmasq.service") 
  * avviare il servizio di dnsmasq hello ("systemctl inizio dnsmasq.service") 
  * modificare "/ e così via/sysconfig/rete/config" e modificare NETCONFIG_DNS_FORWARDER = "" troppo "dnsmasq"
  * aggiornare resolv.conf ("aggiornamento netconfig") tooset hello cache di hello resolver DNS locali
* **OpenLogic (usa NetworkManager)**:
  * installare il pacchetto dnsmasq hello ("sudo yum installazione dnsmasq")
  * abilitare il servizio dnsmasq hello ("systemctl enable dnsmasq.service")
  * avviare il servizio di dnsmasq hello ("systemctl inizio dnsmasq.service")
  * aggiungere "127.0.0.1; server di nome dominio anteporre" too"/etc/dhclient-eth0.conf"
  * Riavviare cache di hello tooset hello rete del servizio ("rete riavviare il servizio") come resolver DNS locali hello

> [!NOTE]
> pacchetto 'dnsmasq' Hello è uno solo di hello molti cache DNS è disponibile per Linux.  Prima di usarla, verificare che sia adatta in base alle esigenze specifiche e assicurarsi che non siano installate altre cache.
> 
> 

**Ripetizione di tentativi sul lato client:**

DNS è principalmente un protocollo UDP.  Come hello protocollo UDP non garantisce il recapito dei messaggi, la logica di ripetizione è gestita nel protocollo DNS hello stesso.  Ogni client DNS (sistema operativo) può presentare una logica di tentativi diverso a seconda delle preferenze creatori di hello:

* I sistemi operativi Windows eseguono un nuovo tentativo dopo 1 secondo e ne eseguono un altro dopo 2, 4 e altri 4 secondi. 
* Hello tentativi di installazione predefinito Linux dopo 5 secondi.  È consigliabile toochange questo tooretry 5 volte intervalli di 1 secondo.  

toocheck hello impostazioni correnti in una VM Linux, '/etc/resolv.conf cat' e cercare alla riga 'opzioni' hello, ad esempio:

    options timeout:1 attempts:5

file resolv.conf Hello è in genere generata automaticamente e non deve essere modificato.  Hello passaggi specifici per l'aggiunta di riga options' hello' variano a seconda distribuzione:

* **Ubuntu** (usa resolvconf):
  * aggiungere hello opzioni riga too'/etc/resolveconf/resolv.conf.d/head' 
  * eseguire tooupdate 'resolvconf -u'
* **SUSE** (usa netconf):
  * aggiungere 'tentativi: 5 timeout:1' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parametro in '/ ecc/sysconfig/rete/configurazione' 
  * eseguire tooupdate 'aggiornamento netconfig'
* **OpenLogic** (usa NetworkManager):
  * aggiungere too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo "Opzioni timeout:1. tentativi: 5" ' ' 
  * eseguire tooupdate 'servizio di rete il riavvio'

## <a name="name-resolution-using-your-own-dns-server"></a>Risoluzione dei nomi usando il server DNS
Esistono una serie di situazioni in cui i requisiti di risoluzione dei nomi possono andare oltre hello funzionalità fornita da Azure, ad esempio quando tramite domini di Active Directory o quando si richiede la risoluzione DNS tra reti virtuali (vnet).  toocover questi scenari, Azure offre la possibilità di hello è toouse dei propri server DNS.  

I server DNS in una rete virtuale possono inoltrare i resolver ricorsivo del DNS query tooAzure tooresolve nomi host all'interno della rete virtuale.  Ad esempio, un Controller di dominio (DC) in esecuzione in Azure può rispondere tooDNS query per i domini e inoltrare tutti gli altri tooAzure di query.  In questo modo le macchine virtuali toosee nomi host fornito da Azure (tramite l'utilità di inoltro hello) sia le risorse locali (tramite hello controller di dominio).  Sistemi di risoluzione ricorsiva dell'accesso tooAzure viene fornito tramite l'indirizzo IP virtuale hello 168.63.129.16.

Inoltro di DNS, inoltre, consente la risoluzione DNS tra reti della rete virtuale e consente il tooresolve macchine locali i nomi host fornito da Azure.  In ordine tooresolve nome host della macchina virtuale, macchina virtuale del server DNS hello deve risiedere in hello stesso virtuale di rete e di essere configurato tooforward hostname query tooAzure.  Come suffisso DNS hello è diverso in ogni rete virtuale, è possibile usare l'inoltro condizionale regole toosend DNS esegue una query toohello correggere rete virtuale per la risoluzione.  Hello seguente immagine mostra due reti virtuali e una rete locale in fase di risoluzione DNS multisito tra l'utilizzo di questo metodo.  Un server d'inoltro DNS di esempio è disponibile in hello [raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) e [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS tra reti virtuali](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Quando si utilizza la risoluzione dei nomi fornita da Azure, un suffisso DNS interno (*. internal.cloudapp.net) è fornito tooeach VM tramite DHCP.  Risoluzione dei nomi host in questo modo il nome host hello sono record nella zona internal.cloudapp.net hello.  Quando si utilizza la propria soluzione di risoluzione del nome, hello nomi IDN suffisso non è specificato tooVMs perché interferisce con altre architetture DNS (ad esempio gli scenari di dominio).  Viene invece fornito un segnaposto non funzionante (reddog.microsoft.com).  

Se necessario, suffisso DNS interno hello può essere determinato tramite API di PowerShell o hello:

* Per le reti virtuali in modelli di distribuzione di gestione delle risorse, è disponibile tramite hello suffisso hello [scheda di interfaccia di rete](https://msdn.microsoft.com/library/azure/mt163668.aspx) risorse o tramite hello [Get AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* Nei modelli di distribuzione classica, è disponibile tramite hello suffisso hello [ottenere API della distribuzione](https://msdn.microsoft.com/library/azure/ee460804.aspx) chiamare o tramite hello [Get-AzureVM-Debug](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

Se l'inoltro delle query tooAzure non in base alle esigenze, è necessario tooprovide la soluzione DNS personalizzata.  Questa soluzione DNS dovrà:

* Fornire una soluzione di risoluzione dei nomi host appropriata, ad esempio tramite [DNS dinamico](virtual-networks-name-resolution-ddns.md).  Si noti che se utilizzando DDNS potrebbe essere necessario toodisable DNS lo scavenging dei record di lease DHCP di Azure sono molto lunghi e lo scavenging può rimuovere DNS registra in modo anomalo. 
* Fornire la risoluzione di tooallow ricorsiva appropriato risoluzione dei nomi di dominio esterno.
* Essere accessibile (TCP e UDP sulla porta 53) dai client hello insieme serve a essere in grado di tooaccess hello internet.
* Essere protetta da accessi da hello internet, toomitigate imbattono dagli agenti esterni.

> [!NOTE]
> Per prestazioni ottimali, quando si usano macchine virtuali di Azure come server DNS, IPv6 deve essere disabilitato e un [indirizzo IP pubblico a livello di istanza](virtual-networks-instance-level-public-ip.md) devono essere assegnate tooeach macchina virtuale del server DNS.  Se si sceglie toouse Windows Server come server DNS [questo articolo](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) fornisce l'analisi delle prestazioni aggiuntivi e le ottimizzazioni.
> 
> 

### <a name="specifying-dns-servers"></a>Specificare i server DNS
Quando si utilizzano i propri server DNS, Azure fornisce hello possibilità toospecify più server DNS per ogni rete virtuale o per ogni rete interfaccia Gestione risorse () / (classico) servizio cloud.  Server DNS specificati per un'interfaccia di rete del servizio cloud di ottenere la precedenza rispetto a quelli specificati per la rete virtuale hello.

> [!NOTE]
> Le proprietà di connessione di rete, ad esempio i server DNS indirizzi IP, non devono essere modificati direttamente all'interno di macchine virtuali di Windows come si possono ottenere cancellati durante il servizio di correzione quando l'adattatore di rete virtuale hello viene sostituito. 
> 
> 

Quando si utilizza il modello di distribuzione del hello Resource Manager, è possono specificare server DNS in hello portale, API e modelli ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) o PowerShell ([rete virtuale](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Quando si utilizza il modello di distribuzione classica hello, server DNS per la rete virtuale hello può essere specificata in hello portale o [hello *configurazione di rete* file](https://msdn.microsoft.com/library/azure/jj157100).  Per i servizi cloud, i server DNS hello vengono specificati tramite [hello *configurazione del servizio* file](https://msdn.microsoft.com/library/azure/ee758710) o di PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Se si modificano le impostazioni DNS hello per una macchina virtuale rete virtuali o che è già stata distribuita, è necessario toorestart ogni VM interessato per effetto di tootake modifiche hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Modello di distribuzione di Resource Manager:

* [Creare o aggiornare una rete virtuale](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Creare o aggiornare una scheda dell'interfaccia di rete](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Modello di distribuzione classica:

* [Schema di configurazione dei servizi di Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Schema di configurazione di Rete virtuale](https://msdn.microsoft.com/library/azure/jj157100)
* [Configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md) 

