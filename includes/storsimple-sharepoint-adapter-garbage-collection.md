<!--author=SharS last changed: 9/17/15-->

In questa procedura, si apprenderà come:

1. [Preparare l'eseguibile del gestore di hello toorun](#to-prepare-to-run-the-maintainer) .
2. [Preparare i database del contenuto hello e il Cestino per l'eliminazione immediata dei blob orfani](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Eseguire Maintainer.exe](#to-run-the-maintainer).
4. [Ripristinare i database del contenuto hello e impostazioni del Cestino](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun hello del gestore
1. Nel server front-end Web hello, aprire hello SharePoint 2013 Management Shell come amministratore.
2. Esplorazione delle cartelle toohello *unità di avvio*: \Programmi\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.
3. Rinominare **Microsoft.Data.sqlremoteblobs.maintainer.exe. config** troppo**Web. config**.
4. Utilizzare `aspnet_regiis -pdf connectionStrings` file Web. config di hello toodecrypt.
5. Nel file Web. config decrittografata hello in hello `connectionStrings` nodo, aggiungere la stringa di connessione hello per l'istanza SQL server e hello Nome database del contenuto. Vedere hello di esempio seguente.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Utilizzare `aspnet_regiis –pef connectionStrings` toore-crittografare file Web. config hello. 
7. Rinominare tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>database del contenuto hello tooprepare e tooimmediately Cestino eliminare BLOB orfani
1. In SQL Server, in SQL Management Studio, hello eseguire hello seguenti query di aggiornamento per il database del contenuto di destinazione hello: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. In hello web in server front-end, **Amministrazione centrale**, modificare hello **impostazioni generali applicazione Web** per hello desiderato hello disable di database del contenuto tootemporarily Cestino. Questa azione verrà inoltre hello vuota al Cestino per tutte le raccolte siti correlati. toodo, fare clic su **Amministrazione centrale** -> **Application Management** -> **applicazioni Web (Gestisci applicazioni web)**  ->  **SharePoint - 80** -> **impostazioni generali applicazione**. Set hello **stato Cestino** troppo**OFF**.
   
    ![Impostazioni generali applicazione Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello del gestore
* Nel server front-end web hello, in SharePoint 2013 Management Shell, hello eseguire hello del gestore come segue:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Solo hello `GarbageCollection` operazione è supportata per StorSimple in questo momento. Si noti inoltre che i parametri di hello emessi per Microsoft.Data.SqlRemoteBlobs.Maintainer.exe sono tra maiuscole e minuscole. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>database del contenuto toorevert hello e impostazioni del Cestino
1. In SQL Server, in SQL Management Studio, hello eseguire hello seguenti query di aggiornamento per il database del contenuto di destinazione hello:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Nel server front-end web hello, in **Amministrazione centrale**, modificare hello **impostazioni generali applicazione Web** per hello desiderato hello toore enable database del contenuto del Cestino. toodo, fare clic su **Amministrazione centrale** -> **Application Management** -> **applicazioni Web (Gestisci applicazioni web)**  ->  **SharePoint - 80** -> **impostazioni generali applicazione**. Impostare hello stato Cestino troppo**ON**.

