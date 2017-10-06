---
title: aaaDeploy un bilanciamento di carico con connessione Internet con IPv6 - modello di Azure | Documenti Microsoft
description: Come toodeploy IPv6 supporta bilanciamento del carico di Azure e macchine virtuali di bilanciamento del carico.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Distribuire una soluzione di bilanciamento del carico con connessione Internet con IPv6 usando un modello

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interfaccia della riga di comando di Azure](load-balancer-ipv6-internet-cli.md)
> * [Modello](load-balancer-ipv6-internet-template.md)

Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP). servizio di bilanciamento del carico Hello garantisce disponibilità elevata mediante la distribuzione del traffico in entrata tra le istanze del servizio di integrità in servizi cloud o macchine virtuali in un set di bilanciamento del carico. Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.

## <a name="example-deployment-scenario"></a>Scenario di distribuzione di esempio

Hello diagramma seguente vengono illustrate soluzioni di bilanciamento del carico di hello distribuito utilizzando il modello di esempio hello descritto in questo articolo.

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

In questo scenario creerai hello seguendo le risorse di Azure:

* un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6
* un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6
* due bilanciamento regole toomap hello VIP toohello privato endpoint pubblici di carico
* un Set di disponibilità che contiene le macchine virtuali hello due
* due macchine virtuali (VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>La distribuzione del modello hello utilizzando hello portale di Azure

In questo articolo fa riferimento a un modello pubblicato in hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) raccolta. È possibile scaricare il modello di hello dalla raccolta hello o avviare la distribuzione di hello in Azure direttamente dalla raccolta hello. Questo articolo si presuppone che computer locale di hello modello tooyour è stato scaricato.

1. Aprire hello portale di Azure e accedere con un account che dispone delle autorizzazioni toocreate macchine virtuali e le risorse di rete all'interno di una sottoscrizione di Azure. Inoltre, a meno che non si utilizzano le risorse esistenti, hello account deve toocreate di autorizzazione per un gruppo di risorse e un account di archiviazione.
2. Fare clic su "+ nuovo" dal menu di hello quindi di tipo "modello" nella casella di ricerca hello. Selezionare i risultati della ricerca hello "Distribuzione del modello".

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. Hello tutti gli elementi nel pannello, fare clic su "Modello di distribuzione".

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Fare clic su "Crea".

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Fare clic su "Modifica modello". Eliminare il contenuto esistente hello e copiare e incollare nell'intero contenuto di hello hello del file di modello (tooinclude hello di inizio e fine {}), quindi fare clic su "Salva".

    > [!NOTE]
    > Se si utilizza Microsoft Internet Explorer, quando si incolla è visualizzata una finestra di dialogo chiesto negli Appunti di Windows tooallow accesso toohello. Fare clic su "Consenti accesso".

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Fare clic su "Modifica parametri". Nel Pannello di hello parametri, specificare i valori hello base alle linee guida hello in hello sezione parametri di modello, quindi fare clic su "Salva" tooclose hello parametri blade. Nel Pannello di distribuzione personalizzata hello, selezionare la sottoscrizione, un gruppo di risorse esistente o crearne uno. Se si sta creando un gruppo di risorse, quindi selezionare un percorso per il gruppo di risorse hello. Successivamente, fare clic su **legali**, quindi fare clic su **acquisto** per le note legali hello. Azure consente di iniziare la distribuzione delle risorse di hello. Sono necessari diversi minuti toodeploy tutte le risorse di hello.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Per ulteriori informazioni su questi parametri, vedere hello [variabili e parametri di modello](#template-parameters-and-variables) sezione più avanti in questo articolo.

7. risorse di hello toosee create dal modello hello, fare clic su Sfoglia, scorrere verso il basso elenco hello fino a quando non si vedere "Gruppi di risorse", quindi farvi clic sopra.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Nel Pannello di gruppi di risorse hello, fare clic sul nome hello hello del gruppo di risorse specificato nel passaggio 6. Viene visualizzato un elenco di tutte le risorse di hello che sono stati distribuiti. Se non si sono verificati errori, verrà visualizzato "Riuscito" in "Ultima distribuzione". In caso contrario, verificare che l'account di hello in uso disponga le risorse necessarie autorizzazioni toocreate hello.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Se si seleziona i gruppi di risorse subito dopo aver completato il passaggio 6, "Ultima distribuzione" verrà visualizzati lo stato di hello della "Distribuzione" vengono distribuite le risorse di hello.

9. Fare clic su "myIPv6PublicIP" nell'elenco di hello delle risorse. Vedrai che contiene un indirizzo IPv6 in indirizzo IP, e che il nome DNS sia il valore di hello specificato per il parametro dnsNameforIPv6LbIP hello nel passaggio 6. Questa risorsa è hello pubblico IPv6 indirizzo e il nome host che è accessibili tooInternet-i client.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Convalidare la connettività

Quando il modello di hello sia stata distribuita correttamente, è possibile convalidare la connettività completando hello seguenti attività:

1. Accedi toohello portale di Azure e connettersi tooeach di macchine virtuali create con la distribuzione modello hello hello. Se è stata distribuita una macchina virtuale Windows Server, eseguire ipconfig /all da un prompt dei comandi. Vengono visualizzate le macchine virtuali hello contengono gli indirizzi IPv4 e IPv6. Se è stato distribuito le macchine virtuali Linux, è necessario tooconfigure hello del sistema operativo Linux tooreceive dinamico gli indirizzi IPv6 utilizzando istruzioni hello fornite per la distribuzione di Linux.
2. Da un client connesso a Internet IPv6, avviare un indirizzo IPv6 di pubblico toohello connessione del servizio di bilanciamento del carico hello. tooconfirm che hello bilanciamento del carico è bilanciamento del carico tra macchine virtuali hello due, è possibile installare un server web come Microsoft Internet Information Services (IIS) in ognuna delle macchine virtuali hello. pagina web predefinita di Hello in ogni server può contenere testo hello "Server0" o "Server1" toouniquely identificarlo. Quindi, aprire un browser Internet in un client connesso a Internet IPv6 e passare il nome host toohello specificato per il parametro dnsNameforIPv6LbIP hello di hello carico bilanciamento tooconfirm end-to-end IPv6 connettività tooeach macchina virtuale. Se viene visualizzato solo hello di pagina web da un solo server, potrebbe essere necessario tooclear cache del browser. Aprire più sessioni di esplorazione private. Verrà visualizzata una risposta da ogni server.
3. Da un client connesso a Internet IPv4, avviare connessione toohello indirizzo IPv4 pubblico del servizio di bilanciamento del carico hello. tooconfirm che hello bilanciamento del carico è il bilanciamento del carico hello due macchine virtuali, è possibile testare l'utilizzo di IIS, come descritto nel passaggio 2.
4. Da ogni macchina virtuale, avviare una connessione in uscita tooan IPv6 o un dispositivo connesso IPv4 Internet. In entrambi i casi, hello IP di origine rilevato da dispositivo di destinazione hello è hello pubblica indirizzo IPv4 o IPv6 di bilanciamento del carico hello.

> [!NOTE]
> ICMP per IPv4 e IPv6 è bloccato in hello rete di Azure. Di conseguenza, gli strumenti ICMP come il ping hanno sempre esito negativo. connettività tootest, utilizzare un'alternativa TCP, ad esempio TCPing o i cmdlet di PowerShell Test-NetConnection hello. Si noti che gli indirizzi IP hello illustrati nel diagramma hello sono esempi di valori che potrebbero verificarsi. Poiché gli indirizzi IPv6 hello vengono assegnati in modo dinamico, gli indirizzi di hello che ricevi variano e possono variare in base a region. Inoltre, è comune per l'indirizzo IPv6 pubblico hello in toostart del servizio di bilanciamento carico di hello con un prefisso diverso rispetto a hello indirizzi IPv6 nel pool back-end hello.

## <a name="template-parameters-and-variables"></a>Parametri e variabili del modello

Un modello di gestione risorse di Azure contiene più variabili e parametri che è possibile personalizzare tooyour esigenze. Per usare valori fissi che non si desidera un toochange utente vengono utilizzate variabili. Per i valori vengono utilizzati parametri che si desidera un tooprovide utente quando si distribuisce il modello di hello. modello di esempio Hello è configurato per uno scenario di hello descritto in questo articolo. È possibile personalizzare questo tooneeds dell'ambiente.

esempio Hello modello utilizzato in questo articolo include seguente hello variabili e parametri:

| Parametro / variabile | Note |
| --- | --- |
| adminUsername |Specificare il nome di hello hello dell'account dell'amministratore utilizzata toosign nelle macchine virtuali toohello con. |
| adminPassword |Specificare la password di hello per l'account amministratore hello utilizzato toosign nelle macchine virtuali toohello con. |
| dnsNameforIPv4LbIP |Specificare nome host DNS di hello desiderati tooassign come nome pubblico di hello del bilanciamento del carico hello. Questo nome viene risolto l'indirizzo IPv4 pubblico del toohello di bilanciamento del carico. Hello deve essere in minuscolo e corrisponde a regex hello: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Specificare nome host DNS di hello desiderati tooassign come nome pubblico di hello del bilanciamento del carico hello. Questo nome viene risolto indirizzo IPv6 del toohello di bilanciamento del carico pubblico. Hello deve essere in minuscolo e corrisponde a regex hello: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Può trattarsi di hello stesso nome come hello indirizzo IPv4. Quando un client invia una query DNS per il nome di Azure restituisce sia hello A e AAAA quando nome hello viene condiviso. |
| vmNamePrefix |Specificare prefisso del nome di macchina virtuale hello. modello Hello aggiunge un numero (0, 1, e così via) nome toohello quando hello macchine virtuali vengono create. |
| nicNamePrefix |Specificare prefisso del nome dell'interfaccia di rete hello. modello Hello aggiunge un numero (0, 1, e così via) toohello nome quando vengono create le interfacce di rete hello. |
| storageAccountName |Immettere il nome di hello di un account di archiviazione esistente o specificare il nome di hello di un nuovo uno toobe creati dal modello hello. |
| availabilitySetName |Immettere quindi il nome della disponibilità di hello set toobe utilizzato con hello macchine virtuali |
| addressPrefix |prefisso dell'indirizzo Hello utilizzato l'intervallo di indirizzi toodefine hello di hello rete virtuale |
| subnetName |nome Hello di subnet di hello creato per hello rete virtuale |
| subnetPrefix |prefisso dell'indirizzo Hello utilizzato l'intervallo di indirizzi hello toodefine della subnet hello |
| vnetName |Specificare il nome di hello per hello rete virtuale utilizzato da hello macchine virtuali. |
| ipv4PrivateIPAddressType |metodo di allocazione Hello utilizzato per hello privato indirizzo IP (statica o dinamica) |
| ipv6PrivateIPAddressType |metodo di allocazione Hello utilizzato per hello private indirizzo IP (dinamico). IPv6 supporta solo l'allocazione dinamica. |
| numberOfInstances |numero di Hello del carico bilanciato istanze distribuite dal modello hello |
| ipv4PublicIPAddressName |Specificare nome DNS hello desiderato toocommunicate toouse con indirizzo IPv4 pubblico hello di bilanciamento del carico hello. |
| ipv4PublicIPAddressType |metodo di allocazione Hello usato per hello indirizzo IP pubblico (statica o dinamica) |
| Ipv6PublicIPAddressName |Specificare nome DNS hello desiderato toocommunicate toouse con l'indirizzo IPv6 pubblico hello di bilanciamento del carico hello. |
| ipv6PublicIPAddressType |metodo di allocazione Hello utilizzato per l'indirizzo IP pubblico hello (dinamico). IPv6 supporta solo l'allocazione dinamica. |
| lbName |Specificare il nome di hello di bilanciamento del carico hello. Questo nome viene visualizzato nel portale di hello o utilizzato quando si fa riferimento tooit con un comando CLI o PowerShell. |

le variabili rimanenti di Hello nel modello hello contengono valori derivati assegnati quando Azure crea risorse hello. Non modificare queste variabili.
