---
title: impostazioni di aaaCustom per gli ambienti del servizio App
description: Impostazioni di configurazione personalizzate per gli ambienti del servizio app
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Impostazioni di configurazione personalizzate per gli ambienti del servizio app
## <a name="overview"></a>Panoramica
Poiché gli ambienti del servizio App sono isolati tooa singolo cliente, esistono alcune impostazioni di configurazione che possono essere applicate esclusivamente tooApp gli ambienti del servizio. In questo articolo illustrata hello diverse personalizzazioni specifiche disponibili per gli ambienti del servizio App.

Se non si dispone di un ambiente del servizio App, vedere [come un ambiente del servizio App tooCreate](app-service-web-how-to-create-an-app-service-environment.md).

È possibile archiviare le personalizzazioni dell'ambiente del servizio App tramite una matrice in hello nuova **clusterSettings** attributo. Questo attributo viene trovato nel dizionario "Proprietà" hello hello *hostingEnvironments* entità di gestione risorse di Azure.

Hello abbreviato Gestione risorse modello frammento seguente viene illustrato hello **clusterSettings** attributo:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Hello **clusterSettings** attributo può essere incluso in un hello tooupdate modello di gestione risorse ambiente del servizio App.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Utilizzare Esplora risorse Azure tooupdate un ambiente del servizio App
In alternativa, è possibile aggiornare l'ambiente del servizio App hello utilizzando [Esplora inventario risorse di Azure](https://resources.azure.com).  

1. In Esplora risorse passare toohello nodo per l'ambiente del servizio App hello (**sottoscrizioni** > **resourceGroups** > **provider**  >  **Microsoft** > **hostingEnvironments**). Quindi fare clic su hello specifico ambiente del servizio App che si desidera tooupdate.
2. Nel riquadro di destra hello, fare clic su **lettura/scrittura** in tooallow barra degli strumenti superiore hello interattivo modifica in Esplora inventario risorse.  
3. Fare clic su hello blu **modifica** toomake hello Gestione risorse modello modificabile.
4. Scorrimento toohello parte inferiore del riquadro di destra hello. Hello **clusterSettings** in hello parte inferiore, in cui è possibile immettere o aggiornare il relativo valore è l'attributo.
5. Matrice di hello tipo (o copia e Incolla) di valori di configurazione desiderati in hello **clusterSettings** attributo.  
6. Fare clic su hello verde **inserire** pulsante che è disponibile nella parte superiore di hello di hello riquadro destro toocommit hello modifica toohello ambiente del servizio App.

Tuttavia, si invia modifica hello, impiegato moltiplicati per il numero di hello di front-end in hello ambiente del servizio App per effetto di hello modifica tootake circa 30 minuti.
Ad esempio, se un ambiente del servizio App dispone di quattro front-end, richiederà circa due ore per hello configurazione aggiornamento toofinish. Durante la modifica di configurazione hello è in fase di implementazione, non esistono altre operazioni di scala o operazioni di modifica della configurazione possono avvenire in hello ambiente del servizio App.

## <a name="disable-tls-10"></a>Disabilitare TLS 1.0
Una domanda ricorrente dai clienti, in particolare i clienti che utilizzano la conformità PCI controlli, è come tooexplicitly disabilitare TLS 1.0 per le app.

TLS 1.0 può essere disabilitato tramite il seguente hello **clusterSettings** voce:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Modifica dell'ordine dei pacchetti di crittografia TLS
Un'altra domanda dai clienti è se è possibile modificare l'elenco di hello crittografie negoziato da server e questo può essere ottenuto modificando hello **clusterSettings** come illustrato di seguito. elenco di Hello dei pacchetti di crittografia disponibili può essere recuperato da [questo articolo MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Se i valori non corretti vengono impostati per pacchetto di crittografia hello che non è possibile comprendere SChannel, tutti i server di tooyour comunicazione TLS potrebbe smettere di funzionare. In tal caso, sarà necessario hello tooremove *FrontEndSSLCipherSuiteOrder* voce **clusterSettings** e inviare hello aggiornato di crittografia predefinito di gestione risorse modello toorevert toohello indietro impostazioni di gruppo.  Usare questa funzionalità con cautela.
> 
> 

## <a name="get-started"></a>Attività iniziali
sito di modello di avvio rapido di Azure Resource Manager Hello include un modello con la definizione di base hello per [la creazione di un ambiente del servizio App](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
