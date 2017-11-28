---
title: aaaSign In istruzioni per hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toosign in Microsoft Azure tramite hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="efece-103">Azure Sign In istruzioni per hello Azure Toolkit per Eclipse</span><span class="sxs-lookup"><span data-stu-id="efece-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="efece-104">Hello Azure Toolkit per Eclipse fornisce due metodi per la firma nell'account di Azure:</span><span class="sxs-lookup"><span data-stu-id="efece-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="efece-105">**Interattivo**: le credenziali di Azure vengono immesse ogni volta che si accede all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="efece-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="efece-106">**Automatizzata** : quando si utilizza questo metodo, si creerà un file di credenziali che contiene i dati dell'entità servizio, dopo il quale è possibile utilizzare hello credenziali file tooautomatically accesso all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="efece-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="efece-107">Hello in hello le sezioni seguenti viene descritta la modalità toouse ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="efece-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="efece-108">Accesso all'account Azure in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="efece-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="efece-109">Hello passaggi seguenti verranno illustrato come toosign in Azure immettendo manualmente le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="efece-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="efece-110">Aprire il progetto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="efece-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="efece-111">Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="efece-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu di Eclipse per l'accesso ad Azure][I01]

1. <span data-ttu-id="efece-113">Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **Interactive**, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="efece-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Finestra di dialogo di accesso][I02]

1. <span data-ttu-id="efece-115">Quando hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="efece-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][I03]

1. <span data-ttu-id="efece-117">Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efece-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="efece-119">Disconnessione dell'account di Azure quando l'accesso è stato eseguito in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="efece-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="efece-120">Dopo aver configurato i passaggi di hello nella sezione precedente di hello, verrà disconnesso automaticamente all'account Azure a ogni avvio di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="efece-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="efece-121">Tuttavia, se si desidera toosign senza accesso all'account di Azure senza dover riavviare Eclipse, utilizzare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="efece-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="efece-122">In Eclipse fare clic su **Tools** (Strumenti), su **Azure** e quindi su **Sign Out** (Disconnetti).</span><span class="sxs-lookup"><span data-stu-id="efece-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu di Eclipse per la disconnessione da Azure][L01]

1. <span data-ttu-id="efece-124">Quando hello **Azure Sign Out** viene visualizzata la finestra di dialogo, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="efece-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Finestra di dialogo di disconnessione][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="efece-126">Firma automaticamente all'account Azure e la creazione di credenziali di un file toouse in hello future</span><span class="sxs-lookup"><span data-stu-id="efece-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="efece-127">Hello passaggi seguenti verranno illustrati la creazione di un file di credenziali che contiene i dati dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="efece-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="efece-128">Dopo aver completato questi passaggi, sarà Eclipse automaticamente si in Azure ogni volta che si usa hello credenziali file tooautomatically sign aprire il progetto.</span><span class="sxs-lookup"><span data-stu-id="efece-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="efece-129">Aprire il progetto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="efece-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="efece-130">Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="efece-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu di Eclipse per l'accesso ad Azure][A01]

1. <span data-ttu-id="efece-132">Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **automatizzata**, quindi fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="efece-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Finestra di dialogo di accesso][A02]

1. <span data-ttu-id="efece-134">Quando hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="efece-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A03]

1. <span data-ttu-id="efece-136">Quando hello **creare file di autenticazione** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello desidera toouse, scegliere la directory di destinazione e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="efece-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A04]

1. <span data-ttu-id="efece-138">Hello **dell'entità servizio Creatation stato** verrà visualizzata la finestra di dialogo, dopo che sono stati creati i file, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efece-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Finestra di dialogo Stato creazione entità servizio][A05]

1. <span data-ttu-id="efece-140">Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="efece-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A06]

1. <span data-ttu-id="efece-142">Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efece-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="efece-144">Disconnessione dell'account Azure quando l'accesso è stato eseguito in modo automatico</span><span class="sxs-lookup"><span data-stu-id="efece-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="efece-145">Dopo aver configurato i passaggi di hello nella sezione precedente di hello, hello Azure Toolkit comporta l'accesso automatico all'account Azure a ogni avvio di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="efece-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="efece-146">Tuttavia, toosign dell'account di Azure e di impedire l'accesso automatico, utilizzare hello, alla procedura seguente hello Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="efece-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="efece-147">In Eclipse fare clic su **Tools** (Strumenti), su **Azure** e quindi su **Sign Out** (Disconnetti).</span><span class="sxs-lookup"><span data-stu-id="efece-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu di Eclipse per la disconnessione da Azure][L01]

1. <span data-ttu-id="efece-149">Quando hello **Azure Sign Out** viene visualizzata la finestra di dialogo, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="efece-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Finestra di dialogo di disconnessione][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="efece-151">Accesso automatico all'account Azure usando un file di credenziali già creato</span><span class="sxs-lookup"><span data-stu-id="efece-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="efece-152">Se si accede all'esterno di Azure quando si usa Eclipse, è necessario tooreconfigure hello Azure Toolkit per Eclipse toouse un file di credenziali che è stato creato prima di poter firmare automaticamente nell'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="efece-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="efece-153">Hello passaggi seguenti verranno illustrati configurazione hello Azure Toolkit toouse un file di credenziali esistente.</span><span class="sxs-lookup"><span data-stu-id="efece-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="efece-154">Aprire il progetto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="efece-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="efece-155">Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="efece-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu di Eclipse per l'accesso ad Azure][A01]

1. <span data-ttu-id="efece-157">Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **automatizzata**, quindi fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="efece-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Finestra di dialogo di accesso][A02]

1. <span data-ttu-id="efece-159">Quando hello **selezionare File autenticato** viene visualizzata la finestra di dialogo, selezionare un file di credenziali creato in precedenza e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="efece-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Finestra di dialogo di accesso][A08]

1. <span data-ttu-id="efece-161">Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="efece-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Finestra di dialogo di accesso ad Azure][A06]

1. <span data-ttu-id="efece-163">Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="efece-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="see-also"></a><span data-ttu-id="efece-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="efece-165">See Also</span></span>
<span data-ttu-id="efece-166">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="efece-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="efece-167">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="efece-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="efece-168">[Novità in Azure Toolkit per Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="efece-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="efece-169">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="efece-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="efece-170">*Sign In istruzioni per hello Azure Toolkit for Eclipse (articolo)*</span><span class="sxs-lookup"><span data-stu-id="efece-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="efece-171">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="efece-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="efece-172">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="efece-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="efece-173">[Novità in Azure Toolkit per IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="efece-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="efece-174">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="efece-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="efece-175">[Sign In istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="efece-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="efece-176">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="efece-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="efece-177">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="efece-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità in Azure Toolkit per Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
