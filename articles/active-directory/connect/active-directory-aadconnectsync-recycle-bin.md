---
title: 'Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory | Microsoft Docs'
description: "In questo argomento consiglia di utilizzare hello della funzionalità del Cestino di Active Directory con Azure AD Connect."
services: active-directory
keywords: Cestino di Active Directory, eliminazione accidentale, ancoraggio di origine
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory
È consigliabile abilitare funzionalità Cestino per Active Directory hello per le in Active Directory locali, che sono sincronizzati tooAzure AD. 

Se è stato eliminato accidentalmente una locale oggetto utente di Active Directory e il ripristino utilizzando funzionalità hello, Azure AD Ripristina oggetto utente di Azure AD corrispondente hello.  Per informazioni sulla funzionalità del Cestino hello Active Directory, vedere tooarticle [panoramica dello Scenario per il ripristino di oggetti Active Directory eliminati](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Vantaggi dell'abilitazione hello AD Cestino
Questa funzionalità consente di con il ripristino di oggetti utente di Azure AD effettuando hello seguenti:

* Se è stato eliminato accidentalmente una locale dell'oggetto utente di Active Directory, hello corrispondente oggetto utente di Azure AD verrà eliminato in hello successivo ciclo di sincronizzazione. Per impostazione predefinita, Azure AD mantiene oggetto utente di Azure AD hello eliminato eliminato per 30 giorni.

* Se si dispone di on-premise funzionalità Cestino per Active Directory è abilitata, è possibile ripristinare hello eliminato oggetto utente di Active Directory in locale senza modificarne il valore di ancoraggio di origine. Quando hello recuperato locale viene sincronizzato l'oggetto utente di Active Directory tooAzure AD, Azure AD verrà ripristinato hello corrispondente eliminato oggetto utente Azure AD. Per informazioni sull'attributo di ancoraggio di origine, fare riferimento tooarticle [Azure AD Connect: concetti di progettazione](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Se non si dispone di on-premise Cestino di Active Directory abilitata la funzionalità Cestino, potrebbe essere richiesto toocreate un oggetto Active Directory utente oggetto tooreplace hello eliminato. Se servizio di sincronizzazione di Azure AD Connect è configurato toouse generato dal sistema attributo di Active Directory (ad esempio ObjectGuid) per l'attributo di ancoraggio di origine hello, hello oggetto utente di Active Directory appena creata verrà non hanno hello stesso valore di ancoraggio di origine come hello eliminato l'oggetto utente di Active Directory. Quando hello oggetto utente di Active Directory appena creata viene sincronizzato tooAzure AD, Azure AD crea un nuovo oggetto utente di Azure AD anziché ripristinare l'oggetto utente di Azure AD hello eliminato.

> [!NOTE]
> Per impostazione predefinita, Azure AD mantiene gli oggetti utente di Azure AD in uno stato di eliminazione temporanea per 30 giorni, prima che vengano eliminati definitivamente. Tuttavia, gli amministratori possono accelerare l'eliminazione di hello di tali oggetti. Una volta oggetti hello vengono eliminati definitivamente, non possono essere ripristinati, anche se locale è abilitata la funzionalità Cestino per Active Directory.



## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)

* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
