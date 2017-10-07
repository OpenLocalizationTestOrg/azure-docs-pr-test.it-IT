---
title: aaaCreate servizi BizTalk di Azure nel portale di Azure hello | Documenti Microsoft
description: Informazioni su come tooprovision oppure creare servizi BizTalk di Azure nel portale di Azure; hello MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Creazione di servizi di BizTalk tramite hello portale di Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign in toohello portale di Azure, è necessario un account Azure e una sottoscrizione di Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Vedere [Versione di valutazione gratuita di Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Creare un servizio BizTalk
A seconda della versione scelta hello, non tutte le impostazioni di BizTalk Service potrebbero essere disponibili.

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Nel riquadro di spostamento inferiore hello, selezionare **NEW**:  
   ![Selezionare nuovo pulsante hello][NEWButton]
3. Selezionare **SERVIZI APP** > **SERVIZIO BIZTALK** > **CREAZIONE PERSONALIZZATA**:  
   ![Selezionare BizTalk Service e quindi Custom Create][NewBizTalkService]
4. Immettere le impostazioni del servizio BizTalk hello:
   
    <table border="1">
    <tr>
    <td><strong>Nome del servizio BizTalk</strong></td>
    <td>È possibile inserire qualsiasi nome, ma deve essere specifico. Di seguito sono riportati alcuni esempi:<br/><br/>
    <em>azienda</em>.biztalk.windows.net<br/>
    <em>aziendaapplicazione</em>.biztalk.windows.net<br/>
    <em>applicazione</em>.biztalk.windows.net<br/><br/>". <yourbiztalkservicename>.BizTalk.Windows.NET" è aggiunto automaticamente toohello nome immesso. Crea un URL che viene utilizzato tooaccess il BizTalk del servizio, ad esempio <strong>https://<em>myapplication</em>. <yourbiztalkservicename>.BizTalk.Windows.NET</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Edizione</strong></td>
    <td>Se si è in fase di test/sviluppo hello, scegliere <strong>Developer</strong>. Se si è in fase di produzione hello, utilizzare hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">servizi BizTalk: grafico edizioni</a> toodetermine se <strong>Premium</strong>, <strong>Standard</strong>, o <strong>Basic</strong>hello scelta corretta per lo scenario aziendale.
    </td>
    </tr>
    <tr>
    <td><strong>Area</strong></td>
    <td>Selezionare hello area geografica toohost il BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>URL del dominio</strong></td>
    <td><strong>Facoltativo</strong>. Per impostazione predefinita, è l'URL del dominio hello <em>Nomeserviziobiztalk</em>. <yourbiztalkservicename>.BizTalk.Windows.NET. È anche possibile specificare un dominio personalizzato. Se ad esempio il dominio è <em>contoso</em>, è possibile immettere: <br/><br/>
    <em>Azienda</em>.contoso.com<br/>
    <em>AziendaApplicazione</em>.contoso.com<br/>
    <em>Applicazione</em>.contoso.com<br/>
    <em>NomeServizioBizTalk</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Selezionare sulla freccia avanti hello.
5. Immettere hello archiviazione e le impostazioni del Database:  <table border="1">
    <tr>
    <td><strong>Account di archiviazione di monitoraggio/archiviazione</strong></td>
    <td>Selezionare un account di archiviazione esistente o crearne uno nuovo. <br/><br/>Se si crea un nuovo account di archiviazione, immettere hello <strong>nome Account di archiviazione</strong>.</td>
    </tr>
    <tr>
    <td><strong>Database di rilevamento</strong></td>
    <td>Se si usa un database SQL di Azure esistente, non potrà essere usato da un altro servizio BizTalk. È necessario il nome di account di accesso hello e una password immesse al momento della creazione di Server di Database SQL Azure.<br/><br/><strong>Suggerimento</strong> Crea database di rilevamento hello e account di archiviazione di monitoraggio/archiviazione in hello stessa area come hello BizTalk Service.</td>
    </tr>
    </table>
Selezionare sulla freccia avanti hello.
6. Immettere le impostazioni del Database hello:  <table border="1">
    <tr>
    <td><strong>Nome</strong></td>
    <td>Disponibile quando <strong>creare una nuova istanza di Database SQL</strong> è selezionata nella schermata precedente hello.
    <br/><br/>
Immettere un toobe Nome Database SQL utilizzato per il BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Server</strong></td>
    <td>Disponibile quando <strong>creare una nuova istanza di Database SQL</strong> è selezionata nella schermata precedente hello.
    <br/><br/>
Selezionare un server di database SQL esistente o crearne uno nuovo.</td>
    </tr>
    <tr>
    <td><strong>Nome account di accesso del server</strong></td>
    <td>Immettere nome utente account di accesso di hello.</td>
    </tr>
    <tr>
    <td><strong>Password di accesso server</strong></td>
    <td>Immettere la password di accesso hello.</td>
    </tr>
    <tr>
    <td><strong>Area</strong></td>
    <td>Disponibile quando è stata selezionata l'opzione <strong>Crea nuova istanza di database SQL</strong>. Selezionare hello area geografica toohost il Database SQL.</td>
    </tr>
    </table>

Selezionare hello segno di spunta toocomplete hello guidata. viene visualizzata l'icona di stato di avanzamento Hello:  
![Icona di avanzamento visualizzata al termine][ProgressComplete]

Al termine, hello servizio BizTalk di Azure viene creato e pronto per le applicazioni. le impostazioni predefinite di Hello sono sufficienti. Se si desiderano toochange le impostazioni predefinite di hello, selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare il BizTalk Service. Vengono visualizzate le impostazioni aggiuntive in hello [schede Dashboard, Monitor e Scale](biztalk-dashboard-monitor-scale-tabs.md) nella parte superiore di hello.

A seconda dello stato hello di hello BizTalk Service, esistono alcune operazioni non possono essere completate. Per un elenco di queste operazioni, andare troppo[grafico dello stato di servizi BizTalk](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Passaggi di post-provisioning
* [Installare il certificato di hello in un computer locale](#InstallCert)
* [Aggiungere un certificato per l'ambiente di produzione](#AddCert)
* [Ottenere lo spazio dei nomi di controllo di accesso hello](#ACS)

#### <a name="InstallCert"></a>Installare il certificato di hello in un computer locale
Come parte del provisioning del servizio BizTalk, un certificato autofirmato viene creato e associato alla sottoscrizione del servizio BizTalk. È necessario scaricare il certificato e installarlo nel computer in cui si distribuiscono applicazioni BizTalk Service o invia messaggi tooa endpoint BizTalk Service.

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare la sottoscrizione di BizTalk Service.
3. Seleziona hello **Dashboard** scheda.
4. Selezionare **Scarica certificato SSL**:  
   ![Modificare un certificato SSL][QuickGlance]
5. Fare doppio clic sul certificato hello ed eseguire certificato hello tooinstall di hello procedura guidata. Assicurarsi di installare il certificato di hello in hello **autorità di certificazione radice attendibili** archiviare.

#### <a name="AddCert"></a>Aggiungere un certificato per l'ambiente di produzione
certificato autofirmato Hello che viene creato automaticamente quando la creazione di servizi BizTalk è destinata solo negli ambienti di sviluppo. Per gli scenari di produzione, è necessario sostituirlo con un certificato di produzione.

1. In hello **Dashboard** , selezionare **certificato SSL di aggiornamento**.
2. Selezionare il certificato SSL privato di tooyour (*CertificateName*con estensione pfx) che include il nome di BizTalk Service, immettere la password di hello e quindi fare clic su hello segno di spunta.

#### <a name="ACS"></a>Ottenere lo spazio dei nomi di controllo di accesso hello
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare il BizTalk Service.
3. Nella barra delle applicazioni hello, selezionare **informazioni di connessione**:  
   ![Selezionare Connection Information][ACSConnectInfo]
4. Copiare i valori di controllo di accesso hello.

Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi. spazio dei nomi controllo di accesso di Hello viene creato automaticamente per il BizTalk Service.

i valori di controllo di accesso Hello è utilizzabile con qualsiasi applicazione. Creazione di servizi BizTalk di Azure, questo spazio dei nomi di controllo di accesso controlla autenticazione hello con la distribuzione di BizTalk Service. Se si desidera toochange hello sottoscrizione o la gestione dello spazio dei nomi hello, selezionare **ACTIVE DIRECTORY** in hello riquadro di spostamento a sinistra e quindi selezionare lo spazio dei nomi. barra delle applicazioni Hello Elenca le opzioni.

Fare clic su **Gestisci** apre hello portale di gestione di controllo di accesso. Nel portale di gestione di controllo di accesso hello, hello utilizza BizTalk Service **identità del servizio**:  
![Identità del servizio ACS nel portale di gestione di controllo di accesso hello][ACSServiceIdentities]

Hello identità del servizio controllo di accesso è un insieme di credenziali che consentono alle applicazioni o client tooauthenticate direttamente con il controllo di accesso e di ricevere un token.

> [!IMPORTANT]
> Usa Hello BizTalk Service **proprietario** per identità di servizio predefinita hello e hello **Password** valore. Se si utilizza il valore di chiave simmetrica hello anziché hello valore della Password, hello può verificarsi.<br/><br/>*Impossibile connettersi account servizio di gestione di controllo di accesso toohello hello specificato credenziali*
> 
> 

[Gestione dello spazio dei nomi del servizio di controllo di accesso](https://msdn.microsoft.com/library/azure/hh674478.aspx) sono fornite alcune linee guida e consigli utili.

## <a name="requirements-explained"></a>Descrizione dei requisiti
Questi requisiti si applicano toohello edizione gratuita.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Elementi necessari</strong></td>
        <td><strong>Perché sono necessari</strong></td>
</tr>
<tr>
<td>Sottoscrizione di Azure</td>
<td>sottoscrizione Hello determina chi può accedere toohello portale di Azure. titolare dell'Account Hello Crea sottoscrizione hello <a HREF="https://account.windowsazure.com/Subscriptions"> sottoscrizioni Azure</a>.
<br/><br/>
Hello account Azure può disporre di più sottoscrizioni e può essere gestito da chiunque è consentito. Ad esempio, il titolare dell'account di Azure crea una sottoscrizione denominata <em>BizTalkServiceSubscription</em> e offre hello amministratori BizTalk all'interno dell'azienda (ad esempio, ContosoBTSAdmins@live.com) accesso toothis sottoscrizione. In questo scenario, gli amministratori BizTalk hello Accedi toohello portale di Azure e sono servizi del hello ospitato tooall diritti di amministratore completi nella sottoscrizione di hello, inclusi servizi BizTalk di Azure. gli amministratori di BizTalk Hello non sono titolari dell'account Azure hello e pertanto non hanno accesso le informazioni di fatturazione tooany.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gestire le sottoscrizioni e gli account di archiviazione nel portale di Azure hello</a> vengono fornite ulteriori informazioni.
</td>
</tr>
<tr>
<td>Database SQL di Azure</td>
<td>Archivia hello tabelle, viste e stored procedure utilizzate da BizTalk Service, inclusi i dati di rilevamento hello hello.
<br/><br/>
Quando si crea un servizio BizTalk, è possibile usare un server di Azure SQL o un database SQL di Azure esistente oppure creare automaticamente un nuovo server o database.
<br/><br/>
Hello scalabilità del Database SQL viene configurato automaticamente. In genere, la scala predefinita hello è sufficiente per un BizTalk Service. Modifica scala hello ha un impatto sui prezzi. Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Account e fatturazione nel database SQL di Azure</a>
<br/><br/>
<strong>Note</strong>
<br/>
<ul>
<li> Quando si crea un nuovo server SQL di Azure e un nuovo database, Servizi di Azure viene abilitato automaticamente. Hello BizTalk Service richiede servizi di Azure essere abilitato.</li>
<li>Se si crea un nuovo Database SQL di Azure in un Server SQL Azure esistente, hello regole del firewall di hello Server non vengono modificati. Di conseguenza, è possibile che altri servizi di Azure non sono consentiti i database del Server di accesso toohello.</li>
</ul>
</td>
</tr>
<tr>
<td>Spazio dei nomi del servizio di controllo di accesso di Azure</td>
<td>Consente di eseguire l'autenticazione con Servizi BizTalk di Azure. Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi. Quando si crea un BizTalk Service, lo spazio dei nomi di controllo di accesso hello viene creato automaticamente.</td>
</tr>

<tr>
<td>Account di archiviazione di Azure</td>
<td>Consente di accedere a tootables, BLOB e code usate con i seguenti hello toosave di BizTalk Service:

<ul>
<li>File di log che hello monitoraggio BizTalk Service. monitoraggio di output di Hello viene visualizzato anche nella hello **monitoraggio** scheda hello portale di Azure.</li>
<li>Quando si crea un X12 o AS2 accordo tra partner, è possibile abilitare la proprietà messaggio hello archiviazione funzionalità toostore. Questi dati vengono salvati in hello account di archiviazione.</li>
</ul>
<br/>
Quando si crea un servizio BizTalk, è possibile usare un account di archiviazione esistente o crearne automaticamente uno nuovo.
<br/><br/>
le impostazioni di archiviazione di Hello predefinite sono sufficienti per un BizTalk Service.
<br/><br/>
Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria. Queste chiavi controllano accesso tooyour account di archiviazione. Hello BizTalk Service utilizza automaticamente hello chiave primaria.
<br/><br/>
Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Archiviazione</a> per altre informazioni.
</td>
</tr>

<tr>
<td>Certificato SSL privato</td>
<td>
Quando si crea un servizio BizTalk di Azure, viene creato anche un URL HTTPS che include il nome del servizio BizTalk. Questo URL è toouse configurato automaticamente un certificato autofirmato solo allo sviluppo. Per l'ambiente di produzione, è necessario un certificato SSL privato.
<br/><br/>
<strong>Informazioni importanti sul certificato SSL</strong>

<ul>
<li>Data di scadenza certificato Hello deve essere inferiore ai 5 anni.</li>
<li>Tutti i certificati privati richiedono una password. Non dimenticare la password e, come procedura consigliata, condividerla con gli amministratori.</li>
<li>I certificati autofirmati possono essere utilizzati in ambienti di sviluppo/test. Quando si utilizzano certificati autofirmati, importare l'archivio certificati personali di hello certificati tooyour e hello archivio certificati Autorità di certificazione radice attendibili.</li>
</ul>
<br/>Quando si invia l'autorità di certificazione tooyour richiesta certificato produzione hello, assegnare hello seguenti proprietà certificato:
<br/>

<ul>
<li><strong>Utilizzo chiavi avanzato</strong>. Servizi BizTalk di Azure richiede almeno l'autenticazione server.</li>
<li><strong>Nome comune</strong>: immettere il nome di dominio completo hello (FQDN) dell'URL di servizio BizTalk di Azure. Vedere <a HREF="#CreateService">Creare un servizio BizTalk</a> in questo articolo.</li>
</ul>
<br/>
È possibile aggiungere un certificato nuovo o diverso dopo hello BizTalk Service viene creato.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>connessioni ibride
Quando si crea un servizio BizTalk di Azure, hello **connessioni ibride** scheda è disponibile:

![scheda per le connessioni ibride][HybridConnectionTab]

Le connessioni ibride sono usate tooconnect di Azure del sito Web tooany servizio mobile di Azure in locale o risorse che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP, servizi mobili e la maggior parte dei servizi Web personalizzati.  Le connessioni ibride e hello servizio Adapter BizTalk sono diversi. Hello servizio Adapter BizTalk è il sistema Line-of-Business (LOB) locale di tooconnect utilizzati servizi BizTalk di Azure tooan.

 Vedere [connessioni ibride](integration-hybrid-connection-overview.md) toolearn altre, incluse la creazione e gestione delle connessioni ibride.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un BizTalk Service, acquisire familiarità con diversi hello [servizi BizTalk: schede Dashboard, Monitor e Scale](biztalk-dashboard-monitor-scale-tabs.md). Il servizio BizTalk è pronto per le applicazioni. creazione di applicazioni, andare troppo toostart[servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Vedere anche
* [Servizi BizTalk: tabella delle edizioni](biztalk-editions-feature-chart.md)<br/>
* [Servizi BizTalk: Tabella degli stati del servizio](biztalk-service-state-chart.md)<br/>
* [Servizi BizTalk: backup e ripristino](biztalk-backup-restore.md)<br/>
* [Servizi BizTalk: limitazione](biztalk-throttling-thresholds.md)<br/>
* [Servizi BizTalk: nome e chiave dell'autorità emittente](biztalk-issuer-name-issuer-key.md)<br/>
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Connessioni ibride](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
