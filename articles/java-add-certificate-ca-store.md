---
title: "archivio certificati Autorità di certificazione Java toohello aaaAdd | Documenti Microsoft"
description: Informazioni su come tooadd archiviare un certificato della CA certificato toohello Java certificato della CA (cacerts) per il servizio di Twilio o Azure Service Bus.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Aggiunta di un archivio di certificati CA Java di toohello certificato
Hello alla procedura seguente viene illustrato in che modo tooadd un certificato della CA certificato toohello Java certificato della CA (cacerts) archiviate. esempio Hello utilizzato per il certificato CA hello richiesta da hello Twilio servizio. Le informazioni fornite più avanti in argomento hello viene descritto come certificato di hello tooinstall autorità di certificazione per hello Azure Service Bus. 

È possibile utilizzare keytool tooadd hello autorità di certificazione certificato precedente toozipping il JDK e aggiungerlo tooyour progetto Azure **approot** cartella oppure è Impossibile eseguire un'attività di avvio di Azure che utilizza keytool tooadd hello certificato. Si presuppone che si aggiungerà un'autorità di certificazione certificato precedente toohello JDK viene compresso. Inoltre, verrà utilizzato un certificato della CA specifico esempio hello, ma i passaggi di hello di ottenere un certificato della CA diverso e importarli hello cacerts archivio sarebbe simile.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>archiviare un cacerts toohello certificato tooadd
1. In un prompt dei comandi che è impostato del JDK tooyour **jdk\jre\lib\security** cartella, eseguire hello toosee vengono installati i certificati seguenti:
   
    `keytool -list -keystore cacerts`
   
    Verrà richiesto di hello archivio password. password predefinita Hello è **modificare**. (Se si desidera password hello toochange, vedere documentazione hello in <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) In questo esempio si presuppone che tale certificato hello con 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 non è presente e che si desidera tooimport it (è necessaria questa particolare certificato dal servizio API di Twilio hello).
2. Ottenere il certificato di hello dall'elenco di hello dei certificati elencati in [i certificati radice GeoTrust](http://www.geotrust.com/resources/root-certificates/). Fare doppio clic su collegamento hello per certificato hello con numero di serie 35:DE:F4:CF e salvarlo toohello **jdk\jre\lib\security** cartella. Ai fini di questo esempio, è stato salvato il file tooa denominato **Equifax\_sicura\_certificato\_Authority.cer**.
3. Importare il certificato di hello tramite hello comando seguente:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Quando viene richiesto tootrust questo certificato, se il certificato di hello ha 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, rispondere digitando **y**.
4. Esecuzione hello seguente certificato di CA hello tooensure comando sia stato importato correttamente:
   
    `keytool -list -keystore cacerts`
5. Comprimere hello JDK e aggiungerlo tooyour progetto Azure **approot** cartella.

Per informazioni sullo strumento Keytool, vedere <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certificati radice di Azure
Le applicazioni che usano servizi di Azure (ad esempio Azure Service Bus) necessario certificato radice Baltimore CyberTrust di hello tootrust. (A partire dal 15 aprile 2013, Azure è stata avviata la migrazione da hello GTE CyberTrust Root globale toohello Baltimore CyberTrust Root. Questa migrazione ha impiegato più mesi toocomplete.)

Hello Baltimore certificato potrebbe già essere installato nell'archivio cacerts, pertanto tenere presente hello toorun **keytool-elenco** comando toosee prima se esiste già.

Se è necessario tooadd hello Baltimore CyberTrust Root, che include il numero di serie 02:00:00:b9 e SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74. Può essere scaricato da <https://cacert.omniroot.com/bc2025.crt>, salvare file locale tooa con estensione **con estensione cer**e quindi importate con **keytool** come illustrato in precedenza.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sui certificati radice hello utilizzato da Azure, vedere [Azure radice certificato migrazione](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Per altre informazioni su Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).

