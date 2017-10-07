---
title: aaaHow tooget un tenant di Azure AD | Documenti Microsoft
description: Come tooget di Azure Active Directory del tenant per la registrazione e la creazione di applicazioni.
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Come tenant di Azure Active Directory tooget
In Azure Active Directory (Azure AD), un [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) rappresenta un'organizzazione.  È un'istanza dedicata di hello servizio di Azure AD che un'organizzazione riceve e diventa proprietaria quando effettua l'iscrizione a un servizio cloud Microsoft, ad esempio Azure, Microsoft Intune o Office 365.  Ogni tenant di Azure AD è distinto e separato dagli altri tenant di Azure AD.  

Un tenant ospita utenti hello in una società e hello le relative informazioni - loro password, i dati del profilo utente, autorizzazioni e così via.  Contiene inoltre i gruppi, applicazioni e altre informazioni correlate tooan organizzazione e la protezione.

tooallow toosign agli utenti di Azure AD nell'applicazione tooyour, è necessario registrare l'applicazione in un tenant di proprie.  La pubblicazione di un'applicazione in un tenant di Azure AD è **assolutamente gratuita**.  Infatti, la maggior parte degli sviluppatori crea più tenant e applicazioni a fini di sperimentazione, sviluppo, staging e test.  Le organizzazioni che iscriversi e usano l'applicazione è possono scegliere facoltativamente licenze toopurchase se desiderano tootake sfruttare le funzionalità avanzate di directory.

Come ottenere un tenant di Azure AD  Hello processo potrebbe risultare poco diverso se si:

* [Si ha un abbonamento a Office 365](#use-an-existing-office-365-subscription)
* [Si ha una sottoscrizione di Azure precedente, associata a un account Microsoft](#use-an-msa-azure-subscription)
* [Si ha una sottoscrizione di Azure precedente, associata a un account aziendale](#use-an-organizational-azure-subscription)
* [Nessuno di hello precedente & desidera toostart da zero](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Usare una sottoscrizione di Office 365 esistente
Se si ha una sottoscrizione di Office 365 esistente, si ha già un tenant di Azure AD. È possibile accedere toohello [portale di Azure](https://portal.azure.com) con il O365 account e iniziare a usare Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Usare una sottoscrizione di Azure associata a un account Microsoft
Se in precedenza è stata creata una sottoscrizione di Azure usando il proprio account Microsoft personale, si ha già un tenant.  Quando si accede toohello [portale Azure](https://portal.azure.com), verrà registrato automaticamente nel tenant di tooyour predefinito. Si è gratuita toouse vedere questo tenant come si adatta - ma è opportuno toocreate un account amministratore dell'organizzazione.

toodo in tal caso, seguire questi passaggi.  In alternativa, è possibile desidera toocreate un nuovo tenant e creare un amministratore nel tenant seguendo un processo simile.

1. Accedere al hello [portale Azure](https://portal.azure.com) con l'account singoli
2. Sezione "Azure Active Directory" toohello del portale hello passare (trovato nella barra di spostamento sinistro hello in **più servizi**)
3. Deve essere firmato automaticamente in toohello "Directory predefinita", se non è possibile passare alla directory facendo clic sul nome account nell'angolo superiore destro di hello.
4. Da hello **operazioni rapide** , scegliere **aggiungere un utente**.
5. In Aggiungi utente Form hello, fornire hello seguenti dettagli:

   * Nome: scegliere un valore appropriato
   * Nome utente: scegliere un nome utente per questo amministratore
   * Profilo: (compilare i valori appropriati di hello per nome, cognome, il titolo professionale e reparto)
   * Ruolo: Amministratore globale
6. Dopo aver completato hello Aggiungi Form utente e ricevere hello password temporanea per nuovo utente amministratore hello, toorecord che la password perché sarà necessaria toologin con il nuovo utente nella password hello toochange di ordine. È anche possibile inviare password hello direttamente toohello utente, tramite messaggio di posta elettronica alternativo.
7. Fare clic su **crea** nuovo utente di toocreate hello.
8. password temporanea toochange hello, accedere [https://login.microsoftonline.com](https://login.microsoftonline.com) con questo nuovo utente dell'account e modificare la password di hello quando richiesto.

## <a name="use-an-organizational-azure-subscription"></a>Usare una sottoscrizione di Azure aziendale
Se in precedenza è stata creata una sottoscrizione di Azure usando il proprio account aziendale, si ha già un tenant.  In hello [portale Azure](https://portal.azure.com), è necessario trovare un tenant quando si visitano troppo "Più servizi" e "Azure Active Directory".  Si è gratuita toouse che questo tenant, come può vedere adatta.

## <a name="start-from-scratch"></a>Iniziare da zero
Se tutti i precedente hello incomprensibile tooyou, non occorre preoccuparsi.  È sufficiente visitare [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign iscrizione a Azure con una nuova organizzazione.  Dopo aver completato il processo di hello, si avrà un proprio tenant Azure AD con il nome di dominio hello di che scelto durante la registrazione.  In hello [portale Azure](https://portal.azure.com), è possibile trovare il tenant passando troppo "Azure Active Directory" nell'articolo NAV hello a sinistra.

Come parte del processo di hello di iscrizione ad Azure, sarà i dettagli della carta di credito tooprovide obbligatorio.  Non c'è nulla di cui preoccuparsi, la pubblicazione di applicazioni in Azure AD o la creazione di nuovi tenant non vengono addebitate.
