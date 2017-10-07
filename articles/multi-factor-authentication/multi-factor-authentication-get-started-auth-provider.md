---
title: Provider di Azure multi-Factor Authentication di avvio aaaGet | Documenti Microsoft
description: Informazioni su come toocreate un Provider di Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Introduzione all'uso di un provider di Azure Multi-Factor Authentication
La verifica in due passaggi è disponibile per impostazione predefinita per gli amministratori globali che si occupano di utenti di Azure Active Directory e Office 365. Tuttavia, se si desidera sfruttare tootake [funzionalità avanzate](multi-factor-authentication-whats-next.md) quindi è necessario acquistare una versione completa di hello di Azure multi-Factor Authentication (MFA).

Viene utilizzato un Provider di Azure multi-Factor Authentication tootake sfruttare le funzionalità fornite da una versione completa di hello di Azure MFA. È destinato agli utenti che **non hanno ottenuto licenze tramite Azure MFA, Azure AD Premium o Enterprise Mobility + Security (EMS)**.  Azure MFA, Azure AD Premium ed EMS includono versione completa hello di Azure MFA per impostazione predefinita. Se si dispone di licenze, non è necessario un provider di Azure Multi-Factor Authentication.

Un provider di Azure multi-Factor Authentication è hello toodownload obbligatorio SDK.

> [!IMPORTANT]
> toodownload hello SDK, è necessario un Provider di Azure multi-Factor Authentication toocreate anche se si dispone di licenze Azure MFA, Azure ad Premium o EMS.  Se si dispone già di licenze a tale scopo, creare un Provider di Azure multi-Factor Authentication, essere certi toocreate hello Provider con hello **Per utente abilitato** modello. Quindi, collegare directory che contiene le licenze di Azure MFA, Azure AD Premium o EMS hello toohello del Provider hello. Questa configurazione assicura che verrà addebitato solo se si dispone di più utenti univoci, eseguire una verifica del numero di hello di licenze possedute in due passaggi.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Che cos'è un provider di Azure Multi-Factor Authentication?

Se non si dispone di licenze per Azure multi-Factor Authentication, è possibile creare una verifica in due passaggi toorequire del provider di autenticazione per gli utenti. Se si sviluppa un'app personalizzata e si desidera tooenable autenticazione a più fattori di Azure, creare un provider di autenticazione e [scaricare hello SDK](multi-factor-authentication-sdk.md).

Esistono due tipi di provider di autenticazione e distinzione hello è intorno come sottoscrizione Azure viene addebitata. opzione di autenticazione basata su Hello calcola il numero di hello di autenticazioni eseguite a fronte del tenant in un mese. Questa opzione è consigliata se si dispone di un numero di utenti che eseguono l'autenticazione solo occasionalmente, come quando si richiede MFA per un'applicazione personalizzata. opzione per ogni utente Hello calcola il numero di hello di persone nel tenant di effettuare la verifica in due fasi in un mese. Questa opzione è migliore se è necessario alcuni utenti con licenza, ma gli utenti di toomore MFA tooextend oltre ai termini della licenza.

## <a name="create-a-multi-factor-auth-provider"></a>Creare un provider di Multi-Factor Authentication
Utilizzare hello seguendo i passaggi toocreate un Provider di Azure multi-Factor Authentication. Provider di Azure multi-Factor Authentication può essere creato solo in hello portale di Azure classico. Se non riesci toohello portale di Azure classico, verificare che sia il tenant di Azure AD toomake [associata a una sottoscrizione di Azure](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore.
2. A sinistra di hello, selezionare **Active Directory**.
3. Nella pagina di Active Directory hello, nella parte superiore di hello, selezionare **provider multi-Factor Authentication**.
   
   ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Nella parte inferiore di hello, fare clic su **New**.
   
   ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. In Servizi app selezionare **Provider di Autenticazione a più fattori**
   
   ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Selezionare **Creazione rapida**.
   
   ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Compilare hello seguente i campi e selezionare **crea**.
   1. **Nome** : hello nome di hello Provider multi-Factor Authentication.
   2. **Modello di utilizzo**: scegliere una delle due opzioni:
      * Per autenticazione: modello di acquisto in cui è previsto l'addebito in base al numero di autenticazioni. Usato, in genere, per scenari in cui viene usato Azure Multi-Factor Authentication in un'applicazione per il consumer.
      * Per utente abilitato: modello di acquisto in cui è previsto l'addebito in base al numero di utenti abilitati. In genere utilizzata per tooapplications accesso dipendente, ad esempio Office 365. Scegliere questa opzione se alcuni utenti dispongono già della licenza per Azure MFA.
   3. **Directory** : hello Azure Active Directory del tenant che hello è associato il Provider di autenticazione a più fattori. Tenere presente i seguenti hello:
      * Non è necessario un toocreate directory Azure AD un Provider multi-Factor Authentication. Lasciare vuoto se si intende solo SDK o hello toodownload Server Azure multi-Factor Authentication.
      * Hello Provider multi-Factor Authentication deve essere associata a un vantaggio tootake directory di Azure AD di hello funzionalità avanzate.
      * È possibile associare un solo provider di Multi-Factor Authentication a una directory di Azure AD.  
      ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Quando si fa clic su Crea, hello viene creato il Provider di autenticazione a più fattori e dovrebbe essere visualizzato un messaggio: **creato correttamente il Provider di autenticazione a più fattori**. Fare clic su **OK**.  
   
   ![Creazione di un provider di MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Gestire il provider di Multi-Factor Authentication

Non è possibile modificare l'utilizzo di hello del modello (per utente abilitato o per l'autenticazione) dopo la creazione di un provider di autenticazione a più fattori. Tuttavia, è possibile eliminare il provider di autenticazione a più fattori hello e quindi crearne uno con un modello di utilizzo diversi.

Se hello corrente i Provider di multi-Factor Authentication è associato a una directory di Azure AD (noto anche come tenant di Azure AD), è possibile eliminare il provider di autenticazione a più fattori hello e creare un tenant toohello collegato stesso Azure Active Directory. In alternativa, se è stato acquistato sufficiente MFA, Azure AD Premium o Enterprise Mobility + Security (EMS) licenze toocover tutti gli utenti che sono abilitati per l'autenticazione a più fattori, è possibile eliminare il provider di autenticazione a più fattori hello completamente.

Se il provider di autenticazione a più fattori non è collegato tooan AD Azure tenant o si collegano tenant hello nuova autenticazione a più fattori provider tooa di Azure AD, le impostazioni utente e le opzioni di configurazione non vengono trasferite. Inoltre, Azure MFA server necessario riattivati con le credenziali di attivazione generate tramite toobe hello nuovo Provider di autenticazione a più fattori. Riattivazione di hello server MFA toolink li toohello nuovo Provider di autenticazione a più fattori non influisce sulla chiamata telefonica e autenticazione dei messaggi di testo, ma le notifiche verranno smettere di funzionare per tutti gli utenti fino a quando la riattivazione di app per dispositivi mobili hello app per dispositivi mobili.

## <a name="next-steps"></a>Passaggi successivi

[Scaricare hello multi-Factor Authentication SDK](multi-factor-authentication-sdk.md)

[Configurare le impostazioni di Multi-Factor Authentication](multi-factor-authentication-whats-next.md)
