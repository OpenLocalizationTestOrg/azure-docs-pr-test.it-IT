---
title: 'Sincronizzazione di Azure AD Connect: la modifica della password di account di dominio Active Directory AD hello | Documenti Microsoft'
description: Il documento di questo argomento viene descritto come tooupdate Azure AD Connect dopo password hello dell'account di dominio Active Directory hello viene modificata.
services: active-directory
keywords: account Active Directory Domain Services, account di Active Directory, password
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Modifica password dell'account di dominio Active Directory hello Active Directory
account di dominio Active Directory AD Hello fa riferimento l'account utente toohello utilizzato da Azure AD Connect toocommunicate con Active Directory locale. Se si modifica la password di hello di hello account di dominio Active Directory, è necessario aggiornare servizio Azure AD Connect sincronizzazione con hello nuova password. In caso contrario, la sincronizzazione non è più possibile sincronizzare correttamente con hello hello Active Directory locale e si verificheranno hello gli errori seguenti:

* In hello operazione Synchronization Service Manager, qualsiasi importazione o esportazione con locale ha esito negativo di Active Directory con **no-start-credenziali** errore.

* In Visualizzatore eventi di Windows, log eventi dell'applicazione hello contiene un errore con **evento ID 6000** e messaggio **'agente di gestione di hello "contoso.com" Impossibile toorun hello credenziali non sono valide'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Come tooupdate hello servizio di sincronizzazione con la nuova password per l'account di dominio Active Directory
nuova password hello tooupdate hello servizio di sincronizzazione:

1. Avviare hello Synchronization Service Manager (servizio di sincronizzazione iniziale →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Passare toohello **connettori** scheda.

3. Seleziona hello **Active Directory Connector** toohello AD account di dominio Active Directory per cui è stata modificata la password corrispondente.

4. In **Azioni** selezionare **Proprietà**.

5. Nella finestra di dialogo popup hello, selezionare **connettersi foresta Directory tooActive**:

6. Immettere hello nuova password dell'account di dominio Active Directory hello in hello **Password** casella di testo.

7. Fare clic su **OK** toosave hello nuova password e finestra di dialogo popup hello Chiudi.

8. Riavvio hello servizio Azure AD Connect sincronizzazione in Gestione controllo servizi di Windows. Si tratta di tooensure che qualsiasi password vecchia toohello di riferimento viene rimosso dalla cache di hello in memoria.

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)

* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
