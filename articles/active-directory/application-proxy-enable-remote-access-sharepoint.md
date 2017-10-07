---
title: aaaEnable tooSharePoint di accesso remoto con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Sono illustrate hello nozioni fondamentali sul toointegrate un server SharePoint locale con Proxy dell'applicazione AD Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Abilitare accesso remoto tooSharePoint con Proxy dell'applicazione Azure AD

Questo articolo illustra come toointegrate un server SharePoint locale con Proxy dell'applicazione Azure Active Directory (Azure AD).

tooenable tooSharePoint di accesso remoto con Proxy dell'applicazione AD Azure, attenersi alle sezioni di hello in questo articolo passo passo.

## <a name="prerequisites"></a>Prerequisiti

Questo articolo presuppone che SharePoint 2013 o versione successiva sia già installato nell'ambiente. Inoltre, prendere in considerazione hello seguenti prerequisiti:

* SharePoint include il supporto nativo di Kerberos. Di conseguenza, gli utenti che accedono ai siti interni in remoto mediante il Proxy di applicazione Azure AD possono presupporre toohave esperienza single sign-on (SSO).

* È necessario toomake alcuni server di SharePoint tooyour di modifiche configurazione. Si consiglia di usare un ambiente di gestione temporanea. In questo modo, è possibile apportare aggiornamenti tooyour gestione temporanea prima di server e quindi facilitare un ciclo di test prima di passare alla produzione.

* Si presuppone che siano già impostati SSL per SharePoint, in quanto è necessario che SSL in hello pubblicati URL. È necessario toohave che SSL abilitato nel sito interno, tooensure collegamenti inviati/mappati correttamente. Se SSL non è ancora stato configurato, vedere [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) (Configurare SSL per SharePoint 2013) per le necessarie istruzioni. Assicurarsi inoltre che tale hello connettore trust hello certificato del computer che si esegue. (certificato hello non è necessario toobe rilasciato pubblicamente.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Passaggio 1: Configurazione di single sign-on tooSharePoint

I clienti vogliono hello SSO migliore esperienza per le applicazioni back-end, server di SharePoint, in questo caso. In questo scenario comune di Azure AD, hello viene autenticato in una sola volta, perché verrà non richiesto per l'autenticazione nuovamente.

Per le applicazioni locali che richiedono né utilizzano l'autenticazione di Windows, è possibile ottenere SSO utilizzando il protocollo di autenticazione Kerberos hello e una funzionalità denominata la delega vincolata Kerberos (KCD). La delega vincolata Kerberos, quando è configurato, consente a un windows tooobtain connettore Proxy dell'applicazione di hello ticket o un token per un utente, anche se hello utente non ha eseguito l'accesso tooWindows direttamente. toolearn ulteriori informazioni sulla delega vincolata Kerberos, vedere [Panoramica della delega vincolata Kerberos](https://technet.microsoft.com/library/jj553400.aspx).

tooset di delega vincolata Kerberos per un server SharePoint, utilizzare procedure hello hello sequenziale sezioni che seguono:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Verificare che SharePoint sia in esecuzione in un account di servizio

Verificare che SharePoint sia in esecuzione in un account di servizio definito, non in un sistema locale, un servizio locale o un servizio di rete. A tale scopo, in modo che è possibile collegare l'account del servizio (SPN) di nomi dell'entità tooa valido. I nomi SPN sono il modo in cui il protocollo Kerberos hello identifica diversi servizi. E si sarà necessario hello account successive tooconfigure hello la delega vincolata Kerberos.

tooensure i siti in esecuzione in un account di servizio definito, eseguire hello alla procedura seguente:

1. Aprire hello **Amministrazione centrale SharePoint 2013** sito.
2. Andare troppo**sicurezza** e selezionare **Configura account di servizio**.
3. Selezionare **Pool di applicazioni Web - SharePoint - 80**. opzioni di Hello potrebbero essere leggermente diverse in base al nome del pool di web hello o se hello pool web utilizza SSL per impostazione predefinita.

  ![Opzioni per la configurazione di un account di servizio](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Se **selezionare un account per questo componente** è **servizio locale** o **servizio di rete**, è necessario un account toocreate. In caso contrario, è terminato e spostare toohello nella sezione successiva.
5. Selezionare **Registra nuovo account gestito**. Dopo aver creato l'account, è necessario impostare **Pool di applicazioni Web** prima di poter usare account hello.

> [!NOTE]
È necessario toohave a precedentemente creato l'account di Azure AD per il servizio di hello. Si consiglia di consentire la modifica automatica della password. Per ulteriori informazioni sul set completo di hello di passaggi e risoluzione dei problemi, vedere [configurare modifica automatica della password in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Configurare SharePoint per Kerberos

Si utilizza la delega vincolata Kerberos tooperform single sign-on toohello server SharePoint e questa procedura funziona solo con Kerberos.

tooconfigure del sito di SharePoint per l'autenticazione Kerberos:

1. Aprire hello **Amministrazione centrale SharePoint 2013** sito.
2. Andare troppo**Application Management**selezionare **Gestisci applicazioni web**e selezionare il sito di SharePoint. In questo esempio si tratta di **SharePoint - 80**.

  ![Selezione di un sito di SharePoint hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Fare clic su **provider di autenticazione** sulla barra degli strumenti hello.
4. In hello **provider di autenticazione** fare clic su **area predefinita** impostazioni hello tooview.
5. In hello **Modifica autenticazione** finestra di dialogo casella, scorrere verso il basso fino a visualizzare **tipi di autenticazione delle attestazioni** e assicurarsi che entrambi **abilitare l'autenticazione di Windows** e  **Autenticazione integrata di Windows** sono selezionati.
6. Nella casella di riepilogo a discesa hello, accertarsi che **negoziazione (Kerberos)** è selezionata.

  ![Finestra di dialogo Modifica autenticazione](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Nella parte inferiore di hello di hello **Modifica autenticazione** la finestra di dialogo, fare clic su **salvare**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Impostare un nome dell'entità servizio per l'account del servizio SharePoint hello

Prima di configurare la delega vincolata Kerberos hello, è necessario tooidentify servizio SharePoint di hello in esecuzione come account del servizio hello che è stato configurato. A questo scopo è necessario impostare un nome di entità servizio (SPN). Per altre informazioni vedere [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx) (Nomi di entità servizio).

formato del nome SPN Hello è:

```
<service class>/<host>:<port>
```

Nel formato del nome SPN hello:

* _classe del servizio_ è un nome univoco per il servizio di hello. Per SharePoint si usa **HTTP**.

* _host_ hello di dominio completo o nome NetBIOS dell'host hello che hello servizio è in esecuzione in. Per un sito di SharePoint, questo testo può essere necessario toobe hello URL del sito di hello, a seconda della versione di hello di IIS che si sta utilizzando.

* La _porta_ è opzionale.

Se il FQDN del server SharePoint hello hello è:

```
sharepoint.demo.o365identity.us
```

Quindi hello SPN è:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

I nomi SPN tooset potrebbe anche essere necessario per specifici siti Web nel server. Per altre informazioni, vedere [Configurare l'autenticazione Kerberos](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Prestare particolare attenzione toohello sezione "Creare nomi dell'entità servizio per le applicazioni Web tramite l'autenticazione Kerberos".

Hello il modo più semplice per è tooset i nomi SPN è formati del nome SPN hello toofollow che potrebbero essere già presenti per i siti. Copiare tali tooregister SPN nell'account di servizio hello. toodo questo:

1. Visitare il sito di toohello con hello SPN da un altro computer.
 Quando, hello rilevanti dei ticket Kerberos è memorizzato nel computer di hello. Questi ticket contengono hello SPN del sito di destinazione hello che è stato selezionato.

2. È possibile effettuare il pull hello SPN per il sito utilizzando uno strumento denominato [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). In una finestra di comando che è in esecuzione in hello stesso contesto utente hello che eseguono il sito a cui si accede hello nel browser hello, hello il comando seguente:
```
Klist
```
Klist restituisce quindi il set di hello di nomi SPN di destinazione. In questo esempio, il valore di hello evidenziato è hello SPN che è necessario:

  ![Risultati Klist di esempio](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Dopo aver creato hello SPN, è necessario assicurarsi che sia configurata correttamente nell'account di servizio hello impostati per un'applicazione web hello in precedenza toomake. Eseguire hello comando seguente dal prompt dei comandi di hello come un amministratore del dominio hello:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Questo comando imposta hello SPN per il servizio SharePoint hello account in esecuzione come _demo\sp_svc_.

 Sostituire _http/sharepoint.demo.o365identity.us_ con hello SPN per il server e _demo\sp_svc_ con account del servizio hello nell'ambiente in uso. comando di Setspn Hello Cerca hello SPN prima viene aggiunto. In questo caso è possibile che venga restituito un errore di **valore SPN duplicato**. Se viene visualizzato questo errore, assicurarsi che il valore di hello è associato l'account del servizio hello.

È possibile verificare tale hello che SPN è stato aggiunto tramite il comando di Setspn hello con l'opzione -l hello. toolearn informazioni su questo comando, vedere [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Verificare che tale connettore hello è impostato come tooSharePoint un delegato attendibile

Configurare la delega vincolata Kerberos hello in modo che servizio Proxy di applicazione AD Azure hello può delegare servizio SharePoint di toohello identità utente. Eseguita abilitando connettore Proxy dell'applicazione hello tooretrieve i ticket Kerberos per gli utenti autenticati in Azure AD. Quindi che il server passa in questo caso l'applicazione di destinazione hello contesto toohello o SharePoint.

hello tooconfigure la delega vincolata Kerberos, ripetizione hello alla procedura seguente per ogni computer del connettore:

1. Accedere come un tooa di amministratore di dominio controller di dominio e quindi aprire **Active Directory Users and Computers**.
2. Trovare hello che hello connettore del computer. In questo esempio è hello stesso server SharePoint.
3. Fare doppio clic sul computer hello e quindi fare clic su hello **delega** scheda.
4. Verificare che le impostazioni di delega hello siano impostate troppo**computer attendibile per la delega toohello specificato solo servizi**, quindi selezionare **utilizza un qualsiasi protocollo di autenticazione**.

  ![Impostazioni di delega](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Fare clic su hello **Aggiungi** fare clic su **utenti o computer**e individuare l'account del servizio hello.

  ![Aggiunta di hello SPN per l'account del servizio hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Nell'elenco di nomi SPN hello selezionare hello uno creato in precedenza per l'account del servizio hello.
7. Fare clic su **OK**. Fare clic su **OK** nuovamente le modifiche di hello toosave.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Passaggio 2: Abilitare l'accesso remoto tooSharePoint

Dopo aver abilitato SharePoint per Kerberos e configurare la delega vincolata Kerberos, si è pronti tooset backup tooSharePoint servizio single sign-on. Quindi dal connettore hello, è possibile pubblicare la farm di SharePoint hello per l'accesso remoto mediante il Proxy di applicazione AD Azure.

hello tooperform seguendo la procedura, è necessario toobe un membro del ruolo amministratore globale di hello nell'account Azure Active Directory dell'organizzazione.

1. Accedi toohello [portale di Azure](https://manage.windowsazure.com) e trovare il tenant di Azure AD.
2. Fare clic su **Applicazioni** e quindi su **Aggiungi**.
3. Selezionare **Pubblica un'applicazione che sarà accessibile dall'esterno della rete**. Se questa opzione non è visualizzata, verificare che sia Azure AD Basic o Premium impostare nel tenant di hello.
4. Completare ciascuna delle opzioni di hello come segue:
 * **Nome**: qualsiasi valore desiderato, ad esempio **SharePoint**.
 * **URL interno**: hello URL del sito di SharePoint hello internamente, ad esempio **https://SharePoint/**. In questo esempio, assicurarsi che toouse **https**.
 * **Metodo di autenticazione preliminare**: selezionare **Azure Active Directory**.

  ![Opzioni per l'aggiunta di un'applicazione](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Dopo la pubblicazione di app hello, fare clic su hello **configura** scheda.
6. Scorrere verso il basso opzione toohello **la conversione dell'URL nelle intestazioni**. valore predefinito di Hello è **Sì**. Modificarlo troppo**n**.

 SharePoint utilizza hello _intestazione Host_ toolook valore sito hello. e, in base a questo valore, genera i collegamenti. Hello risultato finale è che un collegamento che genera l'errore SharePoint sia un URL pubblicato che sia impostato correttamente l'URL esterno di hello toouse toomake. Impostazione valore hello troppo**Sì** anche Abilita hello un'applicazione connettore tooforward hello richiesta toohello back-end. Tuttavia, impostando il valore di hello troppo**n** significa che hello connettore non invia il nome host interno hello. Al contrario, il connettore di hello invia intestazione host hello come hello pubblicato l'applicazione di back-end toohello URL.

 Inoltre, tooensure che SharePoint accetta questo URL, è necessario toocomplete una configurazione di più server SharePoint hello. Operazione che dovrà essere eseguita nella sezione successiva hello.

7. Modifica **metodo di autenticazione interno** troppo**autenticazione integrata di Windows**. Se il tenant di Azure AD Usa un UPN nel cloud hello è diversa da hello UPN locale, tenere presente tooupdate **delega di identità di account di accesso** anche.
8. Impostare **SPN applicazione interna** toohello valore impostato in precedenza. ad esempio **http/sharepoint.demo.o365identity.us**.
9. Assegnare tooyour applicazione hello gli utenti di destinazione.

L'applicazione dovrebbe essere simile toohello esempio seguente:

  ![Applicazione finita](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Passaggio 3: Verificare che SharePoint conosce URL esterno hello

L'ultimo passaggio tooensure SharePoint grado di individuare il sito di hello basato su URL esterno hello, in modo che esegue il rendering di collegamenti in base a tale URL esterno. Questo scopo è la configurazione di mapping di accesso alternativo per il sito di SharePoint hello.

1. Aprire hello **Amministrazione centrale SharePoint 2013** sito.
2. In **Impostazioni di sistema** selezionare **Configura mapping di accesso alternativo**.

 Verrà visualizzata hello **mapping di accesso alternativo** casella.

  ![Casella Mapping di accesso alternativo](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Nell'elenco a discesa hello accanto a **insieme di Mapping di accesso alternativo**selezionare **modifica Mapping insieme di accesso alternativo**.
4. Selezionare il sito, ad esempio **SharePoint - 80**.

  ![Selezione di un sito](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. È possibile scegliere tooadd hello pubblicato URL come URL interno o un URL pubblico. Questo esempio viene utilizzato un URL pubblico come hello extranet.
6. Fare clic su **Modifica URL pubblici** in hello **Extranet** percorso, quindi immettere il percorso di hello per hello pubblicata l'applicazione, come indicato al passaggio precedente hello. Ad esempio: **https://sharepoint-iddemo.msappproxy.net**.

  ![Immettere un percorso di hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Fare clic su **Salva**.

 È ora possibile accedere a un sito di SharePoint hello esternamente tramite Proxy di applicazione di Azure AD.

## <a name="next-steps"></a>Passaggi successivi

- [Come tooprovide proteggere l'accesso remoto applicazioni tooon locali](active-directory-application-proxy-get-started.md)
- [Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md)
- [Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/) (Pubblicazione su SharePoint 2016 e Office Online Server con il proxy di applicazione Azure AD)
