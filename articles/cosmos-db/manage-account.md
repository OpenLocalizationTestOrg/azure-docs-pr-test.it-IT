---
title: un account Azure Cosmos DB tramite il portale di Azure hello aaaManage | Documenti Microsoft
description: Informazioni su come toomanage account del database di Azure Cosmos tramite hello portale di Azure. Trovare una Guida sull'uso di hello Azure Portal tooview, copia, gli account di accesso e di eliminazione.
keywords: Portale di Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Come un account Azure Cosmos DB toomanage
Informazioni su come tooset coerenza globale, utilizzare chiavi ed eliminare un account Azure Cosmos DB hello portale di Azure.

## <a id="consistency"></a>Gestire le impostazioni di coerenza di Azure Cosmos DB
Selezionare il livello di coerenza destra hello dipende dalla semantica hello dell'applicazione. È consigliabile acquisire familiarità con livelli di coerenza disponibili hello in Azure Cosmos DB leggendo [con coerenza livelli toomaximize disponibilità e le prestazioni nel database di Azure Cosmos][consistency]. Azure Cosmos DB offre garanzia su coerenza, disponibilità e prestazioni a ogni livello di coerenza disponibile per l'account di database. La configurazione dell'account del database con un livello di coerenza di sicuro richiede che i dati siano tooa ristretto singola regione di Azure e non è disponibile a livello globale. In hello invece, i livelli di coerenza relaxed - con obsolescenza associata, sessione o eventuale abilitazione hello tooassociate è un numero qualsiasi di aree di Azure con l'account di database. Hello semplici passaggi Mostra come tooselect hello a livello di coerenza predefinita per l'account di database. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>coerenza di toospecify hello predefinito per un account Azure Cosmos DB
1. In hello [portale di Azure](https://portal.azure.com/), accedere all'account Azure Cosmos DB.
2. Nel Pannello di hello account, fare clic su **predefinito coerenza**.
3. In hello **uniformità predefinita** pannello, il nuovo livello di coerenza selezionare hello e fare clic su **salvare**.
    ![Sessione coerenza predefinita][5]

## <a id="keys"></a>Visualizzare, copiare e rigenerare le chiavi di accesso
Quando si crea un account Azure Cosmos DB, il servizio di hello genera due chiavi di accesso generale che possono essere utilizzate per l'autenticazione quando si accede a hello account Azure Cosmos DB. Fornendo due chiavi di accesso, Azure Cosmos DB consente chiavi hello tooregenerate con nessun tooyour interruzione account Azure Cosmos DB. 

In hello [portale di Azure](https://portal.azure.com/), hello accesso **chiavi** blade dal menu di risorsa hello hello **account Azure Cosmos DB** tooview pannello, copia e hello Rigenera chiavi di accesso sono tooaccess utilizzato l'account di Azure Cosmos DB.

![Schermata del portale di Azure, pannello delle chiavi](./media/manage-account/keys.png)

> [!NOTE]
> Hello **chiavi** pannello include anche primaria e le stringhe di connessione secondaria che possono essere utilizzati tooconnect tooyour account da hello [utilità di migrazione dati](import-data.md).
> 
> 

In questo pannello sono anche disponibili chiavi di sola lettura. Lettura e query sono operazioni di sola lettura, a differenza di creazione, eliminazione e sostituzione.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Copiare la chiave di accesso nel portale di Azure hello
In hello **chiavi** pannello, fare clic su hello **copia** toohello pulsante a destra della chiave di hello desiderato toocopy.

![Visualizzare e copiare la chiave di accesso nel portale di Azure, pannello chiavi hello](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Per rigenerare le chiavi di accesso
È necessario impostare account di Azure Cosmos DB tooyour di hello accesso chiavi periodicamente toohelp rendere più sicuro le connessioni. Due chiavi di accesso assegnate tooenable si toomaintain connessioni toohello account Azure Cosmos DB usando una chiave di accesso, mentre si rigenera hello altre chiavi di accesso.

> [!WARNING]
> Rigenerare le chiavi di accesso, influisce su tutte le applicazioni che dipendono dalla chiave corrente hello. Tutti i client che utilizzano hello accesso tooaccess chiave hello Azure Cosmos DB account devono essere una nuova chiave di hello toouse aggiornato.
> 
> 

Se si dispone di applicazioni o servizi cloud tramite hello Azure Cosmos DB account, si perderanno le connessioni hello se si rigenerano le chiavi, a meno che non si esegue il rollback delle chiavi. Hello passaggi seguenti delineano il processo di hello coinvolto nella sequenza delle chiavi.

1. Aggiornare la chiave di accesso hello la chiave di accesso secondaria applicazione codice tooreference hello di hello account Azure Cosmos DB.
2. Rigenerare la chiave di accesso primaria hello per l'account di Azure Cosmos DB. In hello [portale Azure](https://portal.azure.com/), accedere all'account Azure Cosmos DB.
3. In hello **Azure Cosmos DB Account** pannello, fare clic su **chiavi**.
4. In hello **chiavi** pannello, fare clic sul pulsante rigenerare hello, quindi fare clic su **Ok** tooconfirm che si desidera toogenerate una nuova chiave.
    ![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-keys.png)
5. Dopo avere verificato la nuova chiave hello è disponibile per l'utilizzo (circa 5 minuti dopo la rigenerazione), aggiornare la chiave di accesso hello nell'applicazione codice tooreference hello nuova chiave di accesso primaria.
6. Rigenerare la chiave di accesso secondaria hello.
   
    ![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Può richiedere alcuni minuti prima che una chiave appena generata può essere utilizzato tooaccess l'account di Azure Cosmos DB.
> 
> 

## <a name="get-hello--connection-string"></a>Ottiene la stringa di connessione hello
tooretrieve la connessione di stringa, hello seguenti: 

1. In hello [portale di Azure](https://portal.azure.com), accedere all'account Azure Cosmos DB.
2. Scegliere dal menu risorse hello **chiavi**.
3. Fare clic su hello **copia** pulsante Avanti toohello **stringa di connessione primaria** o **stringa di connessione secondaria** casella. 

Se si utilizza la stringa di connessione hello in hello [strumento di migrazione di Database di Azure Cosmos DB](import-data.md), accodare end toohello nome del database hello hello della stringa di connessione. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a> Eliminare un account Azure Cosmos DB
un database di Azure Cosmos tooremove account dal portale di Azure non è più in uso, nome dell'account hello pulsante destro del mouse, hello e fare clic su **eliminare account**.

![Come account di un database di Azure Cosmos toodelete in hello portale di Azure](./media/manage-account/deleteaccount.png)

1. In hello [portale di Azure](https://portal.azure.com/), hello Azure Cosmos DB quale account toodelete di accesso.
2. In hello **account Azure Cosmos DB** pannello, fare doppio clic su account hello e quindi fare clic su **Elimina Account**. 
3. Nel Pannello di conferma risultante hello, digitare il nome account di hello Azure Cosmos DB tooconfirm che si desidera account hello toodelete.
4. Fare clic su hello **eliminare** pulsante.

![Come account di un database di Azure Cosmos toodelete in hello portale di Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Passaggi successivi
Informazioni su come troppo[iniziare con il proprio account Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
