<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Quando si apportano modifiche toohello adattatore StorSimple per la configurazione di SharePoint RBS, è necessario essere connessi con un account utente appartenente al gruppo Domain Admins toohello. Inoltre, è necessario accedere pagina Configurazione hello da un browser in esecuzione su hello stesso host di amministrazione centrale.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Aprire la pagina di amministrazione centrale SharePoint hello e passare troppo**le impostazioni di sistema**. 
2. In hello **Azure StorSimple** fare clic su **configura l'adattatore StorSimple**.
   
    ![Configurare hello adattatore StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. In hello **configura l'adattatore StorSimple** pagina:
   
   1. Verificare che tale hello **Abilita Modifica percorso** casella di controllo è selezionata.
   2. Nella casella di testo hello, digitare il percorso UNC Universal Naming Convention () hello dell'archivio BLOB hello.
      
      > [!NOTE]
      > volume dell'archivio BLOB Hello deve essere ospitato in un volume iSCSI configurato sul dispositivo StorSimple hello.

   3. Fare clic su hello **abilitare** pulsante sotto ogni hello database del contenuto che si desidera tooconfigure per l'archiviazione remota.
      
      > [!NOTE]
      > archivio BLOB Hello deve essere condiviso e raggiungibile da tutti i server (WFE) front-end web e account utente hello è configurato per la server farm di SharePoint hello deve avere condivisione toohello di accesso.
      
      ![Abilitare i provider RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Quando si abilita o disabilita RBS, si verifica anche segue messaggio hello.
      
      ![Configurare l’adattatore StorSimple Adapter Attivazione Disattivazione](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Fare clic su hello **aggiornamento** configurazione hello tooapply dei pulsanti. Quando si fa clic su hello **aggiornamento** pulsante, verrà aggiornato lo stato di configurazione di RBS hello in tutti i server front-end Web e intera farm hello sarà abilitata per RBS. verrà visualizzata la seguente messaggio Hello.
      
      ![Messaggio di configurazione dell’adattatore](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Se si configura RBS per una farm di SharePoint con un numero molto elevato di database (maggiori di 200), pagina web di amministrazione centrale SharePoint hello potrebbe scadere. In questo caso, aggiornare la pagina hello. Questa operazione non influenza il processo di configurazione di hello.

4. Verificare la configurazione di hello:
   
   1. Accedere al sito Web Amministrazione centrale SharePoint toohello e passare toohello **configura l'adattatore StorSimple** pagina.
   2. Controllare hello toomake dettagli di configurazione corrispondenza impostazioni hello immesso. 
5. Verificare che RBS funzioni correttamente:
   
   1. Caricare un documento tooSharePoint. 
   2. Percorso UNC toohello Sfoglia configurata. Assicurarsi che sia stato creato struttura di directory RBS hello e che contenga oggetti hello caricato.
6. (Facoltativo) È possibile utilizzare Microsoft RBS hello `Migrate()` cmdlet di PowerShell incluso con SharePoint toomigrate esistente BLOB toohello contenuto dispositivo StorSimple. Per ulteriori informazioni, vedere [la migrazione del contenuto da o verso RBS in SharePoint 2013] [ 6] o [la migrazione del contenuto e verso RBS (SharePoint Foundation 2010)] [7].
7. (Facoltativo) Nelle installazioni di prova, è possibile verificare che hello BLOB sono stati spostati dal database del contenuto hello come indicato di seguito: 
   
   1. Avviare SQL Management Studio.
   2. Eseguire query ListBlobsInDB_2010.sql o ListBlobsInDB_2013.sql di hello, come indicato di seguito.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Se RBS è stato configurato correttamente, verrà visualizzato un valore NULL nella colonna SizeOfContentInDB hello per qualsiasi oggetto che è stato caricato e quindi esternalizzato con RBS.
8. (Facoltativo) Dopo aver configurato RBS e spostare tutti i BLOB toohello contenuto dispositivo StorSimple, è possibile spostare dispositivo toohello di hello database del contenuto. Se si sceglie di database del contenuto hello toomove, è consigliabile configurare hello archiviazione del database del contenuto nel dispositivo hello come volume principale. Quindi, utilizzare stabilito di che SQL Server best practices il dispositivo StorSimple toohello di toomigrate hello database del contenuto. 
   
   > [!NOTE]
   > Mobile device toohello database del contenuto di hello è supportato solo per serie StorSimple 8000 hello (non è supportata per la serie hello 5000 o 7000).
   
   Se si archiviano i BLOB e database del contenuto hello in volumi separati nel dispositivo StorSimple hello, si consiglia di configurarli in hello stesso contenitore di volumi. Ciò garantisce che essi saranno sottoposti insieme al backup.
   
   > [!WARNING]
   > Se RBS non è stato abilitato, è preferibile non spostare dispositivo StorSimple toohello di hello database del contenuto. Si tratta di una configurazione non testata.
   
9. Passaggio successivo toohello passare: [configurare garbage collection](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
