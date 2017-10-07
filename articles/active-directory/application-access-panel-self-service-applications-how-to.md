---
title: accesso all'applicazione self-service toouse aaaHow | Documenti Microsoft
description: Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni
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
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a>Modalità di accesso dell'applicazione self-service toouse

Gli utenti self-possano individuare le applicazioni dal Pannello di accesso, è necessario tooenable **accesso all'applicazione self-service** tooany applicazioni che si desidera tooallow utenti tooself-individuare e richiedere l'accesso a.

Questa funzionalità è un ottimo modo per si toosave tempo e denaro come un gruppo IT ed è consigliata come parte di una distribuzione di applicazioni moderne con Azure Active Directory.

Questa funzionalità permette di:

-   Consentire agli utenti self-individuare le applicazioni da hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) senza richiedere l'intervento dell'IT hello gruppo.

-   Aggiungere tali gruppo di utenti tooa preconfigurato pertanto è possibile vedere chi ha richiesto l'accesso, rimuovere l'accesso e gestire i ruoli di hello assegnati toothem.

-   Facoltativamente consente un responsabile approvazione business tooapprove le richieste di accesso dell'applicazione in modo che non debba hello gruppo IT.

-   Configurare facoltativamente too10 chiunque possono approvare l'applicazione toothis di accesso.

-   Consente, facoltativamente, un responsabile approvazione business password hello tooset tali utenti possono utilizzare toosign nell'applicazione toohello, direttamente da del revisore business hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).

-   Assegnare facoltativamente automaticamente ruolo applicazione di self-service agli utenti assegnati tooan direttamente.

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

   * I gruppi non sono supportati.

13. **Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera ruolo tooa di tooassign utenti approvati self-service, fare clic su Avanti toohello di hello selettore **toowhich ruolo devono essere assegnati agli utenti in questo applicazione?**  tooselect hello ruolo toowhich devono essere assegnati questi utenti.

14. Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello pannello toofinish.

Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stata abilitata Accesso self-service. Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/). È possibile attivare un messaggio di posta elettronica che comunica loro quando un utente ha richiesto l'applicazione di accesso tooan che richiede l'approvazione. 

Queste approvazioni supportano solo flussi di lavoro, vale a dire che se si specificano più responsabili approvazione, qualsiasi Approvatore singolo può approvare applicazione toohello accesso.

## <a name="next-steps"></a>Passaggi successivi
[Configurazione di Azure Active Directory per la gestione self-service dei gruppi](active-directory-accessmanagement-self-service-group-management.md)
