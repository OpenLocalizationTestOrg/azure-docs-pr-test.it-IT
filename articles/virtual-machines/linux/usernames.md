---
title: i nomi utente di Linux aaaSelecting | Documenti Microsoft
description: Informazioni su come utente tooselect nomi per una macchina virtuale di Linux in Azure.
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
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="6eea3-103">Selezione dei nomi utente per Linux su Azure</span><span class="sxs-lookup"><span data-stu-id="6eea3-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="6eea3-104">Quando si esegue il provisioning di una macchina virtuale di Linux in Azure è necessario specificare il nome di hello di un utente non radice che è possibile utilizzare in un secondo momento toolog in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6eea3-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="6eea3-105">È possibile scegliere il nome di hello del nuovo utente hello o se il provisioning tramite hello portale di Azure classico è possibile accettare predefinito hello azureuser"nome".</span><span class="sxs-lookup"><span data-stu-id="6eea3-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="6eea3-106">Nella maggior parte dei casi l'utente non esiste nell'immagine di base hello e verrà creato durante il processo di provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="6eea3-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="6eea3-107">Se l'utente di hello presente su immagine di macchina virtuale di base hello, agente Linux di Azure hello semplicemente configura quindi password hello e/o la chiave SSH per l'utente in base alle informazioni di hello specificata durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6eea3-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="6eea3-108">**Tuttavia**, Linux definisce un set di nomi utente che non devono essere usati.</span><span class="sxs-lookup"><span data-stu-id="6eea3-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="6eea3-109">Hello provisioning processo verrà **esito negativo** se si tenta di tooprovision una VM Linux di un utente di sistema esistente, è definito come un utente con UID 0 e 99.</span><span class="sxs-lookup"><span data-stu-id="6eea3-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="6eea3-110">Un esempio tipico è hello `root` utente, che ha UID 0.</span><span class="sxs-lookup"><span data-stu-id="6eea3-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="6eea3-111">Vedere anche: [Base standard di Linux - Intervalli ID utente](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="6eea3-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="6eea3-112">di seguito Hello è un elenco di utenti di sistema predefinito comune per CentOS e Ubuntu deve evitare di utilizzare durante il provisioning di una macchina virtuale di Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="6eea3-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="6eea3-113">Questo elenco è solo un esempio, fare riferimento toohello documentazione per la distribuzione tooensure hello nome utente desiderato non è in conflitto con un utente di sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="6eea3-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="6eea3-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="6eea3-114">CentOS</span></span>
* <span data-ttu-id="6eea3-115">abrt</span><span class="sxs-lookup"><span data-stu-id="6eea3-115">abrt</span></span>
* <span data-ttu-id="6eea3-116">adm</span><span class="sxs-lookup"><span data-stu-id="6eea3-116">adm</span></span>
* <span data-ttu-id="6eea3-117">audio</span><span class="sxs-lookup"><span data-stu-id="6eea3-117">audio</span></span>
* <span data-ttu-id="6eea3-118">bin</span><span class="sxs-lookup"><span data-stu-id="6eea3-118">bin</span></span>
* <span data-ttu-id="6eea3-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="6eea3-119">cdrom</span></span>
* <span data-ttu-id="6eea3-120">cgred</span><span class="sxs-lookup"><span data-stu-id="6eea3-120">cgred</span></span>
* <span data-ttu-id="6eea3-121">daemon</span><span class="sxs-lookup"><span data-stu-id="6eea3-121">daemon</span></span>
* <span data-ttu-id="6eea3-122">dbus</span><span class="sxs-lookup"><span data-stu-id="6eea3-122">dbus</span></span>
* <span data-ttu-id="6eea3-123">dialout</span><span class="sxs-lookup"><span data-stu-id="6eea3-123">dialout</span></span>
* <span data-ttu-id="6eea3-124">dip</span><span class="sxs-lookup"><span data-stu-id="6eea3-124">dip</span></span>
* <span data-ttu-id="6eea3-125">disk</span><span class="sxs-lookup"><span data-stu-id="6eea3-125">disk</span></span>
* <span data-ttu-id="6eea3-126">floppy</span><span class="sxs-lookup"><span data-stu-id="6eea3-126">floppy</span></span>
* <span data-ttu-id="6eea3-127">ftp</span><span class="sxs-lookup"><span data-stu-id="6eea3-127">ftp</span></span>
* <span data-ttu-id="6eea3-128">ftp</span><span class="sxs-lookup"><span data-stu-id="6eea3-128">ftp</span></span>
* <span data-ttu-id="6eea3-129">games</span><span class="sxs-lookup"><span data-stu-id="6eea3-129">games</span></span>
* <span data-ttu-id="6eea3-130">gopher</span><span class="sxs-lookup"><span data-stu-id="6eea3-130">gopher</span></span>
* <span data-ttu-id="6eea3-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="6eea3-131">haldaemon</span></span>
* <span data-ttu-id="6eea3-132">halt</span><span class="sxs-lookup"><span data-stu-id="6eea3-132">halt</span></span>
* <span data-ttu-id="6eea3-133">kmem</span><span class="sxs-lookup"><span data-stu-id="6eea3-133">kmem</span></span>
* <span data-ttu-id="6eea3-134">lock</span><span class="sxs-lookup"><span data-stu-id="6eea3-134">lock</span></span>
* <span data-ttu-id="6eea3-135">lp</span><span class="sxs-lookup"><span data-stu-id="6eea3-135">lp</span></span>
* <span data-ttu-id="6eea3-136">mail</span><span class="sxs-lookup"><span data-stu-id="6eea3-136">mail</span></span>
* <span data-ttu-id="6eea3-137">man</span><span class="sxs-lookup"><span data-stu-id="6eea3-137">man</span></span>
* <span data-ttu-id="6eea3-138">mem</span><span class="sxs-lookup"><span data-stu-id="6eea3-138">mem</span></span>
* <span data-ttu-id="6eea3-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="6eea3-139">nfsnobody</span></span>
* <span data-ttu-id="6eea3-140">nobody</span><span class="sxs-lookup"><span data-stu-id="6eea3-140">nobody</span></span>
* <span data-ttu-id="6eea3-141">ntp</span><span class="sxs-lookup"><span data-stu-id="6eea3-141">ntp</span></span>
* <span data-ttu-id="6eea3-142">operator</span><span class="sxs-lookup"><span data-stu-id="6eea3-142">operator</span></span>
* <span data-ttu-id="6eea3-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="6eea3-143">oprofile</span></span>
* <span data-ttu-id="6eea3-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="6eea3-144">postdrop</span></span>
* <span data-ttu-id="6eea3-145">postfix</span><span class="sxs-lookup"><span data-stu-id="6eea3-145">postfix</span></span>
* <span data-ttu-id="6eea3-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="6eea3-146">qpidd</span></span>
* <span data-ttu-id="6eea3-147">root</span><span class="sxs-lookup"><span data-stu-id="6eea3-147">root</span></span>
* <span data-ttu-id="6eea3-148">rpc</span><span class="sxs-lookup"><span data-stu-id="6eea3-148">rpc</span></span>
* <span data-ttu-id="6eea3-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="6eea3-149">rpcuser</span></span>
* <span data-ttu-id="6eea3-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="6eea3-150">saslauth</span></span>
* <span data-ttu-id="6eea3-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="6eea3-151">shutdown</span></span>
* <span data-ttu-id="6eea3-152">slocate</span><span class="sxs-lookup"><span data-stu-id="6eea3-152">slocate</span></span>
* <span data-ttu-id="6eea3-153">sshd</span><span class="sxs-lookup"><span data-stu-id="6eea3-153">sshd</span></span>
* <span data-ttu-id="6eea3-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="6eea3-154">stapdev</span></span>
* <span data-ttu-id="6eea3-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="6eea3-155">stapusr</span></span>
* <span data-ttu-id="6eea3-156">sync</span><span class="sxs-lookup"><span data-stu-id="6eea3-156">sync</span></span>
* <span data-ttu-id="6eea3-157">sys</span><span class="sxs-lookup"><span data-stu-id="6eea3-157">sys</span></span>
* <span data-ttu-id="6eea3-158">tape</span><span class="sxs-lookup"><span data-stu-id="6eea3-158">tape</span></span>
* <span data-ttu-id="6eea3-159">test</span><span class="sxs-lookup"><span data-stu-id="6eea3-159">test</span></span>
* <span data-ttu-id="6eea3-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="6eea3-160">tcpdump</span></span>
* <span data-ttu-id="6eea3-161">tty</span><span class="sxs-lookup"><span data-stu-id="6eea3-161">tty</span></span>
* <span data-ttu-id="6eea3-162">users</span><span class="sxs-lookup"><span data-stu-id="6eea3-162">users</span></span>
* <span data-ttu-id="6eea3-163">utempter</span><span class="sxs-lookup"><span data-stu-id="6eea3-163">utempter</span></span>
* <span data-ttu-id="6eea3-164">utmp</span><span class="sxs-lookup"><span data-stu-id="6eea3-164">utmp</span></span>
* <span data-ttu-id="6eea3-165">uucp</span><span class="sxs-lookup"><span data-stu-id="6eea3-165">uucp</span></span>
* <span data-ttu-id="6eea3-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="6eea3-166">vcsa</span></span>
* <span data-ttu-id="6eea3-167">video</span><span class="sxs-lookup"><span data-stu-id="6eea3-167">video</span></span>
* <span data-ttu-id="6eea3-168">wheel</span><span class="sxs-lookup"><span data-stu-id="6eea3-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="6eea3-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6eea3-169">Ubuntu</span></span>
* <span data-ttu-id="6eea3-170">adm</span><span class="sxs-lookup"><span data-stu-id="6eea3-170">adm</span></span>
* <span data-ttu-id="6eea3-171">admin</span><span class="sxs-lookup"><span data-stu-id="6eea3-171">admin</span></span>
* <span data-ttu-id="6eea3-172">audio</span><span class="sxs-lookup"><span data-stu-id="6eea3-172">audio</span></span>
* <span data-ttu-id="6eea3-173">backup</span><span class="sxs-lookup"><span data-stu-id="6eea3-173">backup</span></span>
* <span data-ttu-id="6eea3-174">bin</span><span class="sxs-lookup"><span data-stu-id="6eea3-174">bin</span></span>
* <span data-ttu-id="6eea3-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="6eea3-175">cdrom</span></span>
* <span data-ttu-id="6eea3-176">crontab</span><span class="sxs-lookup"><span data-stu-id="6eea3-176">crontab</span></span>
* <span data-ttu-id="6eea3-177">daemon</span><span class="sxs-lookup"><span data-stu-id="6eea3-177">daemon</span></span>
* <span data-ttu-id="6eea3-178">dialout</span><span class="sxs-lookup"><span data-stu-id="6eea3-178">dialout</span></span>
* <span data-ttu-id="6eea3-179">dip</span><span class="sxs-lookup"><span data-stu-id="6eea3-179">dip</span></span>
* <span data-ttu-id="6eea3-180">disk</span><span class="sxs-lookup"><span data-stu-id="6eea3-180">disk</span></span>
* <span data-ttu-id="6eea3-181">fax</span><span class="sxs-lookup"><span data-stu-id="6eea3-181">fax</span></span>
* <span data-ttu-id="6eea3-182">floppy</span><span class="sxs-lookup"><span data-stu-id="6eea3-182">floppy</span></span>
* <span data-ttu-id="6eea3-183">fuse</span><span class="sxs-lookup"><span data-stu-id="6eea3-183">fuse</span></span>
* <span data-ttu-id="6eea3-184">games</span><span class="sxs-lookup"><span data-stu-id="6eea3-184">games</span></span>
* <span data-ttu-id="6eea3-185">gnats</span><span class="sxs-lookup"><span data-stu-id="6eea3-185">gnats</span></span>
* <span data-ttu-id="6eea3-186">irc</span><span class="sxs-lookup"><span data-stu-id="6eea3-186">irc</span></span>
* <span data-ttu-id="6eea3-187">kmem</span><span class="sxs-lookup"><span data-stu-id="6eea3-187">kmem</span></span>
* <span data-ttu-id="6eea3-188">landscape</span><span class="sxs-lookup"><span data-stu-id="6eea3-188">landscape</span></span>
* <span data-ttu-id="6eea3-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="6eea3-189">libuuid</span></span>
* <span data-ttu-id="6eea3-190">list</span><span class="sxs-lookup"><span data-stu-id="6eea3-190">list</span></span>
* <span data-ttu-id="6eea3-191">lp</span><span class="sxs-lookup"><span data-stu-id="6eea3-191">lp</span></span>
* <span data-ttu-id="6eea3-192">mail</span><span class="sxs-lookup"><span data-stu-id="6eea3-192">mail</span></span>
* <span data-ttu-id="6eea3-193">man</span><span class="sxs-lookup"><span data-stu-id="6eea3-193">man</span></span>
* <span data-ttu-id="6eea3-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="6eea3-194">messagebus</span></span>
* <span data-ttu-id="6eea3-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="6eea3-195">mlocate</span></span>
* <span data-ttu-id="6eea3-196">netdev</span><span class="sxs-lookup"><span data-stu-id="6eea3-196">netdev</span></span>
* <span data-ttu-id="6eea3-197">news</span><span class="sxs-lookup"><span data-stu-id="6eea3-197">news</span></span>
* <span data-ttu-id="6eea3-198">nobody</span><span class="sxs-lookup"><span data-stu-id="6eea3-198">nobody</span></span>
* <span data-ttu-id="6eea3-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="6eea3-199">nogroup</span></span>
* <span data-ttu-id="6eea3-200">operator</span><span class="sxs-lookup"><span data-stu-id="6eea3-200">operator</span></span>
* <span data-ttu-id="6eea3-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="6eea3-201">plugdev</span></span>
* <span data-ttu-id="6eea3-202">proxy</span><span class="sxs-lookup"><span data-stu-id="6eea3-202">proxy</span></span>
* <span data-ttu-id="6eea3-203">root</span><span class="sxs-lookup"><span data-stu-id="6eea3-203">root</span></span>
* <span data-ttu-id="6eea3-204">sasl</span><span class="sxs-lookup"><span data-stu-id="6eea3-204">sasl</span></span>
* <span data-ttu-id="6eea3-205">shadow</span><span class="sxs-lookup"><span data-stu-id="6eea3-205">shadow</span></span>
* <span data-ttu-id="6eea3-206">src</span><span class="sxs-lookup"><span data-stu-id="6eea3-206">src</span></span>
* <span data-ttu-id="6eea3-207">ssh</span><span class="sxs-lookup"><span data-stu-id="6eea3-207">ssh</span></span>
* <span data-ttu-id="6eea3-208">sshd</span><span class="sxs-lookup"><span data-stu-id="6eea3-208">sshd</span></span>
* <span data-ttu-id="6eea3-209">staff</span><span class="sxs-lookup"><span data-stu-id="6eea3-209">staff</span></span>
* <span data-ttu-id="6eea3-210">sudo</span><span class="sxs-lookup"><span data-stu-id="6eea3-210">sudo</span></span>
* <span data-ttu-id="6eea3-211">sync</span><span class="sxs-lookup"><span data-stu-id="6eea3-211">sync</span></span>
* <span data-ttu-id="6eea3-212">sys</span><span class="sxs-lookup"><span data-stu-id="6eea3-212">sys</span></span>
* <span data-ttu-id="6eea3-213">syslog</span><span class="sxs-lookup"><span data-stu-id="6eea3-213">syslog</span></span>
* <span data-ttu-id="6eea3-214">tape</span><span class="sxs-lookup"><span data-stu-id="6eea3-214">tape</span></span>
* <span data-ttu-id="6eea3-215">tty</span><span class="sxs-lookup"><span data-stu-id="6eea3-215">tty</span></span>
* <span data-ttu-id="6eea3-216">users</span><span class="sxs-lookup"><span data-stu-id="6eea3-216">users</span></span>
* <span data-ttu-id="6eea3-217">utmp</span><span class="sxs-lookup"><span data-stu-id="6eea3-217">utmp</span></span>
* <span data-ttu-id="6eea3-218">uucp</span><span class="sxs-lookup"><span data-stu-id="6eea3-218">uucp</span></span>
* <span data-ttu-id="6eea3-219">video</span><span class="sxs-lookup"><span data-stu-id="6eea3-219">video</span></span>
* <span data-ttu-id="6eea3-220">voice</span><span class="sxs-lookup"><span data-stu-id="6eea3-220">voice</span></span>
* <span data-ttu-id="6eea3-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="6eea3-221">whoopsie</span></span>
* <span data-ttu-id="6eea3-222">www-data</span><span class="sxs-lookup"><span data-stu-id="6eea3-222">www-data</span></span>

