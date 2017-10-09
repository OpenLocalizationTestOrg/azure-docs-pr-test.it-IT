
In questo video di Azure Friday, con Scott Hanselman e Karthik Raman, Principal Engineering Manager, sono disponibili altre informazioni sulla distribuzione globale in Azure Cosmos DB.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Per informazioni sul funzionamento della replica di database globale in Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Aggiungere aree database globale utilizzando hello portale di Azure
Azure Cosmos DB è disponibile in tutte le [aree di Azure][azureregions] del mondo. Dopo aver selezionato a livello di coerenza hello predefinito per l'account di database, è possibile associare uno o più aree (a seconda la scelta delle esigenze di distribuzione globale e a livello di coerenza predefinito).

1. In hello [portale di Azure](https://portal.azure.com/)in hello barra sinistra, fare clic su **Azure Cosmos DB**.
2. In hello **Azure Cosmos DB** blade, hello selezionare database account toomodify.
3. Nel Pannello di hello account, fare clic su **replicare i dati a livello globale** dal menu di hello.
4. In hello **replicare i dati a livello globale** pannello selezionare hello aree tooadd o rimuovere, fare clic su aree mappa hello e quindi fare clic su **salvare**. È presente un aree tooadding costo, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/documentdb/) o hello [distribuire dati a livello globale con DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) per ulteriori informazioni.
   
    ![Fare clic su aree hello in hello mappa tooadd o rimuoverli][1]
    
Dopo aver aggiunto una seconda area, hello **Failover manuale** opzione è abilitata nei hello **replicare i dati a livello globale** pannello nel portale di hello. È possibile utilizzare questo processo di failover di opzione tootest hello o modificare l'area primaria scrittura hello. Dopo aver aggiunto un'area del terzo, hello **le priorità di Failover** è attivata l'opzione hello pannello stesso in modo che è possibile modificare l'ordine di failover hello per le letture.  

### <a name="selecting-global-database-regions"></a>Selezionare aree di database globali
Esistono due scenari comuni per la configurazione di due o più aree:

1. Recapito a bassa latenza accesso agli utenti di tooend toodata indipendentemente da dove si trovano in tutto il mondo hello
2. Aggiunta di resilienza a livello di area per garantire continuità aziendale e ripristino di emergenza (BCDR)

Per la fornitura a bassa latenza tooend utenti, è consigliabile toodeploy entrambi hello applicazione e aggiungere database Cosmos Azure in aree hello corrispondenti agli utenti dell'applicazione hello toowhere si trovano.

Per BCDR, è consigliabile tooadd aree in base alle coppie di area hello descritte in hello [Business continuità e ripristino di emergenza (BCDR): aree abbinate Azure] [ bcdr] articolo.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
