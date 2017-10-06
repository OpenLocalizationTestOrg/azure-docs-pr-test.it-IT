---
title: aaaSet un nuovo dispositivo con Azure AD durante l'installazione | Documenti Microsoft
description: Argomento che spiega come configurare l'aggiunta di Azure AD durante la procedura di configurazione guidata iniziale.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Configurazione di un nuovo dispositivo con Azure AD durante l'installazione
In Windows 10, gli utenti possono partecipare a loro tooAzure dispositivi Active Directory (Azure AD) in hello prima esecuzione (FRX). Questo consente alle organizzazioni toodistribute dispositivi preallocano tootheir dipendenti o studenti o consentire di scegliere i propri dispositivi (CYOD).
Se Windows 10 Professional o Windows 10 Enterprise Edition è installato in un dispositivo, hello che il processo di installazione toohello di valori predefiniti per i dispositivi di proprietà dell'azienda.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin tooAzure un dispositivo Active Directory
1. Quando si attiva il nuovo dispositivo e avviare il processo di installazione di hello, si dovrebbe vedere hello **preparazione** messaggio. Seguire tooset prompt hello del dispositivo.
2. Iniziare personalizzando il paese e la lingua. Quindi accettare condizioni di licenza Software Microsoft hello.
   ![Personalizzare il paese](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Selezionare hello rete toouse per la connessione Internet toohello.
4. Selezionare se si usa un dispositivo personale o di proprietà dell'azienda. Se si tratta di proprietà dell'azienda, fare clic su **questo dispositivo appartiene organizzazione toomy**. Verrà avviata l'esperienza di aggiunta ad Azure AD hello. Di seguito è riportata la schermata che viene visualizzata se si usa Windows 10 Professional.
   <center>
   ![Schermata A chi appartiene questo PC?](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Immettere le credenziali di hello che sono state fornite tooyou dall'organizzazione.
   <center>
   ![Schermata di accesso](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Dopo aver immesso il nome utente, viene trovato il tenant corrispondente in Azure AD. Se trovano in un dominio federato, sarà server reindirizzato tooyour locale Secure Token Service (STS), ad esempio, Active Directory Federation Services (ADFS).
7. Nel caso di un utente in un dominio con federazione, immettere le credenziali direttamente su hello pagina ospitato AD Azure. Se sono state configurate le informazioni personalizzate distintive dell'azienda, vengono visualizzati anche il logo dell'organizzazione e la documentazione di supporto.
8. Viene richiesto di effettuare un'autenticazione a più fattori. La verifica può essere configurata da un amministratore IT.
9. Azure AD verifica se l'utente o il dispositivo richiede la registrazione nella gestione dei dispositivi mobili.
10. Windows registra il dispositivo hello nella directory dell'organizzazione hello in Azure AD e registra nella gestione dei dispositivi mobili, se appropriato.
11. Nel caso di un utente gestito, Windows esegue toohello desktop tramite hello automatico processo di accesso.
12. Se si è un utente federato, si verrà reindirizzati toohello Accedi Windows schermata tooenter le credenziali.

> [!NOTE]
> Aggiunta a un dominio di Windows Server Active Directory locale in Windows hello esperienza out-of-box non è supportata. Pertanto, se si prevede un dominio di computer tooa toojoin, selezionare il collegamento hello **configurare Windows con un account locale** invece. Per partecipare dominio hello dalle impostazioni hello nel computer in uso come effettuata precedentemente.
> 
> 

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

