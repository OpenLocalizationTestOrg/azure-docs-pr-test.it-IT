---
title: aaaSync contenuto da un tooAzure cartella cloud servizio App
description: Informazioni su come toodeploy tooAzure l'app del servizio App tramite il contenuto di sincronizzazione da una cartella di cloud.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Sincronizza il contenuto da un tooAzure cartella cloud servizio App
In questa esercitazione illustra come toodeploy troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) per la sincronizzazione del contenuto da servizi di archiviazione cloud più diffusi come Dropbox e OneDrive. 

## <a name="overview"></a>Panoramica della distribuzione per la sincronizzazione dei contenuti
distribuzione di sincronizzazione del contenuto su richiesta Hello è alimentata dalle hello [motore di distribuzione Kudu](https://github.com/projectkudu/kudu/wiki) integrato con il servizio App. In hello [portale Azure](https://portal.azure.com), è possibile specificare una cartella nella memoria cloud, con il codice dell'app e il contenuto della cartella di lavoro e fare clic su sincronizzazione tooApp servizio con hello di un pulsante. Sincronizzazione del contenuto utilizza processo Kudu hello per la compilazione e distribuzione. 

## <a name="contentsync"></a>Modalità di sincronizzazione di distribuzione contenuto tooenable
sincronizzazione del contenuto di tooenable da hello [portale Azure](https://portal.azure.com), seguire questi passaggi:

1. Nel pannello dell'app nel portale di Azure hello, fare clic su **impostazioni** > **origine distribuzione**. Fare clic su **Scegli origine**, quindi selezionare **OneDrive** o **Dropbox** come origine di hello per la distribuzione. 
   
    ![Sincronizzazione dei contenuti](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > A causa delle differenze sottostanti in hello API, **OneDrive for Business** non è supportato in questo momento. 
   > 
   > 
2. Hello completo autorizzazione del flusso di lavoro tooenable tooaccess di servizio App uno specifico predefiniti percorso designato per OneDrive o Dropbox tutto il contenuto di servizio App in cui verranno archiviati.  
    Dopo hello autorizzazione piattaforma del servizio App fornirà hello opzione toocreate una cartella del contenuto in hello definita percorso del contenuto o una cartella di contenuto esistente in questo percorso contenuto designato toochoose. i percorsi del contenuto Hello designato in account di archiviazione cloud utilizzato per la sincronizzazione di servizio App sono seguente hello:  
   
   * **OneDrive**: `Apps\Azure Web Apps` 
   * **Dropbox**: `Dropbox\Apps\Azure`
3. Dopo aver hello sincronizzazione contenuto hello di sincronizzazione iniziale di contenuto può essere avviata su richiesta dal portale di Azure hello. Cronologia della distribuzione è disponibile con hello **distribuzioni** blade.
   
    ![Cronologia di distribuzione](./media/app-service-deploy-content-sync/onedrive_sync.png)

Altre informazioni sulla distribuzione con Dropbox sono disponibili in [Distribuzione tramite Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

