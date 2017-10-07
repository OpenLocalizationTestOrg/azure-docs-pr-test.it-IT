---
title: aaaVM il riavvio o problemi di ridimensionamento | Documenti Microsoft
description: Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure
> [!div class="op_single_selector"]
> * [Classico](restart-resize-error-troubleshooting.md)
> * [Gestione risorse](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

Quando si tenta di una macchina virtuale di Azure (VM) arrestata toostart, o si ridimensiona una macchina virtuale di Azure esistente, errore comune di hello che si verificano è un errore di allocazione. Questo errore si verifica quando cluster hello o area geografica non è risorse disponibili oppure non è supporto hello richiesto di dimensioni della macchina virtuale.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per la versione di gestione risorse di hello, vedere [qui](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Raccogliere log di controllo
toostart risoluzione dei problemi, controllo hello collect registra errore hello tooidentify associata hello problema.

Nel portale di Azure hello, fare clic su **Sfoglia** > **macchine virtuali** > *la macchina virtuale Linux*  >   **Impostazioni** > **log di controllo**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Errore durante l'avvio di una VM arrestata
Si tenta di toostart una macchina virtuale arrestata ma si otterrà un errore di allocazione.

### <a name="cause"></a>Causa
richiesta di Hello hello toostart arrestato VM ha toobe tentata al cluster originale hello che ospita il servizio cloud hello. Cluster hello è richiesta di spazio libero disponibile toofulfill hello.

### <a name="resolution"></a>Risoluzione
* Creare un nuovo servizio cloud e associarlo a un'area o una rete virtuale basata sull'area, ma non a un gruppo di affinità.
* Eliminare hello arrestato macchina virtuale.
* Ricreare hello macchina virtuale nel nuovo servizio cloud di hello usando dischi hello.
* Avviare hello ricreato macchina virtuale.

Se si verifica un errore durante il tentativo di toocreate un nuovo servizio cloud, riprovare in un secondo momento o modificare hello area per il servizio cloud hello.

> [!IMPORTANT]
> nuovo servizio cloud di Hello avrà un nuovo nome e l'indirizzo VIP, pertanto è necessario toochange tali informazioni per tutte le dipendenze di hello che utilizzano tali informazioni per il servizio cloud esistente hello.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: Errore durante il ridimensionamento di una VM esistente
Si tenta di tooresize una macchina virtuale esistente ma si otterrà un errore di allocazione.

### <a name="cause"></a>Causa
richiesta di Hello tooresize hello VM è toobe tentata al cluster originale hello servizio cloud hello host. Tuttavia, non supporta cluster hello hello richiesto dimensioni della macchina virtuale.

### <a name="resolution"></a>Risoluzione
Ridurre hello richiesto dimensioni della macchina virtuale e riprovare hello ridimensionare richiesta.

* Fare clic su **Esplora tutto** > **Macchine virtuali (classico)** > *la macchina virtuale* > **Impostazioni** > **Dimensioni**. Per informazioni dettagliate, vedere [ridimensionare una macchina virtuale hello](https://msdn.microsoft.com/library/dn168976.aspx).

Se non è possibile tooreduce hello dimensioni della macchina virtuale, seguire questi passaggi:

* Creare un nuovo servizio cloud, assicurandosi che non è collegato il gruppo di affinità tooan e non è associata a una rete virtuale che è il gruppo di affinità tooan collegato.
* Nel servizio creare una nuova VM con dimensioni maggiori.

È possibile consolidare tutte le macchine virtuali in hello stesso servizio cloud. Se il servizio cloud esistente è associato a una rete virtuale basata sull'area, è possibile connettersi hello nuovo cloud servizio toohello rete virtuale esistente.

Se il servizio cloud esistente di hello non è associato a una rete virtuale basata sull'area, quindi si hanno toodelete hello macchine virtuali nel servizio cloud esistente hello e ricrearle in hello nuovo servizio cloud dei dischi. Tuttavia, è importante tooremember che nuovo servizio cloud di hello avrà un nuovo nome e l'indirizzo VIP, pertanto sarà necessario tooupdate per tutte le dipendenze di hello che attualmente utilizzano queste informazioni per il servizio cloud esistente hello.

## <a name="next-steps"></a>Passaggi successivi
Se si verificano problemi durante la creazione di una nuova VM Linux in Azure, vedere [Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Linux in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

