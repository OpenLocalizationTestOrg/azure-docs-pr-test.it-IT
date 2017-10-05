---
title: 'Servizio di sincronizzazione Azure AD Connect: estensioni della directory | Documentazione Microsoft'
description: "Questo argomento illustra la funzionalità relativa alle estensioni della directory in Azure AD Connect."
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Servizio di sincronizzazione Azure AD Connect: estensioni della directory
Le estensioni della directory consentono di estendere lo schema in Azure AD con attributi personalizzati da Active Directory in locale. Questa funzionalità consente di compilare app line-of-business che utilizzano attributi che continuano a essere gestiti in locale. Questi attributi possono essere utilizzati tramite le [estensioni della directory Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/). È possibile visualizzare gli attributi disponibili usando rispettivamente lo [strumento di esplorazione di Azure AD Graph](https://graphexplorer.cloudapp.net) e lo [strumento di esplorazione di Microsoft Graph](https://graphexplorer2.azurewebsites.net/).

Attualmente nessun carico di lavoro di Office 365 utilizza questi attributi.

È possibile configurare gli attributi aggiuntivi da sincronizzare nel percorso delle impostazioni personalizzate nell'installazione guidata.
![Procedura guidata per l'estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
L'installazione mostra gli attributi seguenti, che sono candidati validi:

* Tipi di oggetto utente e gruppo
* Attributi a valore singolo: String, Boolean, Integer, Binary
* Attributi multivalore: String, Binary

L'elenco di attributi viene letto dalla cache dello schema creata durante l'installazione di Azure AD Connect. Se è stato esteso lo schema di Active Directory con altri attributi, prima che questi nuovi attributi siano visibili è quindi necessario [aggiornare lo schema della directory](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) .

Un oggetto in Azure AD può avere al massimo 100 attributi delle estensioni della directory. La lunghezza massima consentita è di 250 caratteri. Se il valore di un attributo è più lungo, viene quindi troncato dal motore di sincronizzazione.

Durante l'installazione di Azure AD Connect viene registrata un'applicazione in cui sono disponibili questi attributi. È possibile visualizzare questa applicazione nel portale di Azure.  
![App estensione dello schema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Questi attributi ora sono disponibili tramite Graph:   
![Grafico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Gli attributi sono preceduti da extension\_{AppClientId}\_. AppClientId ha lo stesso valore per tutti gli attributi nel tenant di Azure AD.

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sulla configurazione della [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md).

Ulteriori informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
