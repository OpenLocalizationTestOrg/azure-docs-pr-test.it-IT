---
title: distribuzione macchina virtuale Windows classica aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi della distribuzione classica quando si crea una nuova macchina virtuale Windows in Azure
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cjiang
ms.openlocfilehash: aa12cb013a18e0572fbef8b7ea69106dd47c1fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Windows in Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per la versione di hello Gestione risorse di questo articolo, vedere [qui](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Raccogliere log di controllo
toostart risoluzione dei problemi, controllo hello collect registra errore hello tooidentify associata hello problema.

Nel portale di Azure hello, fare clic su **Sfoglia** > **macchine virtuali** > *la macchina virtuale Windows*  >   **Impostazioni** > **log di controllo**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** se hello del sistema operativo è Windows generalizzato, viene caricato e/o acquisito con impostazione hello generalizzato, quindi non essere presenti gli eventuali errori. Analogamente, se hello del sistema operativo è Windows specializzati e viene caricato e/o acquisito con hello specializzati impostazione, quindi non essere presenti gli eventuali errori.

**Errori di caricamento:**

**N<sup>1</sup>:** se hello del sistema operativo è generalizzato di Windows e che è stato caricato come specializzato, si otterrà un errore di timeout di provisioning con hello VM bloccato nella schermata di configurazione guidata hello.

**N<sup>2</sup>:** se hello del sistema operativo è Windows specializzati e che è stato caricato come generalizzato, si otterrà un errore di provisioning con hello VM bloccato nella schermata di configurazione guidata hello perché hello nuova macchina virtuale è in esecuzione con computer originale hello nome, nome utente e password.

**Risoluzione:**

caricare entrambi questi errori, tooresolve hello VHD originale, disponibili in locale, con hello stessa impostazione come che per hello del sistema operativo (generalizzata o specializzata). tooupload come generalizzato, tenere presente che innanzitutto toorun sysprep. Vedere [creazione e caricamento di un disco rigido virtuale di Windows Server di tooAzure](createupload-vhd.md) per ulteriori informazioni.

**Errori di acquisizione:**

**N<sup>3</sup>:** se hello del sistema operativo è generalizzato di Windows e l'acquisizione come specializzato, verrà generato un errore di timeout del provisioning poiché hello originale VM non è utilizzabile in quanto è contrassegnato come generalizzato.

**N<sup>4</sup>:** se hello del sistema operativo è Windows specializzati e che viene acquisito come generalizzato, si otterrà un errore di provisioning perché hello nuova macchina virtuale è in esecuzione con il nome del computer originale di hello, username e password. Inoltre, hello originale VM non è utilizzabile perché è contrassegnato come specializzate.

**Risoluzione:**

tooresolve entrambi questi errori, eliminare l'immagine corrente hello dal portale hello e [nuovamente acquisita da hello dischi rigidi virtuali correnti](capture-image.md) con hello stessa impostazione di quello per hello del sistema operativo (generalizzata o specializzata).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Immagine personalizzata/della raccolta/del marketplace - errore di allocazione
Questo errore si verifica nelle situazioni hello nuova VM inviata tooa cluster che non è richiesta hello tooaccommodate di spazio libero disponibile, o non è in grado di supportare dimensioni della macchina virtuale hello richiesta. Non è possibile toomix diverse serie di macchine virtuali in hello stesso servizio cloud. Pertanto, se si desidera toocreate una nuova macchina virtuale di dimensioni diverse rispetto a ciò che può supportare il servizio cloud, hello calcolo richiesta avrà esito negativo.

In base ai vincoli del servizio cloud hello hello è utilizzare toocreate hello nuova macchina virtuale, potrebbe verificarsi un errore causato da uno dei due situazioni.

**Causa 1:** servizio cloud hello è cluster specifico tooa bloccato o è il gruppo di affinità collegati tooan e pertanto bloccata tooa cluster specifico in base alla progettazione. In modo da richieste di nuove risorse di calcolo in quel gruppo di affinità vengono tentati in hello stesso cluster ospitate risorse esistenti hello. Tuttavia, hello dello stesso cluster potrebbe non hello supporto richiesto dimensioni delle macchine Virtuali o dispone di sufficiente spazio disponibile, causando un errore di allocazione. È true se le nuove risorse hello vengono create tramite un nuovo servizio cloud o un servizio cloud esistente.

**Risoluzione 1:**

* Creare un nuovo servizio cloud e associarlo a un'area o una rete virtuale basata sull'area.
* Creare una nuova macchina virtuale nel nuovo servizio cloud di hello.
  Se si verifica un errore durante il tentativo di toocreate un nuovo servizio cloud, riprovare in un secondo momento o modificare hello area per il servizio cloud hello.

> [!IMPORTANT]
> Se si sta tentando di toocreate una nuova macchina virtuale in un servizio cloud esistente ma non è stato e stato toocreate un nuovo servizio cloud per la nuova macchina virtuale, è possibile scegliere tooconsolidate tutte le macchine virtuali in hello stesso servizio cloud. toodo in tal caso, eliminare le macchine virtuali hello nel servizio cloud esistente hello e li riacquisire dei dischi nel nuovo servizio cloud di hello. Tuttavia, è importante tooremember che nuovo servizio cloud di hello avrà un nuovo nome e l'indirizzo VIP, pertanto sarà necessario tooupdate per tutte le dipendenze di hello che attualmente utilizzano queste informazioni per il servizio cloud esistente hello.
> 
> 

**Causa 2:** servizio cloud hello è associata a una rete virtuale è collegato tooan gruppo di affinità, pertanto è bloccato tooa cluster specifico in base alla progettazione. Tutte le nuove richieste di risorse di calcolo in tale gruppo di affinità vengono pertanto tentate in hello stesso cluster ospitate risorse esistenti hello. Tuttavia, hello dello stesso cluster potrebbe non hello supporto richiesto dimensioni delle macchine Virtuali o dispone di sufficiente spazio disponibile, causando un errore di allocazione. È true se le nuove risorse hello vengono create tramite un nuovo servizio cloud o un servizio cloud esistente.

**Risoluzione 2:**

* Crea una nuova rete virtuale a livello di area
* Crea nuova macchina virtuale in una nuova rete virtuale hello hello.
* [Connettere la rete virtuale esistente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nuova rete virtuale. Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). In alternativa, è possibile [eseguire la migrazione della rete virtuale regionale rete virtuale basato su gruppo di affinità tooa](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e quindi creare hello nuova macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi
Se si incontrano problemi quando si avvia una VM Windows arrestata o si ridimensiona una VM Windows esistente in Azure, vedere l'articolo su come [risolvere i problemi della distribuzione classica con il riavvio o il ridimensionamento di una macchina virtuale Windows esistente in Azure](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).

