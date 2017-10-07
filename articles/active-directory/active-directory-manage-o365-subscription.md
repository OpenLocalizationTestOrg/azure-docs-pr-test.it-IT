---
title: directory di hello aaaManage per la sottoscrizione di Office 365 in Azure | Documenti Microsoft
description: La gestione di una directory di sottoscrizione di Office 365 in Azure Active Directory e hello portale di Azure classico
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
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Gestire directory hello per la sottoscrizione di Office 365 in Azure
Questo articolo viene descritto come toomanage una directory in cui è stata creata per una sottoscrizione Office 365, utilizzando hello portale di Azure classico. È necessario essere amministratore del servizio hello o un coamministratore di toosign una sottoscrizione di Azure nel portale di Azure classico toohello. Se non si ha ancora una sottoscrizione di Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita di 30 giorni](https://azure.microsoft.com/trial/get-started-active-directory/) e distribuire la prima soluzione cloud in meno di 5 minuti, usando questo collegamento. Lavoro hello che toouse o dell'istituto di istruzione che l'account utilizzato toosign in tooOffice 365.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

Dopo aver completato hello sottoscrizione di Azure, è possibile accedere al portale di Azure classico toohello e accedere ai servizi di Azure. Fare clic su estensione Active Directory hello toomanage hello stessa directory che autentica gli utenti di Office 365.

Se si dispone già di una sottoscrizione di Azure, hello processo toomanage un'ulteriore directory è piuttosto semplice. Ad esempio, è possibile che Michael Smith abbia una sottoscrizione di Office 365 per Contoso.com e anche una sottoscrizione di Azure che ha ottenuto usando l'account Microsoft msmith@hotmail.com. In questo caso Michael gestisce due directory.

| Subscription | Office 365 | Azure |
| --- | --- | --- |
|   Nome visualizzato |Contoso |Directory di Azure Active Directory (Azure AD) predefinita |
|   Nome di dominio |contoso.com |msmithhotmail.onmicrosoft.com |

Desidera che le identità degli utenti di hello toomanage nella directory di Contoso hello mentre è connesso tooAzure utilizzando il suo account Microsoft, in modo da poter abilitare le funzionalità di Azure AD, ad esempio autenticazione a più fattori. il processo di hello tooillustrate può consentire di Hello seguente diagramma.

![Diagramma toomanage due directory indipendente](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

In questo caso, due directory hello sono indipendenti tra loro.

## <a name="toomanage-two-independent-directories"></a>directory indipendenti toomanage due
In ordine di Michael Smith toomanage entrambe le directory mentre è connesso tooAzure come msmith@hotmail.com, è necessario completare hello alla procedura seguente:

> [!NOTE]
> Questa procedura può essere eseguita solo se l'utente ha eseguito l'accesso con un account Microsoft. Se l'utente hello è firmato con un account aziendale o dell'istituto di istruzione, hello opzione troppo**utilizza directory esistente** non è disponibile. Un account aziendale o dell'istituto di istruzione può essere autenticato solo dalla relativa home directory (vale a dire hello directory in cui hello account aziendale o dell'istituto di istruzione è archiviato tale business hello o dell'istituto di istruzione proprietario).
>
>

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come msmith@hotmail.com.
2. Fare clic su **Nuovo** > **Servizi app** > **Active Directory** > **Directory** > **Creazione personalizzata**.
3. Fare clic su Usa esistente hello directory e seleziona **sono pronti toobe uscire ora** casella di controllo.
4. Accedi toohello portale di Azure classico come amministratore globale di Contoso.onmicrosoft.com (ad esempio, msmith@contoso.com).
5. Quando viene richiesto troppo**directory di Contoso hello usare con Azure?**, fare clic su **continua**.
6. Fare clic su **Esci ora**.
7. Accedi toohello portale di Azure classico come msmith@hotmail.com. directory di Contoso hello e directory predefinita hello vengono visualizzati in hello estensione Active Directory.

Dopo aver completato questi passaggi, msmith@hotmail.com è un amministratore globale nella directory di Contoso hello.

## <a name="tooadminister-resources-as-hello-global-admin"></a>risorse tooadminister come hello amministratore globale
Ora si supponga che Valeria Dal Monte deve amministrare i siti Web e le risorse del database associato alla sottoscrizione di Azure per hello msmith@hotmail.com. Prima che a tale scopo, Michael Smith deve toocomplete i passaggi aggiuntivi seguenti:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) utilizzando account di amministratore del servizio hello per hello sottoscrizione di Azure (in questo esempio, msmith@hotmail.com).
2. Trasferimento di directory di Contoso toohello sottoscrizione hello: fare clic su **impostazioni** > **sottoscrizioni** > selezionare la sottoscrizione hello > **modifica Directory** > selezionare **Contoso (Contoso.com)**. Come parte del trasferimento hello, qualsiasi lavoro o dell'istituto di istruzione vengono rimossi gli account che corrispondono a coamministratori della sottoscrizione hello.
3. Aggiungere Valeria Dal Monte come coamministratore della sottoscrizione hello: fare clic su **impostazioni** > **amministratori** > selezionare la sottoscrizione hello > **Aggiungi** > tipo **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla relazione hello tra sottoscrizioni e directory, vedere [come una sottoscrizione è associata a una directory](active-directory-how-subscriptions-associated-directory.md).
