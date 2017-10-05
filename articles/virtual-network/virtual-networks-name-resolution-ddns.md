---
title: Uso di DNS dinamico per registrare i nomi host
description: Questa pagina offre informazioni dettagliate su come configurare DNS dinamico per registrare i nomi host nei propri server DNS.
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
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="8edcd-103">Uso di DNS dinamico per registrare i nomi host nel proprio server DNS</span><span class="sxs-lookup"><span data-stu-id="8edcd-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="8edcd-104">[Azure offre la risoluzione dei nomi](virtual-networks-name-resolution-for-vms-and-role-instances.md) per le macchine virtuali e le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="8edcd-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="8edcd-105">Tuttavia, quando la risoluzione dei nomi offerta da Azure non è sufficiente, è possibile usare i propri server DNS.</span><span class="sxs-lookup"><span data-stu-id="8edcd-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="8edcd-106">In questo modo è possibile personalizzare la soluzione DNS in base alle esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="8edcd-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="8edcd-107">Ad esempio, può essere necessario accedere a risorse locali tramite il controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8edcd-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="8edcd-108">Quando i server DNS personalizzati vengono ospitati come VM di Azure è possibile inoltrare le query di nome host per la stessa rete virtuale in Azure per risolvere i nomi host.</span><span class="sxs-lookup"><span data-stu-id="8edcd-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="8edcd-109">Se non si desidera usare questa route, è possibile registrare i nomi host delle VM nel server DNS tramite DNS dinamico.</span><span class="sxs-lookup"><span data-stu-id="8edcd-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="8edcd-110">Poiché Azure non è in grado (ad esempio, non offre le credenziali) di creare direttamente i record nei server DNS, è spesso necessario ricorrere a soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="8edcd-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="8edcd-111">Di seguito sono riportati alcuni scenari comuni con alternative.</span><span class="sxs-lookup"><span data-stu-id="8edcd-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="8edcd-112">Client Windows</span><span class="sxs-lookup"><span data-stu-id="8edcd-112">Windows clients</span></span>
<span data-ttu-id="8edcd-113">I client Windows non di dominio cercano di eseguire aggiornamenti DNS dinamici non protetti (DDNS) all'avvio o alla modifica dell'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="8edcd-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="8edcd-114">Il nome DNS è il nome host unito al suffisso DNS primario.</span><span class="sxs-lookup"><span data-stu-id="8edcd-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="8edcd-115">Azure lascia vuoto il suffisso DNS primario, ma può essere impostato nella VM tramite l'[interfaccia utente](https://technet.microsoft.com/library/cc794784.aspx) o [con l'automazione](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="8edcd-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="8edcd-116">I client Windows appartenenti a un dominio registrano i relativi indirizzi IP con il controller di dominio usando DNS dinamico protetto.</span><span class="sxs-lookup"><span data-stu-id="8edcd-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="8edcd-117">Il processo appartenente a un dominio imposta il suffisso DNS primario nel client e crea e gestisce la relazione di trust.</span><span class="sxs-lookup"><span data-stu-id="8edcd-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="8edcd-118">Client Linux</span><span class="sxs-lookup"><span data-stu-id="8edcd-118">Linux clients</span></span>
<span data-ttu-id="8edcd-119">I client Linux solitamente non si registrano con il server DNS all'avvio, presuppongono che il server DHCP esegua l'operazione.</span><span class="sxs-lookup"><span data-stu-id="8edcd-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="8edcd-120">I server DHCP di Azure non sono in grado o non dispongono delle credenziali per registrare i record nel server DNS.</span><span class="sxs-lookup"><span data-stu-id="8edcd-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="8edcd-121">È possibile usare uno strumento denominato *nsupdate*, incluso nel pacchetto di binding, per inviare gli aggiornamenti del DNS dinamico.</span><span class="sxs-lookup"><span data-stu-id="8edcd-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="8edcd-122">Poiché il protocollo DNS dinamico è standardizzato, è possibile usare *nsupdate* anche quando non si usa il pacchetto Bind sul server DNS.</span><span class="sxs-lookup"><span data-stu-id="8edcd-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="8edcd-123">È possibile usare gli hook messi a disposizione dal client DHCP per creare e gestire il nome host nel server DNS.</span><span class="sxs-lookup"><span data-stu-id="8edcd-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="8edcd-124">Durante il ciclo DHCP, il client esegue gli script in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="8edcd-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="8edcd-125">Questo può essere usato per registrare il nuovo indirizzo IP tramite *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="8edcd-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="8edcd-126">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8edcd-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
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

        
        

<span data-ttu-id="8edcd-127">È anche possibile usare il comando *nsupdate* per eseguire gli aggiornamenti dinamici protetti DNS.</span><span class="sxs-lookup"><span data-stu-id="8edcd-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="8edcd-128">Ad esempio, quando si usa un server DNS con Bind, viene [generata](http://linux.yyz.us/nsupdate/)una coppia di chiavi pubblica/privata.</span><span class="sxs-lookup"><span data-stu-id="8edcd-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="8edcd-129">Il server DNS è [configurato](http://linux.yyz.us/dns/ddns-server.html) con la parte pubblica della chiave, che consente di verificare la firma della richiesta.</span><span class="sxs-lookup"><span data-stu-id="8edcd-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="8edcd-130">È necessario usare l'opzione *-k* per indicare la coppia di chiavi a *nsupdate*, in modo da firmare la richiesta di aggiornamento DNS dinamico.</span><span class="sxs-lookup"><span data-stu-id="8edcd-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="8edcd-131">Quando si usa un server DNS Windows, è possibile usare l'autenticazione Kerberos con il parametro *-g* in *nsupdate* (non disponibile nella versione Windows di *nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="8edcd-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="8edcd-132">A tale scopo, usare *kinit* per caricare le credenziali (ad esempio, da un [file keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="8edcd-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="8edcd-133">Quindi, *nsupdate -g* acquisirà le credenziali dalla cache.</span><span class="sxs-lookup"><span data-stu-id="8edcd-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="8edcd-134">Se necessario, aggiungere un suffisso di ricerca DNS alle VM.</span><span class="sxs-lookup"><span data-stu-id="8edcd-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="8edcd-135">Il suffisso DNS è specificato nel file */etc/resolv.conf* .</span><span class="sxs-lookup"><span data-stu-id="8edcd-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="8edcd-136">La maggior parte delle distribuzioni Linux gestiscono automaticamente il contenuto di questo file, quindi solitamente non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="8edcd-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="8edcd-137">Tuttavia, è possibile ignorare il suffisso usando il comando *supersede* del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="8edcd-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="8edcd-138">A tale scopo, in */etc/dhcp/dhclient.conf*aggiungere:</span><span class="sxs-lookup"><span data-stu-id="8edcd-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

