---
title: aaaConfiguring DHCPv6 per le macchine virtuali Linux | Documenti Microsoft
description: Come tooconfigure DHCPv6 per le macchine virtuali Linux.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>Configurazione di DHCPv6 per VM Linux

Alcune delle immagini di macchine virtuali Linux hello in hello Azure Marketplace non è necessario DHCPv6 configurata per impostazione predefinita. IPv6, DHCPv6 toosupport deve essere configurato all'interno di distribuzione del sistema operativo Linux hello che si sta utilizzando. Le diverse distribuzioni Linux hanno modalità diverse per configurare DHCPv6 perché usano pacchetti differenti.

> [!NOTE]
> È state preconfigurate con DHCPv6 recenti immagini SUSE Linux e CoreOS hello Azure Marketplace. Non sono necessarie altre modifiche quando si usano tali immagini.

Questo documento descrive come tooenable DHCPv6 in modo che la macchina virtuale Linux ottenga un indirizzo IPv6.

> [!WARNING]
> Modifica in modo non corretto dei file di configurazione di rete può causare si toolose rete accesso tooyour macchina virtuale. È consigliabile testare le modifiche alla configurazione nei sistemi non di produzione. istruzioni di Hello in questo articolo sono state testate su versioni più recenti di hello delle immagini Linux hello hello Azure Marketplace. Consultare la documentazione di hello per la versione specifica di Linux per istruzioni più dettagliate.

## <a name="ubuntu"></a>Ubuntu

1. Modificare il file hello `/etc/dhcp/dhclient6.conf` e aggiungere hello seguente riga:

        timeout 10;

2. Modificare la configurazione di rete hello per hello eth0 interfaccia con hello seguente configurazione:

   * In **Ubuntu 12.04 e 14.04**, modificare il file hello`/etc/network/interfaces.d/eth0.cfg`
   * In **Ubuntu 16.04**, modificare il file hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Rinnovare l'indirizzo IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Modificare il file hello `/etc/dhcp/dhclient6.conf` e aggiungere hello seguente riga:

        timeout 10;

2. Modificare il file hello `/etc/network/interfaces` e aggiungere hello seguente configurazione:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Rinnovare l'indirizzo IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Modificare il file hello `/etc/sysconfig/network` e aggiungere hello seguente parametro:

        NETWORKING_IPV6=yes

2. Modificare il file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguenti due parametri:

        IPV6INIT=yes
        DHCPV6C=yes

3. Rinnovare l'indirizzo IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 e openSUSE 13

Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6. Non sono necessarie altre modifiche quando si usano tali immagini. Se si dispone di una macchina virtuale in base a un'immagine SUSE personalizzata o precedente, utilizzare hello alla procedura seguente:

1. Installare hello `dhcp-client` del pacchetto, se necessario:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Modificare il file hello `/etc/sysconfig/network/ifcfg-eth0` e aggiungere hello seguente parametro:

        DHCLIENT6_MODE='managed'

3. Rinnovare l'indirizzo IPv6 hello:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 e openSUSE Leap

Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6. Non sono necessarie altre modifiche quando si usano tali immagini. Se si dispone di una macchina virtuale in base a un'immagine SUSE personalizzata o precedente, utilizzare hello alla procedura seguente:

1. Modificare il file hello `/etc/sysconfig/network/ifcfg-eth0` e sostituire il parametro

        #BOOTPROTO='dhcp4'

    con hello il valore seguente:

        BOOTPROTO='dhcp'

2. Aggiungere hello segue parametro troppo`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Rinnovare l'indirizzo IPv6 hello:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Le immagini recenti di CoreOS in Azure sono state preconfigurate con DHCPv6. Non sono necessarie altre modifiche quando si usano tali immagini. Se si dispone di una macchina virtuale in base a un'immagine di CoreOS personalizzata o precedente, utilizzare hello alla procedura seguente:

1. Modificare il file hello`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Rinnovare l'indirizzo IPv6 hello:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
