---
title: Personalizzare un'interfaccia utente tramite criteri personalizzati - Azure AD B2C | Microsoft Docs
description: Informazioni sulla personalizzazione di un'interfaccia utente con l'uso di criteri personalizzati in Azure AD B2C.
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: configurare la personalizzazione dell'interfaccia utente in un criterio personalizzato

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dopo aver completato questo articolo si avrà un criterio personalizzato per l'iscrizione e l'accesso con il proprio marchio e aspetto. Con Azure Active Directory B2C (Azure AD B2C), è possibile utilizzare quasi pieno controllo del contenuto HTML e CSS di hello che ha presentato toousers. Quando si utilizza un criterio personalizzato, configurare personalizzazione dell'interfaccia utente in XML invece di usare i controlli in hello portale di Azure. 

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, completare [Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md). È necessario disporre di un criterio personalizzato di lavoro per l'iscrizione e l'accesso con account locali.

## <a name="page-ui-customization"></a>Personalizzazione dell'interfaccia utente della pagina

Con funzionalità di personalizzazione dell'interfaccia utente di hello pagina, è possibile personalizzare hello aspetto di tutti i criteri personalizzati. È anche possibile mantenere la coerenza visiva e del marchio tra l'applicazione e Azure AD B2C.

Ecco come funziona: Azure AD B2C esegue il codice nel browser del cliente e usa un approccio moderno denominato [Condivisione di risorse tra le origini (CORS)](http://www.w3.org/TR/cors/). Innanzitutto, specificare un URL nei criteri personalizzati di hello con contenuto HTML personalizzato. Azure Active Directory B2C unisce gli elementi dell'interfaccia utente con contenuto HTML che viene caricato dall'URL e quindi Visualizza cliente di hello pagina toohello hello.

## <a name="create-your-html5-content"></a>Creare il contenuto HTML5

Creare contenuto con il nome del marchio del prodotto nel titolo hello HTML.

1. Copiare hello seguente frammento di codice HTML. È ben formato HTML5 con un elemento vuoto denominato  *\<div id = "api"\>\</div\>*  si trova all'interno di hello  *\<corpo\>*  tag. Questo elemento indica il contenuto di Azure Active Directory B2C toobe inserito.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Per motivi di sicurezza, utilizzare hello di JavaScript è attualmente bloccato per la personalizzazione.

2. Incollare frammento hello copiato in un editor di testo e quindi salvare il file hello come *ui.html personalizzare*.

## <a name="create-an-azure-blob-storage-account"></a>Creare un account di archiviazione BLOB di Azure

>[!NOTE]
> In questo articolo, utilizziamo toohost di archiviazione Blob di Azure il contenuto. È possibile scegliere toohost il contenuto in un server web, ma è necessario [abilitare CORS nel server web](https://enable-cors.org/server.html).

toohost questo contenuto HTML nel servizio di archiviazione Blob, hello seguenti:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **Hub** dal menu **New** > **archiviazione** > **account di archiviazione**.
3. Immettere un **nome** unico per l'account di archiviazione.
4. Per **Modello di distribuzione** è possibile lasciare **Resource Manager**.
5. Modifica **tipo Account** troppo**nell'archiviazione Blob**.
6. Per **Prestazioni** è possibile lasciare **Standard**.
7. Per **Replica** è possibile lasciare **RA-GRS**.
8. Per **Livello di accesso** è possibile lasciare **Frequente**.
9. Per **Crittografia del servizio di archiviazione** è possibile lasciare **Disabilitata**.
10. Selezionare una **sottoscrizione** per l'account di archiviazione.
11. Creare un **gruppo di risorse** o selezionarne uno esistente.
12. Seleziona hello **posizione geografica** dell'account di archiviazione.
13. Fare clic su **crea** account di archiviazione toocreate hello.  
    Una volta completata la distribuzione di hello, hello **account di archiviazione** pannello viene aperto automaticamente.

## <a name="create-a-container"></a>Creare un contenitore

un contenitore pubblico nell'archiviazione Blob, toocreate hello seguenti:

1. Fare clic su hello **Panoramica** scheda.
2. Fare clic su **Contenitore**.
3. Per **Nome** digitare **$root**.
4. Impostare **tipo di accesso** troppo**Blob**.
5. Fare clic su **$root** nuovo contenitore di tooopen hello.
6. Fare clic su **Carica**.
7. Fare clic sull'icona di cartella hello Avanti troppo**selezionare un file**.
8. Andare troppo**ui.html personalizzare**, che è stato creato in precedenza in hello [personalizzazione Page UI](#the-page-ui-customization-feature) sezione.
9. Fare clic su **Carica**.
10. Selezionare i blob ui.html personalizzare hello caricato.
11. Avanti troppo**URL**, fare clic su **copia**.
12. In un browser, incollare l'URL copiato hello e visitare il sito toohello. Se hello sito non è accessibile, verificare che il tipo di accesso di hello contenitore è stato impostato troppo**blob**.

## <a name="configure-cors"></a>Configurare CORS

Configurare archiviazione Blob per Cross-Origin Resource Sharing, condivisione eseguendo hello seguenti:

>[!NOTE]
>Desidera tootry le funzionalità di personalizzazione dell'interfaccia utente di hello utilizzando il contenuto HTML e CSS di esempio? È stato fornito uno [strumento di supporto semplice](active-directory-b2c-reference-ui-customization-helper-tool.md) che carica e configura il contenuto di esempio nell'account di archiviazione BLOB. Se si utilizza lo strumento di hello, andare troppo[modificare il criterio personalizzato di iscrizione o accesso](#modify-your-sign-up-or-sign-in-custom-policy).

1. In hello **archiviazione** pannello, in **impostazioni**aprire **CORS**.
2. Fare clic su **Aggiungi**.
3. Per **Origini consentite** digitare un asterisco (\*).
4. In hello **verbi consentiti** elenco a discesa, selezionare **ottenere** e **opzioni**.
5. Per **Intestazioni consentite** digitare un asterisco (\*).
6. Per **Intestazioni esposte** digitare un asterisco (\*).
7. Per **Tempo trascorso massimo (secondi)**, digitare **200**.
8. Fare clic su **Aggiungi**.

## <a name="test-cors"></a>Testare CORS

Convalida che si è pronti eseguendo hello seguenti:

1. Passare toohello [test cors.org](http://test-cors.org/) sito Web, quindi incollare hello URL hello **URL remoto** casella.
2. Fare clic su **Send Request** (Invia richiesta).  
    Se si riceve un messaggio d'errore, verificare che le [impostazioni CORS](#configure-cors) siano corrette. È anche possibile necessario tooclear cache del browser o aprire una sessione di esplorazione in privato premendo Ctrl + MAIUSC + P.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Modificare i criteri personalizzati di iscrizione o di accesso

Nel primo livello hello  *\<TrustFrameworkPolicy\>*  tag, è necessario trovare  *\<BuildingBlocks\>*  tag. All'interno di hello  *\<BuildingBlocks\>*  tag, aggiungere un  *\<ContentDefinitions\>*  tag copiando hello di esempio seguente. Sostituire *your_storage_account* con nome hello dell'account di archiviazione.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Caricare il criterio personalizzato aggiornato

1. In hello [portale di Azure](https://portal.azure.com), [passare nel contesto di hello del tenant di Azure Active Directory B2C](active-directory-b2c-navigate-to-b2c-context.md)e quindi aprire hello **Azure Active Directory B2C** blade.
2. Fare clic su **Tutti i criteri**.
3. Fare clic su **Carica il criterio**.
4. Caricare `SignUpOrSignin.xml` con hello  *\<ContentDefinitions\>*  tag aggiunto in precedenza.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Verificare i criteri personalizzati di hello utilizzando **Esegui ora**

1. In hello **Azure Active Directory B2C** pannello andare troppo**tutti i criteri**.
2. Selezionare i criteri personalizzati hello caricato, quindi scegliere hello **Esegui ora** pulsante.
3. Dovrebbe essere in grado di toosign backup utilizzando un indirizzo di posta elettronica.

## <a name="reference"></a>riferimento

È possibile trovare modelli di esempio per la personalizzazione dell'interfaccia utente qui:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

cartella sample_templates/wingtip Hello contiene i seguenti file HTML hello:

| Modello HTML5 | Descrizione |
|----------------|-------------|
| *phonefactor.html* | Usare questo file come modello per una pagina di autenticazione a più fattori. |
| *resetpassword.html* | Usare questo file come modello per una pagina Password dimenticata. |
| *selfasserted.html* | Usare questo file come modello per una pagina di iscrizione all'account di social networking, una pagina di iscrizione dell'account locale o una pagina di accesso dell'account locale. |
| *unified.html* | Usare questo file come modello per una pagina unificata per l'iscrizione o l'accesso. |
| *updateprofile.html* | Usare questo file come modello per una pagina di aggiornamento del profilo. |

In hello [modificare la sezione criteri personalizzati di iscrizione o accesso](#modify-your-sign-up-or-sign-in-custom-policy), è stato configurato per la definizione del contenuto hello `api.idpselections`. set completo di Hello di definizione del contenuto ID riconosciuti dal framework di esperienza di Azure Active Directory B2C hello identità e le relative descrizioni sono in hello nella tabella seguente:

| ID definizione del contenuto | Descrizione | 
|-----------------------|-------------|
| *api.error* | **Pagina di errore**. Questa pagina viene visualizzata quando viene rilevata un'eccezione o un errore. |
| *api.idpselections* | **Pagina di selezione del provider di identità**. Questa pagina contiene un elenco di identità, i provider che hello utente sono disponibili durante l'accesso. Si tratta di provider di identità aziendali, provider di identità basati su social network, ad esempio Facebook e Google+, o account locali. |
| *api.idpselections.signup* | **Selezione del provider di identità per l'iscrizione**. Questa pagina contiene un elenco di provider che hello utente sono disponibili durante l'iscrizione di identità. Si tratta di provider di identità aziendali, provider di identità basati su social network, ad esempio Facebook e Google+, o account locali. |
| *api.localaccountpasswordreset* | **Pagina Password dimenticata**. Questa pagina contiene un form utente hello deve completare tooinitiate la reimpostazione della password.  |
| *api.localaccountsignin* | **Pagina di accesso dell'account locale**. Questa pagina contiene un modulo per eseguire l'accesso con un account locale basato su indirizzo di posta elettronica o nome utente. modulo Hello può contenere una casella di input di testo e una casella di immissione di password. |
| *api.localaccountsignup* | **Pagina di iscrizione dell'account locale**. Questa pagina contiene un modulo per eseguire l'iscrizione a un account locale basato su indirizzo di posta elettronica o nome utente. modulo Hello può contenere vari controlli di input, ad esempio una casella di input di testo, una casella di immissione della password, un pulsante di opzione, caselle di riepilogo a selezione singola e selezionare più caselle di controllo. |
| *api.phonefactor* | **Pagina dell'autenticazione a più fattori**. In questa pagina gli utenti possono verificare il proprio numero di telefono (tramite SMS o chiamata vocale) durante la procedura di iscrizione o di accesso. |
| *api.selfasserted* | **Pagina di iscrizione dell'account locale**. Questa pagina contiene un modulo di iscrizione che l'utente deve compilare per effettuare l'iscrizione usando un account esistente di un provider di identità basato su social network, ad esempio Facebook o Google+. Questa pagina è simile toohello prima pagina di iscrizione account sociali, ad eccezione di campi di immissione di password hello. |
| *api.selfasserted.profileupdate* | **Pagina di aggiornamento del profilo**. Questa pagina contiene un modulo che gli utenti possono usare tooupdate proprio profilo. Questa pagina è simile toohello account social pagina di iscrizione, ad eccezione di campi di immissione di password hello. |
| *api.signuporsignin* | **Pagina unificata per l'iscrizione o l'accesso**. Questa pagina consente di gestire entrambe hello iscrizione e accesso di utenti, che possono usare provider di identità enterprise, i provider di identità di social networking, ad esempio Facebook o Google + o gli account locali.  |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sugli elementi dell'interfaccia utente che è possibile personalizzare, vedere la [guida di riferimento per la personalizzazione dell'interfaccia utente per i criteri predefiniti](active-directory-b2c-reference-ui-customization.md).
