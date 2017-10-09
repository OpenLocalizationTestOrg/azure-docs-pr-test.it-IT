---
title: password locale Linux aaaHow tooreset su macchine virtuali di Azure | Documenti Microsoft
description: Introdurre hello passaggi tooreset hello Linux password locale nella macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="5b79d-103">Come password Linux locale tooreset nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5b79d-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="5b79d-104">Questo articolo descrive le password di Linux macchina virtuale (VM) di diversi metodi tooreset locale.</span><span class="sxs-lookup"><span data-stu-id="5b79d-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="5b79d-105">Se l'account utente hello è scaduto o è toocreate un nuovo account, è possibile utilizzare hello seguenti metodi toocreate un nuovo account di amministratore locale e ottenere nuovamente accesso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5b79d-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="5b79d-106">Sintomi</span><span class="sxs-lookup"><span data-stu-id="5b79d-106">Symptoms</span></span>

<span data-ttu-id="5b79d-107">Non è possibile accedere toohello VM e viene visualizzato un messaggio che indica che la password hello utilizzato non è corretta.</span><span class="sxs-lookup"><span data-stu-id="5b79d-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="5b79d-108">Inoltre, è possibile utilizzare VMAgent tooreset la password nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5b79d-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="5b79d-109">Procedura di reimpostazione manuale della password</span><span class="sxs-lookup"><span data-stu-id="5b79d-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="5b79d-110">Eliminare hello VM e mantenere i dischi collegato hello.</span><span class="sxs-lookup"><span data-stu-id="5b79d-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="5b79d-111">Collegare l'unità del sistema operativo come una tooanother disco dati hello temporale macchina virtuale in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="5b79d-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="5b79d-112">Eseguire hello successivo comando SSH su hello temporale VM toobecome un utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="5b79d-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="5b79d-113">Eseguire **fdisk -l** o esaminare hello toofind i registri di sistema il disco appena collegato.</span><span class="sxs-lookup"><span data-stu-id="5b79d-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="5b79d-114">Individuare hello unità nome toomount.</span><span class="sxs-lookup"><span data-stu-id="5b79d-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="5b79d-115">Quindi in hello VM temporale, Cerca in hello rilevante file di log.</span><span class="sxs-lookup"><span data-stu-id="5b79d-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="5b79d-116">esempio Hello è riportato l'output del comando grep hello:</span><span class="sxs-lookup"><span data-stu-id="5b79d-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="5b79d-117">Creare un punto di montaggio denominato **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="5b79d-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="5b79d-118">Montare il disco di hello del sistema operativo nel punto di montaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5b79d-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="5b79d-119">In genere, è necessario toomount sdc1 o sdc2.</span><span class="sxs-lookup"><span data-stu-id="5b79d-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="5b79d-120">Questo dipende hello hosting partizione di directory /etc/hosts dal disco di macchina interrotti hello.</span><span class="sxs-lookup"><span data-stu-id="5b79d-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="5b79d-121">Eseguire un backup prima di apportare modifiche:</span><span class="sxs-lookup"><span data-stu-id="5b79d-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="5b79d-122">Reimpostare la password dell'utente hello che è necessario:</span><span class="sxs-lookup"><span data-stu-id="5b79d-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="5b79d-123">Spostamento hello modificati file toohello percorso corretto hello suddiviso disco della macchina.</span><span class="sxs-lookup"><span data-stu-id="5b79d-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="5b79d-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="5b79d-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
