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
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Uso di privilegi root su Linux in Macchine virtuali di Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Per impostazione predefinita, hello `root` utente è disabilitato nelle macchine virtuali Linux in Azure. Gli utenti possono eseguire i comandi con privilegi elevati tramite hello `sudo` comando. Tuttavia, esperienza hello può variare a seconda di come è stato eseguito il provisioning di sistema hello.

1. **Chiave SSH e la password o solo** -macchina virtuale hello è stato eseguito il provisioning con un certificato (`.CER` file) o la chiave SSH, nonché una password, o semplicemente un nome utente e password. In questo caso `sudo` richiederà la password dell'utente hello prima di eseguire il comando hello.
2. **Solo la chiave SSH** -macchina virtuale hello è stato eseguito il provisioning con un certificato (`.cer`, `.pem`, o `.pub` file) o la chiave SSH, ma senza password.  In questo caso `sudo` **non** prompt dei comandi per la password dell'utente hello prima di eseguire il comando hello.

## <a name="ssh-key-and-password-or-password-only"></a>Chiave SSH e password o solo password
Accedere a una macchina virtuale di Linux hello utilizzando l'autenticazione con password o chiave SSH, quindi eseguire i comandi usando `sudo`, ad esempio:

    # sudo <command>
    [sudo] password for azureuser:

In questo caso hello utente verrà richiesto di immettere una password. Dopo aver immesso la password di hello `sudo` verrà eseguito il comando hello con `root` privilegi.

È inoltre possibile abilitare sudo passwordless modificando hello `/etc/sudoers.d/waagent` file, ad esempio:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Questa modifica consentirà passwordless sudo utente hello "azureuser".

## <a name="ssh-key-only"></a>Solo chiave SSH
Accedere a una macchina virtuale di Linux hello utilizzando l'autenticazione con chiave SSH, quindi eseguire i comandi usando `sudo`, ad esempio:

    # sudo <command>

In questo caso utente hello verrà **non** chiesto di specificare una password. Dopo aver premuto `<enter>`, `sudo` verrà eseguito il comando hello con `root` privilegi.

