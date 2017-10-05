---
title: Usare i privilegi root in macchine virtuali Linux | Microsoft Docs
description: Informazioni su come usare i privilegi root in una macchina virtuale Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="7f5d7-103">Uso di privilegi root su Linux in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7f5d7-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7f5d7-104">Per impostazione predefinita, l'utente `root` è disabilitato nelle macchine virtuali Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="7f5d7-105">Gli utenti possono eseguire comandi con privilegi elevati usando il comando `sudo` .</span><span class="sxs-lookup"><span data-stu-id="7f5d7-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="7f5d7-106">L'esperienza può tuttavia variare in base alla modalità usata per il provisioning del sistema.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="7f5d7-107">**Chiave SSH e password o solo password**: il provisioning della macchina virtuale è stato effettuato con un certificato (file `.CER`) o una chiave SSH e con una password oppure solo con un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="7f5d7-108">In questo caso `sudo` richiederà la password dell'utente prima di eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="7f5d7-109">**Solo chiave SSH**: il provisioning della macchina virtuale è stato effettuato con un certificato (file `.cer`, `.pem` o `.pub`) o una chiave SSH, ma senza password.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="7f5d7-110">In questo caso `sudo` **non** richiederà la password dell'utente prima di eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="7f5d7-111">Chiave SSH e password o solo password</span><span class="sxs-lookup"><span data-stu-id="7f5d7-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="7f5d7-112">Accedere alla macchina virtuale Linux usando l'autenticazione con chiave SSH o password, quindi eseguire i comandi tramite `sudo`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7f5d7-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="7f5d7-113">In questo caso, all'utente verrà richiesta una password.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="7f5d7-114">Dopo avere immesso la password `sudo` eseguirà il comando con privilegi `root`.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="7f5d7-115">È anche possibile abilitare sudo senza password modificando il file `/etc/sudoers.d/waagent` , ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7f5d7-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="7f5d7-116">Questa modifica permetterà all'utente azureuser di usare sudo senza password.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="7f5d7-117">Solo chiave SSH</span><span class="sxs-lookup"><span data-stu-id="7f5d7-117">SSH Key Only</span></span>
<span data-ttu-id="7f5d7-118">Accedere alla macchina virtuale Linux usando l'autenticazione con chiave SSH, quindi eseguire i comandi tramite `sudo`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7f5d7-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="7f5d7-119">In questo caso, all'utente **non** verrà richiesta una password.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="7f5d7-120">Dopo aver premuto `<enter>`, `sudo` eseguirà il comando con privilegi `root`.</span><span class="sxs-lookup"><span data-stu-id="7f5d7-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>

