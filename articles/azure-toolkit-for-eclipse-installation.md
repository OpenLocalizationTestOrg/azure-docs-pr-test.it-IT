---
title: Installazione di Azure Toolkit for Eclipse | Microsoft Docs
description: Informazioni su come installare Azure Toolkit for Eclipse.
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
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="69b60-103">Installare il Toolkit di Azure per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69b60-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="69b60-104">Il Toolkit di Azure per Eclipse offre modelli e funzionalità che permettono di creare, sviluppare, testare e distribuire con facilità applicazioni di Azure tramite l'ambiente di sviluppo Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69b60-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="69b60-105">Il Toolkit di Azure per Eclipse è un progetto open source.</span><span class="sxs-lookup"><span data-stu-id="69b60-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="69b60-106">Il codice sorgente è disponibile in base alla licenza MIT da <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="69b60-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="69b60-107">La procedura seguente mostra come installare il Toolkit di Azure per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69b60-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="69b60-108">Per installare il Toolkit di Azure per Eclipse</span><span class="sxs-lookup"><span data-stu-id="69b60-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="69b60-109">Avviare Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69b60-109">Start Eclipse.</span></span>
2. <span data-ttu-id="69b60-110">Fare clic sul menu **Help** (Guida), quindi su **Install New Software** (Installa nuovo software), come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="69b60-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![Installare il Toolkit di Azure per Eclipse.][01]
3. <span data-ttu-id="69b60-112">Nella finestra di dialogo **Available Software** (Software disponibile), nella casella di testo **Work with** (Usa), digitare `http://dl.microsoft.com/eclipse` e quindi premere il tasto **Invio**.</span><span class="sxs-lookup"><span data-stu-id="69b60-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="69b60-113">Nel riquadro **Nome**, controllare il **Toolkit di Azure per Eclipse**, e deselezionare **Contattare tutti i siti di aggiornamento durante l'installazione per trovare il software richiesto**.</span><span class="sxs-lookup"><span data-stu-id="69b60-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="69b60-114">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="69b60-114">Your screen should appear similar to the following:</span></span>
   
    ![Installare il Toolkit di Azure per Eclipse.][02]
5. <span data-ttu-id="69b60-116">Espandendo **Azure Toolkit for Eclipse**, verranno visualizzate le voci seguenti:</span><span class="sxs-lookup"><span data-stu-id="69b60-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="69b60-117">**Plug-in di Application Insights per Java**: questo componente consente di usare servizi di analisi e di registrazione dei dati di telemetria di Azure per le applicazioni e le istanze del server.</span><span class="sxs-lookup"><span data-stu-id="69b60-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="69b60-118">**Azure Access Control Services Filter**: questo componente supporta l'autenticazione degli utenti dell'applicazione ad ACS di Azure, offrendo scenari Single Sign-On ed esternalizzando la logica delle identità dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69b60-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="69b60-119">**Plug-in Azure Common**: questo componente offre le funzionalità comuni necessarie per gli altri componenti del toolkit.</span><span class="sxs-lookup"><span data-stu-id="69b60-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="69b60-120">**Azure Explorer for Eclipse**: questo componente offre le funzionalità comuni necessarie per gli altri componenti del toolkit.</span><span class="sxs-lookup"><span data-stu-id="69b60-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="69b60-121">**Azure Plugin for Eclipse with Java**: questo componente supporta lo sviluppo di progetti per compilare, testare e distribuire le applicazioni Java per il cloud di Microsoft Azure in Eclipse e tramite riga di comando.</span><span class="sxs-lookup"><span data-stu-id="69b60-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="69b60-122">**Azure Web Apps Plugin for Java**: questo componente supporta la distribuzione di applicazioni Web Java in contenitori App Web di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="69b60-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="69b60-123">**Microsoft JDBC Driver 4.2 per SQL Server**: questo componente fornisce l'API JDBC per SQL Server e il database SQL di Microsoft Azure per Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="69b60-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="69b60-124">**Package for Apache Qpid Client Libraries for JMS**: questo componente fornisce il componente client JSMS dal progetto Apache Qpid per consentire all'applicazione di usare la messaggistica basata su AMQP in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="69b60-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="69b60-125">**Package for Microsoft Azure Libraries for Java**: questo componente fornisce le API per accedere ai servizi di Microsoft Azure, ad esempio archiviazione, bus di servizio, runtime del servizio e così via.</span><span class="sxs-lookup"><span data-stu-id="69b60-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="69b60-126">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="69b60-126">Click **Next**.</span></span> <span data-ttu-id="69b60-127">(Se si verificano ritardi insoliti durante l'installazione del toolkit, assicurarsi che **Contattare tutti i siti di aggiornamento durante l'installazione per trovare il software richiesto** sia deselezionato.)</span><span class="sxs-lookup"><span data-stu-id="69b60-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="69b60-128">Nella finestra di dialogo **Install Details** fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="69b60-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Verificare i dettagli di installazione][03]
8. <span data-ttu-id="69b60-130">Nella finestra di dialogo **Esaminare licenze** , rivedere le condizioni dei contratti di licenza.</span><span class="sxs-lookup"><span data-stu-id="69b60-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="69b60-131">Se si accettano le condizioni dei contratti di licenza, fare clic su **I accept the terms of the license agreements** (Accetto le condizioni dei contratti di licenza) e quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="69b60-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="69b60-132">(I passaggi rimanenti suppongono che le condizioni dei contratti di licenza siano state accettate.</span><span class="sxs-lookup"><span data-stu-id="69b60-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="69b60-133">Se non si accettano le condizioni dei contratti di licenza, uscire dal processo di installazione.)</span><span class="sxs-lookup"><span data-stu-id="69b60-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Esaminare licenze][04]
   
    <span data-ttu-id="69b60-135">Eclipse scarica e installa i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="69b60-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Stato dell'installazione][05]
9. <span data-ttu-id="69b60-137">Se viene richiesto di riavviare Eclipse per completare l'installazione, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="69b60-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![Riavviare il prompt dei comandi][06]

## <a name="see-also"></a><span data-ttu-id="69b60-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69b60-139">See Also</span></span>
<span data-ttu-id="69b60-140">Per ulteriori informazioni sui Toolkit di Azure per gli IDE di Java, consultare i seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="69b60-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="69b60-141">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="69b60-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="69b60-142">[Novità di Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="69b60-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="69b60-143">*Installazione di Azure Toolkit per Eclipse (questo articolo)*</span><span class="sxs-lookup"><span data-stu-id="69b60-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="69b60-144">[Istruzioni di accesso ad Azure per il Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="69b60-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="69b60-145">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="69b60-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="69b60-146">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="69b60-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="69b60-147">[Novità del Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="69b60-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="69b60-148">[Installazione del Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="69b60-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="69b60-149">[Istruzioni di accesso ad Azure per il Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="69b60-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="69b60-150">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="69b60-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="69b60-151">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="69b60-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="69b60-152">[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="69b60-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="69b60-153">[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="69b60-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="69b60-154">[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="69b60-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="69b60-155">[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="69b60-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="69b60-156">[Installazione del Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="69b60-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="69b60-157">[Istruzioni di accesso ad Azure per il Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="69b60-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="69b60-158">[Istruzioni di accesso ad Azure per il Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="69b60-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="69b60-159">[Novità di Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="69b60-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="69b60-160">[Novità del Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="69b60-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="69b60-161">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="69b60-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
