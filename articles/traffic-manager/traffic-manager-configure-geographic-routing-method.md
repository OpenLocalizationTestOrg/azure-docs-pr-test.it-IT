---
title: metodo di routing tramite Azure Traffic Manager il traffico aaaConfigure geografica | Documenti Microsoft
description: Questo articolo viene illustrato come tooconfigure hello metodo di routing del traffico geografica tramite Gestione traffico di Azure
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Configurazione metodo di routing del traffico geografica hello tramite Gestione traffico

metodo di routing del traffico geografica Hello consente toodirect traffico toospecific endpoint basati su hello posizione geografica in cui le richieste di hello derivano. In questa esercitazione viene illustrato come profilo di toocreate una gestione traffico con questo metodo di routing e configurare il traffico di hello endpoint tooreceive da aree geografiche specifiche.

## <a name="create-a-traffic-manager-profile"></a>Creazione di un profilo di Gestione traffico

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/).
2. Nel menu Hub hello, fare clic su **New** > **rete** > **tutti**e quindi fare clic su **il profilo di gestione traffico**hello tooopen **profilo di Traffic Manager creare** blade.
3. In hello **profilo di Traffic Manager creare** pannello:
    1. Specificare un nome per il profilo. Questo nome deve toobe univoco all'interno di zona trafficmanager.net hello e nome DNS hello risulterà <profilename>, trafficmanager.net che sarà possibile tooaccess utilizzato il profilo di Traffic Manager.
    2. Seleziona hello **geografico** metodo di routing.
    3. Selezionare la sottoscrizione di hello desiderato toocreate questo profilo.
    4. Utilizzare un gruppo di risorse esistente o creare un nuovo tooplace gruppo di risorse di questo profilo. Se si sceglie toocreate un nuovo gruppo di risorse, utilizzare hello **il percorso del gruppo di risorse** percorso hello toospecify di elenco a discesa hello del gruppo di risorse. Questa impostazione fa riferimento il percorso toohello hello del gruppo di risorse e non ha alcun impatto su hello profilo di Traffic Manager che verrà distribuito a livello globale.
    5. Dopo aver fatto clic su **Crea**, viene creato il profilo di Gestione traffico, che viene poi distribuito a livello globale.

![Creare un profilo di Gestione traffico](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Aggiungere endpoint

1. Ricerca per nome di profilo di gestione traffico hello che appena creato nella barra di ricerca del portale hello e fare clic sul risultato di hello quando visualizzata.
2. Passare troppo**impostazioni** -> **endpoint** nel Pannello di gestione traffico hello.
3. Fare clic su **Aggiungi** tooshow hello **Aggiungi Endpoint** blade.
3. In hello **endpoint** pannello, fare clic su **Aggiungi** e hello **aggiungere endpoint** pannello in cui è visualizzato, completare come segue:
4. Selezionare **tipo** in base al tipo di hello dell'endpoint aggiunto. Per i profili di routing geografico usati nell'ambiente di produzione è consigliabile usare i tipi di endpoint annidati che contengono un profilo figlio con più di un endpoint. Per altre informazioni, vedere le [domande frequenti sui metodi di routing del traffico](traffic-manager-FAQs.md).
5. Fornire un **nome** mediante il quale si desidera toorecognize questo endpoint.
6. Alcuni campi in questo pannello dipendono dal tipo di hello dell'endpoint che si desidera aggiungere:
    1. Se si aggiunge un endpoint di Azure, selezionare hello **tipo di risorsa di destinazione** hello e **destinazione** in base alle risorse di hello si desideri traffico toodirect
    2. Se si aggiunge un **esterno** endpoint, fornire hello **il nome di dominio completo (FQDN)** per l'endpoint.
    3. Se si aggiunge un **Nested endpoint**selezionare hello **risorsa di destinazione** corrispondente il profilo figlio toohello desiderato toouse e specificare hello **endpoint figlio minimo numero**.
7. Nella sezione Geo-mapping hello, utilizzare hello elenco a discesa aree hello tooadd da cui il traffico inviato toobe toothis endpoint. È necessario aggiungere almeno un'area ed è possibile mappare più aree.
8. Ripetere questo passaggio per tutti gli endpoint si desidera tooadd in questo profilo

![Aggiungere un endpoint di Gestione traffico](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utilizzare il profilo di gestione traffico hello
1.  Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che è stato creato nella precedente sezione hello e fare clic sul profilo di gestione traffico hello in hello comporta che hello visualizzato.
2. In hello **profilo di gestione traffico** pannello, fare clic su **Panoramica**.
3. Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato. È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello.  Nel caso di hello di routing geografico, Traffic Manager esamina hello IP di origine della richiesta in ingresso hello e determina hello area da cui viene generato. Se tale area è mappato tooan endpoint, il traffico viene indirizzato toothere. Se questa area non è mappato tooan endpoint, gestione traffico restituisce una risposta alla query NODATA.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sul [Metodo di routing del traffico geografico ](traffic-manager-routing-methods.md#geographic).
- Informazioni su come troppo[verificare le impostazioni di gestione traffico](traffic-manager-testing-settings.md).
