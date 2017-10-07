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
# <a name="installing-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="b3d5d-103">L'installazione di hello Azure Toolkit per Eclipse</span><span class="sxs-lookup"><span data-stu-id="b3d5d-103">Installing hello Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="b3d5d-104">Hello Azure Toolkit per Eclipse fornisce modelli e le funzionalità che consentono di tooeasily creare, sviluppare, testare e distribuire applicazioni Azure mediante l'ambiente di sviluppo Eclipse hello.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-104">hello Azure Toolkit for Eclipse provides templates and functionality that allow you tooeasily create, develop, test, and deploy Azure applications using hello Eclipse development environment.</span></span> <span data-ttu-id="b3d5d-105">Hello Azure Toolkit per Eclipse è un progetto Open Source.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-105">hello Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="b3d5d-106">codice sorgente Hello è disponibile in hello licenza MIT da <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-106">hello source code is available under hello MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="b3d5d-107">Hello alla procedura seguente viene illustrato come tooinstall hello Azure Toolkit per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-107">hello following steps show you how tooinstall hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="b3d5d-108">tooinstall hello Azure Toolkit per Eclipse</span><span class="sxs-lookup"><span data-stu-id="b3d5d-108">tooinstall hello Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="b3d5d-109">Avviare Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-109">Start Eclipse.</span></span>
2. <span data-ttu-id="b3d5d-110">Fare clic su hello **Guida** menu e quindi fare clic su **installa nuovo Software**, come illustrato nella seguente figura hello.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-110">Click hello **Help** menu, and then click **Install New Software**, as shown in hello following illustration.</span></span>
   
    ![L'installazione di hello Azure Toolkit per Eclipse][01]
3. <span data-ttu-id="b3d5d-112">In hello **Software disponibile** finestra di dialogo, all'interno di hello **utilizzano** nella casella di testo `http://dl.microsoft.com/eclipse` seguita da hello **invio** chiave.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-112">In hello **Available Software** dialog, within hello **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by hello **Enter** key.</span></span>
4. <span data-ttu-id="b3d5d-113">In hello **nome** controllo riquadro **Azure Toolkit per Eclipse**e deselezionare **contatta tutti i siti di aggiornamento durante l'installazione software toofind necessari**.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-113">In hello **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install toofind required software**.</span></span> <span data-ttu-id="b3d5d-114">Verrà visualizzata una schermata simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3d5d-114">Your screen should appear similar toohello following:</span></span>
   
    ![L'installazione di hello Azure Toolkit per Eclipse][02]
5. <span data-ttu-id="b3d5d-116">Se si espande hello **Azure Toolkit per Eclipse**, verrà visualizzato hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b3d5d-116">If you expand hello **Azure Toolkit for Eclipse**, you will see hello following items:</span></span>
   
   * <span data-ttu-id="b3d5d-117">**Plug-in Insights di applicazione per Java**: questo componente consente di servizi di Azure toouse telemetria analisi e registrazione per le applicazioni e istanze del server.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-117">**Application Insights Plugin for Java**: This component allows you toouse Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="b3d5d-118">**Azure Access Control Services Filter**: questo componente fornisce il supporto per l'autenticazione degli utenti dell'applicazione con il servizio ACS di Azure, consentendo scenari single sign-on e l'esternalizzazione di logica di identità dall'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from hello application.</span></span>
   * <span data-ttu-id="b3d5d-119">**Plug-in comune Azure**: questo componente fornisce funzionalità comuni di hello necessari per altri componenti del toolkit.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-119">**Azure Common Plugin**: This component provides hello common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="b3d5d-120">**Esplora Azure per Eclipse**: questo componente fornisce funzionalità comuni di hello necessari per altri componenti del toolkit.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-120">**Azure Explorer for Eclipse**: This component provides hello common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="b3d5d-121">**Plug-in Azure per Eclipse con Java**: questo componente fornisce il supporto per lo sviluppo di progetti che consentono di compilare, testare e distribuire le applicazioni Java per cloud di Microsoft Azure hello in Eclipse e tramite riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for hello Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="b3d5d-122">**Plug-in App Web Azure con Java**: questo componente fornisce il supporto per la distribuzione di contenitori di App Web di Azure tooMicrosoft applicazioni web Java.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications tooMicrosoft Azure Web App containers.</span></span>
   * <span data-ttu-id="b3d5d-123">**Microsoft JDBC Driver 4.2 per SQL Server**: questo componente fornisce l'API JDBC per SQL Server e il database SQL di Microsoft Azure per Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="b3d5d-124">**Package for Apache Qpid Client Libraries for JMS**: questo componente fornisce il componente client JMS hello da hello Apache Qpid progetto tooenable di AMQP toouse di applicazione messaggistica in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides hello JMS client component from hello Apache Qpid project tooenable your application toouse AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="b3d5d-125">**Package for Microsoft Azure Libraries for Java**: questo componente fornisce le API per accedere ai servizi di Microsoft Azure, ad esempio archiviazione, bus di servizio, runtime del servizio e così via.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="b3d5d-126">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-126">Click **Next**.</span></span> <span data-ttu-id="b3d5d-127">(Se si verificano ritardi insoliti durante l'installazione di hello toolkit, assicurarsi che **contatta tutti i siti di aggiornamento durante l'installazione software toofind necessari** è deselezionata.)</span><span class="sxs-lookup"><span data-stu-id="b3d5d-127">(If you experience unusual delays when installing hello toolkit, ensure that **Contact all update sites during install toofind required software** is unchecked.)</span></span>
7. <span data-ttu-id="b3d5d-128">In hello **installare dettagli** finestra di dialogo, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-128">In hello **Install Details** dialog, click **Next**.</span></span>
   
    ![Verificare i dettagli di installazione][03]
8. <span data-ttu-id="b3d5d-130">In hello **revisione licenze** finestra di dialogo, esaminare le condizioni di hello hello dei contratti di licenza.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-130">In hello **Review Licenses** dialog, review hello terms of hello license agreements.</span></span> <span data-ttu-id="b3d5d-131">Se si accettano i termini di hello hello dei contratti di licenza, fare clic su **accetto i termini hello hello dei contratti di licenza** e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-131">If you accept hello terms of hello license agreements, click **I accept hello terms of hello license agreements** and then click **Finish**.</span></span> <span data-ttu-id="b3d5d-132">(hello rimanenti passaggi si presuppone che si desidera accettare i termini hello hello dei contratti di licenza.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-132">(hello remaining steps assume you do accept hello terms of hello license agreements.</span></span> <span data-ttu-id="b3d5d-133">Se non si desidera accettare termini hello hello dei contratti di licenza, uscire dal processo di installazione di hello.)</span><span class="sxs-lookup"><span data-stu-id="b3d5d-133">If you do not accept hello terms of hello license agreements, exit hello installation process.)</span></span>
   
    ![Esaminare licenze][04]
   
    <span data-ttu-id="b3d5d-135">Scarica e installa i pacchetti necessari hello Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-135">Eclipse will download and install hello requisite packages.</span></span>
   
    ![Stato dell'installazione][05]
9. <span data-ttu-id="b3d5d-137">Se viene richiesto di installazione di toocomplete toorestart Eclipse, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="b3d5d-137">If prompted toorestart Eclipse toocomplete installation, click **Yes**.</span></span>
   
    ![Riavviare il prompt dei comandi][06]

## <a name="see-also"></a><span data-ttu-id="b3d5d-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b3d5d-139">See Also</span></span>
<span data-ttu-id="b3d5d-140">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="b3d5d-140">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="b3d5d-141">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3d5d-142">[Novità in Azure Toolkit per Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-142">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3d5d-143">*L'installazione di hello Azure Toolkit for Eclipse (articolo)*</span><span class="sxs-lookup"><span data-stu-id="b3d5d-143">*Installing hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="b3d5d-144">[Sign In istruzioni per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-144">[Sign In Instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3d5d-145">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="b3d5d-146">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3d5d-147">[Novità in Azure Toolkit per IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-147">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3d5d-148">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-148">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3d5d-149">[Sign In istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-149">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3d5d-150">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3d5d-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="b3d5d-151">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="b3d5d-151">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

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
