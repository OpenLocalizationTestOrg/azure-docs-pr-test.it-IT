---
title: aaaReference per la navigazione hello portale di Azure
description: Altre esperienze utente diverso hello per applicazione servizio Web tra il portale di gestione di hello e hello portale di Azure
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Riferimento per la navigazione hello portale di Azure
Siti Web di Azure è ora denominato [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714). Stiamo aggiornando i nostri tooreflect documentazione questo nome cambia e tooprovide le istruzioni per hello portale di Azure. Fino al completamento del processo, è possibile utilizzare questo documento come guida per l'utilizzo con App Web hello portale di Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>Hello futuro di hello portale classico di Azure
Mentre si noterà che le modifiche nel portale di Azure classico hello di branding hello, il portale è in corso di hello di verrà sostituito da hello portale di Azure. Come portale classico hello è obsoleta, hello per i nuovi sviluppi attenzione toohello portale di Azure. Tutte le future nuove funzionalità per le app Web sarà quello hello portale di Azure. Iniziare a usare hello Azure Portal tootake sfruttare hello più recente che le app Web sono toooffer.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Differenze di layout tra hello portale classico di Azure e il portale di Azure
Nel portale classico di hello tutti hello Azure servizi sono elencati sul lato sinistro hello. Spostamento nel portale classico hello segue una struttura ad albero, in cui si avvia dal servizio hello e spostarsi in ogni elemento. Questa struttura funziona bene quando si gestiscono componenti indipendenti. Le applicazioni create in Azure, tuttavia, sono una raccolta di servizi interconnessi e questa struttura ad albero non risulta ideale per lavorare con raccolte di servizi. 

portale di Azure Hello rende facile toobuild applicazioni end-to-end con i componenti da più servizi. portale Hello è organizzata come *viaggi*. Oggetto *viaggio* è una serie di *pannelli*, che sono contenitori di hello diversi componenti. Ad esempio, impostando la scalabilità automatica per un'app web è un *viaggio* che consente di passare più pannelli come illustrato nell'esempio seguente hello: hello **sito web** blade (che titolo del pannello non è ancora stato aggiornato toouse Hello terminologia nuova), hello **impostazioni** blade e hello **scalabilità** blade. Nell'esempio hello, scalabilità automatica viene impostata toodepend all'utilizzo della CPU, pertanto è disponibile anche un **percentuale di CPU** blade. i componenti all'interno di hello Hello *pannelli* vengono chiamati *parti*, quale aspetto riquadri. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Esempio di navigazione: creare un'app Web
La creazione di app Web resta un'operazione semplicissima. Hello seguente immagine Mostra hello classic portale e hello portale side-by-side toodemonstrate che non c'è molto è stato modificato nel numero hello di passi necessari tooget un'app web di e in esecuzione. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Nel portale di hello è possibile scegliere da tipi più comuni di hello di App web, incluse le applicazioni più diffusi raccolta WordPress. Per un elenco completo delle applicazioni disponibili, visitare hello [Azure Marketplace].

Quando si crea un'app web, specificare l'URL, il piano di servizio App e il percorso nel portale di hello così come avviene nel portale classico hello. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Inoltre, hello portale consente di definire altre impostazioni comuni. Ad esempio, [gruppi di risorse](../azure-resource-manager/resource-group-overview.md) renderlo toosee semplice e gestire risorse di Azure correlate. 

## <a name="navigation-example-settings-and-features"></a>Esempio di navigazione: impostazioni e funzionalità
Tutte le impostazioni di hello e funzionalità sono ora raggruppate logicamente in un singolo pannello, da cui è possibile spostarsi.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Ad esempio, è possibile creare i domini personalizzati facendo clic su **i domini personalizzati e SSL** in hello **impostazioni** blade.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset di un avviso del monitoraggio, fare clic su **richieste ed errori** e quindi **Aggiungi avviso**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

diagnostica tooenable, fare clic su **log di diagnostica** in hello **impostazioni** blade.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Fare clic su Impostazioni applicazione tooconfigure, **le impostazioni dell'applicazione** in hello **impostazioni** blade. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Diverso da quello hello del marchio, rinominati o raggruppati in modo diverso nel portale di hello alcuni aspetti toomake è semplice toofind li. Ad esempio, di seguito è una schermata della pagina corrispondente di hello per le impostazioni dell'app (**configura**) nel portale classico hello.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Altre risorse
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

