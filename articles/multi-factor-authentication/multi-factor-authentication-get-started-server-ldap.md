---
title: "aaaLDAP l'autenticazione e Server di autenticazione a più fattori di Azure | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto della distribuzione di autenticazione LDAP e il Server Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Autenticazione LDAP e server Azure Multi-Factor Authentication
Per impostazione predefinita, hello del Server Azure multi-Factor Authentication è configurato tooimport o sincronizzare utenti da Active Directory. Tuttavia, può essere configurato toobind toodifferent directory LDAP, ad esempio una directory ADAM o un controller di dominio Active Directory specifico. Quando connesso tooa directory tramite LDAP, hello del Server Azure multi-Factor Authentication può agire come un autenticazioni di tooperform proxy LDAP. Consente inoltre di hello utilizzo di binding LDAP come destinazione RADIUS, di pre-autenticazione degli utenti con l'autenticazione IIS o per l'autenticazione primaria nel portale per gli utenti hello Azure MFA.

toouse Azure multi-Factor Authentication come proxy LDAP, inserire hello del Server Azure multi-Factor Authentication tra il client LDAP hello (ad esempio, applicazione, un accessorio VPN) e il server di directory LDAP hello. Hello del Server Azure multi-Factor Authentication deve essere configurato toocommunicate hello client sia con server con directory LDAP hello. In questa configurazione, hello del Server Azure multi-Factor Authentication accetta richieste LDAP dai client server e le applicazioni e li inoltra toohello destinazione LDAP directory server toovalidate hello credenziali primarie. Se la directory LDAP di hello convalida credenziali primarie hello, Azure multi-Factor Authentication esegue una verifica di identità secondo e invia un client LDAP toohello indietro di risposta. intero processo di autenticazione Hello ha esito positivo solo se sia l'autenticazione del server LDAP hello e verifica del secondo passaggio hello hanno esito positivo.

## <a name="configure-ldap-authentication"></a>Configurare l'autenticazione LDAP
autenticazione LDAP tooconfigure, installare hello del Server Azure multi-Factor Authentication in un server Windows. Utilizzare hello seguente procedura:

### <a name="add-an-ldap-client"></a>Aggiungere un client LDAP

1. In hello del Server Azure multi-Factor Authentication, selezionare l'icona autenticazione LDAP hello nel menu a sinistra di hello.
2. Controllare hello **Abilita autenticazione LDAP** casella di controllo.

   ![Autenticazione LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Nella scheda client hello, modificare la porta TCP hello e la porta SSL se hello servizio LDAP di Azure multi-Factor Authentication deve essere associato toolisten porte toonon standard per le richieste LDAP.
4. Se si prevede di toouse LDAPS da hello client toohello Server Azure multi-Factor Authentication, è necessario installare un certificato SSL in hello stesso server come Server di autenticazione a più fattori. Fare clic su **Sfoglia** toohello Avanti SSL casella del certificato e selezionare toouse un certificato per la connessione protetta hello.
5. Fare clic su **Aggiungi**.
6. Nella finestra di dialogo Aggiungi Client LDAP hello, immettere l'indirizzo IP di hello del dispositivo di hello, server o applicazione che autentica toohello Server e il nome dell'applicazione (facoltativo). nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.
7. Controllare hello **corrispondenza utente richiedono Azure multi-Factor Authentication** se tutti gli utenti sono stati o verranno importati in hello Server e verifica tootwo passaggio soggetto. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o non è interessato dalla verifica in due passaggi, lasciare deselezionata la casella hello. Vedere i file della Guida di Server di autenticazione a più fattori hello per ulteriori informazioni su questa funzionalità.

Ripetere questi passaggi tooadd altri client LDAP.

### <a name="configure-hello-ldap-directory-connection"></a>Configurare una connessione della directory LDAP hello

Quando hello Azure multi-Factor Authentication è configurato tooreceive le autenticazioni di LDAP, deve utilizzare un proxy tali directory LDAP di autenticazioni toohello. Di conseguenza, scheda destinazione hello Visualizza solo un singolo grigio toouse opzione una destinazione LDAP.

1. hello tooconfigure connessione della directory LDAP, fare clic su hello **integrazione Directory** icona.
2. Nella scheda Impostazioni hello selezionare hello **Usa configurazione LDAP specifica** pulsante di opzione.
3. Selezionare **Modifica...**
4. Nella finestra di dialogo Modifica configurazione LDAP di hello, compilare i campi di hello con la directory LDAP hello informazioni necessarie tooconnect toohello. Sono incluse le descrizioni dei campi hello hello del Server Azure multi-Factor Authentication file della Guida.

    ![Integrazione di directory](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Test della connessione LDAP hello facendo hello **Test** pulsante.
6. Se il test della connessione LDAP hello ha esito positivo, fare clic su hello **OK** pulsante.
7. Fare clic su hello **filtri** hello scheda Server è preconfigurato tooload contenitori, gruppi di sicurezza e utenti da Active Directory. Se l'associazione tooa altra directory LDAP, è probabilmente necessario filtri hello tooedit visualizzati. Fare clic su hello **Guida** collegamento per ulteriori informazioni sui filtri.
8. Fare clic su hello **attributi** hello scheda Server è preconfigurato toomap attributi da Active Directory.
9. Se si sta associando tooa diverse directory o toochange hello preconfigurato mapping degli attributi LDAP, fare clic su **modifica...**
10. Nella finestra di dialogo Modifica attributi di hello, modificare i mapping degli attributi di hello LDAP per la directory. I nomi di attributo possono essere digitati o selezionati facendo clic su hello **...** campo tooeach pulsante Avanti. Fare clic su hello **Guida** collegamento per ulteriori informazioni sugli attributi.
11. Fare clic su hello **OK** pulsante.
12. Fare clic su hello **impostazioni società** icona e seleziona hello **risoluzione nome utente** scheda.
13. Se ci si connette tooActive Directory da un server di dominio, lasciare hello **identificatori di sicurezza Usa Windows (SID) per la corrispondenza dei nomi utente** pulsante di opzione selezionato. In caso contrario, seleziona hello **attributo dell'identificatore univoco per la corrispondenza dei nomi utente utilizza LDAP** pulsante di opzione. 

Quando hello **attributo dell'identificatore univoco per la corrispondenza dei nomi utente utilizza LDAP** pulsante di opzione è selezionata, hello del Server Azure multi-Factor Authentication tenta tooresolve identificatore univoco di tooa ogni nome utente nella directory LDAP hello. Viene eseguita una ricerca LDAP nel hello Username attributi definiti in hello integrazione Directory -> scheda attributi. Quando un utente esegue l'autenticazione, nome utente di hello è risolto toohello identificatore univoco nella directory LDAP hello. Identificatore univoco di Hello viene utilizzato per l'utente hello corrispondente nel file di dati di hello Azure multi-Factor Authentication. Sono ammessi confronti senza distinzione tra maiuscole e minuscole e formati dei nomi utente lunghi e corti.

Dopo aver completato questi passaggi, hello Server di autenticazione a più fattori è in ascolto sulle porte configurata hello per le richieste di accesso LDAP dai hello configurato i client e opera come un proxy per tali richieste toohello directory LDAP per l'autenticazione.

## <a name="configure-ldap-client"></a>Configurare il client LDAP
tooconfigure hello client LDAP, attenersi alle linee guida di hello:

* Configurare il dispositivo, server o l'applicazione tooauthenticate tramite LDAP toohello Server Azure multi-Factor Authentication come se fosse la directory LDAP. Utilizzare hello stesso impostazioni che normalmente si utilizzerebbe tooconnect direttamente tooyour elenco LDAP, ad eccezione di nome hello del server o indirizzo IP, che deve corrispondere a quello di hello del Server Azure multi-Factor Authentication.
* Configurare hello LDAP timeout too30-60 secondi, in modo che vi sia tempo toovalidate hello credenziali con una directory LDAP hello, eseguire una verifica di hello secondo passaggio, ricevere la risposta e rispondere toohello richiesta di accesso LDAP.
* Se si utilizza LDAPS, hello accessorio o un server che esegue query LDAP hello deve considerare attendibile hello certificato SSL installato nel Server Azure multi-Factor Authentication hello.

