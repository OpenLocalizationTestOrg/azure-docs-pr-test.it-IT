---
title: aaaRegister dati dall'archivio Data Lake in Azure Data Catalog | Documenti Microsoft
description: Registrare i dati da Archivio Data Lake in Azure Data Catalog
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Registrare i dati da Archivio Data Lake in Azure Data Catalog
In questo articolo si apprenderà come toointegrate Azure Data Lake con Azure Data Catalog toomake i dati memorizzati individuabili all'interno dell'organizzazione da integrato con il catalogo dati. Per altre informazioni sulla catalogazione dei dati, vedere [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md). toounderstand scenari in cui è possibile utilizzare il catalogo dati, vedere [scenari comuni di Azure Data Catalog](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Abilitare la sottoscrizione di Azure** per l'anteprima pubblica di Data Lake Store. Vedere le [istruzioni](data-lake-store-get-started-portal.md).
* **Account di Archivio Data Lake di Azure**. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md). Per questa esercitazione, viene creato un account Archivio Data Lake denominato **datacatalogstore**.

    Dopo aver creato l'account di hello, caricare un tooit di set di dati di esempio. Per questa esercitazione, segnalare il problema caricare tutti i file con estensione csv hello in hello **AmbulanceData** cartella hello [Git Repository di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). È possibile utilizzare vari client, ad esempio [Azure Storage Explorer](http://storageexplorer.com/), contenitore blob tooa di tooupload dati.
* **Azure Data Catalog**. È necessario che per l'organizzazione sia già stato creato un catalogo di Azure Data Catalog. Per ogni organizzazione è consentito un solo catalogo.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Registrare Archivio Data Lake come origine per Data Catalog

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Andare troppo`https://azure.microsoft.com/services/data-catalog`, fare clic su **iniziare**.
2. Accedere al portale di Azure Data Catalog hello e fare clic su **pubblicare dati**.

    ![Registrare un'origine dati](./media/data-lake-store-with-data-catalog/register-data-source.png "Registrare un'origine dati")
3. Nella pagina successiva di hello, fare clic su **Avvia applicazione**. Questo scaricherà i file di manifesto dell'applicazione hello nel computer in uso. Fare doppio clic su un'applicazione hello toostart hello file manifesto.
4. Nella pagina di benvenuto hello, fare clic su **Accedi**, immettere le credenziali.

    ![Schermata iniziale](./media/data-lake-store-with-data-catalog/welcome.screen.png "Schermata iniziale")
5. Hello selezionare una pagina di origine dati, scegliere **Azure Data Lake**, quindi fare clic su **Avanti**.

    ![Selezionare l'origine dati](./media/data-lake-store-with-data-catalog/select-source.png "Selezionare l'origine dati")
6. Nella pagina successiva di hello, fornire hello nome dell'account archivio Data Lake che si desidera tooregister nel catalogo dati. Lasciare hello altre opzioni predefinite e quindi fare clic su **Connetti**.

    ![Connetti toodata origine](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connetti toodata origine")
7. la pagina successiva di Hello può essere suddivisi in hello seguenti segmenti.

    a. Hello **Server gerarchia** casella rappresenta una struttura di cartelle account archivio Data Lake hello. **$Root** rappresenta hello radice account archivio Data Lake, e **AmbulanceData** rappresenta hello cartella creata nel radice hello hello account archivio Data Lake.

    b. Hello **oggetti disponibili** casella sono elencati i file hello e le cartelle in hello **AmbulanceData** cartella.

    c. **Oggetti toobe registrato casella** hello di elenchi di file e cartelle che si desidera tooregister in Azure Data Catalog.

    ![Visualizzare la struttura dei dati](./media/data-lake-store-with-data-catalog/view-data-structure.png "Visualizzare la struttura dei dati")
8. Per questa esercitazione, è necessario registrare tutti i file hello nella directory hello. A tale scopo, fare clic su hello (![spostare gli oggetti](./media/data-lake-store-with-data-catalog/move-objects.png "spostare gli oggetti")) toomove pulsante hello tutti i file troppo**toobe oggetti registrati** casella.

    Poiché i dati di hello verranno registrati in un catalogo di dati dell'organizzazione, è un raccomandati approccio tooadd alcuni metadati che è possibile utilizzare in un secondo momento tooquickly individuare dati hello. Ad esempio, è possibile aggiungere un indirizzo di posta elettronica proprietario dei dati hello (ad esempio, uno che sta caricando dati hello) o aggiungere dati di hello tooidentify un tag. acquisizione schermo Hello riportato di seguito viene illustrato un tag che aggiungiamo toohello dati.

    ![Visualizzare la struttura dei dati](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "Visualizzare la struttura dei dati")

    Fare clic su **Register**.
9. Hello acquisita da schermo seguente indica che i dati hello viene registrati correttamente nel catalogo dati hello.

    ![Registrazione completata](./media/data-lake-store-with-data-catalog/registration-complete.png "Visualizzare la struttura dei dati")
10. Fare clic su **visualizzazione portale** toogo il portale di catalogo dati toohello e verificare che è ora possibile hello accesso registrati i dati dal portale hello. dati hello toosearch, è possibile utilizzare il tag di hello che è utilizzato durante la registrazione dei dati di hello.

     ![Cercare dati nel catalogo](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Cercare dati nel catalogo")
11. È ora possibile eseguire operazioni quali l'aggiunta di annotazioni e dati toohello documentazione. Per ulteriori informazioni, vedere hello seguenti collegamenti.

    * [Annotare le origini dati in Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
    * [Documentare le origini dati in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Vedere anche
* [Annotare le origini dati in Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
* [Documentare le origini dati in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)
* [Integrazione di Data Lake Store con altri servizi di Azure](data-lake-store-integrate-with-other-services.md)
