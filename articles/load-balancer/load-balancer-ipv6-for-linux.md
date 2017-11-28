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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="20c54-104">Configurazione di DHCPv6 per VM Linux</span><span class="sxs-lookup"><span data-stu-id="20c54-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="20c54-105">Alcune delle immagini di macchine virtuali Linux hello in hello Azure Marketplace non è necessario DHCPv6 configurata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="20c54-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="20c54-106">IPv6, DHCPv6 toosupport deve essere configurato all'interno di distribuzione del sistema operativo Linux hello che si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="20c54-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="20c54-107">Le diverse distribuzioni Linux hanno modalità diverse per configurare DHCPv6 perché usano pacchetti differenti.</span><span class="sxs-lookup"><span data-stu-id="20c54-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="20c54-108">È state preconfigurate con DHCPv6 recenti immagini SUSE Linux e CoreOS hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="20c54-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="20c54-109">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="20c54-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="20c54-110">Questo documento descrive come tooenable DHCPv6 in modo che la macchina virtuale Linux ottenga un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="20c54-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="20c54-111">Modifica in modo non corretto dei file di configurazione di rete può causare si toolose rete accesso tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="20c54-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="20c54-112">È consigliabile testare le modifiche alla configurazione nei sistemi non di produzione.</span><span class="sxs-lookup"><span data-stu-id="20c54-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="20c54-113">istruzioni di Hello in questo articolo sono state testate su versioni più recenti di hello delle immagini Linux hello hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="20c54-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="20c54-114">Consultare la documentazione di hello per la versione specifica di Linux per istruzioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="20c54-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="20c54-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="20c54-115">Ubuntu</span></span>

1. <span data-ttu-id="20c54-116">Modificare il file hello `/etc/dhcp/dhclient6.conf` e aggiungere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="20c54-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="20c54-117">Modificare la configurazione di rete hello per hello eth0 interfaccia con hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="20c54-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="20c54-118">In **Ubuntu 12.04 e 14.04**, modificare il file hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="20c54-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="20c54-119">In **Ubuntu 16.04**, modificare il file hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="20c54-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="20c54-120">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="20c54-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="20c54-121">Debian</span><span class="sxs-lookup"><span data-stu-id="20c54-121">Debian</span></span>

1. <span data-ttu-id="20c54-122">Modificare il file hello `/etc/dhcp/dhclient6.conf` e aggiungere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="20c54-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="20c54-123">Modificare il file hello `/etc/network/interfaces` e aggiungere hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="20c54-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="20c54-124">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="20c54-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="20c54-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="20c54-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="20c54-126">Modificare il file hello `/etc/sysconfig/network` e aggiungere hello seguente parametro:</span><span class="sxs-lookup"><span data-stu-id="20c54-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="20c54-127">Modificare il file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguenti due parametri:</span><span class="sxs-lookup"><span data-stu-id="20c54-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="20c54-128">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="20c54-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="20c54-129">SLES 11 e openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="20c54-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="20c54-130">Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="20c54-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="20c54-131">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="20c54-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="20c54-132">Se si dispone di una macchina virtuale in base a un'immagine SUSE personalizzata o precedente, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="20c54-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="20c54-133">Installare hello `dhcp-client` del pacchetto, se necessario:</span><span class="sxs-lookup"><span data-stu-id="20c54-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="20c54-134">Modificare il file hello `/etc/sysconfig/network/ifcfg-eth0` e aggiungere hello seguente parametro:</span><span class="sxs-lookup"><span data-stu-id="20c54-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="20c54-135">Rinnovare l'indirizzo IPv6 hello:</span><span class="sxs-lookup"><span data-stu-id="20c54-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="20c54-136">SLES 12 e openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="20c54-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="20c54-137">Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="20c54-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="20c54-138">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="20c54-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="20c54-139">Se si dispone di una macchina virtuale in base a un'immagine SUSE personalizzata o precedente, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="20c54-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="20c54-140">Modificare il file hello `/etc/sysconfig/network/ifcfg-eth0` e sostituire il parametro</span><span class="sxs-lookup"><span data-stu-id="20c54-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="20c54-141">con hello il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="20c54-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="20c54-142">Aggiungere hello segue parametro troppo`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="20c54-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="20c54-143">Rinnovare l'indirizzo IPv6 hello:</span><span class="sxs-lookup"><span data-stu-id="20c54-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="20c54-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="20c54-144">CoreOS</span></span>

<span data-ttu-id="20c54-145">Le immagini recenti di CoreOS in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="20c54-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="20c54-146">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="20c54-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="20c54-147">Se si dispone di una macchina virtuale in base a un'immagine di CoreOS personalizzata o precedente, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="20c54-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="20c54-148">Modificare il file hello`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="20c54-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="20c54-149">Rinnovare l'indirizzo IPv6 hello:</span><span class="sxs-lookup"><span data-stu-id="20c54-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
