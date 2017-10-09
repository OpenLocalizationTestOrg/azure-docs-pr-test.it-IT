---
title: una macchina virtuale Linux classico utilizzando aaaCreate hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come una macchina virtuale Linux con hello Azure CLI 1.0 toocreate hello modello di distribuzione classica
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Come tooCreate un classico VM Linux con hello Azure CLI 1.0
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per la versione di gestione risorse di hello, vedere [qui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In questo argomento viene descritto come una macchina virtuale Linux (VM) con hello Azure CLI 1.0 toocreate hello modello di distribuzione classica. Viene usata un'immagine Linux da hello disponibile **immagini** in Azure. i comandi CLI di Azure 1.0 Hello offrono hello opzioni di configurazione, tra gli altri seguenti:

* La connessione di rete virtuale di hello VM tooa
* Aggiungere il servizio cloud esistente di hello VM tooan
* Aggiunta di hello VM tooan account di archiviazione esistente
* Aggiunta di set di disponibilità tooan VM hello o percorso

> [!IMPORTANT]
> Se si desidera il toouse VM una rete virtuale per la connessione tooit direttamente dal nome host o configurare connessioni cross-premise, assicurarsi di che specificare la rete virtuale hello quando si crea hello macchina virtuale. Una macchina virtuale può essere toojoin configurata una rete virtuale solo quando si crea hello macchina virtuale. Per informazioni dettagliate sulle reti virtuali, vedere [Panoramica di Rete virtuale](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Come toocreate una VM Linux utilizzando hello modello di distribuzione classica
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

