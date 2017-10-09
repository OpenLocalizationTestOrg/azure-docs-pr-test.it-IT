---
title: distribuzione di VM Linux-RM aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi della distribuzione Resource Manager quando si crea una nuova macchina virtuale Linux in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Risolvere i problemi della distribuzione Resource Manager con la creazione di una nuova macchina virtuale Linux in Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Problemi principali
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Per altri problemi e domande sulla distribuzione delle VM, vedere [Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Raccogliere i log di attività
toostart risoluzione dei problemi, attività di raccolta hello registra errore hello tooidentify associata hello problema. Hello collegamenti riportati di seguito contengono informazioni dettagliate su hello processo toofollow.

[Visualizzare le operazioni di distribuzione](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Visualizzare toomanage log attività Azure le risorse](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** se hello del sistema operativo è generalizzato, Linux e viene caricato e/o acquisito con impostazione hello generalizzato, quindi non essere presenti gli eventuali errori. Analogamente, se hello del sistema operativo Linux specializzato, viene caricato e/o acquisito con hello specializzati impostazione, quindi non essere presenti gli eventuali errori.

**Errori di caricamento:**

**N<sup>1</sup>:** se hello del sistema operativo Linux generalizzato e questo viene caricato come specializzato, verrà generato un errore di timeout del provisioning poiché hello VM è bloccato in fase di provisioning hello.

**N<sup>2</sup>:** se hello del sistema operativo Linux specializzati e che è stato caricato come generalizzato, si otterrà un errore di provisioning perché hello nuova macchina virtuale è in esecuzione con il nome del computer originale di hello, username e password.

**Risoluzione:**

caricare entrambi questi errori, tooresolve hello VHD originale, disponibili in locale, con hello stessa impostazione come che per hello del sistema operativo (generalizzata o specializzata). tooupload come generalizzato, ricordare toorun-eseguire innanzitutto il deprovisioning.

**Errori di acquisizione:**

**N<sup>3</sup>:** se hello del sistema operativo Linux generalizzato e che viene acquisito come specializzato, verrà generato un errore di timeout del provisioning poiché hello originale VM non è utilizzabile in quanto è contrassegnato come generalizzato.

**N<sup>4</sup>:** se hello del sistema operativo Linux specializzati e che viene acquisito come generalizzato, si otterrà un errore di provisioning perché hello nuova macchina virtuale è in esecuzione con il nome del computer originale di hello, username e password. Inoltre, hello originale VM non è utilizzabile perché è contrassegnato come specializzate.

**Risoluzione:**

tooresolve entrambi questi errori, eliminare l'immagine corrente hello dal portale hello e [nuovamente acquisita da hello dischi rigidi virtuali correnti](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) con hello stessa impostazione di quello per hello del sistema operativo (generalizzata o specializzata).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Immagine personalizzata/della raccolta/del marketplace - errore di allocazione
Questo errore si verifica nelle situazioni quando hello nuova macchina virtuale richiesta cluster tooa bloccati che non è in grado di supportare dimensioni della macchina virtuale hello richieste, o non dispone di una richiesta di hello tooaccommodate di spazio libero.

**Causa 1:** cluster hello non è in grado di supportare hello richiesto dimensioni della macchina virtuale.

**Risoluzione 1:**

* Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.
* Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:
  * Arrestare tutte le macchine virtuali hello in set di disponibilità hello.
    Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.
  * Dopo tutte hello arrestare le macchine virtuali, creare hello nuova macchina virtuale in hello dimensioni desiderate.
  * Avviare hello prima nuova macchina virtuale e quindi selezionare hello arrestare le macchine virtuali e fare clic su **avviare**.

**Causa 2:** cluster hello privo di liberare risorse.

**Risoluzione 2:**

* Ripetere la richiesta hello in un secondo momento.
* Se hello nuova macchina virtuale è possibile essere incluso un diverso set di disponibilità
  * Creare una nuova macchina virtuale in un set di disponibilità diverso (in hello stessa regione).
  * Aggiungere hello nuova VM toohello stessa rete virtuale.

## <a name="next-steps"></a>Passaggi successivi
Se si incontrano problemi quando si avvia una VM Linux arrestata o si ridimensiona una VM Linux esistente in Azure, vedere [Risolvere i problemi della distribuzione di Resource Manager con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

