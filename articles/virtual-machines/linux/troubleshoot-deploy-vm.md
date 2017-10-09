---
title: distribuzione di problemi di macchine virtuali Linux in Azure aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure con il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure

problemi relativi alla distribuzione di macchina virtuale (VM) tootroubleshoot in Azure, esaminare hello [problemi principali](#top-issues) per errori e le risoluzioni comuni.

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.

## <a name="top-issues"></a>Problemi principali
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>non supporta cluster Hello hello richiesto dimensioni delle macchine Virtuali
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.
- Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:
    - Arrestare tutte le macchine virtuali hello in set di disponibilità hello. Fare clic su **Gruppi di risorse** > il proprio gruppo di risorse > **Risorse** > il proprio set di disponibilità > **Macchine virtuali** > la propria macchina virtuale > **Arresta**.
    - Dopo che tutti hello arrestare le macchine virtuali, creare hello VM dimensioni hello desiderato.
    - Avviare hello prima nuova macchina virtuale e quindi selezionare hello arrestare le macchine virtuali e fare clic su Avvia.


## <a name="hello-cluster-does-not-have-free-resources"></a>cluster Hello privo di liberare le risorse
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Riprovare più tardi richiesta hello.
- Se hello nuova macchina virtuale è possibile essere incluso un diverso set di disponibilità
    - Creare una macchina virtuale in un set di disponibilità diverso (in hello stessa regione).
    - Aggiungere hello nuova VM toohello stessa rete virtuale.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Come attivare il credito mensile per Visual Studio Enterprise (BizSpark)

tooactivate la frequenza mensile del credito, vedere questo [articolo](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Motivo per cui è possibile non installare driver della GPU hello per una macchina virtuale NV Ubuntu?

Attualmente, il supporto per GPU Linux è disponibile solo sulle macchine virtuali NC di Azure che eseguono Ubuntu Server 16.04 LTS. Per altre informazioni, vedere [Configurare i driver GPU per le VM serie N che eseguono Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>I driver della VM serie N di Linux non sono disponibili

I driver per le macchine virtuali basate su Linux si trovano [qui](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Nella VM Serie N non è disponibile un'istanza GPU

tootake le funzionalità GPU hello di macchine virtuali di Azure serie N che esegue Windows Server 2016 o Windows Server 2012 R2, è necessario installare i driver grafici NVIDIA in ogni macchina virtuale dopo la distribuzione. Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](../windows/n-series-driver-setup.md) e le [VM Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Le VM Serie N sono disponibili nella mia area?

È possibile controllare la disponibilità di hello da hello [i prodotti disponibili dalla tabella region](https://azure.microsoft.com/regions/services), nonché i prezzi [qui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Non mi toosee in grado di famiglia di dimensioni della macchina virtuale che si desidera quando si ridimensiona la macchina virtuale.

Quando una macchina virtuale è in esecuzione, è server fisico tooa distribuito. i server fisici Hello in aree di Azure vengono raggruppati in cluster dell'hardware fisico comuni. Ridimensiona una macchina virtuale che richiede hello VM toobe spostato toodifferent hardware cluster è diversa a seconda di quale modello di distribuzione è stato utilizzato toodeploy hello macchina virtuale.

- Macchine virtuali distribuite nel modello di distribuzione classica, la distribuzione del servizio cloud hello devono essere rimossi e dimensioni di tooa toochange hello macchine virtuali in un altro gruppo di dimensioni di ridistribuzione.

- Macchine virtuali distribuite nel modello di distribuzione di gestione delle risorse, è necessario arrestare tutte le macchine virtuali in hello set di disponibilità prima modifica hello dimensioni di qualsiasi macchina virtuale nel set di disponibilità hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hello elencate dimensioni della macchina virtuale non sono supportata durante la distribuzione in Set di disponibilità.

Scegliere una dimensione è supportata in cluster del set di disponibilità hello. È consigliabile quando si crea che un gruppo di disponibilità toochoose hello più grande dimensioni delle macchine Virtuali si ritiene che e che il primo toohello distribuzione che set di disponibilità.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Quali distribuzioni/versioni di Linux sono supportate in Azure?

È possibile trovare l'elenco di hello in Linux nel [Azure-Endorsed distribuzioni](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>È possibile aggiungere un set di disponibilità tooan VM classico esistente?

Sì. È possibile aggiungere un classico esistente tooa macchina virtuale nuova o Set di disponibilità esistente. Per ulteriori informazioni vedere [aggiungere un set di disponibilità tooan macchina virtuale esistente](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Passaggi successivi
Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/).

In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.
