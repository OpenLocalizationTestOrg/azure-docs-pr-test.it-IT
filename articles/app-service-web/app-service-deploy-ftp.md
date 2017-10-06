---
title: aaaDeploy il tooAzure app servizio App utilizzando FTP/S | Documenti Microsoft
description: Informazioni su come toodeploy tooAzure l'app App Service tramite FTP o FTPS.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Distribuire il servizio App utilizzando FTP/S di tooAzure app

In questo articolo illustra come toouse FTP o FTPS toodeploy l'app web back-end dell'app mobile o app per le API troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

endpoint di Hello FTP/S per l'app è già attivo. Non è distribuzione FTP/S tooenable necessaria alcuna configurazione.

> [!IMPORTANT]
> Si sta eseguendo in modo continuo passaggi tooimprove sicurezza piattaforma Microsoft Azure. Nell'ambito di questa attività in corso un aggiornamento delle applicazioni Web è pianificato per le aree della Germania centrale e nord-orientale. Durante l'esecuzione dell'App Web verrà la disabilitazione della utilizzare hello del protocollo di testo normale FTP per le distribuzioni. I clienti tooour raccomandazione è tooFTPS tooswitch per le distribuzioni. Non Prevediamo qualsiasi servizio tooyour interruzioni durante l'aggiornamento a cui è pianificato per 9/5. Grazie per il sostegno per il lavoro richiesto.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Passaggio 1: Impostare le credenziali per la distribuzione

server di tooaccess hello FTP per l'app, è necessario innanzitutto le credenziali di distribuzione. 

tooset o Reimposta le credenziali di distribuzione, vedere [le credenziali di distribuzione di Azure App Service](app-service-deployment-credentials.md). Questa esercitazione viene illustrato l'utilizzo di hello delle credenziali a livello di utente.

## <a name="step-2-get-ftp-connection-information"></a>Passaggio 2: Ottenere informazioni di connessione a FTP

1. In hello [portale di Azure](https://portal.azure.com), Apri l'app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Selezionare **Panoramica** nel menu a sinistra di hello, quindi annotare i valori hello per **utente FTP/distribuzione**, **nome Host FTP**, e **il nome Host FTPS**. 

    ![Informazioni di connessione a FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Hello **utente FTP/distribuzione** valore utente come visualizzato dal portale di Azure, incluso il nome dell'app hello contesto appropriato tooprovide di ordine per il server FTP hello hello.
    > È possibile trovare hello stesse informazioni quando si seleziona **proprietà** nel menu a sinistra di hello. 
    >
    > Inoltre, la password di hello distribuzione non viene visualizzata. Se si dimentica la password di distribuzione, tornare troppo[passaggio 1](#step1) e reimpostare la password di distribuzione.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Passaggio 3: Distribuire file tooAzure

1. Dal client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)e così via), utilizzare le informazioni di connessione hello raccolte tooconnect tooyour app.
3. Copiare i file e i relativi toohello struttura rispettive directory [ **/sito/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (o hello **/sito/wwwroot/App_Data/processi/** directory per Processi Web).
4. App di hello tooverify URL dell'app tooyour Sfoglia viene eseguito correttamente. 

> [!NOTE] 
> A differenza di [le distribuzioni basate su Git](app-service-deploy-local-git.md), la distribuzione FTP non supporta hello automazioni di distribuzione seguenti: 
>
> - Ripristino delle dipendenze (ad esempio, automazioni NuGet, NPM, PIP e Composer)
> - Compilazione di file binari .NET
> - Generazione di web.config ([esempio di Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Questi file necessari devono essere ripristinati, compilati e generati manualmente nel computer locale e distribuiti con l'app.
>
>

## <a name="next-steps"></a>Passaggi successivi

Per gli scenari più avanzati, provare a [distribuzione tooAzure con Git](app-service-deploy-local-git.md). Distribuzione basati su GIT tooAzure consente il controllo della versione, ripristino del pacchetto, MSBuild e molto altro.

## <a name="more-resources"></a>Altre risorse

* [Creare un'app Web PHP-MySQL e distribuirla tramite FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Credenziali per la distribuzione del Servizio app di Azure](app-service-deploy-ftp.md)
