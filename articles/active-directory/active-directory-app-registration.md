---
title: Registrazione di Active Directory App aaaAzure | Documenti Microsoft
description: In questo articolo viene descritto come toouse hello tooregister portale Azure un'applicazione con Azure Active Directory
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Registrare l'applicazione nel tenant di Azure Active Directory

È possibile utilizzare l'applicazione hello tooregister portale Azure con il tenant di Azure Active Directory (Azure AD). Viene creato un ID dell'applicazione hello e abilita i token tooreceive.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.
4. Seguire le istruzioni di hello e creare una nuova applicazione. Per ottenere esempi specifici per applicazioni Web o per applicazioni native, vedere le [Guide introduttive](active-directory-developers-guide.md).
  * Per le applicazioni Web, fornire hello **Sign-On URL**, ovvero URL di base hello dell'app, in cui gli utenti possono accedere ad esempio `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Per le applicazioni Native, fornire un **URI di reindirizzamento**, quali Azure AD Usa tooreturn token risposte. Immettere un'applicazione, tooyour specifico valore. ad esempio`http://MyFirstAADApp`
5. Dopo aver completato la registrazione, Azure AD le assegna all'applicazione un identificatore client univoci, hello l'ID dell'applicazione.

## <a name="update-application-settings-from-hello-azure-portal"></a>Aggiornare le impostazioni dell'applicazione da hello portale di Azure

È possibile modificare facilmente le impostazioni dell'applicazione esistente usando hello portale di Azure. Ad esempio, è consigliabile tooconfigure un URL di risposta, ovvero in Azure AD rilascia token risposte. È inoltre possibile tooconfigure autorizzazioni tooother applicazioni, per l'istanza tooallow tooaccess l'applicazione hello Microsoft Graph API. È possibile eseguire tutte queste attraverso pagina impostazioni dell'applicazione hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, quindi selezionare l'applicazione dall'elenco di hello.
4. Fare clic su **impostazioni** tooopen pagina Impostazioni hello per un'applicazione hello.
  * Hello **proprietà** pagina consente di modificare le informazioni generali per un'applicazione hello hello. Ciò include nome dell'applicazione hello, hello URL sign-on e URL di disconnessione hello.
  * Hello **gli URL di risposta** pagina permette tooadd un URL di risposta, ovvero in Azure AD invia le risposte di token.
  * Hello **proprietari** pagina permette tooadd i proprietari delle applicazioni.
  * Hello **autorizzazioni** pagina permette tooconfigure le autorizzazioni per l'applicazione hello. Ad esempio, hello tooaccess Microsoft Graph API, fare clic su **Aggiungi** e selezionare **Microsoft Graph** nel selettore hello API, quindi scegliere necessaria, ad esempio l'autorizzazione hello **lettura dati Directory** .
  * Hello **chiavi** pagina permette tooadd i segreti dell'applicazione. Hello segreto verrà visualizzato solo una volta subito dopo la creazione, pertanto è necessario che toocopy per ulteriore utilizzo.

## <a name="use-hello-inline-manifest-editor"></a>Utilizzare l'editor del manifesto hello inline

È possibile utilizzare hello inline editor del manifesto toomodify determinati hello di proprietà dell'applicazione che non sono esposte direttamente nel portale di Azure. Ad esempio, è possibile utilizzare URI di ID App dell'applicazione hello toomodify o tooenable hello OAuth 2.0 flusso implicito invece di autorizzazione predefinito hello concedere flusso del codice.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, quindi selezionare l'applicazione dall'elenco di hello.
4. Fare clic su **manifesto** da hello applicazione pagina tooopen hello inline editor del manifesto.
5. È possibile apportare modifiche toohello direttamente manifesto e salvarlo quando si è pronti. In alternativa, è possibile scaricare tooopen manifesto hello nei Preferiti hello editor e il caricamento manifesto aggiornato.

## <a name="next-steps"></a>Passaggi successivi

1. Estrarre hello [Guide rapide](active-directory-developers-guide.md) per procedure dettagliate di applicazioni esegue l'autenticazione con Azure AD.
2. Per un elenco completo di esempi di codice, vedere [GitHub](https://github.com/azure-samples).
