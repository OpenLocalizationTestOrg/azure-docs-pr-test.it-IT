---
title: Gestire la directory per la sottoscrizione di Office 365 in Azure | Microsoft Docs
description: Informazioni su come gestire la directory di una sottoscrizione di Office 365 con Azure Active Directory e il portale di Azure classico
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: b520a5e96417fb766a757fabc384a1fc4eb0f14e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-the-directory-for-your-office-365-subscription-in-azure"></a>Gestire la directory per la sottoscrizione di Office 365 in Azure
Questo articolo descrive come gestire una directory creata per una sottoscrizione di Office 365 con il portale di Azure classico. Per accedere al portale di Azure classico, è necessario essere l'amministratore del servizio o un coamministratore di una sottoscrizione di Azure. Se non si ha ancora una sottoscrizione di Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita di 30 giorni](https://azure.microsoft.com/trial/get-started-active-directory/) e distribuire la prima soluzione cloud in meno di 5 minuti, usando questo collegamento. Usare l'account aziendale o dell'istituto di istruzione usato per accedere a Office 365.

> [!IMPORTANT]
> Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.

Dopo aver completato la sottoscrizione di Azure, è possibile accedere al portale di Azure classico e accedere ai relativi servizi. Fare clic sull'estensione Active Directory per gestire la stessa directory usata per autenticare gli utenti di Office 365.

Se si ha già una sottoscrizione di Azure, il processo per gestire una directory aggiuntiva è piuttosto semplice. Ad esempio, è possibile che Michael Smith abbia una sottoscrizione di Office 365 per Contoso.com e anche una sottoscrizione di Azure che ha ottenuto usando l'account Microsoft msmith@hotmail.com. In questo caso Michael gestisce due directory.

| Subscription | Office 365 | Azure |
| --- | --- | --- |
|   Nome visualizzato |Contoso |Directory di Azure Active Directory (Azure AD) predefinita |
|   Nome di dominio |contoso.com |msmithhotmail.onmicrosoft.com |

Michael vuole gestire le identità utente nella directory Contoso mentre è connesso ad Azure con il suo account Microsoft per poter abilitare le funzionalità di Azure AD, come l'autenticazione a più fattori. Il diagramma seguente illustra meglio il processo.

![Diagramma per gestire due directory indipendenti](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

In questo caso, le due directory sono indipendenti tra loro.

## <a name="to-manage-two-independent-directories"></a>Per gestire due directory indipendenti
Per poter gestire entrambe le directory mentre è connesso ad Azure come msmith@hotmail.com, Michael Smith deve seguire questa procedura:

> [!NOTE]
> Questa procedura può essere eseguita solo se l'utente ha eseguito l'accesso con un account Microsoft. Se l'utente ha eseguito l'accesso con un account aziendale o dell'istituto di istruzione, l'opzione **Utilizza directory esistente** non è disponibile. Un account aziendale o dell'istituto di istruzione può essere autenticato solo dalla relativa home directory, ovvero dalla directory in cui tale account è archiviato, di proprietà dell'azienda o dell'istituto di istruzione.
>
>

1. Accedere al [portale di Azure classico](https://manage.windowsazure.com) come msmith@hotmail.com.
2. Fare clic su **Nuovo** > **Servizi app** > **Active Directory** > **Directory** > **Creazione personalizzata**.
3. Fare clic su Utilizza directory esistente e selezionare la casella di controllo **È possibile uscire ora** .
4. Accedere al portale di Azure classico come amministratore globale di Contoso.onmicrosoft.com (ad esempio, msmith@contoso.com).
5. Quando viene visualizzata la richiesta **Usare la directory Contoso con Azure?**, fare clic su **Continua**.
6. Fare clic su **Esci ora**.
7. Accedere al portale di Azure classico come msmith@hotmail.com. Entrambe le directory, quella Contoso e quella predefinita, verranno visualizzate nell'estensione Active Directory.

Dopo aver completato questa procedura, msmith@hotmail.com è diventato amministratore globale della directory Contoso.

## <a name="to-administer-resources-as-the-global-admin"></a>Per amministrare le risorse come amministratore globale
Si supponga ora che Jane Doe debba amministrare le risorse di database e di siti Web associate alla sottoscrizione di Azure per msmith@hotmail.com. Prima di poterlo fare, Michael Smith deve effettuare questi passaggi aggiuntivi:

1. Accedere al [portale di Azure classico](https://manage.windowsazure.com) con l'account amministratore del servizio per la sottoscrizione di Azure (in questo esempio msmith@hotmail.com).
2. Trasferire la sottoscrizione alla directory Contoso: fare clic su **Impostazioni** > **Sottoscrizioni** > selezionare la sottoscrizione > **Modifica directory** > selezionare **Contoso (Contoso.com)**. Durante il trasferimento, gli eventuali account aziendali o dell'istituto di istruzione di coamministratori della sottoscrizione verranno rimossi.
3. Aggiungere Jane Doe come coamministratore della sottoscrizione: fare clic su **Impostazioni** > **Amministratori** &gt; selezionare la sottoscrizione &gt; **Aggiungi** &gt; digitare **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulla relazione tra sottoscrizioni e directory, vedere [Associare le sottoscrizioni di Azure ad Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).
