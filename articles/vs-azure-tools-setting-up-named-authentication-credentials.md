---
title: Backup denominato le credenziali di autenticazione aaaSetting | Documenti Microsoft
description: "Informazioni su come servizio cloud tootooprovide credenziali che Visual Studio è possibile utilizzare tooauthenticate richieste tooAzure toopublish tooAzure un'applicazione da Visual Studio o toomonitor esistente... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Configurazione delle credenziali per l'autenticazione denominate
toopublish tooAzure un'applicazione da Visual Studio o toomonitor un servizio cloud esistente, è necessario fornire credenziali che Visual Studio è possibile utilizzare tooauthenticate richiede tooAzure. Esistono diverse posizioni in cui è possibile accedere in tooprovide queste credenziali di Visual Studio. Da Esplora Server hello, ad esempio, è possibile aprire il menu di scelta rapida hello per hello **Azure** nodo e scegliere **connettersi tooMicrosoft sottoscrizione Azure...** . Quando si accede, informazioni sulla sottoscrizione hello associati all'account di Azure è disponibile in Visual Studio e non vi sono altre che è toodo.

Gli strumenti di Azure supporta inoltre un modo meno recente di fornire le credenziali, l'utilizzo di file di sottoscrizione hello (file publishsettings). Questo argomento illustra tale metodo, ancora supportato in Azure SDK 2.2.

Hello seguenti elementi è necessario per l'autenticazione tooAzure:

* ID sottoscrizione
* Un certificato X.509 v3 valido

> [!NOTE]
> lunghezza di Hello della chiave del certificato x. 509 v3 hello deve essere di almeno 2048 bit. Azure rifiuterà qualsiasi certificato che non soddisfa questo requisito o che sia non valido.
>
>

Visual Studio Usa l'ID sottoscrizione e i dati del certificato hello come credenziali. le credenziali appropriate Hello vengono fatto riferimento nel file di sottoscrizione hello (file publishsettings), che contiene una chiave pubblica per il certificato di hello. file di sottoscrizione Hello può contenere le credenziali per più di una sottoscrizione.

È possibile modificare le informazioni sulla sottoscrizione hello da hello **nuova/modifica sottoscrizione** la finestra di dialogo, come descritto più avanti in questo argomento.

Se si desidera toocreate un certificato manualmente, è possibile fare riferimento a istruzioni toohello [creare e caricare un certificato di gestione per Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e caricare manualmente hello certificato toohello [portale di Azure classico ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Queste credenziali che Visual Studio richiede toomanage che non sono i servizi cloud hello stesse credenziali che sono necessari tooauthenticate una richiesta nei servizi di archiviazione di Azure hello.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importare, configurare o modificare le credenziali di autenticazione in Visual Studio
Importare, impostare o modificare le credenziali di autenticazione in hello **nuova sottoscrizione** nella finestra di dialogo viene visualizzata se si esegue hello azione seguente:

* In **Esplora Server**, aprire il menu di scelta rapida hello per hello **Azure** nodo, scegliere **Gestisci e filtra sottoscrizioni...** , scegliere hello **certificati** scheda ed eseguire uno dei seguenti hello:

    * Scegliere **importare** tooopen hello Importa sottoscrizioni di Microsoft Azure finestra di dialogo in cui è possibile scaricare il file sottoscrizioni hello per hello attualmente caricato sottoscrizione, Sfoglia tooits percorso di download e quindi importarlo per l'utilizzo in autenticazione.
    * Scegliere **New** tooopen hello nuova sottoscrizione finestra di dialogo in cui è possibile impostare una nuova sottoscrizione per l'utilizzo dell'autenticazione.
    * Scegliere **modifica** (dopo aver scelto la sottoscrizione) tooopen hello Modifica sottoscrizione finestra di dialogo in cui è possibile modificare una sottoscrizione esistente per l'utilizzo dell'autenticazione. 

Hello nella procedura si presuppone che hello **nuova sottoscrizione** la finestra di dialogo è aperta.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset delle credenziali di autenticazione in Visual Studio
1. In hello **selezionare un certificato esistente** per elenco autenticazione, scegliere un certificato.
2. Scegliere hello **Copia percorso completo di hello** collegamento. percorso di Hello per il certificato di hello (file con estensione cer) è toohello copiato negli Appunti.

   > [!IMPORTANT]
   > toopublish l'applicazione Azure da Visual Studio, è necessario caricare questo certificato toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. certificato hello tooupload toohello portale di Azure:

   1. Aprire hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Se richiesto, accedere al portale toohello e quindi passare troppo**impostazioni**, **i certificati di gestione**.
   3. Nel riquadro di hello gestione certificati, scegliere **caricare**.
   4. Selezionare la sottoscrizione di Azure, incollare percorso completo di hello del file con estensione cer hello appena creato e scegliere **caricare**.
