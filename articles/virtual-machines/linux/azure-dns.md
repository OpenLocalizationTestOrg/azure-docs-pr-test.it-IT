---
title: aaaDNS opzioni di risoluzione nomi per le macchine virtuali Linux in Azure
description: "Scenari di risoluzione dei nomi per macchine virtuali Linux in IaaS di Azure, inclusi i servizi DNS forniti, DNS esterno ibrido e possibilità di usare il proprio server DNS."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opzioni di risoluzione dei nomi DNS per macchine virtuali Linux in Azure
Per impostazione predefinita, Azure fornisce la risoluzione dei nomi DNS per tutte le macchine virtuali contenute in una singola rete virtuale. È possibile implementare la soluzione di risoluzione dei nomi DNS configurando i servizi DNS nelle macchine virtuali ospitate da Azure. Hello negli scenari seguenti consentono di scegliere quello più adatto alla propria situazione hello.

* [Risoluzione dei nomi forniti da Azure](#azure-provided-name-resolution)
* [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server)

tipo di Hello di risoluzione dei nomi in uso dipende in che modo le macchine virtuali e istanze del ruolo necessario toocommunicate tra loro.

Hello nella tabella seguente sono illustrati gli scenari e soluzioni di risoluzione nome corrispondente:

| **Scenario** | **Soluzione** | **Suffisso** |
| --- | --- | --- |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali in hello stessa rete virtuale |[Risoluzione dei nomi forniti da Azure](#azure-provided-name-resolution) |nome host o nome di dominio completo (FQDN) |
| Risoluzione dei nomi tra istanze del ruolo o macchine virtuali presenti in reti virtuali diverse |Server DNS gestiti dal cliente che inoltrano query tra reti virtuali per la risoluzione da parte di Azure (proxy DNS). Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server). |Solo nome di dominio completo |
| Risoluzione dei nomi servizi e computer locali da istanze del ruolo o macchine virtuali in Azure |Server DNS gestiti dal cliente, ad esempio controller di dominio locale, controller di dominio di sola lettura locale o server DNS secondario sincronizzati tramite trasferimenti di zona. Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server). |Solo nome di dominio completo |
| Risoluzione di nomi host di Azure da computer locali |Inoltrare query tooa gestita dal cliente proxy server DNS nella rete virtuale corrispondente hello. server proxy Hello inoltra tooAzure query per la risoluzione. Vedere [Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server). |Solo nome di dominio completo |
| DNS inversi per indirizzi IP interni |[Risoluzione dei nomi usando il server DNS](#name-resolution-using-your-own-dns-server) |N/D |

## <a name="name-resolution-that-azure-provides"></a>Risoluzione dei nomi forniti da Azure
Oltre alla risoluzione dei nomi DNS pubblici, Azure fornisce la risoluzione dei nomi interna per le macchine virtuali e istanze del ruolo presenti nella stessa rete virtuale di hello. Nelle reti virtuali che sono basate su Azure Resource Manager, il suffisso DNS hello sia coerenza in rete virtuale hello. Hello FQDN non è necessaria. Schede di interfaccia di rete tooboth (NIC) e le macchine virtuali, è possono assegnare i nomi DNS. Anche se la risoluzione dei nomi hello forniti da Azure non richiede alcuna configurazione, non è adatta hello per tutti gli scenari di distribuzione, come illustrato nella tabella precedente hello.

### <a name="features-and-considerations"></a>Funzionalità e considerazioni
**Funzionalità**

* Risoluzione dei nomi necessari toouse forniti da Azure è alcuna configurazione.
* servizio di risoluzione dei nomi Hello forniti da Azure è a disponibilità elevata. Non necessari toocreate e gestire i cluster di server DNS.
* servizio di risoluzione nome Hello forniti da Azure può essere utilizzato insieme ai propri tooresolve server DNS sia in locale e i nomi host di Azure.
* Risoluzione dei nomi viene fornita tra le macchine virtuali in reti virtuali senza necessità di hello FQDN.
* È possibile usare nomi host personalizzati in grado di descrivere in modo più adeguato le distribuzioni, anziché usare nomi generati automaticamente.

**Considerazioni:**

* suffisso DNS Hello Azure crea non può essere modificato.
* Non è possibile registrare manualmente i propri record.
* WINS e NetBIOS non sono supportati.
* I nomi host devono essere compatibili con DNS.
    I nomi devono usare solo 0-9, a-z e "-" e non possono iniziare o terminare con un "-". Vedere RFC 3696 Sezione 2.
* Il traffico di query DNS è limitato per ogni macchina virtuale. La limitazione in genere non comporta alcun impatto sulla maggior parte delle applicazioni.  Se viene osservata la limitazione delle richieste, assicurarsi che la memorizzazione nella cache sul lato client sia abilitata.  Per ulteriori informazioni, vedere [ottenere la maggior parte dalla risoluzione dei nomi forniti da Azure hello](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Ottenere la maggior parte dalla risoluzione dei nomi forniti da Azure hello
**Memorizzazione nella cache sul lato client:**

Alcune query DNS non vengono inviati in rete hello. Memorizzazione nella cache sul lato client consente di ridurre la latenza e migliorare le incoerenze di resilienza toonetwork risolvendo ricorrente query DNS da una cache locale. I record DNS contengono un Time-To-Live (TTL), che consente di record toostore hello della cache di hello per maggior tempo possibile senza influire sull'aggiornamento di record. Di conseguenza, la memorizzazione nella cache sul lato client è ideale per la maggior parte delle situazioni.

Alcune distribuzioni Linux non includono la memorizzazione nella cache per impostazione predefinita. Si consiglia di aggiungere una macchina virtuale Linux di cache tooeach dopo aver verificato che non vi è una cache locale già.

Sono disponibili diversi pacchetti di memorizzazione nella cache DNS, ad esempio dnsmasq. Di seguito sono hello passaggi tooinstall dnsmasq nelle distribuzioni più comuni di hello:

**Ubuntu (usa resolvconf)**
  * Installare il pacchetto dnsmasq hello ("sudo installazione apt get dnsmasq").

**SUSE (usa netconf)**:
1. Installare il pacchetto dnsmasq hello ("sudo zypper installazione dnsmasq").
2. Abilitare il servizio dnsmasq hello ("systemctl enable dnsmasq.service").
3. Avviare il servizio di dnsmasq hello ("systemctl inizio dnsmasq.service").
4. Modificare "/ e così via/sysconfig/rete/configurazione" e modificare NETCONFIG_DNS_FORWARDER = "" troppo "dnsmasq".
5. Aggiornare resolv.conf ("aggiornamento netconfig") tooset hello cache di hello resolver DNS locale.

**CentOS di Rogue Wave Software (in precedenza OpenLogic) (usa NetworkManager)**
1. Installare il pacchetto dnsmasq hello ("sudo yum installazione dnsmasq").
2. Abilitare il servizio dnsmasq hello ("systemctl enable dnsmasq.service").
3. Avviare il servizio di dnsmasq hello ("systemctl inizio dnsmasq.service").
4. Aggiungere "127.0.0.1; server di nome dominio anteporre" too"/etc/dhclient-eth0.conf".
5. Riavviare cache di hello tooset hello rete del servizio ("rete riavviare il servizio") come resolver DNS locali hello

> [!NOTE]
> : il pacchetto di 'dnsmasq' hello è uno solo di hello molti DNS memorizza nella cache che sono disponibili per Linux. Prima di usarla, verificare che sia adatta in base alle esigenze specifiche e assicurarsi che non siano installate altre cache.
>
>

**Ripetizione di tentativi sul lato client**

DNS è principalmente un protocollo UDP. Poiché hello protocollo UDP non garantisce il recapito dei messaggi, hello protocollo DNS stesso gestisce la logica di ripetizione. Ogni client DNS (sistema operativo) può presentare una logica di tentativi diverso a seconda delle preferenze del creatore hello:

* i sistemi operativi Windows eseguono un nuovo tentativo dopo 1 secondo e ne eseguono un altro dopo 2, 4 e altri 4 secondi.
* Hello tentativi di installazione predefinito Linux dopo cinque secondi.  È necessario modificare questo tooretry cinque volte a intervalli di un secondo.  

toocheck hello impostazioni correnti in una macchina virtuale Linux, '/etc/resolv.conf cat,' e cercare nella riga "Opzioni" hello, ad esempio:

    options timeout:1 attempts:5

file resolv.conf Hello viene generato automaticamente e non deve essere modificato. Hello passaggi specifici che aggiungono hello 'opzioni' variano a seconda riga di distribuzione:

**Ubuntu** (usa resolvconf)
1. Aggiungere hello opzioni riga too'/etc/resolveconf/resolv.conf.d/head'.
2. Eseguire tooupdate 'resolvconf -u'.

**SUSE** (usa netconf)
1. Aggiungere 'tentativi: 5 timeout:1' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parametro in '/ ecc/sysconfig/rete/configurazione'.
2. Eseguire tooupdate 'aggiornamento netconfig'.

**CentOS di Rogue Wave Software (in precedenza OpenLogic)** (usa NetworkManager)
1. Aggiungere too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo "Opzioni timeout:1. tentativi: 5" ' '.
2. Eseguire tooupdate 'servizio di rete il riavvio'.

## <a name="name-resolution-using-your-own-dns-server"></a>Risoluzione dei nomi usando il server DNS
I requisiti di risoluzione dei nomi possono andare oltre le funzionalità di hello forniti da Azure. Ad esempio, potrebbe essere necessaria una risoluzione DNS tra reti virtuali. toocover questo scenario, è possibile usare i propri server DNS.  

Server DNS all'interno di una rete virtuale può essere che toorecursive resolver di nomi host di Azure tooresolve una query DNS di inoltro in hello stessa rete virtuale. Ad esempio, un server DNS in esecuzione in Azure può rispondere tooDNS query per il proprio DNS i file di zona e inoltrare tutti gli altri tooAzure di query. Questa funzionalità consente a macchine virtuali toosee entrambi le voci nel file di zona e i nomi host forniti da Azure (tramite l'utilità di inoltro hello). Resolver ricorsivo toohello di accesso di Azure viene fornito tramite l'indirizzo IP virtuale hello 168.63.129.16.

Inoltro di DNS, inoltre, consente la risoluzione DNS tra reti virtuali e consente i nomi di tooresolve macchine host locale forniti da Azure. tooresolve nome host della macchina virtuale, macchina virtuale del server DNS hello devono risiedere in hello stessa rete virtuale ed essere tooAzure query di nome host tooforward configurato. Poiché il suffisso DNS hello è diverso in ogni rete virtuale, è possibile usare l'inoltro condizionale regole toosend DNS esegue una query toohello correggere la rete virtuale per la risoluzione. Hello immagine seguente mostra due reti virtuali e una rete locale fase di risoluzione DNS tra reti virtuali tramite questo metodo:

![Risoluzione DNS tra reti virtuali](./media/azure-dns/inter-vnet-dns.png)

Quando si utilizza la risoluzione dei nomi forniti da Azure, il suffisso DNS interno hello viene fornito macchina virtuale tooeach mediante il protocollo DHCP. Quando si utilizza la propria soluzione di risoluzione del nome, il suffisso non è fornito toovirtual macchine perché suffisso hello interferisce con altre architetture DNS. toomachines toorefer dal nome di dominio completo o tooconfigure suffisso hello nelle macchine virtuali, è possibile utilizzare PowerShell o hello suffisso hello toodetermine di API:

* Per le reti virtuali gestiti da Gestione risorse di Azure, è disponibile tramite hello suffisso hello [scheda di interfaccia di rete](https://msdn.microsoft.com/library/azure/mt163668.aspx) risorse. È anche possibile eseguire hello `azure network public-ip show <resource group> <pip name>` comando dettagli hello toodisplay dell'indirizzo IP pubblico, che include hello FQDN di hello scheda di rete.

Se l'inoltro delle query tooAzure non in base alle esigenze, è necessario tooprovide la soluzione DNS personalizzata.  La soluzione DNS deve:

* Offrire una soluzione di risoluzione dei nomi host appropriata, ad esempio tramite [DNS dinamico](../../virtual-network/virtual-networks-name-resolution-ddns.md). Se si utilizza DDNS, si potrebbe essere necessario lo scavenging dei record DNS sul toodisable. Le lease DHCP di Azure sono molto lunghe e lo scavenging può rimuovere i record DNS in modo anomalo.
* Fornire la risoluzione di tooallow ricorsiva appropriato risoluzione dei nomi di dominio esterno.
* Accessibile (TCP e UDP sulla porta 53) dai client hello che serve e hello tooaccess in grado di Internet.
* Essere protetta da accessi da hello Internet toomitigate imbattono dagli agenti esterni.

> [!NOTE]
> Per prestazioni ottimali, quando si utilizzano macchine virtuali nel server DNS di Azure, disabilitare il protocollo IPv6 e assegnare un [indirizzo IP pubblico a livello di istanza](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach macchina virtuale del server DNS.  
>
>
