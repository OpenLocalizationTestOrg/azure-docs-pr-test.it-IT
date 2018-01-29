---
title: 'Procedura: usare le password per le app in Azure MFA | Microsoft Docs'
description: Questa pagina consente agli utenti di comprendere il ruolo e la funzione delle password per le app in Azure MFA.
services: multi-factor-authentication
documentationcenter: 
author: barlanmsft
manager: mtillman
ms.reviewer: richagi
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: barlan
ms.custom: end-user
ms.openlocfilehash: 55ca5ada0db30440e4599c77b7a6834ef671c7a4
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Che cosa sono le password per le app in Azure Multi-Factor Authentication?
Alcune applicazioni non basate su browser, come il client di posta elettronica di Apple, utilizzano Exchange Active Sync e attualmente non supportano l'autenticazione a più fattori. L’autenticazione a più fattori viene abilitata per singolo utente. Questo implica che, se un utente è stato abilitato per l'autenticazione a più fattori e tenta di utilizzare applicazioni non basate su browser, non potrà farlo. La password dell’app consente tale operazione. Se si applica Multi-Factor Authentication tramite criteri di accesso condizionale e non tramite Multi-Factor Authentication per utente, è possibile creare password di app. Le applicazioni che usano criteri di accesso condizionale per controllare l'accesso non hanno bisogno di password di app.

Dopo aver creato una password dell’app, è possibile utilizzarla al posto della password originale con le applicazioni non basate su browser. Questo avviene perché quando ci si registra per la verifica in due passaggi, si indica a Microsoft di non consentire l'accesso con la password a un utente che non possa eseguire anche la seconda verifica. Il client di posta elettronica di Apple sul telefono non può accedere perché per questo client non è possibile richiedere la verifica in due passaggi. La soluzione al problema consiste nel creare una password per l'app più sicura che non venga usata quotidianamente, ma solo per le app che non supportano la verifica in due passaggi. Usare la password per l'app per ignorare l’autenticazione a più fattori e proseguire.

> [!NOTE]
> I client di Office 2013, tra cui Outlook, supportano i nuovi protocolli di autenticazione e possono essere usati con la verifica in due passaggi.  Ciò significa che una volta attivati, le password della app non vengono richieste per l'utilizzo con i Client di Office 2013.  Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica dell'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-to-use-app-passwords"></a>Come utilizzare le password delle app
Di seguito sono riportate alcune considerazioni da tenere presente per l’utilizzo delle password delle app.

* La password per l'app non viene creata dall'utente, ma viene generata automaticamente. Poiché è sufficiente immettere la password per l'app una volta per ogni app, è preferibile usare una password più complessa, generata automaticamente anziché crearne una facile da ricordare.
* Al momento esiste un limite di 40 password per utente. Se si tenta di creare una password dopo aver raggiunto il limite, verrà richiesto di eliminare una delle password per le app esistenti prima di crearne una nuova.
* È consigliabile usare una sola password per dispositivo, non per applicazione. Ad esempio, è possibile creare una sola password per il computer portatile e usarla per tutte le applicazioni su tale computer. Quindi, creare una seconda password per le app da usare per tutte le app sul desktop.
* La prima volta che si esegue la registrazione per la verifica in due passaggi viene comunicata una sola password per le app.  Se sono necessarie password aggiuntive, è possibile crearle.



## <a name="creating-and-deleting-app-passwords"></a>Creazione ed eliminazione delle password di app
Durante l'accesso iniziale, viene fornita una password dell’app che è possibile utilizzare.  Inoltre, è inoltre possibile creare ed eliminare le password per le app in un secondo momento.  La procedura dipende dalla modalità di utilizzo dell’autenticazione a più fattori. Rispondere alle domande seguenti per determinare il luogo in cui è possibile gestire le password per le app:

1. La verifica in due passaggi viene usata per l'account Microsoft personale? Se sì, è consigliabile consultare l'articolo [Password per app e verifica in due passaggi](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) per avere altre informazioni. Altrimenti passare alla seconda domanda.

2. Pertanto, la verifica in due passaggi viene usata per un account aziendale o dell'istituto di istruzione. È usata per accedere alle applicazioni di Office 365? Se sì, è consigliabile consultare [Creare una password dell'app per Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) per avere maggiori informazioni. Altrimenti passare alla terza domanda.

3. La verifica in due passaggi viene usata con Microsoft Azure? Se sì, passare alla sezione [Gestione delle password per le app nel Portale di Azure](#manage-app-passwords-in-the-Azure-portal) di questo articolo. Altrimenti passare alla quarta domanda.

4. Non si è sicuri su dove venga usata la verifica in due passaggi? Passare alla sezione [Gestione delle password per le app nel Portale MyApps](#manage-app-passwords-with-the-myapps-portal) di questo articolo.


## <a name="manage-app-passwords-in-the-azure-portal"></a>Gestione delle password per le app nel Portale di Azure
Se si usa la verifica in due passaggi con Azure, è consigliabile creare password per le app tramite il Portale di Azure.



## <a name="manage-app-passwords-with-the-myapps-portal"></a>Gestione delle password per le app nel portale MyApps.
Se non si è certi di come utilizzare Multi-Factor Authentication, è sempre possibile creare ed eliminare le password per le app tramite il portale Myapps.

### <a name="to-create-an-app-password-using-the-myapps-portal"></a>Per creare una password di app tramite il portale Myapps
1. Effettuare l'accesso ad [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Fare clic sul nome in alto a destra e scegliere **Profilo**.
3. Selezionare **Verifica aggiuntiva di sicurezza**.
   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selezionare **Password delle app**.
   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Fare clic su **Crea**.
6. Immettere un nome per la password dell'app e quindi fare clic su **Avanti**.
7. Copiare la password per l'app negli Appunti, quindi incollarla nell'app.
   ![Creare una password di app](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a>Per eliminare una password di app tramite il portale MyApps
1. Effettuare l'accesso ad [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Nella parte superiore selezionare il profilo.
3. Selezionare **Verifica aggiuntiva di sicurezza**.

   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selezionare **Password delle app**.

   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Accanto alla password dell’app che si desidera rimuovere, selezionare **Elimina**.

   ![Eliminare una password di app](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confermare che si desidera eliminare la password facendo clic su **Sì**.
7. Dopo che la password dell’app è stata eliminata, è possibile fare clic su **Chiudi**.

## <a name="next-steps"></a>Passaggi successivi

- [Gestire le impostazioni della verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md)

- Provare l'[app Microsoft Authenticator](microsoft-authenticator-app-how-to.md) per verificare gli accessi con le notifiche delle app, invece di ricevere messaggi o chiamate.
