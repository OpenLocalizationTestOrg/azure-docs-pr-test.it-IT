---
title: Desktop remoto per una macchina virtuale Linux | Microsoft Docs
description: Informazioni sull'installazione e la configurazione di Desktop remoto per la connessione a una macchina virtuale Linux di Microsoft Azure per il modello di distribuzione classica
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
ms.openlocfilehash: 68031d548bdbeda9a83d1bceaaea7c5bbcab3188
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a><span data-ttu-id="aa4c4-103">Uso di Desktop remoto per connettersi a una macchina virtuale Linux di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="aa4c4-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aa4c4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="aa4c4-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="aa4c4-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="aa4c4-107">Per la versione aggiornata di questo articolo relativa a Resource Manager, vedere [qui](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="aa4c4-107">For the updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="aa4c4-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="aa4c4-108">Overview</span></span>
<span data-ttu-id="aa4c4-109">Il protocollo RDP (Remote Desktop Protocol) è un protocollo proprietario utilizzato per Windows.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="aa4c4-110">Come si può utilizzare RDP per connettersi a una VM (macchina virtuale) Linux in modalità remota?</span><span class="sxs-lookup"><span data-stu-id="aa4c4-110">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="aa4c4-111">L'articolo seguente risponderà a questa domanda.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-111">This guidance will give you the answer!</span></span> <span data-ttu-id="aa4c4-112">Illustrerà come installare e configurare xrdp su una macchina virtuale Linux di Microsoft Azure in modo da connettersi a essa con Desktop remoto da un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-112">It will help you to install and config xrdp on your Microsoft Azure Linux VM, which lets you connect to it with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="aa4c4-113">Utilizzeremo una macchina virtuale Linux che esegue Ubuntu o OpenSUSE come nell'esempio riportato in questa guida.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-113">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span></span>

<span data-ttu-id="aa4c4-114">Lo strumento xrdp è un server RDP open source che consente di connettere il server Linux con Desktop remoto da un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-114">The xrdp tool is an open source RDP server that allows you to connect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="aa4c4-115">RDP offre prestazioni migliori di VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="aa4c4-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="aa4c4-116">VNC esegue il rendering usando una grafica di qualità JPEG e può risultare lento, mentre RDP è veloce e nitido.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4c4-117">È necessario disporre di una macchina virtuale di Microsoft Azure che esegue Linux.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="aa4c4-118">Vedere l'[esercitazione relativa alle macchine virtuali Linux di Azure](createportal.md)per creare e impostare una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-118">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="aa4c4-119">Creare un endpoint per Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="aa4c4-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="aa4c4-120">In questo documento verrà usato l'endpoint predefinito 3389 per Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-120">We will use the default endpoint 3389 for Remote Desktop in this doc.</span></span> <span data-ttu-id="aa4c4-121">Configurare l'endpoint 3389 come `Remote Desktop` per la macchina virtuale Linux nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-121">Set up 3389 endpoint as `Remote Desktop` to your Linux VM like below:</span></span>

![immagine](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="aa4c4-123">Per informazioni su come configurare un endpoint per la macchina virtuale, vedere [queste indicazioni](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="aa4c4-123">If you don't know how to set up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="aa4c4-124">Installare Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="aa4c4-124">Install Gnome Desktop</span></span>
<span data-ttu-id="aa4c4-125">Connettersi alla macchina virtuale Linux tramite `putty` e installare `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-125">Connect to your Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="aa4c4-126">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-126">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="aa4c4-127">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-127">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="aa4c4-128">Installare xrdp</span><span class="sxs-lookup"><span data-stu-id="aa4c4-128">Install xrdp</span></span>
<span data-ttu-id="aa4c4-129">Per Ubuntu, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-129">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="aa4c4-130">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-130">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="aa4c4-131">Aggiornare la versione OpenSUSE con la versione in uso nel comando seguente.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-131">Update the OpenSUSE version with the version you are using in the following command.</span></span> <span data-ttu-id="aa4c4-132">Di seguito è riportato un comando di esempio per `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-132">The example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="aa4c4-133">Avviare xrdp e impostare il servizio xdrp all'avvio</span><span class="sxs-lookup"><span data-stu-id="aa4c4-133">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="aa4c4-134">Per OpenSUSE, usare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-134">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="aa4c4-135">Per Ubuntu, xrdp verrà avviato e abilitato automaticamente al momento dell'avvio dopo l'installazione.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-135">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="aa4c4-136">Uso di xfce se si usa una versione di Ubuntu successiva a Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="aa4c4-136">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="aa4c4-137">Poiché attualmente xrdp non supporta Gnome Desktop per le versioni di Ubuntu successive a Ubuntu 12.04LTS, verrà usato Desktop `xfce`.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-137">Because the current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="aa4c4-138">Per installare `xfce`, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-138">To install `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="aa4c4-139">Quindi abilitare `xfce` usando questo comando:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-139">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="aa4c4-140">Modificare il file di configurazione `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-140">Edit the config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="aa4c4-141">Aggiungere la riga `xfce4-session` prima della riga `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-141">Add the line `xfce4-session` before the line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="aa4c4-142">Per riavviare il servizio xrdp, usare:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-142">To restart the xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="aa4c4-143">Connettersi alla macchina virtuale Linux da un computer Windows</span><span class="sxs-lookup"><span data-stu-id="aa4c4-143">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="aa4c4-144">In un computer Windows avviare il client Desktop remoto e immettere il nome DNS della macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="aa4c4-144">In a Windows machine, start the Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="aa4c4-145">oppure passare al dashboard della macchina virtuale nel portale di Azure e fare clic su `Connect` per connettere la macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-145">Or go to the Dashboard of your VM in the Azure portal and click `Connect` to connect your Linux VM.</span></span> <span data-ttu-id="aa4c4-146">In questo caso verrà visualizzata la finestra di accesso:</span><span class="sxs-lookup"><span data-stu-id="aa4c4-146">In that case, you see the login window:</span></span>

![immagine](./media/remote-desktop/no2.png)

<span data-ttu-id="aa4c4-148">Accedere con il nome utente e la password della macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="aa4c4-148">Log in with the user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4c4-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa4c4-149">Next steps</span></span>
<span data-ttu-id="aa4c4-150">Per altre informazioni sull'uso di xrdp, vedere [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="aa4c4-150">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
