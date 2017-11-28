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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="3888c-104">Aggiornare le precedenti raccolte Java toofetch di applicazioni Java Service Fabric da Maven</span><span class="sxs-lookup"><span data-stu-id="3888c-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="3888c-105">Di recente, è stata spostata file binari del servizio Fabric Java da hello Service Fabric Java SDK tooMaven hosting.</span><span class="sxs-lookup"><span data-stu-id="3888c-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="3888c-106">È ora possibile usare **mavencentral** dipendenze di Service Fabric Java toofetch hello più recente.</span><span class="sxs-lookup"><span data-stu-id="3888c-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="3888c-107">Questa Guida introduttiva si consente di aggiornare le applicazioni Java esistenti, che è stato creato in precedenza toobe utilizzato con Service Fabric Java SDK, utilizzando entrambi Yeoman modello o toobe compatibile con hello compilazione Maven basati su Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3888c-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3888c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3888c-108">Prerequisites</span></span>
1. <span data-ttu-id="3888c-109">È necessario innanzitutto toouninstall hello SDK per Java esistente.</span><span class="sxs-lookup"><span data-stu-id="3888c-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="3888c-110">Il seguente servizio infrastruttura CLI più recente di installazione hello hello i passaggi indicati [qui](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3888c-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="3888c-111">toobuild e attività per le applicazioni Java di infrastruttura servizio hello, è necessario tooensure che si disponga di JDK 1.8 e Gradle installato.</span><span class="sxs-lookup"><span data-stu-id="3888c-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="3888c-112">Se non è ancora installato, è possibile eseguire hello seguenti tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -</span><span class="sxs-lookup"><span data-stu-id="3888c-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="3888c-113">Gli script di installazione o disinstallazione di aggiornamento hello di toouse l'applicazione hello nuovo CLI di infrastruttura servizio seguendo i passaggi di hello indicati [qui](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="3888c-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="3888c-114">È possibile fare riferimento tooour Introduzione [esempi](https://github.com/Azure-Samples/service-fabric-java-getting-started) per riferimento.</span><span class="sxs-lookup"><span data-stu-id="3888c-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="3888c-115">Dopo la disinstallazione di Service Fabric Java SDK hello Yeoman non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="3888c-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="3888c-116">Seguire i prerequisiti di hello indicati [qui](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman dell'infrastruttura del servizio Java generatore modello backup e l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="3888c-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="3888c-117">Librerie Java di Service Fabric in Maven</span><span class="sxs-lookup"><span data-stu-id="3888c-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="3888c-118">Le librerie Java di Service Fabric sono ospitate in Maven.</span><span class="sxs-lookup"><span data-stu-id="3888c-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="3888c-119">È possibile aggiungere le dipendenze di hello in hello ``pom.xml`` o ``build.gradle`` di raccolte di Service Fabric Java toouse di progetti da **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="3888c-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="3888c-120">Actor</span><span class="sxs-lookup"><span data-stu-id="3888c-120">Actors</span></span>

<span data-ttu-id="3888c-121">Supporto di Service Fabric Reliable Actors per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3888c-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="3888c-122">Services</span><span class="sxs-lookup"><span data-stu-id="3888c-122">Services</span></span>

<span data-ttu-id="3888c-123">Supporto di servizi senza stato di Service Fabric per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3888c-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="3888c-124">Altro</span><span class="sxs-lookup"><span data-stu-id="3888c-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="3888c-125">Trasporto</span><span class="sxs-lookup"><span data-stu-id="3888c-125">Transport</span></span>

<span data-ttu-id="3888c-126">Supporto del livello trasporto per l'applicazione Java di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3888c-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="3888c-127">Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio, a meno che la programmazione a livello di trasporto hello.</span><span class="sxs-lookup"><span data-stu-id="3888c-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="3888c-128">Supporto di Fabric</span><span class="sxs-lookup"><span data-stu-id="3888c-128">Fabric support</span></span>

<span data-ttu-id="3888c-129">Supporto di livello di sistema per l'infrastruttura del servizio, che comunica toonative runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3888c-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="3888c-130">Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio.</span><span class="sxs-lookup"><span data-stu-id="3888c-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="3888c-131">Si ottiene recuperato automaticamente da Maven, quando si includono hello altre dipendenze precedente.</span><span class="sxs-lookup"><span data-stu-id="3888c-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="3888c-132">Migrazione di un servizio senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3888c-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="3888c-133">il servizio service Fabric esistente senza stato Java utilizzando le dipendenze di Service Fabric recuperate dal Maven, è necessario tooupdate hello la toobuild in grado di toobe ``build.gradle`` file all'interno di hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="3888c-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="3888c-134">In precedenza e utilizzato toobe come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="3888c-134">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="3888c-135">A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3888c-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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
<span data-ttu-id="3888c-136">In generale, tooget un'idea generale sulla modalità di generazione script hello avrà un aspetto analogo per un servizio di linguaggio senza informazioni sullo stato dell'infrastruttura di servizio, è possibile fare riferimento a esempio tooany da esempi introduttivi.</span><span class="sxs-lookup"><span data-stu-id="3888c-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="3888c-137">Ecco hello [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) per esempio EchoServer hello.</span><span class="sxs-lookup"><span data-stu-id="3888c-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="3888c-138">Migrazione di un servizio Service Fabric Actors</span><span class="sxs-lookup"><span data-stu-id="3888c-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="3888c-139">toobuild in grado di toobe applicazione Java Actor di Service Fabric esistente utilizzando le dipendenze di Service Fabric recuperate dal Maven, è necessario hello tooupdate ``build.gradle`` file all'interno del pacchetto di interfaccia hello e nel pacchetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3888c-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="3888c-140">Se si dispone di un pacchetto TestClient, è necessario che anche tooupdate.</span><span class="sxs-lookup"><span data-stu-id="3888c-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="3888c-141">In questo caso, per l'attore ``Myactor``, seguente hello sarebbe posizioni hello in cui è necessario tooupdate -</span><span class="sxs-lookup"><span data-stu-id="3888c-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="3888c-142">L'aggiornamento di script di compilazione per il progetto di interfaccia hello</span><span class="sxs-lookup"><span data-stu-id="3888c-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="3888c-143">In precedenza e utilizzato toobe come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="3888c-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="3888c-144">A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3888c-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="3888c-145">L'aggiornamento di script di compilazione per il progetto attore hello</span><span class="sxs-lookup"><span data-stu-id="3888c-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="3888c-146">In precedenza e utilizzato toobe come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="3888c-146">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="3888c-147">A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3888c-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="3888c-148">L'aggiornamento di script di compilazione del progetto client di test hello</span><span class="sxs-lookup"><span data-stu-id="3888c-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="3888c-149">Qui le modifiche sono modifiche toohello simili illustrate nella sezione precedente, vale a dire, file di progetto hello attore.</span><span class="sxs-lookup"><span data-stu-id="3888c-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="3888c-150">In precedenza hello Gradle toobe script utilizzato come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="3888c-150">Previously hello Gradle script used toobe like as follows -</span></span>
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
<span data-ttu-id="3888c-151">A questo punto, le dipendenze di hello toofetch Maven, hello **aggiornato** ``build.gradle`` avrebbe parti corrispondenti hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3888c-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3888c-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3888c-152">Next steps</span></span>

* [<span data-ttu-id="3888c-153">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="3888c-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="3888c-154">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse</span><span class="sxs-lookup"><span data-stu-id="3888c-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="3888c-155">Interagire con i cluster di Service Fabric usando hello servizio infrastruttura CLI</span><span class="sxs-lookup"><span data-stu-id="3888c-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
