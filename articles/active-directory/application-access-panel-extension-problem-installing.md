---
title: l'installazione dell'estensione browser hello applicazione accesso pannello aaaProblem | Documenti Microsoft
description: Come toofix comuni errori durante l'installazione dell'estensione hello accesso pannello browser
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problema durante l'installazione di estensione del browser pannello accesso applicazione hello

Hello Pannello di accesso è un portale basato sul web che consente un utente che ha un lavoro o scuola account in Azure Active Directory (Azure AD) tooview e avviare basato su cloud applicazioni che amministratore hello Azure AD ha concesso l'accesso a. Un utente con le edizioni di Azure AD consente inoltre di gruppi self-service e funzionalità di gestione di app tramite hello Pannello di accesso. Hello Pannello di accesso è separato dal portale di Azure hello e non richiede agli utenti toohave una sottoscrizione di Azure.

toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Requisiti del browser per hello Pannello di accesso

Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate. toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello. Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.

Per SSO basato su password, browser dell'utente finale di hello può essere:

-   Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive

-   Edge su Windows 10 Anniversary Edition o versioni successive 

-   Chrome in Windows 7 o versione successiva e MacOS X o versione successiva

-   Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Come tooinstall hello estensione Browser Pannello di accesso

hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:

1.  Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.

2.  Fare clic su un **applicazione password SSO** in hello Pannello di accesso.

3.  Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.

4.  Basata sul browser è il collegamento di download toohello diretto. **Aggiungere** browser tooyour di estensione hello.

5.  Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.

6.  Al termine dell'installazione, **riavviare** la sessione del browser.

7.  Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO

È anche possibile scaricare l'estensione hello per colore e bordo da collegamenti diretti hello riportati di seguito:

-   [Estensione Pannello di accesso per Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Estensione Pannello di accesso per Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Impostazione dei Criteri di gruppo per Internet Explorer

È possibile configurare criteri di gruppo che consentono di estensione del Pannello di accesso tooremotely installazione hello per Internet Explorer nei computer degli utenti.

prerequisiti di Hello includono:

-   È stato impostato [servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e sono stati aggiunti dominio tooyour di computer degli utenti.

-   È necessario disporre di hello tooedit autorizzazione "Modifica impostazioni" hello oggetto Criteri di gruppo (GPO). Per impostazione predefinita, i membri di gruppi di sicurezza seguente hello dispongono di questa autorizzazione: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners. [Altre informazioni](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

Seguire l'esercitazione hello [come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](active-directory-saas-ie-group-policy.md) per istruzioni dettagliate su come tooconfigure hello criteri di gruppo e distribuirlo toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Risoluzione dei problemi hello Pannello di accesso in Internet Explorer

Seguire hello [Troubleshoot hello estensione del Pannello di accesso per Internet Explorer](active-directory-saas-ie-troubleshooting.md) della Guida per l'accesso in uno strumento di diagnostica e istruzioni dettagliate sulla configurazione di estensione hello per Internet Explorer.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se i passaggi di risoluzione dei problemi non risolvono il problema di hello

Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:

-   ID errore di correlazione

-   UPN (indirizzo di posta elettronica dell'utente)

-   ID tenant

-   Tipo di browser

-   Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore

-   Tracce Fiddler

## <a name="next-steps"></a>Passaggi successivi
[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
