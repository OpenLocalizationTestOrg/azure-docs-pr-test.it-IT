---
title: "autenticazione a più fattori toorequire aaaHow | Documenti Microsoft"
description: "Informazioni su come toorequire autenticazione a più fattori (MFA) per le identità con l'estensione di Azure Active Directory Privileged Identity Management hello con privilegi."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Come toorequire autenticazione a più fattori in Azure AD Privileged Identity Management
È consigliabile richiedere l'autenticazione Multi-Factor Authentication (MFA) per tutti gli amministratori. In questo modo si riduce il rischio di hello di un attacco di scadenza password tooa compromesso.

È possibile richiedere agli utenti di compilare una richiesta per l'autenticazione MFA durante l'accesso. post di blog di Hello [MFA per Office 365 e l'autenticazione a più fattori per Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) confronta il contenuto delle sottoscrizioni di Office e Azure, con funzionalità hello contenuta nell'offerta Microsoft Azure multi-Factor Authentication hello.

È anche possibile richiedere agli utenti di compilare una richiesta per l'autenticazione MFA durante l'attivazione di un ruolo in Azure AD PIM. In questo modo, se l'utente hello non è stata completata una richiesta di autenticazione a più fattori quando si è effettuato l'accesso, sarà richiesta toodo così da PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Richiedere l'MFA in Azure AD Privileged Identity Management
Quando si gestiscono le identità in PIM come amministratore dei ruoli con privilegi, è possibile che vengano visualizzati avvisi che consigliano l'autenticazione MFA per gli account con privilegi. Fare clic su protezione hello avviso nel dashboard PIM hello e un nuovo pannello verrà aperto con un elenco di account di amministratore hello che richiede l'autenticazione a più fattori.  È possibile richiedere l'autenticazione a più fattori per la selezione di più ruoli e quindi fare clic su hello **correggere** pulsante, oppure fare clic su Avanti tooindividual ruoli di hello puntini di sospensione e quindi fare clic su hello **correggere** pulsante.

> [!IMPORTANT]
> Ora, autenticazione a più fattori di Azure funziona solo con lavoro o scuola, non un account di Microsoft (in genere un account personale che ha utilizzato toosign in servizi di tooMicrosoft Skype, Xbox, Outlook.com, ecc.) a destra. Per questo motivo, chiunque utilizzi un account Microsoft non può essere un amministratore idoneo perché non possono usare l'autenticazione a più fattori tooactivate i relativi ruoli. Se questi utenti hanno bisogno toocontinue la gestione di carichi di lavoro con un account Microsoft, elevare i loro toopermanent amministratori per il momento.
> 
> 

Inoltre, è possibile modificare il requisito di autenticazione a più fattori hello per un ruolo specifico, fare clic su di esso nella sezione ruoli delle dashboard PIM hello hello. Quindi, fare clic su **impostazioni** nel pannello dei ruoli hello e quindi selezionando **abilitare** con l'autenticazione a più fattori.

## <a name="how-azure-ad-pim-validates-mfa"></a>Modalità di convalida della MFA da parte di Azure AD PIM
Sono disponibili due opzioni per la convalida di MFA quando un utente attiva un ruolo.

l'opzione più semplice Hello è toorely su Azure MFA per gli utenti che l'attivazione di un ruolo con privilegi. toodo, questo controllo prima che gli utenti vengono concessi in licenza, se necessario e sono registrati per l'autenticazione a più fattori di Azure. Ulteriori informazioni su come toodo presenta [Introduzione ad Azure multi-Factor Authentication nel cloud hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). È consigliabile, ma non è obbligatorio, che si configura tooenforce AD Azure MFA per gli utenti effettuano l'accesso. In questo modo i controlli di autenticazione a più fattori hello saranno da Azure AD PIM stesso.

In alternativa, se gli utenti eseguono l'autenticazione in locale, è possibile assegnare al provider di identità la responsabilità dell'autenticazione MFA. Ad esempio, se è stata configurata l'autenticazione basata su smart card di Active Directory Federation Services toorequire prima di accedere AD Azure, [protezione di risorse cloud con Azure multi-Factor Authentication e AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) sono incluse le istruzioni per la configurazione di ADFS toosend attestazioni tooAzure Active Directory. Quando un utente tenta di tooactivate un ruolo, Azure AD PIM accetterà che autenticazione a più fattori è già stato convalidato per utente hello dopo la ricezione delle attestazioni appropriato hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

