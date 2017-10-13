---
title: "Attività comuni di gestione di servizi cloud (versione classica)| Microsoft Docs"
description: Informazioni su come gestire i servizi cloud nel portale di Azure classico.
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
ms.openlocfilehash: 2ee76dfcb579e53975b1f61a6590f8d78dc0961b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-manage-cloud-services"></a>Come gestire i servizi cloud
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-manage-portal.md)
> * [Portale di Azure classico](cloud-services-how-to-manage.md)
>
>

Nell'area **Servizi cloud** del portale di Azure classico è possibile aggiornare un ruolo di servizio o una distribuzione, convertire una distribuzione di gestione temporanea in una distribuzione di produzione, collegare risorse al servizio cloud per visualizzare le dipendenze delle risorse e scalare le risorse insieme, nonché eliminare un servizio cloud o una distribuzione.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Procedura: Aggiornare un ruolo o una distribuzione del servizio cloud
Se è necessario aggiornare il codice dell'applicazione per il servizio cloud, usare **Aggiorna** nel dashboard, pagina **Servizi cloud** o pagina **Istanze**. È possibile aggiornare un singolo ruolo o tutti i ruoli. Sarà necessario caricare un nuovo pacchetto del servizio e un nuovo file di configurazione del servizio.

1. Nel dashboard del [portale di Azure classico](https://manage.windowsazure.com/) fare clic su **Aggiorna** nella pagina **Servizi cloud** o nella pagina **Istanze**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. In **Etichetta distribuzione**, immettere un nome per identificare la distribuzione (ad esempio, mycloudservice4). L'etichetta di distribuzione è disponibile nella **Guida introduttiva** nel dashboard.
3. In **Pacchetto** usare **Sfoglia** per caricare il file del pacchetto di servizio (.cspkg).
4. In **Configurazione** usare **Sfoglia** per caricare il file di configurazione del servizio (.cscfg).
5. In **Ruolo** selezionare **Tutto** per aggiornare tutti i ruoli nel servizio cloud. Per eseguire l'aggiornamento di un singolo ruolo, selezionare il ruolo da aggiornare. Anche se si seleziona un ruolo specifico per l'aggiornamento, gli aggiornamenti nel file di configurazione del servizio vengono applicati a tutti i ruoli.
6. Se l'aggiornamento cambia il numero o le dimensioni dei ruoli, selezionare la casella di controllo **Consenti aggiornamento se cambiano le dimensioni o il numero dei ruoli** per consentire all'aggiornamento di proseguire.

    Tenere presente che se si modificano le dimensioni di un ruolo, ovvero le dimensioni di una macchina virtuale che ospita un'istanza del ruolo, o il numero dei ruoli, è necessario ricreare l'immagine di ogni istanza del ruolo (macchina virtuale) e i dati locali andranno persi.

7. Se uno o più ruoli del servizio contengono una sola istanza del ruolo, selezionare la casella di controllo **Eseguire l'aggiornamento anche se uno o più ruoli contengono una sola istanza** per consentire l'esecuzione dell'aggiornamento.

    Durante un aggiornamento del servizio cloud, Azure può garantire una percentuale di disponibilità del servizio pari solo al 99,95% se ogni ruolo contiene almeno due istanze del ruolo (macchine virtuali). In questo modo, una macchina virtuale può elaborare le richieste dei client mentre l'altra viene aggiornata.

8. Fare clic su **OK** (segno di spunta) per avviare l'aggiornamento del servizio.

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a>Procedura: Scambiare le distribuzioni per convertire una distribuzione di gestione temporanea in una distribuzione di produzione
Utilizzare **Swap** per convertire una distribuzione di gestione temporanea di un servizio cloud in una distribuzione di produzione. Quando si decide di distribuire una nuova versione di un servizio cloud, è possibile inserirla e testarla nell'ambiente di gestione temporanea del servizio cloud mentre i clienti usano la versione corrente in produzione. Quando la nuova versione è pronta per il passaggio in produzione, è possibile usare **Swap** per invertire gli URL di indirizzamento delle due distribuzioni.

È possibile scambiare le distribuzioni dalla pagina **Cloud Services** o dal dashboard.

1. Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Servizi cloud**.
2. Nell'elenco dei servizi cloud fare clic sul servizio cloud per selezionarlo.
3. Fare clic su **Swap**.

    Verrà visualizzata la seguente richiesta di conferma.

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Dopo avere controllato le informazioni sulla distribuzione, fare clic su **Yes** per scambiare le distribuzioni.

    Lo scambio delle distribuzioni avviene rapidamente perché l'unico elemento che cambia è rappresentato dagli indirizzi IP virtuali (VIP) delle distribuzioni.

    Per ridurre i costi di calcolo, è possibile eliminare la distribuzione nell'ambiente di gestione temporanea dopo avere verificato che le prestazioni della nuova distribuzione di produzione corrispondano alle aspettative.

### <a name="common-questions-about-swapping-deployments"></a>Domande comuni sullo scambio di distribuzioni

**Quali sono i prerequisiti per lo scambio delle distribuzioni?**

Esistono due prerequisiti chiave per lo scambio corretto di distribuzioni:

- Se si desidera usare un indirizzo IP statico per lo slot di produzione, è necessario riservarne uno anche per lo slot di gestione temporanea. In caso contrario, lo scambio avrà esito negativo.

- Tutte le istanze dei ruoli devono essere in esecuzione prima di poter eseguire lo scambio. È possibile controllare lo stato delle istanze nel portale di Azure classico o usando il [comando Get-AzureRole in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Si noti che anche gli aggiornamenti del sistema operativo guest e le operazioni di correzione del servizio possono ostacolare il corretto scambio delle distribuzioni. Per altre informazioni, vedere [Risolvere eventuali problemi di distribuzione dei servizi cloud](cloud-services-troubleshoot-deployment-problems.md).

**Uno scambio comporta un tempo di inattività per l'applicazione? Come gestire questa situazione?**

Come descritto nella sezione precedente, lo scambio di distribuzioni è in genere molto veloce perché è una semplice modifica della configurazione in Azure Load Balancer. In alcuni casi, tuttavia, può richiedere più di dieci secondi e causare errori di connessione temporanei. Per limitare l'impatto sui clienti, si consiglia di implementare la [logica di ripetizione dei tentativi nel client](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-to-a-cloud-service"></a>Procedura: Collegare una risorsa a un servizio cloud
Per visualizzare le dipendenze del servizio cloud da altre risorse, è possibile collegare un'istanza di database SQL di Azure o un account di archiviazione al servizio cloud. È possibile collegare o scollegare le risorse nella pagina **Risorse collegato** e monitorare quindi il relativo uso nel dashboard del servizio cloud. Se in un account di archiviazione collegato è attivato il monitoraggio, è possibile monitorare il totale delle richieste nel dashboard del servizio cloud.

Usare **Collegamento** per collegare un'istanza di database SQL nuova o esistente o un account di archiviazione al servizio cloud. È quindi possibile ridimensionare il database insieme al ruolo del servizio cloud che lo usa nella pagina **Piano**. (un account di archiviazione viene scalato automaticamente man mano che aumenta l'utilizzo). Per altre informazioni, vedere [Come ridimensionare un servizio cloud e le risorse collegate](cloud-services-how-to-scale.md).

È inoltre possibile monitorare, gestire e scalare il database nel nodo **Database** del portale di Azure classico.

In questo senso, il "collegamento" di una risorsa non comporta la connessione dell'app alla risorsa. Se si crea un nuovo database mediante **Link**, sarà necessario aggiungere le stringhe di connessione al codice dell'applicazione, quindi aggiornare il servizio cloud. Sarà anche necessario aggiungere le stringhe di connessione se l'app usa risorse in un account di archiviazione collegato.

Nella procedura seguente viene descritto come collegare una nuova istanza di database SQL, distribuita su un nuovo server di database SQL, a un servizio cloud.

### <a name="to-link-a-sql-database-instance-to-a-cloud-service"></a>Per collegare un'istanza di database SQL a un servizio cloud
1. Nel [portale di Azure classico](http://manage.windowsazure.com/)fare clic su **Servizi cloud**. Quindi fare clic sul nome del servizio cloud per aprire il dashboard.
2. Fare clic su **Linked Resources**.

    Verrà visualizzata la pagina **Linked Resources** .

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Fare clic su **Collega una risorsa** o **Collega**.

    Verrà avviata la procedura guidata **Link Resource** .

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Fare clic su **Crea una nuova risorsa** o **Collega una risorsa esistente**.
5. Scegliere il tipo di risorsa da collegare. Nel [portale di Azure classico](http://manage.windowsazure.com/)fare clic su **Database SQL**. Solo il portale di Azure classico supporta il collegamento di un account di archiviazione a un servizio cloud.
6. Per completare la configurazione del database, seguire le istruzioni nella guida per l'area **SQL Databases** del portale di Azure classico.

    È possibile seguire l'avanzamento dell'operazione di collegamento nell'area dei messaggi.

    Terminato il collegamento, è possibile monitorare lo stato della risorsa collegata nel dashboard del servizio cloud. Per informazioni sulla scalabilità di un database SQL collegato, vedere [Come scalare un servizio cloud e le risorse collegate](cloud-services-how-to-scale.md).

### <a name="to-unlink-a-linked-resource"></a>Per scollegare una risorsa collegata
1. Nel [portale di Azure classico](http://manage.windowsazure.com/)fare clic su **Servizi cloud**. Quindi fare clic sul nome del servizio cloud per aprire il dashboard.
2. Fare clic su **Linked Resources**e selezionare la risorsa.
3. Fare clic su **Unlink**. Fare quindi clic su **Yes** alla richiesta di conferma.

    Lo scollegamento di un database SQL non ha alcun effetto sul database o sulle connessioni dell'applicazione al database. È comunque possibile gestire il database nell'area **Database SQL** del portale di Azure classico.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Procedura: Eliminare le distribuzioni e un servizio cloud
Per eliminare un servizio cloud è necessario prima eliminare tutte le distribuzioni esistenti.

Per ridurre i costi di calcolo, è possibile eliminare la distribuzione di gestione temporanea dopo avere verificato che la distribuzione di produzione funzioni nel modo previsto. I costi di calcolo per le istanze del ruolo vengono addebitati anche se il servizio cloud non è in esecuzione.

Per eliminare una distribuzione o il servizio cloud, attenersi alla procedura seguente.

1. Nel [portale di Azure classico](http://manage.windowsazure.com/)fare clic su **Servizi cloud**.
2. Selezionare il servizio cloud e fare clic su **Elimina**. (per selezionare un servizio cloud senza aprire il dashboard, fare clic in un punto qualsiasi tranne che sul nome nella voce del servizio cloud).

    Se è presente una distribuzione di gestione temporanea o di produzione, nella parte inferiore della finestra sarà visualizzato un menu analogo al seguente. Prima di eliminare il servizio cloud, è necessario eliminare le eventuali distribuzioni esistenti.

    ![Menu Delete](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. Per eliminare una distribuzione, fare clic su **Delete production deployment** (Elimina distribuzione di produzione) o **Delete staging deployment** (Elimina distribuzione di staging). Quindi, alla richiesta di conferma fare clic su **Yes**.
4. Se si intende eliminare il servizio cloud, ripetere il passaggio 3, se necessario, per eliminare le altre distribuzioni.
5. Per eliminare il servizio cloud fare clic su **Delete cloud service**. Quindi, alla richiesta di conferma fare clic su **Yes**.

> [!NOTE]
> Se per il servizio cloud è configurato il monitoraggio dettagliato, i dati di monitoraggio dall'account di archiviazione non vengono eliminati quando si elimina il servizio cloud. I dati dovranno essere eliminati manualmente. Per informazioni sull'ubicazione delle tabelle delle metriche, vedere "Procedura: accedere ai dati di monitoraggio dettagliati all'esterno del portale di Azure classico" in [Come monitorare i servizi cloud](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).
* Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).
