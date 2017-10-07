---
title: aaaHow Azure sottoscrizioni associate con Azure Active Directory | Documenti Microsoft
description: Accesso tooMicrosoft Azure e problemi, ad esempio relazione hello tra una sottoscrizione di Azure e Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Associare le sottoscrizioni di Azure ad Azure Active Directory
In questo articolo vengono fornite informazioni sulla relazione hello tra una sottoscrizione di Azure e Azure Active Directory (Azure AD) e come tooadd una directory di Azure AD tooyour sottoscrizione esistente.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure relazione della sottoscrizione di Azure AD
La sottoscrizione di Azure ha una relazione di trust con Azure AD, il che significa che considera attendibili i dispositivi, servizi e utenti tooauthenticate hello. Più sottoscrizioni possono considerare attendibile hello stessa directory, ma ogni sottoscrizione considera attendibile solo una directory. 

relazione di trust Hello che dispone di una sottoscrizione con una directory è diversa dalla relazione hello che con altre risorse in Azure (siti Web, database e così via). Se una sottoscrizione scade, l'accesso toohello arresta anche altre risorse associate alla sottoscrizione hello. Rimane una directory di Azure AD in Azure, ma è possibile associare una sottoscrizione diversa a tale directory e gestire directory hello usando hello nuova sottoscrizione.

![Diagramma che illustra come vengono associate le sottoscrizioni](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Tutti gli utenti dispongono di una singola home directory che li autentica, ma poi possono essere utenti guest in altre directory. In Azure AD, è possibile visualizzare le directory hello di cui l'account utente è un membro o guest.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD e sottoscrizioni di servizi cloud
Azure Active Directory fornisce identità e directory principale di hello funzionalità di gestione dietro la maggior parte dei servizi cloud Microsoft, tra cui:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Quando effettua l'iscrizione per uno di questi servizi cloud Microsoft, si ottiene hello servizio Azure AD gratuito. Se si desidera tooadd una directory tooan Azure AD altra sottoscrizione di Azure, è necessario essere connessi con un account Microsoft. Se si Accedi tooAzure con un lavoro o scuola account, è possibile aggiungere una directory esistente tooan di sottoscrizione di Azure perché l'account aziendale o dell'istituto di istruzione non può essere autenticato direttamente da Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd una directory di Azure AD tooyour sottoscrizione esistente
È necessario accedere con un account esistente in entrambe le directory corrente hello con cui hello è associata la sottoscrizione e nella directory hello desiderato tooadd a. 

1. Accedi toohello [centro Account Azure](https://account.windowsazure.com/Home/Index) con un account che è hello amministratore dell'Account di sottoscrizione hello la cui proprietà si desidera tootransfer.
2. Verificare che tale utente hello indicato come proprietario della sottoscrizione hello toobe si trova nella directory di destinazione hello.
3. Fare clic su **Trasferisci sottoscrizione**.
4. Consente di specificare il destinatario di hello. destinatario Hello ottiene automaticamente un messaggio di posta elettronica con un collegamento di accettazione.
5. destinatario Hello fa clic sul collegamento hello e segue le istruzioni di hello, inclusi immettendo le relative informazioni di pagamento. Quando il destinatario hello ha esito positivo, viene trasferita sottoscrizione hello. 
6. directory predefinita Hello di sottoscrizione hello viene modificato toohello directory utente hello è.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Suggerimenti toomanage una sottoscrizione e una directory
i ruoli amministrativi di Hello per una sottoscrizione di Azure di gestire le risorse collegate toohello sottoscrizione di Azure. Questa sezione illustra le differenze di hello tra amministratori della sottoscrizione di Azure e Azure AD amministratori di directory. Ruoli amministrativi e altri suggerimenti per l'utilizzo di toomanage la sottoscrizione sono illustrati nel [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).

Per impostazione predefinita, è stato assegnato il ruolo di amministratore del servizio hello quando effettua l'iscrizione. Se altri utenti necessario toosign in e accedere ai servizi utilizzando hello stessa sottoscrizione, è possibile aggiungerli come coamministratori. 

Azure AD include un set diverso di directory di ruoli amministrativi toomanage hello e funzionalità correlate alle identità. Messaggio per l'amministratore globale di una directory può, ad esempio, aggiungere utenti e directory toohello gruppi oppure richiedere l'autenticazione a più fattori per gli utenti. Un utente che crea una directory è assegnato il ruolo di amministratore globale toohello e ruoli amministrativi possono assegnare gli utenti tooother. I ruoli amministrativi di Azure AD vengono anche usati da altri servizi, ad esempio Office 365 e Microsoft Intune. 

Gli amministratori della sottoscrizione di Azure e gli amministratori della directory di Azure AD sono due ruoli distinti. 
* Gli amministratori delle sottoscrizioni di Azure possono gestire le risorse in Azure e possono usare Azure AD nel portale di Azure hello (poiché hello portale Azure è una risorsa di Azure). 
* Gli amministratori di directory possono gestire le proprietà solo nella directory di Azure AD hello.

Una persona può rivestire entrambi i ruoli, ma non è obbligatorio. Non è possibile assegnare a un amministratore globale della directory un ruolo di amministratore del servizio o di coamministratore di una sottoscrizione di Azure e viceversa. Senza essere amministratore della sottoscrizione di hello, utente hello toohello portale di Azure per poter accedere, ma non è possibile gestire directory hello per la sottoscrizione nel portale di hello. Tuttavia, questo utente può gestire directory utilizzando altri strumenti, ad esempio Azure AD PowerShell o hello centro di amministrazione di Office 365.

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sugli amministratori toochange per una sottoscrizione di Azure, vedere [trasferire la proprietà di un account di sottoscrizione di Azure tooanother](../billing/billing-subscription-transfer.md)
* toolearn ulteriori informazioni sulla modalità di controllo di accesso alle risorse in Microsoft Azure, vedere [informazioni di accesso alle risorse di Azure](active-directory-understanding-resource-access.md)
* Per ulteriori informazioni su come tooassign ruoli in Azure AD, vedere [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
