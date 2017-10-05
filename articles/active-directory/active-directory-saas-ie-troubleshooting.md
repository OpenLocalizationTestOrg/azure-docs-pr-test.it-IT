---
title: Risoluzione dei problemi relativi all'estensione Pannello di accesso di Azure per Internet Explorer | Documentazione Microsoft
description: Come usare Criteri di gruppo per distribuire il componente aggiuntivo di Internet Explorer per il portale App personali.
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="969ca-103">Risoluzione dei problemi di Access Panel Extension per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="969ca-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="969ca-104">Questo articolo semplifica la risoluzione dei problemi seguenti:</span><span class="sxs-lookup"><span data-stu-id="969ca-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="969ca-105">Non è possibile accedere alle app tramite il portale App personali durante l'uso di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="969ca-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="969ca-106">Viene visualizzato il messaggio "Installa software" anche se è già stato installato il software.</span><span class="sxs-lookup"><span data-stu-id="969ca-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="969ca-107">Se l'utente è un amministratore, vedere anche [Come distribuire Access Panel Extension per Internet Explorer con Criteri di gruppo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="969ca-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="969ca-108">Eseguire lo strumento di diagnostica</span><span class="sxs-lookup"><span data-stu-id="969ca-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="969ca-109">È possibile eseguire la diagnostica dei problemi di installazione di Access Panel Extension scaricando ed eseguendo il relativo strumento di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="969ca-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="969ca-110">Fare clic qui per scaricare lo strumento di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="969ca-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="969ca-111">Aprire il file, quindi premere il pulsante **Estrai tutti** .</span><span class="sxs-lookup"><span data-stu-id="969ca-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Pulsante Estrai tutti](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="969ca-113">Premere il pulsante **Estrai** per continuare.</span><span class="sxs-lookup"><span data-stu-id="969ca-113">Then press the **Extract** button to continue.</span></span>
   
    ![Premere Estrai](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="969ca-115">Per eseguire lo strumento, fare doppio clic con il pulsante destro del mouse sul file denominato **AccessPanelExtensionDiagnosticTool** e quindi selezionare **Apri con > Microsoft Windows Based Script Host**.</span><span class="sxs-lookup"><span data-stu-id="969ca-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Apri con > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="969ca-117">Viene quindi visualizzata la finestra di diagnostica seguente, contenente la descrizione dei possibili errori dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="969ca-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Esempio della finestra di diagnostica](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="969ca-119">Fare clic su "**Sì**" per consentire al programma di risolvere i problemi rilevati.</span><span class="sxs-lookup"><span data-stu-id="969ca-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="969ca-120">Per salvare queste modifiche, chiudere tutte le finestre di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="969ca-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="969ca-121">Se risulta ancora impossibile accedere alle applicazioni, attenersi alla procedura riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="969ca-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="969ca-122">Verificare che Access Panel Extension sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="969ca-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="969ca-123">Per verificare se Access Panel Extension è abilitato in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="969ca-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="969ca-124">In Internet Explorer fare clic sull'**icona a forma di ingranaggio** nell'angolo superiore destro della finestra.</span><span class="sxs-lookup"><span data-stu-id="969ca-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="969ca-125">Selezionare quindi **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="969ca-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="969ca-126">Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="969ca-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Accedere a Strumenti > Opzioni Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="969ca-128">Fare clic sulla scheda **Programmi** e quindi sul pulsante **Gestione componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="969ca-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Fare clic su Gestione componenti aggiuntivi](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="969ca-130">In questa finestra di dialogo selezionare **Access Panel Extension** e quindi fare clic sul pulsante **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="969ca-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Fare clic su Abilita](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="969ca-132">Per salvare queste modifiche, chiudere tutte le finestre di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="969ca-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="969ca-133">Abilitare le estensioni per InPrivate Browsing</span><span class="sxs-lookup"><span data-stu-id="969ca-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="969ca-134">Se si usa la modalità InPrivate Browsing:</span><span class="sxs-lookup"><span data-stu-id="969ca-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="969ca-135">In Internet Explorer fare clic sull'**icona a forma di ingranaggio** nell'angolo superiore destro della finestra.</span><span class="sxs-lookup"><span data-stu-id="969ca-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="969ca-136">Selezionare quindi **Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="969ca-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="969ca-137">Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.</span><span class="sxs-lookup"><span data-stu-id="969ca-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Esempio della finestra di diagnostica](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="969ca-139">Passare alla scheda **Privacy** e **deselezionare** la casella di controllo **Disabilita estensioni e barre degli strumenti all'avvio di InPrivate Browsing**</span><span class="sxs-lookup"><span data-stu-id="969ca-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Deselezionare la casella di controllo Disabilita estensioni e barre degli strumenti all'avvio di InPrivate Browsing](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="969ca-141">Per salvare queste modifiche, chiudere tutte le finestre di Internet Explorer e quindi riaprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="969ca-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="969ca-142">Disinstallare Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="969ca-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="969ca-143">Per disinstallare Access Panel Extension dal computer:</span><span class="sxs-lookup"><span data-stu-id="969ca-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="969ca-144">Sulla tastiera premere il **tasto Windows** per aprire il menu Start.</span><span class="sxs-lookup"><span data-stu-id="969ca-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="969ca-145">Quando il menu è aperto, è possibile digitare un testo qualsiasi per eseguire una ricerca.</span><span class="sxs-lookup"><span data-stu-id="969ca-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="969ca-146">Digitare "Pannello di controllo" e quindi aprire il **Pannello di controllo** quando viene visualizzato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="969ca-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Cercare Pannello di controllo](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="969ca-148">Nell'angolo in alto a destra del Pannello di controllo modificare l'opzione **Visualizza per** impostandola su **Icone grandi**.</span><span class="sxs-lookup"><span data-stu-id="969ca-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="969ca-149">Individuare e fare clic sul pulsante **Programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="969ca-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Modificare la visualizzazione in modo da visualizzare le icone grandi](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="969ca-151">Nell'elenco selezionare **Access Panel Extension** e quindi scegliere il pulsante **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="969ca-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Fare clic su Disinstalla](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="969ca-153">È quindi possibile provare a installare di nuovo l'estensione per verificare se il problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="969ca-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="969ca-154">Se si verificano problemi durante la disinstallazione dell'estensione, è possibile rimuoverla anche usando lo strumento [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) .</span><span class="sxs-lookup"><span data-stu-id="969ca-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="969ca-155">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="969ca-155">Related Articles</span></span>
* [<span data-ttu-id="969ca-156">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="969ca-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="969ca-157">Accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="969ca-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="969ca-158">Come distribuire l'estensione Pannello di accesso per Internet Explorer con Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="969ca-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

