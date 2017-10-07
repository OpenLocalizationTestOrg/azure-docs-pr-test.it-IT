---
title: verifica in due passaggi aaaTroubleshoot | Documenti Microsoft
description: Questo documento fornisce informazioni su quali toodo se si verifica un problema con Azure multi-Factor Authentication.
services: multi-factor-authentication
keywords: client di multi-factor authentication, problema di autenticazione, ID di correlazione
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: f5c980d104de684b052c0f7a13394f00e9828abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-help-with-two-step-verification"></a>Informazioni sulla verifica in due passaggi
In questo articolo risponde alle domande più comuni di hello che gli utenti richiedono sulla verifica in due passaggi. 

## <a name="why-do-i-have-tooperform-two-step-verification-can-i-turn-it-off"></a>Motivo per cui dispone la verifica in due passaggi tooperform? È possibile disattivarla?

Verifica in due passaggi è una funzionalità di sicurezza che l'organizzazione abbia scelto toouse tooprotect gli account. È un metodo più sicuro rispetto alla sola password perché si basa su due forme di autenticazione: un elemento noto e un elemento che l'utente ha con sé. Hello qualcosa che si conosce la password. Hello qualcosa che avere con sé è un telefono o un dispositivo che è in genere con l'utente. Quando l'account è protetto da verifica in due passaggi, che significa che un utente malintenzionato non può effettuare l'accesso come se ne ricevono in qualche modo la password perché non hanno phone tooyour accesso troppo. 

Microsoft offre la verifica in due passaggi, ma funzionalità hello toouse scelta dall'organizzazione. Se il reparto IT richiede, esattamente come non possono rifiutare esplicitamente tooprotect una password utilizzando l'account è non è possibile rifiutare esplicitamente. 

Se si dispone di verifica in due passaggi attivata per l'account Microsoft personale e si desidera toochange le impostazioni, leggere [sulla verifica in due passaggi](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) invece. 

## <a name="i-dont-have-my-phone-with-me-today"></a>Telefono momentaneamente non disponibile

Alcuni giorni si lascia il telefono a casa, ma comunque necessario toosign al lavoro. innanzitutto Hello che è consigliabile provare viene effettuato un altro metodo di verifica. Durante la registrazione per la verifica in due passaggi, stato è impostato più di un numero di telefono? tootry accesso con un metodo diverso, seguire questi passaggi:

1. Accedere come si farebbe normalmente.
2. Quando verrà visualizzata la pagina di verifica in due passaggi hello, scegliere **utilizzare un'altra opzione di verifica**.

   ![Verifica diversa](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selezionare l'opzione di verifica hello da toouse.
4. Procedere con la verifica in due passaggi.

Se non viene visualizzato hello **utilizzare un'altra opzione di verifica** collegare, quindi ciò significa che è stata impostata metodi alternativi durante la prima registrazione per la verifica in due passaggi. Contattare la Guida tooget del reparto IT tooyour account l'accesso. Una volta effettuato, verificare troppo[gestire le impostazioni di](multi-factor-authentication-end-user-manage-settings.md) tooadd ulteriori metodi di verifica per la volta successiva. 

Se viene visualizzato hello **utilizzare un'altra opzione di verifica** collegamento, ma non è tooyour metodi alternativi per l'accesso, contattare la Guida tooget del reparto IT tooyour account l'accesso. 

## <a name="i-lost-my-phone-or-got-a-new-number"></a>Telefono perso o nuovo numero
Esistono due modi tooget in tooyour account. Hello viene innanzitutto toosign utilizzando il numero di telefono di autenticazione alternativo, se è stato configurato uno. Hello in secondo luogo è il tooclear reparto IT tooask le impostazioni.

Se il telefono è stato perso o rubato, è inoltre consigliabile informare il reparto IT in modo che possa reimpostare le password dell'app e cancellare eventuali dispositivi memorizzati. 

### <a name="use-an-alternate-phone-number"></a>Usare un numero di telefono alternativo
Se è stata impostata più opzioni di verifica, ad esempio un numero di telefono secondario o di un'app di autenticazione in un altro dispositivo, è possibile utilizzare uno di essi toosign in.

toosign con numero di telefono alternativo hello, seguire questi passaggi:

1. Accedere come si farebbe normalmente.
2. Quando richiesto toofurther verificare il tuo account, scegliere **utilizzare un'altra opzione di verifica**.
   
   ![Verifica diversa](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Selezionare il numero di telefono hello o un dispositivo che è possibile accedere.
4. Dopo aver verificato nel proprio account, [gestire le impostazioni di](multi-factor-authentication-end-user-manage-settings.md) toochange l'autenticazione il numero di telefono.

### <a name="clear-your-settings"></a>Cancellare le impostazioni
Se non è stato configurato un numero di telefono di autenticazione secondaria, è necessario toocontact il reparto IT per assistenza. Hanno li crittografato hello così le impostazioni successivo di accesso, verrà richiesto troppo[registrare per la verifica in due passaggi](multi-factor-authentication-end-user-first-time.md) nuovamente.

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>Non ricevo messaggi o chiamate sul telefono
Esistono diversi motivi, perché è possibile provare toosign in, ma non ricevere testo hello o chiamata telefonica. È stato ricevuto correttamente testi o telefonate tooyour telefono in hello precedente, si tratta probabilmente un problema con provider phone hello, non l'account. Assicurarsi che si dispone di segnale cella valida e se si sta tentando di tooreceive un messaggio di testo assicurarsi che si è in grado di toorecieve messaggi di testo. Richiedere un toocall friend è o testo come un test. 

Se si siano trascorse diversi minuti prima che un SMS o telefonata, tooget modo più veloce di hello al tuo account è tootry un'opzione diversa.

1. Selezionare **utilizzare un'altra opzione di verifica** nella pagina hello che è in attesa per la verifica.
   
    ![Verifica diversa](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. Selezionare hello phone numero o recapito metodo da toouse.
   
    Se sono stati ricevuti più codici di verifica, utilizzare hello più recente.

Se non si dispone di un altro metodo configurato, contattare il reparto IT e chiedergli di provvedere tooclear le impostazioni. Hello successivo accesso, verrà richiesto troppo[configurare l'autenticazione a più fattori](multi-factor-authentication-end-user-first-time.md) nuovamente.

Se si dispone spesso ritardi a causa del segnale di cella toobad, si consiglia di usare hello [app Authenticator Microsoft](microsoft-authenticator-app-how-to.md) sul tuo smartphone. app Hello può generare codici di sicurezza casuale da utilizzare toosign in, e questi codici non richiedono qualsiasi connessione internet o di segnale di cella.

## <a name="app-passwords-are-not-working"></a>Le password dell'app non funzionano
Innanzitutto, assicurarsi di avere immesso la password di app hello correttamente. password dell'app Hello generato sostituisce la normale password, ma solo per le applicazioni desktop precedenti che non supportano la verifica in due passaggi. Se ancora non funziona, provare ad accedere e [creare una nuova password dell'app](multi-factor-authentication-end-user-app-passwords.md).  Se il problema persiste, contattare il reparto IT e chiedere di [eliminare le password dell'app esistenti](../multi-factor-authentication-manage-users-and-devices.md) in modo da poter creare una nuova password.

## <a name="i-didnt-find-an-answer-toomy-problem"></a>Non è possibile individuare un problema di risposta toomy.
Se dopo aver provato queste procedure si continua a riscontrare problemi, contattare il reparto IT Devono essere in grado di tooassist è.

## <a name="related-topics"></a>Argomenti correlati
* [Gestire le impostazioni per la verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md)  
* [Domande frequenti sull'applicazione Microsoft Authenticator](microsoft-authenticator-app-faq.md)

