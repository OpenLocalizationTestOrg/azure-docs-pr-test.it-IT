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
# <a name="selecting-user-names-for-linux-on-azure"></a>Selezione dei nomi utente per Linux su Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Quando si esegue il provisioning di una macchina virtuale di Linux in Azure è necessario specificare il nome di hello di un utente non radice che è possibile utilizzare in un secondo momento toolog in hello macchina virtuale. È possibile scegliere il nome di hello del nuovo utente hello o se il provisioning tramite hello portale di Azure classico è possibile accettare predefinito hello azureuser"nome".

Nella maggior parte dei casi l'utente non esiste nell'immagine di base hello e verrà creato durante il processo di provisioning hello. Se l'utente di hello presente su immagine di macchina virtuale di base hello, agente Linux di Azure hello semplicemente configura quindi password hello e/o la chiave SSH per l'utente in base alle informazioni di hello specificata durante la creazione di hello macchina virtuale.

**Tuttavia**, Linux definisce un set di nomi utente che non devono essere usati. Hello provisioning processo verrà **esito negativo** se si tenta di tooprovision una VM Linux di un utente di sistema esistente, è definito come un utente con UID 0 e 99. Un esempio tipico è hello `root` utente, che ha UID 0.

* Vedere anche: [Base standard di Linux - Intervalli ID utente](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

di seguito Hello è un elenco di utenti di sistema predefinito comune per CentOS e Ubuntu deve evitare di utilizzare durante il provisioning di una macchina virtuale di Linux in Azure. Questo elenco è solo un esempio, fare riferimento toohello documentazione per la distribuzione tooensure hello nome utente desiderato non è in conflitto con un utente di sistema esistente.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

