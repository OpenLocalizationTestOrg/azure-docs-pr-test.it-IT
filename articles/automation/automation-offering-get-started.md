---
title: aaa Introduzione all'automazione di Azure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica del servizio di automazione di Azure esaminando i dettagli di progettazione e implementazione di hello hello tooonboard preparazione offerta da Azure Marketplace.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Introduzione ad Automazione di Azure

Questa Guida introduttiva introduce i principali concetti correlati toohello distribuzione di automazione di Azure. Se si tooAutomation nuovo in Azure o si ha esperienza con software per l'automazione del flusso di lavoro come System Center Orchestrator, questa Guida consente di comprendere come tooprepare e automazione onboard.  Successivamente, si verrà preparato toobegin runbook per supportare le esigenze di automazione del processo di sviluppo. 


## <a name="automation-architecture-overview"></a>Panoramica dell'architettura di Automazione

![Panoramica di Automazione di Azure](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Automazione di Azure è un software come un'applicazione di servizio (SaaS) che fornisce un multi-tenant scalabile e affidabile, ambiente tooautomate elabora con i runbook e gestire tooWindows modifiche di configurazione e i sistemi Linux utilizzando Configurazione dello stato desiderato (DSC) in Azure, gli altri servizi cloud o locale. Le entità contenute nell'account di Automazione, ad esempio runbook, asset, account RunAs, sono isolate dagli altri account di Automazione nella propria sottoscrizione e in altre sottoscrizioni.  

I runbook eseguiti in Azure vengono eseguiti nelle sandbox di Automazione, ospitate nelle macchine virtuali della piattaforma distribuita come servizio (PaaS) di Azure.  Le sandbox di Automazione forniscono l'isolamento dei tenant per tutti gli aspetti dell'esecuzione dei runbook: moduli, spazio di archiviazione, memoria, comunicazione di rete, flussi di processo e così via. Questo ruolo viene gestito dal servizio hello e non è accessibile dall'account di Azure o di automazione di Azure per si toocontrol.         

tooautomate hello distribuzione e gestione delle risorse nel data center locale o altri servizi cloud, dopo la creazione di un account di automazione, è possibile designare uno o più hello toorun macchine [ibrida Runbook Worker (HRW)](automation-hybrid-runbook-worker.md) ruolo.  Ogni HRW richiede hello agente di gestione di Microsoft con un'area di lavoro Log Analitica tooa connessione e un account di automazione.  Analitica di log viene utilizzato toobootstrap hello installazione, hello agente di gestione di Microsoft di gestire e monitorare funzionalità hello del hello HRW.  recapito Hello dei runbook e hello toorun di istruzione, che essi vengono eseguiti tramite l'automazione di Azure.

È possibile distribuire più HRW tooprovide disponibilità per i runbook, i processi del runbook bilanciamento di carico e in alcuni casi dedicare li per i carichi di lavoro specifici o in ambienti.  Hello Microsoft Monitoring Agent in hello HRW avvia la comunicazione con il servizio di automazione hello sulla porta TCP 443 e non sono previsti requisiti del firewall in entrata.  Quando si dispone di runbook in esecuzione in un HRW ambiente hello e desiderati hello runbook tooperform le attività di gestione con altri computer o i servizi all'interno di tale ambiente, potrebbero essere altre porte che hello runbook richiede l'accesso a.  Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect la rete Internet, vedere l'articolo di hello [OMS Gateway](../log-analytics/log-analytics-oms-gateway.md), che funge da proxy per hello HRW toocollect allo stato dei processi e ricevere le informazioni di configurazione l'account di automazione.

I runbook in esecuzione in un HRW eseguite nel contesto di hello hello locale dell'account di sistema nel computer di hello, hello consigliata contesto di sicurezza durante l'esecuzione di azioni amministrative nel computer di Windows locale hello. Se si desidera hello runbook toorun attività alle risorse esterne al computer locale hello, potrebbe essere toodefine asset di credenziali protette in account di automazione che è possibile accedere dai runbook hello e utilizzare tooauthenticate con una risorsa esterna hello hello. È possibile utilizzare [credenziali](automation-credentials.md), [certificato](automation-certificates.md), e [connessione](automation-connections.md) asset nel runbook con i cmdlet che consentono di toospecify credenziali in modo da poter autenticare.

Le configurazioni DSC archiviate in automazione di Azure possono essere applicati direttamente tooAzure le macchine virtuali. Altre macchine fisiche e virtuali possono richiedere configurazioni da server di pull DSC di automazione di Azure hello.  Per la gestione delle configurazioni dei locale fisici o virtuali Linux e Windows sistemi, non è necessario toodeploy qualsiasi infrastruttura toosupport hello Automation DSC per server di pull, solo accesso Internet in uscita da ogni toobe sistema gestito da DSC di automazione , la comunicazione per il servizio OMS toohello porta 443 TCP.   

## <a name="prerequisites"></a>Prerequisiti

### <a name="automation-dsc"></a>Automation DSC
DSC di automazione di Azure può essere utilizzato toomanage vari computer:

* Macchine virtuali di Azure (versione classica) che eseguono Windows o Linux
* Macchine virtuali di Azure che eseguono Windows o Linux
* Macchine virtuali di Amazon Web Services (AWS) che eseguono Windows o Linux
* Computer fisici/virtuali Windows locali o in un cloud diverso da Azure o AWS
* Computer fisici/virtuali Linux locali o in un cloud diverso da Azure o AWS

più recente di WMF 5 Hello deve essere installato per l'agente di PowerShell DSC hello per Windows toocommunicate in grado di toobe con automazione di Azure. versione più recente di Hello di hello [agente PowerShell DSC per Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) deve essere installato per toocommunicate in grado di toobe Linux con automazione di Azure.

### <a name="hybrid-runbook-worker"></a>ruolo di lavoro ibrido per runbook  
Durante la definizione di un runbook di ibrida toorun computer i processi, il computer deve avere seguito hello:

* Windows Server 2012 o versioni successive
* Windows PowerShell 4.0 o versioni successive.  Si consiglia di installare Windows PowerShell 5.0 nel computer di hello per aumentare l'affidabilità. È possibile scaricare una nuova versione di hello da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Almeno due core
* Almeno 4 GB di RAM

### <a name="permissions-required-toocreate-automation-account"></a>Account di automazione toocreate necessario disporre di autorizzazioni
toocreate o aggiornamento di un account di automazione, è necessario disporre hello seguenti privilegi specifici e le autorizzazioni necessarie toocomplete in questo argomento.   
 
* In ordine toocreate un account di automazione, l'account utente di Active Directory deve toobe tooa aggiunto ruolo con ruolo di proprietario toohello equivalenti autorizzazioni per le risorse di Microsoft come descritto nell'articolo [controllo di accesso basato sui ruoli in automazione di Azure ](automation-role-based-access-control.md).  
* Se le registrazioni di App hello impostazione è troppo**Sì**, gli utenti senza privilegi di amministratore nel tenant di Azure AD possono [registrare AD applicazioni](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Se le registrazioni di app hello impostazione è troppo**n**, utente hello eseguendo questa azione deve essere un amministratore globale di Azure AD. 

Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di toohello amministratore/coamministratore ruolo globale della sottoscrizione di hello, tooActive Directory aggiunti come guest. In questo caso, viene visualizzato un "non si dispone delle autorizzazioni toocreate..." visualizzazione dell'avviso hello **aggiungere Account di automazione** blade. Gli utenti che sono stati aggiunti toohello amministratore/coamministratore ruolo globale può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake prima li un utente in Active Directory completa. tooverify tale situazione, hello **Azure Active Directory** riquadro nel portale di Azure selezionare hello **utenti e gruppi**selezionare **tutti gli utenti** e, dopo aver selezionato hello un utente specifico, seleziona **profilo**. valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.

## <a name="authentication-planning"></a>Pianificazione di autenticazione
Automazione di Azure consente attività tooautomate sulle risorse in Azure, in locale, nonché con altri provider di cloud.  Affinché un tooperform runbook le azioni richieste, deve disporre delle autorizzazioni toosecurely accedere hello alle risorse con diritti minimi di hello necessari all'interno di sottoscrizione hello.  

### <a name="what-is-an-automation-account"></a>Che cos'è un account di Automazione 
Tutte le attività di automazione di hello che è eseguire sulle risorse utilizzando i cmdlet di Azure hello in automazione di Azure di eseguire l'autenticazione tooAzure utilizzando l'autenticazione basata su credenziali identità aziendale di Azure Active Directory.  Un account di automazione è separato dal conto di hello toosign tooconfigure portale toohello e utilizzare le risorse di Azure.  Le risorse di automazione incluse con un account sono seguente hello:

* **Certificati**: contiene un certificato necessario per eseguire l'autenticazione da un runbook o una configurazione DSC o per aggiungerli.
* **Connessioni** -contiene l'autenticazione e la configurazione informazioni necessarie tooconnect tooan servizio esterno o l'applicazione da un runbook o di una configurazione DSC.
* **Credenziali** -è un oggetto PSCredential che contiene le credenziali di sicurezza, ad esempio un nome utente e la password necessari tooauthenticate da un runbook o di una configurazione DSC.
* **I moduli di integrazione** -sono moduli di PowerShell inclusi con un utilizzo toomake account di automazione di Azure di cmdlet all'interno di runbook e le configurazioni DSC.
* **Pianificazioni**: contiene pianificazioni che avviano o arrestano un runbook a un'ora specifica, incluse frequenze ricorrenti.
* **Variabili**: contiene i valori disponibili da un runbook o una configurazione DSC.
* **Le configurazioni DSC** -sono script di PowerShell che descrive come tooconfigure una funzionalità del sistema operativo o le impostazioni o installare un'applicazione in un computer Windows o Linux.  
* **Runbook**: set di attività che esegue un processo automatizzato in Automazione di Azure basato su Windows PowerShell.    

risorse di automazione Hello per ogni account di automazione sono associate a una singola regione di Azure, ma gli account di automazione è possono gestire tutte le risorse di hello nella sottoscrizione. Se si dispone di criteri che richiedono dati e risorse toobe tooa isolato area specifica di un, creare gli account di automazione in aree diverse.

> [!NOTE]
> Gli account di automazione e che contengono le risorse di hello vengono creati nel portale di Azure hello, non è possibile accedere in hello portale di Azure classico. Se si desidera toomanage questi account o le proprie risorse con Windows PowerShell, è necessario utilizzare i moduli di gestione risorse di Azure hello.
> 

Quando si crea un account di automazione in hello portale di Azure, viene creata automaticamente due entità di autenticazione:

* Un account RunAs. Questo account crea un'entità servizio in Azure Active Directory (Azure AD) e un certificato. Assegna inoltre hello collaboratore basata sui ruoli access control (RBAC), che gestisce le risorse di gestione delle risorse con i runbook.
* Un account RunAs classico. Questo account consente di caricare un certificato di gestione, le risorse classiche toomanage utilizzati con i runbook.

Controllo di accesso basato sui ruoli è disponibile con Gestione risorse di Azure toogrant è consentito l'account utente di Azure AD tooan azioni e account RunAs e l'autenticazione di tale entità servizio.  Lettura [controllo di accesso basato sui ruoli nell'articolo di automazione di Azure](automation-role-based-access-control.md) per ulteriori informazioni toohelp sviluppato il modello di gestione delle autorizzazioni di automazione.  

#### <a name="authentication-methods"></a>Metodi di autenticazione
Hello nella tabella seguente sono riepilogate hello diversi metodi di autenticazione per ogni ambiente supportato da automazione di Azure.

| Metodo | Environment 
| --- | --- | 
| Account RunAs di Azure e account RunAs classico |Distribuzione Azure Resource Manager e distribuzione classica di Azure |  
| Account utente di Azure AD |Distribuzione Azure Resource Manager e distribuzione classica di Azure |  
| Autenticazione di Windows |Data center locale o un altro provider di cloud mediante hello Runbook Worker ibrido |  
| Credenziali AWS |Amazon Web Services |  

In hello **come to\Authentication e sicurezza** sezione, sono supportati gli articoli fornita una procedura di panoramica e l'implementazione tooconfigure autenticazione per questi ambienti, con un oggetto esistente o nuovo account dedicare per tale ambiente.  Per hello runas di Azure e classico account RunAs, hello argomento [aggiornamento automazione account RunAs](automation-create-runas-account.md) viene descritto come tooupdate l'account di automazione esistente con hello Run As account dal portale di hello o utilizzo di PowerShell se non è stato configurato inizialmente con un account RunAs o classico runas. Se si desidera toocreate Esegui come e un classico account RunAs con un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA), esaminare questo toolearn articolo come hello toocreate degli account con questa configurazione.     
 
## <a name="network-planning"></a>Pianificazione della rete
Per hello register di tooand tooconnect Runbook Worker ibrido con Microsoft Operations Management Suite (OMS), deve avere accesso toohello numero di porta e gli URL hello descritto di seguito.  Si tratta inoltre toohello [porte e gli URL necessari per Microsoft Monitoring Agent di hello](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Se si utilizza un server proxy per la comunicazione tra agente hello e il servizio OMS hello, è necessario tooensure che hello di risorse appropriate siano accessibili. Se si utilizza un toohello di accesso toorestrict firewall Internet, è necessario tooconfigure all'accesso toopermit firewall.

informazioni di Hello sotto porta hello elenco e gli URL necessari per hello Runbook Worker ibrido toocommunicate con l'automazione.

* Porta: è necessaria solo la porta TCP 443 per l'accesso a Internet in uscita
* URL globale: *.azure-automation.net

Se si dispone di un account di automazione definito per un'area specifica e si desidera toorestrict comunicazione con il data center della regione, hello nella tabella seguente fornisce hello DNS record per ogni area.

| **Area** | **Record DNS** |
| --- | --- |
| Stati Uniti centro-meridionali |scus-jobruntimedata-prod-su1.azure-automation.net |
| Stati Uniti orientali 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Stati Uniti centro-occidentali | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europa occidentale |we-jobruntimedata-prod-su1.azure-automation.net |
| Europa settentrionale |ne-jobruntimedata-prod-su1.azure-automation.net |
| Canada centrale |cc-jobruntimedata-prod-su1.azure-automation.net |
| Asia sudorientale |sea-jobruntimedata-prod-su1.azure-automation.net |
| India centrale |cid-jobruntimedata-prod-su1.azure-automation.net |
| Giappone orientale |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australia sud-orientale |ase-jobruntimedata-prod-su1.azure-automation.net |
| Regno Unito meridionale | uks-jobruntimedata-prod-su1.azure-automation.net |
| US Gov Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Per un elenco di indirizzi IP anziché nomi, scaricare e consultare hello [indirizzo IP del Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653) file xml da hello Microsoft Download Center. 

> [!NOTE]
> Questo file contiene hello intervalli di indirizzi IP (inclusi gli intervalli di calcolo, archiviazione e di SQL) utilizzati in hello Data Center di Microsoft Azure. Un file aggiornato viene registrato ogni settimana che riflette gli intervalli hello attualmente distribuito e gli eventuali intervalli IP toohello modifiche imminenti. Nuovi intervalli di valori visualizzati nel file hello verrà non utilizzati nei data center hello per almeno una settimana. . Download hello nuovo xml del file ogni settimana ed eseguire le modifiche necessarie hello nel sito toocorrectly identificare i servizi in esecuzione in Azure. Express indirizzare gli utenti potrebbero notare che questo file è utilizzato tooupdate hello annuncio BGP di Azure spazio in hello prima settimana del mese. 
> 

## <a name="creating-an-automation-account"></a>Creare un account di Automazione

Esistono diversi modi per creare un account di automazione nel portale di Azure hello.  Hello nella tabella seguente presenta ogni tipo di esperienza di distribuzione e le differenze tra di essi.  

|Metodo | Descrizione |
|-------|-------------|
| Selezionare hello Marketplace di automazione e controllo | Un'offerta, che consente di creare un account di automazione e l'area di lavoro OMS collegato tooone un'altra in hello allo stesso gruppo di risorse e area.  Integrazione con OMS anche include hello vantaggio derivante dall'utilizzo toomonitor Log Analitica e analizzare runbook flussi lo stato e di processo nel tempo e utilizzare funzionalità avanzate tooescalate o esaminare i problemi. Hello offerta anche distribuisce hello il rilevamento delle modifiche e gestione degli aggiornamenti soluzioni, che sono abilitate per impostazione predefinita. |
| Selezionare automazione hello Marketplace | Crea un account di automazione in un gruppo di risorse nuovo o esistente che non è l'area di lavoro OMS tooan collegato e non include una delle soluzioni disponibili dall'offerta di automazione e controllo hello. Questa è una configurazione di base che illustra tooAutomation e utili come toowrite runbook, le configurazioni DSC e utilizzare hello funzionalità del servizio hello. |
| Soluzioni di gestione selezionate | Se si seleziona una soluzione di  **[gestione aggiornamenti](../operations-management-suite/oms-solution-update-management.md)**,  **[avviare o arrestare le macchine virtuali durante gli orari di inattività](automation-solution-vm-management.md)**, o  **[ Il rilevamento delle modifiche](../log-analytics/log-analytics-change-tracking.md)**  chiesto tooselect un'automazione esistente e l'area di lavoro OMS o offerta si hello toocreate opzione entrambi come richiesto per toobe soluzione hello distribuito nella sottoscrizione. |

In questo argomento illustra la creazione di un account di automazione e l'area di lavoro OMS grazie a caricamento hello di automazione e controllo.  un account di automazione per il test o toopreview servizio hello, hello revisione articolo seguente autonomo toocreate [creare account di automazione autonomo](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Creare un account di Automazione integrato con OMS
Hello consigliabile tooonboard metodo che automazione ha dall'offerta di automazione e controllo hello hello Marketplace.  Viene creato un account di automazione e stabilisce integrazione hello con un'area di lavoro OMS, inclusi hello opzione tooinstall hello soluzioni di gestione che sono disponibili con offerta hello.  

1. Accedi toohello portale di Azure con un account che sia un membro del ruolo di amministratori della sottoscrizione hello e al coamministratore della sottoscrizione hello.

2. Fare clic su **New**.<br><br> ![Selezionare l'opzione Nuovo nel portale di Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Cercare **automazione** e quindi in hello risultati della ricerca selezionare **di automazione e controllo***.<br><br> ![Cercare e selezionare Automation &amp; Control nel Marketplace](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Dopo aver letto descrizione hello per offerta hello, fare clic su **crea**.  

5. In hello **di automazione e controllo** pannello impostazioni, seleziona **area di lavoro OMS**.  In hello **aree di lavoro OMS** pannello selezionare un toohello dell'area di lavoro collegato OMS stessa sottoscrizione di Azure che hello account di automazione è in o creare un'area di lavoro OMS.  Se non si dispone di un'area di lavoro OMS, selezionare **Crea nuova area di lavoro** e hello **area di lavoro OMS** pannello eseguire l'esempio hello: 
   - Specificare un nome per hello nuovo **area di lavoro OMS**.
   - Selezionare un **sottoscrizione** toolink tooby selezionare dall'elenco a discesa hello se predefinito hello selezionato non è appropriato.
   - Per il **gruppo di risorse**, è possibile selezionare un gruppo di risorse esistente o crearne uno.  
   - Selezionare un **percorso**.  Non sono attualmente hello solo le posizioni disponibili **Australia sudorientale**, **Stati Uniti orientali**, **Asia sudorientale**, **occidentale Stati Uniti centro**e  **Europa occidentale**.
   - Selezionare un **Piano tariffario**.  soluzione Hello viene offerto con due livelli: libero e di livello per ogni nodo (OMS).  livello gratuito Hello pone un limite sulla quantità di hello di dati raccolti giornalmente, periodo di memorizzazione e runbook processo runtime minuti.  livello per ogni nodo (OMS) Hello non dispone di un limite alla quantità di hello di dati raccolti giornalmente.  
   - Selezionare **Account di Automazione**.  Se si sta creando una nuova area di lavoro OMS, è necessario tooalso creare un account di automazione che è associato a hello nuova area di lavoro OMS specificato in precedenza, inclusa la sottoscrizione di Azure, un gruppo di risorse e area.  È possibile selezionare **creare un account di automazione** e hello **Account di automazione** pannello, fornire il seguente hello: 
  - In hello **nome** immettere nome hello di hello account di automazione.

    Tutte le altre opzioni vengono popolati automaticamente in base a area di lavoro OMS hello selezionata e non è possibile modificare queste opzioni.  Un account RunAs di Azure è metodo di autenticazione predefinito di hello per offerta hello.  Quando si fa clic su **OK**, opzioni di configurazione hello vengono convalidate e viene creato l'account di automazione hello.  È possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello. 

    In alternativa, selezionare un account RunAs di Automazione esistente.  account Hello selezionato non può essere già collegato tooanother area di lavoro OMS, in caso contrario in cui viene visualizzato un messaggio di notifica nel pannello hello.  Se è già collegato, è necessario un diverso account RunAs automazione tooselect o crearne uno.

    Dopo aver completato le informazioni di hello necessarie, fare clic su **crea**.  viene verificate informazioni Hello e vengono creati account di automazione Account Esegui come e hello.  Verrà visualizzata nuovamente toohello **area di lavoro OMS** pannello automaticamente.  

6. Dopo aver specificato le informazioni necessarie hello in hello **area di lavoro OMS** pannello, fare clic su **crea**.  Mentre viene verificate le informazioni di hello e viene creato l'area di lavoro hello, è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello.  Verrà visualizzata nuovamente toohello **Aggiungi soluzione** blade.  

7. In hello **di automazione e controllo** pannello impostazioni, confermare tooinstall hello consigliato soluzioni pre-selezionate. Se ne viene deseleziona qualcuna, sarà possibile installarle singolarmente in un secondo momento.  

8. Fare clic su **crea** tooproceed con caricamento automazione e un'area di lavoro OMS. Tutte le impostazioni vengono convalidate e quindi tenta hello toodeploy offerta nella sottoscrizione.  Questo processo può richiedere alcuni secondi toocomplete ed è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello. 

Una volta caricate offerta hello, è possibile avviare la creazione di soluzioni di gestione è stato abilitato il runbook, utilizzare hello, distribuire un [Runbook worker ibrido](automation-hybrid-runbook-worker.md) ruolo o iniziare a utilizzarla con [Log Analitica](https://docs.microsoft.com/azure/log-analytics) toocollect dati generati dalle risorse cloud o in locale nell'ambiente in uso.   

## <a name="next-steps"></a>Passaggi successivi
* Per verificare che il nuovo account di Automazione possa eseguire l'autenticazione con le risorse di Azure, vedere [Test Azure Automation Run As account authentication](automation-verify-runas-authentication.md) (Testare l'autenticazione di un account RunAs di Automazione di Azure).
* tooget avviato con la creazione di runbook, esaminare innanzitutto hello [tipi di automazione runbook](automation-runbook-types.md) supportati e relative considerazioni prima di iniziare la creazione.


