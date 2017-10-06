---
title: 'Azure Active Directory B2C: strumento di supporto per la personalizzazione dell''interfaccia utente della pagina | Documentazione Microsoft'
description: "Funzionalità di personalizzazione dell'interfaccia utente di toodemonstrate hello pagina usato da uno strumento di supporto in Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure Active B2C di Directory: Uno strumento di supporto utilizzato toodemonstrate hello pagina funzionalità dell'interfaccia utente (UI) personalizzazione
Questo articolo è una toohello complementare [articolo di personalizzazione dell'interfaccia utente principale](active-directory-b2c-reference-ui-customization.md) in Azure Active Directory (Azure AD) B2C. Hello passaggi seguenti descrivono come tooexercise hello funzionalità personalizzazione dell'interfaccia utente delle pagine con contenuto HTML e CSS di esempio che è stato fornito.

## <a name="get-an-azure-ad-b2c-tenant"></a>Ottenere un tenant di Azure AD B2C
Prima di poter personalizzare qualsiasi elemento, è necessario troppo[ottenere un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md) se non si dispone già uno.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Creare un criterio di iscrizione o accesso
Hello contenuto di esempio fornito può essere utilizzato toocustomze due pagine in un [criteri iscrizione o accesso](active-directory-b2c-reference-policies.md): hello [unificata nella pagina di accesso](active-directory-b2c-reference-ui-customization.md) e hello [attributi self-asserzione pagina](active-directory-b2c-reference-ui-customization.md). Quando si [creano criteri di iscrizione o di accesso](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), aggiungere l'account locale (indirizzo di posta elettronica), Facebook, Google e Microsoft come **provider di identità**. Questi sono hello solo IDPs che accetta il contenuto HTML di esempio.  È anche possibile aggiungere un subset di questi provider di identità se necessario.

## <a name="register-an-application"></a>Registrare un'applicazione
È necessario troppo[registrare un'applicazione](active-directory-b2c-app-registration.md) il B2C tenant che può essere utilizzato tooexecute i criteri. Dopo la registrazione dell'applicazione, si dispone di alcune opzioni che è possibile utilizzare tooactually eseguire i criteri di iscrizione:

* Creazione di hello Azure Active Directory B2C avvio rapido di applicazioni elencate nella sezione hello "Guida introduttiva" del [firmare backup e l'accesso degli utenti nelle applicazioni](active-directory-b2c-overview.md#get-started).
* Hello utilizzare predefinita [palestra per Azure Active Directory B2C](https://aadb2cplayground.azurewebsites.net) dell'applicazione. Se si sceglie palestra per hello toouse, è necessario registrare un'applicazione nel tenant di B2C utilizzando hello **URI di reindirizzamento** `https://aadb2cplayground.azurewebsites.net/`.
* Hello utilizzare **Esegui** pulsante i criteri di hello [portale di Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Personalizzare il criterio
toocustomize hello aspetto dei criteri, è necessario toofirst creare file HTML e CSS utilizzando hello convenzioni specifiche di Azure Active Directory B2C. È quindi possibile caricare il percorso disponibile pubblicamente tooa contenuto statico, in modo che possano accedervi Azure Active Directory B2C. ad esempio un server Web dedicato, un archivio BLOB di Azure, una rete per la distribuzione di contenuti di Azure o qualsiasi altro provider di servizi di hosting di risorse statiche. Hello unici requisiti sono che il contenuto è disponibile tramite HTTPS e sono accessibili tramite CORS. Dopo aver esposta su web hello il contenuto statico, è possibile modificare i criteri toopoint toothis località e che i clienti tooyour di contenuto. Hello [articolo di personalizzazione dell'interfaccia utente principale](active-directory-b2c-reference-ui-customization.md) viene illustrato in dettaglio il funzionamento delle funzionalità di personalizzazione hello Azure Active Directory B2C.

Ai fini di hello di questa esercitazione, aver già creato alcuni contenuti di esempio e viene ospitato in archiviazione Blob di Azure. contenuto di esempio Hello è una personalizzazione di base in tema di hello della nostra società fittizia, "Wingtip Toys". tootry, con i propri criteri, seguire questi passaggi:

1. Accedi a tenant tooyour su hello [portale di Azure](https://portal.azure.com/) e passare a pannello funzionalità toohello B2C.
2. Fare clic su **Sign-up or sign-in policies** (Criteri di iscrizione o di accesso) e quindi sul criterio, ad esempio "b2c\_1\_sign\_up\_sign\_in").
3. Fare clic su **Page UI customization** (Personalizzazione dell'interfaccia utente della pagina) e quindi **Pagina unificata per l'iscrizione o l'accesso**.
4. Hello attiva/disattiva **pagina personalizzata utilizza** passare troppo**Sì**. In hello **pagina personalizzati URI** immettere `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Fare clic su **OK**.
5. Fare clic su **Pagina di iscrizione dell'account locale**. Hello attiva/disattiva **Usa modello personalizzato** passare troppo**Sì**. In hello **pagina personalizzati URI** immettere `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Ripetizione hello stesso passaggio per hello **pagina di iscrizione account Social**.
   Fare clic su **OK** pannelli di personalizzazione due volte tooclose hello dell'interfaccia utente.
7. Fare clic su **Salva**.

È ora possibile provare il criterio personalizzato. È possibile utilizzare la propria palestra per Azure Active Directory B2C hello o applicazione se si desidera, ma è possibile scegliere anche semplicemente hello **Esegui** comando nel pannello criteri hello. Selezionare l'applicazione nella casella di riepilogo a discesa hello e scegliere l'URI di reindirizzamento appropriato hello. Fare clic su hello **Esegui ora** pulsante. Verrà aperta una nuova scheda del browser ed è possibile eseguire tramite l'esperienza dell'utente di effettuare l'iscrizione per l'applicazione con il nuovo contenuto hello sul posto hello!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Caricare hello tooAzure contenuto di esempio nell'archiviazione Blob
Se si desidera toouse archiviazione Blob di Azure toohost pagina contenuta, è possibile creare il proprio account di archiviazione e usare il nostro tooupload strumento di supporto B2C i file.

### <a name="create-a-storage-account"></a>Creare un account di archiviazione
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **+ Nuovo** > **Dati e archiviazione** > **Account archiviazione**. È necessario un toocreate sottoscrizione di Azure, un account di archiviazione Blob di Azure. È possibile effettuare l'iscrizione a una versione di valutazione gratuita in hello [sito Web di Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Fornire un **nome** per account di archiviazione hello (ad esempio, "contoso") e selezione hello le selezioni appropriate per **tariffario**, **gruppo di risorse** e  **Sottoscrizione**. Assicurarsi di avere hello **tooStartboard Pin** opzione selezionata. Fare clic su **Crea**.
4. Tornare indietro toohello schermata iniziale e fare clic su account di archiviazione hello appena creato.
5. In hello **riepilogo** fare clic su **contenitori**, quindi fare clic su **+ Aggiungi**.
6. Fornire un **nome** per il contenitore di hello (ad esempio, "b2c") e selezionare **Blob** come hello **tipo di accesso**. Fare clic su **OK**.
7. contenitore Hello creata verrà visualizzata nell'elenco di hello in hello **BLOB** blade. Annotare l'URL di hello del contenitore di hello. ad esempio, dovrebbe essere simile troppo`https://contoso.blob.core.windows.net/b2c`. Chiude hello **BLOB** blade.
8. Nel Pannello di account di archiviazione hello, fare clic su **chiavi** e annotare i valori hello di hello **nome Account di archiviazione** e **chiave di accesso primaria** campi.

> [!NOTE]
> **Chiave di accesso primaria** è una credenziale di sicurezza importante.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Scaricare i file di esempio e lo strumento di supporto hello
È possibile scaricare hello [file archiviazione Blob di Azure helper strumento e di esempio come file con estensione zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) oppure duplicarlo da GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Questo repository contiene una directory `sample_templates\wingtip` , che include file HTML, CSS e immagini di esempio. Per questi modelli tooreference il proprio account di archiviazione Blob di Azure, sono necessari file hello HTML tooedit. Aprire `unified.html` e `selfasserted.html` e sostituire tutte le istanze di `https://localhost` con hello URL del contenitore che si è preso nota in precedenza hello. È necessario utilizzare hello percorso assoluto del file HTML, perché in questo caso, verrà fornito da Azure AD, nel dominio hello hello HTML hello `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Caricare i file di esempio hello
In hello stesso repository, decomprimere `B2CAzureStorageClient.zip` esecuzione hello e `B2CAzureStorageClient.exe` all'interno del file. Questo programma verrà semplicemente caricare tutti i file nella directory hello specificare tooyour account di archiviazione e abilitare l'accesso a CORS per i file hello. Dopo avere eseguito i passaggi di hello precedenti, hello HTML e file CSS verranno ora puntare tooyour account di archiviazione. Si noti che hello nome dell'account di archiviazione fa parte di hello che precede `blob.core.windows.net`, ad esempio `contoso`. È possibile verificare che il contenuto di hello è stato caricato correttamente provando tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` in un browser. Utilizzare inoltre [http://test-cors.org/](http://test-cors.org/) toomake assicurarsi che il contenuto di hello è ora abilitato CORS. (Cercare "stato XHR: 200" nel risultato hello.)

### <a name="customize-your-policy-again"></a>Personalizzare di nuovo il criterio
Ora che hai caricato account di archiviazione personalizzati di hello esempio tooyour contenuto, è necessario modificare tooreference i criteri per l'abbonamento è. Ripetere i passaggi di hello da hello ["Personalizzare il criterio"](#customize-your-policy) sezione precedente, questa volta utilizzando URL del proprio account di archiviazione. Ad esempio, hello percorso del `unified.html` sarà `<url-of-your-container>/wingtip/unified.html`.

È ora possibile usare hello **Esegui** pulsante o tooexecute la propria applicazione nuovamente i criteri. Hello risultato deve cercare quasi esattamente hello stesso - è stato utilizzato hello uguale in entrambi i casi di esempio HTML e CSS. Tuttavia, i criteri fanno riferimento a questo punto la propria istanza di archiviazione Blob di Azure e si sono tooedit gratuita e caricare i file di hello nuovamente come è.. Per ulteriori informazioni sulla personalizzazione hello HTML e CSS, vedere toohello [articolo di personalizzazione dell'interfaccia utente principale](active-directory-b2c-reference-ui-customization.md).

