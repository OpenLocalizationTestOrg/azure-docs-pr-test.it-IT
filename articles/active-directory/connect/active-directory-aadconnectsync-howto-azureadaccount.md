---
title: 'Sincronizzazione di Azure AD Connect: come account del servizio toomanage hello Azure AD | Documenti Microsoft'
description: Questo argomento vengono documentate come account del servizio toorestore hello Azure AD.
services: active-directory
keywords: AADSTS70002, AADSTS50054, come tooreset hello password per hello sincronizzazione di Azure AD Connect account del servizio del connettore
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Sincronizzazione di Azure AD Connect: come account del servizio toomanage hello Azure AD
account di servizio Hello utilizzato dal connettore Azure AD hello dovrebbe toobe servizio gratuitamente. Se è necessario tooreset le sue credenziali, in questo argomento è per l'utente. Ad esempio, se dispone di un amministratore globale per errore reimpostazione hello password nell'account di servizio hello tramite PowerShell.

## <a name="reset-hello-credentials"></a>Reimpostare le credenziali di hello
Se l'account del servizio hello definito in hello Azure Active Directory Connector non riesce a contattare Azure Active Directory a causa di problemi di tooauthentication, è possibile reimpostare la password di hello.

1. Accedi a server di sincronizzazione di Azure AD Connect toohello e avviare PowerShell.
2. Eseguire `Add-ADSyncAADServiceAccount`.  
   ![Cmdlet PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Fornire le credenziali di amministratore globale di Azure Active Directory.

Questo cmdlet Reimposta password hello dell'account del servizio hello e aggiornarlo in Azure AD e nel motore di sincronizzazione hello.

## <a name="known-issues-these-steps-can-solve"></a>Problemi noti che possono essere risolti con questi passaggi
In questa sezione è un elenco di errori segnalati dai clienti che sono stati corretti in delle credenziali predefinite nel hello account del servizio Azure AD.

- - -
Evento 6900  
server di Hello ha rilevato un errore imprevisto durante l'elaborazione di una notifica di modifica password:  
AADSTS70002: Errore di convalida delle credenziali. AADSTS50054: Per l'autenticazione verrà usata la password precedente.

- - -
Evento 659  
Errore durante il recupero della configurazione della sincronizzazione dei criteri password. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: Errore di convalida delle credenziali. AADSTS50054: Per l'autenticazione verrà usata la password precedente.

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

