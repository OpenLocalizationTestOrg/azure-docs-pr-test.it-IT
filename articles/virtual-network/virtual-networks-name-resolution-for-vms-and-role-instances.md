---
title: Risoluzione per le macchine virtuali e le istanze del ruolo
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
ms.openlocfilehash: 479cf8cf358d0b242d8ce030d8639b493e4767d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo
A seconda di come si usa Azure per ospitare soluzioni IaaS, PaaS e ibride, potrebbe essere necessario consentire la comunicazione tra VM e istanze del ruolo create. Nonostante questa comunicazione possa avvenire usando indirizzi IP, è molto più semplice usare nomi che possono essere facilmente ricordati e che non cambiano. 

Quando le istanze del ruolo e le VM ospitate in Azure devono risolvere nomi di dominio trasformandoli in indirizzi IP interni, possono usare uno di questi due metodi:

* [Risoluzione dei nomi fornita da Azure](#azure-provided-name-resolution)
* [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) (che potrebbe inoltrare le query ai server DNS forniti da Azure) 

Il tipo di risoluzione dei nomi usato dipende dal modo in cui VM e istanze del ruolo devono comunicare.

**Nella tabella seguente vengono illustrate diverse ipotesi e le corrispondenti soluzioni di risoluzione dei nomi:**

| **Scenario** | **Soluzione** | **Suffisso** |
| --- | --- | --- |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali situate nello stesso servizio cloud o nella stessa rete virtuale |[Risoluzione dei nomi fornita da Azure](#azure-provided-name-resolution) |nome host o nome di dominio completo |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali situate in diverse reti virtuali |Server DNS gestiti dal cliente che inoltrano query tra reti virtuali per la risoluzione da parte di Azure (proxy DNS).  Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| Risoluzione dei nomi servizi e computer locali da istanze del ruolo o macchine virtuali in Azure |Server DNS gestiti dal cliente, ad esempio controller di dominio locale, controller di dominio di sola lettura locale o server DNS secondario sincronizzati tramite trasferimenti di zona.  Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| Risoluzione di nomi host di Azure da computer locali |Inoltra le query a un server proxy DNS gestito dal cliente nella rete virtuale corrispondente. Il server proxy inoltra le query ad Azure per la risoluzione. Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |Solo nome di dominio completo |
| DNS inversi per indirizzi IP interni |[Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |n/d |
| Risoluzione dei nomi tra macchine virtuali o istanze del ruolo situate in servizi cloud diversi e non in una rete virtuale |Non applicabile Connettività tra macchine virtuali e istanze del ruolo in servizi cloud diversi non è supportata esternamente a una rete virtuale. |n/d |

## <a name="azure-provided-name-resolution"></a>Risoluzione dei nomi fornita da Azure
Oltre alla risoluzione dei nomi DNS pubblici, Azure offre la risoluzione dei nomi interni per VM e istanze del ruolo che si trovano all'interno della stessa rete virtuale o dello stesso servizio cloud.  Le VM e le istanze in un servizio cloud condividono lo stesso suffisso DNS, quindi il nome host da solo è sufficiente, tuttavia, nelle reti virtuali classiche, servizi cloud diversi hanno suffissi DNS diversi, quindi è necessario il nome di dominio completo per la risoluzione dei nomi tra diversi servizi cloud.  Nelle reti virtuali nel modello di distribuzione di Resource Manager il suffisso DNS è coerente nella rete virtuale, quindi il nome di dominio completo non è necessario e i nomi DNS possono essere assegnati sia alle schede di interfaccia di rete che alle macchine virtuali. Sebbene la risoluzione dei nomi fornita da Azure non richieda alcuna configurazione, non è la scelta più appropriata per tutti gli scenari di distribuzione, come illustrato nella tabella precedente.

> [!NOTE]
> Nel caso dei ruoli web e di lavoro, è possibile accedere anche gli indirizzi IP interni delle istanze del ruolo in base al numero di nome e al numero di istanza del ruolo utilizzando l'API REST di gestione dei servizi Azure. Per altre informazioni, vedere [Riferimento all'API REST di gestione dei servizi](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Funzionalità e considerazioni
**Funzionalità**

* Facilità di utilizzo: non è necessaria alcuna configurazione per usare la risoluzione dei nomi fornita da Azure.
* Il servizio di risoluzione dei nomi fornito da Azure garantisce la disponibilità elevata ed evita così di dover creare e gestire i cluster dei propri server DNS.
* Può essere usato in combinazione con i propri server DNS per risolvere i nomi host locali e i nomi host di Azure.
* La risoluzione dei nomi viene offerta tra istanze del ruolo e VM presenti nello stesso servizio cloud senza necessità di un nome di dominio completo.
* Viene fornita la risoluzione dei nomi tra VM in reti virtuali che usano il modello di distribuzione di Resource Manager, senza necessità del nome di dominio completo. Le reti virtuali nel modello di distribuzione classica richiedono il nome di dominio completo per la risoluzione dei nomi in diversi servizi cloud. 
* È possibile usare nomi host personalizzati in grado di descrivere in modo più adeguato le distribuzioni, anziché usare nomi generati automaticamente.

**Considerazioni:**

* Il suffisso DNS creato da Azure non può essere modificato.
* Non è possibile registrare manualmente i propri record.
* WINS e NetBIOS non sono supportati. Non è possibile visualizzare le macchine virtuali in Esplora risorse.
* I nomi host devono essere compatibili con DNS (devono utilizzare solo 0-9, a-z e '-' e non possono iniziare o terminare con un '-'. Vedere RFC 3696 sezione 2).
* Il traffico di query DNS è limitato per ogni VM. Questo in genere non comporta alcun impatto sulla maggior parte delle applicazioni.  Se viene osservata la limitazione delle richieste, assicurarsi che la memorizzazione nella cache sul lato client sia abilitata.  Per altre informazioni, vedere l'articolo che illustra [come usare al meglio la risoluzione dei nomi fornita da Azure](#Getting-the-most-from-Azure-provided-name-resolution).
* Solo le VM nei primi 180 servizi cloud sono registrate per ogni rete virtuale in un modello di distribuzione classica. Ciò non si applica alle reti virtuali nei modelli di distribuzione di Resource Manager.

### <a name="getting-the-most-from-azure-provided-name-resolution"></a>come usare al meglio la risoluzione dei nomi fornita da Azure
**Memorizzazione nella cache sul lato client:**

Non tutte le query DNS devono essere inviate attraverso la rete.  La memorizzazione nella cache sul lato client consente di ridurre la latenza e migliorare la resilienza ai blip (brevi interruzioni) di rete, tramite la risoluzione di query DNS ricorrenti da una cache locale.  I record DNS contengono una durata (TTL) che consente alla cache di memorizzare il record per il periodo di tempo più lungo possibile senza che questo influisca sullo stato di aggiornamento del record. Per questo motivo, la memorizzazione nella cache sul lato client è ideale per la maggior parte delle situazioni.

Il client DNS di Windows predefinito contiene una cache DNS incorporata.  Alcune distribuzioni di Linux non includono la memorizzazione nella cache per impostazione predefinita, è quindi consigliabile aggiungerne una a ogni VM Linux (dopo aver verificato che non sia già presente una cache locale).

Sono disponibili molti pacchetti di memorizzazione nella cache DNS diversi, ad esempio dnsmasq. Di seguito è riportata la procedura per installare dnsmasq nei distro più comuni:

* **Ubuntu (usa resolvconf)**:
  * installare il pacchetto dnsmasq ("sudo apt-get install dnsmasq").
* **SUSE (usa netconf)**:
  * installare il pacchetto dnsmasq ("sudo zypper install dnsmasq") 
  * abilitare il servizio dnsmasq ("systemctl enable dnsmasq.service") 
  * avviare il servizio dnsmasq ("systemctl start dnsmasq.service") 
  * modificare "/etc/sysconfig/network/config" e sostituire NETCONFIG_DNS_FORWARDER="" con "dnsmasq"
  * aggiornare resolv.conf ("netconfig update") per impostare la cache come resolver DNS locale
* **OpenLogic (usa NetworkManager)**:
  * installare il pacchetto dnsmasq ("sudo yum install dnsmasq")
  * abilitare il servizio dnsmasq ("systemctl enable dnsmasq.service")
  * avviare il servizio dnsmasq ("systemctl start dnsmasq.service")
  * aggiungere "prepend domain-name-servers 127.0.0.1;" in "/etc/dhclient-eth0.conf"
  * riavviare il servizio di rete ("service network restart") per impostare la cache come resolver DNS locale

> [!NOTE]
> Il pacchetto 'dnsmasq' è solo una delle cache DNS disponibili per Linux.  Prima di usarla, verificare che sia adatta in base alle esigenze specifiche e assicurarsi che non siano installate altre cache.
> 
> 

**Ripetizione di tentativi sul lato client:**

DNS è principalmente un protocollo UDP.  Poiché il protocollo UDP non garantisce il recapito dei messaggi, la logica di ripetizione dei tentativi viene gestita nel protocollo DNS stesso.  Ogni client DNS (sistema operativo) può includere una logica di ripetizione dei tentativi diversa, in base alle preferenze degli autori.

* I sistemi operativi Windows eseguono un nuovo tentativo dopo 1 secondo e ne eseguono un altro dopo 2, 4 e altri 4 secondi. 
* La configurazione di Linux predefinita esegue il tentativo dopo 5 secondi.  È consigliabile modificare questa impostazione in modo da eseguire 5 tentativi a intervalli di 1 secondo.  

Per verificare le impostazioni correnti in una macchina virtuale Linux, aprire il file 'cat /etc/resolv.conf' e osservare la riga 'options', ad esempio:

    options timeout:1 attempts:5

Il file resolv.conf è solitamente generato automaticamente e non deve essere modificato.  La procedura specifica per aggiungere la riga 'options' varia a seconda del distro:

* **Ubuntu** (usa resolvconf):
  * aggiungere la riga per le opzioni in '/etc/resolveconf/resolv.conf.d/head' 
  * eseguire 'resolvconf -u' per aggiornare
* **SUSE** (usa netconf):
  * aggiungere 'timeout:1 attempts:5' al parametro NETCONFIG_DNS_RESOLVER_OPTIONS="" in '/etc/sysconfig/network/config' 
  * eseguire 'netconfig update' per aggiornare
* **OpenLogic** (usa NetworkManager):
  * aggiungere 'echo "options timeout:1 attempts:5"' in '/etc/NetworkManager/dispatcher.d/11-dhclient' 
  * eseguire 'service network restart' per aggiornare

## <a name="name-resolution-using-your-own-dns-server"></a>Risoluzione dei nomi usando il server DNS
In alcune situazioni le esigenze in termini di risoluzione dei nomi potrebbero andare oltre le funzionalità fornite da Azure, ad esempio quando si usano i domini di Active Directory o quando è necessaria la risoluzione DNS tra reti virtuali.  Per questi scenari specifici, Azure offre la possibilità di usare i propri server DNS.  

I server DNS all'interno di una rete virtuale possono inoltrare query DNS ai resolver ricorsivi di Azure per risolvere i nomi host all'interno di quella rete virtuale.  Ad esempio, un controller di dominio in esecuzione in Azure può rispondere a query DNS per i relativi domini e inoltrare tutte le altre query ad Azure.  Questo consente alle macchine virtuali di visualizzare sia le risorse locali, tramite il controller di dominio, sia i nomi host forniti da Azure, tramite il server di inoltro.  L'accesso ai resolver ricorsivi di Azure viene fornito tramite l'indirizzo IP virtuale 168.63.129.16.

L'inoltro DNS consente anche la risoluzione DNS tra reti virtuali e permette alle macchine virtuali locali di risolvere i nomi host forniti da Azure.  Per risolvere il nome host di una macchina virtuale, la macchina virtuale del server DNS deve risiedere nella stessa rete virtuale ed essere configurata per inoltrare le query relative ai nomi host ad Azure.  Poiché il suffisso DNS è diverso in ogni rete virtuale, è possibile usare le regole di inoltro condizionale per inviare le query DNS alla rete virtuale corretta per la risoluzione.  L'immagine seguente mostra due reti virtuali e una rete locale che gestiscono la risoluzione DNS tra reti virtuali con questo metodo.  Un esempio di server di inoltro DNS è disponibile nella [raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) e su [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS tra reti virtuali](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Quando si usa la risoluzione dei nomi di Azure, un suffisso DNS interno (*.internal.cloudapp.net) viene fornito a ogni macchina virtuale tramite DHCP.  Ciò consente la risoluzione dei nomi host, perché i record relativi ai nomi host si trovano nell'area internal.cloudapp.net.  Quando si usa la soluzione di risoluzione dei nomi personalizzata, il suffisso IDNS non viene fornito alle macchine virtuali perché interferisce con altre architetture DNS, ad esempio gli scenari con aggiunta al dominio.  Viene invece fornito un segnaposto non funzionante (reddog.microsoft.com).  

Se necessario, è possibile determinare il suffisso DNS interno usando PowerShell o l'API:

* Per le reti virtuali nei modelli di distribuzione Azure Resource Manager, il suffisso è disponibile tramite la risorsa [scheda di interfaccia di rete](https://msdn.microsoft.com/library/azure/mt163668.aspx) o il cmdlet [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx).    
* Nei modelli di distribuzione classica il suffisso è disponibile tramite una chiamata all'[API GetDeployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) o il cmdlet [Get-AzureVM -Debug](https://msdn.microsoft.com/library/azure/dn495236.aspx).

Se l'inoltro delle query ad Azure non soddisfa le esigenze correnti, sarà necessario fornire una soluzione DNS personalizzata.  Questa soluzione DNS dovrà:

* Fornire una soluzione di risoluzione dei nomi host appropriata, ad esempio tramite [DNS dinamico](virtual-networks-name-resolution-ddns.md).  Si noti che se si usa il DNS dinamico potrebbe essere necessario disabilitare lo scavenging del record DNS, perché i lease DHCP di Azure sono molto lunghi e potrebbero rimuovere i record DNS anticipatamente. 
* Fornire una soluzione di risoluzione ricorsiva appropriata per consentire la risoluzione dei nomi di dominio esterni.
* Essere accessibile (tramite TCP e UDP sulla porta 53) dai client che gestisce e in grado di accedere a Internet.
* Essere protetta dagli accessi provenienti da Internet per attenuare i rischi rappresentati da agenti esterni.

> [!NOTE]
> Per prestazioni ottimali, quando si usano macchine virtuali di Azure come server DNS, è necessario disabilitare IPv6 e assegnare un indirizzo [IP pubblico a livello di istanza](virtual-networks-instance-level-public-ip.md) a ogni macchina virtuale del server DNS.  Se si sceglie di usare Windows Server come server DNS, [questo articolo](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) offre un'analisi delle prestazioni e ottimizzazioni aggiuntive.
> 
> 

### <a name="specifying-dns-servers"></a>Specificare i server DNS
Quando si usano i propri server DNS, Azure offre la possibilità di specificare più server DNS per ogni rete virtuale o per ogni interfaccia di rete (Resource Manager)/servizio cloud (classico).  I server DNS specificati per un'interfaccia di rete o un servizio cloud ottengono la precedenza su quelli specificati per la rete virtuale.

> [!NOTE]
> Le proprietà di connessione di rete, ad esempio gli indirizzi IP del server DNS, non devono essere modificate direttamente all'interno delle VM di Windows in quanto possono essere cancellate durante il servizio di correzione quando la scheda di rete virtuale viene sostituita. 
> 
> 

Quando si usa il modello di distribuzione Azure Resource Manager, i server DNS possono essere specificati nel portale, nelle API, nei modelli ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) o in PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Quando si usa il modello di distribuzione classica, i server DNS possono essere specificati per la rete virtuale nel portale o [ nel file di *configurazione di rete*](https://msdn.microsoft.com/library/azure/jj157100).  Per i servizi cloud, i server DNS vengono specificati tramite [il file di *configurazione del servizio*](https://msdn.microsoft.com/library/azure/ee758710) o in PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Se si modificano le impostazioni DNS per una rete virtuale o una macchina virtuale che è già stata distribuita, è necessario riavviare ogni VM interessata affinché le modifiche vengano applicate.
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

