---
title: Come usare AMQP 1.0 con l'API del bus di servizio Java | Microsoft Docs
description: Come usare JMS (Java Message Service ) con il bus di servizio di Azure e il protocollo AMQP (Advanced Message Queuing Protocol) 1.0.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="6a302-103">Come usare l'API JMS (Java Message Service) con il bus di servizio e AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="6a302-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="6a302-104">AMQP (Advanced Message Queuing Protocol) 1.0 è un protocollo di messaggistica wire-level efficiente e affidabile che può essere utilizzato per creare potenti applicazioni di messaggistica multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="6a302-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="6a302-105">Grazie al supporto per AMQP 1.0 nel bus di servizio, è ora possibile utilizzare le funzionalità di accodamento e di messaggistica negoziata di pubblicazione/sottoscrizione da numerose piattaforme, tramite un efficiente protocollo binario.</span><span class="sxs-lookup"><span data-stu-id="6a302-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="6a302-106">Inoltre, è possibile creare applicazioni costituite da componenti creati con un insieme di linguaggi, framework e sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="6a302-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="6a302-107">Questo articolo illustra come usare le funzionalità di messaggistica del bus di servizio, ad esempio code e pubblicazione/sottoscrizione di argomenti, da applicazioni Java usando l'API standard JMS più richiesta (Java Message Service).</span><span class="sxs-lookup"><span data-stu-id="6a302-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="6a302-108">È disponibile un [articolo complementare](service-bus-amqp-dotnet.md) che illustra come eseguire le stesse procedure usando l'API . NET del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6a302-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="6a302-109">È possibile consultare queste due guide per acquisire informazioni sulla messaggistica multipiattaforma con AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="6a302-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="6a302-110">Introduzione al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6a302-110">Get started with Service Bus</span></span>
<span data-ttu-id="6a302-111">In questa guida si presuppone di avere già uno spazio dei nomi del bus di servizio contenente una coda denominata **coda1**.</span><span class="sxs-lookup"><span data-stu-id="6a302-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="6a302-112">In caso contrario, è necessario [creare lo spazio dei nomi e la coda](service-bus-create-namespace-portal.md) tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a302-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6a302-113">Per altre informazioni su come creare spazi dei nomi e code del bus di servizio, vedere [Introduzione alle code del bus di servizio](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="6a302-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6a302-114">Le code e gli argomenti partizionati supportano anche AMQP.</span><span class="sxs-lookup"><span data-stu-id="6a302-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="6a302-115">Per altre informazioni, vedere le [entità di messaggistica partizionate](service-bus-partitioning.md) e [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a302-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="6a302-116">Download della libreria client JMS basata su AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="6a302-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="6a302-117">Per informazioni su dove scaricare l'ultima versione della libreria client JMS basata su AMQP 1.0 di Apache Qpid, visitare la pagina [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="6a302-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="6a302-118">È necessario aggiungere i seguenti quattro file JAR dall'archivio di distribuzione AMQP 1.0 di Apache Qpid al CLASSPATH Java durante la compilazione e l'esecuzione di applicazioni JMS con il bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="6a302-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="6a302-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="6a302-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="6a302-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="6a302-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="6a302-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="6a302-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="6a302-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="6a302-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="6a302-123">Compilazione di applicazioni Java</span><span class="sxs-lookup"><span data-stu-id="6a302-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="6a302-124">Java Naming and Directory Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="6a302-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="6a302-125">JMS usa l'interfaccia JNDI (Java Naming and Directory Interface) per creare una separazione tra i nomi logici e i nomi fisici.</span><span class="sxs-lookup"><span data-stu-id="6a302-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="6a302-126">Con JNDI vengono risolti due tipi di oggetti JMS: ConnectionFactory e Destination.</span><span class="sxs-lookup"><span data-stu-id="6a302-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="6a302-127">JNDI utilizza un modello di provider in cui è possibile inserire diversi servizi directory per gestire le attività di risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6a302-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="6a302-128">La libreria JMS basata su AMQP 1.0 di Apache Qpid viene fornita con un semplice provider JNDI, basato su un file delle proprietà, che viene configurato mediante un file di testo:</span><span class="sxs-lookup"><span data-stu-id="6a302-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="6a302-129">Configurare ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="6a302-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="6a302-130">La voce usata per definire un oggetto **ConnectionFactory** nel provider JNDI basato sul file delle proprietà Qpid è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="6a302-131">Dove **[jndi_name]** e **[ConnectionURL]** hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a302-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="6a302-132">**[jndi_name]**: nome logico dell'oggetto ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="6a302-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="6a302-133">Tale nome viene risolto nell'applicazione Java mediante l'utilizzo del metodo JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="6a302-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="6a302-134">**[ConnectionURL]**: URL che comunica alla libreria JMS le informazioni necessarie per il broker AMQP.</span><span class="sxs-lookup"><span data-stu-id="6a302-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="6a302-135">Il formato di **ConnectionURL** è il seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="6a302-136">Dove **[namespace]**, **[SASPolicyName]** e **[SASPolicyKey]** hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a302-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="6a302-137">**[namespace]**: spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6a302-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="6a302-138">**[SASPolicyName]**: nome del criterio della firma di accesso condiviso relativa alla coda.</span><span class="sxs-lookup"><span data-stu-id="6a302-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="6a302-139">**[SASPolicyKey]**: chiave del criterio della firma di accesso condiviso relativa alla coda.</span><span class="sxs-lookup"><span data-stu-id="6a302-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="6a302-140">è necessario applicare manualmente la codifica URL alla password.</span><span class="sxs-lookup"><span data-stu-id="6a302-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="6a302-141">Sul sito [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) è disponibile un'utilità per codificare facilmente l'URL.</span><span class="sxs-lookup"><span data-stu-id="6a302-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="6a302-142">Configurare le destinazioni</span><span class="sxs-lookup"><span data-stu-id="6a302-142">Configure destinations</span></span>
<span data-ttu-id="6a302-143">La voce usata per definire una destinazione nel provider JNDI basato sul file delle proprietà Qpid è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="6a302-144">oppure</span><span class="sxs-lookup"><span data-stu-id="6a302-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="6a302-145">Dove **[jndi\_name]** e **[physical\_name]** hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a302-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="6a302-146">**[jndi_name]**: nome logico della destinazione.</span><span class="sxs-lookup"><span data-stu-id="6a302-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="6a302-147">Tale nome viene risolto nell'applicazione Java mediante l'utilizzo del metodo JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="6a302-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="6a302-148">**[physical_name]**: nome dell'entità del bus di servizio a cui l'applicazione invia messaggi o da cui l'applicazione riceve messaggi.</span><span class="sxs-lookup"><span data-stu-id="6a302-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="6a302-149">In caso di ricezione da una sottoscrizione a un argomento del bus di servizio, il nome fisico specificato in JNDI deve essere il nome dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="6a302-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="6a302-150">Il nome della sottoscrizione viene fornito al momento della creazione della sottoscrizione durevole nel codice dell'applicazione JMS.</span><span class="sxs-lookup"><span data-stu-id="6a302-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="6a302-151">La [guida per sviluppatori di AMQP 1.0 per il bus di servizio](service-bus-amqp-dotnet.md) include istruzioni dettagliate sull'uso di argomenti del bus di servizio di JMS.</span><span class="sxs-lookup"><span data-stu-id="6a302-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="6a302-152">Scrivere l'applicazione JMS</span><span class="sxs-lookup"><span data-stu-id="6a302-152">Write the JMS application</span></span>
<span data-ttu-id="6a302-153">Non esistono API speciali oppure opzioni obbligatorie quando si utilizza JMS con il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6a302-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="6a302-154">Tuttavia, esistono alcune limitazioni che verranno illustrate più avanti.</span><span class="sxs-lookup"><span data-stu-id="6a302-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="6a302-155">Come per qualsiasi applicazione JMS, la prima operazione da eseguire è la configurazione dell'ambiente JNDI, in modo da poter risolvere gli oggetti di tipo **ConnectionFactory** e le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="6a302-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="6a302-156">Configurare il contesto JNDI iniziale</span><span class="sxs-lookup"><span data-stu-id="6a302-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="6a302-157">La configurazione dell'ambiente JNDI viene eseguita passando una tabella hash di informazioni di configurazione al costruttore della classe javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="6a302-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="6a302-158">I due elementi necessari nella tabella hash sono il nome della classe della factory del contesto iniziale e l'URL del provider.</span><span class="sxs-lookup"><span data-stu-id="6a302-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="6a302-159">Nel codice seguente viene illustrato come configurare l'ambiente JNDI per usare il provider JNDI basato sul file delle proprietà Qpid con un file delle proprietà denominato **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="6a302-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="6a302-160">Semplice applicazione JMS che usa la coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6a302-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="6a302-161">L'applicazione di esempio seguente consente di inviare e ricevere messaggi di testo JMS verso e da una coda del bus di servizio con il nome JNDI logico QUEUE.</span><span class="sxs-lookup"><span data-stu-id="6a302-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-the-application"></a><span data-ttu-id="6a302-162">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="6a302-162">Run the application</span></span>
<span data-ttu-id="6a302-163">L'esecuzione dell'applicazione produce un output nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="6a302-164">Messaggistica multipiattaforma tra JMS e .NET</span><span class="sxs-lookup"><span data-stu-id="6a302-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="6a302-165">In questa guida è stato illustrato come inviare e ricevere messaggi verso e dal bus di servizio utilizzando JMS.</span><span class="sxs-lookup"><span data-stu-id="6a302-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="6a302-166">Tuttavia, uno dei principali vantaggi di AMQP 1.0 è che consente di creare applicazioni da componenti scritti in linguaggi diversi, con i messaggi scambiati in modo affidabile e con la massima fedeltà.</span><span class="sxs-lookup"><span data-stu-id="6a302-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="6a302-167">Con l'uso dell'applicazione JMS di esempio descritta in precedenza e un'applicazione .NET simile presa dall'articolo complementare [Come usare AMQP 1.0 con l'API .NET del bus di servizio](service-bus-amqp-dotnet.md), è possibile scambiare messaggi tra .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="6a302-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="6a302-168">Leggere questo articolo per altre informazioni sulla messaggistica multipiattaforma che usa il bus di servizio e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="6a302-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="6a302-169">Da JMS a .NET</span><span class="sxs-lookup"><span data-stu-id="6a302-169">JMS to .NET</span></span>
<span data-ttu-id="6a302-170">Per verificare la messaggistica da JMS a .NET, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="6a302-171">Avviare l'applicazione di esempio .NET senza argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6a302-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="6a302-172">Avviare l'applicazione di esempio Java con l'argomento della riga di comando "sendonly".</span><span class="sxs-lookup"><span data-stu-id="6a302-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="6a302-173">In questa modalità l'applicazione non riceverà messaggi dalla coda, ma potrà solo inviarne.</span><span class="sxs-lookup"><span data-stu-id="6a302-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="6a302-174">Premere alcune volte **INVIO** nella console dell'applicazione Java per inviare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="6a302-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="6a302-175">Questi messaggi vengono ricevuti dall'applicazione .NET.</span><span class="sxs-lookup"><span data-stu-id="6a302-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="6a302-176">Output dell'applicazione JMS</span><span class="sxs-lookup"><span data-stu-id="6a302-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="6a302-177">Output dell'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="6a302-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="6a302-178">Da .NET a JMS</span><span class="sxs-lookup"><span data-stu-id="6a302-178">.NET to JMS</span></span>
<span data-ttu-id="6a302-179">Per verificare la messaggistica da .NET a JMS, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a302-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="6a302-180">Avviare l'applicazione di esempio .NET con l'argomento "sendonly" della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6a302-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="6a302-181">In questa modalità l'applicazione non riceverà messaggi dalla coda, ma potrà solo inviarne.</span><span class="sxs-lookup"><span data-stu-id="6a302-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="6a302-182">Avviare l'applicazione di esempio Java senza argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6a302-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="6a302-183">Premere alcune volte **INVIO** nella console dell'applicazione .NET per inviare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="6a302-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="6a302-184">Questi messaggi vengono ricevuti dall'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="6a302-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="6a302-185">Output dell'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="6a302-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="6a302-186">Output dell'applicazione JMS</span><span class="sxs-lookup"><span data-stu-id="6a302-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="6a302-187">Funzionalità non supportate e restrizioni</span><span class="sxs-lookup"><span data-stu-id="6a302-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="6a302-188">Quando si utilizza JMS su AMQP 1.0 con il bus di servizio esistono le seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="6a302-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="6a302-189">È consentito solo un oggetto **MessageProducer** o **MessageConsumer** per **sessione**.</span><span class="sxs-lookup"><span data-stu-id="6a302-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="6a302-190">Se si vuole creare più oggetti **MessageProducers** o **MessageConsumers** in un'applicazione, creare una **sessione** dedicata per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="6a302-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="6a302-191">Le sottoscrizioni a un argomento volatile non sono attualmente supportate.</span><span class="sxs-lookup"><span data-stu-id="6a302-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="6a302-192">Gli oggetti**MessageSelectors** non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="6a302-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="6a302-193">Le destinazioni temporanee, ad esempio **TemporaryQueue** e **TemporaryTopic**, non sono attualmente supportate, così come le API **QueueRequestor** e **TopicRequestor** da cui vengono usate.</span><span class="sxs-lookup"><span data-stu-id="6a302-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="6a302-194">Le sessioni transazionali non sono supportate e le transazioni distribuite non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="6a302-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="6a302-195">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6a302-195">Summary</span></span>
<span data-ttu-id="6a302-196">Questa guida dettagliata ha illustrato come accedere alle funzionalità di messaggistica negoziata (code e pubblicazione/sottoscrizione di argomenti) del bus di servizio da Java usando la diffusa API JMS e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="6a302-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="6a302-197">È anche possibile utilizzare AMQP 1.0 per il bus di servizio da altri linguaggi, tra cui .NET, C, Python e PHP.</span><span class="sxs-lookup"><span data-stu-id="6a302-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="6a302-198">I componenti creati con questi linguaggi possono scambiare messaggi in modo affidabile e con la massima fedeltà grazie al supporto per AMQP 1.0 nel bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6a302-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a302-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a302-199">Next steps</span></span>
* [<span data-ttu-id="6a302-200">Supporto per il protocollo AMQP 1.0 nel bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="6a302-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="6a302-201">Come usare AMQP 1.0 con l'API .NET del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6a302-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="6a302-202">Guida per sviluppatori di AMQP 1.0 per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6a302-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="6a302-203">Introduzione alle code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6a302-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="6a302-204">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="6a302-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

