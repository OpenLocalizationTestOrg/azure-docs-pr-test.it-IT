---
title: aaaSubmit tooan di processi HPC Pack del cluster in Azure | Documenti Microsoft
description: Informazioni su come tooset backup un toosubmit del computer locale i processi cluster HPC Pack tooan in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Inviare i processi HPC da un cluster di HPC Pack locale computer tooan distribuito in Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configurare un tooa di processi locali client computer toosubmit [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure. Questo articolo illustra come tooset in un computer client locale strumenti toosubmit processo su cluster toohello HTTPS in Azure. In questo modo, più utenti di cluster possono inviare processi tooa basato su cloud cluster HPC Pack, ma senza la connessione diretta toohello macchina virtuale del nodo head o l'accesso a una sottoscrizione di Azure.

![Invio di un cluster di tooa processo in Azure][jobsubmit]

## <a name="prerequisites"></a>Prerequisiti
* **Nodo head di HPC Pack distribuito in una macchina virtuale di Azure** -è consigliabile utilizzare strumenti automatizzati, ad esempio un [modello di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) o [script Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nodo head di toodeploy hello e cluster. È necessario il nome DNS hello del nodo head hello e credenziali di hello di un amministratore cluster per completare i passaggi di hello in questo articolo.
* **Computer client** : è necessario un computer client Windows o Windows server in grado di eseguire le utilità client di HPC Pack (vedere i [requisiti di sistema](https://technet.microsoft.com/library/dn535781.aspx)). Se si desidera solo portale web di HPC Pack hello toouse o processi toosubmit API REST, è possibile utilizzare tutti i computer client di propria scelta.
* **Supporto di installazione di HPC Pack** -tooinstall hello utilità client di HPC Pack, il pacchetto di installazione gratuito hello per la versione più recente di HPC Pack (HPC Pack 2012 R2) è disponibile il [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Assicurarsi di scaricare hello stessa versione di HPC Pack installato nel nodo head hello macchina virtuale.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Passaggio 1: Installare e configurare i componenti web di hello nel nodo head hello
tooenable un cluster toohello di processi toosubmit di interfaccia REST su HTTPS, assicurarsi che i componenti web di HPC Pack hello siano configurati nel nodo head di HPC Pack hello. Se non sono già installati, installare i componenti web di hello eseguendo il file di installazione HpcWebComponents.msi hello. Quindi, configurare i componenti di hello eseguendo uno script di HPC PowerShell hello **set-hpcwebcomponents.ps1**.

Per le procedure dettagliate, vedere [installare i componenti Web di hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Alcuni modelli di avvio rapido di Azure per HPC Pack installare e configurare i componenti web di hello automaticamente. Se si utilizza hello [script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) cluster hello toocreate, è facoltativamente possibile installare e configurare i componenti web di hello come parte della distribuzione hello.
> 
> 

**componenti web di hello tooinstall**

1. Connessione macchina virtuale del nodo head toohello utilizzando hello credenziali di amministratore del cluster.
2. Dalla cartella di installazione di HPC Pack hello, eseguire HpcWebComponents.msi nel nodo head hello.
3. Seguire i passaggi hello nei componenti web di hello guidata tooinstall hello

**componenti web di hello tooconfigure**

1. Nel nodo head hello, avviare HPC PowerShell come amministratore.
2. toochange toohello percorso della directory dello script di configurazione hello, hello tipo comando seguente:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure hello interfaccia REST e avviare hello servizio Web HPC, hello tipo comando seguente:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Quando richiesto tooselect un certificato, scegliere il certificato di hello corrispondente toohello nome DNS pubblico del nodo head hello. Ad esempio, se si distribuisce nodo head di hello macchina virtuale utilizzando il modello di distribuzione classica hello, nome certificato hello è simile a CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Se si Usa modello di distribuzione di gestione risorse di hello, nome certificato hello simile CN =&lt;*HeadNodeDnsName*&gt;.&lt; *area*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Selezionare il certificato in un secondo momento quando si invia nodo head toohello di processi da un computer locale. Non selezionare né configurare un certificato corrispondente al nome del computer del nodo head di hello nel dominio di Active Directory hello toohello (ad esempio CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. portale web di hello tooconfigure per l'invio di processi, hello tipo comando seguente:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Al termine dell'esecuzione dello script hello, arrestare e riavviare il servizio Utilità di pianificazione processi HPC hello digitando hello seguenti comandi:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Passaggio 2: Installare le utilità client di HPC Pack hello in un computer locale
Se si desidera utilità client di HPC Pack hello tooinstall nel computer in uso, scaricare i file di installazione di HPC Pack (installazione completa) dal hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Quando si inizia installazione hello, scegliere l'opzione di installazione di hello per hello **utilità client di HPC Pack**.

nodo head di toohello processi toosubmit VM degli strumenti client di HPC Pack hello toouse, inoltre necessario un certificato dal nodo head hello tooexport e installarlo nel computer client hello. deve essere certificato Hello. Formato CER.

**certificato di hello tooexport dal nodo head hello**

1. Nel nodo head hello, aggiungere hello certificati snap-in tooa Microsoft Management Console per hello account Computer locale. Per i passaggi tooadd hello snap-in, vedere [aggiungere hello Snap-in certificati tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. Nella struttura della console hello espandere **certificati-Computer locale** > **personale**, quindi fare clic su **certificati**.
3. Individuare il certificato hello configurato per i componenti web di HPC Pack hello in [passaggio 1: installare e configurare i componenti web di hello nel nodo head hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (ad esempio CN =&lt;*HeadNodeDnsName* &gt;. n e t).
4. Fare doppio clic su certificato hello e fare clic su **tutte le attività** > **esportare**.
5. In hello esportazione guidata certificati, fare clic su **Avanti**e assicurarsi che **No, non esportare la chiave privata di hello** è selezionata.
6. Seguire hello rimanenti passaggi di hello guidata tooexport hello certificato DER con codifica binaria x. 509 (. Formato CER).

**certificato di hello tooimport nel computer client hello**

1. Copiare il certificato hello esportato da hello nodo head tooa cartella hello computer client.
2. Nel computer client hello eseguire certmgr. msc.
3. In Gestione certificati espandere **Certificati - Utente corrente** > **Autorità di certificazione principale attendibili**, fare clic con il pulsante destro del mouse su **Certificati**, quindi fare clic su **All Tasks** (Tutte le attività) > **Importa**.
4. In Importazione guidata certificati hello, fare clic su **Avanti** e seguire hello passaggi tooimport hello certificato esportato dal hello nodo head toohello archivio Autorità di certificazione radice attendibili.

> [!TIP]
> È possibile visualizzare un avviso di sicurezza, perché l'autorità di certificazione hello nel nodo head hello non viene riconosciuto dal computer client hello. A scopo di test, è possibile ignorare questo avviso e completamento importazione del certificato hello.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Passaggio 3: Eseguire test processi nel cluster hello
la configurazione, riprovare i processi in esecuzione su hello cluster in Azure da hello tooverify locale computer. Ad esempio, è possibile utilizzare gli strumenti di HPC Pack GUI o i comandi della riga di comando toosubmit processi toohello cluster. È possibile utilizzare anche un processi toosubmit portale basato sul web.

**toorun i comandi di invio processi nel computer client hello**

1. In un computer client in cui sono installate utilità client di HPC Pack hello, avviare un prompt dei comandi.
2. Digitare un comando di esempio. Ad esempio, toolist tutti i processi nel cluster hello, digitare un comando di simili tooone di hello seguenti, in base al nome DNS completo hello del nodo head hello:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    oppure
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Utilizzare hello nome DNS completo del nodo head hello, non hello indirizzo IP nell'URL dell'utilità di pianificazione hello. Se si specifica l'indirizzo IP di hello, viene visualizzato un errore simile troppo "certificato server hello deve tooeither presentano una catena di trust o toobe inserito nell'archivio radice attendibile hello valida."
   > 
   > 
3. Quando richiesto, digitare il nome di utente hello (in formato hello &lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore di cluster HPC hello o un altro utente cluster configurato. È possibile scegliere toostore credenziali hello in locale per più operazioni del processo.
   
    Verrà visualizzato un elenco di processi.

**toouse Gestione processi HPC nel computer client hello**

1. Se si non archiviano le credenziali di dominio per un utente del cluster in precedenza durante l'invio di un processo, è possibile aggiungere le credenziali di hello in Gestione credenziali.
   
    a. Nel Pannello di controllo su computer client hello, avviare Gestione credenziali.
   
    b. Fare clic su **Credenziali Windows** > **Aggiungi credenziali generiche**.
   
    c. Specificare l'indirizzo Internet hello (ad esempio https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler o https://&lt;HeadNodeDnsName&gt;.&lt; area&gt;.cloudapp.azure.com/HpcScheduler) e il nome utente hello (&lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore di cluster hello o un altro utente cluster configurato.
2. Nel computer client hello, avviare Gestione processi HPC.
3. In hello **Seleziona nodo Head** della finestra di dialogo tipo hello URL toohello nodo head in Azure (ad esempio https://&lt;HeadNodeDnsName&gt;. c o https://&lt;HeadNodeDnsName&gt;. &lt;area&gt;. cloudapp.azure.com).
   
    Gestione processi HPC apre e visualizza un elenco di processi nel nodo head hello.

**portale web di hello toouse in esecuzione nel nodo head hello**

1. Avviare un web browser nel computer client hello e immettere uno dei seguenti indirizzi, in base al nome DNS completo hello del nodo head hello hello:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    oppure
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. In hello protezione della finestra di dialogo visualizzata digitare le credenziali di dominio hello del messaggio per l'amministratore cluster HPC. È anche possibile aggiungere altri utenti cluster in ruoli diversi. Vedere [Gestione degli utenti del cluster](https://technet.microsoft.com/library/ff919335.aspx).
   
    visualizzazione elenco dei processi toohello viene visualizzato il portale web di Hello.
3. Fare clic su un processo di esempio che restituisce la stringa hello "Hello World" dal cluster hello, toosubmit **nuovo processo** nella navigazione a sinistra di hello.
4. In hello **nuovo processo** pagina **dalle pagine di invio**, fare clic su **HelloWorld**. verrà visualizzata la pagina di invio processo Hello.
5. Fare clic su **Submit**. Se richiesto, fornire le credenziali di dominio hello del messaggio per l'amministratore cluster HPC. il processo di Hello viene inviato e viene visualizzato l'ID di processo hello hello **processi personali** pagina.
6. risultati di hello tooview hello del processo di cui è stata inviata, fare clic su ID di processo hello e quindi fare clic su **Visualizza attività** output del comando hello tooview (in **Output**).

## <a name="next-steps"></a>Passaggi successivi
* È inoltre possibile inviare i processi toohello cluster Azure con hello [API REST di HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Se si desidera toosubmit i processi di cluster da un client Linux, vedere hello Python sample in hello [HPC Pack 2012 R2 SDK e codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
