---
title: aaaInstall MongoDB in una macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni su come creare i tooinstall MongoDB in una macchina virtuale di Azure con il modello di distribuzione classica hello che esegue Windows Server.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Installare MongoDB in una VM Windows in Azure
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. tooinstall e configurare MongoDB mediante modello di distribuzione di gestione risorse di hello, vedere [questo articolo](../install-mongodb.md).

[MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate. In questo articolo viene descritta la creazione di una macchina virtuale Windows Server (VM) hello [portale di Azure][AzurePortal]. Creare e collegare un toohello disco dati VM prima dell'installazione e configurazione di MongoDB. Se si dispone di una macchina virtuale esistente in cui si desidera toouse Azure, è possibile passare direttamente troppo[installazione e configurazione di MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Creare una macchina virtuale che esegue Windows Server
Seguire questi toocreate istruzioni una macchina virtuale.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> È possibile aggiungere un endpoint per MongoDB durante la creazione della macchina virtuale hello e configurarlo come segue: il nome come **Mongo**, utilizzare **TCP** come protocollo di hello e impostare entrambi hello porte pubbliche e private troppo**27017**.
>
>

## <a name="attach-a-data-disk"></a>Collegamento di un disco dati
archiviazione tooprovide per la macchina virtuale hello, collegare un disco dati e quindi inizializzarlo in modo che Windows è possibile utilizzarlo. È possibile collegare un eventuale disco dati esistente o collegare un disco vuoto.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Per istruzioni sull'inizializzazione di hello disco, vedere "procedura: inizializzare un nuovo disco dati in Windows Server" in [come tooattach dati disco macchina virtuale di Windows tooa](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Installare ed eseguire MongoDB sulla macchina virtuale hello
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Riepilogo
In questa esercitazione è stato come toocreate una macchina virtuale che esegue Windows Server, in modalità remota connettersi tooit e collegare un disco dati.  È inoltre appreso tooinstall e configurare MongoDB nella macchina virtuale basato su Windows hello. È ora possibile accedere MongoDB sulla macchina virtuale basato su Windows hello, da seguenti hello avanzata nel hello [documentazione di MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

