---
title: aaaRemote Desktop tooa VM Linux | Documenti Microsoft
description: Informazioni su come tooinstall e configurare Desktop remoto tooconnect tooa VM Linux di Microsoft Azure per modello di distribuzione classica hello
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="6d7f3-103">Utilizzo di Desktop remoto tooconnect tooa VM Linux di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f3-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="6d7f3-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6d7f3-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6d7f3-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6d7f3-107">Per hello aggiornata la versione di gestione risorse di questo articolo, vedere [qui](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="6d7f3-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6d7f3-108">Overview</span></span>
<span data-ttu-id="6d7f3-109">Il protocollo RDP (Remote Desktop Protocol) è un protocollo proprietario utilizzato per Windows.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="6d7f3-110">Come possiamo usare RDP tooconnect tooa VM Linux (macchina virtuale) in modalità remota?</span><span class="sxs-lookup"><span data-stu-id="6d7f3-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="6d7f3-111">Questa Guida verrà fornite risposte hello!</span><span class="sxs-lookup"><span data-stu-id="6d7f3-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="6d7f3-112">Questo risulterà utile xrdp tooinstall e file di configurazione nella macchina virtuale Linux di Microsoft Azure, che consente di connettersi tooit con Desktop remoto da un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="6d7f3-113">Si utilizzerà VM Linux in esecuzione Ubuntu o OpenSUSE come esempio hello in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="6d7f3-114">strumento xrdp Hello è open source server RDP che consente di tooconnect server Linux con Desktop remoto da un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="6d7f3-115">RDP offre prestazioni migliori di VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="6d7f3-116">VNC esegue il rendering usando una grafica di qualità JPEG e può risultare lento, mentre RDP è veloce e nitido.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7f3-117">È necessario disporre di una macchina virtuale di Microsoft Azure che esegue Linux.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="6d7f3-118">toocreate e impostare una VM Linux, vedere hello [esercitazione VM Linux di Azure](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="6d7f3-119">Creare un endpoint per Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="6d7f3-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="6d7f3-120">Si utilizzerà l'endpoint predefinito hello 3389 per Desktop remoto in questo documento. Configurare un endpoint 3389 come `Remote Desktop` tooyour VM Linux come il seguente:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![immagine](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="6d7f3-122">Se non si conosce tooset un endpoint per la macchina virtuale, vedere [questa Guida](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="6d7f3-123">Installare Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="6d7f3-123">Install Gnome Desktop</span></span>
<span data-ttu-id="6d7f3-124">Tooyour VM Linux di connettersi tramite `putty`e installare `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="6d7f3-125">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="6d7f3-126">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="6d7f3-127">Installare xrdp</span><span class="sxs-lookup"><span data-stu-id="6d7f3-127">Install xrdp</span></span>
<span data-ttu-id="6d7f3-128">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="6d7f3-129">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="6d7f3-130">Aggiornare versione OpenSUSE hello con la versione di hello utilizzate nel comando seguente hello.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="6d7f3-131">esempio Hello seguente riguarda `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="6d7f3-132">Avviare xrdp e impostare il servizio xdrp all'avvio</span><span class="sxs-lookup"><span data-stu-id="6d7f3-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="6d7f3-133">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="6d7f3-134">Per Ubuntu, xrdp verrà avviato e abilitato automaticamente al momento dell'avvio dopo l'installazione.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="6d7f3-135">Uso di xfce se si usa una versione di Ubuntu successiva a Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="6d7f3-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="6d7f3-136">Poiché hello versione corrente di xrdp non supporta Desktop Gnome per Ubuntu versioni successiva Ubuntu 12.04LTS, si utilizzerà `xfce` Desktop invece.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="6d7f3-137">tooinstall `xfce`, utilizzare questo comando:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="6d7f3-138">Quindi abilitare `xfce` usando questo comando:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="6d7f3-139">Modificare il file di configurazione di hello `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="6d7f3-140">Aggiungere la riga hello `xfce4-session` prima riga hello `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="6d7f3-141">toorestart hello xrdp servizio, usare questa opzione:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="6d7f3-142">Connettersi alla macchina virtuale Linux da un computer Windows</span><span class="sxs-lookup"><span data-stu-id="6d7f3-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="6d7f3-143">In un computer Windows, avviare il client Desktop remoto hello e il nome DNS VM Linux di input.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="6d7f3-144">O toohello Dashboard della macchina virtuale nel portale di Azure hello, fare clic su `Connect` tooconnect VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="6d7f3-145">In tal caso, si vedere la finestra di accesso hello:</span><span class="sxs-lookup"><span data-stu-id="6d7f3-145">In that case, you see hello login window:</span></span>

![immagine](./media/remote-desktop/no2.png)

<span data-ttu-id="6d7f3-147">Accedere con il nome di utente hello e la password della VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6d7f3-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d7f3-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d7f3-148">Next steps</span></span>
<span data-ttu-id="6d7f3-149">Per altre informazioni sull'uso di xrdp, vedere [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="6d7f3-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
