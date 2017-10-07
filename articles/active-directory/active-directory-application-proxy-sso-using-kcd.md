---
title: sign-on aaaSingle con Proxy dell'applicazione | Documenti Microsoft
description: Descrive come tooprovide single sign-on con Proxy dell'applicazione AD Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Delega vincolata Kerberos per le applicazioni single sign-on tooyour con Proxy dell'applicazione

È possibile fornire l'accesso single sign-on per le applicazioni locali pubblicate mediante il proxy di applicazione che sono protette con l'autenticazione integrata di Windows. Queste applicazioni richiedono un ticket Kerberos per l'accesso. Proxy dell'applicazione utilizza la delega vincolata Kerberos (KCD) toosupport queste applicazioni. 

È possibile abilitare single sign-on tooyour applicazioni utilizzando l'autenticazione integrata di Windows (IWA) assegnando autorizzazioni di connettori Proxy di applicazione in Active Directory tooimpersonate users. connettori Hello utilizzano toosend questa autorizzazione e ricevano i token per loro conto.

## <a name="how-single-sign-on-with-kcd-works"></a>Funzionamento di Single Sign-On con KCD
Questo diagramma illustra il flusso di hello quando un utente tenta di tooaccess un'applicazione locale che utilizza l'autenticazione integrata di Windows.

![Diagramma del flusso di autenticazione di Microsoft AAD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. utente Hello entra in un'applicazione hello URL tooaccess hello locale mediante il Proxy di applicazione.
2. Proxy applicazione reindirizza hello richiesta tooAzure AD autenticazione servizi toopreauthenticate. A questo punto, Azure AD applica gli eventuali criteri di autenticazione e autorizzazione appropriati, ad esempio l'autenticazione a più fattori. Se l'utente hello viene convalidata, Azure AD crea un token e lo invia toohello utente.
3. utente Hello passa hello token tooApplication Proxy.
4. Proxy dell'applicazione convalida il token di hello recupera hello del nome dell'entità utente (UPN) da esso e quindi Invia richiesta hello hello UPN e hello del nome dell'entità servizio (SPN) toohello connettore tramite un canale protetto doppiamente autenticato.
5. Hello connettore esegue la negoziazione di delega vincolata Kerberos (KCD) con hello locale AD, rappresentazione hello utente tooget un'applicazione toohello token Kerberos.
6. Active Directory invia il token Kerberos hello per toohello applicazione hello connettore.
7. Hello connettore invia hello originale richiesta toohello server applicazioni, utilizzando token Kerberos hello ricevuto da Active Directory.
8. un'applicazione Hello invia hello risposta toohello connettore, che viene quindi restituito al servizio Proxy applicazione toohello e infine toohello utente.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare a usare single sign-on per applicazioni di autenticazione integrata di Windows, assicurarsi che l'ambiente è pronto con hello seguenti configurazioni e impostazioni:

* Le app come App Web di SharePoint, vengono impostate toouse autenticazione integrata di Windows. Per altre informazioni, vedere [Attivare il supporto per l'autenticazione Kerberos](https://technet.microsoft.com/library/dd759186.aspx). Per SharePoint, vedere [Pianificare l'autenticazione Kerberos in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Tutte le app devono avere [nomi delle entità servizio](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* in esecuzione sul server Hello: hello connettore e server hello esecuzione applicazione hello vengono aggiunti a un dominio e parte di hello stesso dominio o in domini trusting. Per ulteriori informazioni sull'aggiunta a un dominio, vedere [partecipare a un dominio di tooa Computer](https://technet.microsoft.com/library/dd807102.aspx).
* server Hello in esecuzione hello connettore ha attributo hello TokenGroupsGlobalAndUniversal tooread di accesso per gli utenti. Questa impostazione potrebbe sono stata influita dall'ambiente hello di protezione.

### <a name="configure-active-directory"></a>Configurare Active Directory
configurazione di Active Directory Hello varia a seconda che il connettore Proxy dell'applicazione e il server di applicazioni hello vengano hello nello stesso dominio o non.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Connettore e server applicazioni in hello nello stesso dominio
1. In Active Directory passare troppo**strumenti** > **utenti e computer**.
2. Selezionare hello server che esegue il connettore di hello.
3. Fare clic con il pulsante destro del mouse su **Proprietà** > **Delega**.
4. Selezionare **computer attendibile per i servizi solo di delega toospecified**. 
5. In **toowhich servizi questo account può presentare credenziali delegate** aggiungere valore hello per un'identità SPN del server applicazioni hello hello. Ciò consente agli utenti di tooimpersonate connettore Proxy dell'applicazione di hello in Active Directory in base ad applicazioni hello definite nell'elenco di hello.

   ![Schermata della finestra delle proprietà per Connector-SVR](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Connettore e server applicazione in domini differenti
1. Per un elenco dei prerequisiti necessari per usare la delega vincolata Kerberos tra domini, vedere [Delega vincolata Kerberos tra domini](https://technet.microsoft.com/library/hh831477.aspx).
2. Hello utilizzare `principalsallowedtodelegateto` proprietà hello connettore server tooenable hello Proxy dell'applicazione toodelegate per i server del connettore hello. server applicazioni Hello è `sharepointserviceaccount` e hello delega server `connectormachineaccount`. Per Windows 2012 R2, usare questo codice come esempio:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

È possibile Sharepointserviceaccount account di computer SPS hello o un account di servizio quali hello SPS pool di applicazioni per l'esecuzione.

## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On 
1. Pubblicare l'applicazione in base a istruzioni toohello [pubblicare applicazioni con Proxy dell'applicazione](application-proxy-publish-azure-portal.md). Verificare che tooselect **Azure Active Directory** come hello **metodo di preautenticazione**.
2. Dopo l'applicazione viene visualizzata nell'elenco di hello di applicazioni aziendali, selezionarla e fare clic su **Single sign-on**.
3. Impostare modalità hello single sign-on troppo**autenticazione integrata di Windows**.  
4. Immettere hello **SPN applicazione interna** hello server delle applicazioni. In questo esempio, hello SPN per l'applicazione pubblicata è http/www.contoso.com. Questo toobe esigenze SPN nell'elenco di hello del connettore di servizi toowhich hello può presentare credenziali delegate. 
5. Scegliere hello **delega di identità di account di accesso** per hello connettore toouse per conto degli utenti. Per altre informazioni, vedere [Utilizzo dell'accesso Single Sign-On quando le identità cloud e locali non sono identiche](#Working-with-different-on-premises-and-cloud-identities)

   ![Configurazione avanzata dell'applicazione](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Accesso Single Sign-On per app non Windows
Hello flusso delega Kerberos nel Proxy dell'applicazione Azure Active Directory viene avviata quando Azure AD autentica l'utente hello nel cloud hello. Una volta richiesta hello arriva in locale, hello connector rilascia un ticket Kerberos per conto di utente hello interagendo con un Proxy di applicazione AD Azure hello Active Directory locale. Questo processo è noto tooas delega vincolata Kerberos (KCD). In hello fase successiva, viene inviata una richiesta applicazione back-end toohello con il ticket Kerberos. Esistono diversi protocolli che definiscono come toosend tali richieste. La maggior parte dei server non Windows prevede l'uso del protocollo Negotiate/SPNego, al momento supportato nel proxy di applicazione di Azure AD.

Per ulteriori informazioni su Kerberos, vedere [si desidera tooknow sulla delega vincolata Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Le app non Windows usano generalmente nomi utente o nomi account SAM invece di indirizzi e-mail di dominio. Se questa situazione si applica tooyour applicazioni, è necessario tooconfigure hello delegato accesso identità campo tooconnect delle identità di applicazione tooyour identità cloud. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Utilizzo dell'accesso Single Sign-On quando le identità cloud e locali non sono identiche
Proxy dell'applicazione si presuppone che gli utenti abbiano esattamente hello stessa identità cloud hello e locale. Se non è questo caso di hello, può comunque utilizzare la delega vincolata Kerberos per single sign-on. Configurare un **delega di identità di account di accesso** per ogni applicazione toospecify identità deve essere utilizzato quando si esegue l'accesso single sign-on.  

Questa funzionalità consente di molte organizzazioni che dispone di diversi in locale e cloud identità toohave SSO da app di hello cloud tooon locale senza richiedere hello utenti tooenter diversi Gestione nomi utente e password. Sono incluse organizzazioni che:

* Sono disponibili più domini internamente (joe@us.contoso.com, joe@eu.contoso.com) e un singolo dominio nel cloud hello (joe@contoso.com).
* Dispone di nome di dominio non instradabile internamente (joe@contoso.usa) e una persona nel cloud hello.
* Non usano nomi di dominio internamente (joe).
* Utilizzare alias diversi locale e nel cloud hello. Ad esempio, joe-johns@contoso.com e joej@contoso.com  

Con Proxy dell'applicazione, è possibile selezionare quali hello tooobtain toouse di identità ticket Kerberos. Questa impostazione viene configurata per ogni applicazione. Alcune di queste opzioni sono appropriate per i sistemi che non accettano il formato di indirizzo di posta elettronica, altre sono concepite per l'accesso alternativo.

![Schermata del parametro dell'identità di accesso delegata](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Se viene utilizzata l'identità di accesso delegato, hello valore potrebbe non essere univoco in tutti i domini hello o foreste dell'organizzazione. Per evitare questo problema, pubblicare queste applicazioni due volte usando due gruppi di connettori diversi. Poiché ogni applicazione dispone di un gruppo di destinatari di un utente diverso, è possibile aggiungere il dominio di connettori tooa diverso.

### <a name="configure-sso-for-different-identities"></a>Configurare Single Sign-On per diverse identità
1. Configurare le impostazioni di Azure AD Connect in modo identità principale hello è l'indirizzo di posta elettronica hello (posta elettronica). Questa operazione viene eseguita come parte di hello personalizzarlo, modificando hello **nome entità utente** campo nelle impostazioni di sincronizzazione hello. Queste impostazioni determinano inoltre come gli utenti accedono tooOffice365, Windows10 dispositivi e altre applicazioni che usano Azure AD come archivio identità.  
   ![Schermata di identificazione degli utenti - Elenco a discesa Nome dell'entità utente](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Nelle impostazioni di configurazione dell'applicazione hello per un'applicazione hello desideri toomodify, seleziona hello **delega di identità di account di accesso** toobe utilizzato:

   * Nome dell'entità utente (ad esempio joe@contoso.com)
   * Nome alternativo dell'entità utente (ad esempio joed@contoso.local)
   * Parte del nome utente del nome dell'entità utente (ad esempio joe)
   * Parte del nome utente del nome alternativo dell'entità utente (ad esempio joe)
   * Nome dell'account SAM locale (dipende dalla configurazione del controller di dominio hello)

### <a name="troubleshooting-sso-for-different-identities"></a>Risoluzione dei problemi di accesso Single Sign-On per diverse identità
Se si verifica un errore nel processo SSO hello, viene visualizzato nel registro eventi di hello connettore macchina come spiegato in [risoluzione dei problemi](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Tuttavia, in alcuni casi, hello richiesta viene inviata applicazione back-end toohello mentre l'applicazione risponde in varie altre risposte HTTP. Risoluzione dei problemi di questi casi è consigliabile iniziare esaminando il numero di eventi 24029 computer connettore hello nel registro eventi di sessione Proxy dell'applicazione hello. identità dell'utente Hello utilizzata per la delega viene visualizzato nel campo "user" hello all'interno di dettagli sull'evento hello. tooturn nel log di sessione, selezionare **Mostra analitica e registri di debug** nel menu Visualizza di Visualizzatore eventi hello.

## <a name="next-steps"></a>Passaggi successivi

* [Come tooconfigure un toouse applicazione Proxy dell'applicazione la delega vincolata Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Risolvere i problemi che si verificano con il proxy di applicazione](active-directory-application-proxy-troubleshoot.md)


Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)

