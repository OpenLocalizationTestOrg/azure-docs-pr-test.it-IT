---
title: le immagini client Windows di aaaUse in Azure | Documenti Microsoft
description: Toouse sottoscrizione di Visual Studio come vantaggi toodeploy Windows 7, Windows 8 o Windows 10 in Azure per gli scenari di sviluppo/test
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Usare client Windows in Azure per scenari di sviluppo/test
A condizione di disporre di una sottoscrizione appropriata di Visual Studio (in precedenza MSDN), è possibile usare Windows 7, Windows 8 o Windows 10 in Azure per scenari di sviluppo/test. Questo articolo vengono illustrati i requisiti per l'esecuzione di client Windows in Azure e l'utilizzo di hello immagini della raccolta di Azure hello.

## <a name="subscription-eligibility"></a>Idoneità della sottoscrizione
I sottoscrittori di Visual Studio attivi (ovvero le persone che hanno acquistato una licenza di sottoscrizione per Visual Studio) possono usare client Windows per le finalità di sviluppo e test. Il client Windows può essere usato nel proprio hardware e nelle proprie macchine virtuali di Azure in esecuzione in qualsiasi tipo di sottoscrizione di Azure. Client di Windows potrebbe non essere distribuito tooor usato in Azure per la produzione normale, o da persone che non sono sottoscrittori attivi di Visual Studio.

Per comodità, sono stati apportati alcuni immagini di Windows 10 disponibili dalla raccolta di Azure hello all'interno di [idonei sviluppo/test offre](#eligible-offers). Visual Studio i server di sottoscrizione all'interno di qualsiasi tipo di offerta è anche possibile [adeguatamente preparare e creare](prepare-for-upload-vhd-image.md) un'immagine a 64 bit di Windows 7, Windows 8 o Windows 10 e quindi [caricare tooAzure](upload-generalized-managed.md). utilizzo di Hello rimane limitato toodev dei test da Visual Studio attivi.

## <a name="eligible-offers"></a>Offerte idonee
ID che sono idonei toodeploy Windows 10 tramite hello Azure raccolta di offerta Hello hello dettagli nella tabella seguente. le immagini di Hello Windows 10 solo sono visibile toohello offerte seguenti. I sottoscrittori di Visual Studio che è necessario toorun client di Windows in un tipo di offerta diversa richiedono troppo[adeguatamente preparare e creare](prepare-for-upload-vhd-image.md) un'immagine a 64 bit di Windows 7, Windows 8 o Windows 10 e [quindi caricare tooAzure](upload-generalized-managed.md).

| Nome offerta | Numero offerta | Immagini client disponibili |
|:--- |:---:|:---:|
| [Sviluppo/test con pagamento in base al consumo](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Sottoscrittori di Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Sottoscrittori di Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Sottoscrittori di Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium con MSDN (vantaggio)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Sottoscrittori di Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Sottoscrittori di Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Sviluppo/test Enterprise](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Controllare la sottoscrizione di Azure
Se non si conosce l'ID offerta, è possibile ottenere tramite hello portale di Azure in uno dei due modi:  

- Nel pannello 'Sottoscrizioni' hello:

  ![Dettagli dell'ID offerta dal portale di Azure hello](./media/client-images/offer-id-azure-portal.png) 

- Fare clic su **Fatturazione** e quindi sull'ID sottoscrizione. ID dell'offerta Hello viene visualizzato nel pannello fatturazione hello.

È inoltre possibile visualizzare l'ID dell'offerta hello da hello [scheda 'Sottoscrizioni'](http://account.windowsazure.com/Subscriptions) hello Azure del portale di Account:

![ID dettagli dell'offerta dal portale di Account di Azure hello](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Passaggi successivi
È ora possibile distribuire le VM usando [PowerShell](quick-create-powershell.md), i [modelli di Resource Manager](ps-template.md) o [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

