---
title: Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua nella pagina di accesso in Azure Active Directory | Microsoft Docs
description: Informazioni su come aggiungere testo e immagini di informazioni personalizzate sull'azienda alla pagina di accesso Azure
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua nella pagina di accesso in Azure Active Directory
Per evitare confusione, molte aziende vogliono applicare un aspetto coerente a tutti i siti Web e servizi che gestiscono. Azure Active Directory offre questa funzionalità consentendo di personalizzare l'aspetto delle pagine di accesso, in modo da includere il logo e le combinazioni di colori personalizzate dell'azienda. La pagina di accesso è la pagina visualizzata quando si accede a Office 365 o ad altre applicazioni basate sul Web che usano Azure AD come provider di identità. Interagire con questa pagina per immettere le credenziali.

## <a name="customizing-the-sign-in-page-for-another-language"></a>Personalizzazione della pagina di accesso per un'altra lingua
È possibile aggiungere elementi specifici della lingua alla pagina di accesso personalizzata solo se è già stata creata una pagina di accesso personalizzata come descritto in [Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso](active-directory-branding-custom-signon-azure-portal.md). È possibile configurare una pagina di accesso per ogni directory con un set predefinito di elementi personalizzabili. Dopo avere configurato un set predefinito di elementi di personalizzazione, è possibile configurare altre versioni per impostazioni locali diverse. È anche possibile combinare e abbinare diversi elementi. Ad esempio, è possibile:

* Creare un' **immagine della pagina di accesso** predefinita adatta per tutte le impostazioni cultura, quindi creare versioni specifiche per l'inglese e il francese. Quando si impostano i browser su una di queste due lingue, viene visualizzata l'immagine specifica della lingua, mentre per tutte le altre lingue viene visualizzata l'illustrazione predefinita.
* Configurare loghi diversi per l'organizzazione, ad esempio una versione giapponese o ebraica.

È consigliabile limitare il numero di varianti linguistiche per facilitare la manutenzione e migliorare le prestazioni.

**Per aggiungere informazioni personalizzate distintive dell'azienda alla directory:**

1. Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.
2. Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.

   ![Apertura di Gestione utenti](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Nel pannello **Utenti e gruppi** selezionare **Informazioni personalizzate distintive dell'azienda**.
4. Nel pannello **Utenti e gruppi - Informazioni personalizzate distintive dell'azienda** selezionare il comando **Aggiungi lingua**.

    ![Aggiungere elementi personalizzati distintivi dell'azienda specifiche della lingua](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modificare gli elementi da personalizzare. Tutti gli elementi sono facoltativi.
6. Fare clic su **Save**.

Può trascorrere fino a un'ora prima che qualsiasi modifica apportata per la personalizzazione della pagina di accesso venga visualizzata.

## <a name="next-steps"></a>Passaggi successivi
[Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso](active-directory-branding-custom-signon-azure-portal.md)
