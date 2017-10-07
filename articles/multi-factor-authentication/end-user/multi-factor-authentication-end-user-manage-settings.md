---
title: aaaManage le impostazioni di verifica in due passaggi | Documenti Microsoft
description: Gestire l'utilizzo di Azure Multi-Factor Authentication, inclusa la modifica delle informazioni di contatto e la configurazione dei dispositivi.
services: multi-factor-authentication
keywords: client di multi-factor authentication, problema di autenticazione, ID di correlazione
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>Gestire le impostazioni per la verifica in due passaggi
In questo articolo risponde alle domande sul tooupdate impostazioni per l'autenticazione a più fattori o di verifica in due passaggi. Se si sono verificati problemi di accesso account tooyour, fare riferimento troppo[problemi con la verifica](multi-factor-authentication-end-user-troubleshoot.md) per la risoluzione dei problemi.

## <a name="where-toofind-hello-settings-page"></a>Dove toofind hello pagina Impostazioni
In base al modo in cui l'azienda ha configurato Azure Multi-Factor Authentication, le impostazioni come il numero di telefono possono essere modificate in diverse posizioni.

Se l'amministratore IT inviato un URL specifico o di verifica in due passaggi toomanage di passaggi, seguire le istruzioni. In caso contrario, hello attenendosi alle istruzioni dovrebbe funzionare per qualsiasi altro utente. Se questa procedura, ma non viene visualizzato hello stesse opzioni, che significa che l'azienda o dell'istituto di istruzione proprio portale personalizzato. Chiedere all'amministratore per il portale di Azure multi-Factor Authentication tooyour collegamento hello.

1. Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Selezionare il nome dell'account in hello in alto a destra, quindi selezionare **profilo**.  
3. Selezionare **Verifica aggiuntiva di sicurezza**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. pagina verifica aggiuntiva di sicurezza di Hello carica le impostazioni.

    ![Verifica](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Si desidera toochange numero di telefono o aggiungere un numero secondario
È importante tooconfigure un numero di telefono di autenticazione secondaria.  Poiché primario phone numero e app per dispositivi mobili sono probabilmente in hello stesso telefono, il numero di telefono secondario di hello è unico modo hello sarà in grado di tooget nuovamente al tuo account se il telefono viene smarrito o rubato.

> [!NOTE]
> Se non hanno accesso tooyour numero di telefono principale e assistenza durante il recupero dell'account tooyour, vedere la Guida in [problemi con la verifica](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange numero di telefono primario:**  

1. Nella pagina verifica aggiuntiva di sicurezza di hello, selezionare la casella di testo hello con il numero di telefono corrente e modificarla con il nuovo numero di telefono.  
2. Selezionare **Salva**.  
3. Se si tratta numero hello che verrà usata per l'opzione di verifica preferita, è necessario nuovo numero di tooverify hello prima di poter salvare.  

**tooadd un numero di telefono secondario:**  

1. Nella pagina verifica aggiuntiva di sicurezza di hello, casella di controllo hello accanto troppo**telefono per l'autenticazione alternativo.**  
2. Immettere il numero di telefono secondario nella casella di testo hello.  
3. Selezionare **Salva** e le modifiche sono terminate.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Richiedere di nuovo la verifica in due passaggi in un dispositivo che è stato contrassegnato come attendibile

A seconda delle impostazioni dell'organizzazione si potrebbe avere una casella di controllo del tipo "Non mostrare più la richiesta per **X** giorni" quando si esegue la verifica in due passaggi nel browser. Se questa casella di controllo e quindi perde il dispositivo o ritiene che l'account è compromessa, è necessario ripristinare i dispositivi tooall verifica in due passaggi. 

1. Nella pagina verifica aggiuntiva di sicurezza hello selezionare **ripristino multi-factor authentication per dispositivi precedentemente attendibili**.
2. Hello successivo che si accede in qualsiasi dispositivo, sarà richiesta tooperform la verifica. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Come pulire Microsoft Authenticator dalla periferica precedente e spostare tooa uno nuovo?
Quando si disinstalla l'applicazione hello dal dispositivo o la reimpostazione hello dispositivo, ma non attivazione hello back-end hello. Per altre informazioni, vedere [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Passaggi successivi
* Leggere le informazioni di guida relative ai [problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md)
* Impostare [password di app](multi-factor-authentication-end-user-app-passwords.md) per tutte le applicazioni che non supportano la verifica in due passaggi.
