---
title: aaaHow tooLink un tooAzure di sottoscrizione di Azure Active Directory B2C | Documenti Microsoft
description: Fatturazione tooenable Guida dettagliata per il tenant di Azure Active Directory B2C in una sottoscrizione di Azure.
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Collegamento toopay di tenant Azure B2C tooan una sottoscrizione di Azure per addebiti di utilizzo

Gli addebiti di utilizzo correnti per Azure Active Directory B2C (o Azure Active Directory B2C) vengono fatturati tooan sottoscrizione Azure. È necessario per hello tenant amministratore tooexplicitly collegamento hello Azure Active Directory B2C tenant tooan dopo la creazione di tenant hello B2C stessa sottoscrizione di Azure.  Questo collegamento viene ottenuto tramite la creazione di un annuncio di Azure "B2C Tenant" risorsa di destinazione hello sottoscrizione di Azure. Molti tenant B2C può essere collegato tooa unica sottoscrizione di Azure e altre risorse di Azure (ad esempio, le macchine virtuali, archiviazione dei dati, LogicApps)


> [!IMPORTANT]
> informazioni più recenti sull'utilizzo di fatturazione e i prezzi di B2C è hello dopo Hello: [dei prezzi di Azure Active Directory B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Passaggio 1: Creare un tenant Azure AD B2C
La prima operazione da eseguire è la creazione del tenant B2C. Se il tenant B2C di destinazione è già stato creato, è possibile ignorare questo passaggio. [Introduzione ad Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Passaggio 2: Apri portale di Azure in hello Tenant di Azure AD che mostra la sottoscrizione di Azure
Passare toohello [portale di Azure](https://portal.azure.com). Passare toohello Tenant di Azure AD che mostra hello desideri toouse sottoscrizione di Azure. In questo tenant di Azure AD è diverso dal tenant B2C hello. All'interno di hello portale di Azure, fare clic sul nome dell'account hello in alto a destra hello di hello tooselect tramite dashboard hello Tenant di Azure AD. Una sottoscrizione di Azure è tooproceed necessari. [Ottenere una sottoscrizione di Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Cambio tooyour Tenant di Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Passaggio 3: Creare una risorsa Tenant B2C in Azure Marketplace
Aprire Marketplace facendo clic sull'icona di hello Marketplace, oppure selezionando hello verde "+" in hello nell'angolo superiore sinistro del dashboard hello.  Cercare e selezionare Azure Active Directory B2C. Selezionare Crea.

![Selezionare Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Cercare AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Risorse di Azure Active Directory B2C Hello creare hello include finestra di dialogo seguenti parametri:

1. Tenant di Azure Active Directory B2C: selezionare un Tenant di Azure Active Directory B2C dall'elenco a discesa hello.  che mostra solo i tenant Azure AD B2C idonei.  Tenant B2C idonei soddisfano queste condizioni: hello amministratore globale del tenant hello B2C e tenant hello B2C non è attualmente associato tooan sottoscrizione di Azure

2. Azure Active Directory B2C risorsa nome - è preselezionato toomatch hello di hello B2C Tenant

3. Sottoscrizione: sottoscrizione di Azure attiva di cui l'utente è amministratore o coamministratore.  È possibile aggiungere più tenant di Azure Active Directory B2C tooone sottoscrizione di Azure

4. Gruppo di risorse e Località del gruppo di risorse: questo elemento consente di organizzare più risorse di Azure.  La scelta non influisce in alcun modo sulla località, sulle prestazioni o sullo stato di fatturazione del tenant B2C.

5. Aggiungere toodashboard per tenant di tooyour B2C accesso più semplice e le impostazioni del tenant B2C hello e di informazioni di fatturazione ![Crea risorsa B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Passaggio 4: Gestire le risorse del tenant B2C (facoltativo)
Una volta completata la distribuzione, una nuova risorsa "B2C Tenant" viene creata nel gruppo di risorse di destinazione hello e sottoscrizione di Azure correlate.  Insieme alle altre risorse di Azure viene visualizzata una nuova risorsa di tipo "Tenant B2C".

![Creare una risorsa B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Fare clic su risorse tenant hello B2C, si è in grado di
- Fare clic su informazioni di fatturazione tooreview nome sottoscrizione. Visualizzare Fatturazione e utilizzo.
- Fare clic su impostazioni di Azure Active Directory B2C tooopen una nuova scheda del browser direttamente nel tenant di tooyour B2C pannello impostazioni
- Inviare una richiesta di supporto.
- Spostare il tooanother di risorse tenant B2C tooanother gruppo di risorse, o sottoscrizione Azure.  Questa opzione permette di cambiare la sottoscrizione di Azure a cui vengono addebitati i costi per l'utilizzo.

![Impostazioni della risorsa B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Problemi noti
- Eliminazione del tenant B2C. Se viene creato un Tenant B2C, eliminato e ricreato con hello stesso nome di dominio, anche eliminare e ricreare la risorsa di "Collegamento" hello con hello stesso nome di dominio.  Noterai "Collegamento" risorsa in "Tutte le risorse" nel tenant di sottoscrizione hello tramite hello portale di Azure.
- Restrizione autoimposta nel percorso di risorse regionali.  In rari casi, un utente potrebbe aver stabilito una restrizione regionale per la creazione di risorse di Azure.  Questa restrizione può impedire la creazione di hello di hello collegamento tra una sottoscrizione di Azure e un Tenant B2C. toomitigate, per ridurre questa restrizione.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver completato questa procedura per ogni tenant B2C, i costi vengono addebitati alla sottoscrizione di Azure in base al Contratto Enterprise o Azure Direct.
- Esaminare l'utilizzo e la fatturazione all'interno della sottoscrizione di Azure selezionata
- Esaminare i report dettagliati sull'utilizzo di giorno per giorno utilizzando hello [API di creazione di report di utilizzo](active-directory-b2c-reference-usage-reporting-api.md)
