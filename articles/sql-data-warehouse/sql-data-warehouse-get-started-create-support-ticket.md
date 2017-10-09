---
title: aaaHow toocreate un ticket di supporto per SQL Data Warehouse | Documenti Microsoft
description: Come supporto toocreate ticket in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Modalità di concessione ticket toocreate un supporto per SQL Data Warehouse
In caso di problemi con SQL Data Warehouse, creare un ticket di supporto per ottenere assistenza dal team tecnico.

> [!NOTE] 
> A partire da 20/12/2016, controllo di integrità risorsa hello in hello portale di Azure non è preciso. Stiamo lavorando attivamente toofix questo problema. 


## <a name="create-a-support-ticket"></a>Creare un ticket di supporto
1. Aprire hello [portale di Azure][Azure portal].
2. Nella schermata iniziale di hello, fare clic su hello **Guida e supporto** riquadro.
   
    ![Guida e supporto tecnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. In hello della Guida e supporto, fare clic su **Crea richiesta di supporto**.
   
    ![Nuova richiesta di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Seleziona hello **richiesta è di tipo**.
   
    ![tipo di richiesta](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Per impostazione predefinita, ogni server SQL, ad esempio myserver.database.windows.net, ha una **Quota DTU** pari a 45.000. Questa quota è semplicemente un limite di sicurezza. È possibile aumentare la quota per la creazione di un ticket di supporto e selezionando *Quota* come tipo di richiesta hello. le DTU, è necessario moltiplicare toocalculate hello 7.5 da hello totale [DWU] [ DWU] necessari. Ad esempio, si desidera toohost due DW6000s su un server SQL server, sarà necessario richiedere una quota DTU di 90.000.  È possibile visualizzare il consumo di DTU corrente dal pannello hello SQL server nel portale di hello. Il database sia in pausa e riavviato conteggiati per la quota di DTU hello. 
   > 
   > 
5. Seleziona hello **sottoscrizione** che gli host hello database con problema hello segnalato.
   
    ![Sottoscrizione](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Selezionare **SQL Data Warehouse** come hello risorse.
   
    ![Risorsa](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Selezionare il proprio [piano di supporto di Azure][Azure support plan].
   
   * **fatturazione, quota e gestione delle sottoscrizioni** è disponibile per tutti i livelli.
   * Il supporto **in garanzia** viene fornito tramite il supporto tecnico [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier]. Problemi di riparazione sono i problemi riscontrati dai clienti durante l'utilizzo di Azure in cui è presente un ragionevole supporre che problema hello Microsoft ha causato.
   * **Sviluppatore esperto** e **servizi di consulenza** sono disponibili all'indirizzo hello [Professional Direct] [ Professional Direct] e [Premier] [ Premier] livelli di supporto. 
     
     Se si dispone di un Premier il piano di supporto, è possibile segnalare anche SQL Data Warehouse problemi su hello [portale online Microsoft Premier][Microsoft Premier online portal].  Vedere [piani di supporto tecnico di Azure] [ Azure support plan] toolearn ulteriori informazioni sulle varie supporta i piani ambito, risposta volte, sui prezzi, hello e così via.  Per domande frequenti sul supporto di Azure, vedere [Domande frequenti sul supporto di Azure][Azure support FAQs].  
     
     ![Piano di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Seleziona hello **tipo di problema** e **categoria**. In questo esempio, abbiamo scelto "Strumenti" come tipo di problema hello e "Strumenti Client" come categoria di hello. 
   
    ![Categoria del tipo di problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Descrivere il problema di hello e hello livello di impatto aziendale.
   
    ![Descrizione del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Le **informazioni di contatto** per il ticket di supporto saranno precompilate. Aggiornare le informazioni, se necessario.
    
    ![Informazioni di contatto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Fare clic su **crea** toosubmit hello richiesta di supporto.

## <a name="monitor-a-support-ticket"></a>Monitorare un ticket di supporto
Dopo che è stata inviata una richiesta di supporto hello, il team di supporto tecnico di Azure hello contatterà l'utente. toocheck la stato della richiesta e i dettagli, fare clic su **Gestisci richieste di supporto** dashboard hello.

![Controlla stato](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Altre risorse
Inoltre, è possibile connettersi con hello community di SQL Data Warehouse sul [Overflow dello Stack] [ Stack Overflow] o hello [forum MSDN di Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

