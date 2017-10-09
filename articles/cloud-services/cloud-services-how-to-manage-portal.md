---
title: "attività di gestione del servizio cloud aaaCommon | Documenti Microsoft"
description: Informazioni su come dei servizi cloud toomanage in hello portale di Azure. Questi esempi utilizzano hello portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

In hello **servizi Cloud (classico)** area di hello Azure portale, è possibile aggiornare un ruolo del servizio o una distribuzione, alzare di livello un tooproduction pre-distribuzione, collegare servizio cloud di risorse tooyour in questo modo è possibile visualizzare risorse hello dipendenze e la scala hello risorse insieme ed eliminare un servizio cloud o una distribuzione.

Ulteriori informazioni su come tooscale il servizio cloud è disponibile [qui](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Procedura: Aggiornare un ruolo o una distribuzione del servizio cloud
Se è necessario codice dell'applicazione hello tooupdate per il servizio cloud, utilizzare **aggiornamento** nel Pannello di servizio cloud hello. È possibile aggiornare un singolo ruolo o tutti i ruoli. tooupdate, è possibile caricare un nuovo pacchetto del servizio o un file di configurazione del servizio.

1. In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da tooupdate. Questo passaggio apre il pannello di istanza del servizio cloud hello.
2. Nel Pannello di hello, fare clic su hello **aggiornamento** pulsante.

    ![Pulsante Aggiorna](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Aggiornare la distribuzione di hello con un nuovo file del pacchetto del servizio (con estensione cspkg) e i file di configurazione del servizio (cscfg).

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Facoltativamente** aggiornare l'etichetta della distribuzione hello e account di archiviazione hello.
5. Se i ruoli hanno solo un'istanza del ruolo, selezionare hello **Distribuisci anche se uno o più ruoli contengono una singola istanza** tooenable hello aggiornamento tooproceed.

    Durante un aggiornamento del servizio cloud, Azure può garantire una percentuale di disponibilità del servizio pari solo al 99,95% se ogni ruolo contiene almeno due istanze del ruolo (macchine virtuali). Con due istanze del ruolo, una macchina virtuale elabora le richieste client mentre altri hello viene aggiornato.

6. Controllare **avviare distribuzione** aggiornamento hello toohave applicato dopo il caricamento di hello del pacchetto di hello è terminata.
7. Fare clic su **OK** toobegin hello servizio di aggiornamento.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Procedura: scambiare le distribuzioni toopromote tooproduction una distribuzione di gestione temporanea
Quando si decide di toodeploy una nuova versione di un servizio cloud, fase e testare la nuova release dell'ambiente di gestione temporanea del servizio cloud. Utilizzare **scambiare** tooswitch hello URL da cui hello due distribuzioni vengono indirizzate e alzare di livello un nuovo tooproduction versione.

È possibile scambiare le distribuzioni da hello **servizi Cloud** hello o pagina dashboard.

1. In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da tooupdate. Questo passaggio apre il pannello di istanza del servizio cloud hello.
2. Nel Pannello di hello, fare clic su hello **scambiare** pulsante.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Hello richiesta di conferma seguente viene aperto.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Dopo aver verificato le informazioni di distribuzione hello, fare clic su **OK** distribuzioni hello tooswap.

    lo scambio di distribuzioni Hello possa avvenire rapidamente perché hello unico elemento che viene modificato è hello gli indirizzi IP virtuali (VIP) per le distribuzioni di hello.

    toosave calcolo dei costi, è possibile eliminare hello distribuzione di gestione temporanea dopo aver verificato che la distribuzione di produzione funzioni come previsto.

### <a name="common-questions-about-swapping-deployments"></a>Domande comuni sullo scambio di distribuzioni

**Quali sono i prerequisiti hello per le distribuzioni di effettuare lo swapping?**

Esistono due prerequisiti chiave per lo scambio corretto di distribuzioni:

- Se si desidera usare un indirizzo IP statico toouse slot di produzione, è necessario riservare uno slot di gestione temporanea anche. In caso contrario, lo scambio di hello ha esito negativo.

- Tutte le istanze dei ruoli devono essere in esecuzione prima di poter eseguire lo scambio di hello. È possibile controllare lo stato di hello delle istanze del pannello della panoramica hello di hello portale di Azure. In alternativa, è possibile utilizzare hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando in Windows PowerShell.

Si noti che gli aggiornamenti del sistema operativo Guest e le operazioni di correzione del servizio può essere causato anche distribuzione Scambia toofail. Per altre informazioni, vedere [Risolvere eventuali problemi di distribuzione dei servizi cloud](cloud-services-troubleshoot-deployment-problems.md).

**Uno scambio comporta un tempo di inattività per l'applicazione? Come gestire questa situazione?**

Come descritto nella sezione precedente di hello, in quanto è solo una modifica della configurazione nel servizio di bilanciamento carico di Azure hello è rapido in genere uno scambio di distribuzione. In alcuni casi, tuttavia, può richiedere più di dieci secondi e causare errori di connessione temporanei. i clienti tooyour impatto toolimit, si consiglia di implementare [logica di ripetizione dei client](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Procedura: collegamento di un servizio cloud di risorse tooa
Hello portale di Azure non è collegato risorse insieme come hello corrente portale di Azure classico. In alternativa, distribuire risorse aggiuntive toohello stesso gruppo di risorse utilizzato dal servizio Cloud hello.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Procedura: Eliminare le distribuzioni e un servizio cloud
Per eliminare un servizio cloud è necessario prima eliminare tutte le distribuzioni esistenti.

toosave calcolo dei costi, è possibile eliminare hello distribuzione di gestione temporanea dopo aver verificato che la distribuzione di produzione funzioni come previsto. Vengono addebitati i costi di calcolo per le istanze del ruolo distribuite che sono state arrestate.

Utilizzare hello seguendo procedure toodelete una distribuzione o il servizio cloud.

1. In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da toodelete. Questo passaggio apre il pannello di istanza del servizio cloud hello.
2. Nel Pannello di hello, fare clic su hello **eliminare** pulsante.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. È possibile eliminare hello intero servizio cloud controllando **servizio Cloud e le relative distribuzioni** oppure scegliere uno hello **distribuzione di produzione** o hello **distribuzione di gestione temporanea**.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Fare clic su hello **eliminare** pulsante nella parte inferiore di hello.
5. servizio cloud di hello toodelete, fare clic su **servizio cloud Delete**. Al prompt di conferma hello, quindi fare clic su **Sì**.

> [!NOTE]
> Quando viene eliminato un servizio cloud e il monitoraggio dettagliato è configurato, è necessario eliminare manualmente i dati di hello dall'account di archiviazione. Per informazioni su dove toofind hello tabelle di metrica, vedere [questo](cloud-services-how-to-monitor.md) articolo.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Procedura: Trovare altre informazioni sulle distribuzioni non riuscite
Hello **Panoramica** blade dispone di una barra di stato nella parte superiore di hello. Quando si fa clic sulla barra di hello, un nuovo pannello aprirà e visualizzerà le informazioni di errore. Se la distribuzione di hello non contiene errori, pannello informazioni hello è vuoto.

![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).
