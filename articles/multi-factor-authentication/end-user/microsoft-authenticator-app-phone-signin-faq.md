---
title: aaaMicrosoft autenticatore phone Accedi - account Azure e Microsoft | Documenti Microsoft
description: "Utilizzare il toosign phone tooyour account Microsoft anziché digitare la password. Questo articolo risponde alle domande frequenti su questa funzionalità."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Accedere con il telefono, non con la password

app Microsoft Authenticator Hello consente di proteggere gli account per eseguire una verifica in due passaggi dopo aver immesso la password. Ma non tutti sanno che può sostituire completamente password hello per l'account Microsoft personale? 

Questa funzionalità è disponibile su dispositivi iOS e Android e funziona con gli account personali di Microsoft. 

## <a name="how-it-works"></a>Funzionamento

App Microsoft Authenticator hello di utilizzare per la verifica in due passaggi quando si accede tooyour account Microsoft. Si digita la password, quindi passare toohello app tooeither approvare una notifica o ottenere un codice di verifica. Con phone Accedi, si ignorare password hello ed eseguire le operazioni la verifica dell'identità sul telefono. Poiché Accedi phone sono un tipo di verifica in due passaggi, è comunque necessario tooprovide una cosa si conosce e una cosa tooverify la tua identità. telefono Hello è ancora cosa hello e PIN o la chiave biometrici il telefono è hello che noto. 

## <a name="how-tooget-started"></a>La modalità di avvio tooget

toosign in tooyour account Microsoft personale con il telefono, seguire questi passaggi: 

1. Abilitare l'accesso all'account personale tramite telefono. 

  - Se non è necessario app Microsoft Authenticator hello ancora, installare e aggiungere l'account Microsoft personale in base a passaggi toohello in hello [pagina Microsoft Authenticator](microsoft-authenticator-app-how-to.md). Vengono attivati automaticamente gli account appena aggiunti, in modo da essere toogo valido.

  - Se si utilizza già Microsoft Authenticator per la verifica in due passaggi, selezionare l'account dalla home page di hello app e selezionare **abilitare Accedi phone** dal menu a discesa hello.

  >[!NOTE] 
  >tooprotect il tuo account, è necessario un PIN o un blocco biometrica nel dispositivo. Se si mantengono il telefono sbloccato, viene visualizzata una richiesta di cui si chiede tooset di un blocco prima di abilitare Accedi phone app hello. 

3. La maggior parte delle pagine in cui in genere l'utente inserisce la password dell'account di Microsoft ha un collegamento che dice **Usa un'app**. Selezionare questo toosign collegamento con il telefono. 

4. Microsoft invierà un telefono tooyour di notifica. Approvare hello notifica toosign tooyour account.   

## <a name="faq"></a>domande frequenti 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>In che modo l'accesso tramite telefono è più sicuro dell'accesso tramite password?  

Oggi la maggior parte delle persone Accedi tooweb siti o applicazioni utilizzando un nome utente e password.  Sfortunatamente, le password spesso vengono smarrite, rubate o individuate da pirati informatici. Quando si configura hello Microsoft Authenticator app toosign in, è generare una chiave sul telefono in grado di sbloccare l'account. Proteggiamo questa chiave con hello PIN o biometrici che già in uso sul telefono.  Quando si accede con il telefono, questa chiave è tooprove usato la tua identità in modo sicuro con due fattori: hello phone stesso e toounlock il possibilità è. 

chiave Hello utilizzata è simile chiavi toohello usate in Windows Hello e specifiche FIDO Alliance UAF hello. La biografia sono solo di dati usato tooprotect hello chiave in locale e viene mai inviata a o nel cloud hello. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>In cui è possibile usare il tooreplace phone password e, in cui è ancora necessario password hello?  

Funzione di accesso del telefono hello oggi, funziona solo con le applicazioni web e servizi che vengono compilati in App in Windows 10 che utilizzano un account Microsoft personale, iOS o App per Android che utilizzano un account Microsoft personale e gli account Microsoft personali. Quando si accede tooone di questi siti web o applicazioni, nella pagina hello in cui è in genere immettere la password è presente un collegamento che afferma **in alternativa, usare un'app**. 

Accedi telefono non possono essere utilizzato toounlock un PC Windows, XBOX o tutte le versioni desktop di App di Microsoft, ad esempio le app di Office in questo momento. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Questa funzione sostituisce la verifica in due passaggi? È consigliabile disattivarla?   

In alcuni casi sì. Si sta lavorando espande ambito hello di Accedi phone, ma per ora sono ancora presenti posizioni nell'ecosistema Microsoft hello che non lo supporta. In questi casi, viene usata ancora la verifica in due passaggi per eseguire un accesso sicuro. Per questo motivo, no, non è consigliabile disattivare la verifica in due passaggi per l'account. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>Dunque, se verifica in due passaggi attivata per l'account, è necessario tooapprove due notifiche?

No. Accesso tooyour account Microsoft con il telefono viene considerata verifica in due passaggi. Anziché digitare la password, quindi una notifica di approvazione dimostrare la propria identità conoscendo come toounlock telefono e quindi approvato una notifica. Invieremo è un secondo tooapprove di notifica.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>Se perdo il telefono o non ce l'ho con me, come eseguo l'accesso all'account?  

È sempre possibile fare clic su **in alternativa, usare una password** sulla hello nella pagina di accesso tooswitch annullare toousing la password. Tenere presente che se si utilizza la verifica, è necessario un tooverify metodo secondo accesso. Questo motivo si consiglia di avere info di sicurezza aggiuntivo, aggiornata con l'account toomake. È possibile gestire le informazioni di sicurezza all'indirizzo https://account.live.com/proofs/manage. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Come interrompere l'uso di questa funzionalità e tornare tooentering password?

Fare clic su **Use a password instead** (Usa la password) quando si accede. Si ricorda la scelta più recente e che offrono da hello predefinito successivo che accesso. Se si vuole usare toosigning indietro toogo con il telefono, fare clic su **in alternativa, usare un'app**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>È possibile utilizzare toosign app hello in tooall account personali con Microsoft?   
Questa funzionalità è disponibile solo per gli account personali di Microsoft al momento. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>È possibile accedere al mio PC con il telefono?  
Per il PC, è consigliabile accedere con Windows Hello in Windows 10 usando l'immagine, l'impronta digitale o un PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>È possibile accedere con il mio Windows Phone?  
In questo momento, non stiamo sviluppando questa funzionalità per hello Microsoft Authenticator in Windows Phone. 

## <a name="next-steps"></a>Passaggi successivi
Se è stato scaricato l'app Microsoft Authenticator hello, estrarlo. è disponibile per l'applicazione Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), e phone sign-in è disponibile in app di Microsoft Authenticator hello per [Android](http://go.microsoft.com/fwlink/?Linkid=825072) e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

In caso di domande sull'applicazione hello in generale, dare un'occhiata hello [domande frequenti di autenticazione Microsoft](microsoft-authenticator-app-faq.md)
