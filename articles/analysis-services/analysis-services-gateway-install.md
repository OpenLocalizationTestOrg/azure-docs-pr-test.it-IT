---
title: gateway dati locale di aaaInstall | Documenti Microsoft
description: Informazioni su come tooinstall e configurare un gateway dati locale.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Installare e configurare un gateway dati locale
Un gateway dati locale è obbligatorio quando hello di uno o più server Azure Analysis Services nella stessa area connettersi a origini dati locali tooon. toolearn ulteriori informazioni sui gateway hello, vedere [gateway dati locale](analysis-services-gateway.md).

## <a name="prerequisites"></a>Prerequisiti
**Requisiti minimi:**

* .NET Framework 4.5
* Versione a 64 bit di Windows 7 o Windows Server 2008 R2 (o versione successiva)

**Consigliato:**

* 8 CPU core
* 8 GB di memoria
* Windows 2012 R2 versione a 64 bit (o versione successiva)

**Considerazioni importanti:**

* Durante l'installazione, quando si registra il gateway con Azure, è selezionata l'area predefinita hello per la sottoscrizione. È possibile scegliere un'area diversa. Se si dispone di server in più aree, è necessario installare un gateway per ogni area. 
* Impossibile installare il gateway Hello in un controller di dominio.
* In un singolo computer può essere installato un solo gateway.
* Installare il gateway di hello in un computer che rimanga nel e non va toosleep.
* Non installare il gateway hello in una rete di computer in modalità wireless connesso tooyour. È infatti possibile che si verifichi un calo delle prestazioni.


## <a name="download"></a>Scaricare
 [Scaricare il gateway hello](https://aka.ms/azureasgateway)

## <a name="install"></a>Installare

1. Eseguire l'installazione.

2. Selezionare un percorso, accettare le condizioni di hello e quindi fare clic su **installare**.

   ![Percorso di installazione e condizioni di licenza](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Selezionare **Gateway dati locale (scelta consigliata)**. Azure Analysis Services non supporta la modalità personale.

   ![Scelta del tipo di gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Immettere un account toosign tooAzure. Hello account deve essere del tenant Azure Active Directory. Questo account viene utilizzato per l'amministratore del gateway hello. 

   ![Immettere un account toosign in tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Se si accede con un account di dominio, sarà eseguito il mapping di account aziendale tooyour in Azure AD. Verrà utilizzato l'account aziendale come amministratore del gateway hello hello.

## <a name="register"></a>Registrare
In ordine toocreate una risorsa per il gateway in Azure, è necessario registrare l'istanza locale di hello che è stato installato con il servizio Cloud Gateway hello. 

1.  Selezionare l'opzione **Consente di registrare un nuovo gateway in questo computer**.

    ![Registra](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Digitare un nome e la chiave di ripristino per il gateway. Per impostazione predefinita, il gateway di hello utilizza area predefinita della sottoscrizione. Se è necessario tooselect un'area diversa, selezionare **area Modifica**.

   ![Registra](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Creare una risorsa per il gateway di Azure
Dopo aver installato e registrato il gateway, è necessario toocreate una risorsa di gateway nella sottoscrizione di Azure. Accedi tooAzure con hello stesso account usato durante la registrazione gateway hello.

1. Nel portale di Azure fare clic su **Crea un nuovo servizio** > **Integrazione aziendale**  > **Gateway dati locale** > **Crea**.

   ![Creazione di una risorsa per il gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. In **Crea gateway di connessione**, immettere queste impostazioni:

    * **Nome**: inserire un nome per la risorsa del gateway. 

    * **Sottoscrizione**: selezionare hello tooassociate sottoscrizione di Azure alla risorsa del gateway. 
    La sottoscrizione deve essere il server si trovano nella stessa sottoscrizione di hello.
   
      sottoscrizione predefinita Hello è basata su account di Azure utilizzato toosign in hello.

    * **Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.

    * **Percorso**: area hello selezionare il gateway è stato registrato.

    * **Nome di installazione**: se l'installazione del gateway non è già selezionata, selezionare hello registrato. 

    Al termine dell'operazione, scegliere **Crea**.

## <a name="connect-servers"></a>Connettere i server toohello gateway

1. Nella panoramica del server Azure Analysis Services fare clic su **Gateway dati locale**.

   ![Connessione server toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. In **Pick tooconnect un Gateway dati locale**, selezionare la risorsa del gateway e quindi fare clic su **gateway selezionato Connetti**.

   ![Connettere toogateway server](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Se il gateway non compare nell'elenco di hello, il server è probabile che non nella stessa area come area hello è specificato durante la registrazione gateway hello hello. 

È tutto. Se si necessita di porte tooopen o eseguire attività di risoluzione, essere certi toocheck out [gateway dati locale](analysis-services-gateway.md).

## <a name="next-steps"></a>Passaggi successivi
* [Gestire Analysis Services](analysis-services-manage.md)   
* [Ottenere dati da Azure Analysis Services](analysis-services-connect.md)
