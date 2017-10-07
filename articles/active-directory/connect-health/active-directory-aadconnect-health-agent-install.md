---
title: installazione di aaaAzure AD Connect Health Agent | Documenti Microsoft
description: Si tratta di pagina di Azure AD Connect Health hello che descrive l'installazione dell'agente hello per AD FS e sincronizzazione.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Installazione dell'agente di Azure AD Connect Health
Questo documento viene descritto come installare e configurare gli agenti hello Azure AD Connect Health. È possibile scaricare gli agenti di hello dalla [qui](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Requisiti
Hello nella tabella seguente è riportato un elenco di requisiti per l'utilizzo di Azure AD Connect Health.

| Requisito | Descrizione |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health è una funzionalità di Azure AD Premium e richiede una licenza di Azure AD Premium. </br></br>Per altre informazioni, vedere [Introduzione ad Azure Active Directory Premium](../active-directory-get-started-premium.md). </br>toostart una valutazione gratuita di 30 giorni, vedere [avviare una versione di valutazione.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| È necessario essere un globale avviata amministratore del tooget di Azure AD con Azure AD Connect Health |Per impostazione predefinita, solo amministratori globali di hello possono installare e configurare hello integrità agenti tooget avviato, portale hello di accesso e qualsiasi operazione all'interno di Azure AD Connect Health. Per altre informazioni, vedere [Amministrare la directory di Azure AD](../active-directory-administer.md). <br><br> Tramite controllo dell'accesso basato su ruoli è possibile consentire accesso tooAzure AD Connect Health tooother utenti nell'organizzazione. Per altre informazioni, vedere l'articolo relativo al [controllo degli accessi in base al ruolo per Azure AD Connect Health.](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) </br></br>**Importante:** hello account utilizzato per l'installazione degli agenti hello deve essere un account aziendale o dell'istituto di istruzione. Non può essere un account Microsoft. Per altre informazioni, vedere [Iscriversi ad Azure come organizzazione](../sign-up-organization.md). |
| L'agente di Azure AD Connect Health è installato in ogni server di destinazione | Azure AD Connect Health richiede hello gli agenti integrità toobe installato e configurato sui dati di hello tooreceive i server di destinazione e fornisce funzionalità di monitoraggio e Analitica hello </br></br>Ad esempio, è necessario installare dati tooget dall'infrastruttura di ADFS, agente hello hello ADFS e server Proxy applicazione Web. Analogamente, tooget dati in locale dell'infrastruttura di dominio Active Directory, hello agente deve essere installato nei controller di dominio hello. </br></br> |
| Endpoint del servizio Azure toohello connettività in uscita | Durante l'installazione e runtime, l'agente hello richiede gli endpoint del servizio di connettività tooAzure AD Connect Health. Se la connettività in uscita viene bloccata tramite firewall, verificare che hello seguenti endpoint vengono aggiunti toohello elenco consentito: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Porta: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Connettività in uscita in base agli indirizzi IP | Per IP basato su indirizzi filtrando i firewall, vedere toohello [intervalli IP Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| L'analisi SSL per il traffico in uscita è filtrata o disabilitata | nel caso di ispezione SSL o la chiusura per il traffico in uscita a livello di rete hello, Hello agente registrazione passaggio o dati operazioni di caricamento potrebbero non riuscire. |
| Porte del firewall nel server di hello esecuzione agente hello. |l'agente Hello richiede hello toobe apra hello agente toocommunicate con gli endpoint del servizio integrità di Azure AD hello porte del firewall seguenti.</br></br><li>Porta TCP 443</li><li>Porta TCP 5671</li> |
| Consenti hello seguenti siti Web se è attivata la protezione avanzata di Internet Explorer |Se è attivata la protezione avanzata di Internet Explorer, quindi hello seguenti siti Web deve essere consentito hello server che è installato l'agente continua toohave hello.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>server federativo di Hello per l'organizzazione ritenuto attendibile da Azure Active Directory. Ad esempio: https://sts.contoso.com</li> |
|Disabilitare FIPS|La funzionalità FIPS non è supportata dagli agenti di Azure AD Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>L'installazione di hello Azure AD Connect Health Agent per AD FS
toostart hello installazione dell'agente, fare doppio clic sul file .exe hello che è stato scaricato. Nella prima schermata hello, fare clic su Installa.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Al termine dell'installazione di hello, fare clic su Configura ora.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Verrà avviato un processo di registrazione agente PowerShell finestra tooinitiate hello. Quando richiesto, accedere con un account di Azure AD che ha accesso tooperform la registrazione dell'agente. Per impostazione predefinita hello account di amministratore globale ha accesso.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Dopo l'accesso, PowerShell continuerà. Una volta che è stata completata, è possibile chiudere PowerShell e hello configurazione è stata completata.

A questo punto, hello agente servizi devono essere avviato automaticamente consentendo hello agente caricamento hello necessario dati toohello servizio cloud in modo sicuro.

Se non sono stati soddisfatti tutti hello prerequisiti descritti nelle sezioni precedenti hello, gli avvisi vengono visualizzati nella finestra di PowerShell hello. Essere certi hello toocomplete [requisiti](active-directory-aadconnect-health-agent-install.md#requirements) prima di installare l'agente di hello. Hello schermata seguente è riportato un esempio di questi errori.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify hello agente è stato installato, cercare i seguenti servizi nel server di hello hello. Se è stata completata la configurazione hello, deve già essere in esecuzione. In caso contrario, vengono arrestati fino al completamento configurazione hello.

* Azure AD Connect Health AD FS Diagnostics Service
* Azure AD Connect Health AD FS Insights Service
* Azure AD Connect Health AD FS Monitoring Service

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Installazione dell'agente in server Windows Server 2008 R2
Procedura per server Windows Server 2008 R2:

1. Verificare che il server hello è in esecuzione al Service Pack 1 o versione successiva.
2. Disattivare la funzionalità Protezione avanzata di IE per l'installazione dell'agente:
3. Installare Windows PowerShell 4.0 su ognuno dei server hello avanti rispetto all'installazione hello Agente integrità sistema di Active Directory. tooinstall Windows PowerShell 4.0:
   * Installare [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) utilizzando hello seguente programma di installazione offline collegamento toodownload hello.
   * Installare PowerShell ISE (da Funzionalità Windows)
   * Installare hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Installare Internet Explorer versione 10 o versione successiva nel server di hello. (Obbligatorio per hello servizio integrità tooauthenticate, utilizzando le credenziali di amministratore di Azure).
4. Per ulteriori informazioni sull'installazione di Windows PowerShell 4.0 in Windows Server 2008 R2, vedere l'articolo di wiki hello [qui](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Abilitare il controllo per AD FS
> [!NOTE]
> In questa sezione si applica solo server tooAD ADFS. Non si dispone toofollow questi passaggi nel server Proxy applicazione Web di hello.
>

Affinché hello Analitica di utilizzo della funzionalità toogather e analizzare i dati, hello agente di Azure AD Connect Health devono hello informazioni nei registri di controllo di hello AD FS. Questi log non sono abilitati per impostazione predefinita. Hello utilizzare dopo il controllo di procedure tooenable AD FS e toolocate hello AD FS dei registri, nei server ADFS.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable controllo per ADFS in Windows Server 2008 R2
1. Fare clic su **avviare**, punto troppo**programmi**, punto troppo**strumenti di amministrazione**, quindi fare clic su **criteri di sicurezza locali**.
2. Passare toohello **gestione della sicurezza sicurezza\Criteri locali\Assegnazione diritti** cartella, quindi fare doppio clic su Genera i controlli di sicurezza.
3. In hello **impostazioni di sicurezza locali** scheda, verificare che sia elencato l'account del servizio hello AD FS 2.0. Se non è presente, fare clic su **Aggiungi utente o gruppo** aggiungerlo toohello elenco e quindi fare clic su **OK**.
4. il controllo tooenable, aprire un prompt dei comandi con privilegi elevati ed eseguire hello comando seguente:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Chiudere Criteri di sicurezza locali e quindi aprire lo snap-in Gestione hello. hello tooopen snap-in Gestione, fare clic su **avviare**, punto troppo**programmi**, punto troppo**strumenti di amministrazione**, quindi fare clic su Active Directory gestione di ADFS 2.0.
6. Nel riquadro azioni hello, fare clic su Modifica proprietà servizio federativo.
7. In hello **proprietà servizio federativo** finestra di dialogo fare clic su hello **eventi** scheda.
8. Seleziona hello **Success audits** e **Failure audits** caselle di controllo.
9. Fare clic su **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable controllo per ADFS in Windows Server 2012 R2
1. Aprire **criteri di sicurezza locali** aprendo **Server Manager** nella schermata Start hello o Server Manager nella barra delle applicazioni hello hello desktop, quindi fare clic su **criteri di sicurezza o locale di strumenti**.
2. Passare toohello **protezione\Criteri Locali\assegnazione diritti** cartella, quindi fare doppio clic **generazione controlli di sicurezza**.
3. In hello **impostazioni di sicurezza locali** scheda, verificare che sia elencato l'account del servizio hello AD FS. Se non è presente, fare clic su **Aggiungi utente o gruppo** aggiungerlo toohello elenco e quindi fare clic su **OK**.
4. il controllo tooenable, di aprire un prompt dei comandi con privilegi elevati ed eseguire hello comando seguente: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Chiudi **criteri di sicurezza locali**e quindi aprire hello **gestione ADFS** snap-in (in Server Manager, fare clic su strumenti e quindi selezionare Gestione di AD FS).
6. Nel riquadro azioni hello, fare clic su **Modifica proprietà servizio federativo**.
7. Nella finestra di dialogo Proprietà servizio federativo hello, fare clic su hello **eventi** scheda.
8. Seleziona hello **operazioni riuscite e Failure audits** caselle di controllo e quindi fare clic su **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable controllo per ADFS in Windows Server 2016
1. Aprire **criteri di sicurezza locali** aprendo **Server Manager** nella schermata Start hello o Server Manager nella barra delle applicazioni hello hello desktop, quindi fare clic su **criteri di sicurezza o locale di strumenti**.
2. Passare toohello **protezione\Criteri Locali\assegnazione diritti** cartella, quindi fare doppio clic **generazione controlli di sicurezza**.
3. In hello **impostazioni di sicurezza locali** scheda, verificare che sia elencato l'account del servizio hello AD FS. Se non è presente, fare clic su **Aggiungi utente o gruppo** aggiungere hello AD FS service account toohello elenco e quindi fare clic su **OK**.
4. il controllo tooenable, aprire un prompt dei comandi con privilegi elevati ed eseguire hello comando seguente:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Chiudi **criteri di sicurezza locali**e quindi aprire hello **gestione ADFS** snap-in (in Server Manager, fare clic su strumenti e quindi selezionare Gestione di AD FS).
6. Nel riquadro azioni hello, fare clic su **Modifica proprietà servizio federativo**.
7. Nella finestra di dialogo Proprietà servizio federativo hello, fare clic su hello **eventi** scheda.
8. Seleziona hello **operazioni riuscite e Failure audits** caselle di controllo e quindi fare clic su **OK**. Questa opzione dovrebbe essere abilitata per impostazione predefinita.
9. Aprire una finestra di PowerShell ed eseguire hello comando seguente: ```Set-AdfsProperties -AuditLevel Verbose```.

Si noti che il livello di controllo "di base" è abilitato per impostazione predefinita. Altre informazioni su hello [funzionalità avanzata di controllo di AD FS in Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>log di controllo toolocate hello AD FS
1. Aprire il **Visualizzatore eventi**.
2. Registri tooWindows scegliere **sicurezza**.
3. Hello destro, scegliere **filtro registro corrente**.
4. In Origine evento selezionare **Controllo di ADFS**.

![Log di controllo di ADFS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Un oggetto Criteri di gruppo può disabilitare il controllo di AD FS. Se il controllo di AD FS è disabilitato, non sono disponibili i dati di analisi di utilizzo relativi alle attività di accesso. Assicurarsi che non sia presente un oggetto Criteri di gruppo che disabilita il controllo di AD FS.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>L'installazione di agente di Azure AD Connect Health hello per la sincronizzazione
agente di Hello Azure AD Connect Health per la sincronizzazione viene installato automaticamente nella build più recente di hello di Azure AD Connect. toouse Azure AD Connect per la sincronizzazione, è necessario toodownload hello più recente di Azure AD Connect e installarlo. È possibile scaricare la versione più recente di hello [qui](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify hello agente è stato installato, cercare i seguenti servizi nel server di hello hello. Se è stata completata la configurazione hello, deve già essere in esecuzione. In caso contrario, vengono arrestati fino al completamento configurazione hello.

* Azure AD Connect Health Sync Insights Service
* Azure AD Connect Health Sync Monitoring Service

![Verificare Azure AD Connect Health per la sincronizzazione](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Si tenga presente che l'utilizzo di integrità di Azure AD Connect richiede Azure AD Premium. Se non si dispone di Azure AD Premium, è Impossibile toocomplete configurazione hello hello portale di Azure. Per ulteriori informazioni, vedere hello [nella pagina requisiti](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Registrazione manuale di Azure AD Connect Health per la sincronizzazione
Se hello Azure AD Connect Health per la registrazione dell'agente di sincronizzazione non riesce dopo l'installazione Azure AD Connect, è possibile utilizzare il comando PowerShell toomanually registrare agente hello seguente hello.

> [!IMPORTANT]
> Tramite questo comando di PowerShell è solo necessario se la registrazione dell'agente hello ha esito negativo dopo l'installazione di Azure AD Connect.
>
>

Hello PowerShell seguente comando è obbligatorio solo quando la registrazione dell'Agente integrità hello ha esito negativo anche dopo una corretta installazione e configurazione di Azure AD Connect. servizi di Azure AD Connect Health Hello verrà avviato al termine della registrazione di agente hello.

È possibile registrare manualmente l'agente di hello Azure AD Connect Health per la sincronizzazione tramite il comando PowerShell seguente hello:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

comando Hello accetta seguenti parametri:

* AttributeFiltering: impostare $true (impostazione predefinita) - se Azure AD Connect non esegue la sincronizzazione hello set di attributi predefiniti e che sia stata toouse personalizzato di un attributo filtrato. $false in caso contrario.
* StagingMode: $false (impostazione predefinita) - se il server di Azure AD Connect hello non è in modalità $true di gestione temporanea se hello server è configurato toobe in modalità di gestione temporanea.

Quando richiesto per l'autenticazione è necessario utilizzare hello stesso account di amministratore globale (ad esempio admin@domain.onmicrosoft.com) che è stato utilizzato per la configurazione di Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>L'installazione di hello Azure AD Connect Health Agent di dominio Active Directory
toostart hello installazione dell'agente, fare doppio clic sul file .exe hello che è stato scaricato. Nella prima schermata hello, fare clic su Installa.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Al termine dell'installazione di hello, fare clic su Configura ora.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Viene avviato un prompt dei comandi seguito da codice PowerShell che esegue Register-AzureADConnectHealthADDSAgent. Quando richiesto toosign in tooAzure, vado Avanti ed eseguire l'accesso.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Dopo l'accesso, PowerShell continuerà. Una volta che è stata completata, è possibile chiudere PowerShell e hello configurazione è stata completata.

A questo punto, i servizi hello devono essere avviati automaticamente consentendo toomonitor agente hello e raccolgono i dati. Se non sono stati soddisfatti tutti hello prerequisiti descritti nelle sezioni precedenti hello, gli avvisi vengono visualizzati nella finestra di PowerShell hello. Essere certi hello toocomplete [requisiti](active-directory-aadconnect-health-agent-install.md#requirements) prima di installare l'agente di hello. Hello schermata seguente è riportato un esempio di questi errori.

![Verificare Azure AD Connect Health per Servizi di dominio Active Directory](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

è stato installato l'agente di hello tooverify, cercare i seguenti servizi del controller di dominio hello hello.

* Azure AD Connect Health AD DS Insights Service
* Azure AD Connect Health AD DS Monitoring Service

Se è stata completata la configurazione hello, questi servizi devono già essere in esecuzione. In caso contrario, vengono arrestati fino al completamento configurazione hello.

![Verificare Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Registrazione dell'agente tramite PowerShell
Dopo aver installato hello agente appropriato setup.exe, è possibile eseguire usando i seguenti comandi di PowerShell in base al ruolo hello hello passaggio di registrazione di hello agente. Aprire una finestra di PowerShell ed eseguire il comando appropriato hello:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Questi comandi accettano "Credential" come una registrazione di hello toocomplete parametro in modo interattivo o in un computer Server Core.
* Hello credenziali può essere acquisito in una variabile di PowerShell che viene passata come parametro.
* È possibile fornire qualsiasi identità di Azure AD che ha accesso tooregister hello agenti e non dispone di autenticazione a più fattori abilitata.
* Per impostazione predefinita, gli amministratori globali hanno accesso tooperform la registrazione dell'agente. È inoltre possibile consentire altri meno identità privilegiate tooperform questo passaggio. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Configurare Azure Active Directory gli agenti Connect Health toouse HTTP Proxy
È possibile configurare Azure Active Directory gli agenti Connect Health toowork con un HTTP Proxy.

> [!NOTE]
> * Utilizzo di "Netsh WinHttp set ProxyServerAddress" non è supportato come agente di hello utilizza le richieste web di System.Net toomake invece di Microsoft Windows HTTP Services.
> * Hello indirizzo Http Proxy configurato è usato toopass-tramite Https messaggi crittografati.
> * I proxy autenticati, che usano HTTPBasic, non sono supportati.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Modificare la configurazione del proxy per l'agente di Health
È necessario hello seguenti opzioni tooconfigure Azure AD Connect Health Agent toouse un HTTP Proxy.

> [!NOTE]
> Tutti i servizi di Azure AD Connect Health Agent devono essere riavviati, affinché toobe le impostazioni di proxy hello aggiornato. Eseguire hello comando seguente:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importare le impostazioni del proxy esistenti
##### <a name="import-from-internet-explorer"></a>Importare da Internet Explorer
Impostazioni del proxy HTTP di Internet Explorer possono essere importati, toobe utilizzati da hello Azure AD Connect integrità degli agenti. In ogni server hello esecuzione hello integrità agente, eseguire hello comando PowerShell seguente:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importare da WinHTTP
Le impostazioni proxy WinHTTP possono essere importate, toobe utilizzati da hello Azure AD Connect integrità degli agenti. In ogni server hello esecuzione hello integrità agente, eseguire hello comando PowerShell seguente:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Specificare gli indirizzi proxy manualmente
È possibile specificare manualmente un server proxy in ogni server hello in esecuzione hello integrità agente, eseguendo il comando PowerShell seguente hello:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Esempio: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*

* "address" può essere un nome di server risolvibile con DNS o un indirizzo IPv4
* "port" può essere omesso. Se omesso, viene scelta la porta 443 come porta predefinita.

#### <a name="clear-existing-proxy-configuration"></a>Cancellare la configurazione del proxy esistente
È possibile deselezionare configurazione proxy esistente hello eseguendo hello comando seguente:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Leggere le impostazioni del proxy correnti
È possibile leggere le impostazioni del proxy attualmente configurato hello eseguendo hello comando seguente:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Testare la connettività tooAzure AD servizio Connect Health
È possibile che possono verificarsi i problemi che causano l'agente di Azure AD Connect Health hello toolose connettività del servizio di hello Azure AD Connect Health. ad esempio problemi di rete, problemi di autorizzazioni o di altro tipo.

Se l'agente di hello è servizio di toosend Impossibile dati toohello Azure AD Connect Health per più di due ore, è indicato con hello seguente avviso nel portale di hello: "servizio integrità dati non sono backup toodate." È possibile verificare se agente di Azure AD Connect Health hello interessato è servizio di tooupload in grado di dati toohello Azure AD Connect Health eseguendo il comando PowerShell seguente hello:

    Test-AzureADConnectHealthConnectivity -Role ADFS

il parametro role Hello accetta attualmente hello seguenti valori:

* AD FS
* Sincronizzazione
* ADDS

È possibile utilizzare flag - ShowResults hello in hello comando tooview dettagliati registri. Utilizzare hello di esempio seguente:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> strumento di connettività hello toouse, è necessario prima registrazione dell'agente hello completo. Se non si è in grado di toocomplete la registrazione dell'agente hello, assicurarsi di aver soddisfatto tutti hello [requisiti](active-directory-aadconnect-health-agent-install.md#requirements) per Azure AD Connect Health. Questo test di connettività viene eseguito per impostazione predefinita durante la registrazione dell'agente.
>
>

## <a name="related-links"></a>Collegamenti correlati
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
