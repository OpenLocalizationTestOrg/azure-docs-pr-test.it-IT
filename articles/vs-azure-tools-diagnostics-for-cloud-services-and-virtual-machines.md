---
title: aaaConfiguring diagnostica per servizi Cloud di Azure e macchine virtuali | Documenti Microsoft
description: Viene descritto come tooconfigure informazioni di diagnostica per il debug di servizi cloud di Azure e le macchine virtuali (VM) in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure
Quando è necessario tootroubleshoot un servizio cloud di Azure o una macchina virtuale di Azure, è possibile configurare diagnostica di Azure più facilmente con Visual Studio. Diagnostica Azure cattura i dati di sistema e i dati di registrazione nelle macchine virtuali hello e istanze di macchine virtuali che eseguono il servizio cloud e trasferisce i dati in un account di archiviazione di propria scelta. Per altre informazioni sulla registrazione di diagnostica in Azure, vedere [Abilitare la registrazione diagnostica per le app Web del Servizio app di Azure](app-service-web/web-sites-enable-diagnostic-log.md).

In questo argomento illustra come tooenable e configurare diagnostica Windows Azure in Visual Studio, sia prima sia dopo la distribuzione, nonché in macchine virtuali di Azure. Viene inoltre visualizzato come tipi di hello tooselect di toocollect informazioni di diagnostica e modalità di raccolta informazioni hello tooview dopo di esso.

È possibile configurare diagnostica Azure in hello seguenti modi:

* È possibile modificare le impostazioni di configurazione di diagnostica tramite hello **configurazione di diagnostica** nella finestra di dialogo di Visual Studio. Hello impostazioni vengono salvate in un file denominato Diagnostics. wadcfgx (Diagnostics. wadcfg in Azure SDK 2.4 o versioni precedenti). In alternativa, è possibile modificare direttamente il file di configurazione di hello. Se si aggiorna manualmente il file hello, le modifiche alla configurazione di hello richiederà hello effetto successivo che si distribuisce tooAzure servizio cloud di hello o un servizio hello esecuzione nell'emulatore di hello.
* Utilizzare **Cloud Explorer** o **Esplora Server** nelle impostazioni di diagnostica di Visual Studio toochange hello per una macchina virtuale o un servizio cloud in esecuzione.

## <a name="azure-26-diagnostics-changes"></a>Modifiche alla diagnostica di Azure 2.6
Per i progetti di Azure SDK 2.6 in Visual Studio, hello dopo le modifiche apportata. (Queste modifiche si applicano anche toolater versioni di Azure SDK.)

* emulatore locale Hello supporta ora la diagnostica. Questo significa che è possibile raccogliere dati di diagnostica e verificare che l'applicazione crea hello tracce corrette durante lo sviluppo ed il test in Visual Studio. stringa di connessione Hello `UseDevelopmentStorage=true` Abilita raccolta dati di diagnostica, mentre si esegue il progetto servizio cloud in Visual Studio utilizzando l'emulatore di archiviazione Azure hello. Tutti i dati di diagnostica vengono raccolti nell'account di archiviazione hello (archiviazione di sviluppo).
* stringa di connessione account archiviazione diagnostica Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) viene archiviato nuovamente nel file di configurazione (. cscfg) servizio hello. In Azure SDK 2.5 l'account di archiviazione di diagnostica hello è stato specificato nel file Diagnostics. wadcfgx hello.

Esistono alcune differenze sostanziali tra la stringa di connessione hello lavorato in Azure SDK 2.4 e versioni precedenti e sul relativo funzionamento in Azure SDK 2.6 e versioni successive.

* In Azure SDK 2.4 e versioni precedenti, la stringa di connessione hello è stata utilizzata come runtime dalle hello tooget di plug-in di diagnostica hello informazioni di account di archiviazione per il trasferimento di log di diagnostica.
* In Azure SDK 2.6 e versioni successive, stringa di connessione di diagnostica hello viene utilizzato dall'estensione di diagnostica di Visual Studio tooconfigure hello con informazioni sull'account di archiviazione appropriato hello durante la pubblicazione. stringa di connessione Hello consente di definire diversi account di archiviazione per le configurazioni di servizio diverso che Visual Studio verrà utilizzato durante la pubblicazione. Tuttavia, poiché plug-in di hello diagnostica non è più disponibile (dopo Azure SDK 2.5), file con estensione cscfg hello da sola non è possibile abilitare hello estensione di diagnostica. È l'estensione di hello tooenable separatamente tramite strumenti quali Visual Studio o PowerShell.
* processo di hello toosimplify di configurazione dell'estensione di diagnostica hello con PowerShell, output del pacchetto hello da Visual Studio contiene anche hello pubblico XML di configurazione per l'estensione diagnostica hello per ogni ruolo. Visual Studio Usa hello diagnostica sulle stringhe di connessione toopopulate hello storage account presenti nella configurazione pubblica hello. file di configurazione pubblica Hello vengono creati nella cartella estensioni hello e seguono pattern hello PaaSDiagnostics. &lt;RoleName >. Paasdiagnostics.<NomeRuolo>.pubconfig.Xml. Tutte le distribuzioni basate su PowerShell è possono utilizzare il toomap questo modello ogni tooa configurazione ruolo.
* stringa di connessione Hello in file con estensione cscfg hello viene anche usato dai hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess hello dati di diagnostica in modo che può essere visualizzati in hello **monitoraggio** stringa di connessione scheda hello è necessaria tooconfigure hello servizio tooshow monitoraggio dettagliato dei dati nel portale di hello.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>La migrazione dei progetti tooAzure SDK 2.6 e versioni successive
Quando la migrazione da Azure SDK 2.5 tooAzure SDK 2.6 o versione successiva, se si dispone di un account di archiviazione di diagnostica specificato nel file con estensione wadcfgx hello, quindi viene mantenuta non esiste. account tootake sfruttare la flessibilità di hello dell'utilizzo di archiviazione diversi per diverse configurazioni di archiviazione, sarà necessario toomanually aggiungere progetto tooyour stringa di connessione hello. Se si sta eseguendo la migrazione di un progetto da Azure SDK 2.4 o versioni precedenti tooAzure SDK 2.6, quindi hello vengono mantenute le stringhe di connessione di diagnostica. Tuttavia, si noti come stringhe di connessione vengono considerate in Azure SDK 2.6 specificato nella sezione precedente hello modifiche hello.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Determinazione di account di archiviazione di diagnostica hello Visual Studio
* Se si specifica una stringa di connessione di diagnostica nel file con estensione cscfg hello, Visual Studio viene utilizzata l'estensione diagnostica hello tooconfigure durante la pubblicazione e durante la generazione di file xml di configurazione pubblica hello durante la creazione di pacchetti.
* Se viene specificata alcuna stringa di connessione di diagnostica nel file con estensione cscfg hello, quindi Visual Studio esegue il fallback account di archiviazione hello toousing specificato hello wadcfgx tooconfigure hello diagnostica estensione di file durante la pubblicazione e la generazione di hello pubblico file di configurazione xml quando creazione del pacchetto.
* stringa di connessione di diagnostica Hello in file con estensione cscfg hello ha la precedenza su account di archiviazione hello in file con estensione wadcfgx hello. Se è una stringa di connessione di diagnostica specificati nel file con estensione cscfg hello, Visual Studio utilizza che e ignora l'account di archiviazione hello in con estensione wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Cosa does hello "Aggiorna stringhe di connessione di archiviazione..." …"
casella di controllo per Hello **Aggiorna stringhe di connessione di archiviazione per la diagnostica e la memorizzazione nella cache con le credenziali dell'account di archiviazione di Microsoft Azure quando si pubblicano tooMicrosoft Azure** offre un modo pratico di tooupdate qualsiasi archiviazione account stringhe di connessione con l'account di archiviazione di Azure hello specificato durante la pubblicazione.

Si supponga ad esempio si seleziona questa casella di controllo e hello stringa di connessione specifichi `UseDevelopmentStorage=true`. Quando si pubblica hello tooAzure di progetto, Visual Studio aggiornerà automaticamente stringa di connessione di diagnostica hello con account di archiviazione hello specificato nella procedura guidata di pubblicazione hello. Tuttavia, se un account di archiviazione reale è stato specificato come stringa di connessione di diagnostica hello, allora tale account viene utilizzato invece.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Differenze della funzionalità di diagnostica tra Azure SDK 2.4 e versioni precedenti e Azure SDK 2.5 e versioni successive
Se si esegue l'aggiornamento del progetto da Azure SDK 2.4 tooAzure SDK 2.5 o versioni successive, è necessario tenere hello presente seguenti differenze di funzionalità di diagnostica.

* **Le API di configurazione sono deprecate** : la configurazione a livello di codice della diagnostica è disponibile in Azure SDK 2.4 o versioni precedenti, ma è deprecata in Azure SDK 2.5 e versioni successive. Se la configurazione della diagnostica è attualmente definita nel codice, è necessario tooreconfigure tali impostazioni da zero nel progetto di migrazione hello in ordine per l'utilizzo di diagnostica tookeep. file di configurazione di diagnostica di Hello per Azure SDK 2.4 è Diagnostics. wadcfg e Diagnostics. wadcfgx per Azure SDK 2.5 e versioni successive.
* **Diagnostica per le applicazioni di servizio cloud può essere configurata solo a livello di ruolo hello, non a livello di istanza hello.**
* **Ogni volta che si distribuisce l'app, viene aggiornata la configurazione di diagnostica hello** : ciò può causare problemi di parità se si modifica la configurazione di diagnostica da Esplora Server e quindi distribuire nuovamente l'app.
* **In Azure SDK 2.5 e versioni successive, i dump di arresto anomalo del sistema sono configurati nel file di configurazione diagnostica hello, non nel codice** : nel caso di arresto anomalo del sistema configurato nel codice, sarà necessario configurazione hello di trasferimento toomanually dal file di configurazione toohello di codice, perché i dump di arresto anomalo di hello non vengono trasferiti durante la migrazione di hello tooAzure SDK 2.6.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Abilitare la diagnostica nei progetti di servizi cloud prima della distribuzione
In Visual Studio, è possibile scegliere i dati di diagnostica toocollect per i ruoli in esecuzione in Azure, quando si esegue il servizio hello nell'emulatore hello prima di distribuirlo. Tutte le impostazioni di toodiagnostics modifiche in Visual Studio vengono salvate nel file di configurazione Diagnostics. wadcfgx hello. Queste impostazioni di configurazione specificano l'account di archiviazione hello in cui sono salvati i dati di diagnostica quando si distribuisce il servizio cloud.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>tooenable diagnostica in Visual Studio prima della distribuzione
1. Nel menu di scelta rapida hello ruolo hello desiderato, scegliere **proprietà**, quindi scegliere hello **configurazione** scheda del ruolo hello **proprietà** finestra.
2. In hello **diagnostica** sezione, assicurarsi che tale hello **Abilita diagnostica** casella di controllo è selezionata.
   
    ![Accesso opzione Abilita diagnostica hello](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Scegliere hello puntini di sospensione (…) pulsante toospecify hello account di archiviazione in cui si desidera hello toobe di dati di diagnostica archiviati. account di archiviazione Hello che scelto sarà hello posizione in cui i dati di diagnostica.
   
    ![Specificare toouse account di archiviazione hello](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. In hello **crea stringa di connessione di archiviazione** finestra di dialogo, specificare se si desidera tooconnect utilizzando hello emulatore di archiviazione di Azure, una sottoscrizione di Azure oppure credenziali immesse manualmente.
   
    ![Finestra di dialogo Account di archiviazione](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Se si sceglie l'opzione di hello emulatore di archiviazione di Microsoft Azure, la stringa di connessione hello è impostata tooUseDevelopmentStorage = true.
   * Se si sceglie hello l'opzione di sottoscrizione, è possibile scegliere una sottoscrizione di Azure da nome di account toouse e hello hello. È possibile scegliere che Gestisci account hello pulsante toomanage le sottoscrizioni di Azure.
   * Se si sceglie l'opzione relativa alle credenziali hello immessa manualmente, puoi tooenter richiesta hello nome e la chiave di account Azure a cui si vuole toouse hello.
5. Scegliere hello **configura** hello tooview pulsante **configurazione di diagnostica** la finestra di dialogo. Ogni scheda, ad eccezione di **Generale** e **Directory log** rappresenta un'origine di dati di diagnostica che è possibile raccogliere. scheda predefinita Hello, **generale**, offre hello le seguenti opzioni di raccolta dati di diagnostica: **solo errori**, **tutte le informazioni**, e **piano personalizzato** . opzione predefinita, Hello **solo errori**, accetta hello quantità minima di spazio di archiviazione perché non trasferisce gli avvisi o messaggi di traccia. Hello hello la maggior parte delle informazioni di tutti i trasferimenti di opzione di informazioni ed è, hello, pertanto, l'opzione più costosa in termini di archiviazione.
   
    ![Abilitare la diagnostica e la configurazione di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Per questo esempio, selezionare hello **piano personalizzato** opzione in modo è possibile personalizzare hello dati raccolti.
7. Hello **Quota disco in MB** casella Specifica la quantità di spazio da tooallocate dell'account di archiviazione per i dati di diagnostica. Se si desidera, è possibile modificare il valore di predefinito hello.
8. In ogni scheda dei dati di diagnostica desiderati toocollect, selezionare il **Abilita il trasferimento di <log type>**  casella di controllo. Ad esempio, se si desidera toocollect dei log applicazioni, selezionare hello **Abilita il trasferimento dei log applicazione** casella di controllo hello **log applicazioni** scheda. Specificare anche eventuali altre informazioni richieste da ogni tipo di dati di diagnostica. Vedere la sezione hello **configurare origini dati di diagnostica** più avanti in questo argomento per informazioni sulla configurazione di ogni scheda.
9. Dopo aver abilitato la raccolta di tutti i dati di diagnostica hello desiderato, scegliere hello **OK** pulsante.
10. Eseguire il progetto di servizio cloud di Azure in Visual Studio come di consueto. Quando si utilizza l'applicazione, informazioni di log di hello abilitate vengono salvate toohello account di archiviazione di Azure specificato.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Abilitare la diagnostica nelle macchine virtuali di Azure
In Visual Studio, è possibile scegliere i dati di diagnostica toocollect per macchine virtuali di Azure.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>diagnostica tooenable in macchine virtuali di Azure
1. In **Esplora Server**, scegliere il nodo Azure hello e quindi connettere tooyour sottoscrizione di Azure, se non è già connessi.
2. Espandere hello **macchine virtuali** nodo. È possibile creare una nuova macchina virtuale o selezionare una macchina virtuale già esistente.
3. Hello dal menu di scelta rapida per la macchina virtuale hello desiderato, scegliere **configura**. Mostra la finestra di dialogo di configurazione macchina virtuale hello.
   
    ![Configurazione di una macchina virtuale di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Se non è già stato installato, aggiungere l'estensione di diagnostica di Microsoft Monitoring Agent hello. Questa estensione consente di raccogliere dati di diagnostica per hello macchina virtuale di Azure. Nell'elenco di estensioni installate hello, scegliere il menu di selezionare un elenco a discesa estensione disponibile hello e quindi scegliere la diagnostica di Microsoft Monitoring Agent.
   
    ![Installazione di un'estensione di macchina virtuale di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Sono disponibili altre estensioni di diagnostica per le macchine virtuali. Per altre informazioni, vedere Estensioni VM e funzionalità di Azure.
   > 
   > 
5. Scegliere hello **Aggiungi** pulsante tooadd hello estensione e visualizzare il relativo **configurazione di diagnostica** la finestra di dialogo.
6. Scegliere hello **configura** toospecify un account di archiviazione e quindi scegliere hello **OK** pulsante.
   
    Ogni scheda, ad eccezione di **Generale** e **Directory log** rappresenta un'origine di dati di diagnostica che è possibile raccogliere.
   
    ![Abilitare la diagnostica e la configurazione di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    scheda predefinita Hello, **generale**, offre hello le seguenti opzioni di raccolta dati di diagnostica: **solo errori**, **tutte le informazioni**, e **piano personalizzato** . opzione predefinita, Hello **solo errori**, accetta hello quantità minima di spazio di archiviazione perché non trasferisce gli avvisi o messaggi di traccia. Hello **tutte le informazioni** opzione trasferimenti hello la maggior parte delle informazioni e, pertanto, hello più costosa in termini di archiviazione.
7. Per questo esempio, selezionare hello **piano personalizzato** opzione in modo è possibile personalizzare hello dati raccolti.
8. Hello **Quota disco in MB** casella Specifica la quantità di spazio da tooallocate dell'account di archiviazione per i dati di diagnostica. Se si desidera, è possibile modificare il valore di predefinito hello.
9. In ogni scheda dei dati di diagnostica desiderati toocollect, selezionare il **Abilita il trasferimento di <log type>**  casella di controllo.
   
    Ad esempio, se si desidera toocollect dei log applicazioni, selezionare hello **Abilita il trasferimento dei log applicazione** casella di controllo hello **log applicazioni** scheda. Specificare anche eventuali altre informazioni richieste da ogni tipo di dati di diagnostica. Vedere la sezione hello **configurare origini dati di diagnostica** più avanti in questo argomento per informazioni sulla configurazione di ogni scheda.
10. Dopo aver abilitato la raccolta di tutti i dati di diagnostica hello desiderato, scegliere hello **OK** pulsante.
11. Salvare il progetto aggiornato hello.
    
     Verrà visualizzato un messaggio hello **Log attività di Microsoft Azure** finestra hello macchina virtuale è stata aggiornata.

## <a name="configure-diagnostics-data-sources"></a>Configurare le origini dati di diagnostica
Dopo aver abilitato la raccolta dati di diagnostica, è possibile scegliere esattamente quali origini dati si desidera toocollect e i dati raccolti. Hello seguito è riportato un elenco delle schede nel hello **configurazione di diagnostica** la finestra di dialogo e significa che ogni opzione di configurazione.

### <a name="application-logs"></a>Log applicazioni
**Application logs** includono informazioni di diagnostica prodotte da un'applicazione Web. Se si desidera toocapture dei log applicazioni, selezionare hello **Abilita il trasferimento dei log applicazione** casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i log applicazioni hello tooyour account di archiviazione modificando hello **periodo di trasferimento (min)** valore. È inoltre possibile modificare quantità hello di informazioni acquisite nei log hello mediante l'impostazione di valore del livello di Log hello. Ad esempio, è possibile scegliere **Verbose** tooget ulteriori informazioni o scegliere **critico** toocapture soltanto degli errori critici. Se si dispone di un provider di diagnostica specifici che genera log applicazioni, è possibile acquisirli aggiungendo toohello GUID del provider di hello **GUID Provider** casella.

  ![Log applicazioni](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Per altre informazioni sui log applicazioni, vedere [Abilitare la registrazione diagnostica per le app Web del Servizio app di Azure](app-service-web/web-sites-enable-diagnostic-log.md).

### <a name="windows-event-logs"></a>Registri eventi di Windows
Se si desidera toocapture nei registri eventi di Windows, selezionare hello **Abilita trasferimento registri eventi di Windows** casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i registri eventi hello tooyour account di archiviazione modificando hello **periodo di trasferimento (min)** valore. Selezionare le caselle di controllo hello per i tipi di eventi che si desidera tootrack hello.

  ![Log eventi](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Se si usa Azure SDK 2.6 o versione successiva e si desidera toospecify un'origine dati personalizzata, immetterla hello  **<Data source name>**  testo, quindi scegliere hello **Aggiungi** tooit di pulsante Avanti. origine dati Hello viene aggiunto toohello cfcfg file.

Se si usa Azure SDK 2.5 e si desidera toospecify un'origine dati personalizzata, è possibile aggiungerla alla toohello `WindowsEventLog` sezione di hello wadcfgx file, ad esempio hello di esempio seguente.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Contatori delle prestazioni
Le informazioni sui contatori delle prestazioni possono semplificare l'individuazione dei colli di bottiglia e l'ottimizzazione delle prestazioni del sistema e delle applicazioni. Per altre informazioni, vedere [Creare e usare contatori di prestazioni in un'applicazione Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) . Se si desidera toocapture contatori delle prestazioni, selezionare hello **Abilita il trasferimento di contatori delle prestazioni** casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i registri eventi hello tooyour account di archiviazione modificando hello **periodo di trasferimento (min)** valore. Selezionare le caselle di controllo hello per hello contatori delle prestazioni che si desidera tootrack.

  ![Contatori delle prestazioni](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack un contatore delle prestazioni elencato, immetterlo utilizzando hello sintassi suggerita e quindi scegliere hello **Aggiungi** pulsante. il sistema operativo Hello nella macchina virtuale hello determina i contatori delle prestazioni è possibile tenere traccia. Per altre informazioni sulla sintassi, vedere [Specificare un percorso del contatore](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Log infrastruttura
Se si desidera che il log dell'infrastruttura toocapture, che contenga informazioni sul modulo RemoteForwarder hello, modulo RemoteAccess hello e hello dell'infrastruttura diagnostica di Azure, selezionare hello **Abilita il trasferimento di log dell'infrastruttura**casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i log di hello tooyour account di archiviazione modificando hello periodo di trasferimento (min) valore.

  ![Log dell'infrastruttura di diagnostica](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Per altre informazioni, vedere [Raccogliere dati di registrazione usando Diagnostica Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) .

### <a name="log-directories"></a>Directory log
Se si desidera che la directory log di toocapture, che contenga dati raccolti dalle directory di log per le richieste Internet Information Services (IIS), le richieste non riuscite o le cartelle selezionate, selezionare hello **Abilita il trasferimento di directory di Log**casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i log di hello tooyour account di archiviazione modificando hello **periodo di trasferimento (min)** valore.

È possibile selezionare le caselle di hello dei registri hello toocollect, si desidera, ad esempio **registri IIS** e **richieste non riuscite** log. Sono disponibili i nomi dei contenitori di archiviazione predefinito, ma se si desidera, è possibile modificare i nomi di hello.

È anche possibile acquisire log da qualsiasi cartella. Specificare solo il percorso di hello in hello **Log da Directory assoluta** sezione e quindi scegliere hello **Aggiungi Directory** pulsante. Hello log verranno acquisiti toohello specificato contenitori.

  ![Directory log](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Log ETW
Se si utilizza [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) e si desidera toocapture ai log ETW, seleziona hello **Abilita il trasferimento di log ETW** casella di controllo. È possibile aumentare o ridurre il numero di hello di minuti quando vengono trasferiti i log di hello tooyour account di archiviazione modificando hello **periodo di trasferimento (min)** valore.

gli eventi di Hello vengono acquisiti da origini evento e i manifesti eventi specificati. toospecify un'origine evento, immettere un nome in hello **origini evento** sezione e quindi scegliere hello **Aggiungi origine evento** pulsante. Analogamente, è possibile specificare un manifesto di eventi in hello **manifesti evento** sezione e quindi scegliere hello **Aggiungi manifesto evento** pulsante.

  ![Log ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  framework ETW Hello è supportato in ASP.NET tramite classi hello [System.Diagnostics.aspx] (spazio dei nomi https://msdn.microsoft.com/library/system.diagnostics (110). spazio dei nomi Microsoft.WindowsAzure.Diagnostics Hello, che eredita da ed estende standard (classi https://msdn.microsoft.com/library/system.diagnostics (110), consente di utilizzare hello di [System.Diagnostics.aspx] ([System.Diagnostics.aspx] https://msdn.microsoft.com/library/System.Diagnostics (110) come framework di registrazione nell'ambiente Azure hello. Per altre informazioni, vedere [Controllare la registrazione e la traccia in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [Abilitazione di Diagnostica in servizi cloud e macchine virtuali di Azure](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Dump di arresto anomalo del sistema
Se si desiderano toocapture informazioni quando si blocca un'istanza del ruolo, selezionare hello **Abilita il trasferimento di dump di arresto anomalo** casella di controllo. Poiché la maggior parte delle eccezioni è gestita da ASP.NET, questo è in genere utile solo per i ruoli di lavoro. È possibile aumentare o ridurre hello percentuale di spazio di archiviazione spazio dedicato toohello arresto anomalo del sistema modificando hello **Quota di Directory (%)** valore. È possibile modificare il contenitore dell'archivio hello in cui vengono memorizzati i dump di arresto anomalo hello ed è possibile selezionare se si desidera toocapture un **completo** o **Mini** dump.

vengono elencati i processi di Hello attualmente monitorati. Selezionare le caselle di controllo hello per i processi di hello che si desidera toocapture. tooadd elenco toohello a un altro processo, immettere il nome di processo hello e quindi scegliere hello **Aggiungi processo** pulsante.

  ![Dump di arresto anomalo del sistema](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Per altre informazioni, vedere [Controllare la registrazione e la traccia in Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [Diagnostica di Microsoft Azure - Parte 4: Personalizzare i componenti di registrazione e modifiche a Diagnostica di Azure 1.3](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/).

## <a name="view-hello-diagnostics-data"></a>Visualizza i dati di diagnostica hello
Dopo aver raccolto i dati di diagnostica hello per un servizio cloud o una macchina virtuale, è possibile visualizzarlo.

### <a name="tooview-cloud-service-diagnostics-data"></a>dati di diagnostica del servizio cloud tooview
1. Distribuire il servizio cloud come di consueto, quindi eseguirlo.
2. È possibile visualizzare i dati di diagnostica hello in un report generato da Visual Studio o le tabelle nell'account di archiviazione. dati hello tooview in un report, aprire **Cloud Explorer** o **Esplora Server**, aprire il menu di scelta rapida hello del nodo hello per ruolo hello desiderato e quindi scegliere **Visualizza dati di diagnostica** .
   
    ![Visualizza dati di diagnostica](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Viene visualizzato un report che mostra i dati disponibili hello.
   
    ![Report Diagnostica di Microsoft Azure in Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Se i dati più recenti di hello non viene visualizzata, potrebbe essere toowait per tooelapse periodo di trasferimento hello.
   
    Scegliere hello **aggiornamento** collegare tooimmediately aggiornamento hello dati o scegliere un intervallo hello **aggiornamento automatico** elenco a discesa elenco casella toohave hello i dati aggiornati automaticamente. dati di errore hello tooexport, scegliere hello **esportare tooCSV** pulsante toocreate un file con valori delimitati da virgole è possibile aprire un foglio di calcolo.
   
    In **Cloud Explorer** o **Esplora Server**, aprire l'account di archiviazione hello associata a una distribuzione di hello.
3. Aprire tabelle di diagnostica hello in Visualizzatore di tabelle hello e quindi esaminare i dati di hello raccolti. Per i log IIS e i log personalizzati sarà possibile aprire un contenitore BLOB. Rivedendo hello nella tabella seguente, è possibile trovare hello tabella o il contenitore blob che contiene dati hello desiderato. Inoltre toohello dati per tale file di log, le voci della tabella hello contengono EventTickCount, DeploymentId, ruolo e RoleInstance toohelp è identificare macchina virtuale e del ruolo generato dati hello e quando. 
   
   | Dati di diagnostica | Descrizione | Località |
   | --- | --- | --- |
   | Log applicazioni |Registra il codice genera l'errore chiamando i metodi della classe Trace hello. |WADLogsTable |
   | Log eventi |Questi dati provengono dai registri eventi di Windows hello in macchine virtuali hello. Informazioni sono archiviate in questi registri di Windows, ma servizi e applicazioni inoltre utilizzano tooreport errori o informazioni di registrazione. |WADWindowsEventLogsTable |
   | Contatori delle prestazioni |È possibile raccogliere dati su qualsiasi contatore delle prestazioni che è disponibile nella macchina virtuale hello. sistema operativo Hello fornisce contatori delle prestazioni, che includono molte statistiche, ad esempio il tempo di elaborazione e utilizzo della memoria. |WADPerformanceCountersTable |
   | Log infrastruttura |Questi log vengono generati dall'infrastruttura di diagnostica hello stesso. |WADDiagnosticInfrastructureLogsTable |
   | Log di IIS |Questi log registrano le richieste Web. Se il servizio cloud riceve una quantità significativa di traffico, questi log possono essere abbastanza lunghi. È quindi consigliabile raccogliere e archiviare questi dati solo quando necessario. |È possibile trovare i log di richieste non riuscite nel contenitore blob hello in wad-iis-failedreqlogs nel percorso per la distribuzione, ruolo e istanza. I log completi sono disponibili in wad-iis-logfiles. Per ogni file vengono immessi nella tabella WADDirectories hello. |
   | Dump di arresto anomalo del sistema |Queste informazioni forniscono immagini binarie del processo del servizio cloud, in genere un ruolo di lavoro. |Contenitore BLOB wad-crush-dumps |
   | File di log personalizzati |Registra i dati definiti dall'utente. |È possibile specificare nel percorso di codice hello dei file di log personalizzati nell'account di archiviazione. Ad esempio, è possibile specificare un contenitore BLOB personalizzato. |
4. Se qualsiasi tipo di dati viene troncati, è possibile provare a incremento buffer hello per tale tipo di dati o la riduzione dell'intervallo hello tra i trasferimenti di dati dall'account di archiviazione tooyour hello macchina virtuale.
5. (facoltativo) In alcuni casi ripulitura dati dall'archiviazione hello account tooreduce i costi di archiviazione complessivo.
6. Quando si esegue una distribuzione completa, file Diagnostics cscfg hello (con estensione wadcfgx per Azure SDK 2.5) viene aggiornato in Azure e il servizio cloud rileva qualsiasi configurazione della diagnostica tooyour le modifiche. Se, invece, aggiorna una distribuzione esistente, i file con estensione cscfg hello non viene aggiornato in Azure. È comunque possibile modificare le impostazioni di diagnostica, tuttavia, seguendo i passaggi di hello nella sezione successiva hello. Per altre informazioni sull'esecuzione di una distribuzione completa e sull'aggiornamento di una distribuzione esistente, vedere [Procedura guidata Pubblica l'applicazione Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>dati di diagnostica tooview macchina virtuale
1. Scegliere hello dal menu di scelta rapida per la macchina virtuale hello, **Visualizza dati di diagnostica**.
   
    ![Visualizzare i dati di diagnostica nella macchina virtuale di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Verrà visualizzata hello **riepilogo diagnostica** finestra.
   
    ![Riepilogo di diagnostica della macchina virtuale di Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Se i dati più recenti di hello non viene visualizzata, potrebbe essere toowait per tooelapse periodo di trasferimento hello.
   
    Scegliere hello **aggiornamento** collegare tooimmediately aggiornamento hello dati o scegliere un intervallo hello **aggiornamento automatico** elenco a discesa elenco casella toohave hello i dati aggiornati automaticamente. dati di errore hello tooexport, scegliere hello **esportare tooCSV** pulsante toocreate un file con valori delimitati da virgole è possibile aprire un foglio di calcolo.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Configurare la diagnostica del servizio cloud dopo la distribuzione
Se si sta verificando un problema con un servizio cloud già in esecuzione, è possibile toocollect dati che non hai specificato prima di ruolo è distribuito originariamente hello. In questo caso, è possibile avviare toocollect che i dati utilizzando le impostazioni di hello in Esplora Server. È possibile configurare la diagnostica per una singola istanza o tutte le istanze di hello in un ruolo, a seconda se si apre la finestra di dialogo di configurazione di diagnostica hello dal menu di scelta rapida hello istanza hello o al ruolo hello. Se si configura il nodo di ruolo hello, le modifiche vengono applicate istanze tooall. Se si configura il nodo di istanza hello, le modifiche vengono applicate solo l'istanza toothat.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>diagnostica tooconfigure per un servizio cloud in esecuzione
1. In Esplora Server espandere hello **servizi Cloud** nodo, quindi espandere i nodi toolocate hello ruolo o istanza che si desidera tooinvestigate o entrambi.
   
    ![Configurazione di Diagnostica](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Hello dal menu di scelta rapida per un nodo di istanza o un ruolo, scegliere **Aggiorna impostazioni di diagnostica**, quindi scegliere le impostazioni di diagnostica che si desidera toocollect hello.
   
    Per informazioni sulle impostazioni di configurazione di hello, vedere **configurare origini dati di diagnostica** in questo argomento. Per informazioni su come tooview hello dati di diagnostica, vedere **visualizzare dati di diagnostica hello** in questo argomento.
   
    Se si modifica la raccolta di dati in **Esplora server**, tali modifiche rimarranno validi fino a una nuova distribuzione completa del servizio cloud. Se si utilizza le impostazioni di pubblicazione predefinito hello modifiche hello non vengono sovrascritte, poiché di pubblicazione predefinito hello impostazione tooupdate distribuzione esistente di hello, anziché eseguire una ridistribuzione completa. impostazioni hello che toomake cancellate al momento della distribuzione, passa toohello **impostazioni avanzate** scheda nella procedura guidata di pubblicazione hello e crittografato hello **aggiornamento distribuzione** casella di controllo. Quando esegue la ridistribuzione con tale casella di controllo deselezionata, le impostazioni di hello ripristino toothose nel file con estensione wadcfgx (o wadcfg) di hello impostate tramite l'editor delle proprietà per il ruolo di hello hello. Se si aggiorna la distribuzione, Azure mantiene le impostazioni precedenti hello.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Risolvere i problemi del servizio cloud di Azure
Se si verificano problemi con i progetti servizio cloud, ad esempio un ruolo bloccato nello stato "occupato", più volte viene riciclato o genera un errore interno del server, sono disponibili strumenti e tecniche è possibile utilizzare toodiagnose e risolvere questi problemi. Per esempi specifici di problemi e soluzioni comuni, nonché una panoramica dei concetti di hello e strumenti utilizzati toodiagnose e risolvere tali errori, vedere [dati di diagnostica di calcolo di Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Domande e risposte
**Che cos'è una dimensione del buffer hello e devono essere grandi come?**

In ogni istanza di macchina virtuale, le quote limitano la quantità di dati diagnostici possono essere archiviati hello file System locale. È anche possibile specificare una dimensione del buffer per ogni tipo di dato di diagnostica disponibile. Tale dimensione del buffer funge da quota individuale per quel tipo di dati. Selezionando la finestra di dialogo hello di fondo hello, è possibile determinare hello quota complessiva e la quantità di hello di memoria rimanente. Se si specificano buffer più grandi o più tipi di dati, verrà usata hello quota complessiva. È possibile modificare hello quota complessiva modificando i file di configurazione diagnostics.wadcfg/.wadcfgx hello. diagnostica Hello dati vengono archiviati in hello stesso file System dei dati dell'applicazione, pertanto se l'applicazione utilizza una grande quantità di spazio su disco, è consigliabile non aumentare hello quota complessiva di diagnostica.

**Che cos'è il periodo di trasferimento hello e quanto tempo deve essere?**

periodo di trasferimento Hello è hello periodo di tempo che trascorre tra i dati acquisiti. Dopo ogni periodo di trasferimento, i dati vengono spostati dal file System locale hello in una macchina virtuale tootables nell'account di archiviazione. Se hello di dati raccolti supera la quota hello prima fine hello del periodo di trasferimento, è possibile che i dati meno recenti vengono eliminati. È il periodo di trasferimento hello toodecrease se si sta perdita di dati perché i dati superano le dimensioni del buffer di hello o hello quota complessiva.

**Quale fuso orario sono hello timestamp in?**

Hello time stamp sono fuso orario locale hello del centro dati hello che ospita il servizio cloud. Hello seguenti tre colonne di tipo timestamp nelle tabelle di log hello vengono utilizzate.

* **PreciseTimeStamp** hello ETW timestamp dell'evento hello. Vale a dire evento hello hello viene registrato dal client hello.
* **TIMESTAMP** viene PreciseTimeStamp arrotondato per difetto toohello limite di frequenza di caricamento. In tal caso, se la frequenza di caricamento è 5 minuti ed evento hello ora 00:17:12, TIMESTAMP sarà 00:15:00.
* **Timestamp** hello timestamp in cui hello entità è stata creata in hello tabelle di Azure.

**Come si gestiscono i costi durante la raccolta delle informazioni di diagnostica?**

Hello le impostazioni predefinite (**livello di registrazione** impostare troppo**errore** e **periodo di trasferimento** impostare troppo**1 minuto**) sono progettate toominimize costo. Il calcolo dei costi aumenta se raccogliere più dati di diagnostica o ridurre il periodo di trasferimento hello. Non raccogliere più dati del necessario e non dimenticare la raccolta dei dati toodisable quando non è più necessario. È possibile sempre abilitarlo nuovamente, anche in fase di esecuzione, come illustrato nella sezione precedente hello.

**Come si raccolgono log relativi alle richieste non riuscite da IIS?**

Per impostazione predefinita, IIS non raccoglie log relativi alle richieste non riuscite. È possibile configurare IIS toocollect loro se si modifica hello file Web. config per il ruolo web.

**Non si ottengono informazioni di traccia dai metodi RoleEntryPoint quali OnStart. Qual è il problema?**

metodi di Hello di RoleEntryPoint vengono chiamati nel contesto di hello di WAIISHost.exe e non di IIS. Pertanto, hello le informazioni di configurazione Web. config che normalmente abilita la traccia non è valida. tooresolve questo problema, aggiungere un progetto di ruolo web. config file tooyour e nome hello file toomatch hello output assembly che contiene il codice di RoleEntryPoint hello. Nel progetto di ruolo web predefinito hello, il nome di hello del file con estensione config hello sarebbe Waiishost.exe. Aggiungere quindi hello seguenti righe toothis file:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

A questo punto, in hello **proprietà** finestra, hello set **copiare tooOutput Directory** proprietà troppo**Copia sempre**.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su Diagnostica registrazione in Azure, vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](cloud-services/cloud-services-dotnet-diagnostics.md) e [abilitare la registrazione diagnostica per le app web in Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).

