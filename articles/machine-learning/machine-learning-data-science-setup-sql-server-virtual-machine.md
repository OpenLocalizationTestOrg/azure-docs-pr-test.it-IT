---
title: aaaSet rapidamente una macchina virtuale di SQL Server come server IPython Notebook | Documenti Microsoft
description: Configurazione di una macchina virtuale per l'analisi scientifica dei dati con SQL Server e IPython Server.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurare una macchina virtuale SQL Server di Azure come server IPython Notebook per l'analisi avanzata
Questo argomento viene illustrato come tooprovision e configurare un toobe macchina virtuale di SQL Server utilizzato come parte di un ambiente di analisi scientifica dei dati basati su cloud. macchina virtuale di Windows Hello è configurato con supporto di strumenti, ad esempio IPython Notebook, Azure Storage Explorer, AzCopy, nonché altre utilità che sono utili per i progetti di analisi scientifica dei dati. Azure Storage Explorer e AzCopy, ad esempio, fornire agevolmente archiviazione blob di tooAzure tooupload dati dal computer locale o toodownload è tooyour locali dall'archiviazione blob.

raccolta di macchine virtuali di Azure Hello include diverse immagini contenenti Microsoft SQL Server. Selezionare l'immagine di una macchina virtuale di SQL Server adatta alle esigenze dei dati di cui si dispone. Di seguito sono riportate le immagini consigliate:

* SQL Server 2012 SP2 Enterprise per le dimensioni dei dati di piccole dimensioni toomedium
* SQL Server 2012 SP2 Enterprise con ottimizzazione per carichi di lavoro di DataWarehouse per toovery di grandi dimensioni di dati di grandi dimensioni
  
  > [!NOTE]
  > L'immagine di SQL Server 2012 SP2 Enterprise **non include un disco dati**. Si sarà necessario tooadd e/o collegare uno o più toostore di dischi rigidi virtuali dei dati. Quando si crea una macchina virtuale di Azure, è un disco per unità di toohello C del sistema operativo eseguito il mapping di hello e un'unità di toohello D disco temporaneo mappato. Non utilizzare hello D unità toostore dati. Come suggerisce il nome di hello, fornisce esclusivamente all'archiviazione temporanea. Non offre funzionalità di ridondanza o backup perché non risiede nel servizio di archiviazione di Azure.
  > 
  > 

## <a name="Provision"></a>Toohello portale classico di Azure di connettersi ed eseguire il provisioning di una macchina virtuale di SQL Server
1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com/) con l'account.
   Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
2. Nel portale di Azure classico hello, a sinistra di hello nella parte inferiore della pagina web hello, fare clic su **+ nuovo**, fare clic su **calcolo**, fare clic su **macchina virtuale**, quindi fare clic su **FROM RACCOLTA**.
3. In hello **creare una macchina virtuale** pagina, selezionare un'immagine di macchina virtuale contenente SQL Server in base alle proprie esigenze di dati e quindi fare clic sulla freccia avanti hello nella parte inferiore destra della pagina hello. Per informazioni più aggiornate di hello in hello supportate immagini di SQL Server in Azure, vedere [Introduzione a SQL Server in macchine virtuali di Azure](http://go.microsoft.com/fwlink/p/?LinkId=294720) argomento hello [SQL Server in macchine virtuali di Azure](http://go.microsoft.com/fwlink/p/?LinkId=294719) set di documentazione.
   
   ![Selezionare la macchina virtuale SQL Server][1]
4. In hello prima **configurazione della macchina virtuale** pagina, fornire le informazioni seguenti:
   
   * Specificare un nome in **NOME MACCHINA VIRTUALE**.
   * In hello **nuovo nome utente** casella, il nome utente univoco di tipo per hello account amministratore locale della macchina virtuale.
   * In hello **nuova PASSWORD** , digitare una password complessa. Per ulteriori informazioni, vedere [Password complesse](http://msdn.microsoft.com/library/ms161962.aspx).
   * In hello **conferma PASSWORD** casella, digitare nuovamente la password hello.
   * Seleziona hello appropriato **dimensioni** da hello nell'elenco a discesa.
     
     > [!NOTE]
     > dimensioni Hello della macchina virtuale hello viene specificata durante il provisioning: A2 hello dimensione è minima consigliata per i carichi di lavoro. Le dimensioni minime consigliate per una macchina virtuale corrispondono ad A3 quando si usa SQL Server Enterprise Edition. Selezionare A3 o un valore superiore per l'uso di SQL Server Enterprise Edition. Selezionare A4 per l'uso di immagini di SQL Server 2012 o 2014 Enterprise ottimizzato per carichi di lavoro transazionali.
     > Selezionare A7 per l'uso di immagini di SQL Server 2012 o 2014 Enterprise ottimizzato per carichi di lavoro di data warehouse. dimensione Hello selezionata limita il numero di dischi dati, che è possibile configurare. Per informazioni più aggiornate sulle dimensioni delle macchine virtuali disponibili e il numero di hello di dischi dati che è possibile collegare macchina virtuale tooa, vedere [dimensioni delle macchine virtuali per Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Per informazioni sui prezzi, vedere [Macchine virtuali - Prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Fare clic sulla freccia avanti hello in hello nella parte inferiore destra toocontinue.
   
   ![Configurazione macchina virtuale][2]
5. In hello secondo **configurazione della macchina virtuale** pagina, configurare le risorse di rete, archiviazione e la disponibilità:
   
   * In hello **servizio Cloud** scegliere **creare un nuovo servizio cloud**.
   * In hello **nome DNS del servizio Cloud** casella, specificare hello prima parte del nome DNS desiderato, in modo che completi un nome nel formato **TESTNAME.cloudapp.net**
   * In hello **AFFINITÀ di area/gruppo/rete virtuale** , selezionare un'area in cui verrà ospitata questa immagine virtuale.
   * In hello **Account di archiviazione**, selezionare un account di archiviazione esistente o selezionarne uno generato automaticamente.
   * In hello **SET di disponibilità** , quindi selezionare **(nessuno)**.
   * Leggere e accettare hello informazioni sui prezzi.
6. In hello **endpoint** fare clic su nell'elenco a discesa vuoto hello in **nome**e selezionare **MSSQL** quindi digitare il numero di porta hello dell'istanza del motore di Database (hello**1433** per l'istanza predefinita di hello).
7. La macchina virtuale di SQL Server può inoltre essere utilizzata come server di IPython Notebook, che verrà configurato in un momento successivo.
   Aggiungere un nuovo toouse porta hello di toospecify endpoint per il server di IPython Notebook. Immettere un nome in hello **nome** colonna, selezionare un numero di porta desiderato per la porta pubblica hello e 9999 per la porta privata hello.
   
   Fare clic sulla freccia avanti hello in hello nella parte inferiore destra toocontinue.
   
   ![Selezionare le porte MSSQL e IPython][3]
8. Accettare l'impostazione predefinita hello **agente VM installato** opzione è selezionata e fare clic su hello hello segno di spunta nell'angolo in basso hello della hello toocomplete tramite procedura guidata hello processo di provisioning di macchine Virtuali.
   
   `![Opzioni finali della macchina virtuale][4]
9. Attendere durante la preparazione della macchina virtuale in Azure. Previsto tooproceed stato macchina virtuale di hello tramite:
   
   * Starting (Provisioning)
   * Arrestato
   * Starting (Provisioning)
   * Running (Provisioning)
   * In esecuzione

## <a name="RemoteDesktop"></a>Aprire hello virtual machine tramite Desktop remoto e completare la configurazione
1. Quando al termine del provisioning, fare clic sul nome di hello della pagina DASHBOARD toohello toogo macchina virtuale. Nella parte inferiore di hello della pagina hello, fare clic su **Connetti**.
2. Scegliere tooopen hello rpd file utilizzando il programma di Desktop remoto di Windows hello (`%windir%\system32\mstsc.exe`).
3. In hello **la sicurezza di Windows** finestra di dialogo, fornire la password di hello per l'account amministratore locale specificato in un passaggio precedente.
   (Potrebbe essere necessario credenziali hello tooverify della macchina virtuale hello.)
4. Hello prima volta che accede nella macchina virtuale toothis diversi processi potrebbe essere necessario toocomplete, tra cui il programma di installazione del desktop, gli aggiornamenti di Windows e il completamento dell'attività di configurazione iniziale di Windows hello (sysprep). Al termine delle attività di configurazione iniziali di Windows, verranno completate le attività di configurazione di SQL Server. Queste attività potrebbero causare un ritardo di pochi minuti mentre vengono completate. `SELECT @@SERVERNAME`non può restituire il nome corretto hello fino a quando non viene completata l'installazione di SQL Server e SQL Server Management Studio potrebbe non essere visibile nella pagina iniziale di hello.

Una volta toohello connessa la macchina virtuale con Desktop remoto di Windows, hello macchina virtuale funziona come qualsiasi altro computer. Connettersi toohello di istanza predefinita di SQL Server con SQL Server Management Studio (in esecuzione nella macchina virtuale hello) in hello normalmente.

## <a name="InstallIPython"></a>Installare IPython Notebook e altri strumenti di supporto
tooconfigure il nuovo tooserve macchina virtuale SQL Server come server IPython Notebook e installazione di supporto aggiuntive degli strumenti tali AzCopy, Azure Storage Explorer, pacchetti Python di analisi scientifica dei dati utili e ad altri utenti, uno script di personalizzazione speciale viene fornito tooyou. tooinstall:

1. Pulsante destro del mouse hello **Start di Windows** icona e fare clic su **prompt dei comandi (amministrazione)**
2. Comandi seguenti di hello di copia e Incolla, al prompt dei comandi di hello.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Quando richiesto, immettere una password di propria scelta per hello server IPython Notebook.
4. script di personalizzazione Hello automatizza varie procedure post-installazione, tra cui:
    * Installazione e configurazione del server di IPython Notebook
    * Apertura di porte TCP in hello Windows firewall per endpoint hello creato in precedenza:
    * Per la connessione remota di SQL Server
    * Per la connessione remota del server di IPython Notebook
    * Recupero di blocchi appunti IPython e script SQL di esempio
    * Download e installazione di pacchetti Python per l'analisi scientifica dei dati
    * Download e installazione di strumenti Azure come AzCopy ed Esplora archivi Azure   
    <br>
5. È possibile accedere ed eseguire IPython Notebook da qualsiasi browser locale o remoto utilizzando un URL di form hello `https://<virtual_machine_DNS_name>:<port>`, in cui la porta è pubblica porta selezionato durante il provisioning di macchina virtuale hello IPython hello.
6. Server IPython Notebook è in esecuzione come servizio in background e verrà riavviato automaticamente quando si riavvia una macchina virtuale hello.

## <a name="Optional"></a>Collegare un disco dati secondo necessità
Se l'immagine di macchina virtuale include dischi dati, ad esempio, i dischi diversi da unità C (disco del sistema operativo) e l'unità D (disco temporaneo), è necessario tooadd uno o più dati dischi toostore i dati. immagine della macchina virtuale per SQL Server 2012 SP2 Enterprise con ottimizzazione per carichi di lavoro DataWarehouse Hello è preconfigurata con dischi aggiuntivi per i file di dati e di log di SQL Server.

> [!NOTE]
> Non utilizzare hello D unità toostore dati. Come suggerisce il nome di hello, fornisce esclusivamente all'archiviazione temporanea. Non offre funzionalità di ridondanza o backup perché non risiede nel servizio di archiviazione di Azure.
> 
> 

i dischi dati aggiuntivi tooattach, seguire i passaggi di hello descritti in [come tooAttach tooa un disco dati macchina virtuale Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), che consentono di:

1. Collegamento di macchina virtuale di dischi vuoti toohello provisioning nei passaggi precedenti
2. Inizializzazione di hello nuovi dischi nella macchina virtuale hello

## <a name="SSMS"></a>Connettersi tooSQL Server Management Studio e abilitare l'autenticazione modalità mista
Hello il motore di Database di SQL Server non è possibile utilizzare l'autenticazione di Windows senza l'ambiente di dominio. tooconnect toohello motore di Database da un altro computer, configurare SQL Server per l'autenticazione modalità mista. L'autenticazione in modalità mista consente sia l'autenticazione di SQL Server sia l'autenticazione di Windows. Modalità di autenticazione SQL è necessaria nei dati tooingest ordine direttamente dal database nella macchina virtuale SQL Server il [Azure Machine Learning Studio](https://studio.azureml.net) usando il modulo di importazione dei dati hello.

1. Durante la macchina virtuale di toohello connessi tramite Desktop remoto, usare Windows hello **ricerca** riquadro e tipo **SQL Server Management Studio** (SMSS). Fare clic su hello toostart SQL Server Management Studio (SSMS). È opportuno tooadd tooSSMS un collegamento sul Desktop per utilizzi futuri.
   
   ![Avvio di SQL Server Management Studio][5]
   
   Hello prima apertura di Management Studio, è necessario creare l'ambiente di hello utenti Management Studio. L'operazione potrebbe richiedere alcuni istanti.
2. Quando si apre, Management Studio presenta hello **connettersi tooServer** la finestra di dialogo. In hello **nome Server** casella, il nome del tipo hello di hello macchina virtuale tooconnect toohello motore di Database con hello Esplora oggetti.
   (Anziché il nome di macchina virtuale hello è inoltre possibile utilizzare **(local)** o un singolo periodo come hello **nome Server**. Selezionare **l'autenticazione di Windows**, lasciando  ***il\_VM\_nome*\\il\_locale\_amministratore**  in hello **nome utente** casella. Fare clic su **Connetti**.
   
   ![Connettersi tooServer][6]
   
   <br>
   
   > [!TIP]
   > È possibile modificare la modalità di autenticazione SQL Server hello mediante una modifica della chiave del Registro di sistema Windows o SQL Server Management Studio hello. modalità di autenticazione toochange con cambio di una chiave del Registro di sistema hello, avviare un **nuova Query** ed eseguire lo script seguente hello:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    modalità di autenticazione hello toochange utilizzando SQL Server management Studio:

1. In **Esplora oggetti di SQL Server Management Studio**, fare doppio clic sul nome dell'istanza di hello di SQL Server (nome della macchina virtuale hello) e quindi fare clic su **proprietà**.
   
   ![Proprietà del server][7]
2. In hello **sicurezza** pagina **l'autenticazione Server**selezionare **modalità di autenticazione di Windows e SQL Server**e quindi fare clic su **OK** .
   
   ![Selezione della modalità di autenticazione][8]
3. In hello **SQL Server Management Studio** la finestra di dialogo, fare clic su **OK** per riconoscere hello requisito toorestart SQL Server.
4. In **Esplora oggetti** fare clic con il pulsante destro del mouse sul server e quindi scegliere **Riavvia**. (Se SQL Server Agent è in esecuzione, anch'esso dovrà essere riavviato).
   
   ![Riavvia][9]
5. In hello **SQL Server Management Studio** la finestra di dialogo, fare clic su **Sì** per accettare che si desidera toorestart SQL Server.

## <a name="Logins"></a>Creare gli account di accesso di SQL Server
tooconnect toohello motore di Database da un altro computer, è necessario creare almeno un accesso con autenticazione SQL Server.  

È possibile creare nuovi account di accesso di SQL Server a livello di programmazione o utilizzando hello SQL Server Management Studio. toocreate un nuovo utente sysadmin con autenticazione di SQL Server a livello di codice avvia un **nuova Query** ed eseguire lo script seguente hello. Sostituire <new user name\> e <new password\> con il *nome utente* e la *password* da usare. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Modificare i criteri password hello in base alle esigenze (codice di esempio hello viene disattivata la scadenza di criteri di controllo e la password). Per ulteriori informazioni sugli account di accesso di SQL Server, vedere [Creazione di un account di accesso](http://msdn.microsoft.com/library/aa337562.aspx).  

toocreate nuovi accessi di SQL Server utilizzando SQL Server Management Studio hello:

1. In **Esplora oggetti di SQL Server Management Studio**, espandere la cartella hello hello dell'istanza del server in cui si desidera toocreate hello nuovo account di accesso.
2. Pulsante destro del mouse hello **sicurezza** cartella, scegliere troppo**nuovo**e selezionare **account di accesso...** .
   
   ![Nuovo account di accesso][10]
3. In hello **accesso - nuovo** della finestra di dialogo hello **generale** pagina, immettere il nome di hello del nuovo utente hello in hello **nome account di accesso** casella.
4. Selezionare **Autenticazione di SQL Server**.
5. In hello **Password** casella, immettere una password per hello nuovo utente. Immettere nuovamente quella password in hello **Conferma Password** casella.
6. Selezionare le opzioni dei criteri password tooenforce per complessità e l'applicazione, **Applica criteri password** (scelta consigliata). Si tratta di un'opzione predefinita quando si seleziona l'autenticazione di SQL Server.
7. Selezionare le opzioni dei criteri password tooenforce per la scadenza, **Imponi scadenza password** (scelta consigliata). Applica criteri password deve essere tooenable selezionata questa casella di controllo. Si tratta di un'opzione predefinita quando si seleziona l'autenticazione di SQL Server.
8. tooforce hello utente toocreate viene utilizzata una nuova password dopo hello prima volta che l'account di accesso, selezionare **cambiamento obbligatorio password all'accesso successivo** (opzione consigliata se l'account di accesso è per un utente toouse else. Se l'account di accesso di hello è per uso personale, non selezionare questa opzione.) Imponi scadenza password deve essere tooenable selezionata questa casella di controllo. Si tratta di un'opzione predefinita quando si seleziona l'autenticazione di SQL Server.
9. Da hello **database predefinito** , selezionare un database predefinito per l'account di accesso hello. **master** hello predefinito per questa opzione. Se non è ancora stato creato un database utente, lasciare questa impostazione è troppo**master**.
10. In hello **Default language** elenco, lasciare **predefinito** come valore di hello.
    
    ![Proprietà account di accesso][11]
11. Nel caso di accesso di hello prima che si sta creando, si desidera definire l'account di accesso come amministratore di SQL Server. A questo scopo, nella pagina **Ruoli server** selezionare **sysadmin**.
    
    > [!IMPORTANT]
    > I membri del ruolo predefinito del server sysadmin di hello sono controllo completo di hello motore di Database. Per motivi di sicurezza, è opportuno limitare attentamente le appartenenze a questo ruolo.
    > 
    > 
    
    ![sysadmin][12]
12. Fare clic su OK.

## <a name="DNS"></a>Determinare il nome DNS hello della macchina virtuale hello
tooconnect toohello, il motore di Database di SQL Server da un altro computer, è necessario conoscere hello sistema DNS (Domain Name) nome della macchina virtuale hello.

(Si tratta di hello Nome hello internet utilizza tooidentify hello macchina virtuale. È possibile utilizzare l'indirizzo IP di hello, ma l'indirizzo IP hello potrebbe cambiare quando Azure consente di spostare risorse per la ridondanza o la manutenzione. nome DNS Hello sarà stabile perché può essere reindirizzato tooa nuovo indirizzo IP.)

1. Nel portale di Azure classico hello (o dal passaggio precedente hello), selezionare **macchine VIRTUALI**.
2. In hello **istanze di macchine VIRTUALI** pagina hello **nome DNS** colonna di ricerca e copia nome hello DNS per la macchina virtuale hello visualizzato preceduto da **http://**. (interfaccia utente di hello potrebbe non essere visualizzati nome intero hello, ma è possibile fare doppio clic su di esso e scegliere Copia.)

## <a name="cde"></a>Connettersi toohello motore di Database da un altro computer
1. In un computer connesso toohello internet, aprire SQL Server Management Studio.
2. In hello **connettersi tooServer** o **connettersi tooDatabase motore** della finestra di dialogo hello **nome Server** , immettere il nome DNS hello della macchina virtuale (determinata hello attività precedente) e un numero di porta endpoint pubblico nel formato hello *Nomedns, NumeroPorta* , ad esempio **tutorialtestVM.cloudapp.net,57500**.
3. In hello **autenticazione** , quindi selezionare **autenticazione di SQL Server**.
4. In hello **accesso** casella, il nome del tipo hello di un account di accesso è stato creato in un'attività precedente.
5. In hello **Password** casella, digitare la password dell'account di accesso di hello creati in un'attività precedente hello.
6. Fare clic su **Connetti**.

## <a name="amlconnect"></a>Connettersi toohello motore di Database da Azure Machine Learning
In fasi successive della hello processo di analisi scientifica dei dati di Team, si utilizzerà hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild e distribuire modelli di machine learning. tooingest dati dal database di macchina virtuale SQL Server direttamente in Azure Machine Learning per training o la valutazione, utilizzare hello **l'importazione dei dati** modulo in un nuovo [Azure Machine Learning Studio](https://studio.azureml.net) provare. Questo argomento viene descritto in dettaglio tramite hello collegamenti di Guida di processo di analisi scientifica dei dati del Team. Per un'introduzione, vedere [Informazioni su Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md).

1. In hello **proprietà** riquadro di hello [modulo Importa dati](https://msdn.microsoft.com/library/azure/dn905997.aspx)selezionare **Database SQL di Azure** da hello **origine dati** elenco a discesa.
2. In hello **nome server Database** testo immettere`tcp:<DNS name of your virtual machine>,1433`
3. Immettere nome utente SQL hello in hello **nome dell'account utente Server** casella di testo.
4. Immettere la password dell'utente sql hello in hello **password dell'account utente Server** casella di testo.
   
   ![Dati di importazione di Azure Machine Learning][13]

## <a name="shutdown"></a>Arresto e deallocazione della macchina virtuale quando non in uso
Macchine virtuali di Azure è disponibile con **pagamento a consumo**. tooensure che non vengono fatturate quando non si utilizza la macchina virtuale, è toobe in hello **arrestato (deallocato)** stato.

> [!NOTE]
> Arresto della macchina virtuale hello da all'interno (tramite Opzioni risparmio energia di Windows), hello macchina virtuale è stato arrestato ma rimane allocata. tooensure non viene addebitata, sempre arrestare le macchine virtuali da hello [portale di Azure classico](http://manage.windowsazure.com/). È anche possibile arrestare hello VM tramite Powershell chiamando ShutdownRoleOperation con uguale a "PostShutdownAction" troppo "StoppedDeallocated".
> 
> 

tooshutdown e deallocare una macchina virtuale hello:

1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com/) con l'account.  
2. Selezionare **macchine VIRTUALI** dalla barra di spostamento a sinistra di hello.
3. Nell'elenco di hello delle macchine virtuali, fare clic sul nome hello la macchina virtuale, quindi passa toohello **DASHBOARD** pagina.
4. Nella parte inferiore di hello della pagina hello, fare clic su **arresto**.

![Arresto della macchina virtuale][15]

macchina virtuale Hello verranno deallocata ma non eliminato. È possibile riavviare la macchina virtuale in qualsiasi momento da hello portale classico di Azure.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>La macchina virtuale di Azure SQL Server è pronto toouse: che cos'è successivo?
La macchina virtuale è ora pronto toouse negli esercizi di analisi scientifica dei dati. macchina virtuale Hello è pronto per l'utilizzo come un server di IPython Notebook per l'elaborazione dei dati e l'esplorazione di hello e altre attività in combinazione con Azure Machine Learning e hello Team Data Science processo (TDSP).

Hello passaggi successivi nel processo di analisi scientifica dei dati hello vengono eseguito il mapping in hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere passaggi spostare i dati in HDInsight, processo e, di esempio in preparazione per l'apprendimento dai dati hello con Azure macchina Apprendimento.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

