---
title: operazioni di Active Directory Connect Health aaaAzure
description: Questo articolo descrive le operazioni aggiuntive che possono essere eseguite dopo avere distribuito Azure AD Connect Health.
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Operazioni di Azure Active Directory Connect Health
In questo argomento descrive hello varie operazioni è possibile eseguire tramite Azure Active Directory (Azure AD) Connect Health.

## <a name="enable-email-notifications"></a>Abilitare le notifiche di posta elettronica
È possibile configurare notifiche tramite posta elettronica di hello Azure AD Connect Health service toosend quando gli avvisi indicano che l'infrastruttura di identità non è integro. Questo errore si verifica quando viene generato un avviso e quando viene risolto.

![Schermata delle impostazioni delle notifiche di posta elettronica di Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> Le notifiche di posta elettronica sono abilitate per impostazione predefinita.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>notifiche di posta elettronica tooenable Azure AD Connect Health
1. Aprire hello **avvisi** pannello per il servizio di hello per cui si desidera tooreceive notifica di posta elettronica.
2. Dalla barra delle azioni hello, fare clic su **le impostazioni di notifica**.
3. Switch di notifica di posta elettronica hello, selezionare **ON**.
4. Se si desidera che tutte le notifiche di posta elettronica agli amministratori globali tooreceive, selezionare la casella di controllo hello.
5. Se si desidera tooreceive notifiche di posta elettronica a tutti gli altri indirizzi di posta elettronica, specificarle nel hello **altri destinatari di posta elettronica** casella. tooremove un indirizzo di posta elettronica da questo elenco, fare clic sulla voce hello e selezionare **eliminare**.
6. Fare clic su modifiche hello toofinalize, **salvare**. Le modifiche diventano effettive dopo il salvataggio.

## <a name="delete-a-server-or-service-instance"></a>Eliminare un server o un'istanza del servizio

In alcuni casi, è possibile tooremove un server di monitoraggio. Ecco cosa occorre tooknow tooremove un server dal servizio di hello Azure AD Connect Health.

Quando si vuole eliminare un server, tenere hello segue:

* Questa azione interrompe la raccolta di altri dati da tale server. Questo server viene rimosso dal servizio di monitoraggio hello. Dopo questa azione, non è in grado di tooview nuovi avvisi, monitoraggio o dati di utilizzo analitica per questo server.
* Questa azione non Disinstalla hello Agente integrità dal server. Se non è stato disinstallato hello integrità agente prima di eseguire questo passaggio, si potrebbe riscontrare errori correlati toohello Agente integrità nel server di hello.
* Questa azione non elimina i dati di hello già raccolti da questo server. I dati vengono eliminati in base ai criteri di conservazione dei dati di Azure hello.
* Dopo aver eseguito questa azione, se si desidera che il monitoraggio toostart hello nello stesso server nuovamente, è necessario disinstallare e reinstallare hello Agente integrità su questo server.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>un server dal servizio di hello Azure AD Connect Health toodelete
Azure AD Connect Health per Active Directory Federation Services (AD FS) e Azure AD Connect (sincronizzazione):

1. Aprire hello **Server** pannello da hello **elenco Server** pannello selezionando toobe nome di server hello rimosso.
2. In hello **Server** fare clic su pannello, dalla barra delle azioni hello **eliminare**.
3. Confermare digitando il nome del server hello nella finestra di conferma hello.
4. Fare clic su **Elimina**.

Azure AD Connect Health per Azure Active Directory Domain Services:

1. Aprire hello **i controller di dominio** dashboard.
2. Selezionare hello controller di dominio toobe rimosso.
3. Dalla barra delle azioni hello, fare clic su **selezionata l'opzione Elimina**.
4. Conferma hello azione toodelete hello server.
5. Fare clic su **Elimina**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Eliminare un'istanza del servizio dal servizio Azure AD Connect Health
In alcuni casi, potrebbe essere tooremove un'istanza del servizio. Ecco cosa ne necessario tooknow tooremove un servizio dell'istanza dal servizio di hello Azure AD Connect Health.

Quando si vuole eliminare un'istanza del servizio, tenere hello segue:

* Questa azione rimuove l'istanza del servizio corrente hello dalla hello monitoraggio del servizio.
* Questa azione non Disinstalla o rimuovere hello integrità agente da qualsiasi server hello che sono stati monitorati come parte di questa istanza del servizio. Se non è stato disinstallato hello integrità agente prima di eseguire questo passaggio, si potrebbe riscontrare errori correlati toohello Agente integrità nei server hello.
* Tutti i dati da questa istanza del servizio viene eliminato in base ai criteri di conservazione dei dati di Azure hello.
* Dopo aver eseguito questa azione, se si desidera toostart hello servizio di monitoraggio, disinstallare e reinstallare hello integrità agente su tutti i server hello. Dopo aver eseguito questa azione, se si desidera toostart monitoraggio hello nello stesso server, disinstallare, reinstallare e registrare hello integrità agente su tale server.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete un'istanza del servizio dal servizio di hello Azure AD Connect Health
1. Aprire hello **servizio** pannello da hello **elenco servizio** pannello selezionando l'identificatore del servizio hello (nome di farm) che si desidera tooremove.
2. In hello **Server** fare clic su pannello, dalla barra delle azioni hello **eliminare**.
3. Conferma digitando il nome del servizio hello nella finestra di conferma hello (ad esempio: sts.contoso.com).
4. Fare clic su **Elimina**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Gestire l'accesso con il controllo degli accessi in base al ruolo
[Controllo di accesso basato sui ruoli (RBAC)](../role-based-access-control-configure.md) per Azure AD Connect Health fornisce accesso toousers e gruppi diversi da amministratori globali. RBAC Assegna ruoli toohello destinato utenti e gruppi e consentono agli amministratori globali di hello toolimit all'interno della directory.

### <a name="roles"></a>Ruoli
Azure AD Connect Health supporta hello ruoli predefiniti seguenti:

| Ruolo | Autorizzazioni |
| --- | --- |
| Proprietario |I proprietari possono *gestire l'accesso* (ad esempio, assegnare un ruolo tooa utente o gruppo), *tutte le informazioni sulla* (ad esempio, visualizzare gli avvisi) dal portale hello e *modificare le impostazioni di* ( ad esempio, le notifiche di posta elettronica) all'interno di Azure AD Connect Health. <br>Per impostazione predefinita, gli amministratori globali di Azure AD vengono assegnati a questo ruolo e questa assegnazione non è modificabile. |
| Collaboratore |I collaboratori possono *tutte le informazioni sulla* (ad esempio, visualizzare gli avvisi) dal portale hello e *modificare le impostazioni di* (ad esempio, notifiche tramite posta elettronica) all'interno di Azure AD Connect Health. |
| Reader |I lettori possono *tutte le informazioni sulla* (ad esempio, visualizzare gli avvisi) dal portale hello all'interno di Azure AD Connect Health. |

Tutti gli altri ruoli (ad esempio, gli amministratori di accesso utente o gli utenti di DevTest Labs) non hanno tooaccess alcun impatto all'interno di Azure AD Connect Health, anche se hello ruoli sono disponibili in esperienza del portale hello.

### <a name="access-scope"></a>Ambito di accesso
Azure AD Connect Health supporta la gestione dell'accesso a due livelli:

* **Tutte le istanze di servizio**: si tratta di hello consigliata nella maggior parte dei casi. Controlla l'accesso per tutte le istanze del servizio (ad esempio, una farm AD FS) in tutti i tipi di ruolo che vengono monitorati da Azure AD Connect Health.
* **Istanza del servizio**: In alcuni casi, potrebbe essere necessario toosegregate l'accesso basato sui tipi di ruolo o da un'istanza del servizio. In questo caso, è possibile gestire l'accesso a livello di istanza servizio hello.  

Se un utente finale ha accesso a directory hello o il servizio l'autorizzazione è concessa livello di istanza.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Consentire agli utenti o gruppi di accesso tooAzure AD Connect Health
Hello passaggi seguenti viene illustrato come accedere a tooallow.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Passaggio 1: Selezionare l'ambito di accesso appropriato hello
un utente l'accesso a hello tooallow *tutte le istanze di servizio* livello all'interno di Azure AD Connect Health, pannello principale di hello open in Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Passaggio 2: Aggiungere utenti e gruppi e assegnare ruoli
1. Da hello **configura** fare clic su **utenti**.<br>
   ![Schermata del pannello principale del Controllo degli accessi in base al ruolo di Azure AD Connect Health con gli utenti evidenziati](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Selezionare **Aggiungi**.
3. In hello **selezionare un ruolo** riquadro, selezionare un ruolo (ad esempio, **proprietario**).<br>
   ![Schermata della finestra Utenti del Controllo degli accessi in base al ruolo di Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Nome del tipo hello o identificatore di destinazione hello utente o gruppo. È possibile selezionare uno o più utenti o gruppi di hello contemporaneamente. Fare clic su **Seleziona**.
   ![Schermata della finestra Utenti del Controllo degli accessi in base al ruolo di Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Selezionare **OK**.<br>
6. Al termine dell'assegnazione di ruolo hello, hello utenti e gruppi vengono visualizzati nell'elenco di hello.<br>
   ![Schermata della finestra Utenti del Controllo degli accessi in base al ruolo di Azure AD Connect Health con nuovi utenti evidenziati](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Ora hello elencati utenti e gruppi dispongono dell'accesso, in base tootheir assegnati ruoli.

> [!NOTE]
> * Gli amministratori globali hanno sempre le operazioni di accesso completo tooall hello, ma gli account di amministratore globale non sono presenti nel precedente elenco hello.
> * funzionalità di Hello invitare gli utenti non è supportato in Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Passaggio 3: Condividere il percorso di blade hello con utenti o gruppi
1. Dopo che le autorizzazioni sono state assegnate, un utente può accedere ad Azure AD Connect Health da [qui](http://aka.ms/aadconnecthealth).
2. Nel Pannello di hello, è possibile aggiungere utente hello pannello hello, o diverse parti di esso, toohello dashboard. Fare semplicemente clic hello **toodashboard Pin** icona.<br>
   ![Schermata del pannello di aggiunta del Controllo degli accessi in base al ruolo di Azure AD Connect Health con l'icona di aggiunta evidenziata](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Un utente con ruolo di lettore hello assegnato non è in grado di tooget estensione di Azure AD Connect Health da hello Azure Marketplace. utente Hello non è possibile eseguire in modo toodo hello necessarie "Crea" operazione. utente Hello può comunque essere toohello pannello da toohello passare prima di collegamento. Per un uso successivo, utente hello può aggiungere dashboard di toohello di hello blade.
>
>

### <a name="remove-users-or-groups"></a>Rimuovere utenti o gruppi
È possibile rimuovere un utente o un gruppo aggiunto tooAzure AD connettersi RBAC di integrità. Semplicemente hello utente o gruppo e scegliere **rimuovere**.<br>
![Schermata della finestra Utenti del Controllo degli accessi in base al ruolo di Azure AD Connect Health con Rimuovi evidenziato](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Passaggi successivi
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
