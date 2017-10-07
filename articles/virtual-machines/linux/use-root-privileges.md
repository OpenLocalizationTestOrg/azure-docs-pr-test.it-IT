---
title: privilegi radice aaaUse nelle macchine virtuali Linux | Documenti Microsoft
description: Informazioni su come radice toouse privilegi in una macchina virtuale di Linux in Azure.
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
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="c2ecb-103">Uso di privilegi root su Linux in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c2ecb-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c2ecb-104">Per impostazione predefinita, hello `root` utente è disabilitato nelle macchine virtuali Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="c2ecb-105">Gli utenti possono eseguire i comandi con privilegi elevati tramite hello `sudo` comando.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="c2ecb-106">Tuttavia, esperienza hello può variare a seconda di come è stato eseguito il provisioning di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="c2ecb-107">**Chiave SSH e la password o solo** -macchina virtuale hello è stato eseguito il provisioning con un certificato (`.CER` file) o la chiave SSH, nonché una password, o semplicemente un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="c2ecb-108">In questo caso `sudo` richiederà la password dell'utente hello prima di eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="c2ecb-109">**Solo la chiave SSH** -macchina virtuale hello è stato eseguito il provisioning con un certificato (`.cer`, `.pem`, o `.pub` file) o la chiave SSH, ma senza password.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="c2ecb-110">In questo caso `sudo` **non** prompt dei comandi per la password dell'utente hello prima di eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="c2ecb-111">Chiave SSH e password o solo password</span><span class="sxs-lookup"><span data-stu-id="c2ecb-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="c2ecb-112">Accedere a una macchina virtuale di Linux hello utilizzando l'autenticazione con password o chiave SSH, quindi eseguire i comandi usando `sudo`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="c2ecb-113">In questo caso hello utente verrà richiesto di immettere una password.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="c2ecb-114">Dopo aver immesso la password di hello `sudo` verrà eseguito il comando hello con `root` privilegi.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="c2ecb-115">È inoltre possibile abilitare sudo passwordless modificando hello `/etc/sudoers.d/waagent` file, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="c2ecb-116">Questa modifica consentirà passwordless sudo utente hello "azureuser".</span><span class="sxs-lookup"><span data-stu-id="c2ecb-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="c2ecb-117">Solo chiave SSH</span><span class="sxs-lookup"><span data-stu-id="c2ecb-117">SSH Key Only</span></span>
<span data-ttu-id="c2ecb-118">Accedere a una macchina virtuale di Linux hello utilizzando l'autenticazione con chiave SSH, quindi eseguire i comandi usando `sudo`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="c2ecb-119">In questo caso utente hello verrà **non** chiesto di specificare una password.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="c2ecb-120">Dopo aver premuto `<enter>`, `sudo` verrà eseguito il comando hello con `root` privilegi.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

