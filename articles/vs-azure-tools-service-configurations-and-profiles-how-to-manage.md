---
title: profili e configurazioni del servizio aaaHow toomanage | Documenti Microsoft
description: Informazioni su come toowork con i file di configurazione profili e configurazioni del servizio | quale archiviare le impostazioni per gli ambienti di distribuzione hello e pubblicare le impostazioni per i servizi cloud.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Come toomanage configurazioni del servizio e profili
## <a name="overview"></a>Panoramica
Quando si pubblica un servizio cloud, Visual Studio archivia le informazioni di configurazione in due tipi di file di configurazione, ovvero le configurazioni e i profili del servizio. Configurazioni del servizio (file con estensione cscfg) archiviano le impostazioni per gli ambienti di distribuzione hello per un servizio cloud di Azure. Azure usa questi file di configurazione quando gestisce i servizi cloud. In hello invece, le impostazioni per i servizi cloud di pubblicazione di archivio dei profili (file con estensione azurepubxml). Queste impostazioni sono un record delle scelte effettuate quando si utilizza hello Creazione guidata pubblicazione e sono utilizzate localmente da Visual Studio. Questo argomento viene illustrato come toowork con entrambi i tipi di file di configurazione.

## <a name="service-configurations"></a>Configurazioni del servizio
È possibile creare più toouse di configurazioni di servizio per ognuno degli ambienti di distribuzione. Ad esempio, si potrebbe creare una configurazione del servizio per l'ambiente locale di hello utilizzare toorun e testare un'applicazione Azure e un'altra configurazione del servizio per l'ambiente di produzione.

È possibile aggiungere, eliminare, rinominare e modificare queste configurazioni del servizio in base alle proprie esigenze. È possibile gestire queste configurazioni del servizio da Visual Studio, come illustrato nella seguente figura hello.

![Gestisci configurazioni di servizio](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

È inoltre possibile aprire hello **Gestisci configurazioni** finestra di dialogo Pagine delle proprietà del ruolo hello. proprietà di hello tooopen per un ruolo nel progetto Azure, aprire il menu di scelta rapida hello per tale ruolo e quindi scegliere **proprietà**. In hello **impostazioni** espandere hello **configurazione del servizio** elenco e quindi selezionare **Gestisci** tooopen hello **Gestisci configurazioni**la finestra di dialogo.

### <a name="tooadd-a-service-configuration"></a>tooadd una configurazione del servizio
1. In Esplora soluzioni, aprire il menu di scelta rapida hello hello progetto Azure e quindi selezionare **Gestisci configurazioni**.
   
    Hello **Gestisci configurazioni servizio** viene visualizzata la finestra di dialogo.
2. tooadd una configurazione del servizio, è necessario creare una copia di una configurazione esistente. toodo, scegliere configurazione hello toocopy dall'elenco Nome hello desiderati e quindi selezionare **creare copia**.
3. Configurazione del servizio hello toogive (facoltativo) un nome diverso, scegliere hello nuova configurazione del servizio dall'elenco Nome hello e quindi selezionare **rinominare**. In hello **nome** casella di testo, il nome del tipo hello che desidera toouse per questa configurazione del servizio e quindi selezionare **OK**.
   
    Un nuovo file di configurazione servizio denominato ServiceConfiguration. [Nome] con estensione cscfg viene aggiunto toohello progetto Azure in Esplora soluzioni.

### <a name="toodelete-a-service-configuration"></a>toodelete una configurazione del servizio
1. In Esplora soluzioni, aprire il menu di scelta rapida hello hello progetto Azure e quindi selezionare **Gestisci configurazioni**.
   
    Hello **Gestisci configurazioni servizio** viene visualizzata la finestra di dialogo.
2. toodelete una configurazione del servizio, scegliere configurazione hello che si desidera toodelete da hello **nome** elenco e quindi selezionare **rimuovere**. Una finestra di dialogo viene visualizzata tooverify che si desidera toodelete questa configurazione.
3. Selezionare **Elimina**.
   
     file di configurazione del servizio Hello viene rimosso dal progetto Azure in Esplora soluzioni hello.

### <a name="toorename-a-service-configuration"></a>toorename una configurazione del servizio
1. In Esplora soluzioni, aprire il menu di scelta rapida hello per hello progetto Azure e quindi selezionare **Gestisci configurazioni**.
   
    Hello **Gestisci configurazioni servizio** viene visualizzata la finestra di dialogo.
2. toorename una configurazione del servizio, scegliere nuova configurazione del servizio hello hello **nome** elenco e quindi selezionare **rinominare**. In hello **nome** casella di testo, il nome del tipo hello desidera toouse per questa configurazione del servizio e quindi selezionare **OK**.
   
    nome di Hello del file di configurazione del servizio hello viene modificato in hello progetto Azure in Esplora soluzioni.

### <a name="toochange-a-service-configuration"></a>toochange una configurazione del servizio
* Se si desidera toochange una configurazione del servizio, aprire il menu di scelta rapida hello per ruolo specifico di hello toochange nel progetto Azure hello desiderato e quindi selezionare **proprietà**. Vedere [procedura: configurare i ruoli di hello per un servizio Cloud di Azure con Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) per ulteriori informazioni.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Effettuare diverse combinazioni di impostazioni usando i profili
Usando un profilo, è possibile popolare automaticamente in hello **pubblicazione guidata** con diverse combinazioni di impostazioni per scopi diversi. Ad esempio, è possibile definire un profilo per eseguire il debug e uno per le build di rilascio. In tal caso, il **Debug** profilo avrebbe **IntelliTrace** abilitato e hello **Debug** configurazione selezionata e **versione** profilo avrebbe **IntelliTrace** disabilitato e hello **versione** configurazione selezionata. È anche possibile usare diversi profili toodeploy un servizio utilizzando un account di archiviazione diverso.

Quando si esegue la procedura guidata hello per hello prima volta, viene creato un profilo predefinito. Visual Studio archivia profilo hello in un file con estensione azurepubxml, che viene aggiunto un progetto Azure in hello tooyour **profili** cartella. Se si specificano manualmente opzioni diverse quando si esegue la procedura guidata hello in un secondo momento, aggiorna automaticamente i file hello. Prima di eseguire hello procedura, è necessario avere già pubblicato il servizio cloud almeno una volta.

### <a name="tooadd-a-profile"></a>tooadd un profilo
1. Aprire il menu di scelta rapida hello per il progetto Azure e quindi selezionare **pubblica**.
2. Avanti toohello **profilo di destinazione** elenco, seleziona hello **Salva profilo** pulsante, come hello seguente illustrazione. Verrà creato un profilo per l'utente.
   
    ![Creare un nuovo profilo](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Dopo aver creato il profilo di hello, selezionare **< Gestisci >** in hello **profilo di destinazione** elenco.
   
    Hello **Gestione profili** viene visualizzata la finestra di dialogo, come hello seguente illustrazione.
   
    ![Finestra di dialogo Gestione profili](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. In hello **nome** elenco, scegliere un profilo e quindi selezionare **Crea copia**.
5. Scegliere hello **Chiudi** pulsante.
   
    Hello nuovo profilo compare nell'elenco di profili di destinazione hello.
6. In hello **profilo di destinazione** elenco profilo selezionare hello appena creato. le impostazioni di pubblicazione guidata Hello vengono popolate scelte hello dal profilo hello selezionato.
7. Seleziona hello **precedente** e **Avanti** i pulsanti di ogni pagina della procedura guidata di pubblicazione hello toodisplay e quindi personalizzare le impostazioni di hello per questo profilo. Per altre informazioni, vedere [Procedura guidata per la pubblicazione dell'applicazione Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
8. Dopo aver completato la personalizzazione delle impostazioni di hello, selezionare **Avanti** toogo toohello back-pagina delle impostazioni. Hello profilo viene salvato quando si pubblica il servizio di hello utilizzando queste impostazioni o se si seleziona **salvare** Avanti toohello elenco dei profili.

### <a name="toorename-or-delete-a-profile"></a>toorename o eliminazione di un profilo
1. Aprire il menu di scelta rapida hello per il progetto Azure e quindi selezionare **pubblica**.
2. In hello **profilo di destinazione** elenco, selezionare **Gestisci**.
3. In hello **Gestione profili** della finestra di dialogo profilo hello selezionare desidera toodelete e quindi selezionare **rimuovere**.
4. In hello conferma della finestra di dialogo visualizzata selezionare **OK**.
5. Selezionare **Chiudi**.

### <a name="toochange-a-profile"></a>toochange un profilo
1. Aprire il menu di scelta rapida hello per il progetto Azure e quindi selezionare **pubblica**.
2. In hello **profilo di destinazione** elenco profilo selezionare hello che si desidera toochange.
3. Seleziona hello **precedente** e **Avanti** pulsanti toodisplay hello di ogni pagina della procedura guidata di pubblicazione, quindi modificare le impostazioni di hello desiderato. Per altre informazioni, vedere [Procedura guidata per la pubblicazione dell'applicazione Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
4. Dopo aver completato la modifica delle impostazioni di hello, selezionare **Avanti** toohello indietro toogo **impostazioni** pagina.
5. (Facoltativo) selezionare **pubblica** servizio cloud di hello toopublish utilizzando hello nuove impostazioni. Se non si desidera toopublish il servizio cloud in questa fase e si chiude Visual Studio chiede se si desidera toosave hello modifiche toohello profilo hello pubblicazione guidata.

## <a name="next-steps"></a>Passaggi successivi
toolearn sulla configurazione di altre parti del progetto Azure da Visual Studio, vedere [configurazione di un progetto di Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

