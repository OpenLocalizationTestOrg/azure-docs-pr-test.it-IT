---
title: "attività di gestione del servizio cloud aaaCommon (classico) | Documenti Microsoft"
description: Informazioni su come toomanage cloud services nel portale di Azure classico hello.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>Come tooManage dei servizi Cloud
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-manage-portal.md)
> * [portale di Azure classico](cloud-services-how-to-manage.md)
>
>

In hello **servizi Cloud** area di Azure classico hello portale, è possibile aggiornare un ruolo del servizio o una distribuzione, alzare di livello un tooproduction pre-distribuzione, collegare servizio cloud di risorse tooyour in questo modo è possibile visualizzare risorse hello dipendenze e la scala hello risorse insieme ed eliminare un servizio cloud o una distribuzione.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Procedura: Aggiornare un ruolo o una distribuzione del servizio cloud
Se è necessario codice dell'applicazione hello tooupdate per il servizio cloud, utilizzare **aggiornamento** nel dashboard di hello, **servizi Cloud** pagina o **istanze** pagina. È possibile aggiornare un singolo ruolo o tutti i ruoli. È necessario tooupload un nuovo pacchetto del servizio e i file di configurazione del servizio.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), nel dashboard di hello, **servizi Cloud** pagina o **istanze** pagina, fare clic su **aggiornamento**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. In **etichetta distribuzione**, immettere una distribuzione di hello tooidentify nome (ad esempio, mycloudservice4). Sono disponibili etichetta distribuzione hello in **introduttiva** dashboard hello.
3. In **pacchetto**, utilizzare **Sfoglia** file pacchetto del servizio hello tooupload (con estensione cspkg).
4. In **configurazione**, utilizzare **Sfoglia** file di configurazione servizio hello tooupload (. cscfg).
5. In **ruolo**selezionare **tutti** se si desidera tooupgrade tutti i ruoli di hello servizio cloud. tooperform un singolo ruolo, aggiornare il ruolo di hello selezionare da tooupdate. Anche se si seleziona un ruolo specifico di tooupdate, gli aggiornamenti di hello in file di configurazione del servizio hello sono ruoli tooall applicato.
6. Se le modifiche di aggiornamento hello hello numero di ruoli o le dimensioni di hello di qualsiasi ruolo, selezionare hello **consentire l'aggiornamento se cambia le dimensioni dei ruoli o il numero di ruoli** tooproceed aggiornamento hello tooenable di casella di controllo.

    Tenere presente che se si modifica la dimensione hello di un ruolo (ovvero dimensione hello di una macchina virtuale che ospita un'istanza del ruolo) o hello numero di ruoli, ogni istanza del ruolo (macchina virtuale) deve essere ricreato l'immagine e tutti i dati locali vanno persi.

7. Se i ruoli del servizio dispongono solo un'istanza del ruolo, selezionare hello **aggiornare anche se uno o più ruoli contengono una casella di controllo della singola istanza** tooenable hello aggiornamento tooproceed.

    Durante un aggiornamento del servizio cloud, Azure può garantire una percentuale di disponibilità del servizio pari solo al 99,95% se ogni ruolo contiene almeno due istanze del ruolo (macchine virtuali). Che consente una macchina virtuale tooprocess client richieste durante l'aggiornamento hello altri.

8. Fare clic su **OK** toobegin (segno di spunta) hello servizio di aggiornamento.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Procedura: scambiare le distribuzioni toopromote tooproduction una distribuzione di gestione temporanea
Utilizzare **scambiare** toopromote una distribuzione di gestione temporanea di un tooproduction servizio cloud. Quando si decide di toodeploy una nuova versione di un servizio cloud, è possibile fase e testare la nuova release dell'ambiente di gestione temporanea del servizio cloud, mentre i clienti utilizzano la versione corrente di hello nell'ambiente di produzione. Quando si è pronti toopromote hello tooproduction versione nuova, è possibile utilizzare **scambiare** tooswitch hello URL da cui hello due distribuzioni.

È possibile scambiare le distribuzioni da hello **servizi Cloud** hello o pagina dashboard.

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**.
2. Nell'elenco di hello dei servizi cloud, fare clic su tooselect servizio cloud di hello è.
3. Fare clic su **Swap**.

    Hello richiesta di conferma seguente viene aperto.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Dopo aver verificato le informazioni di distribuzione hello, fare clic su **Sì** distribuzioni hello tooswap.

    lo scambio di distribuzioni Hello possa avvenire rapidamente perché hello unico elemento che viene modificato è hello gli indirizzi IP virtuali (VIP) per le distribuzioni di hello.

    toosave calcolo dei costi, è possibile eliminare la distribuzione di hello in hello ambiente di gestione temporanea quando si è certi nuova distribuzione di produzione hello funzionando come previsto.

### <a name="common-questions-about-swapping-deployments"></a>Domande comuni sullo scambio di distribuzioni

**Quali sono i prerequisiti hello per le distribuzioni di effettuare lo swapping?**

Esistono due prerequisiti chiave per lo scambio corretto di distribuzioni:

- Se si desidera usare un indirizzo IP statico toouse slot di produzione, è necessario riservare uno slot di gestione temporanea anche. In caso contrario, lo scambio di hello avrà esito negativo.

- Tutte le istanze dei ruoli devono essere in esecuzione prima di poter eseguire lo scambio di hello. È possibile controllare lo stato di hello delle istanze in hello portale di Azure classico o mediante [hello comando Get-AzureRole in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Si noti che gli aggiornamenti del sistema operativo guest e le operazioni di correzione del servizio può essere causato anche toofail lo scambio di distribuzione. Per altre informazioni, vedere [Risolvere eventuali problemi di distribuzione dei servizi cloud](cloud-services-troubleshoot-deployment-problems.md).

**Uno scambio comporta un tempo di inattività per l'applicazione? Come gestire questa situazione?**

Come descritto nella sezione precedente di hello, lo scambio di distribuzioni in genere è molto veloce perché è solo una modifica della configurazione nel servizio di bilanciamento carico di Azure hello. In alcuni casi, tuttavia, può richiedere più di dieci secondi e causare errori di connessione temporanei. i clienti tooyour impatto toolimit, si consiglia di implementare [logica di ripetizione dei client](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Procedura: collegamento di un servizio cloud di risorse tooa
tooshow le dipendenze del servizio cloud su altre risorse, è possibile collegare un'istanza di Database SQL di Azure o un servizio di cloud toohello account di archiviazione. È possibile collegare e scollegare risorse hello **risorse collegate** pagina e quindi monitorarne l'utilizzo nel dashboard del servizio cloud hello. Se un account di archiviazione collegato ha attivato il monitoraggio, è possibile monitorare Totale richieste nel dashboard del servizio cloud hello.

Utilizzare **collegamento** toolink un nuovo o esistente del Database SQL istanza o archiviazione account tooyour servizio cloud. È quindi possibile scalare il database di hello insieme al ruolo del servizio cloud hello che è utilizzandolo su hello **scala** pagina. (un account di archiviazione viene scalato automaticamente man mano che aumenta l'utilizzo). Per ulteriori informazioni, vedere [come tooScale un servizio Cloud e le risorse collegate](cloud-services-how-to-scale.md).

È anche possibile monitorare, gestire e scalare il database di hello in hello **database** nodo di hello portale di Azure classico.

Una risorsa in questo senso di "collegamento" non connessione la risorsa toohello app. Se si crea un nuovo database utilizzando **collegamento**, sarà necessario tooadd hello connessione stringhe tooyour codice dell'applicazione e servizio cloud hello quindi eseguire l'aggiornamento. Le stringhe di connessione tooadd è necessario anche se l'app Usa le risorse in un account di archiviazione collegato.

Hello seguente procedura descrive come toolink una nuova istanza di Database SQL, distribuita in un nuovo server di Database SQL, il servizio di cloud tooa.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink servizio cloud tooa istanza Database SQL
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**. Quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
2. Fare clic su **Linked Resources**.

    Hello **risorse collegate** verrà visualizzata la pagina.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Fare clic su **Collega una risorsa** o **Collega**.

    Hello **collega risorsa** avviata.

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Fare clic su **Crea una nuova risorsa** o **Collega una risorsa esistente**.
5. Scegliere il tipo di hello di toolink di risorse. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **Database SQL**. (Solo hello portale di Azure classico supporta il collegamento di un servizio di cloud tooa account di archiviazione).
6. configurazione del database hello toocomplete, seguire le istruzioni nella Guida per hello **database SQL** area del portale di Azure classico hello.

    È possibile seguire lo stato di avanzamento hello di hello collegare nell'area dei messaggi hello.

    Quando il collegamento è stato completato, è possibile monitorare lo stato di hello della risorsa collegata hello nel dashboard del servizio cloud hello. Per informazioni sulla scalabilità di un Database SQL collegato, vedere [come tooScale un servizio Cloud e le risorse collegate](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>toounlink una risorsa collegata
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**. Quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.
2. Fare clic su **risorse collegate**, quindi selezionare la risorsa hello.
3. Fare clic su **Unlink**. Quindi fare clic su **Sì** al prompt di conferma hello.

    Lo scollegamento di un Database SQL non ha effetto sul database di hello o dell'applicazione hello connessioni toohello. È comunque possibile gestire database hello in hello **database SQL** area del portale di Azure classico hello.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Procedura: Eliminare le distribuzioni e un servizio cloud
Per eliminare un servizio cloud è necessario prima eliminare tutte le distribuzioni esistenti.

toosave calcolo dei costi, dopo aver verificato che la distribuzione di produzione funzioni come previsto, è possibile eliminare la distribuzione di gestione temporanea. I costi di calcolo per le istanze del ruolo vengono addebitati anche se il servizio cloud non è in esecuzione.

Utilizzare hello seguendo procedure toodelete una distribuzione o il servizio cloud.

1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**.
2. Selezionare servizio cloud hello e quindi fare clic su **eliminare**. (tooselect un servizio cloud senza dover aprire il dashboard di hello, fare clic in un punto qualsiasi tranne il nome di hello nella voce di servizio cloud hello.)

    Se si dispone di una distribuzione in gestione temporanea o produzione, si verrà visualizzato un menu di opzioni di toohello simile segue quello nella parte inferiore di hello della finestra hello. Prima di poter eliminare il servizio di cloud hello, è necessario eliminare tutte le distribuzioni esistenti.

    ![Menu Delete](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. Fare clic su una distribuzione, toodelete **Elimina la distribuzione di produzione** o **Elimina la distribuzione di gestione temporanea**. Al prompt di conferma hello, quindi fare clic su **Sì**.
4. Se si prevede di servizio cloud di hello toodelete, ripetere il passaggio 3, se necessario, toodelete l'altra distribuzione.
5. servizio cloud di hello toodelete, fare clic su **servizio cloud Delete**. Al prompt di conferma hello, quindi fare clic su **Sì**.

> [!NOTE]
> Se il monitoraggio dettagliato è configurato per il servizio cloud, Azure non elimina i dati di monitoraggio dall'account di archiviazione quando si elimina il servizio di cloud hello hello. Sarà necessario dati hello toodelete manualmente. Per informazioni su dove toofind hello tabelle di metrica, vedere "procedura: accedere ai dati di monitoraggio dettagliato di fuori di hello portale di Azure classico" in [come servizi Cloud tooMonitor](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).
