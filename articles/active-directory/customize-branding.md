---
title: aaaCustomize accesso pagina hello Azure Active Directory | Documenti Microsoft
description: Informazioni su come tooadd una pagina toohello Accedi Azure branding aziendale
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Guida introduttiva: Aggiungere informazioni personalizzate distintive tooyour nella pagina di accesso di Azure AD della società
tooavoid confusione, molte società desidera tooapply un aspetto coerente in tutti i siti Web di hello e i servizi gestiti. Azure Active Directory (Azure AD) offre questa funzionalità, consentendo l'aspetto di hello toocustomize di hello nella pagina di accesso con il logo della società e combinazioni di colori personalizzati. pagina di accesso Hello è hello pagina viene visualizzata quando si accede tooOffice 365 o altre applicazioni basate su web che usano Azure AD come provider di identità. Si interagiscono con tooenter questa pagina delle credenziali.

> [!NOTE]
> * Branding aziendale è disponibile solo se è stato aggiornato toohello Premium o Edizione Basic di Azure Active Directory o avere una licenza di Office 365. toolearn se una funzionalità è supportata dal tipo di licenza, controllare hello [pagina informazioni sui prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Azure Active Directory Premium e le edizioni Basic sono disponibili per i clienti in Cina tramite hello istanza globale di Azure Active Directory. Azure Active Directory Premium e le edizioni Basic non sono attualmente supportate nel servizio di Microsoft Azure hello gestito da 21Vianet in Cina. Per ulteriori informazioni, contattare Microsoft in hello [Forum di Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Personalizzazione pagina di accesso hello

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Le personalizzazioni di personalizzazione sono disponibili nella pagina di accesso hello Azure AD quando gli utenti accedono un URL specifico del tenant, ad esempio società [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Quando gli utenti visitano un URL generico, ad esempio www.office.com, hello nella pagina di accesso non contiene marchio personalizzazioni perché il sistema di hello non riconosce l'identità utente hello della società. Le informazioni personalizzate distintive dell'azienda vengono visualizzate non appena gli utenti immettono l'ID utente o selezionano un riquadro utente.

> [!NOTE]
> * Il nome di dominio deve risultare "Attivo" nella hello **domini** hello di parte del portale di Azure in cui è stata configurata la personalizzazione. Per altre informazioni, vedere [Add a custom domain name](add-custom-domain.md) (Aggiungere un nome di dominio personalizzato).
> * Personalizzazione pagina di accesso non trasferiti toohello-pagina di accesso per gli account Microsoft personale. Se ai dipendenti o agli utenti guest aziendali accedere con un account Microsoft personale, la pagina di accesso non riflette hello personalizzazione dell'organizzazione.


### <a name="banner-logo"></a>Logo banner 

Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
logo banner Hello viene visualizzato nella Accedi hello e pagine del Pannello di accesso hello.<br>In hello-pagina di accesso, vengono visualizzati una volta determinato organizzazione dell'utente hello, in genere dopo l'immissione di nome utente hello.  | JPG o PNG trasparente<br>Altezza massima: 36 pixel<br>Larghezza massima: 245 pixel | Usare il logo dell'organizzazione in questa posizione.<br>Usare un'immagine trasparente. Non presupporre che background hello sarà bianco.<br>Non aggiungere spaziatura interna del logo nell'immagine hello o il logo avrà un aspetto estremamente piccolo.

### <a name="username-hint"></a>Suggerimento per il nome utente   
Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
Consente di personalizzare il testo di suggerimento hello nel campo nome utente hello. | Testo Unicode dei caratteri too64<br>Solo testo normale | È consigliabile non impostarla se si prevede che gli utenti guest di fuori del toosign organizzazione nell'app tooyour.
            
### <a name="sign-in-page-text"></a>Testo della pagina di accesso   
Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
Questo verrà visualizzato nella parte inferiore di hello del modulo di accesso hello e può essere utilizzato toocommunicate informazioni aggiuntive, ad esempio hello phone numero tooyour help desk o una nota legale. | Testo Unicode dei caratteri too256<br>Solo testo normale, senza collegamenti o tag HTML 

### <a name="sign-in-page-image"></a>Immagine della pagina di accesso  
Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
Questo valore viene visualizzato in background hello di hello-pagina di accesso, è ancorata toohello centro di spazio visualizzabile hello e scalare e ritagliare toofill finestra del browser hello.  <br>Negli schermi stretti, come quelli dei telefoni cellulari, l'immagine non viene visualizzata.<br>Una maschera nera con opacità 0,55 verrà applicata su questa immagine dal codice quando viene caricata la pagina hello. | JPG o PNG<br>Dimensioni immagine: 1920 x 1080 pixel<br>Dimensioni del file: &gt; 300 KB | <br>Usare le immagini nei casi in cui non è necessario richiamare l'attenzione sull'argomento. Hello opaco Accedi form viene visualizzato il centro di hello di questa immagine e possono coprire qualsiasi parte dell'immagine di hello in base alle dimensioni di hello hello finestra del browser.<br>Mantenere i tempi di caricamento rapido tooensure possibili assuma dimensioni del file hello. 

### <a name="background-color"></a>Colore di sfondo
Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
Questo colore è usato al posto di immagine di sfondo hello per le connessioni a larghezza di banda ridotta. |   Colore RGB in formato esadecimale (esempio: #FFFFFF) | È consigliabile utilizzare il colore primario hello del logo banner hello o il colore dell'organizzazione.

### <a name="show-option-tooremain-signed-in"></a>Mostra l'opzione tooremain effettuato l'accesso
Descrizione | Vincoli | Raccomandazioni
------- | ------- | ----------
Accesso AD Azure offre hello utente hello opzione tooremain connesso quando viene chiuso e riaprire il browser. Utilizzare questo toohide tale opzione.<br>Impostare questo troppo "No" toohide questa opzione agli utenti. | &nbsp; | Questa impostazione non influisce sulla durata della sessione.<br>Alcune funzionalità di SharePoint Online e Office 2010 dipendono dagli utenti in grado di toochoose tooremain effettuato l'accesso. Se si imposta questo toobe nascosta, gli utenti potrebbero notare aggiuntive e impreviste prompt toosign-in.

> [!NOTE]
> Tutti gli elementi sono facoltativi. Ad esempio, se si specifica un logo banner con alcuna immagine di sfondo, hello nella pagina di accesso mostrerà immagine di sfondo del logo e hello per il sito di destinazione hello (ad esempio, Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Aggiungere informazioni personalizzate distintive tooyour directory della società

1. Accedi troppo[hello Azure portal](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **personalizzazione specifica della società**.
4. In hello **utenti e gruppi - personalizzazione specifica della società** blade, seleziona hello **modifica** comando.

    ![Modificare le informazioni personalizzate](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificare gli elementi di hello desiderati toocustomize. Tutti gli elementi sono facoltativi.
6. Fare clic su **Salva**.

Potrebbe essere necessaria fino tooan ora per tutte le modifiche apportate toohello Accedi pagina tooappear personalizzazione.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Aggiungere personalizzazione tooyour directory della società specifiche della lingua

1. Accedi toohello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **personalizzazione specifica della società**.
4. In hello **utenti e gruppi - personalizzazione specifica della società** blade, seleziona hello **Aggiungi lingua** comando.

    ![Aggiungere elementi personalizzati distintivi dell'azienda specifiche della lingua](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modificare gli elementi di hello desiderati toocustomize. Tutti gli elementi sono facoltativi.
6. Fare clic su **Salva**.

Potrebbe essere necessaria fino tooan ora per tutte le modifiche apportate toohello Accedi pagina tooappear personalizzazione.

## <a name="next-steps"></a>Passaggi successivi
In questa Guida rapida, si è appreso come tooadd aziendale personalizzazione tooyour Azure Active directory. 

È possibile utilizzare hello seguente collegamento tooconfigure azienda di branding di Azure AD da hello portale di Azure.

> [!div class="nextstepaction"]
> [Configurare la personalizzazione aziendale](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 