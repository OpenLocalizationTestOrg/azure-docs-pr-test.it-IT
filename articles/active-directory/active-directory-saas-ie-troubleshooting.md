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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Risoluzione dei problemi di estensione del Pannello di accesso hello per Internet Explorer
In questo articolo consente di risolvere i seguenti problemi hello:

* Si sta tooaccess Impossibile App tramite il portale di My Apps hello durante l'utilizzo di Internet Explorer.
* Viene visualizzato anche se si è già installato il software di hello del messaggio "Installazione Software" hello.

Se si è un amministratore, vedere anche: [come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Eseguire lo strumento di diagnostica hello
È possibile diagnosticare i problemi di installazione di hello estensione del Pannello di accesso, scaricare ed eseguire lo strumento Diagnostica di hello Pannello di accesso:

1. [Fare clic qui lo strumento di diagnostica hello toodownload.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. File aperti hello e premere **estrarre tutti** pulsante.
   
    ![Pulsante Estrai tutti](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Premere quindi hello **estrarre** toocontinue pulsante.
   
    ![Premere Estrai](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. strumento hello toorun, file hello rapida denominato **AccessPanelExtensionDiagnosticTool**, quindi selezionare **Apri con > Host Microsoft Windows basato su Script**.
   
    ![Apri con > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Verrà quindi visualizzato hello successiva finestra di diagnostica, che descrive quale potrebbe essere errato con l'installazione.
   
    ![Un esempio di finestra diagnostica hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Fare clic su "**Sì**" toolet hello programma hello problemi che sono stati trovati.
7. toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.<br />Se non è possibile accedere le applicazioni, provare a passaggi hello riportati di seguito.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Verificare che hello che è abilitata l'estensione del Pannello di accesso
tooverify che hello estensione del Pannello di accesso è abilitato in Internet Explorer:

1. In Internet Explorer, fare clic su hello **icona dell'ingranaggio** nell'hello angolo superiore destro della finestra hello. Selezionare quindi **Opzioni Internet**.<br />Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.
   
    ![Passare tooTools > Opzioni Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Fare clic su hello **programmi** tab, quindi fare clic su hello **Gestione componenti aggiuntivi** pulsante.
   
    ![Fare clic su Gestione componenti aggiuntivi](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. In questa finestra di dialogo selezionare **estensione del Pannello di accesso** e quindi fare clic su hello **abilitare** pulsante.
   
    ![Fare clic su Abilita](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.

## <a name="enable-extensions-for-inprivate-browsing"></a>Abilitare le estensioni per InPrivate Browsing
Se si utilizza la modalità InPrivate Browsing hello:

1. In Internet Explorer, fare clic su hello **icona dell'ingranaggio** nell'hello angolo superiore destro della finestra hello. Selezionare quindi **Opzioni Internet**.<br />Nelle versioni precedenti di Internet Explorer scegliere **Strumenti > Opzioni Internet**.
   
    ![Un esempio di finestra diagnostica hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Passare toohello **Privacy** scheda, quindi **deselezionare** hello casella **disabilitare le barre degli strumenti ed estensioni quando si avvia InPrivate Browsing**</p>
   
    ![Deselezionare la casella di controllo Disabilita estensioni e barre degli strumenti all'avvio di InPrivate Browsing](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave queste modifiche, chiudere ogni finestra di Internet Explorer e quindi riaprire Internet Explorer.

## <a name="uninstall-hello-access-panel-extension"></a>Disinstallare l'estensione del Pannello di accesso hello
hello toouninstall estensione del Pannello di accesso dal computer:

1. Sulla tastiera, premere hello **tasto Windows** menu Start di hello tooopen. Quando viene aperto il menu di hello, è possibile digitare qualsiasi toodo una ricerca. Digitare "Pannello di controllo" e quindi aprire hello **Pannello di controllo** quando viene visualizzato nei risultati della ricerca hello.
   
    ![Cercare Pannello di controllo](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. In hello angolo superiore destro del Pannello di controllo di hello, modificare hello **visualizzare** opzione troppo**icone grandi**. Quindi, individuare e fare clic su hello **programmi e funzionalità** pulsante.
   
    ![Registrazione hello vista tooshow icone grandi](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Selezionare nell'elenco hello **estensione del Pannello di accesso**e fare clic su hello hello **Disinstalla** pulsante.
   
    ![Fare clic su Disinstalla](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. È quindi possibile provare estensione hello tooinstall toosee nuovamente se il problema di hello è stato risolto.

Se si verificano problemi di disinstallazione di hello estensione, è inoltre possibile rimuovere tramite hello [Microsoft Correggi](https://go.microsoft.com/?linkid=9779673) strumento.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](active-directory-saas-ie-group-policy.md)

