---
title: 'Sincronizzazione di Azure AD Connect: la modifica di account del servizio di sincronizzazione connettersi hello Azure AD | Documenti Microsoft'
description: Il documento di questo argomento descrive la chiave di crittografia hello e come tooabandon dopo password hello viene modificato.
services: active-directory
keywords: Account del servizio Azure AD Sync, password
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Modifica password account del servizio sincronizzazione hello Azure AD Connect
Se si modifica password account del servizio sincronizzazione hello Azure AD Connect, hello servizio di sincronizzazione non sarà in grado di avviare correttamente finché non si hanno abbandonato la chiave di crittografia hello e reinizializzata password account del servizio sincronizzazione hello Azure AD Connect. 

Azure AD Connect, come parte di hello Synchronization Services utilizza una password di hello toostore chiave di crittografia di hello di dominio Active Directory e gli account del servizio Azure AD.  Questi account vengono crittografati prima di essere archiviati nel database di hello. 

Hello chiave di crittografia utilizzata sia protetta con [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI protegge chiave di crittografia di hello utilizzando hello **password dell'account di servizio hello Azure AD Connect sincronizzazione**. 

Se è necessario toochange password account del servizio hello è possibile utilizzare le procedure di hello in [chiave di crittografia Abandoning hello Azure AD Sync connettersi](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish questo.  Queste procedure devono essere utilizzate anche se è necessario chiave di crittografia hello tooabandon per qualsiasi motivo.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problemi causati da Modifica password hello
Sono presenti due elementi che devono toobe eseguita quando si modifica la password di account di servizio hello.

In primo luogo, è necessario password hello toochange in Gestione controllo servizi Windows hello.  Finché non si risolve questo problema, verranno visualizzati gli errori seguenti:


- Se si tenta di hello toostart il servizio di sincronizzazione in Gestione controllo servizi di Windows, viene visualizzato l'errore hello "**Windows non è stato possibile avviare il servizio di Microsoft Azure AD Sync hello nel Computer locale**". **Errore 1069: Impossibile avviare il servizio hello a causa di errore di accesso tooa.** "
- In Visualizzatore eventi di Windows hello registro eventi di sistema contiene un errore con **7038 ID evento** e il messaggio "**hello servizio ADSync era toolog Impossibile sul come con password hello attualmente configurata a causa di toohello seguente errore: nome utente Hello o password non è corretta.** "

In secondo luogo, in determinate condizioni, se hello password viene aggiornata, hello servizio di sincronizzazione non più possibile recuperare la chiave di crittografia hello tramite DPAPI. Senza la chiave di crittografia hello hello da che servizio di sincronizzazione non è possibile decrittografare hello toosynchronize obbligatorio di password a / locale AD e Azure AD.
Verranno visualizzati gli errori seguenti:

- In Gestione controllo servizi di Windows, se si tenta di hello toostart servizio di sincronizzazione e non è possibile recuperare la chiave di crittografia hello non riesce con errore "* * Windows non è stato possibile avviare Microsoft Azure AD Sync hello nel Computer locale. Per ulteriori informazioni, esaminare il registro eventi di sistema hello. Se questo è un servizio non Microsoft, contattare il fornitore del servizio di hello e fare riferimento a codice di errore specifico tooservice * *-21451857952 * * *. "
- In Visualizzatore eventi di Windows, log eventi dell'applicazione hello contiene un errore con **6028 ID evento** e messaggio di errore *"**chiave di crittografia hello del server non è accessibile.* *"*

tooensure che non si ricevono questi errori, seguire le procedure di hello in [chiave di crittografia Abandoning hello Azure AD Sync connettersi](#abandoning-the-azure-ad-connect-sync-encryption-key) quando si modifica la password di hello.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Chiave di crittografia di abbandono hello Azure AD Connect Sync
>[!IMPORTANT]
>Hello nelle procedure seguenti si applicano solo AD tooAzure Connetti compilazione 1.1.443.0 precedente o successiva.

Utilizzare hello seguente chiave di crittografia di procedure tooabandon hello.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Quali toodo se occorre una chiave di crittografia hello tooabandon

Se è necessaria una chiave di crittografia hello tooabandon, questa scheda hello tooaccomplish le procedure seguenti.

1. [Chiave di crittografia esistente hello abbandonare](#abandon-the-existing-encryption-key)

2. [Specificare la password hello di hello account di dominio Active Directory](#provide-the-password-of-the-ad-ds-account)

3. [Reinizializzare la password di hello di hello account di Azure AD sync](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Avviare il servizio di sincronizzazione hello](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Chiave di crittografia esistente hello abbandonare
Abbandonare chiave di crittografia esistente hello in modo che nuova chiave di crittografia può essere creati:

1. Accedi tooyour Server di connettersi AD Azure come amministratore.

2. Avviare una nuova sessione di PowerShell.

3. Passare toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Eseguire il comando hello:`./miiskmu.exe /a`

![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Specificare la password hello di hello account di dominio Active Directory
Le password esistenti di hello archiviate hello database non possono essere decrittografate, è necessario tooprovide hello, servizio di sincronizzazione con la password di hello dell'account di dominio Active Directory hello. Hello servizio di sincronizzazione consente di crittografare le password hello usando hello nuova chiave di crittografia:

1. Avviare hello Synchronization Service Manager (servizio di sincronizzazione iniziale →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Passare toohello **connettori** scheda.
3. Seleziona hello **Active Directory Connector** corrispondente tooyour AD locale. Se si dispone di più di un connettore di Active Directory, è possibile ripetere hello seguendo i passaggi per ognuna di esse.
4. In **Azioni** selezionare **Proprietà**.
5. Nella finestra di dialogo popup hello, selezionare **connettersi foresta Directory tooActive**:
6. Immettere la password di hello dell'account di dominio Active Directory hello in hello **Password** casella di testo. Se non si conosce la password, è necessario impostare tooa noto valore prima di eseguire questo passaggio.
7. Fare clic su **OK** toosave hello nuova password e finestra di dialogo popup hello Chiudi.
![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Reinizializzare la password di hello di hello account di Azure AD sync
È possibile fornire direttamente la password di hello del servizio di Azure AD hello, toohello account servizio di sincronizzazione. In alternativa, è necessario toouse hello cmdlet **Aggiungi ADSyncAADServiceAccount** tooreinitialize hello account del servizio Azure AD. cmdlet di Hello Reimposta password dell'account hello e rende disponibile toohello servizio di sincronizzazione:

1. Avviare una nuova sessione di PowerShell nel server di Azure AD Connect hello.
2. Eseguire il cmdlet `Add-ADSyncAADServiceAccount`.
3. Nella finestra di dialogo popup hello, fornire le credenziali di amministratore globale di hello Azure AD per il tenant di Azure AD.
![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Se ha esito positivo, verrà visualizzato hello prompt dei comandi di PowerShell.

#### <a name="start-hello-synchronization-service"></a>Avviare il servizio di sincronizzazione hello
Ora che hello servizio di sincronizzazione ha chiave di crittografia toohello di accesso e tutte le password di hello è necessario, è possibile riavviare il servizio di hello in Gestione controllo servizi Windows hello:


1. Passare tooWindows Gestione controllo servizi (Services → avvio).
2. Selezionare **Microsoft Azure AD Sync** e fare clic su Riavvia.

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)

* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
