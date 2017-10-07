---
title: 'Azure AD Connect: funzionamento dell''accesso Single Sign-On facile | Microsoft Docs'
description: "In questo articolo viene descritto il funzionamento hello Azure Active Directory trasparente funzionalità Single Sign-On."
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Accesso Single Sign-On facile di Azure Active Directory: approfondimento tecnico

Questo articolo riporta i dettagli tecnici in hello Azure Active Directory trasparente Single Sign-On (SSO trasparente) funzionamento.

>[!IMPORTANT]
>caratteristica di SSO trasparente Hello è attualmente in anteprima.

## <a name="how-does-seamless-sso-work"></a>Come opera la SSO facille?

In questa sezione presenta due parti tooit:
1. Hello il programma di installazione della funzionalità SSO trasparente hello.
2. Funzionamento di una transazione di accesso utente singolo con SSO facile.

### <a name="how-does-set-up-work"></a>Installazione

L'accesso SSO facile viene abilitato con Azure AD Connect, come illustrato [qui](active-directory-aadconnect-sso-quick-start.md). Durante l'abilitazione di funzionalità hello, si verifica hello alla procedura seguente:
- Un account computer denominato `AZUREADSSOACCT`, che rappresenta Azure AD, viene creato in Active Directory (AD) locale.
- chiave di decrittografia Kerberos dell'account del computer Hello è condivisa in modo sicuro con Azure AD.
- Inoltre, due Kerberos nomi dell'entità servizio (SPN) vengono creati due URL toorepresent utilizzati durante l'accesso AD Azure.

>[!NOTE]
> vengono creati account di computer Hello e i nomi SPN Kerberos hello in ogni foresta di Active Directory si sincronizza tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera SSO senza problemi. Spostare hello `AZUREADSSOACCT` tooan account computer unità Organizzativa in cui sono archiviate tooensure che è gestito in altri account di computer hello stesso modo e non viene eliminato.

>[!IMPORTANT]
>È consigliabile si [rollover chiave di decrittografia Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) di hello `AZUREADSSOACCT` account computer almeno ogni 30 giorni.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Funzionamento dell'accesso SSO facile

Una volta completata l'installazione di hello, SSO trasparente funziona hello stesso modo di qualsiasi altra Accedi che utilizza l'autenticazione integrata di Windows (IWA). flusso Hello è come segue:

1. utente di Hello tenta tooaccess un'applicazione (ad esempio, hello Outlook Web App - https://outlook.office365.com/owa/) da un dispositivo azienda appartenenti a un dominio all'interno della rete aziendale.
2. Se l'utente hello non è già effettuato l'accesso, utente hello è reindirizzato toohello Azure AD nella pagina di accesso.

  >[!NOTE]
  >Se hello Azure AD Accedi richiesta include un `domain_hint` (identificazione del tenant, ad esempio, contoso.onmicrosoft.com) o `login_hint` (identificazione utente hello - ad esempio, user@contoso.onmicrosoft.com o user@contoso.com) parametro, quindi il passaggio 2 è stata ignorata.

3. tipi di utente Hello in nome utente nella pagina di accesso hello Azure AD.
4. Utilizzo di JavaScript nel background hello, il Azure AD richiede browser hello, tramite una risposta 401 non autorizzato, tooprovide un ticket Kerberos.
5. browser Hello, a sua volta, richiede un ticket da Active Directory per hello `AZUREADSSOACCT` account computer (rappresentato da Azure AD).
6. Active Directory individua account computer hello e restituisce un browser toohello del ticket Kerberos crittografato con la chiave privata dell'account del computer hello.
7. browser Hello inoltra il ticket Kerberos hello acquisito da Active Directory tooAzure Active Directory (in uno dei hello [gli URL di Azure Active Directory aggiunti in precedenza le impostazioni di zona Intranet del browser toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD esegue la decrittografia hello ticket Kerberos, che include l'identità di hello dell'utente hello effettuato l'accesso a dispositivi aziendali hello, utilizzate in precedenza hello di chiave condivisa.
9. Dopo aver valutato, Azure Active Directory restituisce una token toohello indietro di applicazione o chiede hello utente tooperform prove aggiuntive, ad esempio multi-Factor Authentication.
10. Se hello utente Accedi ha esito positivo, l'utente hello è tooaccess in grado di un'applicazione hello.

Hello diagramma seguente illustra tutti i componenti di hello e hello passaggi della procedura.

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso2.png)

SSO trasparente è opportunistico, vale a dire in caso contrario, esperienza di accesso hello fallback comportamento normale tooits - ad esempio, hello utente deve tooenter toosign le password in.

## <a name="next-steps"></a>Passaggi successivi

- [**Guida introduttiva**](active-directory-aadconnect-sso-quick-start.md): avvio ed esecuzione di Accesso SSO facile di Azure AD.
- [**Domande frequenti su** ](active-directory-aadconnect-sso-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
