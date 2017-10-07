---
title: 'Portale di Azure: Maschera dati dinamica del database SQL di Azure | Documentazione Microsoft'
description: "La modalità di avvio tooget con Database SQL la maschera dati dinamica in hello portale di Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Introduzione a Database SQL la maschera dati dinamica con hello portale di Azure

In questo argomento illustra come tooimplement [la maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md) con hello portale di Azure. È anche possibile implementare con maschera dati dinamica [cmdlet del Database di SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Impostare la maschera dati dinamica per il database utilizzando hello portale di Azure
1. Avvio hello portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).
2. Passare il pannello impostazioni toohello del database hello che include i dati sensibili hello desiderato toomask.
3. Fare clic su hello **maschera dati dinamica** riquadro che consente di avviare hello **maschera dati dinamica** Pannello di configurazione.
   
   * In alternativa, è possibile scorrere verso il basso toohello **operazioni** sezione e fare clic su **maschera dati dinamica**.
     
     ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. In hello **maschera dati dinamica** pannello configurazione potrebbe essere visualizzato alcune colonne di database tale motore indicazioni hello è contrassegnata per la maschera. Ordinare tooaccept indicazioni hello, è sufficiente scegliere **Aggiungi maschera** per una o più colonne e una maschera verrà create in base al tipo di hello predefinito per questa colonna. È possibile modificare hello funzione di maschera facendo clic sulla regola per la maschera hello e modifica hello maschera campo tooa diverso formato di propria scelta. Tooclick assicurarsi di essere **salvare** toosave le impostazioni.
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. una maschera per qualsiasi colonna del database, nella parte superiore di hello di hello tooadd **maschera dati dinamica** configurazione fare clic su pannello **Aggiungi maschera** tooopen hello **Aggiungi regola di maschera** Pannello di configurazione
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Seleziona hello **Schema**, **tabella** e **colonna** hello toodefine designato campo che verrà nascosta.
7. Scegliere un **formato maschera del campo** dall'elenco di hello della maschera di categorie di dati sensibili.
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Fare clic su **salvare** nel set di hello tooupdate pannello regole di maschera le regole di criteri di maschera dati dinamica hello di maschera dati hello.
9. Utenti SQL hello di tipo o identità di Azure ad che devono essere esclusi dalla maschera e ha accesso a dati riservati toohello non mascherato. Deve trattarsi di un elenco di utenti separati da punto e virgola. Si noti che gli utenti con privilegi di amministratore dispongano sempre di dati senza maschera di accesso toohello originale.
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake hello così di livello applicazione è possibile visualizzare i dati sensibili per gli utenti con privilegi di applicazione, aggiungere hello utente SQL o un'applicazione hello identità AAD utilizza database hello tooquery. È consigliabile che questo elenco contiene un numero minimo di esposizione toominimize gli utenti con privilegi di dati sensibili hello.
   > 
   > 
10. Fare clic su **salvare** in Criteri di configurazione pannello toosave hello maschera nuove o aggiornate di maschera dati hello.


## <a name="next-steps"></a>Passaggi successivi

* Per una panoramica, vedere l'articolo su [Maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md).
* È anche possibile implementare con maschera dati dinamica [cmdlet del Database di SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).
