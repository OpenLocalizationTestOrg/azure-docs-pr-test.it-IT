---
title: Come reimpostare la password di Linux locale nelle VM di Azure | Microsoft Docs
description: Viene illustrata la procedura per reimpostare la password di Linux locale in una VM di Azure
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
ms.openlocfilehash: bd48128a078821b7a4baa02d5d7ceecc6de99608
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="d2761-103">Come reimpostare la password di Linux locale nelle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="d2761-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="d2761-104">Questo articolo illustra diversi metodi per reimpostare le password delle macchine virtuali (VM) di Linux locali.</span><span class="sxs-lookup"><span data-stu-id="d2761-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="d2761-105">Se l'account utente è scaduto o si vuole creare un nuovo account, è possibile usare i metodi seguenti per creare un nuovo account amministratore locale e riottenere l'accesso alla VM.</span><span class="sxs-lookup"><span data-stu-id="d2761-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="d2761-106">Sintomi</span><span class="sxs-lookup"><span data-stu-id="d2761-106">Symptoms</span></span>

<span data-ttu-id="d2761-107">Non è possibile accedere alla VM e viene visualizzato un messaggio indicante che la password usata non è corretta.</span><span class="sxs-lookup"><span data-stu-id="d2761-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="d2761-108">Inoltre non è possibile usare VMAgent per reimpostare la password nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2761-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="d2761-109">Procedura di reimpostazione manuale della password</span><span class="sxs-lookup"><span data-stu-id="d2761-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="d2761-110">Eliminare la VM e mantenere i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="d2761-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="d2761-111">Collegare l'unità del sistema operativo come disco dati a un'altra VM temporale nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="d2761-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="d2761-112">Usare il comando SSH seguente nella VM temporale per diventare utente con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="d2761-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="d2761-113">Eseguire **fdisk -l** o esaminare i log di sistema per trovare il nuovo disco collegato.</span><span class="sxs-lookup"><span data-stu-id="d2761-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="d2761-114">Trovare il nome dell'unità da montare,</span><span class="sxs-lookup"><span data-stu-id="d2761-114">Locate the drive name to mount.</span></span> <span data-ttu-id="d2761-115">quindi nella VM temporale esaminare il file di log pertinente.</span><span class="sxs-lookup"><span data-stu-id="d2761-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="d2761-116">Il seguente è l'output di esempio del comando grep:</span><span class="sxs-lookup"><span data-stu-id="d2761-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="d2761-117">Creare un punto di montaggio denominato **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="d2761-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="d2761-118">Montare il disco del sistema operativo nel punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="d2761-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="d2761-119">È in genere necessario montare sdc1 o sdc2</span><span class="sxs-lookup"><span data-stu-id="d2761-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="d2761-120">a seconda della partizione di hosting nella directory /etc del disco del computer danneggiato.</span><span class="sxs-lookup"><span data-stu-id="d2761-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="d2761-121">Eseguire un backup prima di apportare modifiche:</span><span class="sxs-lookup"><span data-stu-id="d2761-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="d2761-122">Reimpostare la password dell'utente necessaria:</span><span class="sxs-lookup"><span data-stu-id="d2761-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="d2761-123">Spostare i file modificati nella posizione corretta sul disco del computer danneggiato.</span><span class="sxs-lookup"><span data-stu-id="d2761-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="d2761-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="d2761-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)