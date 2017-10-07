---
title: app Authenticator aaaMicrosoft per telefoni cellulari | Documenti Microsoft
description: "Informazioni su come tooupgrade toohello più recente di Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Introduzione a app Microsoft Authenticator hello
app Microsoft Authenticator Hello offre un ulteriore livello di sicurezza dell'account aziendale o dell'istituto di istruzione (ad esempio, bsimon@contoso.com) o l'account Microsoft (ad esempio, bsimon@outlook.com).

Hello app funziona in uno dei due modi:

* **Notifica**. app Hello consente di impedire accessi non autorizzati tooaccounts e arrestare le transazioni illecite effettuando il push di un tablet o smartphone tooyour notifica. È sufficiente visualizzare la notifica di hello e, se legittima, selezionare **verificare**. In caso contrario, è possibile selezionare **Nega**. 
* **Codice di verifica**. applicazione Hello può essere utilizzata come un software di un codice di verifica OAuth toogenerate del token. Dopo avere immesso nome utente e password, immettere il codice hello fornito dall'applicazione hello hello sign nella schermata. codice di verifica Hello fornisce una seconda forma di autenticazione.

app Microsoft Authenticator Hello sostituisce l'app Azure Authenticator hello. app Azure Authenticator Hello continui a funzionare, ma se si decide di toomove toohello nuovo Microsoft Authenticator app, in questo articolo forniscono informazioni utili.  

## <a name="opt-in-for-two-step-verification"></a>Fornire il consenso esplicito per la verifica in due passaggi

app Microsoft Authenticator Hello non funziona automaticamente. Configurare ogni tooprompt l'account di un secondo metodo di verifica dopo aver Accedi con il nome utente e password. 

Per un account aziendale o dell'istituto di istruzione, non si in genere Ottiene toochoose questa funzionalità per se stessi. Al contrario, un amministratore della sicurezza acconsente per conto dell'utente e invia una notifica tooregister i metodi di verifica per l'account. Se questo scenario si applica tooyou, per ulteriori [cosa Azure multi-Factor Authentication per me](multi-factor-authentication-end-user.md).

Per un account personale, è necessario tooset una verifica in due passaggi per se stessi. Per un account Microsoft, questi passaggi sono disponibili in [Informazioni sulla verifica in due passaggi](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

È anche possibile utilizzare hello Microsoft Authenticator con l'account non Microsoft. Può chiamare la funzione hello diverso verifica in due passaggi, ma dovrebbe essere in grado di toofind in impostazioni di protezione o l'accesso. 

## <a name="install-hello-app"></a>Installare l'applicazione hello
è disponibile per app di Microsoft Authenticator Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Aggiungere gli account toohello app
Per ogni account che si desidera tooadd toohello Microsoft Authenticator app, utilizzare uno dei hello seguire le procedure seguenti:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Aggiungere un'app di toohello account Microsoft personale

Per un account Microsoft personale (uno che userai toosign tooOutlook.com, Xbox, Skype, e così via), toodo è Accedi tooyour account nell'app Microsoft Authenticator hello.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Aggiungere un lavoro o scuola account toohello app scanner di codici a matrice hello utilizzando
1. Passare toohello blindata verifica le impostazioni.  Per informazioni su come tooget toothis schermata, vedere [modificando le impostazioni di sicurezza](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Casella di controllo hello accanto troppo**app Authenticator** selezionare **configura**.

    ![pulsante Configura Hello nella schermata Impostazioni di verifica di sicurezza hello](./media/authenticator-app-how-to/azureauthe.png)

    Verrà visualizzata una schermata contenente un codice a matrice.

    ![Schermata che fornisce il codice a matrice hello](./media/authenticator-app-how-to/barcode2.png)
3. App Microsoft Authenticator hello aperto. In hello **account** selezionare  **+** e quindi specificare che si desidera tooadd un account aziendale o dell'istituto di istruzione.
4. Codice hello fotocamera tooscan hello QR e quindi selezionare **eseguita** schermata di codice a matrice hello tooclose.

    Se la fotocamera non funziona correttamente, è possibile [immettere manualmente il codice a matrice hello e l'URL](#add-an-account-to-the-app-manually).

5. Quando il nome dell'account con un codice a sei cifre sotto l'applicazione hello, completato. 

    ![Schermata Account](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Aggiungere manualmente un'app toohello account
1. Passare toohello blindata verifica le impostazioni.  Per informazioni su come tooget toothis schermata, vedere [modificando le impostazioni di sicurezza](multi-factor-authentication-end-user-manage-settings.md).
2. Selezionare **Configura**.

    ![pulsante Configura Hello nella schermata Impostazioni di verifica di sicurezza hello](./media/authenticator-app-how-to/azureauthe.png)

    Verrà visualizzata una schermata contenente un codice a matrice.  Si noti il codice hello e l'URL.

    ![Schermata che fornisce il codice a matrice hello e l'URL](./media/authenticator-app-how-to/barcode2.png)
3. App Microsoft Authenticator hello aperto. In hello **account** selezionare  **+** e quindi specificare che si desidera tooadd un account aziendale o dell'istituto di istruzione.

4. Scanner hello, selezionare **immette manualmente il codice**.

    ![Schermata per la scansione di un codice a matrice](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Immettere il codice hello e l'URL di hello nelle caselle appropriate hello hello app, quindi selezionare **fine**.

    ![Schermata per l'immissione del codice e dell'URL](./media/authenticator-app-how-to/manual.png)

6. Quando il nome dell'account con un codice a sei cifre sotto l'applicazione hello, completato.

    ![Schermata Account](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Aggiungere un'app toohello account utilizzando l'ID tocco
app Microsoft Authenticator Hello in iOS supporta ID tocco.  Azure multi-Factor Authentication consente alle organizzazioni toorequire un PIN per i dispositivi. Con l'ID tocco, gli utenti di iOS non necessario tooenter un PIN. Possono invece effettuare la scansione della propria impronta digitale e selezionare **Approva**.

Configurare Touch ID con Microsoft Authenticator è semplice. Si completa una normale richiesta di verifica con un PIN. Se il dispositivo supporta Touch ID, viene automaticamente configurato per l'account da Microsoft Authenticator.

![Verifica della configurazione di Touch ID](./media/authenticator-app-how-to/touchid1.png)

Dal momento in poi, quando si è necessario tooverify l'accesso in, si seleziona notifica push hello ricevuto e analizzare l'impronta digitale anziché immettere il PIN.

![Notifica push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Utilizzare l'applicazione hello quando accedi

Dopo aver aggiunto l'account app toohello, potrebbe essere richiesta toodo un toomake di verifica di test che tutto ciò che è stato configurato correttamente. Dopo questa verifica, la procedura è terminata. Non è necessario toodo altro fino a quando non hello successivo accesso.

Se si sceglie di codici di verifica toouse nell'app hello, iniziare toosee loro hello home page. Questi codici cambiano ogni 30 secondi in modo da riceverne sempre uno nuovo ogni volta che è necessario. Ma non è necessario toodo nulla farne finché non si Accedi e sono tooenter richiesto un codice di verifica.  
