---
title: aaaHow toogenerate e trasferire chiavi HSM protette per insieme credenziali chiavi Azure | Documenti Microsoft
description: Utilizzare questo toohelp articolo pianificare, generare e trasferire la propria toouse chiavi HSM protette insieme di credenziali chiave di Azure. Anche noto come BYOK o Bring Your Own Key.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Come toogenerate e trasferire chiavi HSM protette per l'insieme di credenziali chiave di Azure
## <a name="introduction"></a>Introduzione
Per maggiore sicurezza, quando si usa l'insieme di credenziali chiave di Azure, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello. Questo scenario è spesso tooas cui *trasferire la propria chiave*, o BYOK. Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato. Insieme di credenziali chiave di Azure Usa famiglia nShield di Thales di tooprotect moduli di protezione hardware le chiavi.

Utilizzare informazioni hello toohelp in questo argomento si pianificano, generare e trasferire la propria toouse chiavi HSM protette insieme di credenziali chiave di Azure.

Questa funzionalità non è disponibile per la versione di Azure per la Cina.

> [!NOTE]
> Per altre informazioni sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)  
>
> Per un'esercitazione introduttiva che illustra la creazione di un insieme di credenziali delle chiavi per chiavi HSM protette, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).
>
>

Ulteriori informazioni sulla generazione e trasferimento di una chiave HSM protetta tramite Internet hello:

* Chiave di hello è generata in una workstation offline per ridurre la superficie di attacco hello.
* chiave di Hello viene crittografata con una chiave chiave (scambio), che rimane crittografata finché viene trasferito toohello moduli di protezione hardware dell'insieme di credenziali chiave di Azure. Solo hello versione crittografata della chiave lascia workstation originale hello.
* Hello set di strumenti imposta proprietà sulla chiave del tenant che associa la chiave toohello ambiente di sicurezza insieme credenziali chiavi Azure. Pertanto dopo moduli di protezione hardware dell'insieme di credenziali chiave hello Azure ricevuto e decrittografato la chiave, solo questi componenti a poterla usare. La chiave non può essere esportata. Questa associazione viene applicata dai moduli di protezione hardware Thales hello.
* Hello chiave chiave (scambio) che viene utilizzato tooencrypt la chiave viene generata nei moduli di protezione hardware dell'insieme di credenziali chiave hello Azure e non è esportabile. i moduli HSM Hello imporre che non può essere una versione crittografata di hello KEK all'esterno di hello moduli di protezione hardware. Set di strumenti hello include inoltre un'attestazione di Thales che hello KEK non è esportabile e che è stata generata in un modulo di protezione hardware originale prodotto da Thales.
* set di strumenti Hello include un'attestazione di Thales che hello insieme credenziali chiavi Azure anche l'ambiente di sicurezza è stato generato in un modulo di protezione hardware originale prodotto da Thales. Questa attestazione dimostri tooyou che Microsoft Usa hardware originale.
* Microsoft usa certificati KEK separati e ambienti di sicurezza separati in ogni area geografica. Questa separazione assicura la chiave può essere utilizzata solo nei data center nell'area di hello in cui è stata generata. Una chiave di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Altre informazioni sui moduli di protezione hardware di Thales e sui servizi di Microsoft
Thales e-Security è un leader a livello di crittografia dei dati e servizi finanziari toohello soluzioni sicurezza informatica, tecnologico, produzione, enti pubblici e settori di tecnologia. Con un 40 anni di protezione aziendali e informazioni per enti pubblici, le soluzioni Thales vengono usate da quattro hello cinque principali energetico e aerospaziale società. in 22 paesi NATO, e consentono di proteggere più dell'80 percento delle transazioni di pagamento in tutto il mondo.

Microsoft ha collaborato con lo stato di Thales tooenhance hello livello tecnologico dei moduli di protezione hardware. Questi miglioramenti consentono tooget hello tra i vantaggi dei servizi ospitati senza perdere il controllo sulle proprie chiavi. In particolare, questi miglioramenti consentono a Microsoft gestire hello moduli di protezione hardware in modo che non è necessario. Come cloud di Azure, servizio insieme di credenziali chiave garantisce la scalabilità verticale a breve preavviso toomeet picchi di utilizzo dell'organizzazione. AT hello stesso tempo, la chiave è protetta all'interno di Microsoft: si mantiene il controllo sul ciclo di vita chiave hello perché genera chiave hello e trasferirlo hardware del tooMicrosoft.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure
Hello utilizzare seguenti informazioni e procedure, se si intende generare la propria chiave HSM protetta e quindi trasferire tale insieme di credenziali chiave tooAzure: hello portare il proprio scenario key (BYOK).

## <a name="prerequisites-for-byok"></a>Prerequisiti per la modalità BYOK
Vedere hello seguente tabella per un elenco di prerequisiti per trasferire la propria chiave (BYOK) per insieme credenziali chiavi Azure.

| Requisito | Altre informazioni |
| --- | --- |
| TooAzure una sottoscrizione |toocreate un insieme di credenziali chiave di Azure, necessaria una sottoscrizione di Azure: [iscriversi per una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) |
| Hello insieme di credenziali chiave di Azure Premium del servizio livello toosupport chiavi HSM protette |Per ulteriori informazioni sui livelli di servizio hello e funzionalità per l'insieme di credenziali chiave di Azure, vedere hello [dei prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) sito Web. |
| Moduli di protezione hardware Thales, smart card e software di supporto |È necessario disporre di accesso tooa modulo di protezione Hardware Thales e base conoscenze operative di protezione hardware Thales. Vedere [modulo di protezione Hardware Thales](https://www.thales-esecurity.com/msrms/buy) per elenco hello dei modelli compatibili o toopurchase un modulo HSM se non è uno. |
| Hello hardware e software seguenti:<ol><li>Una workstation x64 offline con Windows 7 come versione minima del sistema operativo Windows e software Thales nShield con versione minima 11.50.<br/><br/>Se questa workstation esegue Windows 7, è necessario [installare Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Una workstation in cui è connesso toohello Internet e ha un sistema operativo di Windows 7 e [Azure PowerShell](/powershell/azure/overview) **minima versione 1.1.0** installato.</li><li>Unità USB o un altro dispositivo di archiviazione portatile con almeno 16 MB di spazio disponibile.</li></ol> |Per motivi di sicurezza, è consigliabile che prima workstation hello non è connesso tooa rete. Questa indicazione tuttavia non viene applicata a livello di codice.<br/><br/>Si noti che nelle istruzioni hello che seguono, questa workstation workstation disconnessa hello tooas cui viene fatto riferimento.</p></blockquote><br/>Inoltre, se la chiave del tenant è per una rete di produzione, è consigliabile utilizzare una seconda workstation separata toodownload hello set di strumenti e il caricamento hello chiave del tenant. Ma a scopo di test, è possibile utilizzare hello stessa workstation come primo hello.<br/><br/>Si noti che nelle istruzioni hello che seguono, alla seconda workstation workstation connessa a Internet di cui viene fatto riferimento tooas hello.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Generare e trasferire la chiave tooAzure modulo di protezione hardware dell'insieme di credenziali chiave
Verranno utilizzati i seguenti cinque passaggi toogenerate hello e trasferire la chiave tooan hardware dell'insieme di credenziali chiave di Azure:

* [Passaggio 1: Preparare la workstation connessa a Internet](#step-1-prepare-your-internet-connected-workstation)
* [Passaggio 2: Preparare la workstation disconnessa](#step-2-prepare-your-disconnected-workstation)
* [Passaggio 3: Generare la chiave](#step-3-generate-your-key)
* [Passaggio 4: Preparare la chiave per il trasferimento](#step-4-prepare-your-key-for-transfer)
* [Passaggio 5: Trasferire la chiave tooAzure insieme di credenziali chiave](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Passaggio 1: Preparare la workstation connessa a Internet
Per il primo passaggio, hello seguire le procedure seguenti nella workstation che è connesso toohello Internet.

### <a name="step-11-install-azure-powershell"></a>Passaggio 1.1: Installare Azure PowerShell
Dalla workstation connessa a Internet hello, scaricare e installare modulo Azure PowerShell hello che include i cmdlet di hello toomanage insieme credenziali chiavi Azure. È necessaria la versione minima 0.8.13.

Per istruzioni sull'installazione, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Passaggio 1.2: Ottenere l'ID sottoscrizione di Azure
Avviare una sessione di Azure PowerShell e accedere tooyour account Azure con hello comando seguente:

        Add-AzureAccount
Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password. Utilizzare quindi hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:

        Get-AzureSubscription
Dall'output di hello, individuare l'ID di hello per sottoscrizione hello che si utilizzeranno per insieme credenziali chiavi Azure. Questo ID sottoscrizione verrà usato in seguito.

Non chiudere la finestra di Azure PowerShell hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Passaggio 1.3: Scaricare il set di strumenti BYOK hello per insieme credenziali chiavi Azure
Passare toohello Microsoft Download Center e [scaricare set di strumenti BYOK insieme di credenziali chiave di Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) per area geografica o istanza di Azure. Utilizzare la seguente hello hash del pacchetto toodownload nome pacchetto di informazioni tooidentify hello e il corrispondente SHA-256:

- - -
**Stati Uniti:**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europa:**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Asia:**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**America Latina:**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Giappone:**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Corea:**

KeyVault-BYOK-strumenti-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Australia:**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure per enti pubblici:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**Dipartimento della difesa del governo degli Stati Uniti:**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Canada:**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Germania:**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**India:**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Regno Unito:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

integrità hello toovalidate dello scaricato set di strumenti BYOK, dalla sessione di PowerShell di Azure, utilizzare hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

set di strumenti di Hello include seguente hello:

* Un pacchetto di chiavi per lo scambio di chiavi (KEK) con un nome che inizia con **BYOK-KEK-pkg-.**
* Un pacchetto relativo all'ambiente di sicurezza con un nome che inizia con **BYOK-SecurityWorld-pkg-.**
* Uno script python denominato **verifykeypackage.py.**
* File eseguibile dalla riga di comando denominato **KeyTransferRemote.exe** e DLL associate.
* Componente Visual C++ Redistributable Package denominato **vcredist_x64.exe.**

Copia un'unità USB tooa hello pacchetto o altro dispositivo di archiviazione portatile.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Passaggio 2: Preparare la workstation disconnessa
Per questo secondo passaggio, hello seguire le procedure seguenti in workstation hello che non sia connessa tooa rete (hello Internet o rete interna).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Passaggio 2.1: Preparare workstation disconnessa hello con modulo di protezione hardware Thales
Installare il software di supporto nCipher (Thales) hello in un computer Windows e quindi collegare un computer toothat di protezione hardware Thales.

Verificare che hello strumenti Thales si trovino nei percorsi (**%nfast_home%\bin**). Ad esempio, digitare il seguente hello:

        set PATH=%PATH%;"%nfast_home%\bin"

Per ulteriori informazioni, vedere Guida dell'utente hello inclusa con hello di protezione hardware Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Passaggio 2.2: Installazione hello set di strumenti BYOK nella workstation disconnessa hello
Copiare pacchetto di set di strumenti BYOK hello dall'unità USB hello o un altro dispositivo di archiviazione portatile e quindi hello seguenti:

1. Estrarre i file di hello dal pacchetto scaricato hello in una cartella qualsiasi.
2. In tale cartella eseguire vcredist_x64.exe.
3. Seguire le istruzioni di hello toohello installare i componenti di runtime di hello Visual C++ per Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Passaggio 3: Generare la chiave
Per questo terzo passaggio, hello seguire le procedure seguenti nella workstation disconnessa hello. toocomplete questo passaggio il modulo di protezione hardware deve essere in modalità di inizializzazione. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Passaggio 3.1: Modificare hello HSM modalità too'I'
Se si utilizza nShield di Thales bordo, in modalità hello toochange: 1. Modalità hello modalità pulsante toohighlight hello obbligatorio. 2. Entro pochi secondi, tenere premuto il pulsante Cancella hello per pochi secondi. Se viene modificata la modalità hello, hello nuova modalità si arresta LED lampeggiante e rimane acceso. Hello il LED di stato potrebbe flash irregolare per pochi secondi e quindi fa lampeggiare regolarmente quando il dispositivo hello è pronto. In caso contrario, hello dispositivo rimane in modalità corrente hello con la modalità appropriata hello LED acceso.

### <a name="step-32-create-a-security-world"></a>Passaggio 3.2: Creare un ambiente di sicurezza
Avviare un prompt dei comandi ed eseguire hello programma new-world di Thales.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Tale programma crea un **ambiente di sicurezza** file NFAST_KMDATA%\local\world, che corrisponde a cartella C:\ProgramData\nCipher\Key Management data\local. toohello %. È possibile utilizzare valori diversi per il quorum hello ma in questo esempio, si è ancora schede vuote tooenter richiesta tre e un codice PIN per ciascuna di esse. Quindi, qualsiasi coppia di schede forniti ambiente di sicurezza toohello accesso completo. Tali schede diventano hello **Set di schede amministrative** per il nuovo ambiente di sicurezza hello.

Quindi hello seguenti:

* Eseguire il backup di file di hello world. Proteggere i file di hello world hello amministratore schede e i codici PIN e assicurarsi che nessuna singola persona possa accedere toomore rispetto a una scheda.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Passaggio 3.3: Modificare hello HSM modalità too'O'
Se si utilizza nShield di Thales bordo, in modalità hello toochange: 1. Modalità hello modalità pulsante toohighlight hello obbligatorio. 2. Entro pochi secondi, tenere premuto il pulsante Cancella hello per pochi secondi. Se viene modificata la modalità hello, hello nuova modalità si arresta LED lampeggiante e rimane acceso. Hello il LED di stato potrebbe flash irregolare per pochi secondi e quindi fa lampeggiare regolarmente quando il dispositivo hello è pronto. In caso contrario, hello dispositivo rimane in modalità corrente hello con la modalità appropriata hello LED acceso.


### <a name="step-34-validate-hello-downloaded-package"></a>Passaggio 3.4: Convalidare il pacchetto scaricato hello
Questo passaggio è facoltativo ma consigliato, in modo che sia possibile convalidare seguente hello:

* Chiave di scambio di chiave che è incluso nel set di strumenti hello Hello è stato generato da un modulo di protezione hardware Thales originale.
* hash Hello di hello World di sicurezza che è incluso nel set di strumenti hello è stato generato da un modulo di protezione hardware Thales originale.
* Chiave di scambio chiave Hello è non esportabile.

> [!NOTE]
> hello toovalidate scaricato pacchetto, hello HSM deve essere connessa, acceso e deve avere un ambiente di sicurezza (ad esempio hello quello che appena creato).
>
>

pacchetto di hello scaricato toovalidate:

1. Eseguire script verifykeypackage.py hello digitando uno dei seguenti hello, a seconda dell'area geografica o l'istanza di Azure:

   * America del Nord

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Europa

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Asia

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * America Latina

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Giappone

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Per la Corea:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Per l'Australia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Per il Dipartimento della difesa del governo degli Stati Uniti:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Per il Canada:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Per la Germania:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Per l'India:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hello software Thales include python nel %NFAST_HOME%\python\bin
     >
     >
2. Confermare la visualizzazione seguente hello, che indica il completamento della convalida: **risultato: operazione riuscita**

Questo script consente di convalidare la catena di firmatari hello backup toohello chiave radice di Thales. Hello hash di questa chiave radice è incorporata nello script hello e il relativo valore deve essere **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Si può anche confermare questo valore separatamente visitando hello [sito Web di Thales](http://www.thalesesec.com/).

Si è ora pronto toocreate una nuova chiave.

### <a name="step-35-create-a-new-key"></a>Passaggio 3.5: Creare una nuova chiave
Generare una chiave tramite hello Thales **generatekey** programma.

Eseguire hello seguente tasto di comando toogenerate hello:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Quando si esegue il comando, usare le istruzioni seguenti:

* parametro Hello *proteggere* deve essere impostato il valore di toohello **modulo**, come illustrato. Verrà creata una chiave protetta tramite modulo. set di strumenti BYOK Hello non supporta le chiavi protette da OCS.
* Sostituire il valore di hello di *contosokey* per hello **ident** e **plainname** con qualsiasi valore di stringa. sovraccarico amministrativo toominimize e ridurre il rischio di hello di errori, è consigliabile utilizzare hello stesso valore per entrambi. Hello **ident** valore deve contenere solo numeri, trattini e lettere minuscole.
* elemento pubexp Hello viene lasciato vuoto (impostazione predefinita) in questo esempio, ma è possibile specificare valori specifici. Per ulteriori informazioni, vedere la documentazione di Thales hello.

Questo comando crea un file di chiave in formato token nella cartella %NFAST_KMDATA%\local con un nome che inizia con **key_simple _**, seguito da hello **ident** che è stato specificato nel comando hello. Ad esempio: **key_simple_contosokey**. Questo file contiene una chiave crittografata.

Eseguire il backup del file di chiave in formato token in un percorso sicuro.

> [!IMPORTANT]
> Quando in seguito si trasferisce la chiave tooAzure insieme di credenziali chiave, Microsoft non è possibile esportare questa chiave tooyou indietro, pertanto è estremamente importante eseguire il backup della chiave e la sicurezza dell'ambiente in modo sicuro. Per ottenere informazioni aggiuntive e procedure consigliate per eseguire il backup della chiave, contattare Thales.
>
>

Si sono ora pronti tootransfer la chiave tooAzure insieme di credenziali chiave.

## <a name="step-4-prepare-your-key-for-transfer"></a>Passaggio 4: Preparare la chiave per il trasferimento
Per questo passaggio quarto hello seguire le procedure seguenti nella workstation disconnessa hello.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Passaggio 4.1: Creare una copia della chiave con autorizzazioni ridotte

Aprire un nuovo prompt dei comandi e modificare hello toohello percorso della directory corrente in cui è stato decompresso file zip di hello BYOK. le autorizzazioni di hello tooreduce per la chiave, da un prompt dei comandi, eseguono uno dei seguenti hello, a seconda dell'area geografica o l'istanza di Azure:

* America del Nord

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Europa

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Asia

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* America Latina

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Giappone

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Per la Corea:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Per l'Australia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Per il Dipartimento della difesa del governo degli Stati Uniti:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Per il Canada:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Per la Germania:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Per l'India:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Quando si esegue questo comando, sostituire *contosokey* con hello stesso valore specificato in **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.

Verrà chiesto tooplug le schede amministrazione ambiente di sicurezza.

Al termine, il comando hello vedrai **risultato: successo** e copia hello della chiave con autorizzazioni ridotte si trovano in hello file denominato key_xferacid _<contosokey>.

È possibile controlla hello gli ACL mediante i seguenti comandi utilizzando hello utilità Thales:

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Quando si eseguono questi comandi, sostituire contosokey con hello stesso valore specificato in **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Passaggio 4.2: Crittografare la chiave tramite la chiave per lo scambio di chiavi di Microsoft
Eseguire uno dei seguenti comandi, a seconda dell'area geografica o l'istanza di Azure hello:

* America del Nord

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Europa

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Asia

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* America Latina

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Giappone

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per la Corea:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per l'Australia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per il Dipartimento della difesa del governo degli Stati Uniti:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per il Canada:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per la Germania:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Per l'India:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Quando si esegue il comando, usare le istruzioni seguenti:

* Sostituire *contosokey* con identificatore hello usato chiave hello toogenerate **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.
* Sostituire *SubscriptionID* con ID hello hello sottoscrizione di Azure che contiene l'insieme di credenziali chiave. Questo valore è stato recuperato in precedenza, in **passaggio 1.2: ottenere l'ID sottoscrizione di Azure** da hello [preparare la workstation connessa a Internet](#step-1-prepare-your-internet-connected-workstation) passaggio.
* Sostituire *ContosoFirstHSMKey* con un'etichetta che viene usata per il nome del file di output.

Quando viene completato correttamente, viene visualizzato **risultato: operazione riuscita** ed è presente un nuovo file nella cartella corrente hello con hello dopo il nome: KeyTransferPackage -*ContosoFirstHSMkey*byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Passaggio 4.3: Copiare la workstation connessa a Internet di trasferimento della chiave pacchetto toohello
Utilizzare un'unità USB o un altro file di output di archiviazione portatile toocopy hello da hello precedente (KeyTransferPackage-ContosoFirstHSMkey.byok) passaggio tooyour workstation connessa a Internet.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Passaggio 5: Trasferire la chiave tooAzure insieme di credenziali chiave
Per il passaggio finale, utilizzare hello nella workstation connessa a Internet, hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello chiave pacchetto di trasferimento è stato copiato da hello disconnesso workstation toohello hardware dell'insieme di credenziali chiave di Azure:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Se il caricamento di hello ha esito positivo, viene visualizzato proprietà hello visualizzato della chiave di hello appena aggiunto.

## <a name="next-steps"></a>Passaggi successivi
È ora possibile usare questa chiave HSM protetta nell'insieme di credenziali delle chiavi. Per ulteriori informazioni, vedere hello **se si desidera che un modulo di protezione hardware (HSM) toouse** sezione hello [introduzione insieme credenziali chiavi Azure](key-vault-get-started.md) esercitazione.
