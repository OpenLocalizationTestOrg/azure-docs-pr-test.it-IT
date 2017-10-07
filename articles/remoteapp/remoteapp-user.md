---
title: una raccolta di Azure RemoteApp di tooyour utente aaaAdd | Documenti Microsoft
description: Informazioni su come tooadd utenti tooyour raccolta di Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Come tooadd tooyour un utente raccolta di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Prima gli utenti possono visualizzare e usare le App in Azure RemoteApp, è necessario toogrant raccolta tooyour loro l'accesso. Questo aspetto è parte di facile hello: su hello **accesso utente** scheda, immettere le informazioni sull'account hello per utente hello e quindi fare clic su hello segno di spunta.

Quali informazioni sull'account sono necessarie? Che dipende dal tipo di hello di raccolta creato (cloud o ibrida) e se si utilizza Office 365 ProPlus in tale raccolta.

## <a name="supported-user-identities"></a>Identità degli utenti supportate
tipi di raccolta diverso Hello (cloud e ibrido) supportano l'utilizzo di identità utente diverse per tooapplications di accesso.  

Per una raccolta ibrida di RemoteApp, è necessario tooset di un'infrastruttura di dominio Active Directory locale e un tenant di Azure Active Directory con l'integrazione di Directory (e facoltativamente accesso single sign-on). Inoltre, è necessario toocreate alcuni oggetti di Active Directory nella directory locale hello.  

Per una raccolta di cloud di RemoteApp, è possibile concedere a qualsiasi utente con Azure Active Directory supporta le identità utente accesso tooRemoteApp tooinclude Accounts di Microsoft.  Vedere la tabella hello seguente.

Gli utenti di Office 365 sono utenti di Azure Active Directory. Agli utenti che dispongono di account ibridi con sincronizzazione della directory di Azure Active Directory è possibile concedere l'accesso utente in una distribuzione ibrida di RemoteApp.   

È possibile utilizzare questa tabella come riferimento rapido per cui identità è supportato nella raccolta di e quali sono i requisiti di Active Directory hello.

| Account utente | Cloud | Ibrido |
| --- | --- | --- |
| Account Microsoft |Sì |No |
| Azure Active Directory (Azure AD) | | |
| Solo cloud Azure AD |Sì |No |
| Sincronizzazione Active Directory con sincronizzazione password |Sì |Sì |
| Sincronizzazione Active Directory senza sincronizzazione password |Sì |No |
| Sincronizzazione Active Directory con ADFS |Sì |sì |
| [Provider di identità di terze parti supportati da Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx), ad esempio Ping |sì |Sì |
| Autenticazione a più fattori |Sì |Sì |

Per [altre informazioni](remoteapp-ad.md) , vedere Configurare Azure Active Directory per RemoteApp.

> [!NOTE]
> gli utenti di Azure Active Directory Hello devono essere di tenant hello è associato alla sottoscrizione. (È possibile visualizzare e modificare la sottoscrizione hello **impostazioni** scheda nel portale di hello. Vedere [tenant di Azure Active Directory hello modifica usata da RemoteApp](remoteapp-changetenant.md) per ulteriori informazioni.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informazioni sugli account utente di Office 365 ProPlus
Se si utilizza Office 365 ProPlus immagine di modello hello nella raccolta di *o* se si crea un'immagine personalizzata che usa Office 365, è consentito solo agli utenti di Azure Active Directory tooadd che dispone di sottoscrizioni di Office 365 per hello dominio predefinito della sottoscrizione. Per altre informazioni, vedere l'articolo relativo all' [uso di Office 365 con Azure RemoteApp](remoteapp-o365.md) .

