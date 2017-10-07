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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Come toouse hello Java Message Service (JMS) API con il Bus di servizio e AMQP 1.0
Hello Advanced Message Queuing Protocol (AMQP) 1.0 è un protocollo di messaggistica efficiente, affidabile e a livello di rete che è possibile utilizzare toobuild affidabile tra piattaforme diverse applicazioni di messaggistica.

Supporto per AMQP 1.0 nel Bus di servizio, significa che è possibile utilizzare hello Accodamento messaggi e pubblicazione/sottoscrizione funzionalità di messaggistica negoziata da una vasta gamma di piattaforme usando un protocollo binario efficiente. Inoltre, è possibile creare applicazioni costituite da componenti creati con un insieme di linguaggi, framework e sistemi operativi.

Questo articolo spiega come toouse Bus di servizio le funzionalità di messaggistica (code e pubblicazione/sottoscrizione argomenti) da applicazioni Java tramite hello diffusi Java Message Service (JMS) API standard. È presente un [articolo complementare](service-bus-amqp-dotnet.md) che spiega come toodo hello stesso utilizzando hello API .NET del Bus di servizio. È possibile utilizzare questi toolearn contemporaneamente due guide sulle piattaforme di messaggistica tramite AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Introduzione al bus di servizio
In questa guida si presuppone di avere già uno spazio dei nomi del bus di servizio contenente una coda denominata **coda1**. Se non fosse possibile, è quindi possibile [creare lo spazio dei nomi hello e coda](service-bus-create-namespace-portal.md) utilizzando hello [portale di Azure](https://portal.azure.com). Per ulteriori informazioni su spazi dei nomi Service Bus toocreate e code, vedere [iniziare con le code del Bus di servizio](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Le code e gli argomenti partizionati supportano anche AMQP. Per altre informazioni, vedere le [entità di messaggistica partizionate](service-bus-partitioning.md) e [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Libreria client di download hello AMQP 1.0 JMS
Per informazioni su dove toodownload hello versione più recente della libreria client hello AMQP 1.0 di Apache Qpid JMS, visitare [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

È necessario aggiungere hello seguenti quattro file JAR dagli hello AMQP 1.0 di Apache Qpid JMS distribuzione archivio toohello CLASSPATH Java durante la compilazione e l'esecuzione di applicazioni JMS con il Bus di servizio:

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Compilazione di applicazioni Java
### <a name="java-naming-and-directory-interface-jndi"></a>Java Naming and Directory Interface (JNDI)
JMS Usa hello Java Naming and Directory Interface (JNDI) toocreate una separazione tra i nomi logici e fisici. Con JNDI vengono risolti due tipi di oggetti JMS: ConnectionFactory e Destination. JNDI Usa un modello di provider in cui è possibile collegare i compiti di risoluzione nome di directory diversi servizi toohandle. Hello Apache Qpid JMS AMQP 1.0 libreria dotata di una proprietà semplice Provider JNDI basato su file che viene configurato usando un file delle proprietà seguenti hello formato:

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

#### <a name="configure-hello-connectionfactory"></a>Configurare hello ConnectionFactory
Hello toodefine voce utilizzata una **ConnectionFactory** in hello Qpid provider JNDI delle proprietà del file è di hello seguente formato:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Dove **[jndi_name]** e **[ConnectionURL]** hanno hello seguenti significati:

* **[jndi_name] **: nome logico di hello di hello ConnectionFactory. Si tratta hello nome che verrà risolto in un'applicazione Java hello utilizzando il metodo JNDI Intialcontext hello.
* **[ConnectionURL] **: Un URL che fornisce informazioni di hello libreria JMS hello necessario gestore AMQP toohello.

formato Hello di hello **ConnectionURL** è indicato di seguito:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Dove **[spazio dei nomi]**, **[SASPolicyName]** e **[SASPolicyKey]** hanno hello seguenti significati:

* **[spazio dei nomi] **: hello dello spazio dei nomi Service Bus.
* **[SASPolicyName] **: nome del criterio di firma di accesso condiviso della coda di hello.
* **[SASPolicyKey] **: chiave dei criteri di firma di accesso condiviso della coda hello.

> [!NOTE]
> È necessario applicare la codifica URL password hello manualmente. Sul sito [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) è disponibile un'utilità per codificare facilmente l'URL.
> 
> 

#### <a name="configure-destinations"></a>Configurare le destinazioni
usare l'immissione di Hello toodefine che è una destinazione presente nel provider JNDI del file delle proprietà Qpid hello di hello seguente formato:

```
queue.[jndi_name] = [physical_name]
```

oppure

```
topic.[jndi_name] = [physical_name]
```

Dove **[jndi\_nome]** e **[fisico\_nome]** hanno hello seguenti significati:

* **[jndi_name] **: nome logico di hello della destinazione hello. Si tratta hello nome che verrà risolto in un'applicazione Java hello utilizzando il metodo JNDI Intialcontext hello.
* **[physical_name] **: nome hello di hello applicazione hello del Bus di servizio entità toowhich invia o riceve messaggi.

> [!NOTE]
> Quando si riceve da una sottoscrizione di argomento del Bus di servizio, il nome fisico hello specificato in JNDI deve essere il nome di hello di argomento hello. nome della sottoscrizione Hello viene fornito quando sottoscrizione durevoli hello viene creato nel codice dell'applicazione JMS hello. Hello [Guida per gli sviluppatori di Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) vengono fornite informazioni dettagliate sull'utilizzo di argomenti del Bus di servizio da JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Scrivere un'applicazione hello JMS
Non esistono API speciali oppure opzioni obbligatorie quando si utilizza JMS con il bus di servizio. Tuttavia, esistono alcune limitazioni che verranno illustrate più avanti. Come per qualsiasi applicazione JMS, hello in primo luogo necessario configurazione dell'ambiente JNDI hello, tooresolve in grado di toobe un **ConnectionFactory** e destinazioni.

#### <a name="configure-hello-jndi-initialcontext"></a>Configurare hello InitialContext JNDI
ambiente JNDI Hello è configurata per il passaggio di una tabella hash delle informazioni di configurazione al costruttore hello della classe javax.naming.InitialContext hello. due elementi obbligatori Hello nella hashtable hello sono hello nome della classe di Factory del contesto iniziale hello e hello URL del Provider. Hello codice seguente viene illustrato come tooconfigure hello JNDI ambiente toouse hello Qpid file delle proprietà del Provider JNDI basato su con un file di proprietà denominato **ServiceBus**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Semplice applicazione JMS che usa la coda del bus di servizio
Hello programma di esempio seguente invia JMS TextMessages tooa della coda del Bus di servizio con nome logico di hello JNDI della coda e riceve messaggi hello nuovamente.

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

### <a name="run-hello-application"></a>Eseguire un'applicazione hello
L'esecuzione di un'applicazione hello produce l'output del modulo hello:

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

## <a name="cross-platform-messaging-between-jms-and-net"></a>Messaggistica multipiattaforma tra JMS e .NET
Questa guida è stata illustrata come toosend e ricevere messaggi tooand dal Bus di servizio con JMS. Tuttavia, uno dei vantaggi principali di hello del protocollo AMQP 1.0 è che consente applicazioni toobe compilata da componenti scritti in linguaggi diversi, con i messaggi scambiati in modo affidabile e alla massima fedeltà.

Utilizzo di un'applicazione hello esempio JMS descritto in precedenza e un'applicazione .NET simile eseguita da un altro articolo, [tramite il Bus di servizio da .NET con AMQP 1.0](service-bus-amqp-dotnet.md), è possibile scambiare messaggi tra .NET e Java. Leggere questo articolo per ulteriori informazioni sui dettagli hello di tramite AMQP 1.0 e Bus di servizio di messaggistica multipiattaforma.

### <a name="jms-toonet"></a>Too.NET JMS
toodemonstrate JMS too.NET messaggistica:

* Avviare l'applicazione di esempio .NET hello senza argomenti della riga di comando.
* Avviare l'applicazione di esempio Java hello con argomento della riga di comando di hello "sendonly". In questa modalità, hello applicazione non riceve i messaggi dalla coda di hello, questo invierà.
* Premere **invio** più volte nella console di applicazioni Java hello, causando toobe i messaggi inviati.
* Questi messaggi vengono ricevuti dal hello applicazione .NET.

#### <a name="output-from-jms-application"></a>Output dell'applicazione JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Output dell'applicazione .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>TooJMS .NET
toodemonstrate tooJMS di .NET di messaggistica:

* Avviare l'applicazione di esempio .NET hello con argomento della riga di comando di hello "sendonly". In questa modalità, hello applicazione non riceve i messaggi dalla coda di hello, questo invierà.
* Avviare l'applicazione di esempio Java hello senza argomenti della riga di comando.
* Premere **invio** più volte nella console di application hello .NET, causando toobe i messaggi inviati.
* Questi messaggi vengono ricevuti dal hello applicazione Java.

#### <a name="output-from-net-application"></a>Output dell'applicazione .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Output dell'applicazione JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Funzionalità non supportate e restrizioni
Hello seguenti restrizioni esiste quando si usa JMS tramite AMQP 1.0 con il Bus di servizio, vale a dire:

* È consentito solo un oggetto **MessageProducer** o **MessageConsumer** per **sessione**. Se è necessario toocreate più **MessageProducers** o **MessageConsumers** in un'applicazione, creare una dedicata **sessione** per ognuno di essi.
* Le sottoscrizioni a un argomento volatile non sono attualmente supportate.
* Gli oggetti**MessageSelectors** non sono attualmente supportati.
* Destinazioni temporanee; ad esempio, **TemporaryQueue**, **TemporaryTopic** non sono attualmente supportati, insieme a hello **QueueRequestor** e **TopicRequestor**API che li utilizzano.
* Le sessioni transazionali non sono supportate e le transazioni distribuite non sono supportate.

## <a name="summary"></a>Riepilogo
Questa procedura-tooguide è stato illustrato come toouse negoziata di Service Bus le funzionalità di messaggistica (code e pubblicazione/sottoscrizione argomenti) da Java tramite hello API JMS più diffusi e AMQP 1.0.

È anche possibile utilizzare AMQP 1.0 per il bus di servizio da altri linguaggi, tra cui .NET, C, Python e PHP. I componenti compilati con questi linguaggi diversi possono scambiare messaggi in modo affidabile e alla massima fedeltà utilizzando il supporto di hello AMQP 1.0 nel Bus di servizio.

## <a name="next-steps"></a>Passaggi successivi
* [Supporto per il protocollo AMQP 1.0 nel bus di servizio di Azure](service-bus-amqp-overview.md)
* [Come toouse AMQP 1.0 con hello API .NET del Bus di servizio](service-bus-dotnet-advanced-message-queuing.md)
* [Guida per sviluppatori di AMQP 1.0 per il bus di servizio](service-bus-amqp-dotnet.md)
* [Introduzione alle code del bus di servizio](service-bus-dotnet-get-started-with-queues.md)
* [Java Developer Center](https://azure.microsoft.com/develop/java/)

