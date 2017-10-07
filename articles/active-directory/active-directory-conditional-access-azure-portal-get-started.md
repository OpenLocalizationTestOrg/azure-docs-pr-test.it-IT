---
title: aaaGet avviato con l'accesso condizionale in Azure Active Directory | Documenti Microsoft
description: "Verificare l'accesso condizionale usando una condizione della località."
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Introduzione all'accesso condizionale in Azure Active Directory

Accesso condizionale è una funzionalità di Azure Active Directory che consente di toodefine condizioni in cui gli utenti autorizzati possono accedere le applicazioni. 

Questo argomento fornisce istruzioni per testare un accesso condizionale in base a una condizione della località nell'ambiente usato.  


## <a name="scenario-description"></a>Descrizione dello scenario

Un requisito comune in molte organizzazioni è tooonly richiedono l'autenticazione a più fattori per tooapps di accesso che non viene eseguita dalla rete intranet aziendale hello. Azure Active Directory permette di ottenere facilmente questo risultato mediante la configurazione di criteri di accesso condizionale basati sulla località. Questo argomento fornisce istruzioni dettagliate per la configurazione di criteri correlati, si basa su criteri Hello [gli indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish tra i tentativi di accesso da hello aziendale della rete intranet e tutti gli altri percorsi.


## <a name="prerequisites"></a>Prerequisiti

Hello scenario descritto in questo argomento si presuppone che si ha familiarità con concetti hello descritti nella [accesso condizionale di Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest questo scenario, è necessario:

- Creare un utente test. 

- Assegnare un utente di test toohello licenza Azure AD Premium

- Configurare un'app gestita e assegnare il tooit utente test

- Configurare indirizzi IP attendibili.

Per altre informazioni sull'argomento, vedere [Indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Procedura di configurazione dei criteri

**tooconfigure i criteri di accesso condizionale, eseguire:**

1. Nel portale di Azure nella barra di spostamento sinistro hello, hello fare clic su **Azure Active Directory**. 

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. In hello **Azure Active Directory** pannello in hello **Gestisci** fare clic su **accesso condizionale**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. In hello **accesso condizionale** blade, hello tooopen **New** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **Aggiungi**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. In hello **New** pannello in hello **nome** casella di testo, digitare un nome per il criterio.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. In hello **assegnazione** fare clic su **utenti e gruppi**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. In hello **utenti e gruppi** pannello eseguire hello alla procedura seguente:

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Fare clic su **Seleziona utenti e gruppi**.

    b. Fare clic su **Seleziona**.

    c. In hello **selezionare** pannello, selezionare l'utente test e quindi fare clic su **selezionare**.

    d. In hello **utenti e gruppi** pannello, fare clic su **eseguita**.

7. In hello **New** blade, hello tooopen **App Cloud** pannello in hello **assegnazione** fare clic su **App Cloud**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. In hello **App Cloud** pannello eseguire hello alla procedura seguente:

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Fare clic su **Selezionare le app**.

    b. Fare clic su **Seleziona**.

    c. In hello **selezionare** pannello, selezionare l'applicazione cloud e quindi fare clic su **selezionare**.

    d. In hello **App Cloud** pannello, fare clic su **eseguita**.

9. In hello **New** blade, hello tooopen **condizioni** pannello in hello **assegnazione** fare clic su **condizioni**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. In hello **condizioni** blade, hello tooopen **percorsi** pannello, fare clic su **percorsi**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. In hello **percorsi** pannello eseguire hello alla procedura seguente:

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. In **Configura** fare clic su **Sì**.

    b. In **Includi** fare clic su **Tutte le località**.

    c. Fare clic su **Escludi** e quindi su **Tutti gli indirizzi IP attendibili**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Fare clic su **Done**.

12. In hello **condizioni** pannello, fare clic su **eseguita**.

13. In hello **New** blade, hello tooopen **Grant** pannello in hello **controlli** fare clic su **Grant**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. In hello **Grant** pannello eseguire hello alla procedura seguente:

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Selezionare **Richiedi autenticazione a più fattori**.

    b. Fare clic su **Seleziona**.

15. In hello **New** pannello, in **abilitare i criteri di**, fare clic su **su**.

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. In hello **New** pannello, fare clic su **crea**.


## <a name="testing-hello-policy"></a>Criteri di test hello

tootest dei criteri, è necessario accedere all'app da un dispositivo che: 

1. Accedere all'app da un dispositivo con un indirizzo IP compreso nell'intervallo di indirizzi IP attendibili configurato. 

1. Accedere all'app da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi IP attendibili configurato.

L'autenticazione a più fattori deve essere necessaria solo durante il tentativo di connessione da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi attendibili. 


## <a name="next-steps"></a>Passaggi successivi

Se si desidera toolearn ulteriori informazioni sull'accesso condizionale, vedere [accesso condizionale di Azure Active Directory](active-directory-conditional-access-azure-portal.md).

