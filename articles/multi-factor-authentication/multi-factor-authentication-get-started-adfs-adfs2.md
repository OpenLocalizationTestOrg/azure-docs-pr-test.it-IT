---
title: Azure MFA Server con AD FS 2.0 aaaUse | Documenti Microsoft
description: "Si tratta hello Azure multi-Factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA e AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Configurare il Server Azure multi-Factor Authentication toowork con AD FS 2.0
In questo articolo è per le organizzazioni che sono federate con Azure Active Directory e toosecure risorse che risiedono in locale o nel cloud hello. Proteggere le risorse utilizzando hello del Server Azure multi-Factor Authentication e configurandolo toowork con AD FS in modo che la verifica viene attivata per il punto finale di alto valore.

Questa documentazione viene illustrato l'utilizzo di hello del Server Azure multi-Factor Authentication con AD FS 2.0. Per altre informazioni su AD FS, vedere [Protezione delle risorse cloud e locali tramite il server Azure Multi-Factor Authentication con Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Proteggere ADFS 2.0 con un proxy
toosecure AD FS 2.0 con un proxy, installare hello del Server Azure multi-Factor Authentication nel server proxy di hello AD FS.

### <a name="configure-iis-authentication"></a>Configurare l'autenticazione IIS
1. In hello del Server Azure multi-Factor Authentication, fare clic su hello **autenticazione IIS** icona nel menu a sinistra di hello.
2. Fare clic su hello **basata su Form** scheda.
3. Fare clic su **Aggiungi**.

   <center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. le variabili nome utente, password e dominio toodetect automaticamente, immettere l'URL di accesso hello (ad esempio https://sso.contoso.com/adfs/ls) nella finestra di dialogo Configura automaticamente sito Web di hello e fare clic su **OK**.
5. Controllare hello **corrispondenza utente richiedono Azure multi-Factor Authentication** se tutti gli utenti sono stati o verranno importati in hello Server e verifica tootwo passaggio soggetto. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti da verifica in due passaggi, lasciare deselezionata la casella hello.
6. Se le variabili di pagina hello non possono essere rilevate automaticamente, fare clic su hello **specificare manualmente...** pulsante nella finestra di dialogo Configura automaticamente sito Web di hello.
7. Nella finestra di dialogo Aggiungi sito Web di hello, immettere la pagina accesso hello URL toohello AD FS nel campo URL di invio hello (ad esempio https://sso.contoso.com/adfs/ls) e immettere un nome di applicazione (facoltativo). nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.
8. Impostare il formato di richiesta di hello troppo**POST o GET**.
9. Immettere una variabile di nome utente hello (ctl00$ ContentPlaceHolder1$ UsernameTextBox) e la variabile Password (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Se la pagina di accesso basato su form viene visualizzata una casella di testo di dominio, immettere anche variabili di dominio di hello. nomi di hello toofind delle caselle di input di hello nella pagina di accesso hello, pagina di accesso toohello andare in un web browser, fare doppio clic sulla pagina hello e selezionare **Visualizza origine**.
10. Controllare hello **corrispondenza utente richiedono Azure multi-Factor Authentication** se tutti gli utenti sono stati o verranno importati in hello Server e verifica tootwo passaggio soggetto. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti da verifica in due passaggi, lasciare deselezionata la casella hello.
    <center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Fare clic su **Avanzate** tooreview impostazioni avanzate. Ecco le impostazioni che possono essere configurate:

    - Selezionare un file di paging di rifiuto personalizzato
    - Cache le autenticazioni riuscite toohello sito Web utilizza i cookie
    - Selezionare la modalità tooauthenticate hello credenziali primarie

12. Poiché il server proxy di hello AD FS non è più probabile toobe aggiunti a un dominio toohello, è possibile utilizzare controller di dominio tooyour tooconnect LDAP per pre-autenticazione e l'importazione degli utenti. Nella finestra di dialogo sito Web basato su form avanzato hello, fare clic su hello **autenticazione primaria** e selezionare **binding LDAP** per tipo di autenticazione preautenticazione hello.
13. Al termine, fare clic su **OK** finestra di dialogo Aggiungi sito Web toohello tooreturn.
14. Fare clic su **OK** tooclose hello finestra di dialogo.
15. Una volta hello URL e rilevate o immesse le variabili di pagina, vengono visualizzati dati del sito Web hello in hello pannello basata su Form.
16. Fare clic su hello **modulo nativo** scheda e selezionare hello server, sito Web di hello che proxy ADFS hello Active Directory è in esecuzione in (ad esempio "sito Web predefinito"), o hello AD FS proxy dell'applicazione (ad esempio "ls" in "adfs") tooenable hello plug-in hello IIS livello desiderato.
17. Fare clic su hello **autenticazione IIS abilitare** casella in alto hello hello.

l'autenticazione IIS Hello è ora abilitato.

### <a name="configure-directory-integration"></a>Configurare l'integrazione di directory
È abilitata l'autenticazione di IIS, ma tooperform hello pre-autenticazione tooyour Active Directory (AD) tramite LDAP, è necessario configurare hello controller di dominio toohello connessione LDAP.

1. Fare clic su hello **integrazione Directory** icona.
2. Nella scheda Impostazioni hello selezionare hello **Usa configurazione LDAP specifica** pulsante di opzione.

   <center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Fare clic su **Modifica**.
4. Nella finestra di dialogo Modifica configurazione LDAP hello, popolare i campi di hello con controller di dominio AD toohello hello informazioni tooconnect obbligatorio. Sono incluse le descrizioni dei campi hello hello del Server Azure multi-Factor Authentication file della Guida.
5. Test della connessione LDAP hello facendo hello **Test** pulsante.

   <center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Se il test della connessione LDAP hello ha esito positivo, fare clic su **OK**.

### <a name="configure-company-settings"></a>Configurare le impostazioni aziendali
1. Successivamente, fare clic su hello **impostazioni società** icona e seleziona hello **risoluzione nome utente** scheda.
2. Seleziona hello **attributo dell'identificatore univoco per la corrispondenza dei nomi utente utilizza LDAP** pulsante di opzione.
3. Se gli utenti immettono il proprio nome utente nel formato "dominio\nomeutente", hello Server deve dominio hello toostrip in grado di toobe off hello username durante la creazione di query LDAP hello. Che può essere eseguita tramite un'impostazione del Registro di sistema.
4. Aprire l'editor del Registro di sistema hello e passare tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive reti/PhoneFactor su un server a 64 bit. Se in un server a 32 bit, richiedere hello "Wow6432Node" dal percorso hello. Creare un valore DWORD chiave del Registro di sistema denominata "UsernameCxz_stripPrefixDomain" e impostare too1 valore hello. Proxy AD FS hello è ora protetta da Azure multi-Factor Authentication.

Verificare che gli utenti importati da Active Directory nel Server hello. Vedere hello [sezione indirizzi IP attendibili](#trusted-ips) se si vogliono toowhitelist gli indirizzi IP interni in modo che la verifica non è necessaria quando si accede nel sito Web toohello da tali percorsi.

<center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 diretto senza un proxy
È possibile proteggere ADFS quando non viene utilizzato il proxy di ADFS hello AD. Installare hello del Server Azure multi-Factor Authentication nel server di hello AD FS e configurare hello Server hello seguendo i passaggi:

1. All'interno di hello del Server Azure multi-Factor Authentication, fare clic su hello **autenticazione IIS** icona nel menu a sinistra di hello.
2. Fare clic su hello **HTTP** scheda.
3. Fare clic su **Aggiungi**.
4. Nella finestra di dialogo Aggiungi URL di Base di hello, immettere l'URL hello per sito Web di ADFS in cui viene eseguita l'autenticazione HTTP (ad esempio https://sso.domain.com/adfs/ls/auth/integrated) nel campo URL di Base hello hello. e immettere un nome di applicazione (facoltativo). nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.
5. Se si desidera, regolare il timeout di inattività hello e massimo i tempi di sessione.
6. Controllare hello **corrispondenza utente richiedono Azure multi-Factor Authentication** se tutti gli utenti sono stati o verranno importati in hello Server e verifica tootwo passaggio soggetto. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti da verifica in due passaggi, lasciare deselezionata la casella hello.
7. Hello cookie cache casella di controllo se si desidera.

   <center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Fare clic su **OK**.
9. Fare clic su hello **modulo nativo** scheda e selezionare hello server, hello sito Web (ad esempio "sito Web predefinito") o hello tooenable di applicazione (ad esempio "ls" in "adfs") hello ADFS plug-in hello IIS desiderato livello.
10. Fare clic su hello **autenticazione IIS abilitare** casella in alto hello hello.

AD FS è protetto da Azure Multi-Factor Authentication.

Verificare che gli utenti importati da Active Directory nel Server hello. Vedere hello sezione indirizzi IP attendibili se si desidera IP interno toowhitelist indirizzi in modo che la verifica non è necessaria quando si accede nel sito Web toohello da tali percorsi.

## <a name="trusted-ips"></a>IP attendibili
Indirizzi IP attendibili consente agli utenti toobypass Azure multi-Factor Authentication per le richieste del sito Web provenienti da specifici indirizzi IP o subnet. Ad esempio, si consiglia agli utenti di tooexempt di verifica in due passaggi quando effettuano l'accesso dall'ufficio hello. A tale scopo, è necessario specificare subnet dell'ufficio hello come una voce di indirizzi IP attendibili.

### <a name="tooconfigure-trusted-ips"></a>indirizzi IP attendibili tooconfigure
1. Nella sezione autenticazione IIS hello, fare clic su hello **gli indirizzi IP attendibili** scheda.
2. Fare clic su hello **Aggiungi...** .
3. Quando viene visualizzata la finestra di dialogo di hello aggiungere gli indirizzi IP attendibili, selezionare una delle hello **IP singolo**, **intervallo IP**, o **Subnet** pulsanti di opzione.
4. Immettere l'indirizzo IP hello, intervallo di indirizzi IP o subnet che deve essere abilitata. Se si immette una subnet, selezionare hello appropriato hello subnet mask e fare clic su **OK** pulsante. Hello attendibile che IP è stata aggiunta.

<center>![Configurazione](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
