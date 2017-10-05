---
title: Configurazione di DHCPv6 per VM Linux | Microsoft Docs
description: Come configurare DHCPv6 per VM Linux.
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="14907-104">Configurazione di DHCPv6 per VM Linux</span><span class="sxs-lookup"><span data-stu-id="14907-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="14907-105">Per alcune delle immagini di macchina virtuale Linux in Azure Marketplace, DHCPv6 non è configurato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="14907-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="14907-106">Per supportare IPv6, è necessario configurare DHCPv6 all'interno della distribuzione del sistema operativo Linux usato.</span><span class="sxs-lookup"><span data-stu-id="14907-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="14907-107">Le diverse distribuzioni Linux hanno modalità diverse per configurare DHCPv6 perché usano pacchetti differenti.</span><span class="sxs-lookup"><span data-stu-id="14907-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="14907-108">Le immagini recenti di SUSE Linux e CoreOS in Azure Marketplace sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="14907-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="14907-109">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="14907-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="14907-110">Questo documento descrive come abilitare DHCPv6 in modo che la macchina virtuale Linux ottenga un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="14907-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="14907-111">La modifica errata dei file di configurazione della rete può causare la perdita dell'accesso alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14907-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="14907-112">È consigliabile testare le modifiche alla configurazione nei sistemi non di produzione.</span><span class="sxs-lookup"><span data-stu-id="14907-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="14907-113">Le istruzioni riportate in questo articolo sono state testate sulle versioni più recenti delle immagini Linux in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="14907-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="14907-114">Consultare la documentazione per la versione specifica di Linux per istruzioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="14907-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="14907-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="14907-115">Ubuntu</span></span>

1. <span data-ttu-id="14907-116">Modificare il file `/etc/dhcp/dhclient6.conf` e aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="14907-117">Modificare la configurazione della rete per l'interfaccia eth0 con la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="14907-118">In **Ubuntu 12.04 e 14.04** modificare il file `/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="14907-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="14907-119">In **Ubuntu 16.04**modificare il file `/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="14907-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="14907-120">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="14907-121">Debian</span><span class="sxs-lookup"><span data-stu-id="14907-121">Debian</span></span>

1. <span data-ttu-id="14907-122">Modificare il file `/etc/dhcp/dhclient6.conf` e aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="14907-123">Modificare il file `/etc/network/interfaces` e aggiungere la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="14907-124">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="14907-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="14907-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="14907-126">Modificare il file `/etc/sysconfig/network` e aggiungere il parametro seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="14907-127">Modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere i due parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="14907-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="14907-128">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="14907-129">SLES 11 e openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="14907-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="14907-130">Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="14907-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="14907-131">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="14907-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="14907-132">Con una macchina virtuale basata su un'immagine di SUSE personalizzata o precedente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="14907-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="14907-133">Installare il pacchetto `dhcp-client` , se necessario:</span><span class="sxs-lookup"><span data-stu-id="14907-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="14907-134">Modificare il file `/etc/sysconfig/network/ifcfg-eth0` e aggiungere il parametro seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="14907-135">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="14907-136">SLES 12 e openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="14907-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="14907-137">Le immagini recenti di SLES e openSUSE in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="14907-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="14907-138">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="14907-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="14907-139">Con una macchina virtuale basata su un'immagine di SUSE personalizzata o precedente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="14907-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="14907-140">Modificare il file `/etc/sysconfig/network/ifcfg-eth0` e sostituire questo parametro</span><span class="sxs-lookup"><span data-stu-id="14907-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="14907-141">con il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="14907-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="14907-142">Aggiungere il parametro seguente a `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="14907-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="14907-143">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="14907-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="14907-144">CoreOS</span></span>

<span data-ttu-id="14907-145">Le immagini recenti di CoreOS in Azure sono state preconfigurate con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="14907-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="14907-146">Non sono necessarie altre modifiche quando si usano tali immagini.</span><span class="sxs-lookup"><span data-stu-id="14907-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="14907-147">Con una macchina virtuale basata su un'immagine di CoreOS personalizzata o precedente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="14907-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="14907-148">Modificare il file `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="14907-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="14907-149">Rinnovare l'indirizzo IPv6:</span><span class="sxs-lookup"><span data-stu-id="14907-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
