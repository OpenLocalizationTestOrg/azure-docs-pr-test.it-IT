---
title: "aaaGet avviato con la protezione dell'identità Azure Active Directory e Microsoft Graph | Documenti Microsoft"
description: Fornisce un tooquery Introduzione Microsoft Graph per un elenco di eventi di rischio e le informazioni associate da Azure Active Directory.
services: active-directory
keywords: "azure active directory identity protection, evento di rischio, vulnerabilità, criteri di sicurezza, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph
Microsoft Graph è hello Microsoft unified endpoint API e hello home di [la protezione di Azure Active Directory identità](active-directory-identityprotection.md) API. prima di Hello API, **identityRiskEvents**, consente tooquery Microsoft Graph per un elenco di [gli eventi di rischio](active-directory-identityprotection-risk-events-types.md) e informazioni associate. Questo articolo fornisce un'introduzione all'esecuzione di query su questa API. Per un'introduzione approfondita, la documentazione completa e accesso toohello Esplora grafico, vedere hello [sito Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

Esistono tre i dati di protezione dell'identità tooaccessing passaggi tramite Microsoft Graph:

1. Aggiungere un'applicazione con un segreto client. 
2. Utilizzare il segreto e alcuni altri blocchi di informazioni tooauthenticate tooMicrosoft grafico, in cui si riceve un token di autenticazione. 
3. Usare questo endpoint toohello API le richieste di token toomake e ottenere dati di protezione dell'identità.

Ecco gli elementi che occorre avere prima di iniziare:

* Applicazione toocreate hello privilegi di amministratore in Azure AD
* nome Hello del dominio del tenant (ad esempio, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Aggiungere un'applicazione con un segreto client
1. [Accedi](https://manage.windowsazure.com) tooyour portale di Azure classico come amministratore. 
2. Nel riquadro di spostamento sinistro hello scegliere **Active Directory**. 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
4. Scegliere dal menu hello in primo piano hello **applicazioni**.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. In hello **informazioni sull'applicazione** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. In hello **nome** casella di testo, digitare un nome per l'applicazione (ad esempio: applicazione dell'API AADIP rischio evento).
   
    b. Come **Tipo** selezionare **Applicazione Web e/o API Web**.
   
    c. Fare clic su **Avanti**.
8. In hello **proprietà App** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. In hello **Sign-On URL** casella tipo `http://localhost`.
   
    b. In hello **URI ID App** casella tipo `http://localhost`.
   
    c. Fare clic su **Completa**.

A questo punto è possibile configurare l'applicazione.

![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Concedere il hello toouse di autorizzazione applicazione API
1. Nella pagina dell'applicazione, nel menu hello nella parte superiore di hello, fare clic su **configura**. 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. In hello **autorizzazioni tooother applicazioni** fare clic su **aggiungere applicazione**.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. In hello **autorizzazioni tooother applicazioni** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Selezionare **Microsoft Graph**.
   
    b. Fare clic su **Complete**.
4. Fare clic su **Autorizzazioni applicazione: 0** e quindi selezionare **Legge tutte le informazioni sugli eventi di rischio dell'identità**.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Ottenere una chiave di accesso
1. Nella pagina dell'applicazione hello **chiavi** , selezionare 1 anno come durata.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. Nella sezione chiavi hello, copiare il valore di hello della chiave appena creato e quindi incollarlo in un luogo sicuro.
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Se si perde la chiave, si hanno tooreturn toothis sezione e creare una nuova chiave. Mantenere la chiave segreta, perché chiunque ne fosse a conoscenza potrà accedere ai dati.
   > 
   > 
4. In hello **proprietà** sezione, hello copia **ID Client**e quindi incollarlo in un luogo sicuro. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Autenticare tooMicrosoft grafico e hello query identità rischio eventi API
A questo punto saranno disponibili:

* ID client hello è stato copiato in precedenza
* chiave di Hello che è stato copiato in precedenza
* nome di Hello del dominio del tenant

tooauthenticate, inviare un post richiesta troppo`https://login.microsoft.com` con i seguenti parametri nel corpo di hello hello:

* grant_type: "**client_credentials**"
* resource: "**https://graph.microsoft.com**"
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> Sono necessari valori di tooprovide per hello **client_id** hello e **client_secret** parametro.
> 
> 

Se la richiesta riesce, verrà restituito un token di autenticazione.  
hello toocall API, creare un'intestazione con hello seguente parametro:

    `Authorization`=”<token_type> <access_token>"


Per l'autenticazione, è possibile trovare il tipo di token hello e token di accesso in hello ha restituito un token.

Inviare questa intestazione come toohello una richiesta API URL seguente:`https://graph.microsoft.com/beta/identityRiskEvents`

risposta Hello, se ha esito positivo, è una raccolta di identità rischi e i dati in formato JSON OData, che può essere analizzato e gestito secondo necessità hello associati.

Di seguito è riportato il codice di esempio per l'autenticazione e la chiamata API hello tramite Powershell.  
Aggiungere semplicemente l'ID client, la chiave e il dominio del tenant.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Passaggi successivi
Complimenti, il primo tooMicrosoft chiamata grafico appena creata.  
Ora è possibile eseguire una query eventi di rischio di identità e utilizzare dati hello desiderato.

toolearn ulteriori informazioni su Microsoft Graph e come applicazioni toobuild utilizzando hello API Graph, estrarre hello [documentazione](https://graph.microsoft.io/docs) e molto altro ancora su hello [sito Microsoft Graph](https://graph.microsoft.io/). Assicurarsi inoltre che hello toobookmark [API di Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) pagina che elenca tutti hello identità API di protezione disponibili nel grafico. Quando si aggiungono nuovi modi toowork con la protezione dell'identità tramite l'API, si verrà visualizzato nella pagina.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Tipi di eventi di rischio rilevati da Azure Active Directory Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Overview of Microsoft Graph (Panoramica di Microsoft Graph)](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection Service Root (Radice del servizio Azure AD Identity Protection)](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

