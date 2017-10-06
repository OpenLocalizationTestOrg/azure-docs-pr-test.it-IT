---
title: aaaSet un dispositivo Windows 10 con Azure AD dalle impostazioni | Documenti Microsoft
description: Viene illustrato come gli utenti possono partecipare tooAzure AD tramite il menu di impostazioni hello.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Configurazione di un dispositivo Windows 10 con Azure AD da Impostazioni
Se si ha già con Windows 7 o Windows 8 e un computer o dispositivo è stato aggiornato tooWindows 10, è possibile unire tooAzure Active Directory (Azure AD) tramite il menu di impostazioni hello.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure Active Directory dal menu Impostazioni hello
1. Da hello **avviare** menu, fare clic su hello **impostazioni** accesso.
2. Da **Impostazioni** selezionare **Sistema**->**Informazioni**->**Aggiungi ad Azure AD**.
   
   <center>
   ![Aggiungere Azure Active Directory dal menu Impostazioni hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Fare clic su **continua** nella finestra di messaggio hello aggiunta ad Azure AD.
   
   <center>
   ![Finestra di messaggio Aggiungi ad Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. Fornire le credenziali di accesso. Questa esperienza di accesso includerà tutti i passaggi di hello che sono necessari toocomplete autenticazione. Se si fa parte di un tenant federato, l'amministratore sarà con esperienza di federazione hello è ospitato dalla propria organizzazione.
   <center>
   ![Fornire le credenziali di accesso](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. Se l'organizzazione ha configurato Azure multi-Factor Authentication per l'aggiunta AD tooAzure, fornire secondo fattore di hello prima di procedere.
6. Fare clic su **Accept** su hello **consentire questa toobe dispositivo gestito** dello schermo.
7. Verrà visualizzato il messaggio hello "il dispositivo è ora tooyour unita in join dell'organizzazione in Azure AD".

## <a name="additional-information"></a>Informazioni aggiuntive
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)

