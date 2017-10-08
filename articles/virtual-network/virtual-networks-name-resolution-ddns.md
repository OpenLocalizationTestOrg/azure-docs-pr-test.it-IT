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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Utilizzando i nomi host tooregister DNS dinamico nel proprio server DNS
[Azure offre la risoluzione dei nomi](virtual-networks-name-resolution-for-vms-and-role-instances.md) per le macchine virtuali e le istanze del ruolo. Tuttavia, quando la risoluzione dei nomi offerta da Azure non è sufficiente, è possibile usare i propri server DNS. In questo modo si hello power tootailor il toosuit soluzione DNS esigenze specifiche. Ad esempio, potrebbe essere necessario tooaccess alle risorse locali tramite il controller di dominio Active Directory.

Quando i server DNS personalizzati vengono ospitati come macchine virtuali di Azure è possibile inoltrare hostname query per hello stessi nomi host tooresolve tooAzure di rete virtuale. Se non si desidera toouse questa route, è possibile registrare i nomi host macchina virtuale nel server DNS tramite DNS dinamico.  Azure non dispone di hello capacità (ad esempio credenziali) toodirectly creare i record nel server DNS, in modo alternativi disposizioni sono spesso necessarie. Di seguito sono riportati alcuni scenari comuni con alternative.

## <a name="windows-clients"></a>Client Windows
I client Windows non di dominio cercano di eseguire aggiornamenti DNS dinamici non protetti (DDNS) all'avvio o alla modifica dell'indirizzo IP. nome DNS Hello è hostname hello più il suffisso DNS primario di hello. Azure lascia vuoto il suffisso DNS primario di hello, ma è possibile impostarlo in hello VM, tramite hello [dell'interfaccia utente](https://technet.microsoft.com/library/cc794784.aspx) o [utilizzando l'automazione](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

I client Windows di dominio registrano gli indirizzi IP con il controller di dominio hello tramite DNS dinamico protetto. il processo di aggiunta al dominio Hello imposta il suffisso DNS primario di hello client hello e crea e gestisce la relazione di trust hello.

## <a name="linux-clients"></a>Client Linux
I client Linux in genere non effettuano la registrazione con il server DNS hello all'avvio, si presume che il server DHCP hello lo fa. Server DHCP di Azure non è necessario il possibilità hello o record tooregister credenziali nel server DNS.  È possibile utilizzare uno strumento denominato *nsupdate*, che è incluso nel pacchetto di binding hello, gli aggiornamenti dinamici DNS toosend. Poiché il protocollo DNS dinamico hello standardizzato, è possibile utilizzare *nsupdate* anche quando non si usi Bind sul server DNS hello.

È possibile utilizzare gli hook hello forniti da toocreate di client DHCP hello e mantenere una voce di nome host hello del server DNS hello. Durante il ciclo di hello DHCP, client hello esegue script hello in */etc/dhcp/dhclient-exit-hooks.d/*. Può essere usato tooregister hello nuovo indirizzo IP tramite *nsupdate*. ad esempio:

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

        
        

È inoltre possibile utilizzare hello *nsupdate* tooperform comando Aggiorna il DNS dinamico protetto. Ad esempio, quando si usa un server DNS con Bind, viene [generata](http://linux.yyz.us/nsupdate/)una coppia di chiavi pubblica/privata.  server DNS Hello è [configurato](http://linux.yyz.us/dns/ddns-server.html) con parte pubblica di hello della chiave di hello in modo che si possa verificare hello firma richiesta hello. È necessario utilizzare hello *-k* tooprovide opzione hello coppia di chiavi troppo*nsupdate* affinché hello DNS dinamico aggiornare toobe richiesta firmata.

Quando si utilizza un server DNS di Windows, è possibile utilizzare l'autenticazione Kerberos con hello *-g* parametro *nsupdate* (non disponibile in versione di Windows hello *nsupdate* ). toodo questa operazione, utilizzare *kinit* credenziali hello tooload (ad esempio da un [file keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Quindi *nsupdate -g* selezionerà credenziali hello dalla cache di hello.

Se necessario, è possibile aggiungere un tooyour suffisso di ricerca DNS macchine virtuali. viene specificato un suffisso DNS Hello in hello */etc/resolv.conf* file. La maggior parte delle distribuzioni di Linux gestire automaticamente il contenuto di hello di questo file, pertanto, in genere non è possibile modificarlo. Tuttavia, è possibile eseguire l'override di suffisso hello utilizzando hello DHCP client *sostituiscono* comando. toodo questo, in */etc/dhcp/dhclient.conf*, aggiungere:

        supersede domain-name <required-dns-suffix>;

