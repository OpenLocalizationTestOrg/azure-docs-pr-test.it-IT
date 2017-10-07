---
title: "società aaaAdd personalizzazione tooyour sign-on e pagine del Pannello di accesso"
description: Informazioni su come una pagina toohello Accedi Azure personalizzazione aziendale tooadd hello pagina e accesso Pannello
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Aggiungere informazioni personalizzate distintive tooyour sign-on e pagine del Pannello di accesso della società
tooavoid confusione, molte società desidera tooapply un aspetto coerente in tutti i siti Web di hello e i servizi gestiti. Azure Active Directory fornisce questa funzionalità, consentendo di aspetto hello toocustomize di hello seguenti pagine web con il logo della società e combinazioni di colori personalizzati:

* **Nella pagina di accesso** -si tratta di pagina di hello che viene visualizzata quando si accede tooOffice 365 o di altre applicazioni basate su web che usano Azure AD come provider di identità. L'interazione con questa pagina durante una Home Realm Discovery o tooenter le credenziali. Hello Home Realm Discovery consente hello sistema tooredirect federata utenti tootheir locale servizio token di sicurezza (ad esempio AD FS).
* **Pagina di accesso pannello** : hello Pannello di accesso è un portale basato sul web che consente di tooview e avviare hello basato su cloud applicazioni l'amministratore di Azure AD ha concesso l'accesso a. tooaccess hello Pannello di accesso, utilizzare hello seguente URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).

In questo argomento viene descritto come personalizzare hello nella pagina di accesso e pagina pannello di accesso hello.

> [!NOTE]
> * Marchio della società è una funzionalità che è disponibile solo se è stato aggiornato toohello Premium o Edizione Basic di Azure Active Directory o un utente di Office 365. Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).
> * Azure Active Directory Premium e le edizioni Basic sono disponibili per i clienti in Cina tramite hello istanza globale di Azure Active Directory. Azure Active Directory Premium e le edizioni Basic non sono attualmente supportate nel servizio di Microsoft Azure hello gestito da 21Vianet in Cina. Per ulteriori informazioni, contattare Microsoft in hello [Forum di Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Personalizzazione pagina di accesso hello
In genere, se è necessario l'accesso basato su browser tooyour cloud App e servizi sottoscritti dall'organizzazione, utilizzare hello nella pagina di accesso.

Se è stato applicato le modifiche tooyour nella pagina di accesso, può richiedere tooan orari per tooappear modifiche hello.

Una pagina di accesso personalizzata viene visualizzata solo quando si visita un servizio con un URL specifico del tenant, ad esempio https://outlook.com/**contoso**.com o https://mail.**contoso**.com.

Quando si visita un servizio con URL non specifici del tenant (ad esempio, https://mail.office365.com), viene visualizzata una pagina di accesso non personalizzata. In questo caso, la personalizzazione viene visualizzata dopo avere immesso il proprio ID utente o avere selezionato un riquadro utente.

> [!NOTE]
> * Il nome di dominio deve risultare "Attivo" nella hello **Active Directory** > **Directory** > **domini** sezione del portale di Azure classico hello in cui è stata configurata la personalizzazione.
> * Personalizzazione pagina di accesso non si estende su toohello consumer firmare nella pagina di Microsoft. Se si accede con un account Microsoft personale, si potrebbe visualizzare un elenco personalizzato di sezioni utente sottoposto a rendering da Azure AD, ma hello personalizzazione dell'organizzazione non è applicabile toohello Microsoft account-pagina di accesso.
>
>

Se si desidera tooshow il marchio dell'azienda, colori e altri elementi personalizzabili in questa pagina, vedere hello seguenti immagini toounderstand hello differenza due esperienze hello.

Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **prima** una personalizzazione:

![Pagina di accesso di Office 365 prima della personalizzazione][1]

Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **dopo** una personalizzazione:

![Pagina di accesso di Office 365 dopo la personalizzazione][2]

Hello schermata riportata di seguito viene illustrato un esempio di pagina di accesso hello Office 365 in un dispositivo mobile **prima** una personalizzazione:

![Pagina di accesso di Office 365 prima della personalizzazione][3]

Hello schermata riportata di seguito viene illustrato un esempio di pagina di accesso hello Office 365 in un dispositivo mobile **dopo** una personalizzazione:

![Pagina di accesso di Office 365 dopo la personalizzazione][4]

Quando si ridimensiona una finestra del browser, hello immagine di grandi dimensioni, ad esempio hello illustrato in precedenza, è spesso ritagliate tooaccommodate le proporzioni dello schermo diverse. A tal fine, è consigliabile provare tookeep hello elementi visivi principali nell'illustrazione hello in modo che vengano sempre visualizzati nell'angolo superiore sinistro hello (alto a destra per lingue da destra a sinistra). Questo è importante perché il ridimensionamento in genere si verifica uscire bottom-right-corner hello verso hello superiore / sinistro o dal basso hello parte superiore di hello.

Hello immagine riportata di seguito viene illustrato come figura hello viene ritagliata quando hello browser ridimensionato toohello a sinistra:

![][6]

Ecco come viene visualizzato dopo hello browser ridimensionato verso l'alto hello:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Gli elementi nella pagina hello è possibile personalizzare?
È possibile personalizzare i seguenti elementi nella pagina di accesso hello hello:

![][5]

| Elemento della pagina | Posizione nella pagina hello |
|:--- | --- |
| Logo banner |Visualizzato hello superiore destro della pagina hello. Sostituisce hello logo hello destinazione sito che cui si accede toodisplays (ad esempio. Office 365 o Azure. |
| Immagine di grandi dimensioni/colore di sfondo |Visualizzati a sinistra di hello della pagina hello. Sostituisce hello immagine hello destinazione sito che cui si accede toodisplays. Hello colore di sfondo può essere visualizzato in sostituzione hello immagine di grandi dimensioni per le connessioni a larghezza di banda ridotta o nelle schermate "narrow". |
| Mantieni l'accesso |Visualizzato nella casella di testo Password hello. |
| Testo pagina di accesso |Sopra il piè di pagina hello quando è necessario tooconvey informazioni utili prima un Accedi con un account aziendale o dell'istituto di istruzione. Ad esempio, è consigliabile tooinclude hello phone numero tooyour help desk o una nota legale. |

> [!NOTE]
> Tutti gli elementi sono facoltativi. Ad esempio, se si specifica un Logo Banner ma nessuna immagine di grandi dimensioni, pagina di accesso hello Mostra il logo e hello illustrazione per il sito di destinazione hello (vale a dire hello California di Office 365 autostrada immagine).
>
>

Nella pagina accesso hello **Mantieni l'accesso** casella di controllo permette tooremain un utente connesso quando viene chiuso e riaprire il browser. Non influisce sulla durata della sessione. È possibile nascondere una casella di controllo hello hello Azure Active Directory nella pagina di accesso.

Se non viene visualizzata la casella hello dipende dall'impostazione di hello di **nascondere KMSI**.

![][9]

toohide hello casella di controllo, configurare questa impostazione troppo**Hidden**.

> [!NOTE]
> Alcune funzionalità di SharePoint Online e Office 2010 dipendono dagli utenti in grado di toocheck questa casella. Se si configura questa impostazione toohidden, gli utenti potrebbero notare aggiuntive e impreviste prompt toosign-in.
>
>

È anche possibile localizzare tutti gli elementi della pagina. Dopo aver configurato un set di elementi di personalizzazione "predefinito", è possibile configurare altre versioni per impostazioni locali diverse. È anche possibile combinare e abbinare diversi elementi. Ad esempio, è possibile:

* Creare un'immagine di grandi dimensioni "predefinita" adatta per tutte le impostazioni cultura, quindi creare versioni specifiche per l'inglese e il francese. Quando si imposta il tooone browser di queste due lingue, hello specifico immagine viene visualizzata, mentre l'immagine predefinita hello viene visualizzata per tutti gli altri linguaggi.
* Configurare logo diversi per l'organizzazione, ad esempio una versione giapponese o ebraica.

## <a name="access-panel-page-customization"></a>Personalizzazione del pannello di accesso
pagina del Pannello di accesso Hello è essenzialmente una pagina del portale per App per cloud toohello accesso rapido che è stato concesso l'accesso tooby l'amministratore. In questa pagina le app vengono visualizzate come icone applicazione su cui è possibile fare clic.

Hello seguente schermata mostra un esempio di una pagina del Pannello di accesso dopo la personalizzazione.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Configurare la directory con informazioni personalizzate distintive dell'azienda
È possibile configurare un set predefinito di elementi personalizzabili per ogni directory nel portale di Azure classico hello. Dopo che sono state salvate le impostazioni predefinite di hello, un amministratore può aggiungere versioni localizzate di ogni elemento, per le diverse lingue / impostazioni locali. Tutti gli elementi personalizzabili sono facoltativi.

Ad esempio, se si configura un Logo Banner predefinito, ma nessuna immagine di grandi dimensioni, hello nella pagina di accesso consente di visualizzare il logo nell'angolo superiore destro di hello. Tuttavia, viene visualizzata l'immagine predefinita hello del sito hello.

Si supponga hello seguente configurazione:

* Un logo del banner predefinito e testo della pagina di accesso in inglese
* Testo della pagina di accesso specifica della lingua per il tedesco

Se le preferenze di lingua sono il tedesco, si ottiene hello predefinito Logo Banner ma hello testo in tedesco.

Sebbene sia tecnicamente possibile configurare un set diverso per ogni lingua supportata da Azure AD, si consiglia di mantenere il numero di hello di varianti basso, per motivi di prestazioni e manutenzione.

> [!IMPORTANT]
> Yammer non non mostra hello di Azure AD marchio nella pagina di accesso fino a dopo l'accesso dell'utente hello. utente Hello Visualizza hello innanzitutto generica pagina di Office 365, e quindi hello marchio pagina in seguito.   
 
 
**tooadd personalizzazione tooyour directory aziendale, eseguire hello alla procedura seguente:**

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore della directory hello desiderato toocustomize.
2. Selezionare la directory di hello desiderato toocustomize.
3. Nella barra degli strumenti hello in primo piano hello, fare clic su **configura**.
4. Fare clic su **Modifica personalizzazione**.
5. Modificare gli elementi di hello desiderati toocustomize. Tutti i campi sono facoltativi.
6. Fare clic su **Salva**.

Può richiedere tooan ora per la nuova modifica viene apportata toohello nella pagina di accesso tooappear di branding.

**società specifiche della lingua tooadd personalizzazione, eseguire hello alla procedura seguente:**

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore della directory hello desiderato toocustomize.
2. Selezionare la directory di hello desiderato toocustomize.
fs3. Nella barra degli strumenti hello in primo piano hello, fare clic su **configura**.
4. Fare clic su **Modifica personalizzazione**.
5. Fare clic su **Aggiungi impostazioni di personalizzazione per una lingua specifica**.
6. Selezionare hello lingua che si desidera che il logo hello toocustomize per, quindi fare clic su **Avanti**.
7. Modificare solo gli elementi di hello per cui si desidera esegue l'override di tooconfigure specifici della lingua. Tutti i campi sono facoltativi. Se un campo viene lasciato vuoto, quindi valore predefinito personalizzato hello viene visualizzato invece (o hello predefinito Microsoft se non è configurato un valore predefinito personalizzato).
8. Fare clic su **Salva**.

**società tooremove personalizzazione dalla directory, eseguire hello alla procedura seguente:**

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore della directory hello desiderato toocustomize.
2. Selezionare la directory di hello desiderato toocustomize.
3. Nella barra degli strumenti hello in primo piano hello, fare clic su **configura**.
4. Fare clic su **Modifica personalizzazione**.
5. Nella pagina Modifica personalizzazione hello selezionare **Modifica impostazioni di personalizzazione esistenti** e quindi passare toohello di pagina successiva.
6. A seconda di quali elementi si desidera tooremove, eseguire una o più dei seguenti hello:

    a. In **Logo banner** selezionare **Rimuovi logo caricato**.

    b. In **Logo icona** selezionare **Rimuovi logo caricato**.

    c. Rimuovere il testo hello da tutte le caselle di testo.

    d. Fare clic su **Next**.

    e. Rimuovere il testo hello da tutte le caselle di testo.
7. Fare clic su **salvare** elementi hello tooremove.
8. Se necessario, fare clic su **personalizzazione** nuovamente e ripetere i passaggi per tutte le specifiche della lingua personalizzazione che deve toobe rimosso.
    Tutte le impostazioni di personalizzazione sono state rimosse quando si fa clic **personalizzazione** e vedere hello **predefinito personalizzazione** modulo senza configurata alcuna impostazione esistente.

## <a name="testing-and-examples"></a>Test ed esempi
È consigliabile tentare con un tenant di prova prima di apportare modifiche nell'ambiente di produzione.

**tooverify se la personalizzazione sia stata applicata:**

1. Aprire una sessione del browser in incognito o InPrivate.
2. Visitare https://outlook.com/contoso.com, sostituendo contoso.com con il dominio hello che è stato personalizzato.

Questo metodo funziona con i domini simili a contoso.onmicrosoft.com.

toohelp si creano set di personalizzazione efficaci, sono state personalizzate hello due fittizio delle pagine di accesso seguenti:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

le impostazioni specifiche della lingua hello tootest, è necessario preferenze della lingua predefinita hello toomodify nel web browser tooa lingua installata nella personalizzazione. In Internet Explorer è eseguire questa configurazione in hello **Opzioni Internet** menu.

## <a name="customizable-elements"></a>Elementi personalizzabili
Alcuni elementi personalizzabili in Azure AD prevedono più casi di utilizzo. È possibile configurare il logo della società una volta per ogni directory e viene utilizzata, accedi hello sia nel Pannello di accesso. Alcuni elementi personalizzabili sono specifici solo toohello nella pagina di accesso. Hello nella tabella seguente fornisce dettagli per hello diversi elementi personalizzabili.

| Nome | Descrizione | Vincoli | Consigli |
| --- | --- | --- | --- |
| Logo banner |Logo Banner Hello viene visualizzata nella pagina di accesso hello hello Pannello di accesso. |<p>JPG o PNG</p><p>60x280 pixel</p><p>10 KB</p> |<p>Usare il logo completo dell'organizzazione, inclusi il simbolo e il logotipo</p><p>Mantenerla in 30 pixel tooavoid elevata Introduzione a barre di scorrimento nei dispositivi mobili</p><p>Non superare 4 KB</p><p>Usare un PNG trasparente (non presupporre che hello nella pagina di accesso dispone sempre di uno sfondo bianco)</p> |
| Logo icona |(attualmente non utilizzato nella pagina di accesso hello) In hello future, questo testo può essere utilizzato tooreplace hello generico "aziendale o dell'istituto di istruzione account" pittogramma in diverse posizioni dell'esperienza di hello. |<p>JPG o PNG</p><p>120x120 pixel</p><p>10 KB</p> |<p>Usare uno stile semplice (non testo piccolo), come questa immagine può essere ridimensionato too50% |
| </p> | | | |
| Etichetta nome utente pagina di accesso |(attualmente non utilizzato nella pagina di accesso hello) In hello future, questo testo può essere utilizzato tooreplace hello stringa generica "aziendale o dell'istituto di istruzione account" in diverse posizioni dell'esperienza di hello. È possibile impostare toosomething come "account Contoso" o "ID Contoso" |<p>Testo Unicode, i caratteri too50</p><p>Solo testo normale, senza collegamenti o tag HTML</p> |<p>Mantenere breve e semplice</p><p>Chiedere agli utenti come sono in genere riferimento toohello lavoro o scuola account che loro fornito.</p> |
| Testo pagina di accesso |Il testo "standard" viene visualizzato sotto forma di hello nella pagina di accesso e può essere utilizzato toocommunicate ulteriori istruzioni, oppure dove tooget Guida e supporto tecnico. |<p>Testo Unicode, i caratteri too256</p><p>Solo testo normale, senza collegamenti o tag HTML</p> |Mantenere il numero di caratteri inferiore a 250 (circa tre righe di testo) |
| Illustrazione pagina di accesso |Figura Hello è un'immagine di grandi dimensioni che viene visualizzata a sinistra di toohello hello nella pagina di accesso del modulo della pagina di accesso hello. |<p>JPG o PNG</p><p>1420x1200</p><p>500 KB</p> |<p>1420x1200 pixel</p><p>Importante: mantenere il file quanto più piccolo possibile, idealmente meno di 200 KB. Se questa immagine è troppo grande, sulle prestazioni di hello di hello nella pagina di accesso quando non è memorizzato nella cache immagine hello</p><p>Questa immagine viene spesso ritagliata, proporzioni dello schermo diverse tooaccommodate. Tenere elementi visivi principali hello hello nell'angolo superiore sinistro (superiore destro per le lingue da destra a sinistra), in quanto si verifica il ridimensionamento nell'angolo inferiore destro hello verso hello superiore / sinistro, come finestra del browser hello compatta.</p> |
| Colore di sfondo della pagina di accesso |colore di sfondo nella pagina di accesso Hello viene utilizzato a sinistra di toohello hello area del modulo della pagina di accesso hello. |Deve essere un colore RGB in formato esadecimale (esempio: #FFFFFF) |<p>colore di sfondo Hello può essere visualizzato in sostituzione hello immagine di grandi dimensioni per le connessioni a larghezza di banda ridotta</p><p>Si consiglia di selezionare il colore primario hello di hello Logo Banner</p> |

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
