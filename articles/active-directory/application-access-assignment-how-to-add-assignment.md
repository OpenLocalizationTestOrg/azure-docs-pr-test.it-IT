---
title: applicazione tooan utenti e gruppi aaaHow tooassign | Documenti Microsoft
description: Assegnare gli utenti l'accesso toogrant toohello applicazione
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a>Come applicazione di tooan tooassign utenti e gruppi

Prima che gli utenti possono eseguire hello sotto per un'applicazione specifica, è necessario toofirst **assegnarli applicazione toohello** toogrant loro l'accesso:

-   Accedere a un'applicazione da **passando direttamente l'URL dell'applicazione toohello** (noto anche come SP initiated sign-on).

-   Accedere a un'applicazione utilizzando hello **URL di accesso utente** in un'applicazione **proprietà** pagina (noto anche come avviata da IDP sign-on).

-   Visualizzare un'applicazione nel [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) o l'applicazione per dispositivi mobili.

-   Visualizzare un'applicazione nell'[icona di avvio delle app di Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).

## <a name="methods-tooassign-applications-with-azure-active-directory"></a>Applicazioni tooassign metodi con Azure Active Directory 

Esistono 3 modi per poter assegnare applicazioni con Azure Active Directory:

-   [Assegnare un utente direttamente tooan applicazione come amministratore](#assign-a-user-directly-as-an-administrator)

-   [Assegnare un gruppo direttamente tooan applicazione come amministratore](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>Assegnare un utente direttamente come amministratore

tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.

7.  Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.

9.  Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.

10. Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.

13. Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.

Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Assegnare un gruppo direttamente tooan applicazione come amministratore

tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.

7.  Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.

9.  Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.

10. Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.

13. Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.

Dopo un breve periodo di tempo, gli utenti di hello all'interno di gruppi di hello selezionati in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello. Se i gruppi sono dinamici, potrebbe verificarsi un ritardo di elaborazione aggiuntivo nella visualizzazione di queste assegnazioni per gli utenti dei gruppi assegnati.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni

Accesso all'applicazione self-service è tooself di utenti tooallow un ottimo modo-individuare le applicazioni, se lo si desidera consentire hello business gruppo tooapprove accesso toothose applicazioni. È possibile consentire le credenziali di hello toomanage di hello business gruppo assegnati agli utenti di toothose per il diritto di Single Sign-in applicazioni Password dai loro pannelli di accesso.

tooenable self-service accesso tooan applicazione, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello tooenable accesso self-service toofrom hello elenco.

7.  Una volta che un'applicazione hello caricato, fare clic su **self-service** dal menu di navigazione a sinistra dell'applicazione hello.

8.  tooenable accesso all'applicazione self-service per questa applicazione, attivare hello **consentire agli utenti dell'applicazione di toothis accesso toorequest?** attivare o disattivare troppo**Sì.**

9.  Tooselect hello toowhich agli utenti del gruppo che richiedono accesso toothis applicazione deve essere aggiunto, fare quindi clic su Avanti toohello etichetta di hello selettore **toowhich gruppo deve assegnare gli utenti aggiunti?** e selezionare un gruppo.

10. **Facoltativo:** toorequire un'approvazione business prima che gli utenti sono autorizzati ad accedere, impostare hello **richiedono l'approvazione prima di concedere l'accesso toothis applicazione?** attivare o disattivare troppo**Sì**.

11. **Facoltativo: per applicazioni tramite password single sign-on, solo** tooallow password hello toospecify responsabili approvazione business che vengono inviate toothis applicazione per gli utenti approvati, impostare hello **Consenti ai responsabili approvazione tooset password dell'utente per questa applicazione?**  attivare o disattivare troppo**Sì**.

12. **Facoltativo:** toospecify hello business responsabili approvazione sono consentiti l'applicazione di toothis tooapprove accesso, fare clic sull'etichetta hello selettore successivo toohello **chi è autorizzato l'applicazione di toothis tooapprove accesso?** tooselect backup responsabili approvazione singole business too10.

  >[!NOTE]
  >I gruppi non sono supportati.
  >
  >

13. **Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera ruolo tooa di tooassign utenti approvati self-service, fare clic su Avanti toohello di hello selettore **toowhich ruolo devono essere assegnati agli utenti in questo applicazione?**  tooselect hello ruolo toowhich devono essere assegnati questi utenti.

14. Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello pannello toofinish.

Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stata abilitata Accesso self-service. Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/). È possibile attivare un messaggio di posta elettronica che comunica loro quando un utente ha richiesto l'applicazione di accesso tooan che richiede l'approvazione. 

Queste approvazioni supportano solo flussi di lavoro, vale a dire che se si specificano più responsabili approvazione, qualsiasi Approvatore singolo può applicazione toohello di responsabile approvazione accesso.

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)
