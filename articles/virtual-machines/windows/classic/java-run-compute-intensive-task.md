---
title: applicazione Java con utilizzo intensivo aaaCompute in una macchina virtuale | Documenti Microsoft
description: "Informazioni su come toocreate una macchina virtuale di Azure che esegue un'applicazione Java con utilizzo intensivo di calcolo che può essere monitorata da un'altra applicazione Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Come attività toorun un uso intensivo di calcolo nel linguaggio in una macchina virtuale
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Con Azure, è possibile utilizzare una macchina virtuale toohandle calcolo intensivo. Ad esempio, una macchina virtuale può gestire le attività e recapitare macchine tooclient risultati o applicazioni per dispositivi mobili. Dopo aver letto questo articolo, si avrà una conoscenza di come toocreate una macchina virtuale che esegue un'applicazione Java con utilizzo intensivo di calcolo che può essere monitorata da un'altra applicazione Java.

In questa esercitazione si presuppone che conoscere come applicazioni di console toocreate Java, è possibile importare l'applicazione Java tooyour di librerie e può generare un file Java archive (JAR). Non è richiesta alcuna conoscenza di Microsoft Azure.

Si acquisiranno le nozioni seguenti:

* Come toocreate una macchina virtuale con Java Development Kit (JDK) già installato.
* Modalità di accesso nella macchina virtuale tooyour tooremotely.
* Come spazio dei nomi del bus toocreate un servizio.
* Come toocreate un'applicazione Java che esegue un'attività a elevato utilizzo di calcolo.
* Toocreate un'applicazione Java che consente di monitorare hello come stato di avanzamento dell'attività a elevato utilizzo di calcolo hello.
* Toorun hello come applicazioni Java.
* Toostop hello come applicazioni Java.

In questa esercitazione verrà utilizzato hello problema del commesso viaggiatore per attività complesse hello. Hello Ecco un esempio di hello Java applicazione in esecuzione hello complesse attività.

![Risolutore del Problema del commesso viaggiatore][solver_output]

Hello Ecco un esempio di hello Java applicazione hello complesse l'attività di monitoraggio.

![Client del Problema del commesso viaggiatore][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate una macchina virtuale
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Fare clic su **Nuovo**, **Calcolo**, **Macchina virtuale** e quindi su **Da raccolta**.
3. In hello **selezionare immagine di macchina virtuale** nella finestra di dialogo **JDK 7 Windows Server 2012**.
   Si noti che **JDK 6 Windows Server 2012** è disponibile nel caso in cui si dispone di applicazioni legacy che non sono ancora pronti toorun JDK 7.
4. Fare clic su **Avanti**.
5. In hello **configurazione della macchina virtuale** la finestra di dialogo:
   1. Specificare un nome per la macchina virtuale hello.
   2. Specificare hello toouse di dimensioni per la macchina virtuale hello.
   3. Immettere un nome per l'amministratore di hello in hello **nome utente** campo. Prendere nota della password nome e hello che passerà successivamente, verranno utilizzati quando si accede in remoto nella macchina virtuale toohello.
   4. Immettere una password in hello **nuova password** campo e immettere nuovamente in hello **conferma** campo. Si tratta di password dell'account amministratore hello.
   5. Fare clic su **Avanti**.
6. In hello Avanti **configurazione della macchina virtuale** la finestra di dialogo:
   1. Per **servizio Cloud**, utilizzare hello predefinito **creare un nuovo servizio cloud**.
   2. valore per Hello **nome DNS del servizio Cloud** deve essere univoco in cloudapp.net. Se necessario, modificarlo in modo che sia indicato come univoco in Azure.
   3. Specificare un'area, un gruppo di affinità o una rete virtuale. Ai fini di questa esercitazione, specificare come area **West US**.
   4. Nella casella **Account di archiviazione** selezionare **Usa un account di archiviazione generato automaticamente** .
   5. Nella casella **Set di disponibilità** selezionare **(Nessuno)**.
   6. Fare clic su **Avanti**.
7. In hello finale **configurazione della macchina virtuale** la finestra di dialogo:
   1. Accettare le voci di endpoint di hello predefinito.
   2. Fare clic su **Complete**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>log tooremotely nella macchina virtuale tooyour
1. Accesso toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Fare clic su **Virtual machines**.
3. Fare clic su nome hello della macchina virtuale hello che si desidera toolog in.
4. Fare clic su **Connetti**.
5. Risposta toohello chiede come macchina virtuale di toohello tooconnect necessari. Quando viene richiesta la password e il nome amministratore hello, usare valori hello forniti al momento della creazione macchina virtuale hello.

Si noti che la funzionalità di Azure Service Bus hello richiede toobe di certificato radice Baltimore CyberTrust hello installato come parte di JRE **cacerts** archiviare. Questo certificato viene inclusa automaticamente in hello Java Runtime Environment (JRE) utilizzato da questa esercitazione. Se non è il certificato nel JRE **cacerts** archiviare, vedere [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java] [ add_ca_cert] per informazioni sull'aggiunta del modello (così come informazioni sulla visualizzazione di hello certificati nell'archivio cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Come spazio dei nomi del bus toocreate un servizio
utilizzo di Service Bus toobegin le code in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio. che fornisce un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.

toocreate uno spazio dei nomi servizio:

1. Accesso toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro di navigazione a sinistra hello di hello portale di Azure classico, fare clic su **Service Bus, Access Control e la memorizzazione nella cache**.
3. Nel riquadro superiore sinistro di hello di hello portale di Azure classico, fare clic su hello **Bus di servizio** nodo, quindi fare clic su hello **New** pulsante.  
   ![Schermata nodo bus di servizio][svc_bus_node]
4. In hello **creare un nuovo Namespace servizio** finestra di dialogo immettere un **Namespace**, e quindi assicurarsi che sia univoco, toomake il **verifica disponibilità** pulsante.  
   ![Schermata Create a New Namespace][create_namespace]
5. Dopo aver verificato il nome di spazio dei nomi hello è disponibile, scegliere il paese o regione in cui deve essere ospitato lo spazio dei nomi e quindi fare clic su hello **creare Namespace** pulsante.  
   
   spazio dei nomi di Hello creato verrà visualizzato nel portale di Azure classico hello e accetta un tooactivate momento. Attendere fino a quando non è stato hello **Active** prima di procedere al passaggio successivo hello.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Ottenere hello predefinito le credenziali di gestione per lo spazio dei nomi hello
Nelle operazioni di gestione tooperform ordine, ad esempio la creazione di una coda, in hello nuovo spazio dei nomi, sono necessarie le credenziali di gestione di tooobtain hello per lo spazio dei nomi.

1. Nel riquadro di spostamento a sinistra di hello, fare clic su hello **Bus di servizio** nodo per visualizzare l'elenco di hello degli spazi dei nomi disponibili.
   ![Schermata relativa agli spazi dei nomi disponibili][avail_namespaces]
2. Selezionare lo spazio dei nomi hello che appena create dall'elenco di hello illustrato.
   ![Schermata relativa all'elenco degli spazi dei nomi][namespace_list]
3. Hello destro **proprietà** riquadro contiene proprietà hello per il nuovo spazio dei nomi.
   ![Schermata pannello Proprietà][properties_pane]
4. Hello **chiave predefinita** è nascosto. Fare clic su hello **vista** pulsante credenziali di sicurezza toodisplay hello.
   ![Schermata Default Key][default_key]
5. Prendere nota di hello **autorità di certificazione predefinita** hello e **chiave predefinita** come utilizzare queste informazioni di sotto di tooperform operazioni con lo spazio dei nomi.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Come toocreate un'applicazione Java che esegue un'attività a elevato utilizzo di calcolo
1. Nel computer di sviluppo (che non dispone di macchina virtuale di hello toobe creato), download hello [Azure SDK per Java](https://azure.microsoft.com/develop/java/).
2. Creare un'applicazione console Java mediante il codice di esempio hello alla fine di hello in questa sezione. In questa esercitazione si userà **TSPSolver.java** come nome del file hello Java. Modificare hello **il\_servizio\_bus\_dello spazio dei nomi**, **il\_servizio\_bus\_proprietario**e **il\_servizio\_bus\_chiave** toouse segnaposto del bus di servizio **dello spazio dei nomi**, **autorità di certificazione predefinita** e  **Chiave predefinita** rispettivamente i valori.
3. Dopo la generazione di codice, esportazione hello applicazione tooa eseguibile Java archive (JAR) hello pacchetto necessari e librerie in hello generato JAR. In questa esercitazione si userà **TSPSolver.jar** come nome di file JAR hello generato.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Come un'applicazione Java che esegue il monitoraggio toocreate hello lo stato di avanzamento dell'attività complesse hello
1. Nel computer di sviluppo, creare un'applicazione console Java mediante il codice di esempio hello alla fine di hello in questa sezione. In questa esercitazione si userà **TSPClient.java** come nome del file hello Java. Come illustrato in precedenza, modificare hello **il\_servizio\_bus\_dello spazio dei nomi**, **il\_servizio\_bus\_proprietario**, e **il\_servizio\_bus\_chiave** toouse segnaposto del bus di servizio **dello spazio dei nomi**, **autorità di certificazione predefinita**e **chiave predefinita** rispettivamente i valori.
2. Esportare tooa applicazione hello JAR eseguibili, hello pacchetto è necessario e librerie in hello generato JAR. In questa esercitazione si userà **TSPClient.jar** come nome di file JAR hello generato.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Come toorun hello applicazioni Java
Eseguire un'applicazione hello complesse, prima coda di hello toocreate quindi toosolve hello in viaggio Saleseman problema, che aggiungerà hello corrente migliore route toohello coda di service bus. Hello durante l'applicazione con utilizzo intensivo di calcolo è in esecuzione o in un secondo momento, risultati di esecuzione hello client toodisplay dalla coda di service bus hello.

### <a name="toorun-hello-compute-intensive-application"></a>applicazione hello complesse toorun
1. Accedere a macchina virtuale tooyour.
2. Creare una cartella in cui eseguire l'applicazione, ad esempio **c:\TSP**.
3. Copia **TSPSolver.jar** troppo**c:\TSP**,
4. Creare un file denominato **c:\TSP\cities.txt** con hello seguente contenuto.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. Al prompt dei comandi, modificare le directory tooc:\TSP.
6. Verificare che nella cartella bin di JRE hello sia nella variabile di ambiente PATH hello.
7. Coda del bus di servizio toocreate hello è necessario prima di eseguire le permutazioni Risolutore di hello problema del commesso Viaggiatore. Comando che segue di hello esecuzione coda toocreate hello service bus.
   
        java -jar TSPSolver.jar createqueue
8. Dopo aver creato hello coda, è possibile eseguire le permutazioni Risolutore di hello problema del commesso Viaggiatore. Ad esempio, eseguire hello seguendo il Risolutore di comando toorun hello per le 8 città.
   
        java -jar TSPSolver.jar 8
   
   Se non si specifica un numero, il risolutore verrà eseguito per 10 città. Come Risolutore di hello rileva route più brevi corrente, li aggiunge toohello coda.

> [!NOTE]
> Hello maggiore hello numero specificato, verrà eseguito il Risolutore di hello più hello. Ad esempio, l'esecuzione per 14 città potrebbe richiedere diversi minuti, mentre l'esecuzione per 15 città potrebbe richiedere parecchie ore. Giorni di runtime (infine settimane, mesi e anni) potrebbe causare aumentando too16 o più città. Ciò è dovuto toohello rapido aumento hello numero di permutazioni ritenuti dal Risolutore di hello hello aumentare del numero di città.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Come toorun hello monitoraggio dell'applicazione client
1. Accedere tooyour macchina in cui si eseguirà l'applicazione client hello. Non è necessario toobe hello stesso computer che esegue hello **TSPSolver** un'applicazione, sebbene possa essere.
2. Creare una cartella in cui eseguire l'applicazione, ad esempio **c:\TSP**.
3. Copia **TSPClient.jar** troppo**c:\TSP**,
4. Verificare che nella cartella bin di JRE hello sia nella variabile di ambiente PATH hello.
5. Al prompt dei comandi, modificare le directory tooc:\TSP.
6. Eseguire hello comando seguente.
   
        java -jar TSPClient.jar
   
    Facoltativamente, specificare il numero di hello di toosleep minuti tra il controllo coda hello, passando un argomento della riga di comando. Hello sospensione periodo predefinito per il controllo coda hello è 3 minuti, che viene utilizzato se nessun argomento della riga di comando è passato troppo**TSPClient**. Se si desidera toouse un valore diverso per intervallo di inattività hello, ad esempio, un minuto, eseguire hello comando seguente.
   
        java -jar TSPClient.jar 1
   
    Hello client verrà eseguito finché riceve un messaggio nella coda di "Completa". Si noti che se si eseguono più occorrenze di Risolutore di hello senza eseguire il client di hello, potrebbe essere necessario client hello toorun coda vuota hello di toocompletely più volte. In alternativa, è possibile eliminare la coda hello e quindi crearlo nuovamente. coda di hello toodelete, eseguire il seguente hello **TSPSolver** (non **TSPClient**) comando.
   
        java -jar TSPSolver.jar deletequeue
   
    Risolutore di Hello verrà eseguito fino al termine dell'analisi di tutte le route.

## <a name="how-toostop-hello-java-applications"></a>Come toostop hello applicazioni Java
Risolutore di hello e nelle applicazioni client, è possibile premere **Ctrl + C** tooexit se si desidera tooend toonormal precedente completamento.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
