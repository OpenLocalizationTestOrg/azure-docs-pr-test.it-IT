---
title: aaaHow toouse hello Azure slave plug-in con l'integrazione continua di Hudson | Documenti Microsoft
description: Viene descritto come slave toouse hello Azure plug-in con l'integrazione continua di Hudson.
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Modalità slave toouse hello Azure plug-in con l'integrazione continua di Hudson
in fase di compilazione in esecuzione distribuita, Hello Azure slave plug-in per Hudson consente tooprovision i nodi secondari in Azure.

## <a name="install-hello-azure-slave-plug-in"></a>Installare hello Azure Slave plug-in
1. Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.
2. In hello **gestire Hudson** pagina, fare clic su **gestire plug-in**.
3. Fare clic su hello **disponibile** scheda.
4. Fare clic su **ricerca** e tipo **Azure** toolimit hello elenco toorelevant plug-in.
   
    Se si sceglie tooscroll elenco hello di plug-in disponibili, si noterà hello Azure slave plug-in hello **distribuita di compilazione e gestione dei Cluster** sezione hello **altri** scheda.
5. Selezionare una casella di controllo hello **plug-in Azure Slave**.
6. Fare clic su **Installa**.
7. Riavviare Hudson.

Ora è installato il plug-in hello, passaggi successivi hello sarebbe hello tooconfigure plug-in con il profilo di sottoscrizione di Azure e toocreate un modello che verrà utilizzato per la creazione di hello macchine Virtuali per nodo slave hello.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Configurare hello Azure Slave plug-in con il profilo di sottoscrizione
Un profilo di sottoscrizione, anche tooas cui le impostazioni di pubblicazione, è un file XML che contiene credenziali protette e informazioni aggiuntive, è necessario toowork con Azure nell'ambiente di sviluppo. tooconfigure hello Azure slave plug-in, è necessario:

* ID sottoscrizione personale
* Un certificato di gestione per la sottoscrizione

Questi elementi sono disponibili nel [profilo di sottoscrizione]. Di seguito è riportato un esempio di un profilo di sottoscrizione.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Dopo aver creato il profilo di sottoscrizione, seguire questi hello tooconfigure passaggi Azure slave plug-in.

1. Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.
2. Fare clic su **Configure System**.
3. Scorrere verso il basso hello di hello pagina toofind **Cloud** sezione.
4. Fare clic su **Add new cloud > Microsoft Azure** (Aggiungi nuovo cloud > Microsoft Azure).
   
    ![aggiungere nuovo cloud][add new cloud]
   
    Campi hello in cui è necessario tooenter verranno visualizzati i dettagli della sottoscrizione.
   
    ![configurare profilo][configure profile]
5. Copiare i certificati di gestione e l'id sottoscrizione hello dal profilo di sottoscrizione e incollarli nei campi appropriati hello.
   
    Quando si copia certificato di gestione e l'id di sottoscrizione hello, **non** includere hello virgolette che racchiudono i valori hello.
6. Fare clic su **Verify configuration**.
7. Quando si verifica configurazione hello correttamente, fare clic su **salvare**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Impostare un modello di macchina virtuale per hello Azure Slave plug-in
Un modello di macchina virtuale definisce i parametri di hello hello plug-in userà toocreate un nodo secondario in Azure. In hello alla procedura seguente si sarà creazione modello per una VM Ubuntu.

1. Nel dashboard di Hudson hello, fare clic su **gestire Hudson**.
2. Fare clic su **Configure System**.
3. Scorrere verso il basso hello di hello pagina toofind **Cloud** sezione.
4. All'interno di hello **Cloud** sezione, trovare **aggiungere modello di macchina virtuale di Azure** e fare clic su hello **Aggiungi** pulsante.
   
    ![aggiungere modello macchina virtuale][add vm template]
5. Specificare un nome di servizio cloud in hello **nome** campo. Se nome hello specificato fa riferimento tooan servizio cloud esistente, verrà eseguito il provisioning hello VM in quel servizio. In caso contrario, Azure ne creerà uno nuovo.
6. In hello **descrizione** immettere testo che descrive il modello di hello si sta creando. Queste informazioni sono esclusivamente a scopo di documentazione e non vengono utilizzate nel provisioning di una macchina virtuale.
7. In hello **etichette** immettere **linux**. Questa etichetta modello hello tooidentify usato che si sta creando e modello hello tooreference successivamente utilizzati durante la creazione di un processo Hudson.
8. Selezionare un'area in cui verrà creato hello macchina virtuale.
9. Selezionare dimensioni della macchina virtuale appropriata hello.
10. Specificare un account di archiviazione in cui verrà creato hello macchina virtuale. Assicurarsi che sia in hello stessa area hello del servizio cloud che verranno utilizzati. Se si desidera creare nuovo toobe di archiviazione, è possibile lasciare vuoto questo campo.
11. Periodo di conservazione hello numero di minuti prima dell'eliminazione di un secondario inattivo Hudson. Mantenere questa hello valore predefinito di 60.
12. In **utilizzo**, selezionare hello condizione appropriata quando verrà utilizzato questo nodo secondario. Per il momento, selezionare **Utilize this node as much as possible**.
    
     A questo punto, il modulo avrà un aspetto simile toothis:
    
     ![configurazione modello][template config]
13. In **famiglia di immagine o Id** è toospecify quale immagine del sistema verrà installato nella macchina virtuale. È possibile scegliere da un elenco di famiglie di immagini o specificare un'immagine personalizzata.
    
     Se si desidera tooselect da un elenco delle famiglie di immagine, immettere hello primo carattere (maiuscole/minuscole) del nome della famiglia hello immagine. Ad esempio, digitando **U** verrà visualizzato l'elenco delle famiglie di Ubuntu Server. Dopo aver selezionato dall'elenco di hello, Jenkins utilizzerà più recente di tale immagine del sistema da tale gruppo hello durante il provisioning di una macchina virtuale.
    
     ![elenco famiglie sistemi operativi][OS family list]
    
     Se si dispone di un'immagine personalizzata che si desidera invece toouse, immettere il nome di hello di tale immagine personalizzata. I nomi delle immagini personalizzate non vengono visualizzati in un elenco in modo che sia tooensure che hello nome sia stato immesso correttamente.    
    
     Per questa esercitazione, digitare **U** toobring un elenco di immagini Ubuntu e selezionare **Ubuntu Server 14.04 LTS**.
14. Per **Launch method** (Metodo di avvio), selezionare **SSH**.
15. Script hello seguente di copia e Incolla in hello **Init script** campo.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Hello **Init script** verrà eseguito dopo la creazione della macchina virtuale hello. In questo esempio, script hello installa ant Java e git.
16. In hello **Username** e **Password** campi, immettere i valori preferiti per l'account amministratore hello che verrà creato nella macchina virtuale.
17. Fare clic su **verificare modello** toocheck se i parametri di hello specificati sono validi.
18. Fare clic su **Save**.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Creare un processo Hudson eseguito in un nodo slave in Azure
In questa sezione si creerà un'attività di Hudson che verrà eseguita in un nodo slave in Azure.

1. Nel dashboard di Hudson hello, fare clic su **nuovo processo**.
2. Immettere un nome per il processo di hello che si sta creando.
3. Tipo di processo hello selezionare **compilazione di un processo software stile liberare**.
4. Fare clic su **OK**.
5. Nella pagina di configurazione processo hello, selezionare **limita l'accesso in cui è possibile eseguire questo progetto**.
6. Selezionare **nodo e l'etichetta del menu** e selezionare **linux** (è specificata questa etichetta quando si crea il modello di macchina virtuale hello nella sezione precedente hello).
7. In hello **compilare** fare clic su **istruzione di compilazione Aggiungi** e selezionare **eseguire shell**.
8. Modificare lo script seguente, la sostituzione di hello **{nome account github}**, **{nome del progetto}**, e **{directory del progetto}** con valori appropriati e incollare hello modificare uno script nell'area di testo hello che viene visualizzato.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Fare clic su **Save**.
10. In dashboard Hudson hello, trovare il processo di hello appena creato e fare clic su hello **pianificare una compilazione** icona.

Hudson verrà quindi creare un nodo secondario utilizzando il modello di hello creato nella sezione precedente hello e hello script specificato in fase di compilazione hello per questa attività.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

<!-- URL List -->

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[profilo di sottoscrizione]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

