---
title: aaaGet avviato con l'integrazione di log di Azure | Documenti Microsoft
description: Scopri il servizio di integrazione di log tooinstall hello Azure e integrare i registri di archiviazione di Azure, i log di controllo di Azure e gli avvisi del Centro sicurezza di Azure.
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Integrazione dei log di Azure con la registrazione di Diagnostica di Azure e l'inoltro di eventi di Windows
Integrazione di Log di Azure (AzLog) consente di toointegrate registri raw dalle risorse di Azure in sistemi di informazioni di sicurezza e gestione di eventi (SIEM) locale. Questa integrazione rende possibili toohave un dashboard di sicurezza unificata di tutte le risorse, locale o nel cloud hello, in modo che è possibile aggregare, correlare, analizzare e avviso per gli eventi di protezione associati alle applicazioni.
>[!NOTE]
Per ulteriori informazioni sull'integrazione di Log di Azure, è possibile esaminare hello [panoramica dell'integrazione di Azure Log](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

In questo articolo consentono di iniziare con l'integrazione di Log di Azure, porre l'attenzione sul installazione hello di hello Azlog servizio e l'integrazione di servizio hello con diagnostica di Azure. servizio di integrazione di Azure Log Hello potranno quindi essere in grado di toocollect informazioni del registro eventi di Windows da hello canale di eventi di sicurezza di Windows da macchine virtuali distribuite in Azure IaaS. Questa operazione è molto simile troppo "Inoltro degli eventi" che è stata utilizzata in locale.

>[!NOTE]
>output di Hello possibilità toobring hello di integrazione di log di Azure in toohello SIEM viene fornito da hello SIEM stesso. Vedere l'articolo hello [l'integrazione di Azure Log integrazione con SIEM locale](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) per ulteriori informazioni.

toobe molto chiaro - hello servizio di integrazione di Log di Azure viene eseguito in un computer fisico o virtuale che utilizza hello Windows Server 2008 R2 o versioni successive del sistema operativo (Windows Server 2012 R2 o Windows Server 2016 sono preferito).

computer fisico Hello può eseguire in locale (o in un sito di hosting). Se si sceglie di servizio di integrazione di Azure Log toorun hello in una macchina virtuale, che la macchina virtuale può essere situata in locale o in un cloud pubblico, come Microsoft Azure.

Hello fisico o macchina virtuale in esecuzione il servizio di integrazione di Log di Azure hello richiede la connettività di rete toohello cloud pubblico di Azure. Passaggi in questo articolo forniscono dettagli sulla configurazione di hello.

## <a name="prerequisites"></a>Prerequisiti
Come minimo, l'installazione di hello di AzLog richiede hello seguenti elementi:
* Una **sottoscrizione di Azure**. Se non si ha una sottoscrizione, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).
* Oggetto **account di archiviazione** che può essere utilizzato per la registrazione diagnostica Windows Azure (è possibile utilizzare un account di archiviazione configurati in precedenza o crearne uno nuovo, si illustrerà come tooconfigure hello account di archiviazione più avanti in questo articolo)
  >[!NOTE]
  A seconda dello scenario, potrebbe non essere necessario un account di archiviazione. Per hello uno scenario di diagnostica di Azure illustrate in questo articolo è necessaria una.
* **Due sistemi**: un computer in cui verrà eseguito il servizio di integrazione di Log di Azure hello e un computer che verrà monitorato e avere le informazioni di registrazione inviate toohello Azlog computer del servizio.
   * Una macchina da toomonitor: si tratta di una macchina virtuale in esecuzione come un [macchina virtuale di Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Un computer in cui verrà eseguito servizio di integrazione di hello log di Azure. questa macchina raccoglierà tutte le informazioni del log hello che verranno successivamente importate in SIEM.
    * Questo sistema può essere locale o in Microsoft Azure.  
    * È necessario toobe in esecuzione un x64 versione di Windows server 2008 R2 SP1 o versione successiva e avere .NET 4.5.1 installato. È possibile determinare una versione di .NET hello installata dal seguente hello articolo intitolato [procedura: determinare quali versioni di .NET Framework installate](https://msdn.microsoft.com/library/hh925568)  
    Deve disporre di connettività toohello account di archiviazione Azure usato per la registrazione diagnostica di Azure. Microsoft fornirà le istruzioni su come verificare la connettività più avanti in questo articolo

Per una dimostrazione del processo di hello di creazione di una macchina virtuale tramite il portale di Azure hello rapidamente un quadro hello video sotto.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione
Durante il test di integrazione di Log di Azure, è possibile utilizzare qualsiasi sistema che soddisfi i requisiti minimi del sistema operativo hello. Tuttavia, per un hello ambiente di produzione carico potrebbe richiedere tooplan per la scalabilità verticale o.

Se il volume di eventi è elevato, è possibile eseguire più istanze del servizio di integrazione di Azure Log hello (un'istanza per ogni macchina virtuale o fisica). Inoltre, è possibile bilanciare il carico gli account di archiviazione di diagnostica Azure per Windows (WAD) e il numero di hello di istanze di sottoscrizioni tooprovide toohello devono basarsi sulle capacità di.
>[!NOTE]
In questo momento non è indicazioni specifiche per quando il log macchine integrazione (ad esempio, i computer che eseguono il servizio di integrazione di log di Azure hello) tooscale istanze di Azure o per gli account di archiviazione o sottoscrizioni. Le decisioni di scalabilità si devono basare sulle osservazioni delle prestazioni in ognuna di queste aree.

È inoltre hello opzione tooscale backup toohelp servizio di integrazione di Azure Log hello di migliorare le prestazioni. Hello seguenti metriche delle prestazioni consentono di ridimensionamento macchine hello scegliere servizio di integrazione toorun hello log di Azure:
* Su un computer con 8 processori (memoria centrale), una singola istanza dell'integratore Azlog può elaborare circa 24 milioni di eventi al giorno (all'incirca 1 milione all'ora).

* Su un computer con 4 processori (memoria centrale), una singola istanza dell'integratore Azlog può elaborare circa 1,5 milioni di eventi al giorno (all'incirca 62,5 K all'ora).

## <a name="install-azure-log-integration"></a>Installare l'integrazione dei log di Azure
tooinstall integrazione di Log di Azure, è necessario hello toodownload [integrazione di log di Azure](https://www.microsoft.com/download/details.aspx?id=53324) file di installazione. Eseguire routine di installazione hello e decidere se si desidera tooMicrosoft informazioni di telemetria tooprovide.  

![Schermata di installazione con la casella della telemetria selezionata](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> È consigliabile consentire i dati di telemetria toocollect Microsoft. Per disabilitare la raccolta dei dati di telemetria è possibile deselezionare questa opzione.
>


servizio di integrazione di Azure Log Hello raccoglie dati di telemetria da computer hello in cui è installato.  

I dati di telemetria raccolti sono:

* Eccezioni che si verificano durante l'esecuzione dell'integrazione dei log di Azure
* Metriche relative al numero di hello di query e gli eventi elaborati
* Statistiche sulle opzioni della riga di comando Azlog.exe che vengono usate

il processo di installazione di Hello è trattato nella hello video sotto.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Passaggi successivi all'installazione e di convalida
Dopo il completamento delle routine di installazione di base hello, si è pronti tooperform post installazione e la convalida passaggi:
1. Aprire una finestra di PowerShell con privilegi elevata e passare troppo**c:\Program Files\Microsoft Azure Log integrazione**
2. primo passaggio Hello è necessario tootake è hello tooget che azlog Cmdlets importati. È possibile farlo eseguendo script hello **LoadAzlogModule.ps1** (avviso hello ". \" nel comando seguente hello). Digitare **.\LoadAzlogModule.ps1** e premere **INVIO**.  
Dovrebbe essere simile a quello visualizzato nella figura hello seguente. </br></br>
![Schermata di installazione con la casella della telemetria selezionata](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. È ora necessario tooconfigure AzLog toouse un ambiente di Azure specifico. Un ambiente"Azure" è hello "tipo" del cloud di Azure data center che si desidera toowork con. Mentre sono presenti diversi ambienti di Azure in questo momento, sono opzioni attualmente rilevanti hello **cloud** o **AzureUSGovernment**.   Nell'ambiente di PowerShell con privilegi elevati assicurarsi di essere in **C:\Programmi\Integrazione log di Microsoft Azure\** </br></br>
    Una volta, eseguire il comando hello: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (per l'area commerciale di Azure)

      >[!NOTE]
      Quando il comando hello ha esito positivo, non riceverà eventuali commenti e suggerimenti.  Se si desidera cloud di Microsoft Azure per enti pubblici hello toouse, si utilizzerebbe **AzureUSGovernment** (per hello - variabile Name) per hello cloud governo USA. Al momento gli altri cloud di Azure non sono supportati.  
4. Prima di poter monitorare un sistema è necessario il nome di hello hello dell'account di archiviazione in uso per la diagnostica di Azure.  In hello portale di Azure passare troppo**macchine virtuali** e cercare di macchina virtuale hello che verrà monitorato. In hello **proprietà** , scegliere **le impostazioni di diagnostica**.  Fare clic su **agente** e prendere nota del nome di account di archiviazione hello specificato. Il nome dell'account sarà necessario per un passaggio successivo.
![Impostazioni di Diagnostica di Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Impostazioni di Diagnostica di Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Se il monitoraggio non è stato abilitato durante la creazione della macchina virtuale sarà possibile hello opzione tooenable, come illustrato in precedenza.
5. Ora Sostituiamo nostri toohello indietro attenzione macchina di integrazione di log di Azure. È necessario tooverify di disporre di connettività toohello, Account di archiviazione dal sistema hello in cui è installato l'integrazione di Log di Azure. computer fisico Hello o macchina virtuale che esegue hello Azure Log Integration service deve accedere a informazioni di toohello storage account tooretrieve registrate da diagnostica di Azure, come configurato in ogni hello monitorato sistemi.  
  1. È possibile scaricare Azure Storage Explorer [qui](http://storageexplorer.com/).
  2. Eseguire routine di installazione hello
  3. Una volta completata la fare clic su installazione hello **Avanti** e lasciare la casella di controllo hello **avviare Microsoft Azure Storage Explorer** selezionata.  
  4. Accedi tooAzure.
  5. Verificare che è possibile visualizzare l'account di archiviazione hello è configurato per la diagnostica di Azure.  
![Account di archiviazione](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Si noti che ci sono alcune opzioni sotto gli account di archiviazione. Una di esse è **Tabelle**. Sotto **Tabelle** dovrebbe essere presente una tabella denominata **WADWindowsEventLogsTable**. </br></br>
   ![Account di archiviazione](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Integrare la registrazione di Diagnostica di Azure
In questo passaggio, si configurerà macchina hello hello Azure Log Integration service tooconnect toohello account di archiviazione che contiene i file di log hello.
toocomplete questo passaggio è necessario alcuni aspetti di inizio.  
* **FriendlyNameForSource:** si tratta di un nome descrittivo che è possibile applicare l'account di archiviazione toohello di aver configurato informazioni toostore hello della macchina virtuale da diagnostica di Azure
* **: StorageAccountName** hello nome dell'account di archiviazione hello specificato quando è stato configurato diagnotics Azure.  
* **Proprietà StorageKey:** tratta hello archiviazione chiave hello account di archiviazione in cui le informazioni di diagnostica Azure hello è archiviato per questa macchina virtuale.  

Eseguire hello chiave di archiviazione hello tooobtain i passaggi seguenti:
 1. Sfoglia toohello [portale di Azure](http://portal.azure.com).
 2. Nel riquadro di spostamento hello di hello Azure console, scorrere in basso toohello e fare clic su **più servizi.**

 ![Altri servizi](./media/security-azure-log-integration-get-started/more-services.png)
 3. Immettere **archiviazione** in hello **filtro** casella di testo. Fare clic su **Account di archiviazione** (il valore sarà visualizzato dopo avere immesso **Archiviazione**)

   ![casella Filtro](./media/security-azure-log-integration-get-started/filter.png)
 4. Verrà visualizzato un elenco di account di archiviazione, fare doppio clic sull'account hello tooLog archiviazione assegnato.

   ![elenco degli account di archiviazione](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Fare clic su **le chiavi di accesso** in hello **impostazioni** sezione.

  ![chiavi di accesso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Copia **key1** e inserirlo in un luogo sicuro che è possibile accedere per successiva hello.

   ![due chiavi di accesso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Nel server di hello di integrazione di Log di Azure installato, aprire un prompt dei comandi con privilegi elevati (si noti che viene usata una finestra prompt dei comandi con privilegi elevata in questo caso, non è una console di PowerShell con privilegi elevata).
 8. Passare troppo**c:\Program Files\Microsoft Azure Log integrazione**
 9. Eseguire ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> Ad esempio ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` se si desidera tooshow ID di sottoscrizione hello backup nell'evento hello XML, aggiungere nome descrittivo toohello ID sottoscrizione hello: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` o, ad esempio,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Attendere fino a too60 minuti, quindi visualizzare gli eventi di hello che vengono estratti dall'account di archiviazione hello. tooview, aprire **Visualizzatore eventi > i registri di Windows > eventi inoltrati** su hello Azlog Integrator.

Qui è possibile visualizzare un video trasmessi tramite i passaggi di hello descritti sopra.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Cosa accade se dati non vengono visualizzati nella cartella eventi inoltrati hello?
Se dopo un'ora dati non vengono visualizzati in hello **eventi inoltrati** cartella, quindi:

1. Servizio di integrazione di Log di Azure in esecuzione hello di hello macchina e confermare che possa accedere a Azure. tootest connettività, provare a tooopen hello [portale di Azure](http://portal.azure.com) dal browser hello.
2. Verificare che account utente di hello **Azlog** dispone dell'autorizzazione di scrittura sulla cartella hello **users\Azlog**.
  <ol type="a">
   <li>Aprire **Esplora risorse** </li>
  <li> Passare troppo**c:\users** </li>
  <li> Fare clic con il pulsante destro del mouse su **C:\users\Azlog** </li>
  <li> Fare clic su **Protezione**  </li>
  <li> Fare clic su **Service\Azlog NT** e controllare le autorizzazioni di hello per conto di hello. Se non è presente in questa scheda account hello o se le autorizzazioni appropriate di hello non sono attualmente visualizzato possibile concedere diritti dell'account hello in questa scheda.</li>
  </ol>
3.Rendere che account di archiviazione hello aggiunto nel comando hello **Azlog origine aggiungere** è elencato quando si esegue il comando hello **elenco origine Azlog**.
4. Andare troppo**Visualizzatore eventi > i registri di Windows > applicazione** toosee se sono presenti errori segnalati dall'integrazione di log di Azure hello.


Se si verificano problemi durante l'installazione di hello e configurazione, aprire un [richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md)selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.

Un'altra opzione di supporto è hello [Forum MSDN di Azure Log integrazione](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Qui può supportare loro community hello con domande, le risposte, suggerimenti e consigli su come tooget hello più dal Log di Azure di integrazione. Inoltre, il team di integrazione di Azure Log hello questo forum consente di monitorare e aiutano ogni volta che è possibile.

## <a name="next-steps"></a>Passaggi successivi
toolearn più informazioni sull'integrazione di Log di Azure, vedere hello seguenti documenti:

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Integrazione log di Microsoft Azure) - Area download per informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.
* [Integrazione di log di introduzione tooAzure](security-azure-log-integration-overview.md) : questo documento introduce tooAzure integrazione di log, le funzionalità chiave e il funzionamento.
* [Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – questo post di blog viene illustrato come tooconfigure Azure log toowork integrazione con soluzioni di partner Splunk e ArcSight HP, IBM QRadar. Si tratta di linea Guida corrente in modo tooconfigure hello componenti SIEM. Per altri dettagli, contattare prima di tutto il fornitore SIEM.
* [Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md) - Queste domande frequenti riguardano l'integrazione dei log di Azure.
* [L'integrazione di Centro sicurezza PC avvisi con Azure log integrazione](../security-center/security-center-integrating-alerts-with-log-integration.md) : questo documento viene illustrato come centro di sicurezza toosync avvisi, insieme agli eventi di sicurezza di macchina virtuale raccolti da diagnostica di Azure e di log attività di Azure, con analitica del log o una soluzione SIEM.
* [Nuove funzionalità di diagnostica di Azure e i log di controllo di Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : questo post di blog introduce i log di controllo tooAzure e altre funzionalità che consentono di ottenere informazioni approfondite operazioni hello delle risorse di Azure.
