---
title: aaaSign-nelle istruzioni per hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toosign in tooMicrosoft Azure tramite hello Azure Toolkit per IntelliJ.
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="2cf1c-103">Accesso le istruzioni per hello Azure Toolkit per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2cf1c-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="2cf1c-104">Hello Azure Toolkit per IntelliJ fornisce due metodi per la firma in tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="2cf1c-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="2cf1c-105">**Interattivo**: immesso le credenziali di Azure ogni volta che si accede in tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="2cf1c-106">**Automatizzata**: puoi creare un file di credenziali che è possibile utilizzare tooautomatically sign in tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="2cf1c-107">Hello sezioni seguenti descrivono come toouse ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="2cf1c-108">Accedi tooyour account Azure in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="2cf1c-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="2cf1c-109">toosign in tooAzure immettendo manualmente le credenziali di Azure, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2cf1c-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="2cf1c-110">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="2cf1c-111">Fare clic su **strumenti**, punto troppo**Azure**, quindi fare clic su **Azure Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando IntelliJ Azure Accedi Hello][I01]

3. <span data-ttu-id="2cf1c-113">In hello **Azure Accedi** selezionare **Interactive**, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello Azure Accedi finestra con Interactive selezionato][I02]

4. <span data-ttu-id="2cf1c-115">In hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![finestra di dialogo di accesso di Azure Hello][I03]

5. <span data-ttu-id="2cf1c-117">In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="2cf1c-119">Disconnettersi dall'account di Azure dopo che l'accesso è stato eseguito in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="2cf1c-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="2cf1c-120">Dopo aver configurato l'account utilizzando hello passaggi precedenti, verrà automaticamente disconnesso all'account Azure ogni volta che si riavvia IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="2cf1c-121">Tuttavia, se si desidera toosign senza accesso all'account Azure *senza* riavvio IntelliJ IDEA, hello seguente.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="2cf1c-122">In IntelliJ IDEA, su hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Sign Out**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![comando IntelliJ Azure Disconnetti Hello][L01]

2. <span data-ttu-id="2cf1c-124">In hello **Azure Sign Out** finestra di conferma, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![finestra Hello Azure Sign Out conferma][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="2cf1c-126">Accedi automaticamente tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="2cf1c-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="2cf1c-127">La sezione seguente illustra come creare un file di credenziali che contiene i dati dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="2cf1c-128">Dopo aver completato questo processo, Eclipse utilizza hello credenziali file tooautomatically sign in tooAzure ogni volta che si aprire il progetto.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="2cf1c-129">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="2cf1c-130">In hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando IntelliJ Azure Accedi Hello][A01]

3. <span data-ttu-id="2cf1c-132">In hello **Azure Accedi** selezionare **automatizzata**e quindi fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Hello Azure Accedi finestra con automatizzati selezionata][A02]

4. <span data-ttu-id="2cf1c-134">In hello **finestra di dialogo account di accesso Azure** finestra, immettere le credenziali di Azure e quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![finestra di dialogo di accesso di Azure Hello][A03]

5. <span data-ttu-id="2cf1c-136">In hello **creare un file di autenticazione** (finestra), le sottoscrizioni selezionare hello desidera toouse, scegliere la directory di destinazione e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![finestra di creare file di autenticazione Hello][A04]

6. <span data-ttu-id="2cf1c-138">In hello **lo stato di creazione dell'entità servizio** nella finestra di dialogo dopo i file sono stati creati correttamente, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Hello nella finestra di dialogo dello stato di creazione dell'entità servizio][A05]

7. <span data-ttu-id="2cf1c-140">In hello **Azure Accedi** finestra, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A06]

8. <span data-ttu-id="2cf1c-142">In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="2cf1c-144">Disconnettersi dall'account di Azure dopo che l'accesso è stato in modo automatico</span><span class="sxs-lookup"><span data-stu-id="2cf1c-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="2cf1c-145">Dopo aver configurato l'account utilizzando hello passaggi precedenti, hello Azure Toolkit si accede automaticamente tooyour account Azure ogni volta che si riavvia IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="2cf1c-146">Tuttavia, toosign dell'account di Azure e di evitare hello Azure Toolkit da l'accesso automatico, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2cf1c-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="2cf1c-147">In IntelliJ IDEA, su hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Sign Out**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![comando IntelliJ Azure Disconnetti Hello][L01]

2. <span data-ttu-id="2cf1c-149">In hello **Azure Sign Out** finestra di conferma, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![finestra Hello Azure Sign Out conferma][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="2cf1c-151">Accedi tooyour account Azure automaticamente utilizzando un file di credenziali esistente</span><span class="sxs-lookup"><span data-stu-id="2cf1c-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="2cf1c-152">Se si accede senza accesso all'account Azure quando si utilizza IntelliJ IDEA, è necessario utilizzare un segno di tooautomatically file credenziali esistenti in toohello account.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="2cf1c-153">tooconfigure hello Azure Toolkit per Eclipse toouse un file di credenziali esistente, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2cf1c-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="2cf1c-154">Aprire il progetto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="2cf1c-155">In hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando IntelliJ Azure Accedi Hello][A01]

3. <span data-ttu-id="2cf1c-157">In hello **Azure Accedi** selezionare **automatizzata**, quindi fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Hello Azure Accedi finestra con automatizzati selezionata][A02]

4. <span data-ttu-id="2cf1c-159">In hello **seleziona File di autenticazione** nella finestra di dialogo selezionare un file di credenziali creato in precedenza e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![finestra di dialogo Seleziona File di autenticazione Hello][A08]

5. <span data-ttu-id="2cf1c-161">In hello **Azure Accedi** finestra, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Hello Azure Accedi finestra con automatizzati selezionata][A06]

6. <span data-ttu-id="2cf1c-163">In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cf1c-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][A07]

## <a name="next-steps"></a><span data-ttu-id="2cf1c-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cf1c-165">Next steps</span></span>
<span data-ttu-id="2cf1c-166">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="2cf1c-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="2cf1c-167">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2cf1c-168">[Novità di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2cf1c-169">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2cf1c-170">[Istruzioni di accesso per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2cf1c-171">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="2cf1c-172">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2cf1c-173">[Novità di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2cf1c-174">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2cf1c-175">*Accesso le istruzioni per hello Azure Toolkit per IntelliJ* (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="2cf1c-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="2cf1c-176">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2cf1c-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="2cf1c-177">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="2cf1c-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Istruzioni di accesso per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

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
