---
title: aaaEnable o la disabilitazione di macchina virtuale di Azure Monitoring
description: Viene descritto come tooEnable o disabilitare il monitoraggio di macchina virtuale Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Abilitare o disabilitare il monitoraggio delle VM di Azure

In questa sezione viene descritto come tooenable o disabilitare il monitoraggio su virtuale dei computer in esecuzione in Azure. È possibile abilitare o disabilitare il monitoraggio tramite il portale di hello o interfaccia della riga di comando di Azure per Mac, Linux e Windows (Buongiorno CLI di Azure).

> [!IMPORTANT]
> Questo documento descrive versione 2.3 di hello estensione diagnostica per Linux, che è stato deprecato. La versione 2.3 sarà supportata fino al 30 giugno 2018.
>
> Versione 3.0 di hello che estensione diagnostica per Linux può invece essere abilitato. Per ulteriori informazioni, vedere [hello documentazione](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Abilitare o disabilitare il monitoraggio tramite hello portale di Azure

È possibile abilitare il monitoraggio della VM di Azure, che fornisce dati sull'istanza ogni minuto (sono incluse le modifiche dell'archivio). Dati di diagnostica dettagliate sono quindi disponibili per hello VM nei grafici portale hello o tramite API hello. Per impostazione predefinita, il portale di Azure consente di abilitare il monitoraggio basato su host di un set limitato di metriche. È possibile abilitare il monitoraggio delle metriche all'interno di una macchina virtuale durante hello che macchina virtuale è in esecuzione o in stato di arresto.

* Aprire hello Azure portale in [https://portal.azure.com](https://portal.azure.com).
* Nel riquadro di spostamento sinistro di hello, fare clic su macchine virtuali.
* Nelle macchine virtuali di hello elenco, selezionare un'istanza in esecuzione o arrestata. Apre il pannello di "Macchina virtuale" Hello.
* Fare clic su Tutte le impostazioni.
* Fare clic su Diagnostica.
* Modificare lo stato tooOn o impostata su Off. È anche possibile selezionare in questo livello di hello Pannello di controllo dettaglio tooenable desiderato per la macchina virtuale.

![Abilitare o disabilitare il monitoraggio tramite hello portale di Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Abilitare/Disabilitare il monitoraggio con l'interfaccia della riga di comando di Azure

tooenable monitoraggio per una macchina virtuale di Azure.

* Creare un file denominato, ad esempio, PrivateConfig.json:

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Abilitare estensione hello tramite CLI di Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Per ulteriori informazioni, vedere [estensione diagnostica per Linux tramite tooMonitor Linux VM dati sulle prestazioni e diagnostica](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
