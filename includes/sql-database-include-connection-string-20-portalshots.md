
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Ottenere la stringa di connessione hello da hello portale di Azure
Hello utilizzare [portale di Azure](https://portal.azure.com/) tooobtain di stringa di connessione hello necessari per il toointeract programma client con il Database SQL di Azure: 

1. Fare clic su **ESPLORA** > **Database SQL**.
2. Immettere il nome di hello del database nella casella di testo filtro hello quasi hello angolo superiore sinistro di hello **database SQL** blade.
3. Fare clic sulla riga hello per il database.
4. Una volta pannello hello visualizzato per il database, per agevolarne è possibile fare clic su hello standard ridurre al minimo pannelli di hello toocollapse controlli utilizzati per la ricerca e filtro di database. 
   
    ![Filtrare tooisolate del database][10-FilterDatabase]
5. Nel Pannello di hello per il database, fare clic su **Mostra le stringhe di connessione di database**.
6. Se si intende una raccolta di connessioni ADO.NET hello toouse, copiare la stringa di hello etichettata **ADO**. 
   
    ![Copiare una stringa di connessione ADO hello per il database][20-CopyAdoConnectionString]
7. In un formato o un altro, incollare il codice del programma client informazioni della stringa di connessione hello.

Per altre informazioni, vedere:<br/>[Stringhe di connessione e file di configurazione](http://msdn.microsoft.com/library/ms254494.aspx).

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
