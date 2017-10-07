---
title: 'Azure Active Directory B2C: introduzione ai criteri personalizzati | Microsoft Docs'
description: "La modalità di avvio tooget con i criteri personalizzati di Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: introduzione ai criteri personalizzati

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dopo aver completato i passaggi di hello in questo articolo, il criterio personalizzato supporterà "LocalAccount" iscrizione o accesso tramite un indirizzo di posta elettronica e una password. Si preparerà anche l'ambiente per l'aggiunta di provider di identità (ad esempio Facebook o Azure Active Directory). Si consiglia di toocomplete questi passaggi prima della lettura su altri utilizzi di hello Azure Active Directory (Azure AD) B2C identità esperienza Framework.

## <a name="prerequisites"></a>Prerequisiti

Prima di procedere, assicurarsi di disporre di un tenant di Azure AD B2C, che è un contenitore per tutti gli utenti, le app, i criteri e altro ancora. Se si non è ancora disponibile, è necessario troppo[creare un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md). È fortemente incoraggiare tutti gli sviluppatori toocomplete hello procedure dettagliate di Azure Active Directory B2C criteri predefiniti e configurare le applicazioni con i criteri predefiniti prima di procedere. Le applicazioni funziona con entrambi i tipi di criteri di una volta apportata un modifica secondaria toohello criteri nome tooinvoke hello criteri personalizzati.

>[!NOTE]
>tooaccess Modifica criterio personalizzato, è necessario un tenant tooyour collegato la sottoscrizione di Azure valida. Se non hai [collegato il tooan tenant di Azure Active Directory B2C sottoscrizione di Azure](active-directory-b2c-how-to-enable-billing.md) o la sottoscrizione di Azure è disabilitata, hello identità esperienza Framework pulsante non sarà disponibile.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Aggiungere la firma e crittografia tenant tooyour B2C chiavi per l'utilizzo mediante criteri personalizzati

1. Aprire hello **identità esperienza Framework** pannello nelle impostazioni del tenant di Azure Active Directory B2C.
2. Selezionare **chiavi dei criteri** chiavi hello tooview disponibili nel tenant.
3. Se non esiste, creare B2C_1A_TokenSigningKeyContainer:<br>
    a. Selezionare **Aggiungi**. <br>
    b. Selezionare **Genera**.<br>
    c. Per **Nome** usare `TokenSigningKeyContainer`. <br> 
    prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.<br>
    d. For **Tipo di chiave** usare **RSA**.<br>
    e. Per **date**, utilizzare quelli predefiniti hello. <br>
    f. Per **Uso chiave** usare **Firma**.<br>
    g. Selezionare **Crea**.<br>
4. Se non esiste, creare B2C_1A_TokenEncryptionKeyContainer:<br>
 a. Selezionare **Aggiungi**.<br>
 b. Selezionare **Genera**.<br>
 c. Per **Nome** usare `TokenEncryptionKeyContainer`. <br>
   prefisso Hello `B2C_1A`_ potrebbero essere aggiunti automaticamente.<br>
 d. For **Tipo di chiave** usare **RSA**.<br>
 e. Per **date**, utilizzare quelli predefiniti hello.<br>
 f. Per **Uso chiave** usare **Crittografia**.<br>
 g. Selezionare **Crea**.<br>
5. Creare B2C_1A_FacebookSecret. <br>
Se si dispone già di un segreto dell'applicazione Facebook, aggiungerlo come tenant tooyour chiave dei criteri. In caso contrario, è necessario creare chiave hello con un valore segnaposto, in modo che i criteri di convalida.<br>
 a. Selezionare **Aggiungi**.<br>
 b. Per **Opzioni** usare **Manuale**.<br>
 c. Per **Nome** usare `FacebookSecret`. <br>
 prefisso Hello `B2C_1A_` potrebbero essere aggiunti automaticamente.<br>
 d. In hello **Secret** , immettere il FacebookSecret da developers.facebook.com o `0` come segnaposto. *Non si tratta dell'ID dell'app Facebook*. <br>
 e. Per **Uso chiave** usare **Firma**. <br>
 f. Selezionare **Crea** e confermare la creazione.

## <a name="register-identity-experience-framework-applications"></a>Registrare le applicazioni del framework dell'esperienza di gestione delle identità

Azure Active Directory B2C richiede tooregister due applicazioni aggiuntive che vengono utilizzate da hello motore toosign backup ed eseguire l'accesso agli utenti.

>[!NOTE]
>È necessario creare due applicazioni che abilita Accedi con account locali: IdentityExperienceFramework (un'app web) e ProxyIdentityExperienceFramework (un'applicazione nativa) con delega autorizzazioni app IdentityExperienceFramework hello. Gli account locali esistono solo nel tenant. Gli utenti iscriversi con un tooaccess combinazione/password dell'indirizzo di posta elettronica univoco applicazioni tenant registrato.

### <a name="create-hello-identityexperienceframework-application"></a>Creare un'applicazione hello IdentityExperienceFramework

1. In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Aprire hello **Azure Active Directory** blade (non hello **Azure Active Directory B2C** pannello). Potrebbe essere necessario tooselect **più servizi** toofind è.
3. Selezionare **Registrazioni per l'app**.
4. Selezionare **Registrazione nuova applicazione**.
   * Per **Nome** usare `IdentityExperienceFramework`.
   * Per **Tipo di applicazione** usare **App Web/API**.
   * Per **URL di accesso** usare `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, dove `yourtenant` è il nome del dominio del tenant di Azure AD B2C.
5. Selezionare **Crea**.
6. Una volta creato, selezionare un'applicazione hello appena creato **IdentityExperienceFramework**.<br>
   * Selezionare **Proprietà**.<br>
   * Copiare l'ID dell'applicazione hello e salvarlo per un momento successivo.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Creare un'applicazione hello ProxyIdentityExperienceFramework

1. Selezionare **Registrazioni per l'app**.
1. Selezionare **Registrazione nuova applicazione**.
   * Per **Nome** usare `ProxyIdentityExperienceFramework`.
   * Per **Tipo di applicazione** usare **Nativo**.
   * Per **URI di reindirizzamento** usare `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, dove `yourtenant` è il tenant di Azure AD B2C.
1. Selezionare **Crea**.
1. Dopo che è stato creato, selezionare un'applicazione hello **ProxyIdentityExperienceFramework**.<br>
   * Selezionare **Proprietà**. <br>
   * Copiare l'ID dell'applicazione hello e salvarlo per un momento successivo.
1. Selezionare **Autorizzazioni necessarie**.
1. Selezionare **Aggiungi**.
1. Fare clic su **Selezionare un'API**.
1. Ricerca per nome hello IdentityExperienceFramework. Selezionare **IdentityExperienceFramework** in hello risultati e quindi fare clic su **selezionare**.
1. Selezionare la casella di controllo hello troppo Avanti**accesso IdentityExperienceFramework**, quindi fare clic su **selezionare**.
1. Selezionare **Operazione completata**.
1. Selezionare **Concedi autorizzazioni** e quindi confermare selezionando **Sì**.

## <a name="download-starter-pack-and-modify-policies"></a>Scaricare lo starter pack e modificare i criteri

Criteri personalizzati sono un set di file XML che è necessario tenant di Azure Active Directory B2C tooyour toobe caricato. Offriamo starter Pack tooget si lavorare rapidamente. Ogni pacchetto nel seguente elenco hello contiene hello più piccolo numero di profili di tecnici e i percorsi utente necessari scenari hello tooachieve descritti:
 * LocalAccounts. Consente l'utilizzo di hello di solo gli account locali.
 * SocialAccounts. Consente l'utilizzo di hello dei conti social (o federazione).
 * **SocialAndLocalAccounts**. Questo file è usato per questa procedura dettagliata hello.
 * SocialAndLocalAccountsWithMFA. Qui sono incluse le opzioni social, locale e Multi-Factor Authentication.

Ogni pacchetto Starter contiene:

* Hello [file base](active-directory-b2c-overview-custom.md#policy-files) dei criteri di hello. Alcune modifiche sono necessari toohello base.
* Hello [file di estensione](active-directory-b2c-overview-custom.md#policy-files) dei criteri di hello.  Questo file è quello in cui viene eseguita la maggior parte delle modifiche di configurazione.
* I [file relying party](active-directory-b2c-overview-custom.md#policy-files) sono file specifici delle attività chiamati dall'applicazione.

>[!NOTE]
>Se l'editor XML supporta la convalida, convalidare file hello rispetto allo schema XML TrustFrameworkPolicy_0.3.0.0.xsd hello che si trova nella directory radice di hello del pacchetto hello. La convalida dello schema XML identifica gli errori prima del caricamento.

 Di seguito sono riportati i requisiti iniziali:

1. Scaricare active-directory-b2c-custom-policy-starterpack da GitHub. [Scaricare i file con estensione zip hello](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) o eseguire

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Apri cartella SocialAndLocalAccounts hello.  file base Hello (TrustFrameworkBase.xml) in questa cartella contiene contenuto necessario per gli account locali e sociale/aziendale. contenuto social Hello non interferisce con i passaggi di hello per gli account locali di installare e in esecuzione.
3. Aprire TrustFrameworkBase.xml. Se occorre un editor XML, provare [Visual Studio Code](https://code.visualstudio.com/download), un editor multipiattaforma leggero.
4. Nella radice di hello `TrustFrameworkPolicy` elemento, hello aggiornamento `TenantId` e `PublicPolicyUri` gli attributi, sostituendo `yourtenant.onmicrosoft.com` con il nome di dominio hello del tenant di Azure Active Directory B2C:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`è nome criterio hello che viene visualizzato nel portale di hello e nome hello mediante il quale il file di criteri viene fatto riferimento da altri file di criteri.

5. Salvare il file hello.
6. Aprire TrustFrameworkExtensions.xml. Modificare hello stesso due sostituendo `yourtenant.onmicrosoft.com` con il tenant di Azure Active Directory B2C. Rendere hello stesso sostituzione in hello `<TenantId>` elemento per un totale di tre modifiche. Salvare il file hello.
7. Aprire SignUpOrSignIn.xml. Modificare hello stesso sostituendo `yourtenant.onmicrosoft.com` con il tenant di Azure Active Directory B2C in tre posizioni. Salvare il file hello.
8. La reimpostazione della password hello aprire e modificare i file di profilo. Modificare hello stesso sostituendo `yourtenant.onmicrosoft.com` con il tenant di Azure Active Directory B2C nei tre punti in ogni file. Salvare i file hello.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Aggiungere criteri personalizzati tooyour ID applicazione hello
Aggiungere file estensioni toohello ID dell'applicazione hello (`TrustFrameworkExtensions.xml`):

1. Nel file estensioni hello (TrustFrameworkExtensions.xml), trovare l'elemento hello `<TechnicalProfile Id="login-NonInteractive">`.
2. Sostituire le istanze di `IdentityExperienceFrameworkAppId` con ID applicazione hello hello applicazione identità esperienza Framework creato in precedenza. Di seguito è fornito un esempio:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Sostituire le istanze di `ProxyIdentityExperienceFrameworkAppId` con ID applicazione hello hello applicazione Proxy identità esperienza Framework creato in precedenza.
4. Salvare il file delle estensioni.

## <a name="upload-hello-policies-tooyour-tenant"></a>Caricare tenant tooyour di hello criteri

1. In hello [portale di Azure](https://portal.azure.com), passare in hello [contesto del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md), aprire hello e **Azure Active Directory B2C** blade.
2. Fare clic su **Framework dell'esperienza di gestione delle identità**.
3. Selezionare **Carica criteri**.

    >[!WARNING]
    >file di criteri personalizzati Hello devono essere caricati in hello seguente ordine:

1. Caricare TrustFrameworkBase.xml.
2. Caricare TrustFrameworkExtensions.xml.
3. Caricare SignUpOrSignin.xml.
4. Caricare gli altri file dei criteri.

Quando viene caricato un file, il nome di hello del file di criteri hello è preceduto da `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test dei criteri personalizzati di hello tramite Esegui

1. Aprire **le impostazioni di Azure Active Directory B2C** e andare troppo**identità esperienza Framework**.

   >[!NOTE]
   >**Esegui ora** richiede almeno un'applicazione toobe preregistrate tenant hello. Le applicazioni devono essere registrate nel tenant di hello B2C utilizzando hello **applicazioni** selezione dei menu in Azure Active Directory B2C o mediante hello identità esperienza Framework tooinvoke criteri incorporati e personalizzati. È necessaria una sola registrazione per applicazione.<br><br>
   toolearn tooregister applicazioni, vedere hello Azure Active Directory B2C [iniziare](active-directory-b2c-get-started.md) articolo o hello [registrazione dell'applicazione](active-directory-b2c-app-registration.md) articolo.  

2. Aprire B2C_1A_signup_signin, hello criteri personalizzati di relying party (RP) che è stata caricata. Selezionare **Esegui adesso**.

3. È necessario essere in grado di toosign utilizzando un indirizzo di posta elettronica.

4. Accedere con hello stesso account tooconfirm che è necessario hello configurazione corretta.

>[!NOTE]
>Una causa comune degli errori di accesso è la configurazione non corretta dell'app IdentityExperienceFramework.


## <a name="next-steps"></a>Passaggi successivi

### <a name="add-facebook-as-an-identity-provider"></a>Aggiungere Facebook come provider di identità
tooset di Facebook:
1. [Configurare un'applicazione Facebook in developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Aggiunta di un tenant di tooyour secret Azure Active Directory B2C applicazione Facebook hello](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. Nel file di criteri TrustFrameworkExtensions hello, sostituire il valore di hello di `client_id` con l'ID dell'applicazione Facebook hello:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Caricare tenant tooyour di hello TrustFrameworkExtensions.xml criteri file.
5. Test utilizzando **Esegui ora** oppure richiamando criteri hello direttamente dall'applicazione registrata.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Aggiungere Azure Active Directory come provider di identità
file di base Hello già utilizzato in questa Guida introduttiva contiene alcuni dei contenuti di hello che è necessario per l'aggiunta di altri provider di identità. Per informazioni sull'impostazione di accessi, vedere hello [Azure Active Directory B2C: l'accesso con account di Azure AD](active-directory-b2c-setup-aad-custom.md) articolo.

Per una panoramica di criteri personalizzati di Azure Active Directory B2C che utilizzano hello identità esperienza Framework, vedere hello [Azure Active Directory B2C: i criteri personalizzati](active-directory-b2c-overview-custom.md) articolo. 
