---
title: aaaThe elementi di posta elettronica di invito collaborazione B2B di Azure Active Directory hello | Documenti Microsoft
description: Modello di messaggio di posta elettronica di invito per la collaborazione B2B di Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>elementi Hello di posta elettronica di invito collaborazione B2B di hello

Messaggi di posta elettronica di invito sono un partner di toobring componente cruciale a bordo come utenti di collaborazione B2B di Azure AD. È possibile utilizzare le attendibilità del destinatario tooincrease hello. è possibile aggiungere legittimità e posta elettronica toohello prova social networking, destinatario hello che toomake abbia dimestichezza con la selezione di hello **iniziare** pulsante invito hello tooaccept. Questa relazione di trust è una chiave tooreduce le forze di attrito di condivisione. E si desidera anche toomake hello posta elettronica aspetto grande!

![Messaggio di posta elettronica di invito per la collaborazione B2B](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Descrivere il messaggio di posta elettronica hello
Ecco alcuni elementi di posta elettronica hello per sapere come meglio toouse le relative funzionalità.

### <a name="subject"></a>Oggetto
oggetto del messaggio di posta elettronica hello Hello segue hello seguente motivo: si è invitati toohello &lt;tenantname&gt; organizzazione

### <a name="from-address"></a>Indirizzo del mittente.
Si utilizzano un modello simile LinkedIn per hello dall'indirizzo.  Si dovrebbe essere chiaro che è di mittente dell'invito hello e da cui società e inoltre aiutare a chiarire che posta elettronica hello proviene da un indirizzo di posta elettronica di Microsoft. formato Hello: &lt;nome visualizzato del mittente dell'invito&gt; da &lt;tenantname&gt; (tramite Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Rispondi a
risposta Hello-tooemail è impostato posta elettronica del mittente toohello quando è disponibile, in modo da rispondere tramite posta elettronica toohello invia un mittente dell'invito toohello indietro di posta elettronica.

### <a name="branding"></a>Personalizzazione
invito di Hello messaggi di posta elettronica dal tenant di usare società hello personalizzazione che potrebbero impostati per il tenant. Se si desidera tootake sfruttare questa funzionalità, [qui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello dettagli su come tooconfigure è. logo banner Hello viene visualizzato nel messaggio di posta elettronica hello. Dimensioni dell'immagine hello seguire le istruzioni di qualità e [qui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) per ottenere risultati ottimali. Inoltre, il nome di società hello viene visualizzato anche in tooaction chiamata hello.

### <a name="call-tooaction"></a>Chiamare tooaction
Hello chiamata tooaction è costituito da due parti: descrivere il motivo per cui destinatario hello ha ricevuto messaggi hello e viene richiesto il destinatario hello toodo su di esso.
- Hello "perché" sezione può essere risolti usando hello seguente motivo: già applicazioni tooaccess invitati hello &lt;tenantname&gt; organizzazione

- La sezione "cosa vi viene richiesto toodo" è indicata dalla presenza di hello di hello hello e **iniziare** pulsante. Quando il destinatario hello è stato aggiunto senza necessità di hello di inviti, questo pulsante non viene visualizzato.

### <a name="inviters-information"></a>Informazioni sul mittente dell'invito
nome visualizzato del mittente Hello è incluso nel messaggio di posta elettronica hello. E, inoltre, se l'installazione di un'immagine del profilo per l'account di Azure AD, hello invito tramite posta elettronica include anche l'immagine. Entrambe è di confidenza del destinatario nel messaggio di posta elettronica hello tooincrease desiderato.

Se ancora stato impostato l'immagine del profilo, viene visualizzata un'icona con iniziali del mittente hello al posto di immagine hello:

  ![visualizzazione iniziali del mittente hello](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Corpo
corpo Hello contiene il messaggio hello che inviter hello compone o viene passato tramite invito hello API. Si tratta di un'area di testo, che quindi non supporta l'elaborazione dei tag HTML per motivi di sicurezza.

### <a name="footer-section"></a>Sezione piè di pagina
piè di pagina Hello contiene marchio di società Microsoft hello e informa il destinatario hello se posta elettronica hello è stato inviato da un alias non monitorato. Casi speciali:

- mittente dell'invito Hello non dispone di un indirizzo di posta elettronica in hello si invitano tenancy

  ![immagine del mittente dell'invito non dispone di un indirizzo di posta elettronica in hello si invitano tenancy](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- destinatario Hello non deve necessariamente invito hello tooredeem

  ![Quando i destinatari non necessario tooredeem invito](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è la collaborazione B2B di Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](active-directory-b2b-admin-add-users.md)
* [Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker](active-directory-b2b-iw-add-users.md)
* [Riscatto dell'invito di Collaborazione B2B](active-directory-b2b-redemption-experience.md)
* [Licenze per la Collaborazione B2B di Azure AD](active-directory-b2b-licensing.md)
* [Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Domande frequenti su Collaborazione B2B di Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalizzazione per Collaborazione B2B di Azure Active Directory](active-directory-b2b-api.md)
* [Autenticazione a più fattori per utenti di Collaborazione B2B](active-directory-b2b-mfa-instructions.md)
* [Aggiungere gli utenti per la Collaborazione B2B senza un invito](active-directory-b2b-add-user-without-invite.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
