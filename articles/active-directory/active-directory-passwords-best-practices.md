---
title: 'Implementazione: Reimpostazione password self-service di Azure AD | Microsoft Docs'
description: Consigli per l'implementazione della reimpostazione password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Implementare la reimpostazione della password per gli utenti

La maggior parte dei clienti seguono passaggi hello tooensure una facile implementazione della funzionalità SSPR.

1. [Abilitare la reimpostazione della password nella directory](active-directory-passwords-getting-started.md)
2. [Configurare le autorizzazioni AD locali per il writeback delle password](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Configurare il writeback delle password](active-directory-passwords-writeback.md#configuring-password-writeback) password toowrite da Azure AD eseguire il backup di directory locale tooyour
4. [Assegnare e verificare le licenze necessarie](active-directory-passwords-licensing.md)
5. Se si desidera tooroll, gradualmente, è possibile facoltativamente limite reimpostazione della password tooa gruppo di utenti tooroll funzione hello lentamente nel tempo. toodo questo impostato hello **Self Service per la Password Reimposta abilitato** passare dal **tutti gli utenti** troppo**un gruppo** e selezionare un tooenable del gruppo di sicurezza per la reimpostazione della password. devono tutti avere licenze assegnate toothem Hello membri di questo gruppo ed è un ottimo modo tooenable [gruppo basato su licenze](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Numero minimo di hello popolare [dati di autenticazione](active-directory-passwords-data.md), in base ai criteri.
7. Indicare agli utenti come toouse SSPR, inviando istruzioni tooshow li come tooregister e come tooreset.
    > [!NOTE]
    > Testare la reimpostazione password self-service con un utente e non con un amministratore, perché Microsoft applica requisiti di autenticazione avanzata per gli account di tipo amministratore di Azure. Per altre informazioni sui criteri password di amministratore hello, vedere il nostro [articolo approfondimento](active-directory-passwords-how-it-works.md).

8. È possibile scegliere tooenforce registrazione in qualsiasi momento e richiedono tooreconfirm agli utenti le informazioni di autenticazione dopo un certo periodo di tempo. Se non si desidera il tooregister toohave gli utenti, è possibile [distribuire password reimpostare senza richiedere la registrazione dell'utente finale](active-directory-passwords-data.md).
9. Nel corso del tempo, esaminare gli utenti che la registrazione e l'utilizzo visualizzando hello [reporting fornite da Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Implementazione basata sulla posta elettronica

Molti clienti di trovare che una campagna di posta elettronica, con istruzioni toouse semplice, è hello più semplice modo tooget utenti toouse SSPR. [Sono stati creati tre semplici messaggi di posta elettronica che è possibile utilizzare come modelli toohelp nell'implementazione.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Presto disponibile** toobe modello utilizzato in settimane hello o giorni prima dell'implementazione toolet informarli devono toodo qualcosa di posta elettronica.
* **Ora disponibili** modello toobe utilizzato hello giorno avvio toodrive utenti tooregister di posta elettronica e confermare i propri dati di autenticazione, quindi possono essere utilizzate SSPR in qualsiasi momento.
* **Effettuare l'iscrizione promemoria** modello per alcuni giorni tooweeks di posta elettronica dopo la distribuzione tooremind utenti tooregister e confermare i propri dati di autenticazione.

## <a name="creating-your-own-password-portal"></a>Creazione del portale delle password

Molti clienti maggiori scegliere la pagina Web toohost e creare una voce DNS, ad esempio https://passwords.contoso.com radice. Appartengono a questa pagina con collegamenti toohello Azure AD la reimpostazione della password, la registrazione, i portali di modifica delle password e altre informazioni specifiche dell'organizzazione di reimpostazione della password. In qualsiasi comunicazioni tramite posta elettronica o volantini, si inviano, è possibile quindi includere un marchio, facili da ricordare, che gli utenti possono accedere toowhen devono servizi hello toouse URL.

* Portale di reimpostazione della password: https://passwordreset.microsoftonline.com/
* Portale di registrazione per la reimpostazione della password: http://aka.ms/ssprsetup
* Portale di modifica della password: https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Uso della registrazione applicata

Se si desidera il tooregister gli utenti per la reimpostazione della password, è possibile forzare li tooregister quando effettuano l'accesso tramite Azure AD. È possibile abilitare questa opzione della directory **di reimpostazione della Password** pannello abilitando hello **tooRegister richiedere agli utenti quando si accede a** opzione hello **registrazione** scheda.

Gli amministratori possono richiedere agli utenti la registrazione toore dopo un periodo di tempo dall'impostazione hello **numero di giorni prima che gli utenti frequenti tooreconfirm le informazioni di autenticazione** compreso tra 0 e 730 giorni.

Dopo aver abilitato questa opzione, gli utenti firma verranno visualizzato un messaggio che informa l'amministratore ha richiesto loro tooverify le informazioni di autenticazione.

## <a name="populate-authentication-data"></a>Popolare i dati di autenticazione

Se si [popolare i dati di autenticazione per gli utenti](active-directory-passwords-data.md), quindi gli utenti non richiedono tooregister per la reimpostazione prima di essere in grado di toouse SSPR password. Fino a quando gli utenti dispongono di dati di autenticazione hello definiti che soddisfa i criteri di reimpostazione password hello è definito, gli utenti sono in grado di tooreset le proprie password.

## <a name="disabling-self-service-password-reset"></a>Disabilitazione della reimpostazione self-service della password

La disabilitazione di reimpostazione della password self-service è semplice come l'apertura di tenant di Azure AD e in uscita troppo**di reimpostazione della Password**, **proprietà**e scegliendo **Nessuno** in  **Self-Service di reimpostazione della Password abilitata**

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR
