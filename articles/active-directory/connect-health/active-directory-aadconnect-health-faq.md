---
title: aaaAzure Active Directory Connect Health domande frequenti - Azure | Documenti Microsoft
description: "Di seguito sono elencate le domande frequenti e le relative risposte su Azure AD Connect Health. Queste domande frequenti sono contenute le informazioni sull'utilizzo del servizio di hello, tra cui hello fatturazione modello, funzionalità, limitazioni e supporto."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Domande frequenti su Azure AD Connect Health
In questo articolo vengono fornite le risposte toofrequently domande frequenti (FAQ) sullo stato di connessione di Azure Active Directory (Azure AD). Queste domande frequenti riguardano domande su come toouse hello servizio, che include hello modello, funzionalità, limitazioni e supporto di fatturazione.

## <a name="general-questions"></a>Domande generali
**D: Quando si gestiscono più directory di Azure AD, Come passare toohello uno con Azure Active Directory Premium?**

tooswitch tra diversi Azure AD i tenant, seleziona hello attualmente firmato aggiuntivo **nome utente** via hello angolo superiore destro e quindi scegliere account appropriato hello. Se l'account di hello non è elencato qui, selezionare **Disconnetti**, e quindi utilizza le credenziali di amministratore globale di hello della directory hello con Azure Active Directory Premium abilitato toosign in.

**D: Quali versioni dei ruoli di identità sono supportate da Azure AD Connect Health?**

Hello nella tabella seguente sono elencati i ruoli di hello e le versioni del sistema operativo supportate.

|Ruolo| Sistema operativo/Versione|
|--|--|
|Active Directory Federation Services (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Versione 1.0.9125 o successiva|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Si noti che le funzionalità di hello fornite dal servizio hello possono variare in base ruolo hello e del sistema operativo hello. In altre parole, tutte le funzionalità di hello potrebbero non essere disponibile per tutte le versioni del sistema operativo. Descrizioni delle funzionalità di hello per informazioni dettagliate, vedere.

**D: come numero di licenze si devo toomonitor dell'infrastruttura?**

* Hello prima Connect Health Agent richiede almeno una licenza di Azure AD Premium.
* Ogni agente registrato successivamente richiede altre 25 licenze Azure AD Premium.
* Numero di agenti è equivalente toohello il numero totale di agenti che sono registrati in tutti i ruoli monitorati (AD FS, Azure AD Connect e/o dominio Active Directory).

Informazioni sulle licenze sono inoltre disponibili in hello [pagina dei prezzi di Azure AD](https://aka.ms/aadpricing).

Esempio:

| Agenti registrati | Licenze necessarie | Esempio di configurazione di monitoraggio |
| ------ | --------------- | --- |
| 1 | 1 | 1 server di Azure AD Connect |
| 2 | 26| 1 server di Azure AD Connect e 1 controller di dominio |
| 3 | 51 | 1 server di Active Directory Federation Services (AD FS), 1 proxy di AD FS e 1 controller di dominio |
| 4 | 76 | 1 server di AD FS, 1 proxy di AD FS e 2 controller di dominio |
| 5 | 101 | 1 server di Azure AD Connect, 1 server di AD FS, 1 proxy di AD FS e 2 controller di dominio |


## <a name="installation-questions"></a>Domande sull'installazione

**D: qual è l'impatto di hello dell'installazione di Azure AD Connect Health Agent hello nei singoli server?**

Hello impatto dell'installazione di server di proxy applicazione web Microsoft Azure AD Connect Health Agent, AD FS, hello, i server di Azure AD Connect (sincronizzazione), i controller di dominio è minimo con riguardo toohello CPU, utilizzo della memoria, larghezza di banda di rete e archiviazione.

Hello dopo i numeri è un'approssimazione:

* Utilizzo della CPU: ~1-5% di incremento.
* Utilizzo della memoria: % too10 hello totale di memoria di sistema.

> [!NOTE]
> Se l'agente hello non può comunicare con Azure, agente hello archivia i dati di hello in locale per un limite massimo definito. agente Hello sovrascrive hello "memorizzato nella cache" dati "serviti meno di recente".
>
>

* Archiviazione buffer locale per gli agenti di Azure AD Connect Health: ~20 MB.
* Per i server ADFS, è consigliabile che si esegua il provisioning uno spazio su disco pari a 1024 MB (1 GB) per il canale di controllo hello ADFS di Azure Active Directory gli agenti Connect Health tooprocess tutti i dati di controllo di hello prima che vengano sovrascritti.

**D: ho tooreboot my Server durante l'installazione di hello degli agenti hello Azure AD Connect Health?**

No. installazione di Hello degli agenti di hello non richiederanno tooreboot hello il server. Installazione di alcuni passaggi potrebbe tuttavia richiedere il riavvio del server di hello.

In Windows Server 2008 R2, ad esempio, l'installazione di .NET 4.5 Framework richiede un riavvio del server.

**D: Il servizio Azure AD Connect Health usa un proxy HTTP pass-through?**

Sì. Per le operazioni in corso, è possibile configurare hello integrità agente toouse richieste HTTP in uscita un HTTP proxy tooforward.
Per altre informazioni, vedere la [configurazione del proxy HTTP per gli agenti per l'integrità](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Se è necessario un proxy tooconfigure durante la registrazione dell'agente, potrebbe essere toomodify le impostazioni Proxy di Internet Explorer in anticipo.

1. Aprire Internet Explorer > **Impostazioni** > **Opzioni Internet** > **Connessioni** > **Impostazioni LAN**.
2. Selezionare **Usa un server di proxy per la rete LAN**.
3. Selezionare **Avanzate** se sono presenti porte proxy diverse per HTTP e HTTPS/Protetto.

**Q: esegue l'autenticazione di base di supporto di Azure AD Connect Health quando la connessione proxy tooHTTP?**

No. Un meccanismo toospecify un nome utente non autorizzato e la password per l'autenticazione di base non è attualmente supportato.

**D: le porte del firewall che cosa è necessario tooopen per hello Azure AD Connect Health Agent toowork?**

Vedere hello [sezione Requisiti](active-directory-aadconnect-health-agent-install.md#requirements) per elenco hello delle porte del firewall e altri requisiti di connettività.

**D: perché è non vengono visualizzati due server con stesso nome nel portale di hello Azure AD Connect Health hello?**

Quando si rimuove un agente da un server, server hello non viene rimosso automaticamente dal portale di Azure AD Connect Health hello. Se si rimuove un agente da un server o rimuovere manualmente server hello stesso, è necessario toomanually voce server hello di eliminazione dal portale di hello Azure AD Connect Health.

È possibile ricreare l'immagine di un server o creare un nuovo server con hello stessi dettagli (ad esempio nome del computer). Server già registrati hello non è stato rimosso dal portale di hello Azure AD Connect Health, se è installato l'agente di hello nel nuovo server hello, si possono essere visualizzate due voci con hello stesso nome.

In questo caso, è possibile eliminare manualmente voce hello appartenente toohello precedente server. dati Hello per questo server devono essere aggiornati.

## <a name="health-agent-registration-and-data-freshness"></a>Registrazione dell'agente per l'integrità e aggiornamento dati

**D: quali sono i motivi comuni per gli errori di registrazione dell'agente di integrità di hello e come risolvere i problemi?**

Hello Agente integrità sistema può non riuscire tooregister scadenza toohello seguenti cause:

* agente Hello non può comunicare con gli endpoint hello richiesto perché un firewall sta bloccando il traffico. Questa situazione è molto comune nei server proxy applicazione Web. Assicurarsi di aver abilitato le porte e gli endpoint necessario toohello le comunicazioni in uscita. Vedere hello [sezione Requisiti](active-directory-aadconnect-health-agent-install.md#requirements) per informazioni dettagliate.
* Le comunicazioni in uscita sono ispezione SSL tooan sottoposti dal livello di rete hello. In questo modo certificato hello agente hello utilizza toobe sostituiti da entità/server hello ispezione e la registrazione dell'agente hello toocomplete hello passaggi esito negativo.
* utente Hello non dispone di accesso tooperform hello registrazione dell'agente di hello. Per impostazione predefinita, agli amministratori globali l'accesso è consentito. È possibile utilizzare [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate accesso tooother gli utenti.

**D: Sto recupero avvisato che "servizio integrità dati non sono backup toodate." Come risolvere il problema di hello?**

Azure AD Connect Health Genera avviso di hello quando non riceve tutti i punti dati hello dal server hello in hello ultime due ore. I motivi per cui questo avviso viene generato possono essere diversi.

* agente Hello non può comunicare con gli endpoint hello richiesto perché un firewall sta bloccando il traffico. Questa situazione è molto comune nei server proxy applicazione Web. Assicurarsi di aver abilitato le comunicazioni in uscita toohello necessario punti di fine e le porte. Vedere hello [sezione Requisiti](active-directory-aadconnect-health-agent-install.md#requirements) per informazioni dettagliate.
* Le comunicazioni in uscita sono ispezione SSL tooan sottoposti dal livello di rete hello. In questo modo certificato hello agente hello utilizza toobe sostituiti da entità/server hello ispezione e il processo di hello ha esito negativo del servizio di Azure AD Connect Health tooupload dati toohello.
* È possibile utilizzare il comando di connettività hello compilato nell'agente hello. [Altre informazioni](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* gli agenti di Hello supportano inoltre la connettività in uscita tramite un HTTP Proxy non autenticati. [Altre informazioni](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Domande sulle operazioni
**D: è necessario tooenable controllo nei server proxy applicazione web di hello?**

No, il controllo non è necessario toobe abilitato nel server proxy applicazione web di hello.

**D: In che modo vengono risolti gli avvisi di Azure AD Connect Health?**

Gli avvisi di Azure AD Connect Health vengono risolti se si verifica una condizione di esito positivo. Azure Active Directory gli agenti Connect Health rilevare e segnalare servizio toohello condizioni di esito positivo hello periodicamente. Per alcuni avvisi, l'eliminazione hello è basato sul tempo. In altre parole, se hello stessa condizione di errore non viene osservata entro 72 ore dalla generazione dell'avviso, hello avviso viene risolto automaticamente.

**D: Sto recupero avvisato che "richiesta di autenticazione di Test (transazione sintetica) non riuscito tooobtain un token." Come risolvere il problema di hello?**

Azure AD Connect Health per AD FS questo avviso viene generato quando hello Health Agent installato in un server AD FS non riesce tooobtain un token come parte di una transazione sintetica avviata da hello Agente integrità sistema. Agente integrità Hello utilizza il contesto di sistema locale hello e prova tooget un token per una relying party self. Si tratta di un test di catch-all di tooensure che ADFS si trova in uno stato di rilascio di token.

Spesso questo test non riesce perché hello integrità agente nome della farm non è possibile tooresolve hello AD FS. Questa situazione può verificarsi se i server ADFS hello Active Directory sono protetti da un bilanciamento del carico di rete e richiesta hello viene avviata da un nodo di bilanciamento del carico hello (come tooa anziché regolare client che si trova davanti al servizio di bilanciamento del carico hello). Può essere risolto aggiornando il file hosts"hello" sotto l'indirizzo IP di "C:\WINDOWS\system32\drivers\etc." tooinclude hello del server AD FS hello o un indirizzo IP di loopback (127.0.0.1) per il nome di farm hello ADFS (ad esempio sts.contoso.com). Aggiunta del file host hello verrà corto circuito di chiamata di rete hello, consentendo in tal modo i token di hello integrità agente tooget hello.

**D: ho ricevuto un messaggio di posta elettronica che indica che il computer non sono corretti per gli attacchi ransomeware recenti hello. Qual è il motivo per cui si riceve tale messaggio di posta elettronica?**

Servizio di Azure AD Connect Health analizzati hello tutte le macchine vengono controllate le patch necessarie hello tooensure sono state installate. gli amministratori tenant toohello è stato inviato da posta elettronica Hello se almeno un computer non dispone di patch critiche hello. Hello seguenti logica è stato utilizzato toomake questa operazione.
1. Trovare tutti gli hotfix hello è installati nel computer di hello.
2. Controllare se almeno uno di hello hotfix da hello definito l'elenco è presente.
3. In caso affermativo, macchina di hello è protetta. In caso contrario, hello macchina è il rischio di attacco hello.

È possibile utilizzare hello tooperform script PowerShell seguente questo controllo manualmente. Implementa hello sopra logica.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Collegamenti correlati
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
