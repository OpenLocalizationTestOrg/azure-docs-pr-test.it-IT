---
title: Aggiungere un dispositivo personale all'organizzazione| Documentazione Microsoft
description: Descrive come gli utenti possono registrare i dispositivi Windows 10 personali nella rete aziendale e fornisce i passaggi di distribuzione per uno scenario BYOD.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a>Aggiunta di un dispositivo personale all'organizzazione
## <a name="to-join-a-windows-10-device-to-your-organization"></a>Per aggiungere un dispositivo Windows 10 personale all'organizzazione
1. Nel menu **Start** selezionare **Impostazioni**.
2. Selezionare **Account**, quindi fare clic su **Account**.
3. Fare clic su **Aggiungi account aziendale o dell'istituto di istruzione**e quindi digitare l'account dell'organizzazione.
4. Nella pagina di accesso per l'organizzazione, immettere il nome utente e la password e quindi fare clic su **OK**.
5. Verrà richiesto di effettuare una verifica Multi-Factor Authentication. La verifica può essere configurata da un amministratore IT.
6. Azure Active Directory (Azure AD) controlla se il dispositivo richiede la registrazione per la gestione di dispositivi mobili.
7. Windows registra il dispositivo nella directory dell'organizzazione in Azure AD e lo inserisce nella gestione dei dispositivi mobili, se appropriato.
8. Se si è un utente gestito, Windows visualizza il desktop tramite l'accesso automatico.
9. Se si è un utente federato, viene visualizzata una schermata di accesso di Windows che consente di immettere le proprie credenziali.

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettere dispositivi appartenenti a un dominio ad Azure AD per usufruire di Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

