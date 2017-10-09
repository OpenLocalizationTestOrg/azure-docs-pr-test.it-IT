---
title: nome di dominio completo per una VM Linux nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un nome di dominio completo o nome di dominio completo per un gestore di risorse basato su macchina virtuale nel portale di Azure hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Creare un nome di dominio completo nel portale di Azure hello per una VM Linux

Quando si crea una macchina virtuale (VM) in hello [portale di Azure](https://portal.azure.com), viene creata automaticamente una risorsa IP pubblica per la macchina virtuale hello. Utilizzare questo hello di accesso tooremotely indirizzo IP VM. Anche se il portale di hello non crea un [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o nome di dominio completo, è possibile aggiungere uno dopo hello viene creata la VM. Questo articolo illustra hello passaggi toocreate un nome DNS o il nome FQDN.

## <a name="create-a-fqdn"></a>Creare un nome di dominio completo
In questo articolo si presuppone che sia già stata creata una VM. Se necessario, è possibile [creare una macchina virtuale nel portale di hello](quick-create-portal.md) o [con hello Azure CLI](quick-create-cli.md). Dopo che la macchina virtuale è operativa, seguire questi passaggi:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

È ora possibile connettersi in remoto toohello nome di macchina virtuale che utilizza questo server DNS, ad esempio con `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Passaggi successivi
Quando la macchina virtuale ha un indirizzo IP pubblico e un nome DNS, è possibile distribuire framework applicazioni o servizi comuni, ad esempio nginx, MongoDB, Docker e così via.

Per suggerimenti sulla creazione di distribuzioni di Azure, vedere la pagina relativa all'[uso di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

