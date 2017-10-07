---
title: Asset aaaPre carico su un endpoint rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toopre carico memorizzato nella cache il contenuto di un endpoint rete CDN di Azure.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Precaricamento di risorse in un endpoint della rete CDN di Azure
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Per impostazione predefinita, gli asset vengono prima di tutto memorizzati nella cache quando vengono richiesti. Ciò significa che prima richiesta di hello da ogni area può richiedere più tempo, poiché non dispone di server edge hello contenuto hello memorizzati nella cache e sarà necessario tooforward hello richiesta toohello origine server. Il precaricamento del contenuto consente di evitare questa latenza della prima richiesta.

Inoltre tooproviding soddisfazione del cliente, precaricamento risorse memorizzate nella cache può anche ridurre il traffico di rete sul server di origine hello.

> [!NOTE]
> Precaricamento in corso asset è utile per eventi di grandi dimensioni o contenuto che diventa tooa contemporaneamente disponibili numerosi utenti, ad esempio una nuova versione di film o un aggiornamento software.
> 
> 

Questa esercitazione illustra in modo dettagliato il precaricamento di contenuto memorizzato nella cache in tutti i nodi perimetrali della rete CDN di Azure.

## <a name="walkthrough"></a>Procedura dettagliata
1. In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN toohello contenente hello endpoint desiderato toopre carico.  Apre il pannello di profilo Hello.
2. Fare clic sull'endpoint hello nell'elenco di hello.  Apre il pannello di endpoint Hello.
3. Dal Pannello di endpoint rete CDN hello, fare clic sul pulsante Carica hello.
   
    ![Pannello dell'endpoint della rete CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Apre il pannello di carico Hello.
   
    ![Pannello di caricamento della rete CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Immettere il percorso completo di hello di ciascuna risorsa desiderato tooload (ad esempio, `/pictures/kitten.png`) in hello **percorso** casella di testo.
   
   > [!TIP]
   > Ulteriori **percorso** nelle caselle di testo verrà visualizzato dopo l'immissione di testo tooallow si toobuild un elenco di più risorse.  È possibile eliminare l'asset dall'elenco hello facendo clic sul pulsante con puntini di sospensione (…) hello.
   > 
   > I percorsi devono contenere un URL relativo che si adatta a seguito di hello [espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Caricare un singolo percorso di file `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Caricare un singolo file con stringa di query `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Ogni asset deve avere il proprio percorso.  Non esiste alcuna funzionalità con caratteri jolly per il pre-caricamento degli asset.
   > 
   > 
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Fare clic su hello **carico** pulsante.
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Le richieste di caricamento sono limitate a un massimo di 10 al minuto per ogni profilo di rete CDN. Sono consentiti 50 percorsi per richiesta. Ogni percorso ha un limite di lunghezza di 1024 caratteri.
> 
> 

## <a name="see-also"></a>Vedere anche
* [Ripulire un endpoint della rete CDN di Azure](cdn-purge-endpoint.md)
* [Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint](https://msdn.microsoft.com/library/mt634451.aspx)

