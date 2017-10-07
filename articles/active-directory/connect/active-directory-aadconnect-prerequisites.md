---
title: 'Azure AD Connect: Prerequisiti e hardware | Microsoft Docs'
description: In questo argomento vengono descritti i prerequisiti hello hello requisiti hardware e per Azure AD Connect
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Prerequisiti di Azure AD Connect
Questo argomento descrive i prerequisiti hello hello requisiti hardware e per Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Prima di installare Azure AD Connect
Prima di installare Azure AD Connect, sono necessari alcuni elementi.

### <a name="azure-ad"></a>Azure AD
* Sottoscrizione di Azure o [sottoscrizione di una versione di valutazione di Azure](https://azure.microsoft.com/pricing/free-trial/). Questa sottoscrizione è solo necessario per l'accesso a hello portale di Azure e non per l'utilizzo di Azure AD Connect. Se si utilizza PowerShell o Office 365, non è necessario un toouse sottoscrizione di Azure, Azure AD Connect. Se si dispone di una licenza di Office 365, è possibile utilizzare il portale di Office 365 hello. Con una licenza di Office 365 a pagamento, è inoltre possibile ottenere in hello portale di Azure dal portale di Office 365 hello.
  * È inoltre possibile utilizzare hello [portale di Azure](https://portal.azure.com). che non richiede una licenza di Azure AD.
* [Aggiungere e verificare il dominio hello](../active-directory-domains-add-azure-portal.md) toouse si prevede di Azure AD. Ad esempio, se si prevede contoso.com toouse per gli utenti, assicurarsi che questo dominio è stato verificato e non si usa solo dominio predefinito di hello contoso.onmicrosoft.com.
* Per impostazione predefinita, in un tenant di Azure AD sono consentiti 50.000 oggetti. Quando si verifica il dominio, il limite di hello è oggetti too300k maggiore. Se è necessario anche più oggetti in Azure AD, è necessario tooopen aumentato ancor di più di un limite di hello toohave case di supporto. Se sono necessari più di 500.000 oggetti, allora occorre una licenza, ad esempio Office 365, Azure AD Basic, Azure AD Premium o Enterprise Mobility and Security.

### <a name="prepare-your-on-premises-data"></a>Preparare i dati locali
* Utilizzare [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify errori, ad esempio i duplicati e problemi di formattazione della directory prima di sincronizzare tooAzure AD e Office 365.
* Esaminare le [funzionalità di sincronizzazione facoltative che è possibile abilitare in Azure AD](active-directory-aadconnectsyncservice-features.md) e valutare quali funzionalità abilitare.

### <a name="on-premises-active-directory"></a>Active Directory locale
* livello di funzionalità di Hello Active Directory schema versione e della foresta deve essere Windows Server 2003 o versione successiva. i controller di dominio Hello possono eseguire qualsiasi versione, purché siano soddisfatti i requisiti livello hello dello schema e della foresta.
* Se si prevede funzionalità hello toouse **writeback delle password**, hello i controller di dominio deve essere in Windows Server 2008 (con Service Pack più recente) o versioni successive. Se i controller di dominio sono nella versione 2008, precedente a R2, è necessario applicare anche l'[hotfix KB2386717](http://support.microsoft.com/kb/2386717).
* il controller di dominio Hello usato da Azure AD deve essere accessibile in scrittura. È **non supportato** toouse un controller di dominio (controller di dominio di sola lettura) e Azure AD Connect non è conforme a ogni scrittura reindirizzamenti.
* È **non supportato** toouse foreste o domini locali con i domini (domini con etichetta singola).
* È **non supportato** toouse foreste o domini locali tramite "puntata" (nome contiene un punto ".") Nomi NetBios.
* È consigliabile troppo[abilitare il Cestino di Active Directory hello](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Server di Azure AD Connect
* Azure AD Connect non può essere installato su Small Business Server o Windows Server Essentials. server Hello devono utilizzare Windows Server standard o superiore.
* server di Hello Azure AD Connect deve avere un'interfaccia utente grafica completa installata. È **non supportato** tooinstall in server core.
* Azure AD Connect deve essere installato in Windows Server 2008 o versione successiva. Questo server può essere un controller di dominio o un server membro, se si usano le impostazioni rapide. Se si utilizzano le impostazioni personalizzate, server hello può anche essere autonomi e non dispone di toobe tooa aggiunti a un dominio.
* Se si installa Azure AD Connect in Windows Server 2008 o Windows Server 2008 R2, verificare che tooapply hello aggiornamenti rapidi più recenti da Windows Update. installazione di Hello non è in grado di toostart con un server senza patch.
* Se si prevede funzionalità hello toouse **la sincronizzazione delle password**, quindi è necessario hello Azure AD Connect server in Windows Server 2008 R2 SP1 o versioni successive.
* Se si prevede di toouse un **account del servizio gestito di gruppo**, quindi è necessario hello Azure AD Connect server in Windows Server 2012 o versioni successive.
* Hello Azure AD Connect server deve disporre di [.NET Framework 4.5.1](#component-prerequisites) o versione successiva e [Microsoft PowerShell 3.0](#component-prerequisites) installato o versione successiva.
* server di Azure AD Connect Hello non deve avere criteri di gruppo trascrizione PowerShell abilitato.
* Se viene distribuito Active Directory Federation Services server hello in cui sono installati ADFS o Proxy applicazione Web deve essere Windows Server 2012 R2 o versioni successive. [Gestione remota Windows](#windows-remote-management) .
* Se viene distribuito Active Directory Federation Services, sono necessari i [Certificati SSL](#ssl-certificate-requirements).
* Se viene distribuito Active Directory Federation Services, quindi è necessario tooconfigure [la risoluzione dei nomi](#name-resolution-for-federation-servers).
* Se gli amministratori globali dispongono di autenticazione a più fattori abilitata, quindi hello URL **https://secure.aadcdn.microsoftonline-p.com** deve essere presente nell'elenco siti attendibili di hello. Si è richiesta tooadd questo elenco siti attendibili toohello sito quando viene richiesto per una richiesta di autenticazione a più fattori e non è aggiunto prima. È possibile utilizzare Internet Explorer tooadd è tooyour siti attendibili.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server usato da Azure AD Connect
* Azure AD Connect richiede un Server SQL database toostore identità dei dati. Per impostazione predefinita viene installato SQL Server 2012 Express LocalDB (una versione ridotta di SQL Server Express). SQL Server Express è un limite di dimensioni di 10GB che consente di toomanage circa 100.000 oggetti. Se è necessario toomanage un volume maggiore di oggetti directory, è necessario toopoint hello installazione guidata tooa installazione diversa di SQL Server.
* Se si usa un SQL Server separato, si applicano questi requisiti:
  * Azure AD Connect supporta tutte le versioni di Microsoft SQL Server da SQL Server 2008 (con Service Pack più recente) tooSQL Server 2016 SP1. Il database SQL di Microsoft Azure **non è supportato** come database.
  * È necessario usare regole di confronto SQL senza distinzione tra maiuscole e minuscole. Queste regole di confronto sono identificate da \_CI_ all'interno del nome. È **non supportato** toouse le regole di confronto tra maiuscole e minuscole, identificato da \_cs nel nome.
  * È possibile avere un unico motore di sincronizzazione per istanza SQL. È **non supportato** tooshare SQL dell'istanza con Azure AD Sync, DirSync o FIM o MIM sincronizzazione.

### <a name="accounts"></a>Account
* Un account di amministratore globale di Azure Active Directory per il tenant di Azure AD hello desiderato toointegrate con. Questo account deve essere un **account aziendale o dell'istituto di istruzione** e non un **account Microsoft**.
* Se si usano le impostazioni rapide o si esegue l'aggiornamento da DirSync, è necessario disporre di un account di amministratore dell'organizzazione per il servizio Active Directory locale.
* [Account in Active Directory](active-directory-aadconnect-accounts-permissions.md) se si utilizza il percorso di installazione di hello impostazioni personalizzate.

### <a name="connectivity"></a>Connettività
* server di Hello Azure AD Connect deve risoluzione DNS per internet e intranet. Hello server DNS deve essere in grado di tooresolve i nomi degli endpoint di Azure AD Active Directory e hello tooyour in locale.
* Se sono presenti firewall sulla rete Intranet ed è necessario tooopen porte tra il server di connessione hello Azure AD e i controller di dominio, vedere [Azure AD Connect porte](active-directory-aadconnect-ports.md) per ulteriori informazioni.
* Se il limite di proxy o firewall che gli URL accessibili, quindi hello documentato nell'URL [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) deve essere aperto.
  * Se si utilizza hello Cloud Microsoft in Germania e hello cloud di Microsoft Azure per enti pubblici, quindi vedere [istanze del servizio di sincronizzazione di Azure AD Connect considerazioni](active-directory-aadconnect-instances.md) per gli URL.
* Azure AD Connect è per impostazione predefinita utilizzando toocommunicate TLS 1.0 con Azure AD. È possibile modificare questo tooTLS 1.2 seguendo procedure hello [abilitare TLS 1.2 per Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Se si utilizza un proxy in uscita per la connessione Internet toohello, hello dopo l'impostazione di hello **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** file devono essere aggiunti per l'installazione guidata di hello e Azure AD Connect sincronizzazione toobe tooconnect in grado di toohello Internet e Azure AD. Questo testo deve essere immesso nella parte inferiore di hello del file hello. In questo codice, &lt;PROXYADRESS&gt; rappresenta hello nome host o indirizzo IP proxy effettivo.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Se il server proxy richiede l'autenticazione, hello [account del servizio](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) deve trovarsi in hello dominio ed è necessario utilizzare hello personalizzata impostazioni installazione percorso toospecify un [account del servizio personalizzato](active-directory-aadconnect-get-started-custom.md#install-required-components). È inoltre necessario toomachine.config una modifica diversa. Con questa modifica in Machine. config, motore di sincronizzazione e di creazione guidata di installazione hello rispondere tooauthentication richieste dal server proxy hello. In tutte le pagine della procedura guidata di installazione, escludendo hello **configura** pagina hello effettuato l'accesso dell'utente vengono utilizzate le credenziali. In hello **configura** pagina alla fine di hello hello dell'installazione guidata di, il contesto di hello viene switch toohello [account del servizio](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) creato dall'utente. sezione di Hello Machine. config dovrebbe essere simile al seguente.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Quando Azure AD Connect invia un tooAzure richiesta web Active Directory come parte della sincronizzazione della directory, Azure AD può richiedere too5 minuti toorespond. È comune per la configurazione del proxy server toohave connessione timeout di inattività. Verificare la configurazione di hello prevede tooat almeno 6 minuti o più.

Per ulteriori informazioni, vedere MSDN sull'hello [proxy elemento predefinito](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Per altre informazioni in caso di problemi di connettività, vedere [Risolvere i problemi di connettività](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Altre
* Facoltativo: Un test utente tooverify la sincronizzazione degli account.

## <a name="component-prerequisites"></a>Prerequisiti dei componenti
### <a name="powershell-and-net-framework"></a>PowerShell e .Net Framework
Azure AD Connect si basa su Microsoft PowerShell e .NET Framework 4.5.1. Nel server deve essere installata questa versione o una versione successiva. A seconda della versione di Windows Server, hello seguenti:

* Windows Server 2012 R2
  * Microsoft PowerShell viene installato per impostazione predefinita, non è necessaria alcuna azione.
  * .NET Framework 4.5.1 e versioni successive sono disponibili tramite Windows Update. Verificare che è stato installato tooWindows gli aggiornamenti più recenti di hello Server hello Pannello di controllo.
* Windows Server 2008 R2 e Windows Server 2012
  * versione più recente di Hello di PowerShell di Microsoft è disponibile in **Windows Management Framework 4.0**, disponibile su [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 e versioni successive sono disponibili nell' [Area download Microsoft](http://www.microsoft.com/downloads).
* Windows Server 2008
  * è disponibile nella versione di Hello supportata più recente di PowerShell **Windows Management Framework 3.0**, disponibile su [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 e versioni successive sono disponibili nell' [Area download Microsoft](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Abilitare TLS 1.2 per Azure AD Connect
Azure AD Connect utilizza TLS 1.0 per impostazione predefinita per la crittografia delle comunicazioni hello tra server del motore di sincronizzazione hello e Azure AD. È possibile modificare questo configurare .net applicazioni toouse TLS 1.2 per impostazione predefinita nei server hello. Altre informazioni su TLS 1.2 sono disponibili nell'articolo [Advisory Microsoft sulla sicurezza 2960358](https://technet.microsoft.com/security/advisory/2960358).

1. Non è possibile abilitare TLS 1.2 in Windows Server 2008. È necessario Windows Server 2008 R2 o una versione successiva. Assicurarsi di disporre di hotfix di .net 4.5.1 hello installato per il sistema operativo, vedere [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358). Questo hotfix o una versione successiva potrebbe essere già installata nel server.
2. Se si usa Windows Server 2008 R2, verificare che TLS 1.2 sia abilitato. In Windows Server 2012 e versioni successive, TLS 1.2 dovrebbe essere già abilitato.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Per tutti i sistemi operativi, impostare questa chiave del Registro di sistema e riavviare il server di hello.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Se si desidera anche tooenable TLS 1.2 tra server del motore di sincronizzazione hello e un Server SQL remoto, quindi verificare che si dispone di versioni di hello necessario installate per [il supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Prerequisiti per l'installazione e la configurazione dei servizi federativi
### <a name="windows-remote-management"></a>Gestione remota Windows
Quando si utilizza Azure AD Connect toodeploy Active Directory Federation Services o hello Proxy applicazione Web, verificare i requisiti seguenti:

* Se il server di destinazione hello è aggiunto a un dominio, quindi verificare che Windows di gestito remoto sia abilitato
  * In una finestra di comando PSH con privilegi elevati, utilizzare il comando `Enable-PSRemoting –force`
* Se il server di destinazione hello è aggiunto a un dominio di non-machine WAP, quindi esistono alcuni requisiti aggiuntivi
  * Nel computer di destinazione hello (macchina WAP):
    * Assicurarsi di hello winrm (gestione remota Windows / WS-Management) servizio è in esecuzione tramite lo snap-in servizi di hello
    * In una finestra di comando PSH con privilegi elevati, utilizzare il comando `Enable-PSRemoting –force`
  * Nel computer di hello in cui hello procedura guidata è in esecuzione (se il computer di destinazione hello non di dominio non trusted o aggiunti a un dominio):
    * In una finestra di comando PSH con privilegi elevata, utilizzare il comando di hello`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * In Server Manager:
      * aggiungere il pool di toomachine DMZ WAP host (server manager -> Gestisci -> Aggiungi server... utilizzare la scheda DNS)
      * Scheda Server Manager tutti i server: fare clic con il pulsante destro server WAP e scegliere l'account di gestione, immettere le credenziali locali (non di dominio) per la macchina WAP hello
      * toovalidate PSH connettività remota, nella scheda Server Manager tutti i server hello: fare clic con il pulsante destro server WAP e scegliere di Windows PowerShell. Apre una sessione remota di PSH sia possibile stabilire sessioni di PowerShell remote tooensure.

### <a name="ssl-certificate-requirements"></a>Requisiti dei certificati SSL
* È consigliabile toouse hello stesso certificato SSL in tutti i nodi della farm AD FS e tutti i server proxy applicazione Web.
* certificato di Hello deve essere un X509 certificato.
* È possibile utilizzare un certificato autofirmato su server federativi in un ambiente di testing. Tuttavia, per un ambiente di produzione, è consigliabile che il certificato hello da una CA pubblica.
  * Se si utilizza un certificato non attendibile pubblicamente, verificare che tale certificato hello installato in ogni server Proxy applicazione Web è attendibile sia server locali hello e in tutti i server federativi
* identità di Hello del certificato hello deve corrispondere (ad esempio, sts.contoso.com) nome del servizio federativo hello.
  * identità di Hello è un'estensione di nome alternativo oggetto (SAN) dell'oggetto di tipo dNSName oppure, se non sono presenti voci SAN, il nome di soggetto hello specificato come un nome comune.  
  * Più voci SAN possono essere presente nel certificato hello, purché una di esse corrisponda nome del servizio federativo hello.
  * Se si intende toouse alla rete aziendale, aggiuntivi è necessario un valore di hello **enterpriseregistration.** seguito dal suffisso del nome dell'entità utente (UPN) hello dell'organizzazione, ad esempio, **enterpriseregistration.contoso.com**.
* I certificati basati su chiavi CNG (CryptoAPI next generation) chiavi e i provider di archiviazione chiavi non sono supportati. Ciò significa che è necessario utilizzare un certificato basato su un provider del servizio di crittografia e non su un provider di archiviazione chiavi.
* I certificati con caratteri jolly sono supportati.

### <a name="name-resolution-for-federation-servers"></a>Risoluzione dei nomi per i server federativi
* Impostare i record DNS per hello Nome servizio federativo di ADFS (ad esempio sts.contoso.com) per hello extranet (DNS pubblico tramite registrar di dominio) e hello intranet (server DNS interno). Per i record DNS intranet di hello, assicurarsi di usare un record e non i record CNAME. È necessario per windows autenticazione toowork correttamente da computer aggiunti a un dominio.
* Se si intende distribuire più server AD FS o un server Proxy applicazione Web, assicurarsi di aver configurato il servizio di bilanciamento del carico e che i record DNS hello hello AD FS federation service (ad esempio sts.contoso.com) Nome punto toohello bilanciamento del carico.
* Per toowork l'autenticazione integrata di windows per le applicazioni browser con Internet Explorer in intranet, verificare che hello Nome servizio federativo di ADFS (ad esempio sts.contoso.com) sia aggiunto toohello l'area intranet in Internet Explorer. Questo può essere controllato tramite criteri di gruppo e distribuito tooall computer aggiunti al dominio.

## <a name="azure-ad-connect-supporting-components"></a>Componenti di supporto di Azure AD Connect
Hello seguito è riportato un elenco di componenti che consente di installare Azure AD Connect nel server di hello in cui è installato Azure AD Connect. L'elenco riguarda un'istallazione di SQL Express di base. Se si sceglie toouse un altro Server SQL in hello installare pagina Servizi di sincronizzazione, quindi LocalDB di SQL Express non è installato in locale.

* Azure AD Connect Health
* Assistente per l'accesso a Microsoft Online Services per professionisti IT (installato ma senza dipendenze)
* Utilità della riga di comando di Microsoft SQL Server 2012
* Microsoft SQL Server 2012 Express LocalDB
* Client nativo di Microsoft SQL Server 2012
* Microsoft Visual C++ 2013 Redistribution Package

## <a name="hardware-requirements-for-azure-ad-connect"></a>Requisiti hardware per Azure AD Connect
tabella di Hello seguente illustra i requisiti minimi di hello per computer di sincronizzazione di Azure AD Connect hello.

| Numero di oggetti in Active Directory | CPU | Memoria | Dimensioni del disco rigido |
| --- | --- | --- | --- |
| Meno di 10.000 |1,6 GHz |4 GB |70 GB |
| 10.000-50.000 |1,6 GHz |4 GB |70 GB |
| 50.000-100.000 |1,6 GHz |16 GB |100 GB |
| Per 100.000 o più oggetti è necessaria versione completa di hello di SQL Server | | | |
| 100.000-300.000 |1,6 GHz |32 GB |300 GB |
| 300.000-600.000 |1,6 GHz |32 GB |450 GB |
| Più di 600.000 |1,6 GHz |32 GB |500 GB |

requisiti minimi per i computer che esegue AD FS Hello o server applicazioni Web è seguente hello:

* CPU: dual core da 1,6 GHz o superiore
* MEMORIA: 2 GB o superiore
* Macchina virtuale di Azure: configurazione A2 o superiore

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
