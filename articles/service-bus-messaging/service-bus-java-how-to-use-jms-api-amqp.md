---
title: aaaHow toouse AMQP 1.0 con hello API del Bus di servizio Java | Documenti Microsoft
description: Come toouse hello Java Message Service (JMS) con Service Bus di Azure e Advanced Message Queuing Protodol (AMQP) 1.0.
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
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="13645-103">Come toouse hello Java Message Service (JMS) API con il Bus di servizio e AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="13645-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="13645-104">Hello Advanced Message Queuing Protocol (AMQP) 1.0 è un protocollo di messaggistica efficiente, affidabile e a livello di rete che è possibile utilizzare toobuild affidabile tra piattaforme diverse applicazioni di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="13645-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="13645-105">Supporto per AMQP 1.0 nel Bus di servizio, significa che è possibile utilizzare hello Accodamento messaggi e pubblicazione/sottoscrizione funzionalità di messaggistica negoziata da una vasta gamma di piattaforme usando un protocollo binario efficiente.</span><span class="sxs-lookup"><span data-stu-id="13645-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="13645-106">Inoltre, è possibile creare applicazioni costituite da componenti creati con un insieme di linguaggi, framework e sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="13645-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="13645-107">Questo articolo spiega come toouse Bus di servizio le funzionalità di messaggistica (code e pubblicazione/sottoscrizione argomenti) da applicazioni Java tramite hello diffusi Java Message Service (JMS) API standard.</span><span class="sxs-lookup"><span data-stu-id="13645-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="13645-108">È presente un [articolo complementare](service-bus-amqp-dotnet.md) che spiega come toodo hello stesso utilizzando hello API .NET del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="13645-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="13645-109">È possibile utilizzare questi toolearn contemporaneamente due guide sulle piattaforme di messaggistica tramite AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="13645-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="13645-110">Introduzione al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="13645-110">Get started with Service Bus</span></span>
<span data-ttu-id="13645-111">In questa guida si presuppone di avere già uno spazio dei nomi del bus di servizio contenente una coda denominata **coda1**.</span><span class="sxs-lookup"><span data-stu-id="13645-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="13645-112">Se non fosse possibile, è quindi possibile [creare lo spazio dei nomi hello e coda](service-bus-create-namespace-portal.md) utilizzando hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13645-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="13645-113">Per ulteriori informazioni su spazi dei nomi Service Bus toocreate e code, vedere [iniziare con le code del Bus di servizio](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="13645-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="13645-114">Le code e gli argomenti partizionati supportano anche AMQP.</span><span class="sxs-lookup"><span data-stu-id="13645-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="13645-115">Per altre informazioni, vedere le [entità di messaggistica partizionate](service-bus-partitioning.md) e [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13645-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="13645-116">Libreria client di download hello AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="13645-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="13645-117">Per informazioni su dove toodownload hello versione più recente della libreria client hello AMQP 1.0 di Apache Qpid JMS, visitare [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="13645-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="13645-118">È necessario aggiungere hello seguenti quattro file JAR dagli hello AMQP 1.0 di Apache Qpid JMS distribuzione archivio toohello CLASSPATH Java durante la compilazione e l'esecuzione di applicazioni JMS con il Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="13645-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="13645-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="13645-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="13645-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="13645-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="13645-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="13645-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="13645-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="13645-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="13645-123">Compilazione di applicazioni Java</span><span class="sxs-lookup"><span data-stu-id="13645-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="13645-124">Java Naming and Directory Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="13645-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="13645-125">JMS Usa hello Java Naming and Directory Interface (JNDI) toocreate una separazione tra i nomi logici e fisici.</span><span class="sxs-lookup"><span data-stu-id="13645-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="13645-126">Con JNDI vengono risolti due tipi di oggetti JMS: ConnectionFactory e Destination.</span><span class="sxs-lookup"><span data-stu-id="13645-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="13645-127">JNDI Usa un modello di provider in cui è possibile collegare i compiti di risoluzione nome di directory diversi servizi toohandle.</span><span class="sxs-lookup"><span data-stu-id="13645-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="13645-128">Hello Apache Qpid JMS AMQP 1.0 libreria dotata di una proprietà semplice Provider JNDI basato su file che viene configurato usando un file delle proprietà seguenti hello formato:</span><span class="sxs-lookup"><span data-stu-id="13645-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="13645-129">Configurare hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="13645-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="13645-130">Hello toodefine voce utilizzata una **ConnectionFactory** in hello Qpid provider JNDI delle proprietà del file è di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="13645-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="13645-131">Dove **[jndi_name]** e **[ConnectionURL]** hanno hello seguenti significati:</span><span class="sxs-lookup"><span data-stu-id="13645-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="13645-132">**[jndi_name] **: nome logico di hello di hello ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="13645-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="13645-133">Si tratta hello nome che verrà risolto in un'applicazione Java hello utilizzando il metodo JNDI Intialcontext hello.</span><span class="sxs-lookup"><span data-stu-id="13645-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="13645-134">**[ConnectionURL] **: Un URL che fornisce informazioni di hello libreria JMS hello necessario gestore AMQP toohello.</span><span class="sxs-lookup"><span data-stu-id="13645-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="13645-135">formato Hello di hello **ConnectionURL** è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13645-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="13645-136">Dove **[spazio dei nomi]**, **[SASPolicyName]** e **[SASPolicyKey]** hanno hello seguenti significati:</span><span class="sxs-lookup"><span data-stu-id="13645-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="13645-137">**[spazio dei nomi] **: hello dello spazio dei nomi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="13645-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="13645-138">**[SASPolicyName] **: nome del criterio di firma di accesso condiviso della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="13645-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="13645-139">**[SASPolicyKey] **: chiave dei criteri di firma di accesso condiviso della coda hello.</span><span class="sxs-lookup"><span data-stu-id="13645-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="13645-140">È necessario applicare la codifica URL password hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="13645-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="13645-141">Sul sito [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) è disponibile un'utilità per codificare facilmente l'URL.</span><span class="sxs-lookup"><span data-stu-id="13645-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="13645-142">Configurare le destinazioni</span><span class="sxs-lookup"><span data-stu-id="13645-142">Configure destinations</span></span>
<span data-ttu-id="13645-143">usare l'immissione di Hello toodefine che è una destinazione presente nel provider JNDI del file delle proprietà Qpid hello di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="13645-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="13645-144">oppure</span><span class="sxs-lookup"><span data-stu-id="13645-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="13645-145">Dove **[jndi\_nome]** e **[fisico\_nome]** hanno hello seguenti significati:</span><span class="sxs-lookup"><span data-stu-id="13645-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="13645-146">**[jndi_name] **: nome logico di hello della destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="13645-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="13645-147">Si tratta hello nome che verrà risolto in un'applicazione Java hello utilizzando il metodo JNDI Intialcontext hello.</span><span class="sxs-lookup"><span data-stu-id="13645-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="13645-148">**[physical_name] **: nome hello di hello applicazione hello del Bus di servizio entità toowhich invia o riceve messaggi.</span><span class="sxs-lookup"><span data-stu-id="13645-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="13645-149">Quando si riceve da una sottoscrizione di argomento del Bus di servizio, il nome fisico hello specificato in JNDI deve essere il nome di hello di argomento hello.</span><span class="sxs-lookup"><span data-stu-id="13645-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="13645-150">nome della sottoscrizione Hello viene fornito quando sottoscrizione durevoli hello viene creato nel codice dell'applicazione JMS hello.</span><span class="sxs-lookup"><span data-stu-id="13645-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="13645-151">Hello [Guida per gli sviluppatori di Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) vengono fornite informazioni dettagliate sull'utilizzo di argomenti del Bus di servizio da JMS.</span><span class="sxs-lookup"><span data-stu-id="13645-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="13645-152">Scrivere un'applicazione hello JMS</span><span class="sxs-lookup"><span data-stu-id="13645-152">Write hello JMS application</span></span>
<span data-ttu-id="13645-153">Non esistono API speciali oppure opzioni obbligatorie quando si utilizza JMS con il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="13645-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="13645-154">Tuttavia, esistono alcune limitazioni che verranno illustrate più avanti.</span><span class="sxs-lookup"><span data-stu-id="13645-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="13645-155">Come per qualsiasi applicazione JMS, hello in primo luogo necessario configurazione dell'ambiente JNDI hello, tooresolve in grado di toobe un **ConnectionFactory** e destinazioni.</span><span class="sxs-lookup"><span data-stu-id="13645-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="13645-156">Configurare hello InitialContext JNDI</span><span class="sxs-lookup"><span data-stu-id="13645-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="13645-157">ambiente JNDI Hello è configurata per il passaggio di una tabella hash delle informazioni di configurazione al costruttore hello della classe javax.naming.InitialContext hello.</span><span class="sxs-lookup"><span data-stu-id="13645-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="13645-158">due elementi obbligatori Hello nella hashtable hello sono hello nome della classe di Factory del contesto iniziale hello e hello URL del Provider.</span><span class="sxs-lookup"><span data-stu-id="13645-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="13645-159">Hello codice seguente viene illustrato come tooconfigure hello JNDI ambiente toouse hello Qpid file delle proprietà del Provider JNDI basato su con un file di proprietà denominato **ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="13645-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="13645-160">Semplice applicazione JMS che usa la coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="13645-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="13645-161">Hello programma di esempio seguente invia JMS TextMessages tooa della coda del Bus di servizio con nome logico di hello JNDI della coda e riceve messaggi hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="13645-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
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

### <a name="run-hello-application"></a><span data-ttu-id="13645-162">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="13645-162">Run hello application</span></span>
<span data-ttu-id="13645-163">L'esecuzione di un'applicazione hello produce l'output del modulo hello:</span><span class="sxs-lookup"><span data-stu-id="13645-163">Running hello application produces output of hello form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="13645-164">Messaggistica multipiattaforma tra JMS e .NET</span><span class="sxs-lookup"><span data-stu-id="13645-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="13645-165">Questa guida è stata illustrata come toosend e ricevere messaggi tooand dal Bus di servizio con JMS.</span><span class="sxs-lookup"><span data-stu-id="13645-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="13645-166">Tuttavia, uno dei vantaggi principali di hello del protocollo AMQP 1.0 è che consente applicazioni toobe compilata da componenti scritti in linguaggi diversi, con i messaggi scambiati in modo affidabile e alla massima fedeltà.</span><span class="sxs-lookup"><span data-stu-id="13645-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="13645-167">Utilizzo di un'applicazione hello esempio JMS descritto in precedenza e un'applicazione .NET simile eseguita da un altro articolo, [tramite il Bus di servizio da .NET con AMQP 1.0](service-bus-amqp-dotnet.md), è possibile scambiare messaggi tra .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="13645-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="13645-168">Leggere questo articolo per ulteriori informazioni sui dettagli hello di tramite AMQP 1.0 e Bus di servizio di messaggistica multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="13645-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="13645-169">Too.NET JMS</span><span class="sxs-lookup"><span data-stu-id="13645-169">JMS too.NET</span></span>
<span data-ttu-id="13645-170">toodemonstrate JMS too.NET messaggistica:</span><span class="sxs-lookup"><span data-stu-id="13645-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="13645-171">Avviare l'applicazione di esempio .NET hello senza argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="13645-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="13645-172">Avviare l'applicazione di esempio Java hello con argomento della riga di comando di hello "sendonly".</span><span class="sxs-lookup"><span data-stu-id="13645-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="13645-173">In questa modalità, hello applicazione non riceve i messaggi dalla coda di hello, questo invierà.</span><span class="sxs-lookup"><span data-stu-id="13645-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="13645-174">Premere **invio** più volte nella console di applicazioni Java hello, causando toobe i messaggi inviati.</span><span class="sxs-lookup"><span data-stu-id="13645-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="13645-175">Questi messaggi vengono ricevuti dal hello applicazione .NET.</span><span class="sxs-lookup"><span data-stu-id="13645-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="13645-176">Output dell'applicazione JMS</span><span class="sxs-lookup"><span data-stu-id="13645-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="13645-177">Output dell'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="13645-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="13645-178">TooJMS .NET</span><span class="sxs-lookup"><span data-stu-id="13645-178">.NET tooJMS</span></span>
<span data-ttu-id="13645-179">toodemonstrate tooJMS di .NET di messaggistica:</span><span class="sxs-lookup"><span data-stu-id="13645-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="13645-180">Avviare l'applicazione di esempio .NET hello con argomento della riga di comando di hello "sendonly".</span><span class="sxs-lookup"><span data-stu-id="13645-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="13645-181">In questa modalità, hello applicazione non riceve i messaggi dalla coda di hello, questo invierà.</span><span class="sxs-lookup"><span data-stu-id="13645-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="13645-182">Avviare l'applicazione di esempio Java hello senza argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="13645-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="13645-183">Premere **invio** più volte nella console di application hello .NET, causando toobe i messaggi inviati.</span><span class="sxs-lookup"><span data-stu-id="13645-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="13645-184">Questi messaggi vengono ricevuti dal hello applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="13645-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="13645-185">Output dell'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="13645-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="13645-186">Output dell'applicazione JMS</span><span class="sxs-lookup"><span data-stu-id="13645-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="13645-187">Funzionalità non supportate e restrizioni</span><span class="sxs-lookup"><span data-stu-id="13645-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="13645-188">Hello seguenti restrizioni esiste quando si usa JMS tramite AMQP 1.0 con il Bus di servizio, vale a dire:</span><span class="sxs-lookup"><span data-stu-id="13645-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="13645-189">È consentito solo un oggetto **MessageProducer** o **MessageConsumer** per **sessione**.</span><span class="sxs-lookup"><span data-stu-id="13645-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="13645-190">Se è necessario toocreate più **MessageProducers** o **MessageConsumers** in un'applicazione, creare una dedicata **sessione** per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="13645-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="13645-191">Le sottoscrizioni a un argomento volatile non sono attualmente supportate.</span><span class="sxs-lookup"><span data-stu-id="13645-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="13645-192">Gli oggetti**MessageSelectors** non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="13645-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="13645-193">Destinazioni temporanee; ad esempio, **TemporaryQueue**, **TemporaryTopic** non sono attualmente supportati, insieme a hello **QueueRequestor** e **TopicRequestor**API che li utilizzano.</span><span class="sxs-lookup"><span data-stu-id="13645-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="13645-194">Le sessioni transazionali non sono supportate e le transazioni distribuite non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="13645-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="13645-195">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="13645-195">Summary</span></span>
<span data-ttu-id="13645-196">Questa procedura-tooguide è stato illustrato come toouse negoziata di Service Bus le funzionalità di messaggistica (code e pubblicazione/sottoscrizione argomenti) da Java tramite hello API JMS più diffusi e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="13645-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="13645-197">È anche possibile utilizzare AMQP 1.0 per il bus di servizio da altri linguaggi, tra cui .NET, C, Python e PHP.</span><span class="sxs-lookup"><span data-stu-id="13645-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="13645-198">I componenti compilati con questi linguaggi diversi possono scambiare messaggi in modo affidabile e alla massima fedeltà utilizzando il supporto di hello AMQP 1.0 nel Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="13645-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13645-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13645-199">Next steps</span></span>
* [<span data-ttu-id="13645-200">Supporto per il protocollo AMQP 1.0 nel bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="13645-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="13645-201">Come toouse AMQP 1.0 con hello API .NET del Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="13645-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="13645-202">Guida per sviluppatori di AMQP 1.0 per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="13645-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="13645-203">Introduzione alle code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="13645-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="13645-204">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="13645-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

