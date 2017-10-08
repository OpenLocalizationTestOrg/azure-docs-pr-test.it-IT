---
title: aaaVM il riavvio o il ridimensionamento dei problemi in Azure | Documenti Microsoft
description: Risolvere i problemi della distribuzione Resource Manager con il riavvio e il ridimensionamento di una macchina virtuale Windows esistente in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a>Risolvere i problemi di distribuzione con il riavvio o il ridimensionamento di una VM Windows esistente in Azure
Quando si tenta di una macchina virtuale di Azure (VM) arrestata toostart, o si ridimensiona una macchina virtuale di Azure esistente, errore comune di hello che si verificano è un errore di allocazione. Questo errore si verifica quando cluster hello o area geografica non è risorse disponibili oppure non è supporto hello richiesto di dimensioni della macchina virtuale.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Raccogliere i log di attività
toostart risoluzione dei problemi, attività di raccolta hello registra errore hello tooidentify associata hello problema. Hello seguenti collegamenti contenga informazioni dettagliate sul processo hello:

[Visualizzare le operazioni di distribuzione](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Visualizzare toomanage log attività Azure le risorse](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Errore durante l'avvio di una VM arrestata
Si tenta di toostart una macchina virtuale arrestata ma si otterrà un errore di allocazione.

### <a name="cause"></a>Causa
richiesta di Hello hello toostart arrestato VM ha toobe tentata al cluster originale hello che ospita il servizio cloud hello. Cluster hello è richiesta di spazio libero disponibile toofulfill hello.

### <a name="resolution"></a>Risoluzione
* Arrestare hello tutte le macchine virtuali in disponibilità hello set e quindi riavviare ogni macchina virtuale.
  
  1. Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.
  2. Dopo che tutti hello arrestare le macchine virtuali, selezionare hello arrestare le macchine virtuali e fare clic su Avvia.
* Ripetere la richiesta di riavvio hello in un secondo momento.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: Errore durante il ridimensionamento di una VM esistente
Si tenta di tooresize una macchina virtuale esistente ma si otterrà un errore di allocazione.

### <a name="cause"></a>Causa
richiesta di Hello tooresize hello VM è toobe tentata al cluster originale hello servizio cloud hello host. Tuttavia, non supporta cluster hello hello richiesto dimensioni della macchina virtuale.

### <a name="resolution"></a>Risoluzione
* Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.
* Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:
  
  1. Arrestare tutte le macchine virtuali hello in set di disponibilità hello.
     
     * Fare clic su **Gruppi di risorse** > *gruppo di risorse personale* > **Risorse** > *set di disponibilità personale* > **Macchine virtuali** > *macchina virtuale personale* > **Arresta**.
  2. Dopo che tutti hello arrestare le macchine virtuali, ridimensionare hello desiderato VM tooa maggiori dimensioni.
  3. Seleziona hello ridimensionato macchina virtuale e fare clic su **avviare**, e quindi avviare ogni di hello arrestato macchine virtuali.

## <a name="next-steps"></a>Passaggi successivi
Se si verificano problemi durante la creazione di una nuova VM Windows in Azure, vedere [Risolvere i problemi della distribuzione Resource Manager con la creazione di una nuova macchina virtuale Windows in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

