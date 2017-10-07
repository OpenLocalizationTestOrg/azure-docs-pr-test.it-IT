---
title: problemi di connessione aaaTroubleshoot Azure point-to-site | Documenti Microsoft
description: Informazioni su come i problemi di connessione point-to-site tootroubleshoot.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Risoluzione dei problemi: problemi di connessione da punto a sito di Azure

Questo articolo elenca i problemi comuni di connessione da punto a sito che l'utente potrebbe riscontrare. e le possibili cause e soluzioni.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Errore del client VPN: Impossibile trovare un certificato

### <a name="symptom"></a>Sintomo

Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:

**Impossibile trovare un certificato utilizzabile con il protocollo EAP (Extensible Authentication Protocol). (Errore 798)**

### <a name="cause"></a>Causa

Questo problema si verifica se manca il certificato di client hello **certificati - corrente\Personale\Certificati**.

### <a name="solution"></a>Soluzione

Verificare che il certificato client hello sia installato nel seguente percorso dell'archivio certificati hello (Certmgr.msc) hello:
 
**Certificati - Utente corrente\Personale\Certificati**

Per ulteriori informazioni su come tooinstall hello certificato client, vedere [generare ed esportare i certificati per le connessioni point-to-site](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Quando si importa certificato client hello, non selezionare hello **Abilita protezione avanzata chiave privata** opzione.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Errore del client VPN: il messaggio hello ricevuto è imprevisto o non formattato correttamente

### <a name="symptom"></a>Sintomo

Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:

**messaggio ricevuto è imprevisto o non formattato correttamente. (Errore 0x80090326)**

### <a name="cause"></a>Causa

Questo problema si verifica se non è stata caricata chiave pubblica del certificato radice hello in gateway VPN di Azure hello. Può verificarsi anche se la chiave hello è danneggiata o scaduta.

### <a name="solution"></a>Soluzione

tooresolve questo problema, controllare lo stato di hello della radice hello in hello toosee portale Azure certificato se è stato revocato. Se non si è revocato, provare a reupload e un certificato radice di hello toodelete. Per altre informazioni, vedere [Creare certificati](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Errore del client VPN: Una catena di certificati è stata elaborata correttamente, ma termina 

### <a name="symptom"></a>Sintomo 

Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:

**Una catena di certificati elaborata, ma termina con un certificato radice considerato non attendibile dal provider di attendibilità hello.**

### <a name="solution"></a>Soluzione

1. Verificare che tale hello seguendo i certificati siano nella posizione corretta hello:

    | Certificate | Località |
    | ------------- | ------------- |
    | AzureClient.pfx  | Utente corrente\Personale\Certificati |
    | Azuregateway-*GUID*.cloudapp.net  | Utente corrente\Autorità di certificazione radice attendibili|
    | AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer    | Computer locale\Autorità di certificazione radice attendibili|

2. Se sono già nel percorso hello certificati hello, provare a certificati hello toodelete e reinstallarlo. Hello  **azuregateway -*GUID*. cloudapp.net** certificato è nel pacchetto di configurazione con i client VPN hello che è stato scaricato dal portale di Azure hello. È possibile utilizzare file archivers tooextract hello del file dal pacchetto hello.

## <a name="file-download-error-target-uri-is-not-specified"></a>Errore di download del file: L'URI di destinazione non è specificato

### <a name="symptom"></a>Sintomo

Viene visualizzato hello seguente messaggio di errore:

**Errore di download del file. L'URI di destinazione non è specificato.**

### <a name="cause"></a>Causa 

Questo problema si verifica a causa di un tipo di gateway non corretto. 

### <a name="solution"></a>Soluzione

deve essere il tipo di gateway VPN Hello **VPN**, e deve essere di tipo VPN hello **tipo RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Errore del client VPN: Azure VPN custom script failed (Impossibile eseguire lo script personalizzato per la VPN di Azure) 

### <a name="symptom"></a>Sintomo

Quando si tenta di tooconnect tooan rete virtuale di Azure utilizzando hello VPN client, viene visualizzato hello seguente messaggio di errore:

**Script personalizzato (tooupdate la tabella di routing.) non è riuscita. (Errore 8007026f)**

### <a name="cause"></a>Causa

Questo problema può verificarsi se la connessione VPN site-to-point di hello tooopen utilizzando un collegamento.

### <a name="solution"></a>Soluzione 

Aprire il pacchetto VPN hello direttamente anziché aprirlo dal collegamento hello.

## <a name="cannot-install-hello-vpn-client"></a>Non è possibile installare i client VPN hello

### <a name="cause"></a>Causa 

Gateway VPN di hello tootrust necessarie per la rete virtuale non è un certificato aggiuntivo. certificato Hello è incluso nel pacchetto di configurazione con i client VPN hello che viene generato da hello portale di Azure.

### <a name="solution"></a>Soluzione

Estrarre il pacchetto di configurazione client VPN di hello e trovare il file con estensione cer hello. tooinstall hello del certificato, seguire questi passaggi:

1. Aprire mmc.exe.
2. Aggiungere hello **certificati** snap-in.
3. Seleziona hello **Computer** account per il computer locale hello.
4. Pulsante destro del mouse hello **autorità di certificazione radice attendibili** nodo. Fare clic su **All attività** > **importazione**e i file con estensione cer toohello Sfoglia estratti dal pacchetto di configurazione client VPN hello.
5. Riavviare il computer di hello. 
6. Provare a eseguire tooinstall hello VPN client.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Errore del portale di Azure: Impossibile gateway VPN di toosave hello e dati hello non validi

### <a name="symptom"></a>Sintomo

Quando si tenta di modifiche hello toosave per il gateway VPN hello in hello portale di Azure, viene visualizzato hello seguente messaggio di errore:

**Gateway di rete virtuale non riuscita toosave &lt;* nome del gateway*&gt;. Data for certificate &lt;*certificate ID*&gt; is invalid.** (I dati per il certificato ID certificato non sono validi.)

### <a name="cause"></a>Causa 

Questo problema può verificarsi se hello radice certificato chiave pubblica è stata caricata contiene un carattere non valido, ad esempio uno spazio.

### <a name="solution"></a>Soluzione

Assicurarsi che i dati di hello nel certificato hello non contengano caratteri non validi, ad esempio le interruzioni di riga (ritorno a capo). valore intero di Hello deve essere una riga lunga. Dopo il testo Hello è riportato un esempio del certificato hello:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Errore del portale di Azure: Impossibile gateway VPN di toosave hello e nome risorsa hello non valido

### <a name="symptom"></a>Sintomo

Quando si tenta di modifiche hello toosave per il gateway VPN hello in hello portale di Azure, viene visualizzato hello seguente messaggio di errore: 

**Gateway di rete virtuale non riuscita toosave &lt;* nome del gateway*&gt;. Nome della risorsa &lt; *nome certificato si tenta di tooupload* &gt; è valido * *.

### <a name="cause"></a>Causa

Questo problema si verifica perché il nome di hello del certificato hello contiene un carattere non valido, ad esempio uno spazio. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Errore del portale di Azure: VPN package file download error 503 (Errore 503 relativo al download del file del pacchetto VPN)

### <a name="symptom"></a>Sintomo

Quando si tenta di pacchetto di configurazione client VPN hello toodownload, viene visualizzato hello seguente messaggio di errore:

**Nel file hello toodownload non riuscita. Dettagli errore: errore 503. Hello server è occupato.**
 
### <a name="solution"></a>Soluzione

Questo errore può essere causato da un problema di rete temporaneo. Riprovare pacchetto VPN di hello toodownload dopo alcuni minuti.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Aggiornamento di Gateway VPN di Azure: client P2S tutti sono tooconnect Impossibile

### <a name="cause"></a>Causa

Se il certificato di hello è più del 50% tramite la relativa durata, il certificato di hello venga eseguito il rollover.

### <a name="solution"></a>Soluzione

tooresolve questo problema, creare e ridistribuire i nuovi certificati toohello VPN client. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Troppi client VPN connessi contemporaneamente

Per ogni gateway VPN, numero massimo di hello di connessioni consentite è 128. È possibile visualizzare numero totale di hello di client connessi in hello portale di Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Point-to-site VPN aggiunge in modo non corretto di una route per tabella di route toohello 10.0.0.0/8

### <a name="symptom"></a>Sintomo

Quando si effettua la connessione VPN nel client point-to-site hello hello, i client VPN hello deve aggiungere una route verso hello rete virtuale di Azure. servizio di supporto IP Hello deve aggiungere una route per la subnet hello del client VPN hello. 

intervallo di client VPN Hello appartiene tooa subnet più piccole di 10.0.0.0/8, ad esempio 10.0.12.0/24. Invece di una route per 10.0.12.0/24, viene aggiunta una route per 10.0.0.0/8 con priorità più alta. 

Questa route non corretta viene interrotta la connettività con altre reti locali che potrebbe appartenere a subnet tooanother nell'intervallo 10.0.0.0/8 hello, ad esempio 10.50.0.0/24, che non dispongono di una route specifica definita. 

### <a name="cause"></a>Causa

Questo è il comportamento da progettazione per i client Windows. Quando il client di hello Usa protocollo PPP IPCP hello, ottenuta indirizzo IP hello interfaccia tunnel hello dal server hello (gateway VPN di hello in questo caso). Tuttavia, a causa di restrizioni nel protocollo hello, client hello è la subnet mask di hello. Poiché non esiste alcun altro tooget modo, client hello tenta tooguess hello la subnet mask basata sulla classe hello di indirizzo IP dell'interfaccia tunnel hello. 

Pertanto, viene aggiunta una route in base a hello dopo un mapping statico: 

Se l'indirizzo appartiene A tooclass--> applicare valore/8

Se l'indirizzo appartiene tooclass--> B applicare /16

Se l'indirizzo appartiene tooclass--> C applicare /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>Il client VPN non riesce ad accedere alle condivisioni file di rete

### <a name="symptom"></a>Sintomo

client VPN Hello è connesso toohello rete virtuale di Azure. Client hello tuttavia non è possibile accedere a condivisioni di rete.

### <a name="cause"></a>Causa

protocollo SMB Hello viene utilizzato per l'accesso alla condivisione file. Quando viene avviata la connessione hello, client VPN hello aggiunge credenziali sessione hello e si verifica un errore di hello. Dopo aver stabilita la connessione hello, hello client deve le credenziali nella cache di hello toouse per l'autenticazione Kerberos. Questo processo viene avviato query toohello Centro distribuzione chiavi (un controller di dominio) tooget un token. Poiché client hello si connette da hello Internet, potrebbe non essere in grado di tooreach controller di dominio hello. Pertanto, client hello possibile eseguire il failover da tooNTLM Kerberos. 

Hello solo ora, tale client hello è richiesto per una credenziale è quando si dispone di un certificato valido (con SAN = UPN) rilasciato da toowhich dominio hello viene unita in join. client Hello deve essere connessa fisicamente toohello rete di dominio. In questo caso, i client hello tenta certificato hello toouse e raggiunge toohello controller di dominio. Restituirà un errore di "KDC_ERR_C_PRINCIPAL_UNKNOWN" hello Centro distribuzione chiavi. client hello è forzato toofail su tooNTLM. 

### <a name="solution"></a>Soluzione

toowork problema hello, disabilitare la memorizzazione nella cache di hello delle credenziali di dominio da hello seguente sottochiave del Registro di sistema: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Impossibile trovare la connessione VPN point-to-site di hello in Windows dopo la reinstallazione di client VPN hello

### <a name="symptom"></a>Sintomo

Rimuovere la connessione VPN point-to-site di hello e quindi reinstallare i client VPN hello. In questo caso, hello connessione VPN non è configurato correttamente. Non è presente connessione VPN hello in hello **connessioni di rete** impostazioni di Windows.

### <a name="solution"></a>Soluzione

problema di hello tooresolve, delete hello precedente VPN client i file di configurazione **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, quindi eseguire nuovamente il programma di installazione di hello VPN client.
