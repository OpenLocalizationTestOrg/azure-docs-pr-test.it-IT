---
title: 'Guida introduttiva: Reimpostazione password self-service di Azure AD | Microsoft Docs'
description: Distribuire rapidamente la reimpostazione self-service della password di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Guida introduttiva: Reimpostazione self-service della password di Azure AD

> [!IMPORTANT]
> **Se si sta visualizzando questa pagina perché si riscontrano problemi nell'accesso,** [seguire questa procedura per cambiare e reimpostare la password](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Distribuire rapidamente la reimpostazione self-service della password

Reimpostazione della password self-service (SSPR) offre un semplice significa che per tooreset di utenti tooempower gli amministratori IT o sbloccare le password o account. Hello sistema include tootrack report dettagliati quando gli utenti utilizzano il sistema di hello e notifiche tooalert si toomisuse o evitare eventuali abusi.

Questa guida presuppone che sia già disponibile un tenant di valutazione o con licenza di Azure AD. Se è necessario informazioni sull'impostazione di Azure AD, vedere l'articolo hello [introduzione AD Azure](https://azure.microsoft.com/trial/get-started-active-directory/).

1. Nel tenant di Azure AD esistente, selezionare **"Reimpostazione password"**

2. Da hello **"Proprietà"** schermata opzione hello "Self Service Password reimpostato Enabled" scegliere uno dei seguenti hello
    * Nessuno - Nessuna uno è una funzionalità SSPR toouse in grado di
    * Un gruppo, solo i membri di un annuncio di Azure specifico gruppo che si sceglie sono in grado di toouse SSPR funzionalità
    * Tutti gli utenti - tutti gli utenti con account nel tenant di Azure AD sono funzionalità SSPR toouse in grado di

3. Da hello **"Metodi di autenticazione"** schermata scegliere
    * Numero di metodi richiesto tooreset: È supportato un minimo di uno o a un massimo di due
    * Toousers disponibili metodi - è necessario almeno un ma mai di influisce negativamente sulle toohave un'opzione aggiuntiva disponibile
        * **Messaggio di posta elettronica** invia un messaggio di posta elettronica a un utente toohello codice configurata dell'indirizzo di posta elettronica di autenticazione
        * **Cellulare** offre hello utente hello scelta tooreceive una chiamata o di testo con un codice di tootheir configurato il numero di telefono cellulare
        * **Telefono ufficio** utente hello chiamate con un codice di tootheir configurato numero di telefono dell'ufficio
        * **Domande di sicurezza** richiede toochoose
            * Numero di domande richiesto tooregister: minimo hello per la registrazione ha esito positivo, vale a dire un utente può scegliere tooanswer toocreate più un pool di domande toopull da. Questa opzione può essere impostata da 3 a 5 e deve essere maggiore o uguale toohello numero di domande necessarie tooreset.
                * Fare clic sul pulsante "Custom" hello quando la selezione delle domande di sicurezza è possono aggiungere alle domande più comuni
            * Numero di domande necessarie tooreset - può essere impostato da 3 a 5 domande toobe ha risposto correttamente prima di consentire un toobe di password utenti, reimpostare o sbloccato.

4. CONSIGLIATO: **"Personalizzazione"** consente toochange hello "Contattare l'amministratore di" collegamento toopoint tooa pagina o l'indirizzo email è definire

5. Facoltativo: hello **"Registration"** schermata offre agli amministratori opzioni hello per:
    * Richiedi tooregister gli utenti durante l'accesso
    * Numero di giorni prima che gli utenti frequenti tooreconfirm le informazioni di autenticazione

6. Facoltativo: hello **"Notifica"** schermata offre agli amministratori le opzioni di hello per:
    * Inviare notifiche agli utenti al momento della reimpostazione della password
    * Inviare una notifica a tutti gli amministratori quando altri amministratori reimpostano le proprie password

**A questo punto è stata configurata la reimpostazione password self-service per il tenant di Azure AD**. È possibile interrompere la procedura o continuare a tooconfigure sincronizzazione delle password tooan locale dominio di Active Directory.

> [!NOTE]
> Testare la reimpostazione password self-service con un utente e non con un amministratore, perché Microsoft applica requisiti di autenticazione avanzata per gli account di tipo amministratore di Azure. Per altre informazioni sui criteri password di amministratore hello, vedere il nostro [articolo criteri password](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Configurare l'origine di sincronizzazione tooexisting identità

tooenable tooAzure sincronizzazione identità Active Directory in locale, è necessario tooinstall e configurare [Azure AD Connect](./connect/active-directory-aadconnect.md) in un server all'interno dell'organizzazione. Questa applicazione gestisce la sincronizzazione utenti e gruppi dal tenant di Azure AD tooyour esistente origine identità.

* [Eseguire l'aggiornamento da DirSync o Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Introduzione alle impostazioni rapide per Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)
* [Configurare il writeback delle password](active-directory-passwords-writeback.md#configuring-password-writeback) password toowrite da Azure AD eseguire il backup di directory locale tooyour.

## <a name="disabling-self-service-password-reset"></a>Disabilitazione della reimpostazione self-service della password

La disabilitazione di reimpostazione della password self-service è semplice come l'apertura di tenant di Azure AD e in uscita troppo**di reimpostazione della Password > proprietà** > scegliere **Nessuno** in **reimpostazione Password Self-Service Abilitato**

### <a name="learn-more"></a>Altre informazioni
Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come la reimpostazione della password self-service tooconfigure per gli utenti. toocontinue toohello Azure toocomplete portale, seguono questi passaggi hello collegamento sotto toohello portale.

> [!div class="nextstepaction"]
> [Abilitare la reimpostazione self-service delle password](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

