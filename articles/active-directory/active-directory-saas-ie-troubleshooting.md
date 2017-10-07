---
title: hello aaaTroubleshooting estensione del Pannello di accesso di Azure per Internet Explorer | Documenti Microsoft
description: Toouse come gruppo di criteri toodeploy hello Internet Explorer del componente aggiuntivo per il portale di My Apps hello.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="9015c-103">Risoluzione dei problemi di estensione del Pannello di accesso hello per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9015c-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="9015c-104">In questo articolo consente di risolvere i seguenti problemi hello:</span><span class="sxs-lookup"><span data-stu-id="9015c-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="9015c-105">Si sta tooaccess Impossibile App tramite il portale di My Apps hello durante l'utilizzo di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9015c-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="9015c-106">Viene visualizzato anche se si è già installato il software di hello del messaggio "Installazione Software" hello.</span><span class="sxs-lookup"><span data-stu-id="9015c-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="9015c-107">Se si è un amministratore, vedere anche: [come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="9015c-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="9015c-108">Eseguire lo strumento di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="9015c-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="9015c-109">È possibile diagnosticare i problemi di installazione di hello estensione del Pannello di accesso, scaricare ed eseguire lo strumento Diagnostica di hello Pannello di accesso:</span><span class="sxs-lookup"><span data-stu-id="9015c-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="9015c-110">Fare clic qui lo strumento di diagnostica hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="9015c-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="9015c-111">File aperti hello e premere **estrarre tutti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Pulsante Estrai tutti](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="9015c-113">Premere quindi hello **estrarre** toocontinue pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Premere Estrai](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="9015c-115">strumento hello toorun, file hello rapida denominato **AccessPanelExtensionDiagnosticTool**, quindi selezionare **Apri con > Host Microsoft Windows basato su Script**.</span><span class="sxs-lookup"><span data-stu-id="9015c-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Apri con > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="9015c-117">Verrà quindi visualizzato hello successiva finestra di diagnostica, che descrive quale potrebbe essere errato con l'installazione.</span><span class="sxs-lookup"><span data-stu-id="9015c-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Un esempio di finestra diagnostica hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="9015c-119">Fare clic su "**Sì**" toolet hello programma hello problemi che sono stati trovati.</span><span class="sxs-lookup"><span data-stu-id="9015c-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="9015c-120">toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9015c-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="9015c-121">Se non è possibile accedere le applicazioni, provare a passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="9015c-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="9015c-122">Verificare che hello che è abilitata l'estensione del Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="9015c-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="9015c-123">tooverify che hello estensione del Pannello di accesso è abilitato in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="9015c-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="9015c-124">In Internet Explorer, fare clic su hello **icona dell'ingranaggio** nell'hello angolo superiore destro della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="9015c-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="9015c-125">Selezionare quindi **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="9015c-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="9015c-126">Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="9015c-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Passare tooTools > Opzioni Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="9015c-128">Fare clic su hello **programmi** tab, quindi fare clic su hello **Gestione componenti aggiuntivi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Fare clic su Gestione componenti aggiuntivi](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="9015c-130">In questa finestra di dialogo selezionare **estensione del Pannello di accesso** e quindi fare clic su hello **abilitare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Fare clic su Abilita](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="9015c-132">toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9015c-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="9015c-133">Abilitare le estensioni per InPrivate Browsing</span><span class="sxs-lookup"><span data-stu-id="9015c-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="9015c-134">Se si utilizza la modalità InPrivate Browsing hello:</span><span class="sxs-lookup"><span data-stu-id="9015c-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="9015c-135">In Internet Explorer, fare clic su hello **icona dell'ingranaggio** nell'hello angolo superiore destro della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="9015c-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="9015c-136">Selezionare quindi **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="9015c-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="9015c-137">Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="9015c-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Un esempio di finestra diagnostica hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="9015c-139">Passare toohello **Privacy** scheda, quindi **deselezionare** hello casella **disabilitare le barre degli strumenti ed estensioni quando si avvia InPrivate Browsing**</span><span class="sxs-lookup"><span data-stu-id="9015c-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Deselezionare la casella di controllo Disabilita estensioni e barre degli strumenti all'avvio di InPrivate Browsing](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="9015c-141">toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9015c-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="9015c-142">Disinstallare l'estensione del Pannello di accesso hello</span><span class="sxs-lookup"><span data-stu-id="9015c-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="9015c-143">hello toouninstall estensione del Pannello di accesso dal computer:</span><span class="sxs-lookup"><span data-stu-id="9015c-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="9015c-144">Sulla tastiera, premere hello **tasto Windows** menu Start di hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="9015c-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="9015c-145">Quando viene aperto il menu di hello, è possibile digitare qualsiasi toodo una ricerca.</span><span class="sxs-lookup"><span data-stu-id="9015c-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="9015c-146">Digitare "Pannello di controllo" e quindi aprire hello **Pannello di controllo** quando viene visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9015c-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Cercare Pannello di controllo](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="9015c-148">In hello angolo superiore destro del Pannello di controllo di hello, modificare hello **visualizzare** opzione troppo**icone grandi**.</span><span class="sxs-lookup"><span data-stu-id="9015c-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="9015c-149">Quindi, individuare e fare clic su hello **programmi e funzionalità** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Registrazione hello vista tooshow icone grandi](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="9015c-151">Selezionare nell'elenco hello **estensione del Pannello di accesso**e fare clic su hello hello **Disinstalla** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9015c-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Fare clic su Disinstalla](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="9015c-153">È quindi possibile provare estensione hello tooinstall toosee nuovamente se il problema di hello è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="9015c-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="9015c-154">Se si verificano problemi di disinstallazione di hello estensione, è inoltre possibile rimuovere tramite hello [Microsoft Correggi](https://go.microsoft.com/?linkid=9779673) strumento.</span><span class="sxs-lookup"><span data-stu-id="9015c-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="9015c-155">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="9015c-155">Related Articles</span></span>
* [<span data-ttu-id="9015c-156">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9015c-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="9015c-157">Accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9015c-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9015c-158">Come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="9015c-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

