
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave costi, è possibile sospendere e riprendere calcolo risorse su richiesta. Ad esempio, se si prevede di usare database hello durante la notte hello e i fine settimana, è possibile sospenderla durante le ore e riprenderlo giornata hello. È non verrà addebitato Dwu mentre hello database resta sospesa.

Quando si sospende un database:

* Risorse di calcolo e memoria vengono restituite toohello pool di risorse disponibili nel centro dati hello
* I costi DWU sono pari a zero per la durata di hello di pausa hello.
* L'archivio dati non è interessato e i dati rimangano invariati. 
* SQL Data Warehouse annulla tutte le operazioni in esecuzione o in coda.

