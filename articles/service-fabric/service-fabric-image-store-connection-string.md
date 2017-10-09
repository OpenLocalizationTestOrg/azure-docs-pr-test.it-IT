---
title: stringa di connessione di Service Fabric immagine archivio aaaAzure | Documenti Microsoft
description: Comprendere una stringa di connessione archivio hello immagine
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Comprendere l'impostazione ImageStoreConnectionString hello

In alcuni documentazione è indicato brevemente esistenza hello di un parametro "ImageStoreConnectionString" senza che descrive il significato. E dopo aver esaminato un articolo come [distribuire e rimuovere le applicazioni con PowerShell][10], sembra che non è il valore di hello Copia/Incolla, così come viene visualizzato nel manifesto del cluster di destinazione hello hello cluster. Impostazione di hello devono pertanto essere configurabili per ogni cluster, ma quando si crea un cluster tramite hello [portale di Azure][11], non vi è alcun tooconfigure opzione questa impostazione e i relativi sempre "fabric: ImageStore". Qual è la funzione hello di quindi questa impostazione?

![Manifesto del cluster][img_cm]

Service Fabric iniziato come piattaforma per l'utilizzo Microsoft interno per molti team diversi, pertanto alcuni aspetti sono altamente personalizzabili: hello, "Image Store" è un aspetto di questo tipo. In pratica, hello Image Store è un repository di collegamento per l'archiviazione dei pacchetti di applicazioni. Quando l'applicazione è distribuita tooa nodo cluster hello, tale nodo Scarica il contenuto di hello del pacchetto di applicazione da hello archivio immagini. ImageStoreConnectionString Hello è un'impostazione che include tutte le informazioni necessarie hello per i client e i nodi toofind hello corretto archivio immagini per un determinato cluster.

Esistono attualmente tre tipi possibili di provider i Archivio immagini e le relative stringhe di connessione sono le seguenti:

1. Servizio di archiviazione immagini: "fabric:ImageStore"

2. File System: "file:[file system path]"

3. Archiviazione di Azure: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

tipo di provider Hello utilizzato nell'ambiente di produzione è hello immagine il servizio di archiviazione, un servizio di sistema persistente con stato che si può vedere dal Service Fabric Explorer. 

![Servizio di archiviazione immagini][img_is]

Hosting hello Image Store in un servizio di sistema all'interno di cluster hello stesso Elimina dipendenze esterne per il repository di pacchetti hello e offre maggiore controllo sulla località hello di archiviazione. Futuri miglioramenti intorno hello Image Store sono provider dell'archivio di immagini tootarget probabilmente hello in primo luogo, se non in modo esclusivo. stringa di connessione Hello per provider di servizio di archiviazione immagine hello non dispone di informazioni univoche perché il client di hello è già connesso toohello cluster di destinazione. client Hello deve solo tooknow che devono essere utilizzati i protocolli hello servizio di sistema di destinazione.

Hello File System provider viene utilizzato anziché hello immagine il servizio di archiviazione per i cluster di una casella locali durante il cluster di sviluppo toobootstrap hello leggermente superiore. differenza Hello è tipicamente piccola, ma è un'ottimizzazione per la maggior parte delle utile durante lo sviluppo. È possibile toodeploy una casella locale di un cluster con hello anche altri tipi di provider di archiviazione, ma non è in genere toodo così poiché il flusso di lavoro di hello sviluppo/test non hello uguali indipendentemente dal provider. Diverso da questo utilizzo, il provider di archiviazione di Azure e File System hello esiste solo per il supporto legacy.

Pertanto, mentre hello ImageStoreConnectionString è configurabile, è in genere solo utilizzare hello impostazione predefinita. Quando si pubblicano tooAzure tramite [Visual Studio][12], parametro hello viene impostato automaticamente di conseguenza. Per la distribuzione a livello di codice tooclusters ospitato in Azure, la stringa di connessione hello è sempre "fabric: ImageStore". Anche se in caso di dubbi, il relativo valore può essere verificato sempre recuperando hello manifesto del cluster da [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), o [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Test sia in locale e i cluster di produzione devono essere sempre anche provider di servizio di archiviazione immagine hello toouse configurato.

### <a name="next-steps"></a>Passaggi successivi
[Deploy and remove applications using PowerShell][10] (Distribuire e rimuovere applicazioni con PowerShell)

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
