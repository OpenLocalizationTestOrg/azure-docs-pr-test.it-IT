---
title: aaaHow toouse le password di App di Azure MFA? | Microsoft Docs
description: "Questa pagina consente agli utenti comprendere quali sono le password di app e quali sono utilizzati per con considerare tooAzure autenticazione a più fattori."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Che cosa sono le password per le app in Azure Multi-Factor Authentication?
Alcune App non basate su browser, ad esempio, client di posta elettronica native Apple hello che usa Exchange Active Sync, attualmente non supportano l'autenticazione a più fattori. L’autenticazione a più fattori viene abilitata per singolo utente.  Ciò significa che l'utente non può usare l'autenticazione a più fattori se:

- Hello utente è abilitato per multi-factor authentication
- utente Hello tenta toouse un'app non basate su browser.

Una password di app consente hello utente toouse hello app.

Dopo avere creato una password dell'app, è possibile usarla al posto della password originale con le applicazioni non basate su browser. Quando si registra per la verifica in due passaggi, si sta indica Microsoft non toolet tutti gli utenti di accedere con la password se non possono inoltre eseguire la verifica di hello secondo. client di posta elettronica native Apple Hello sul telefono non è possibile accedere come si perché non è possibile richiedere la verifica in due passaggi. soluzione toothis problema Hello è una password più sicura di app che non si utilizza toocreate quotidiane. Le password di app sono destinate solo a tutte le app che non supportano la verifica in due passaggi. Utilizzare password dell'app hello in modo che le applicazioni possono ignorare multi-factor authentication e continuare toowork.


> [!NOTE]
> I client di Office 2013, tra cui Outlook, supportano i nuovi protocolli di autenticazione e possono essere usati con la verifica in due passaggi. Le password di app non vengono richieste per l'uso con i client Office 2013.  Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica dell'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Come le password di app toouse
Ecco alcuni aspetti tooknow sulle password di app:

* La password per l'app non viene creata dall'utente, Vengono generate automaticamente.
* Al momento esiste un limite di 40 password per utente. 
* Se si tenta di toocreate una password dell'app dopo aver raggiunto il limite di hello, sarà necessario toodelete una delle password esistenti prima di creare una nuova.
* Usare una sola password per dispositivo, non per applicazione. Ad esempio, è possibile creare una sola password per il computer portatile e usarla per tutte le applicazioni su tale computer. Creare quindi un secondo toouse password di app per tutte le app sul desktop. 
* È possibile hello password di app una prima volta che si registra per la verifica in due passaggi.  Se sono necessarie password aggiuntive, è possibile crearle.



## <a name="creating-and-deleting-app-passwords"></a>Creazione ed eliminazione delle password di app
Durante l'accesso iniziale, viene fornita una password dell'app che è possibile usare.  È possibile anche creare ed eliminare le password per le app in un secondo momento. La procedura di eliminazione delle password di app dipende dalla modalità di utilizzo dell'autenticazione a più fattori. Hello risposte seguenti domande toodetermine in cui è necessario usare password di app toomanage: 

1. La verifica in due passaggi viene usata per l'account Microsoft personale? In caso affermativo, è consigliabile consultare toohello [verifica in due passaggi e le password di App](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) articolo per la Guida. Se no, continua tooquestion due.

2. Pertanto, la verifica in due passaggi viene usata per un account aziendale o dell'istituto di istruzione. Utilizzi toosign nelle App tooOffice 365? In caso affermativo, è consigliabile consultare troppo[creare una password di app per Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) per assistenza. Se no, continua tooquestion tre. 

3. La verifica in due passaggi viene usata con Microsoft Azure? In caso affermativo, continuare toohello [gestione delle password di app nel portale di Azure hello](#manage-app-passwords-in-the-Azure-portal) sezione di questo articolo. Se no, continua tooquestion quattro.

4. Non si è sicuri su dove venga usata la verifica in due passaggi? Continuare toohello [gestione delle password di app con il portale MyApps hello](#manage-app-passwords-with-the-myapps-portal) sezione di questo articolo. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Gestione delle password di app nel portale di Azure hello
Se si usa verifica in due passaggi con Azure, è necessario toocreate le password di app tramite hello portale di Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>password di app toocreate in hello portale di Azure
1. Accedi toohello portale di Azure classico.
2. Nella parte superiore di hello, fare doppio clic su nome utente e selezionare verifica aggiuntiva di sicurezza.
3. Nella pagina di verifica hello, nella parte superiore di hello, selezionare le password di app
4. Fare clic su **Crea**.
5. Immettere un nome per la password di app hello e fare clic su **successivo**
6. Copiare negli Appunti toohello password di app hello e incollarlo nell'app.
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>password di app toodelete in hello portale di Azure
1. Accedi toohello portale di Azure classico.
2. Nella parte superiore di hello, fare doppio clic su nome utente e selezionare verifica aggiuntiva di sicurezza.
3. Nella parte superiore di hello, verifica di sicurezza tooadditional successiva, selezionare **le password di app.**
4. Password di app toohello successiva da toodelete, selezionare **eliminare**.
5. Confermare l'eliminazione di hello facendo **Sì**.
6. Una volta la password di app hello viene eliminata, è possibile fare clic su **chiudere**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Gestione delle password di app con il portale MyApps hello.
Se non sei sicuro come si utilizza l'autenticazione a più fattori, quindi è possibile creare ed eliminare le password di app tramite il portale di myapps hello.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>una password di app utilizzando toocreate hello portale Myapps
1. Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Fare clic sul nome in alto a destra hello e scegliere **profilo**.
3. Selezionare **Verifica aggiuntiva di sicurezza**.
   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selezionare **Password delle app**.
   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Fare clic su **Crea**.
6. Immettere un nome per la password di app hello e fare clic su **Avanti**.
7. Copiare negli Appunti toohello password di app hello e incollarlo nell'app.
   ![Creare una password di app](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>una password di app utilizzando toodelete hello portale Myapps
1. Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Nella parte superiore di hello, selezionare il profilo.
3. Selezionare **Verifica aggiuntiva di sicurezza**.

   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selezionare **Password delle app**.

   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Fare clic su Avanti password di app toohello da toodelete, **eliminare**.

   ![Eliminare una password di app](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confermare che si desidera toodelete che la password facendo clic su **Sì**.
7. Una volta la password di app hello viene eliminata, è possibile fare clic su **chiudere**.

## <a name="next-steps"></a>Passaggi successivi

- [Gestire le impostazioni della verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md)

- Provare a hello [app Authenticator Microsoft](microsoft-authenticator-app-how-to.md) tooverify gli accessi con le notifiche dell'app, anziché la ricezione di testi o chiamate. 
