---
title: aaaMigrate dal SDK per Java tooMaven - aggiornamento precedente applicazioni Java di Azure Service Fabric toouse Maven | Documenti Microsoft
description: Aggiornamento hello precedenti applicazioni Java utilizzato hello toouse Service Fabric Java SDK, le dipendenze di Service Fabric Java toofetch Maven. Dopo aver completato il programma di installazione, le applicazioni Java precedenti sarebbe in grado di toobuild.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Aggiornare le precedenti raccolte Java toofetch di applicazioni Java Service Fabric da Maven
Di recente, è stata spostata file binari del servizio Fabric Java da hello Service Fabric Java SDK tooMaven hosting. È ora possibile usare **mavencentral** dipendenze di Service Fabric Java toofetch hello più recente. Questa Guida introduttiva si consente di aggiornare le applicazioni Java esistenti, che è stato creato in precedenza toobe utilizzato con Service Fabric Java SDK, utilizzando entrambi Yeoman modello o toobe compatibile con hello compilazione Maven basati su Eclipse.

## <a name="prerequisites"></a>Prerequisiti
1. È necessario innanzitutto toouninstall hello SDK per Java esistente.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Il seguente servizio infrastruttura CLI più recente di installazione hello hello i passaggi indicati [qui](service-fabric-cli.md).

3. toobuild e attività per le applicazioni Java di infrastruttura servizio hello, è necessario tooensure che si disponga di JDK 1.8 e Gradle installato. Se non è ancora installato, è possibile eseguire hello seguenti tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Gli script di installazione o disinstallazione di aggiornamento hello di toouse l'applicazione hello nuovo CLI di infrastruttura servizio seguendo i passaggi di hello indicati [qui](service-fabric-application-lifecycle-sfctl.md). È possibile fare riferimento tooour Introduzione [esempi](https://github.com/Azure-Samples/service-fabric-java-getting-started) per riferimento.

>[!TIP]
> Dopo la disinstallazione di Service Fabric Java SDK hello Yeoman non funzionerà. Seguire i prerequisiti di hello indicati [qui](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman dell'infrastruttura del servizio Java generatore modello backup e l'utilizzo.

## <a name="service-fabric-java-libraries-on-maven"></a>Librerie Java di Service Fabric in Maven
Le librerie Java di Service Fabric sono ospitate in Maven. È possibile aggiungere le dipendenze di hello in hello ``pom.xml`` o ``build.gradle`` di raccolte di Service Fabric Java toouse di progetti da **mavenCentral**.

### <a name="actors"></a>Actor

Supporto di Service Fabric Reliable Actors per l'applicazione.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Services

Supporto di servizi senza stato di Service Fabric per l'applicazione.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Altro
#### <a name="transport"></a>Trasporto

Supporto del livello trasporto per l'applicazione Java di Service Fabric. Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio, a meno che la programmazione a livello di trasporto hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Supporto di Fabric

Supporto di livello di sistema per l'infrastruttura del servizio, che comunica toonative runtime di Service Fabric. Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio. Si ottiene recuperato automaticamente da Maven, quando si includono hello altre dipendenze precedente.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a>Migrazione di un servizio senza stato di Service Fabric

il servizio service Fabric esistente senza stato Java utilizzando le dipendenze di Service Fabric recuperate dal Maven, è necessario tooupdate hello la toobuild in grado di toobe ``build.gradle`` file all'interno di hello del servizio. In precedenza e utilizzato toobe come le seguenti:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
In generale, tooget un'idea generale sulla modalità di generazione script hello avrà un aspetto analogo per un servizio di linguaggio senza informazioni sullo stato dell'infrastruttura di servizio, è possibile fare riferimento a esempio tooany da esempi introduttivi. Ecco hello [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) per esempio EchoServer hello.

## <a name="migrating-service-fabric-actor-service"></a>Migrazione di un servizio Service Fabric Actors

toobuild in grado di toobe applicazione Java Actor di Service Fabric esistente utilizzando le dipendenze di Service Fabric recuperate dal Maven, è necessario hello tooupdate ``build.gradle`` file all'interno del pacchetto di interfaccia hello e nel pacchetto di servizio hello. Se si dispone di un pacchetto TestClient, è necessario che anche tooupdate. In questo caso, per l'attore ``Myactor``, seguente hello sarebbe posizioni hello in cui è necessario tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>L'aggiornamento di script di compilazione per il progetto di interfaccia hello

In precedenza e utilizzato toobe come le seguenti:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a>L'aggiornamento di script di compilazione per il progetto attore hello

In precedenza e utilizzato toobe come le seguenti:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a>L'aggiornamento di script di compilazione del progetto client di test hello

Qui le modifiche sono modifiche toohello simili illustrate nella sezione precedente, vale a dire, file di progetto hello attore. In precedenza hello Gradle toobe script utilizzato come le seguenti:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a>Passaggi successivi

* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse](service-fabric-get-started-eclipse.md)
* [Interagire con i cluster di Service Fabric usando hello servizio infrastruttura CLI](service-fabric-cli.md)
