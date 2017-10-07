---
title: aaaRelated e le risorse collegate in hello riquadro raccolta
description: Informazioni sulle risorse correlate e collegate che vengono visualizzate nella raccolta di riquadro hello del portale di anteprima di Azure hello.
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a>Risorse correlate e collegate in hello riquadro raccolta
raccolta di riquadro Hello consente toofind riquadri per una particolare risorsa e trascinarli il pannello corrente. Usando hello riquadro raccolta, è possibile creare viste di gestione che si estendono su risorse. Per qualsiasi risorsa specificato, hello correlate risorse includono tutte le risorse di hello relativo gruppo di risorse e le eventuali risorse che si collegano tooor dalla risorsa hello.

## <a name="linked-resources-in-resource-manager"></a>Risorse collegate in Resource Manager
Il collegamento è una funzionalità di gestione risorse di hello.  La procedura permette toodeclare relazioni tra le risorse anche se non risiedono in hello stesso gruppo di risorse. Il collegamento non ha alcun impatto sull'ambiente di esecuzione hello di alcun impatto sull'accesso basato sui ruoli, senza impatto sulla fatturazione e le risorse.  È semplicemente un meccanismo che è possibile utilizzare le relazioni toorepresent in modo che gli strumenti come raccolta riquadro hello può fornire una gestione avanzata esperienza.  Gli strumenti possono controllare i collegamenti di hello tramite collegamenti hello API e fornire l'esperienza nonché della gestione delle relazioni personalizzate. 

## <a name="how-do-i-link-my-resources"></a>Come si collegano le risorse?
Quando si creano risorse tramite il portale di hello o distribuzione di un modello tramite Azure PowerShell o l'interfaccia CLI di Azure, vengono creati automaticamente collegamenti per alcune risorse dipendenti. È possibile collegare anche a livello di codice alle risorse tramite hello [API REST di risorse collegato](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Passaggi successivi
* Se è necessario modelli di gestione risorse toowriting un'introduzione, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).
* vedere toounderstand più informazioni sull'utilizzo di gruppi di risorse tramite il portale di hello [Using hello toomanage portale Azure le risorse di Azure](../azure-resource-manager/resource-group-portal.md).

