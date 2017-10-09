<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>L'aggiornamento di SharePoint 2010 tooSharePoint 2013 e quindi installare hello StorSomple Adapter per SharePoint
> [!IMPORTANT]
> Tutti i file precedentemente spostati archiviazione tooexternal tramite RBS non saranno disponibili fino al termine aggiornamento hello e hello funzionalità RBS riabilitata. utente toolimit sulle, eseguire qualsiasi aggiornamento o reinstallazione durante una finestra di manutenzione pianificata.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade 2010 a SharePoint 2013 e quindi installare hello adapter
1. Nella farm di SharePoint 2010 hello, nota hello BLOB archiviare percorso per hello esternalizzata i BLOB e database del contenuto hello per cui RBS è abilitato. 
2. Installare e configurare la nuova farm di SharePoint 2013 hello. 
3. Spostare le raccolte siti, applicazioni e i database da SharePoint 2010 hello farm toohello nuova farm di SharePoint 2013. Per istruzioni, vedere troppo[Panoramica del processo di aggiornamento di hello tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Installare hello adattatore StorSimple per SharePoint nella nuova farm hello. Andare troppo[hello di installazione dell'adattatore StorSimple per SharePoint](#install-the-storsimple-adapter-for-sharepoint) per le procedure.
5. Utilizzare informazioni hello annotato nel passaggio 1 per abilitare RBS per hello stesso set di database del contenuto e forniscono l'archivio di BLOB stesso percorso utilizzato nell'installazione di SharePoint 2010 hello hello. Andare troppo[configurare RBS](#configure-rbs) per le procedure. Dopo aver completato questo passaggio, è possibile che i file esternalizzati in precedenza devono essere accessibili dalla nuova farm hello. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Aggiornare hello adattatore StorSimple per SharePoint
> [!IMPORTANT]
> È consigliabile pianificare questa toooccur aggiornamento durante una finestra di manutenzione pianificata per hello seguenti motivi:
> 
> * In precedenza il contenuto esternalizzato non sarà disponibile fino a quando non viene reinstallato adapter hello.
> * Qualsiasi contenuto caricato sito toohello dopo disinstalla una versione precedente di hello di hello adattatore StorSimple per SharePoint, ma prima di installare una nuova versione hello, verrà archiviato nel database del contenuto hello. Sarà necessario toomove dispositivo StorSimple toohello contenuto dopo aver installato il nuovo adapter di hello. È possibile utilizzare Microsoft hello` RBS Migrate()` cmdlet di PowerShell incluso nel contenuto di SharePoint toomigrate hello. Per ulteriori informazioni, vedere [Migrazione del contenuto in o da RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>hello tooupgrade adattatore StorSimple per SharePoint
1. Disinstallare una versione precedente di hello dell'adattatore StorSimple per SharePoint.
   
   > [!NOTE]
   > Verrà automaticamente disabilitato RBS nel database del contenuto hello. Tuttavia, BLOB esistenti rimarranno nel dispositivo StorSimple hello. Poiché RBS è disabilitata e hello BLOB non sono stati migrati toohello indietro i database del contenuto, tutte le richieste per tali BLOB avranno esito negativo. 
   > 
   > 
2. Installazione hello nuovo adattatore StorSimple per SharePoint. nuovo adattatore Hello riconoscerà automaticamente i database del contenuto hello che sono stati precedentemente abilitati o disabilitati per RBS e userà le impostazioni precedenti hello.

