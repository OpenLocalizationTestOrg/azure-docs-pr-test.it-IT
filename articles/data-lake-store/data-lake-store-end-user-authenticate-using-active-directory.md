---
title: 'Autenticazione dell''utente finale: Data Lake Store con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come l'autenticazione degli utenti finali tooachieve con archivio Data Lake tramite Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store usa Azure Active Directory per l'autenticazione. Prima di creazione di un'applicazione che funziona con archivio Azure Data Lake o Azure Data Lake Analitica, è necessario innanzitutto decidere come tooauthenticate l'applicazione con Azure Active Directory (Azure AD). Hello due opzioni disponibili sono:

* Autenticazione dell'utente finale (questo articolo)
* Autenticazione da servizio a servizio

Entrambe queste opzioni comportare l'applicazione viene fornita con un token OAuth 2.0, che ottiene tooeach collegato richiesta effettuata tooAzure archivio Data Lake o Azure Data Lake Analitica.

Questo articolo illustra come creare un'**applicazione nativa di Azure AD per l'autenticazione dell'utente finale**. Per istruzioni sulla configurazione dell'applicazione Azure AD per l'autenticazione da servizio a servizio, vedere [Autenticazione da servizio a servizio con Data Lake Store tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* ID sottoscrizione personale. È possibile recuperarlo dal portale di Azure hello. Ad esempio, è disponibile dal Pannello di account archivio Data Lake hello.
  
    ![Ottenere l'ID sottoscrizione](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Il nome di dominio di Azure AD. È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure. Dalla schermata hello riportata di seguito, il nome di dominio hello è **contoso.onmicrosoft.com**, e hello GUID racchiuso tra parentesi quadre è hello ID del tenant. 
  
    ![Ottenere il dominio AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Autenticazione dell'utente finale
Si tratta di hello approccio consigliato se si desidera un toolog gestito dall'utente nell'applicazione tooyour tramite Azure AD. L'applicazione sarà in grado di tooaccess risorse di Azure con hello stesso livello di accesso dell'utente finale di hello connesso. L'utente finale sarà necessario tooprovide le proprie credenziali periodicamente in modo che l'accesso toomaintain dell'applicazione.

il risultato di Hello dell'utente finale di hello Accedi è che l'applicazione viene fornito un token di accesso e un token di aggiornamento. token di accesso Hello Ottiene richiesta tooeach collegato archivio Lake tooData o Data Lake Analitica, e è valido per un'ora per impostazione predefinita. token di aggiornamento Hello può essere utilizzato tooobtain un nuovo token di accesso e è valido per le settimane tootwo per impostazione predefinita, se utilizzate regolarmente. È possibile usare due diversi approcci per l'accesso degli utenti finali.

### <a name="using-hello-oauth-20-pop-up"></a>Utilizzando i menu a comparsa hello OAuth 2.0
L'applicazione può attivare un popup di autorizzazione OAuth 2.0, in cui hello degli utenti finali possono immettere le credenziali. Questa opzione funziona anche con il processo di autenticazione di Azure AD a due fattori (2FA) hello, se necessario. 

> [!NOTE]
> Questo metodo non ancora supportato in hello Azure AD Authentication Library (ADAL) per Python o Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Accesso diretto tramite le credenziali dell'utente
L'applicazione può fornire direttamente tooAzure le credenziali utente Active Directory. Questo metodo funziona solo con gli account utente con ID organizzazione. Non è compatibile con gli account utente personali/con "ID dinamico", inclusi quelli che terminano con @outlook.com o @live.com. Inoltre, questo metodo non è compatibile con gli account utente che richiedono l'autenticazione a due fattori (2FA) di Azure AD.

### <a name="what-do-i-need-toouse-this-approach"></a>Che cosa è necessario toouse questo approccio?
* Il nome di dominio di Azure AD. È già elencata nel prerequisito hello di questo articolo.
* **L'applicazione nativa** di Azure AD
* ID dell'applicazione nativa hello Azure AD
* URI di reindirizzamento per hello applicazione nativa AD Azure
* Impostare autorizzazioni delegate


## <a name="step-1-create-an-active-directory-native-application"></a>Passaggio 1: creare un'applicazione nativa di Active Directory

Creare e configurare un'applicazione nativa di Azure AD per l'autenticazione dell'utente finale con Azure Data Lake Store tramite Azure Active Directory. Per istruzioni, vedere [Creare un'applicazione Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Seguendo le istruzioni di hello in hello di sopra di collegamento, assicurarsi di selezionare **nativo** per il tipo di applicazione, come illustrato nella schermata di hello riportata di seguito.

![Creare un'app Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Creare un'app nativa")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Passaggio 2: ottenere l'ID dell'applicazione e l'URI di reindirizzamento

Vedere [Ottieni ID applicazione hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello id applicazione (detto anche l'ID client hello nel portale di Azure classico hello) di un'applicazione nativa hello Azure AD.

hello tooretrieve URI di reindirizzamento, attenersi alla procedura hello riportata di seguito.

1. Hello portale di Azure, selezionare **Azure Active Directory**, fare clic su **registrazioni di App**, quindi individuare e fare clic su un'applicazione nativa hello Azure AD appena creato.

2. Da hello **impostazioni** pannello per un'applicazione hello, fare clic su **Redirect URIs**.

    ![Ottenere l'URI di reindirizzamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Copiare il valore di hello visualizzato.


## <a name="step-3-set-permissions"></a>Passaggio 3: Impostare le autorizzazioni

1. Hello portale di Azure, selezionare **Azure Active Directory**, fare clic su **registrazioni di App**, quindi individuare e fare clic su un'applicazione nativa hello Azure AD appena creato.

2. Da hello **impostazioni** pannello per un'applicazione hello, fare clic su **delle autorizzazioni necessarie**, quindi fare clic su **Aggiungi**.

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. In hello **aggiungere l'accesso all'API** pannello, fare clic su **selezionare un'API**, fare clic su **Azure Data Lake**, quindi fare clic su **selezionare**.

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  In hello **aggiungere l'accesso all'API** pannello, fare clic su **selezionare le autorizzazioni**, selezionare hello toogive casella di controllo **accesso completo archivio Lake tooData**, quindi fare clic su **selezionare** .

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Fare clic su **Done**.

5. Ripetizione hello ultimi due passaggi toogrant le autorizzazioni per **API di gestione del servizio di Windows Azure** anche.
   
## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stata creata un'applicazione nativa AD Azure e raccolte informazioni hello che è necessario nelle applicazioni client che si creano utilizzando il SDK di .NET SDK per Java, API REST, e così via. È ora possibile procedere toohello seguenti articoli in cui descrivere come toofirst di applicazione web di toouse hello Azure AD eseguire l'autenticazione con l'archivio Data Lake ed eseguono altre operazioni sull'archivio hello.

* [Introduzione a Azure Data Lake Store utilizzando .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Introduzione ad Azure Data Lake Store con Java SDK](data-lake-store-get-started-java-sdk.md)
* [Introduzione ad Azure Data Lake Store con API REST](data-lake-store-get-started-rest-api.md)

