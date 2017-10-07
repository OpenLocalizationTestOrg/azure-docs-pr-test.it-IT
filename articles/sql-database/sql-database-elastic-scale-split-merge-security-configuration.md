---
title: configurazione della sicurezza di tipo merge aaaSplit | Documenti Microsoft
description: Impostazione dei certificati 409 per la crittografia
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Configurazione della sicurezza del servizio di divisione e unione
servizio di suddivisione/unione hello toouse, è necessario configurare correttamente sicurezza. servizio Hello fa parte della funzionalità di scalabilità elastica hello di Database SQL di Microsoft Azure. Per altre informazioni, vedere [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Configurazione dei certificati
I certificati vengono configurati in due modi. 

1. [hello tooConfigure certificato SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure i certificati Client](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>certificati tooobtain
Certificati possono essere ottenuti da una autorità di certificazione (CA) pubblica o da hello [servizio certificato Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Questi sono hello preferito metodi tooobtain certificati.

Se tali opzioni non sono disponibili, è possibile generare **certificati autofirmati**.

## <a name="tools-toogenerate-certificates"></a>Certificati toogenerate strumenti
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>strumenti di hello toorun
* Da un Prompt dei comandi per gli sviluppatori per Visual Studio, vedere l'articolo relativo al [prompt dei comandi di Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Se installato, passare a:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Ottenere hello WDK da [Windows 8.1: Download di Kit e strumenti](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certificato SSL di hello tooconfigure
Un certificato SSL è obbligatorio tooencrypt hello comunicazione e l'autenticazione server hello. Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:

### <a name="create-a-new-self-signed-certificate"></a>Creare un nuovo certificato autofirmato
1. [Creare un certificato autofirmato](#create-a-self-signed-certificate)
2. [Creare un file PFX per il certificato SSL autofirmato](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Caricare il certificato SSL tooCloud servizio](#upload-ssl-certificate-to-cloud-service)
4. [Aggiornare il certificato SSL nel file di configurazione del servizio](#update-ssl-certificate-in-service-configuration-file)
5. [Importare l'Autorità di certificazione SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>archiviare un certificato esistente dal certificato hello toouse
1. [Esportare il certificato SSL dall'archivio certificati](#export-ssl-certificate-from-certificate-store)
2. [Caricare il certificato SSL tooCloud servizio](#upload-ssl-certificate-to-cloud-service)
3. [Aggiornare il certificato SSL nel file di configurazione del servizio](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse un certificato esistente in un file PFX
1. [Caricare il certificato SSL tooCloud servizio](#upload-ssl-certificate-to-cloud-service)
2. [Aggiornare il certificato SSL nel file di configurazione del servizio](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certificati client tooconfigure
In ordine tooauthenticate richieste toohello service sono richiesti certificati client. Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:

### <a name="turn-off-client-certificates"></a>Disabilitare i certificati client
1. [Disabilitare l'autenticazione basata su certificati client](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Rilasciare nuovi certificati autofirmati
1. [Creare un'autorità di certificazione autofirmata](#create-a-self-signed-certification-authority)
2. [Carica certificato della CA tooCloud servizio](#upload-ca-certificate-to-cloud-service)
3. [Aggiornare il certificato della CA nel file di configurazione del servizio](#update-ca-certificate-in-service-configuration-file)
4. [Rilasciare certificati client](#issue-client-certificates)
5. [Creare file PFX per i certificati client](#create-pfx-files-for-client-certificates)
6. [Importare il certificato client](#Import-Client-Certificate)
7. [Copiare le identificazioni personali del certificato client](#copy-client-certificate-thumbprints)
8. [Configurare i client consentiti in File di configurazione del servizio hello](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Usare i certificati client esistenti
1. [Find CA Public Key](#find-ca-public-key)
2. [Carica certificato della CA tooCloud servizio](#Upload-CA-certificate-to-cloud-service)
3. [Aggiornare il certificato della CA nel file di configurazione del servizio](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Copiare le identificazioni personali del certificato client](#Copy-Client-Certificate-Thumbprints)
5. [Configurare i client consentiti in File di configurazione del servizio hello](#configure-allowed-clients-in-the-service-configuration-file)
6. [Configurare il controllo della revoca del certificato client](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Indirizzi IP consentiti
Endpoint di servizio di accesso toohello può essere limitato toospecific intervalli di indirizzi IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>crittografia tooconfigure per archivio hello
Le credenziali di hello tooencrypt obbligatorio archiviate nell'archivio dei metadati hello è un certificato. Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:

### <a name="use-a-new-self-signed-certificate"></a>Usare un nuovo certificato autofirmato
1. [Creare un certificato autofirmato](#create-a-self-signed-certificate)
2. [Creare un file PFX per il certificato di crittografia autofirmato](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Caricare il certificato di crittografia tooCloud servizio](#upload-encryption-certificate-to-cloud-service)
4. [Aggiornare il certificato di crittografia nel file di configurazione del servizio](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Usare un certificato esistente dall'archivio certificati hello
1. [Esportare il certificato di crittografia dall'archivio certificati](#export-encryption-certificate-from-certificate-store)
2. [Caricare il certificato di crittografia tooCloud servizio](#upload-encryption-certificate-to-cloud-service)
3. [Aggiornare il certificato di crittografia nel file di configurazione del servizio](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Usare un certificato esistente in un file PFX
1. [Caricare il certificato di crittografia tooCloud servizio](#upload-encryption-certificate-to-cloud-service)
2. [Aggiornare il certificato di crittografia nel file di configurazione del servizio](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>configurazione predefinita di Hello
configurazione predefinita di Hello Nega tutte endpoint HTTP toohello di accesso. Si tratta di hello impostazione, consigliata poiché hello richieste toothese endpoint potrebbe contenere informazioni riservate come le credenziali del database.
configurazione predefinita di Hello consente tutti endpoint HTTPS toohello di accesso. Tale impostazione può essere limitata ulteriormente.

### <a name="changing-hello-configuration"></a>Modifica configurazione hello
Hello gruppo di regole di controllo di accesso che si applicano tooand endpoint sono configurati in hello  **<EndpointAcls>**  sezione hello **file di configurazione del servizio**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

le regole di Hello in un gruppo di controllo di accesso vengono configurate un <AccessControl name=""> sezione del file di configurazione del servizio hello. 

formato di Hello è illustrato nella documentazione relativa a elenchi di controllo di accesso rete.
Ad esempio, tooallow solo indirizzi IP in hello 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint di intervallo, le regole di hello sono analogo al seguente:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Prevenzione di attacchi Denial of Service
Esistono due diversi meccanismi supportati toodetect e impediscono attacchi Denial of Service:

* Limitare il numero di richieste simultanee per host remoto (opzione disattivata per impostazione predefinita).
* Limitare la frequenza di accesso per host remoto (opzione attivata per impostazione predefinita).

Questi sono basati sulle funzionalità di hello documentata in sicurezza IP dinamica in IIS. Quando la modifica di questa configurazione prestare attenzione al hello seguenti fattori:

* comportamento di Hello di proxy e i dispositivi NAT sulle informazioni relative a host remoto hello
* Ogni risorsa tooany richiesta nel ruolo web hello è considerato (ad esempio, il caricamento di script, immagini e così via)

## <a name="restricting-number-of-concurrent-accesses"></a>Limitazione del numero di accessi simultanei
Hello impostazioni che consentono di configurare questo comportamento sono:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Modificare DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable questa protezione.

## <a name="restricting-rate-of-access"></a>Limitazione della frequenza di accesso
Hello impostazioni che consentono di configurare questo comportamento sono:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Configurazione hello risposta tooa ha negato la richiesta
Hello seguente consente di configurare hello risposta tooa ha negato la richiesta:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Per altri valori supportati, consultare la documentazione di toohello per la sicurezza IP dinamica in IIS.

## <a name="operations-for-configuring-service-certificates"></a>Operazioni per la configurazione dei certificati di servizio
Questo argomento è solo per riferimento. Eseguire le operazioni di configurazione hello descritte in:

* Configurare il certificato SSL hello
* Configurare i certificati client.

## <a name="create-a-self-signed-certificate"></a>Creare un certificato autofirmato
Eseguire:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* URL del servizio - n con hello. Sono supportati caratteri jolly ("CN=*.cloudapp.net") e nomi alternativi ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").
* -e con data di scadenza certificato hello creare una password complessa e specificarlo quando richiesto.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Creare un file PFX per il certificato SSL autofirmato
Eseguire:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Immettere la password e quindi esportare il certificato con queste opzioni:

* Sì, Esporta la chiave privata di hello
* Esporta tutte le proprietà estese

## <a name="export-ssl-certificate-from-certificate-store"></a>Esportare il certificato SSL dall'archivio certificati
* Trovare il certificato.
* Fare clic su Azioni -> Tutte le attività -> Esporta.
* Esportare il certificato in un file PFX con queste opzioni:
  * Sì, Esporta la chiave privata di hello
  * Se possibile, Includi tutti i certificati nel percorso certificazione hello * esportare tutte le proprietà estese

## <a name="upload-ssl-certificate-toocloud-service"></a>Caricare il servizio toocloud certificato SSL
Caricamento del certificato con hello esistente o generati. File PFX con hello coppia di chiavi SSL:

* Immettere la password di hello la protezione delle informazioni sulla chiave privata di hello

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Aggiornare il certificato SSL nel file di configurazione del servizio
Aggiornare il valore di identificazione personale hello di hello impostazione nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Importare l'Autorità di certificazione SSL
Seguire questi passaggi nell'account/macchina tutti che comunicherà con il servizio hello:

* Fare doppio clic su hello. File CER in Esplora risorse
* Nella finestra di dialogo certificato hello, fare clic su Installa certificato...
* Importare certificato nell'archivio Autorità di certificazione radice attendibili hello

## <a name="turn-off-client-certificate-based-authentication"></a>Disabilitare l'autenticazione basata su certificati client
Solo autenticazione basata sui certificati client è supportata e disabilitarlo consentirà l'accesso pubblico toohello gli endpoint del servizio, a meno che non esistono altri meccanismi sono disponibili (ad esempio Microsoft rete virtuale di Azure).

Modificare queste impostazioni toofalse in funzionalità del servizio configurazione file tooturn hello hello off:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Nell'impostazione del certificato CA hello, copiare hello hello SSL stessa identificazione digitale certificato:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Creare un'autorità di certificazione autofirmata
Eseguire i seguenti passaggi toocreate tooact un certificato autofirmato come autorità di certificazione hello:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize,

* -e con la data di scadenza certificazione hello

## <a name="find-ca-public-key"></a>Trovare la chiave pubblica CA
Tutti i certificati client devono essere stati rilasciati da un'autorità di certificazione attendibile per il servizio di hello. Trovare toohello chiave pubblica hello autorità di certificazione che ha emesso i certificati client hello che verranno toobe utilizzata per l'autenticazione in tooupload ordine servizio cloud toohello.

Se il file hello con chiave pubblica hello non è disponibile, è possibile esportarlo dall'archivio certificati hello:

* Trovare il certificato.
  * Ricerca di un certificato client emesso da hello stessa autorità di certificazione
* Fare doppio clic sul certificato hello.
* Selezionare scheda Percorso certificazione hello nella finestra di dialogo certificato hello.
* Fare doppio clic sulla voce di autorità di certificazione hello nel percorso di hello.
* Annotare le proprietà del certificato hello.
* Chiude hello **certificato** finestra di dialogo.
* Trovare il certificato.
  * Ricerca di hello CA indicata in precedenza.
* Fare clic su Azioni -> Tutte le attività -> Esporta.
* Esportare il certificato in un file con estensione CER con queste opzioni:
  * **No, non esportare la chiave privata di hello**
  * Se possibile, Includi tutti i certificati nel percorso certificazione hello.
  * Esportare tutte le proprietà estese.

## <a name="upload-ca-certificate-toocloud-service"></a>Autorità di certificazione certificato toocloud servizio di caricamento
Caricamento del certificato con hello esistente o generati. File CER con chiave pubblica hello autorità di certificazione.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Aggiornare il certificato della CA nel file di configurazione del servizio
Aggiornare il valore di identificazione personale hello di hello impostazione nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Aggiornare il valore di hello di hello dopo l'impostazione con hello stessa identificazione personale:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Rilasciare certificati client
Ogni servizio di hello singoli tooaccess autorizzato deve avere un certificato client emesso per his/hers esclusivo usare e deve scegliere che una password complessa tooprotect his/hers proprietari relativa chiave privata. 

Hello alla procedura seguente deve essere eseguito in hello nello stesso computer in cui hello autorità di certificazione certificato autofirmato è stato generato e archiviato:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Personalizzazione

* -n con un ID per il client toohello che verrà autenticata con il certificato
* -e con data di scadenza certificato hello
* MyID.pvk e MyID.cer con nomi file univoci per il certificato client

Questo comando richiederà una password toobe creata e quindi utilizzata una sola volta. Usare una password complessa.

## <a name="create-pfx-files-for-client-certificates"></a>Creare file PFX per i certificati client
Per ogni certificato client generato, eseguire:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizzazione

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Immettere la password e quindi esportare il certificato con queste opzioni:

* Sì, Esporta la chiave privata di hello
* Esporta tutte le proprietà estese
* Questo certificato viene emessa la toowhom singoli Hello deve scegliere password esportazione hello

## <a name="import-client-certificate"></a>Importare il certificato client
Ogni singolo per il quale è stato emesso un certificato client deve importare una coppia di chiavi hello in macchine hello potrà utilizzerà toocommunicate con servizio hello:

* Fare doppio clic su hello. File PFX in Esplora risorse
* Importare certificati in hello personale archiviare con almeno questa opzione:
  * Includi tutte le proprietà estese.

## <a name="copy-client-certificate-thumbprints"></a>Copiare le identificazioni personali del certificato client
Ogni singolo per il quale è stato emesso un certificato client è necessario seguire questi passaggi nell'identificazione personale hello tooobtain di ordine di his/hers certificato che verrà aggiunto il file di configurazione servizio toohello:

* Eseguire certmgr.exe.
* Selezionare la scheda personale hello
* Fare doppio clic sul certificato client hello toobe utilizzato per l'autenticazione
* In hello certificato finestra di dialogo visualizzata, selezionare scheda Dettagli hello
* Assicurarsi che in Mostra sia visualizzato Tutti.
* Campo di selezione hello denominato identificazione personale nell'elenco di hello
* Copiare il valore di hello dell'identificazione digitale hello * * eliminare i caratteri Unicode non visibili davanti prima cifra hello * * eliminare tutti gli spazi

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Configurare i client consentiti in file di configurazione del servizio hello
Aggiornare il valore di hello di hello seguente impostazione nel file di configurazione del servizio hello con un elenco delimitato da virgole di identificazioni personali di hello dei certificati client hello consentiti l'accesso toohello servizio:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Configurare il controllo della revoca del certificato client
impostazione predefinita Hello non verifica con hello autorità di certificazione per lo stato di revoca dei certificati client. tooturn su hello controlla se l'autorità di certificazione che ha rilasciato i certificati client hello hello supporta tali controlli, modificare hello seguente impostazione con uno dei valori hello definiti nell'enumerazione X509RevocationMode hello:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Creare un file PFX per certificati di crittografia autofirmati
Per un certificato di crittografia eseguire:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalizzazione

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Immettere la password e quindi esportare il certificato con queste opzioni:

* Sì, Esporta la chiave privata di hello
* Esporta tutte le proprietà estese
* Quando si carica il servizio cloud di hello certificato toohello, sarà necessario password hello.

## <a name="export-encryption-certificate-from-certificate-store"></a>Esportare il certificato di crittografia dall'archivio certificati
* Trovare il certificato.
* Fare clic su Azioni -> Tutte le attività -> Esporta.
* Esportare il certificato in un file PFX con queste opzioni: 
  * Sì, Esporta la chiave privata di hello
  * Se possibile, Includi tutti i certificati nel percorso certificazione hello 
* Esporta tutte le proprietà estese

## <a name="upload-encryption-certificate-toocloud-service"></a>Servizio di crittografia certificato toocloud di caricamento
Caricamento del certificato con hello esistente o generati. File PFX con una coppia di chiavi di crittografia hello:

* Immettere la password di hello la protezione delle informazioni sulla chiave privata di hello

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Aggiornare il certificato di crittografia nel file di configurazione del servizio
Aggiornare il valore di identificazione personale hello di hello impostazioni nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Operazioni comuni relative ai certificati
* Configurare il certificato SSL hello
* Configurare i certificati client.

## <a name="find-certificate"></a>Trovare il certificato.
A tale scopo, seguire questa procedura:

1. Eseguire mmc.exe.
2. File -> Aggiungi/Rimuovi snap-in.
3. Selezionare **Certificati**.
4. Fare clic su **Aggiungi**.
5. Scegliere percorso dell'archivio certificati hello.
6. Fare clic su **Finish**.
7. Fare clic su **OK**.
8. Espandere **Certificati**.
9. Espandere il nodo di archivio certificato hello.
10. Espandere il nodo figlio di hello certificato.
11. Selezionare un certificato nell'elenco di hello.

## <a name="export-certificate"></a>Esportare il certificato
In hello **esportazione guidata certificati**:

1. Fare clic su **Avanti**.
2. Selezionare **Sì**, quindi **Esporta chiave privata di hello**.
3. Fare clic su **Avanti**.
4. Selezionare il formato di file di hello output desiderato.
5. Controllare le opzioni di hello desiderato.
6. Selezionare **Password**.
7. Immettere una password complessa e confermarla.
8. Fare clic su **Avanti**.
9. Digitare o selezionare un nome di file in cui toostore hello certificato (usare una. Con estensione PFX).
10. Fare clic su **Avanti**.
11. Fare clic su **Finish**.
12. Fare clic su **OK**.

## <a name="import-certificate"></a>Importare il certificato
In Importazione guidata certificati hello:

1. Selezionare il percorso di archivio hello.
   
   * Selezionare **utente corrente** se solo i processi in esecuzione in utente corrente avrà accesso servizio hello
   * Selezionare **computer locale** se altri processi nel computer avrà accesso servizio hello
2. Fare clic su **Avanti**.
3. Se l'importazione da un file, confermare il percorso del file hello.
4. Se si importa un file PFX:
   1. Immettere la password di hello protegge la chiave privata di hello
   2. Selezionare le opzioni di importazione.
5. Selezionare i certificati di "Posto" nel seguente archivio hello
6. Fare clic su **Sfoglia**.
7. Selezionare l'archivio di hello desiderato.
8. Fare clic su **Finish**.
   
   * Se è stato scelto l'archivio di autorità di certificazione radice attendibili hello, fare clic su **Sì**.
9. Fare clic su **OK** in tutte le finestre di dialogo.

## <a name="upload-certificate"></a>Caricamento del certificato
In hello [portale di Azure](https://portal.azure.com/)

1. Selezionare **Servizi cloud**.
2. Selezionare servizio cloud hello.
3. Scegliere dal menu superiore hello **certificati**.
4. Nella barra inferiore hello, fare clic su **caricare**.
5. Selezionare il file di certificato hello.
6. Se si tratta di una. PFX file, immettere la password di hello per la chiave privata di hello.
7. Al termine, copiare l'identificazione personale del certificato hello da hello nuova voce di elenco hello.

## <a name="other-security-considerations"></a>Altre considerazioni sulla sicurezza
le impostazioni SSL Hello descritte in questo documento crittografare le comunicazioni tra il servizio hello e i relativi client quando viene utilizzato l'endpoint HTTPS hello. Questo aspetto è importante perché le credenziali per l'accesso al database e altri potenziali informazioni riservate contenute nella comunicazione hello. Si noti tuttavia che il servizio hello mantiene lo stato interno, incluse le credenziali, in tabelle interne nel database SQL di Microsoft Azure hello fornito per l'archiviazione dei metadati nella sottoscrizione di Microsoft Azure. Il database è stato definito come parte di hello seguente impostazione nel file di configurazione del servizio (. File CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Le credenziali archiviate in questo database vengono crittografate. Tuttavia, come procedura consigliata, assicurarsi che i ruoli web e di lavoro delle distribuzioni del servizio vengono conservati backup toodate e sicura man mano che prevedono toohello metadati del database e hello certificato di accesso utilizzato per la crittografia e decrittografia di credenziali archiviate. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

