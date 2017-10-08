---
title: aaaAbout immagini per le macchine virtuali Windows | Documenti Microsoft
description: Informazioni sull'utilizzo delle immagini con macchine virtuali Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Informazioni sulle immagini per le macchine virtuali Windows
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sulla ricerca e utilizzo di immagini nel modello di gestione risorse di hello, vedere [qui](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Utilizzo di immagini

È possibile utilizzare il modulo di Azure PowerShell hello e hello toomanage portale Azure hello immagini disponibili tooyour sottoscrizione di Azure. modulo di Azure PowerShell Hello fornisce più opzioni di comando, individuare esattamente ciò che si desidera toosee o eseguire. Hello portale di Azure fornisce un'interfaccia utente grafica per la maggior parte delle attività amministrative quotidiane hello.

Di seguito sono riportati alcuni esempi che utilizzano il modulo di Azure PowerShell hello.

* **Ottenere tutte le immagini**:`Get-AzureVMImage`restituisce un elenco di tutte le immagini di hello disponibili nella sottoscrizione corrente: le immagini e quelle fornite da Azure o i partner. elenco di Hello risultante potrebbe essere elevato. Hello esempi successivi viene illustrato come tooget un elenco più breve.
* **Ottenere famiglie di immagini**: `Get-AzureVMImage | select ImageFamily` restituisce un elenco delle famiglie di immagini visualizzando la proprietà **ImageFamily** delle stringhe.
* **Ottenere tutte le immagini in una famiglia specifica**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Trovare le immagini VM**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` questo cmdlet funziona filtrando la proprietà DataDiskConfiguration di hello, che si applica solo le immagini tooVM. In questo esempio viene inoltre Filtra hello output tooonly hello etichetta e il nome.
* **Salvare un'immagine generalizzata**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Salvare un'immagine specializzata**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > Hello parametro OSState è necessario toocreate un'immagine di macchina virtuale, che include disco del sistema operativo hello e i dischi dati collegati. Se non si utilizza il parametro hello, hello cmdlet crea un'immagine del sistema operativo. valore di Hello del parametro hello indica se l'immagine hello è generalizzata o specializzata, in base se disco del sistema operativo hello è stato preparato per il riutilizzo.

* **Eliminare un'immagine**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Passaggi successivi
È anche possibile [creare una macchina Windows hello portale di Azure usando](tutorial.md).
