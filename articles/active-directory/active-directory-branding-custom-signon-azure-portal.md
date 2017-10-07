---
title: aaaCustomize accesso pagina hello Azure Active Directory | Documenti Microsoft
description: Informazioni su come tooadd una pagina toohello Accedi Azure branding aziendale
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Aggiungere informazioni personalizzate distintive tooyour nella pagina di accesso in hello Azure Active Directory della società
tooavoid confusione, molte società desidera tooapply un aspetto coerente in tutti i siti Web di hello e i servizi gestiti. Azure Active Directory fornisce questa funzionalità, consentendo l'aspetto di hello toocustomize di hello nella pagina di accesso con il logo della società e combinazioni di colori personalizzati. pagina di accesso Hello è hello pagina viene visualizzata quando si accede tooOffice 365 o altre applicazioni basate su web che usano Azure AD come provider di identità. Si interagiscono con tooenter questa pagina delle credenziali.

Se si desidera tooshow il marchio dell'azienda, colori e altri elementi personalizzabili in questa pagina, vedere hello seguenti immagini toounderstand hello differenza due esperienze hello.

Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **prima** una personalizzazione:

![Pagina di accesso di Office 365 prima della personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **dopo** una personalizzazione:

![Pagina di accesso di Office 365 dopo la personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Personalizzazione pagina di accesso hello
In genere, se è necessario l'accesso basato su browser tooyour cloud App e servizi sottoscritti dall'organizzazione, utilizzare hello nella pagina di accesso.

Se è stato applicato le modifiche tooyour nella pagina di accesso, può richiedere tooan orari per tooappear modifiche hello.

Una pagina di accesso personalizzata viene visualizzata solo quando si visita un servizio con un URL specifico del tenant, ad esempio https://outlook.com/**contoso**.com o https://mail.**contoso**.com.

Quando si visita un servizio con URL non specifici del tenant (ad esempio, https://mail.office365.com), viene visualizzata una pagina di accesso non personalizzata. In questo caso, la personalizzazione viene visualizzata dopo avere immesso il proprio ID utente o avere selezionato un riquadro utente.

> [!NOTE]
> * Il nome di dominio deve risultare "Attivo" nella hello **domini** hello di parte del portale di Azure in cui è stata configurata la personalizzazione. Per altre informazioni, vedere l'argomento relativo all' [aggiunta di nomi di dominio personalizzati](active-directory-domains-add-azure-portal.md).
> * Personalizzazione pagina di accesso non si estende su toohello consumer firmare nella pagina di Microsoft. Se si accede con un account Microsoft, si potrebbe visualizzare un elenco personalizzato di sezioni utente sottoposto a rendering da Azure AD, ma hello personalizzazione dell'organizzazione non è applicabile toohello Microsoft account-pagina di accesso.
>
>

Nella pagina accesso hello **Mantieni l'accesso** casella di controllo permette tooremain un utente connesso quando viene chiuso e riaprire il browser.

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Non influisce sulla durata della sessione. È possibile nascondere una casella di controllo hello hello Azure Active Directory nella pagina di accesso.
Se non viene visualizzata la casella hello dipende dall'impostazione di hello di **Mantieni l'accesso disabilitato**.

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide hello casella di controllo, configurare questa impostazione troppo**Sì**.

> [!NOTE]
> Alcune funzionalità di SharePoint Online e Office 2010 dipendono dagli utenti in grado di toocheck questa casella. Se si configura questa impostazione toohidden, gli utenti potrebbero notare aggiuntive e impreviste prompt toosign-in.
>
>

**directory tooadd aziendale personalizzazione tooyour:**

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **personalizzazione specifica della società**.
4. In hello **utenti e gruppi - personalizzazione specifica della società** blade, seleziona hello **modifica** comando.

    ![Modificare le informazioni personalizzate](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificare gli elementi di hello desiderati toocustomize. Tutti gli elementi sono facoltativi.
6. Fare clic su **Salva**.

Potrebbe essere necessaria fino tooan ora per tutte le modifiche apportate toohello Accedi pagina tooappear personalizzazione.

## <a name="next-steps"></a>Passaggi successivi
[Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua](active-directory-branding-localize-azure-portal.md)
