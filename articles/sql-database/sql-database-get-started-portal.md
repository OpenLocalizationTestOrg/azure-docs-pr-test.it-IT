---
title: 'Portale di Azure: creare un database SQL | Microsoft Docs'
description: Informazioni su come toocreate un server logico di Database SQL regola del firewall a livello di server e database hello portale di Azure. Inoltre tooquery un database SQL di Azure mediante hello portale di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a>Creare un database SQL di Azure nel portale di Azure hello

In questa esercitazione introduttiva illustra come toocreate un SQL database in Azure. Database SQL di Azure è un "Database-as-a-Service" offerta che consente di scala e toorun database di SQL Server a disponibilità elevata nel cloud hello. Questa Guida introduttiva illustra la modalità di avvio tooget mediante la creazione di un database SQL tramite hello portale di Azure.

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="create-a-sql-database"></a>Creazione di un database SQL

Un database SQL di Azure viene creato con un set definito di [risorse di calcolo e di archiviazione](sql-database-service-tiers.md). Hello database viene creato all'interno di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) e in un [server logico di Database SQL di Azure](sql-database-features.md). 

Seguire questi passaggi toocreate un database SQL contenente dati di esempio Adventure Works LT hello. 

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Selezionare **database** da hello **New** pagina e selezionare **Database SQL** da hello **database** pagina.

   ![Creare il database 1](./media/sql-database-get-started-portal/create-database-1.png)

3. Compilare il modulo di Database SQL hello con hello le seguenti informazioni, come mostrato nella precedente immagine hello:   

   | Impostazione       | Valore consigliato | Descrizione | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Database name** (Nome database) | mySampleDatabase | Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificatori di database). | 
   | **Sottoscrizione** | Sottoscrizione in uso  | Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni). |
   | **Gruppo di risorse**  | myResourceGroup | Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). |
   | **Seleziona origine** | Sample (AdventureWorksLT) (Esempio - AdventureWorksLT) | Carica i dati e schema AdventureWorksLT hello nel nuovo database |

   > [!IMPORTANT]
   > Perché viene utilizzato nel resto di hello di questa Guida introduttiva, è necessario selezionare il database di esempio hello in questo modulo.
   > 

4. In **Server**, fare clic su **Configura le impostazioni obbligatorie** e compilare hello formato SQL server (server logico) con hello le seguenti informazioni, come illustrato nella seguente immagine hello:   

   | Impostazione       | Valore consigliato | Descrizione | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Server name** (Nome server) | Qualsiasi nome globalmente univoco | Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). | 
   | **Nome di accesso amministratore server** | Qualsiasi nome valido | Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificatori di database). |
   | **Password** | Qualsiasi password valida | La password deve contenere almeno 8 caratteri e deve contenere caratteri di tre delle seguenti categorie di hello: lettere maiuscole, lettere minuscole, numeri e caratteri non alfanumerici e. |
   | **Sottoscrizione** | Sottoscrizione in uso | Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni). |
   | **Gruppo di risorse** | myResourceGroup | Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). |
   | **Posizione** | Qualsiasi località valida | Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/). |

   > [!IMPORTANT]
   > account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida introduttiva. Prendere nota di queste informazioni per usarle in seguito. 
   >  

   ![Creare il server di database](./media/sql-database-get-started-portal/create-database-server.png)

5. Dopo aver completato il modulo di hello, fare clic su **selezionare**.

6. Fare clic su **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo database. Utilizzare hello dispositivo di scorrimento tooselect **20 Dtu** e **250** GB di spazio di archiviazione. Per altre informazioni sulle DTU, vedere il relativo [articolo](sql-database-what-is-a-dtu.md).

   ![Creare il database s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. Dopo il periodo selezionato hello di Dtu, fare clic su **applica**.  

8. Dopo aver completato il form di Database SQL hello, fare clic su **crea** database hello tooprovision. Il provisioning richiede alcuni minuti. 

9. Sulla barra degli strumenti hello, fare clic su **notifiche** toomonitor processo di distribuzione hello.

   ![notifica](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Creare una regola del firewall a livello di server

Hello servizio Database SQL consente di creare un firewall hello a livello server che impedisce la connessione server toohello o da qualsiasi database nel server di hello, solo una regola del firewall creata firewall hello tooopen per indirizzi IP specifici strumenti e applicazioni esterne. Seguire questi passaggi toocreate un [regola del firewall a livello di server SQL Database](sql-database-firewall-configure.md) per indirizzo IP del client e abilitare la connettività esterna tramite firewall del Database SQL hello per solo l'indirizzo IP. 

> [!NOTE]
> Il database SQL comunica attraverso la porta 1433. Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete. In questo caso, è possibile connettersi tooyour server di Database SQL di Azure, a meno che il reparto IT consente di aprire la porta 1433.
>

1. Al termine della distribuzione di hello, fare clic su **database SQL** dal menu a sinistra di hello e quindi fare clic su **mySampleDatabase** su hello **database SQL** pagina. pagina di panoramica per l'apertura del database, che mostra hello completamente Hello completo del server (ad esempio **mynewserver20170313.database.windows.net**) e offre opzioni per un'ulteriore configurazione. Copiare il nome completo del server per usarlo in seguito.

   > [!IMPORTANT]
   > È necessario il server di tooyour tooconnect nome completo del server e i relativi database nelle successive guide introduttive.
   > 

   ![Nome del server](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Fare clic su **impostare firewall server** sulla barra degli strumenti hello, come illustrato nella figura precedente hello. Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello. 

   ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. Fare clic su **Aggiungi indirizzo IP del client** su hello barra degli strumenti tooadd il corrente l'indirizzo IP di tooa nuova regola del firewall. Una regola del firewall può aprire la porta 1433 per un indirizzo IP singolo o un intervallo di indirizzi IP.

4. Fare clic su **Salva**. Una regola del firewall a livello di server viene creata per l'indirizzo IP corrente, aprire la porta 1433 sul server logico hello.

   ![Impostare la regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Fare clic su **OK** e quindi chiudere hello **le impostazioni del Firewall** pagina.

È ora possibile connettersi a server di Database SQL toohello e i relativi database tramite SQL Server Management Studio o un altro strumento di propria scelta da questo indirizzo IP utilizzando l'account amministratore di server hello creato in precedenza.

> [!IMPORTANT]
> Per impostazione predefinita, l'accesso attraverso il firewall di Database SQL hello è abilitato per tutti i servizi di Azure. Fare clic su **OFF** su toodisable questa pagina per tutti i servizi di Azure.
>

## <a name="query-hello-sql-database"></a>Database SQL di hello query

Ora che è stato creato un database di esempio in Azure, si strumento hello query incorporata all'interno di hello Azure tooconfirm portale è possibile collegare dati di hello toohello database e query. 

1. Nella pagina Database SQL di hello per il database, fare clic su **strumenti** sulla barra degli strumenti hello. Hello **strumenti** verrà visualizzata la pagina.

   ![Menu Strumenti](./media/sql-database-get-started-portal/tools-menu.png) 

2. Fare clic su **editor di Query (anteprima)**, fare clic su hello **anteprima termini** casella di controllo, quindi fare clic su **OK**. verrà visualizzata la pagina dell'editor di Query Hello.

3. Fare clic su **accesso** e quindi, quando richiesto, selezionare **autenticazione di SQL server** e quindi specificare l'account di accesso amministratore server hello e la password creata in precedenza.

   ![Accesso](./media/sql-database-get-started-portal/login.png) 

4. Fare clic su **OK** toolog in.

5. Dopo l'autenticazione, digitare quanto segue di hello eseguire una query nel riquadro dell'editor di query hello.

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. Fare clic su **eseguire** ed esaminarne i risultati della query hello in hello **risultati** riquadro.

   ![Risultati dell'Editor di query](./media/sql-database-get-started-portal/query-editor-results.png)

7. Chiude hello **editor di Query** pagina e hello **strumenti** pagina.

## <a name="clean-up-resources"></a>Pulire le risorse

Se non è necessario queste risorse per un altro conosca (vedere [passaggi successivi](#next-steps)), è possibile eliminarle eseguendo hello seguenti:


1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su **myResourceGroup**. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, tipo **myResourceGroup** in hello casella di testo e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti. Per altre informazioni, scegliere uno strumento di seguito:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.JS](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)
