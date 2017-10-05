---
title: Selezione dei nomi utente per Linux | Microsoft Docs
description: Informazioni su come selezionare i nomi utente per una macchina virtuale Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="01623-103">Selezione dei nomi utente per Linux su Azure</span><span class="sxs-lookup"><span data-stu-id="01623-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="01623-104">Durante il provisioning di una macchina virtuale Linux in Azure è necessario specificare il nome di un utente non radice, che in un secondo momento è possibile utilizzare per accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="01623-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="01623-105">È possibile scegliere il nome del nuovo utente o se il provisioning avviene tramite il portale di Azure classico è possibile accettare il nome predefinito "azureuser".</span><span class="sxs-lookup"><span data-stu-id="01623-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="01623-106">Nella maggior parte dei casi questo nuovo utente non esiste nell'immagine di base e viene creato durante il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="01623-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="01623-107">Se l'utente esiste nell'immagine della VM di base, l'agente Linux di Azure configura la password (e/o la chiave SSH) per tale utente in base alle informazioni specificate durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="01623-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="01623-108">**Tuttavia**, Linux definisce un set di nomi utente che non devono essere usati.</span><span class="sxs-lookup"><span data-stu-id="01623-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="01623-109">Se si prova a eseguire il provisioning di una macchia virtuale Linux usando un utente di sistema esistente, definito come utente con un valore UID compreso tra 0 e 99, il processo avrà **esito negativo** .</span><span class="sxs-lookup"><span data-stu-id="01623-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="01623-110">Un esempio tipico è rappresentato dall'utente `root` , il cui valore UID è 0.</span><span class="sxs-lookup"><span data-stu-id="01623-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="01623-111">Vedere anche: [Base standard di Linux - Intervalli ID utente](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="01623-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="01623-112">L'elenco seguente include utenti di sistema predefiniti comuni per CentOS e Ubuntu che non devono essere usati quando si effettua il provisioning di una macchina virtuale Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="01623-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="01623-113">Questo elenco è solo un esempio. Vedere la documentazione specifica della distribuzione per assicurarsi che il nome utente scelto non sia in conflitto con un utente di sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="01623-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="01623-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="01623-114">CentOS</span></span>
* <span data-ttu-id="01623-115">abrt</span><span class="sxs-lookup"><span data-stu-id="01623-115">abrt</span></span>
* <span data-ttu-id="01623-116">adm</span><span class="sxs-lookup"><span data-stu-id="01623-116">adm</span></span>
* <span data-ttu-id="01623-117">audio</span><span class="sxs-lookup"><span data-stu-id="01623-117">audio</span></span>
* <span data-ttu-id="01623-118">bin</span><span class="sxs-lookup"><span data-stu-id="01623-118">bin</span></span>
* <span data-ttu-id="01623-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="01623-119">cdrom</span></span>
* <span data-ttu-id="01623-120">cgred</span><span class="sxs-lookup"><span data-stu-id="01623-120">cgred</span></span>
* <span data-ttu-id="01623-121">daemon</span><span class="sxs-lookup"><span data-stu-id="01623-121">daemon</span></span>
* <span data-ttu-id="01623-122">dbus</span><span class="sxs-lookup"><span data-stu-id="01623-122">dbus</span></span>
* <span data-ttu-id="01623-123">dialout</span><span class="sxs-lookup"><span data-stu-id="01623-123">dialout</span></span>
* <span data-ttu-id="01623-124">dip</span><span class="sxs-lookup"><span data-stu-id="01623-124">dip</span></span>
* <span data-ttu-id="01623-125">disk</span><span class="sxs-lookup"><span data-stu-id="01623-125">disk</span></span>
* <span data-ttu-id="01623-126">floppy</span><span class="sxs-lookup"><span data-stu-id="01623-126">floppy</span></span>
* <span data-ttu-id="01623-127">ftp</span><span class="sxs-lookup"><span data-stu-id="01623-127">ftp</span></span>
* <span data-ttu-id="01623-128">ftp</span><span class="sxs-lookup"><span data-stu-id="01623-128">ftp</span></span>
* <span data-ttu-id="01623-129">games</span><span class="sxs-lookup"><span data-stu-id="01623-129">games</span></span>
* <span data-ttu-id="01623-130">gopher</span><span class="sxs-lookup"><span data-stu-id="01623-130">gopher</span></span>
* <span data-ttu-id="01623-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="01623-131">haldaemon</span></span>
* <span data-ttu-id="01623-132">halt</span><span class="sxs-lookup"><span data-stu-id="01623-132">halt</span></span>
* <span data-ttu-id="01623-133">kmem</span><span class="sxs-lookup"><span data-stu-id="01623-133">kmem</span></span>
* <span data-ttu-id="01623-134">lock</span><span class="sxs-lookup"><span data-stu-id="01623-134">lock</span></span>
* <span data-ttu-id="01623-135">lp</span><span class="sxs-lookup"><span data-stu-id="01623-135">lp</span></span>
* <span data-ttu-id="01623-136">mail</span><span class="sxs-lookup"><span data-stu-id="01623-136">mail</span></span>
* <span data-ttu-id="01623-137">man</span><span class="sxs-lookup"><span data-stu-id="01623-137">man</span></span>
* <span data-ttu-id="01623-138">mem</span><span class="sxs-lookup"><span data-stu-id="01623-138">mem</span></span>
* <span data-ttu-id="01623-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="01623-139">nfsnobody</span></span>
* <span data-ttu-id="01623-140">nobody</span><span class="sxs-lookup"><span data-stu-id="01623-140">nobody</span></span>
* <span data-ttu-id="01623-141">ntp</span><span class="sxs-lookup"><span data-stu-id="01623-141">ntp</span></span>
* <span data-ttu-id="01623-142">operator</span><span class="sxs-lookup"><span data-stu-id="01623-142">operator</span></span>
* <span data-ttu-id="01623-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="01623-143">oprofile</span></span>
* <span data-ttu-id="01623-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="01623-144">postdrop</span></span>
* <span data-ttu-id="01623-145">postfix</span><span class="sxs-lookup"><span data-stu-id="01623-145">postfix</span></span>
* <span data-ttu-id="01623-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="01623-146">qpidd</span></span>
* <span data-ttu-id="01623-147">root</span><span class="sxs-lookup"><span data-stu-id="01623-147">root</span></span>
* <span data-ttu-id="01623-148">rpc</span><span class="sxs-lookup"><span data-stu-id="01623-148">rpc</span></span>
* <span data-ttu-id="01623-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="01623-149">rpcuser</span></span>
* <span data-ttu-id="01623-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="01623-150">saslauth</span></span>
* <span data-ttu-id="01623-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="01623-151">shutdown</span></span>
* <span data-ttu-id="01623-152">slocate</span><span class="sxs-lookup"><span data-stu-id="01623-152">slocate</span></span>
* <span data-ttu-id="01623-153">sshd</span><span class="sxs-lookup"><span data-stu-id="01623-153">sshd</span></span>
* <span data-ttu-id="01623-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="01623-154">stapdev</span></span>
* <span data-ttu-id="01623-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="01623-155">stapusr</span></span>
* <span data-ttu-id="01623-156">sync</span><span class="sxs-lookup"><span data-stu-id="01623-156">sync</span></span>
* <span data-ttu-id="01623-157">sys</span><span class="sxs-lookup"><span data-stu-id="01623-157">sys</span></span>
* <span data-ttu-id="01623-158">tape</span><span class="sxs-lookup"><span data-stu-id="01623-158">tape</span></span>
* <span data-ttu-id="01623-159">test</span><span class="sxs-lookup"><span data-stu-id="01623-159">test</span></span>
* <span data-ttu-id="01623-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="01623-160">tcpdump</span></span>
* <span data-ttu-id="01623-161">tty</span><span class="sxs-lookup"><span data-stu-id="01623-161">tty</span></span>
* <span data-ttu-id="01623-162">users</span><span class="sxs-lookup"><span data-stu-id="01623-162">users</span></span>
* <span data-ttu-id="01623-163">utempter</span><span class="sxs-lookup"><span data-stu-id="01623-163">utempter</span></span>
* <span data-ttu-id="01623-164">utmp</span><span class="sxs-lookup"><span data-stu-id="01623-164">utmp</span></span>
* <span data-ttu-id="01623-165">uucp</span><span class="sxs-lookup"><span data-stu-id="01623-165">uucp</span></span>
* <span data-ttu-id="01623-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="01623-166">vcsa</span></span>
* <span data-ttu-id="01623-167">video</span><span class="sxs-lookup"><span data-stu-id="01623-167">video</span></span>
* <span data-ttu-id="01623-168">wheel</span><span class="sxs-lookup"><span data-stu-id="01623-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="01623-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="01623-169">Ubuntu</span></span>
* <span data-ttu-id="01623-170">adm</span><span class="sxs-lookup"><span data-stu-id="01623-170">adm</span></span>
* <span data-ttu-id="01623-171">admin</span><span class="sxs-lookup"><span data-stu-id="01623-171">admin</span></span>
* <span data-ttu-id="01623-172">audio</span><span class="sxs-lookup"><span data-stu-id="01623-172">audio</span></span>
* <span data-ttu-id="01623-173">backup</span><span class="sxs-lookup"><span data-stu-id="01623-173">backup</span></span>
* <span data-ttu-id="01623-174">bin</span><span class="sxs-lookup"><span data-stu-id="01623-174">bin</span></span>
* <span data-ttu-id="01623-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="01623-175">cdrom</span></span>
* <span data-ttu-id="01623-176">crontab</span><span class="sxs-lookup"><span data-stu-id="01623-176">crontab</span></span>
* <span data-ttu-id="01623-177">daemon</span><span class="sxs-lookup"><span data-stu-id="01623-177">daemon</span></span>
* <span data-ttu-id="01623-178">dialout</span><span class="sxs-lookup"><span data-stu-id="01623-178">dialout</span></span>
* <span data-ttu-id="01623-179">dip</span><span class="sxs-lookup"><span data-stu-id="01623-179">dip</span></span>
* <span data-ttu-id="01623-180">disk</span><span class="sxs-lookup"><span data-stu-id="01623-180">disk</span></span>
* <span data-ttu-id="01623-181">fax</span><span class="sxs-lookup"><span data-stu-id="01623-181">fax</span></span>
* <span data-ttu-id="01623-182">floppy</span><span class="sxs-lookup"><span data-stu-id="01623-182">floppy</span></span>
* <span data-ttu-id="01623-183">fuse</span><span class="sxs-lookup"><span data-stu-id="01623-183">fuse</span></span>
* <span data-ttu-id="01623-184">games</span><span class="sxs-lookup"><span data-stu-id="01623-184">games</span></span>
* <span data-ttu-id="01623-185">gnats</span><span class="sxs-lookup"><span data-stu-id="01623-185">gnats</span></span>
* <span data-ttu-id="01623-186">irc</span><span class="sxs-lookup"><span data-stu-id="01623-186">irc</span></span>
* <span data-ttu-id="01623-187">kmem</span><span class="sxs-lookup"><span data-stu-id="01623-187">kmem</span></span>
* <span data-ttu-id="01623-188">landscape</span><span class="sxs-lookup"><span data-stu-id="01623-188">landscape</span></span>
* <span data-ttu-id="01623-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="01623-189">libuuid</span></span>
* <span data-ttu-id="01623-190">list</span><span class="sxs-lookup"><span data-stu-id="01623-190">list</span></span>
* <span data-ttu-id="01623-191">lp</span><span class="sxs-lookup"><span data-stu-id="01623-191">lp</span></span>
* <span data-ttu-id="01623-192">mail</span><span class="sxs-lookup"><span data-stu-id="01623-192">mail</span></span>
* <span data-ttu-id="01623-193">man</span><span class="sxs-lookup"><span data-stu-id="01623-193">man</span></span>
* <span data-ttu-id="01623-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="01623-194">messagebus</span></span>
* <span data-ttu-id="01623-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="01623-195">mlocate</span></span>
* <span data-ttu-id="01623-196">netdev</span><span class="sxs-lookup"><span data-stu-id="01623-196">netdev</span></span>
* <span data-ttu-id="01623-197">news</span><span class="sxs-lookup"><span data-stu-id="01623-197">news</span></span>
* <span data-ttu-id="01623-198">nobody</span><span class="sxs-lookup"><span data-stu-id="01623-198">nobody</span></span>
* <span data-ttu-id="01623-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="01623-199">nogroup</span></span>
* <span data-ttu-id="01623-200">operator</span><span class="sxs-lookup"><span data-stu-id="01623-200">operator</span></span>
* <span data-ttu-id="01623-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="01623-201">plugdev</span></span>
* <span data-ttu-id="01623-202">proxy</span><span class="sxs-lookup"><span data-stu-id="01623-202">proxy</span></span>
* <span data-ttu-id="01623-203">root</span><span class="sxs-lookup"><span data-stu-id="01623-203">root</span></span>
* <span data-ttu-id="01623-204">sasl</span><span class="sxs-lookup"><span data-stu-id="01623-204">sasl</span></span>
* <span data-ttu-id="01623-205">shadow</span><span class="sxs-lookup"><span data-stu-id="01623-205">shadow</span></span>
* <span data-ttu-id="01623-206">src</span><span class="sxs-lookup"><span data-stu-id="01623-206">src</span></span>
* <span data-ttu-id="01623-207">ssh</span><span class="sxs-lookup"><span data-stu-id="01623-207">ssh</span></span>
* <span data-ttu-id="01623-208">sshd</span><span class="sxs-lookup"><span data-stu-id="01623-208">sshd</span></span>
* <span data-ttu-id="01623-209">staff</span><span class="sxs-lookup"><span data-stu-id="01623-209">staff</span></span>
* <span data-ttu-id="01623-210">sudo</span><span class="sxs-lookup"><span data-stu-id="01623-210">sudo</span></span>
* <span data-ttu-id="01623-211">sync</span><span class="sxs-lookup"><span data-stu-id="01623-211">sync</span></span>
* <span data-ttu-id="01623-212">sys</span><span class="sxs-lookup"><span data-stu-id="01623-212">sys</span></span>
* <span data-ttu-id="01623-213">syslog</span><span class="sxs-lookup"><span data-stu-id="01623-213">syslog</span></span>
* <span data-ttu-id="01623-214">tape</span><span class="sxs-lookup"><span data-stu-id="01623-214">tape</span></span>
* <span data-ttu-id="01623-215">tty</span><span class="sxs-lookup"><span data-stu-id="01623-215">tty</span></span>
* <span data-ttu-id="01623-216">users</span><span class="sxs-lookup"><span data-stu-id="01623-216">users</span></span>
* <span data-ttu-id="01623-217">utmp</span><span class="sxs-lookup"><span data-stu-id="01623-217">utmp</span></span>
* <span data-ttu-id="01623-218">uucp</span><span class="sxs-lookup"><span data-stu-id="01623-218">uucp</span></span>
* <span data-ttu-id="01623-219">video</span><span class="sxs-lookup"><span data-stu-id="01623-219">video</span></span>
* <span data-ttu-id="01623-220">voice</span><span class="sxs-lookup"><span data-stu-id="01623-220">voice</span></span>
* <span data-ttu-id="01623-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="01623-221">whoopsie</span></span>
* <span data-ttu-id="01623-222">www-data</span><span class="sxs-lookup"><span data-stu-id="01623-222">www-data</span></span>

