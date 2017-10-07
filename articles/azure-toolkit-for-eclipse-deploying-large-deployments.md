---
title: aaaDeploying distribuzioni di grandi dimensioni
description: Informazioni su come le distribuzioni di grandi dimensioni toodeploy utilizzando hello Azure Toolkit per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Distribuire distribuzioni di grandi dimensioni
Se la distribuzione è troppo grande toobe contenuta nella cartella approot predefinita di hello, è possibile utilizzare una risorsa di archiviazione locale come cartella radice di distribuzione hello per il JDK e server applicazioni.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse una risorsa di archiviazione locale come cartella radice di distribuzione hello per le distribuzioni di grandi dimensioni
1. Creare una nuova una risorsa di archiviazione locale nome Hello della risorsa di hello non è rilevante. Risorse di archiviazione sono definite a livello di ruolo hello. Hello più rapido modo tooaccess hello archiviazione locale finestra di dialogo configurazione, da cui è possibile creare una nuova risorsa di archiviazione locale, è tramite hello alla procedura seguente: ruolo di hello pulsante destro del mouse in hello **Esplora progetti** vista (espandere il Azure nodo del progetto se non viene visualizzato il ruolo di hello), fare clic su **Azure**, quindi fare clic su **archiviazione locale**. All'interno di hello **archiviazione locale** finestra di dialogo, fare clic su **Aggiungi** toocreate una nuova risorsa di archiviazione locale.

2. Hello set desiderato di dimensioni tooat almeno 2048 MB (un valore minore potrebbe causare hello stessi problemi di dimensioni di file si riscontrerebbero in hello approot).

3. Verificare che **pulire contenuto hello quando l'istanza del ruolo hello viene riciclato** è selezionato; Ciò consentirà di impedire l'esecuzione in è in conflitto con i file preesistenti nella risorsa hello logica di avvio della distribuzione di hello quando hello ruolo istanza viene riciclata.

4. Verificare che hello **l'archiviazione variabile di ambiente hello percorso della directory della risorsa dopo la distribuzione** valore viene impostato stringa toohello **DEPLOYROOT**. La finestra di dialogo di risorse di archiviazione locale avrà un aspetto simile toohello seguente.

   ![][ic667943]

In alternativa, se si utilizza **DEPLOYROOT** come hello *nome* di risorsa locale e non modificare il nome variabile di ambiente generato automaticamente hello (che verrà impostato troppo **DEPLOYROOT_PATH** in questo caso), che viene utilizzata per l'applicazione.

Altre informazioni sulla creazione di una risorsa di archiviazione locale sono reperibili in [Proprietà dell'archiviazione locale][Local storage properties].

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
