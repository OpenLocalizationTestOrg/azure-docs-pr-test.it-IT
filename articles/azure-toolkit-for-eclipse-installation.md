---
title: aaaInstalling hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come tooinstall hello Azure Toolkit per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>L'installazione di hello Azure Toolkit per Eclipse
Hello Azure Toolkit per Eclipse fornisce modelli e le funzionalità che consentono di tooeasily creare, sviluppare, testare e distribuire applicazioni Azure mediante l'ambiente di sviluppo Eclipse hello. Hello Azure Toolkit per Eclipse è un progetto Open Source. codice sorgente Hello è disponibile in hello licenza MIT da <https://github.com/microsoft/azure-tools-for-java>.

Hello alla procedura seguente viene illustrato come tooinstall hello Azure Toolkit per Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>tooinstall hello Azure Toolkit per Eclipse
1. Avviare Eclipse.
2. Fare clic su hello **Guida** menu e quindi fare clic su **installa nuovo Software**, come illustrato nella seguente figura hello.
   
    ![L'installazione di hello Azure Toolkit per Eclipse][01]
3. In hello **Software disponibile** finestra di dialogo, all'interno di hello **utilizzano** nella casella di testo `http://dl.microsoft.com/eclipse` seguita da hello **invio** chiave.
4. In hello **nome** controllo riquadro **Azure Toolkit per Eclipse**e deselezionare **contatta tutti i siti di aggiornamento durante l'installazione software toofind necessari**. Verrà visualizzata una schermata simile toohello seguenti:
   
    ![L'installazione di hello Azure Toolkit per Eclipse][02]
5. Se si espande hello **Azure Toolkit per Eclipse**, verrà visualizzato hello seguenti elementi:
   
   * **Plug-in Insights di applicazione per Java**: questo componente consente di servizi di Azure toouse telemetria analisi e registrazione per le applicazioni e istanze del server.
   * **Azure Access Control Services Filter**: questo componente fornisce il supporto per l'autenticazione degli utenti dell'applicazione con il servizio ACS di Azure, consentendo scenari single sign-on e l'esternalizzazione di logica di identità dall'applicazione hello.
   * **Plug-in comune Azure**: questo componente fornisce funzionalità comuni di hello necessari per altri componenti del toolkit.
   * **Esplora Azure per Eclipse**: questo componente fornisce funzionalità comuni di hello necessari per altri componenti del toolkit.
   * **Plug-in Azure per Eclipse con Java**: questo componente fornisce il supporto per lo sviluppo di progetti che consentono di compilare, testare e distribuire le applicazioni Java per cloud di Microsoft Azure hello in Eclipse e tramite riga di comando.
   * **Plug-in App Web Azure con Java**: questo componente fornisce il supporto per la distribuzione di contenitori di App Web di Azure tooMicrosoft applicazioni web Java.
   * **Microsoft JDBC Driver 4.2 per SQL Server**: questo componente fornisce l'API JDBC per SQL Server e il database SQL di Microsoft Azure per Java Platform Enterprise Edition 8.
   * **Package for Apache Qpid Client Libraries for JMS**: questo componente fornisce il componente client JMS hello da hello Apache Qpid progetto tooenable di AMQP toouse di applicazione messaggistica in Microsoft Azure.
   * **Package for Microsoft Azure Libraries for Java**: questo componente fornisce le API per accedere ai servizi di Microsoft Azure, ad esempio archiviazione, bus di servizio, runtime del servizio e così via.
6. Fare clic su **Avanti**. (Se si verificano ritardi insoliti durante l'installazione di hello toolkit, assicurarsi che **contatta tutti i siti di aggiornamento durante l'installazione software toofind necessari** è deselezionata.)
7. In hello **installare dettagli** finestra di dialogo, fare clic su **Avanti**.
   
    ![Verificare i dettagli di installazione][03]
8. In hello **revisione licenze** finestra di dialogo, esaminare le condizioni di hello hello dei contratti di licenza. Se si accettano i termini di hello hello dei contratti di licenza, fare clic su **accetto i termini hello hello dei contratti di licenza** e quindi fare clic su **fine**. (hello rimanenti passaggi si presuppone che si desidera accettare i termini hello hello dei contratti di licenza. Se non si desidera accettare termini hello hello dei contratti di licenza, uscire dal processo di installazione di hello.)
   
    ![Esaminare licenze][04]
   
    Scarica e installa i pacchetti necessari hello Eclipse.
   
    ![Stato dell'installazione][05]
9. Se viene richiesto di installazione di toocomplete toorestart Eclipse, fare clic su **Sì**.
   
    ![Riavviare il prompt dei comandi][06]

## <a name="see-also"></a>Vedere anche
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Toolkit di Azure per Eclipse]
  * [Novità in Azure Toolkit per Eclipse hello]
  * *L'installazione di hello Azure Toolkit for Eclipse (articolo)*
  * [Sign In istruzioni per hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
* [Toolkit di Azure per IntelliJ]
  * [Novità in Azure Toolkit per IntelliJ hello]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Sign In istruzioni per hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In istruzioni per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità in Azure Toolkit per Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
