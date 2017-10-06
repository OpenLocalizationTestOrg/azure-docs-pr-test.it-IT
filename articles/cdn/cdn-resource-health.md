---
title: "integrità hello aaaMonitor delle risorse di rete CDN di Azure | Documenti Microsoft"
description: "Informazioni su come toomonitor hello integrità delle risorse di rete CDN di Azure utilizzando l'integrità delle risorse di Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Monitoraggio integrità hello delle risorse di rete CDN di Azure
  
L'integrità delle risorse della rete CDN di Azure costituisce un sottoinsieme di [Integrità risorse di Azure](../resource-health/resource-health-overview.md).  È possibile utilizzare risorse di Azure toomonitor hello dell'integrità delle risorse di rete CDN e ricevere problemi tootroubleshoot Guida.

>[!IMPORTANT] 
>Integrità delle risorse della rete CDN di Azure attualmente solo account per l'integrità di hello di recapito della rete CDN globale e delle funzionalità dell'API.  Non vengono verificati i singoli endpoint della rete CDN.
>
>Segnala Hello che feed integrità delle risorse di rete CDN di Azure può essere up too15 minuti di ritardo.

## <a name="how-toofind-azure-cdn-resource-health"></a>Come toofind integrità delle risorse di rete CDN di Azure

1. In hello [portale di Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.

2. Fare clic su hello **impostazioni** pulsante.

    ![Pulsante Impostazioni](./media/cdn-resource-health/cdn-profile-settings.png)

3. In *Supporto e risoluzione dei problemi* fare clic su **Integrità risorsa**.

    ![Integrità delle risorse della rete CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>È anche possibile trovare le risorse di rete CDN nell'hello *integrità delle risorse* riquadro in hello *Guida e supporto* blade.  È possibile ottenere rapidamente troppo*Guida e supporto* facendo hello cerchiato **?** in hello alto a destra del portale hello.
>
> ![Guida e supporto tecnico](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Messaggi specifici della rete CDN di Azure

Integrità delle risorse della rete CDN tooAzure correlati stati può trovarsi sotto.

|Message | Azione consigliata |
|---|---|
|Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto | Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto.|
|Siamo spiacenti, non è attualmente disponibile hello servizio di gestione della rete CDN | Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.|
|Gli endpoint di rete CDN potrebbero essere interessati dai problemi in corso con alcuni provider di servizi di rete CDN | Fare nuovamente clic qui per gli aggiornamenti di stato. Utilizzare la modalità toolearn strumento di risoluzione dei problemi hello tootest l'origine e l'endpoint rete CDN. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico. |
|Sono stati riscontrati ritardi di propagazione delle modifiche di configurazione agli endpoint di rete CDN | Fare nuovamente clic qui per gli aggiornamenti di stato. Se le modifiche di configurazione non vengono propagate completamente nel tempo previsto di hello, contattare il supporto tecnico.|
|Siamo spiacenti, che si sono verificati problemi durante il caricamento portale supplementare hello | Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.|
Sono stati riscontrati problemi con alcuni provider di servizi di rete CDN | Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico. |

## <a name="next-steps"></a>Passaggi successivi

- [Panoramica su Integrità risorse di Azure](../resource-health/resource-health-overview.md)
- [Risolvere i problemi di compressione della rete CDN](./cdn-troubleshoot-compression.md)
- [Risolvere i problemi relativi a errori 404](./cdn-troubleshoot-endpoint.md)