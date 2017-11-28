---
title: i nomi host tooregister DNS dinamico aaaUsing
description: Questa pagina fornisce informazioni dettagliate su come tooset i nomi host tooregister DNS dinamico nei propri server DNS.
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="c60de-103">Utilizzando i nomi host tooregister DNS dinamico nel proprio server DNS</span><span class="sxs-lookup"><span data-stu-id="c60de-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="c60de-104">[Azure offre la risoluzione dei nomi](virtual-networks-name-resolution-for-vms-and-role-instances.md) per le macchine virtuali e le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="c60de-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="c60de-105">Tuttavia, quando la risoluzione dei nomi offerta da Azure non è sufficiente, è possibile usare i propri server DNS.</span><span class="sxs-lookup"><span data-stu-id="c60de-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="c60de-106">In questo modo si hello power tootailor il toosuit soluzione DNS esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="c60de-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="c60de-107">Ad esempio, potrebbe essere necessario tooaccess alle risorse locali tramite il controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c60de-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="c60de-108">Quando i server DNS personalizzati vengono ospitati come macchine virtuali di Azure è possibile inoltrare hostname query per hello stessi nomi host tooresolve tooAzure di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c60de-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="c60de-109">Se non si desidera toouse questa route, è possibile registrare i nomi host macchina virtuale nel server DNS tramite DNS dinamico.</span><span class="sxs-lookup"><span data-stu-id="c60de-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="c60de-110">Azure non dispone di hello capacità (ad esempio credenziali) toodirectly creare i record nel server DNS, in modo alternativi disposizioni sono spesso necessarie.</span><span class="sxs-lookup"><span data-stu-id="c60de-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="c60de-111">Di seguito sono riportati alcuni scenari comuni con alternative.</span><span class="sxs-lookup"><span data-stu-id="c60de-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="c60de-112">Client Windows</span><span class="sxs-lookup"><span data-stu-id="c60de-112">Windows clients</span></span>
<span data-ttu-id="c60de-113">I client Windows non di dominio cercano di eseguire aggiornamenti DNS dinamici non protetti (DDNS) all'avvio o alla modifica dell'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="c60de-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="c60de-114">nome DNS Hello è hostname hello più il suffisso DNS primario di hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="c60de-115">Azure lascia vuoto il suffisso DNS primario di hello, ma è possibile impostarlo in hello VM, tramite hello [dell'interfaccia utente](https://technet.microsoft.com/library/cc794784.aspx) o [utilizzando l'automazione](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="c60de-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="c60de-116">I client Windows di dominio registrano gli indirizzi IP con il controller di dominio hello tramite DNS dinamico protetto.</span><span class="sxs-lookup"><span data-stu-id="c60de-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="c60de-117">il processo di aggiunta al dominio Hello imposta il suffisso DNS primario di hello client hello e crea e gestisce la relazione di trust hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="c60de-118">Client Linux</span><span class="sxs-lookup"><span data-stu-id="c60de-118">Linux clients</span></span>
<span data-ttu-id="c60de-119">I client Linux in genere non effettuano la registrazione con il server DNS hello all'avvio, si presume che il server DHCP hello lo fa.</span><span class="sxs-lookup"><span data-stu-id="c60de-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="c60de-120">Server DHCP di Azure non è necessario il possibilità hello o record tooregister credenziali nel server DNS.</span><span class="sxs-lookup"><span data-stu-id="c60de-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="c60de-121">È possibile utilizzare uno strumento denominato *nsupdate*, che è incluso nel pacchetto di binding hello, gli aggiornamenti dinamici DNS toosend.</span><span class="sxs-lookup"><span data-stu-id="c60de-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="c60de-122">Poiché il protocollo DNS dinamico hello standardizzato, è possibile utilizzare *nsupdate* anche quando non si usi Bind sul server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="c60de-123">È possibile utilizzare gli hook hello forniti da toocreate di client DHCP hello e mantenere una voce di nome host hello del server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="c60de-124">Durante il ciclo di hello DHCP, client hello esegue script hello in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="c60de-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="c60de-125">Può essere usato tooregister hello nuovo indirizzo IP tramite *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="c60de-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="c60de-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c60de-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="c60de-127">È inoltre possibile utilizzare hello *nsupdate* tooperform comando Aggiorna il DNS dinamico protetto.</span><span class="sxs-lookup"><span data-stu-id="c60de-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="c60de-128">Ad esempio, quando si usa un server DNS con Bind, viene [generata](http://linux.yyz.us/nsupdate/)una coppia di chiavi pubblica/privata.</span><span class="sxs-lookup"><span data-stu-id="c60de-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="c60de-129">server DNS Hello è [configurato](http://linux.yyz.us/dns/ddns-server.html) con parte pubblica di hello della chiave di hello in modo che si possa verificare hello firma richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="c60de-130">È necessario utilizzare hello *-k* tooprovide opzione hello coppia di chiavi troppo*nsupdate* affinché hello DNS dinamico aggiornare toobe richiesta firmata.</span><span class="sxs-lookup"><span data-stu-id="c60de-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="c60de-131">Quando si utilizza un server DNS di Windows, è possibile utilizzare l'autenticazione Kerberos con hello *-g* parametro *nsupdate* (non disponibile in versione di Windows hello *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="c60de-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="c60de-132">toodo questa operazione, utilizzare *kinit* credenziali hello tooload (ad esempio da un [file keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="c60de-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="c60de-133">Quindi *nsupdate -g* selezionerà credenziali hello dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="c60de-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="c60de-134">Se necessario, è possibile aggiungere un tooyour suffisso di ricerca DNS macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c60de-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="c60de-135">viene specificato un suffisso DNS Hello in hello */etc/resolv.conf* file.</span><span class="sxs-lookup"><span data-stu-id="c60de-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="c60de-136">La maggior parte delle distribuzioni di Linux gestire automaticamente il contenuto di hello di questo file, pertanto, in genere non è possibile modificarlo.</span><span class="sxs-lookup"><span data-stu-id="c60de-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="c60de-137">Tuttavia, è possibile eseguire l'override di suffisso hello utilizzando hello DHCP client *sostituiscono* comando.</span><span class="sxs-lookup"><span data-stu-id="c60de-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="c60de-138">toodo questo, in */etc/dhcp/dhclient.conf*, aggiungere:</span><span class="sxs-lookup"><span data-stu-id="c60de-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

