---
title: Istruzioni di accesso per Azure Toolkit for IntelliJ | Microsoft Docs
description: Informazioni su come accedere a Microsoft Azure con Azure Toolkit for IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="7ab5f-103">Istruzioni di accesso per Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7ab5f-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="7ab5f-104">Azure Toolkit for IntelliJ consente di accedere all'account Azure in due metodi diversi:</span><span class="sxs-lookup"><span data-stu-id="7ab5f-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="7ab5f-105">**Interactive** (Interattivo): immettere le credenziali di Azure ogni volta che si accede all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="7ab5f-106">**Automated** (Automatico): si crea un file di credenziali che è possibile usare per accedere automaticamente all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="7ab5f-107">Le sezioni seguenti descrivono come usare ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="7ab5f-108">Accedere all'account Azure in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="7ab5f-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="7ab5f-109">Per accedere ad Azure immettendo manualmente le credenziali, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="7ab5f-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="7ab5f-110">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="7ab5f-111">Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Azure Sign In** (Accesso ad Azure).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Comando di accesso ad Azure in IntelliJ][I01]

3. <span data-ttu-id="7ab5f-113">Quando viene visualizzata la finestra **Azure Sign In** (Accesso ad Azure), selezionare **Interactive** (Interattivo) e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Finestra di accesso in Azure con opzione interattiva selezionata][I02]

4. <span data-ttu-id="7ab5f-115">Nella finestra di dialogo **Azure Log In** (Accedi ad Azure) immettere le credenziali di Azure e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][I03]

5. <span data-ttu-id="7ab5f-117">Nella finestra di dialogo **Select Subscriptions** (Seleziona sottoscrizioni) selezionare le sottoscrizioni da usare e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="7ab5f-119">Disconnettersi dall'account di Azure dopo che l'accesso è stato eseguito in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="7ab5f-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="7ab5f-120">Dopo avere configurato l'account usando i passaggi precedenti, la disconnessione dall'account Azure verrà eseguita automaticamente a ogni riavvio di IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="7ab5f-121">Se tuttavia si vuole disconnettersi dall'account di Azure *senza* riavviare IntelliJ IDEA, eseguire queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="7ab5f-122">In IntelliJ IDEA fare clic su **Tools** (Strumenti), puntare su **Azure** e quindi fare clic su **Azure Sign Out** (Disconnessione da Azure).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Comando di disconnessione da Azure in IntelliJ][L01]

2. <span data-ttu-id="7ab5f-124">Nella finestra di conferma **Azure Sign Out** (Disconnessione da Azure) fare clic su **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Finestra di conferma della disconnessione da Azure][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="7ab5f-126">Accedere automaticamente all'account Azure</span><span class="sxs-lookup"><span data-stu-id="7ab5f-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="7ab5f-127">La sezione seguente illustra come creare un file di credenziali che contiene i dati dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="7ab5f-128">Dopo avere completato questo processo, Eclipse usa il file di credenziali per l'accesso ad Azure ogni volta che si apre il progetto.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="7ab5f-129">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="7ab5f-130">Fare clic su **Tools** (Strumenti), puntare su **Azure** e quindi fare clic su **Azure Sign In** (Accesso ad Azure).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Comando di accesso ad Azure in IntelliJ][A01]

3. <span data-ttu-id="7ab5f-132">Nella finestra **Azure Sign In** (Accesso ad Azure) selezionare **Automated** (Automatico) e quindi fare clic su **New** (Nuovo).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Finestra di accesso ad Azure con opzione automatica selezionata][A02]

4. <span data-ttu-id="7ab5f-134">Nella finestra **Azure Log In** (Accedi ad Azure) immettere le credenziali di Azure e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A03]

5. <span data-ttu-id="7ab5f-136">Nella finestra **Create authentication files** (Crea file di autenticazione) selezionare le sottoscrizioni da usare, scegliere la directory di destinazione e quindi fare cli su **Start** (Avvio).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Finestra di creazione dei file di autenticazione][A04]

6. <span data-ttu-id="7ab5f-138">Nella finestra di dialogo **Service Principal Creation Status** (Stato creazione entità servizio) fare clic su **OK** al termine della creazione dei file.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Finestra di dialogo sullo stato di creazione dell'entità servizio][A05]

7. <span data-ttu-id="7ab5f-140">Nella finestra **Azure Sign In** (Accesso ad Azure) fare clic su **Sign in** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A06]

8. <span data-ttu-id="7ab5f-142">Nella finestra di dialogo **Select Subscriptions** (Seleziona sottoscrizioni) selezionare le sottoscrizioni da usare e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="7ab5f-144">Disconnettersi dall'account di Azure dopo che l'accesso è stato in modo automatico</span><span class="sxs-lookup"><span data-stu-id="7ab5f-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="7ab5f-145">Dopo avere configurato l'account usando i passaggi precedenti, Azure Toolkit esegue automaticamente la connessione all'account Azure a ogni riavvio di IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="7ab5f-146">Per disconnettersi dall'account Azure e impedire l'accesso automatico eseguito da Azure Toolkit, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="7ab5f-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="7ab5f-147">In IntelliJ IDEA fare clic su **Tools** (Strumenti), puntare su **Azure** e quindi fare clic su **Azure Sign Out** (Disconnessione da Azure).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Comando di disconnessione da Azure in IntelliJ][L01]

2. <span data-ttu-id="7ab5f-149">Nella finestra di conferma **Azure Sign Out** (Disconnessione da Azure) fare clic su **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Finestra di conferma della disconnessione da Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="7ab5f-151">Accedere al proprio account Azure automaticamente usando un file di credenziali esistente</span><span class="sxs-lookup"><span data-stu-id="7ab5f-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="7ab5f-152">Se si esegue la disconnessione dall'account Azure quando si usa IntelliJ IDEA, è necessario usare un file esistente di credenziali per accedere di nuovo automaticamente all'account.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="7ab5f-153">Per configurare Azure Toolkit for Eclipse in modo da usare un file di credenziali esistente, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="7ab5f-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="7ab5f-154">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="7ab5f-155">Fare clic su **Tools** (Strumenti), puntare su **Azure** e quindi fare clic su **Azure Sign In** (Accesso ad Azure).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Comando di accesso ad Azure in IntelliJ][A01]

3. <span data-ttu-id="7ab5f-157">Nella finestra **Azure Sign In** (Accesso ad Azure) selezionare **Automated** (Automatico) e quindi fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Finestra di accesso ad Azure con opzione automatica selezionata][A02]

4. <span data-ttu-id="7ab5f-159">Nella finestra di dialogo **Select Authenticated File** (Seleziona file autenticazione) selezionare un file di credenziali creato in precedenza e quindi fare clic su **Select** (Seleziona).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Finestra di dialogo di selezione del file di autenticazione][A08]

5. <span data-ttu-id="7ab5f-161">Nella finestra **Azure Sign In** (Accesso ad Azure) fare clic su **Sign in** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="7ab5f-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Finestra di accesso ad Azure con opzione automatica selezionata][A06]

6. <span data-ttu-id="7ab5f-163">Nella finestra di dialogo **Select Subscriptions** (Seleziona sottoscrizioni) selezionare le sottoscrizioni da usare e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ab5f-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="next-steps"></a><span data-ttu-id="7ab5f-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ab5f-165">Next steps</span></span>
<span data-ttu-id="7ab5f-166">Per ulteriori informazioni sui Toolkit di Azure per gli IDE di Java, consultare i seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="7ab5f-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="7ab5f-167">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7ab5f-168">[Novità di Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7ab5f-169">[Installare il Toolkit di Azure per Eclipse.]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7ab5f-170">[Istruzioni di accesso per Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7ab5f-171">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="7ab5f-172">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7ab5f-173">[Novità di Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7ab5f-174">[Installazione del Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7ab5f-175">*Istruzioni di accesso per Azure Toolkit for IntelliJ* (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="7ab5f-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="7ab5f-176">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7ab5f-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="7ab5f-177">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="7ab5f-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="7ab5f-178">[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="7ab5f-179">[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="7ab5f-180">[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="7ab5f-181">[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="7ab5f-182">[Installare il Toolkit di Azure per Eclipse.]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="7ab5f-183">[Installazione del Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="7ab5f-184">[Istruzioni di accesso per Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="7ab5f-185">[Novità di Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="7ab5f-186">[Novità di Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="7ab5f-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="7ab5f-187">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="7ab5f-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="7ab5f-188">[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="7ab5f-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
