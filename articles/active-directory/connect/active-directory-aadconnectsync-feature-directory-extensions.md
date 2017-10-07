---
title: 'Servizio di sincronizzazione Azure AD Connect: estensioni della directory | Documentazione Microsoft'
description: "In questo argomento vengono descritte funzionalità estensioni di directory hello in Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Servizio di sincronizzazione Azure AD Connect: estensioni della directory
Le estensioni di directory consente di schema hello tooextend in Azure AD con gli attributi da Active Directory locale. Questa funzionalità permette di App LOB toobuild utilizzo di attributi continui toomanage locale. Questi attributi possono essere utilizzati tramite le [estensioni della directory Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/). È possibile visualizzare gli attributi di hello disponibili tramite [Esplora Azure AD Graph](https://graphexplorer.cloudapp.net) e [Esplora Microsoft Graph](https://graphexplorer2.azurewebsites.net/) rispettivamente.

Attualmente nessun carico di lavoro di Office 365 utilizza questi attributi.

Configurare attributi aggiuntivi di cui si desidera toosynchronize nel percorso di impostazioni personalizzate hello nell'installazione guidata di hello.
![Procedura guidata per l'estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
installazione di Hello Mostra hello gli attributi, che costituiscono candidati validi seguenti:

* Tipi di oggetto utente e gruppo
* Attributi a valore singolo: String, Boolean, Integer, Binary
* Attributi multivalore: String, Binary

elenco di Hello di attributi viene letto dalla cache di schema hello creata durante l'installazione di Azure AD Connect. Se è stato esteso lo schema di Active Directory hello con attributi aggiuntivi, hello [schema deve essere aggiornato](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) prima che questi nuovi attributi sono visibili.

Un oggetto in Azure AD può avere gli attributi di estensioni di directory too100. la lunghezza massima di Hello è 250 caratteri. Se un valore di attributo è più lungo, viene troncato dal motore di sincronizzazione hello.

Durante l'installazione di Azure AD Connect viene registrata un'applicazione in cui sono disponibili questi attributi. È possibile visualizzare l'applicazione nel portale di Azure hello.  
![App estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Questi attributi ora sono disponibili tramite Graph:   
![Grafico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

gli attributi di Hello sono preceduti da estensione\_{AppClientId}\_. Hello AppClientId ha hello stesso valore per tutti gli attributi nel tenant di Azure AD.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
