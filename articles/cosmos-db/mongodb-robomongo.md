---
title: aaaUse Robomongo per Azure Cosmos DB | Documenti Microsoft
description: 'Informazioni su come toouse Robomongo con un database di Azure Cosmos: API per conto di MongoDB'
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Usare Robomongo con un account Azure Cosmos DB: API per MongoDB
tooconnect tooan DB Cosmos Azure: API per conto di MongoDB mediante Robomongo, è necessario:

* Scaricare e installare [Robomongo](https://robomongo.org/)
* Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB

## <a name="connect-using-robomongo"></a>Connettersi tramite Robomongo
tooadd del database di Azure Cosmos: API per conto di MongoDB toohello Robomongo MongoDB connessioni, eseguire hello alla procedura seguente.

1. Recuperare il database di Azure Cosmos: API MongoDB account informazioni di connessione utilizzando le istruzioni di hello [qui](connect-mongodb-account.md).

    ![Cattura di schermata del pannello stringa di connessione hello](./media/mongodb-robomongo/connectionstringblade.png)
2. Eseguire *Robomongo.exe*

3. Fare clic sul pulsante di connessione hello in **File** toomanage le connessioni. Quindi, fare clic su **crea** in hello **connessioni MongoDB** finestra verrà aperta hello **le impostazioni di connessione** finestra.

4. In hello **le impostazioni di connessione** finestra, scegliere un nome. Quindi, individuare hello **Host** e **porta** da informazioni di connessione nel passaggio 1 e immetterli in **indirizzo** e **porta**rispettivamente .

    ![Cattura di schermata di hello Robomongo Gestisci connessioni](./media/mongodb-robomongo/manageconnections.png)
5. In hello **autenticazione** scheda, fare clic su **Esegui autenticazione**. Immettere il valore nel campo **User Name** (Nome utente) (il valore predefinito è *Admin*) e la **password**.
I valori per i campi **User Name** (Nome utente) e **Password** possono essere trovati nelle informazioni di connessione nel Passaggio 1.

    ![Cattura di schermata della scheda autenticazione Robomongo hello](./media/mongodb-robomongo/authentication.png)
6. In hello **SSL** scheda **protocollo Usa SSL**, quindi modificare hello **metodo di autenticazione** troppo**certificato autofirmato**.

    ![Cattura di schermata della scheda SSL Robomongo hello](./media/mongodb-robomongo/SSL.png)
7. Infine, fare clic su **Test** tooverify che si è in grado di tooconnect, **salvare**.

## <a name="next-steps"></a>Passaggi successivi
* Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.
