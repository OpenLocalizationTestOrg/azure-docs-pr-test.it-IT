---
title: "Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni | Documentazione Microsoft"
description: "In questo argomento vengono descritte le attività operative per la sincronizzazione di Azure AD Connect e come tooprepare per l'uso di questo componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni
obiettivo di Hello di questo argomento è toodescribe attività operative per la sincronizzazione di Azure AD Connect.

## <a name="staging-mode"></a>Modalità di gestione temporanea
La modalità di gestione temporanea può essere usata per diversi scenari, ad esempio:

* Disponibilità elevata.
* Testare e distribuire le nuove modifiche della configurazione.
* Introduce un nuovo server e rimuovere le autorizzazioni hello precedente.

Con un server in modalità di gestione temporanea, è possibile apportare modifiche toohello configurazione e anteprima hello modifiche prima di apportare active server hello. Consente inoltre importazione completa toorun e tooverify sincronizzazione completa che tutte le modifiche sono previsti prima di apportare queste modifiche nell'ambiente di produzione.

Durante l'installazione, è possibile selezionare hello server toobe in **modalità di gestione temporanea**. Questa azione rende attivo per l'importazione e la sincronizzazione server hello, ma non esegue alcuna esportazione. Un server in modalità di gestione temporanea non eseguirà la sincronizzazione o il writeback delle password, anche se queste funzionalità sono state selezionate durante l'installazione. Quando si disattiva modalità di staging, hello server avvia l'esportazione, consente la sincronizzazione della password e abilita il writeback delle password.

È comunque possibile forzare un'esportazione utilizzando Gestione servizio di sincronizzazione hello.

Un server in modalità di gestione temporanea continua tooreceive modifiche da Active Directory e Azure AD. Include sempre una copia delle modifiche più recenti di hello e può essere molto veloci take su responsabilità hello di un altro server. Se si apportano server primario tooyour modifiche di configurazione, è la responsabilità toomake hello allo stesso server di toohello di modifiche nella modalità di gestione temporanea.

Per coloro con conoscenza delle tecnologie di sincronizzazione precedenti, hello in modalità di gestione temporanea è diverso dal server hello dispone del proprio database SQL. Questa architettura consente hello modalità server toobe che si trova in un altro Data Center di gestione temporanea.

### <a name="verify-hello-configuration-of-a-server"></a>Verificare la configurazione di un server hello
tooapply questo metodo, seguire questi passaggi:

1. [Preparare](#prepare)
2. [Configurazione](#configuration)
3. [Importare e sincronizzare](#import-and-synchronize)
4. [Verificare](#verify)
5. [Cambiare il server attivo](#switch-active-server)

#### <a name="prepare"></a>Preparazione
1. Installare Azure AD Connect, selezionare **modalità di gestione temporanea**e deselezionare **avviare la sincronizzazione** hello ultima pagina nell'installazione guidata di hello. Questa modalità consente di motore di sincronizzazione hello toorun manualmente.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Accesso disattivato/sign in e da hello avviare menu selezionare **servizio di sincronizzazione**.

#### <a name="configuration"></a>Configurazione
Se sono state apportate modifiche personalizzate toohello primario configurazione server e si desidera toocompare hello con hello server di gestione temporanea, quindi utilizzare [analizzatore di configurazione di Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importare e sincronizzare
1. Selezionare **connettori**, e selezionare hello primo connettore con tipo di hello **servizi di dominio Active Directory**. Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**. Eseguire questi passaggi per tutti i connettori di questo tipo.
2. Seleziona hello connettore con tipo **Azure Active Directory (Microsoft)**. Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**.
3. Verificare che sia ancora selezionata la scheda hello connettori. Per ogni connettore con il tipo **Active Directory Domain Services** fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e fare clic su **OK**.
4. Seleziona hello connettore con tipo **Azure Active Directory (Microsoft)**. Fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e quindi fare clic su **OK**.

È ora esportazione staging cambia tooAzure Active Directory e AD locale (se si utilizza distribuzione ibrida di Exchange). passaggi successivi Hello consentono tooinspect Novità sulla toochange prima di avviare effettivamente directory toohello di esportazione hello.

#### <a name="verify"></a>Verificare
1. Avviare un prompt dei comandi e passare troppo`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Esegui: `csexport "Name of Connector" %temp%\export.xml /f:x` nome hello del connettore hello è reperibile nel servizio di sincronizzazione. Include un too"contoso.com simile nome-AAD" per Azure AD.
3. Copiare uno script di PowerShell hello dalla sezione hello [CSAnalyzer](#appendix-csanalyzer) tooa file denominato `csanalyzer.ps1`.
4. Aprire una finestra di PowerShell e Sfoglia cartella toohello in cui è stato creato uno script di PowerShell hello.
5. Eseguire: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. A questo punto si avrà un file denominato **processedusers1.csv**, che può essere esaminato in Microsoft Excel. Tutte le modifiche inserite toobe esportato tooAzure Active Directory sono riportati in questo file.
7. Apportare le modifiche necessarie toohello dati o configurazione ed eseguire questi passaggi nuovamente (importazione e sincronizzazione e verifica) finché non sono previste modifiche che stanno toobe esportato hello.

#### <a name="switch-active-server"></a>Cambiare il server attivo
1. Nel server attualmente attivo hello, disattivare il server di hello (DirSync/FIM/Azure AD Sync) in modo che non viene esportato tooAzure AD o impostare il valore nella modalità (Azure AD Connect) di gestione temporanea.
2. Eseguire l'installazione guidata di hello in server hello **modalità di gestione temporanea** e disabilitare **modalità di gestione temporanea**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Ripristino di emergenza
Parte della progettazione dell'implementazione di hello è tooplan per quali toodo in caso di emergenza in cui si perde il server di sincronizzazione hello. Sono disponibili diversi modelli toouse e quale uno toouse dipende da diversi fattori tra cui:

* Che cos'è la tolleranza per non è in grado di apportare le modifiche tooobjects in Azure AD durante i tempi di inattività hello?
* Se si utilizza la sincronizzazione delle password, gli utenti di hello intendesse che hanno una password hello toouse in Azure AD nel caso in cui modificarlo locale?
* Si ha una dipendenza dalle operazioni in tempo reale, ad esempio il writeback delle password?

A seconda hello risposte toothese domande e i criteri dell'organizzazione, una delle seguenti strategie hello può essere implementata:

* Ricompilare quando necessario.
* Avere un server di standby di riserva, ovvero in **modalità di gestione temporanea**.
* Usare macchine virtuali.

Se non si utilizza il database di SQL Express incorporati di hello, quindi è inoltre consigliabile esaminare hello [la disponibilità elevata SQL](#sql-high-availability) sezione.

### <a name="rebuild-when-needed"></a>Ricompilare quando necessario
Una strategia valida è tooplan per una ricompilazione di server, quando necessario. In genere, l'installazione di hello motore di sincronizzazione e hello importazione iniziale e la sincronizzazione può essere completata entro alcune ore. Se non esiste un server di riserva non è disponibile, è possibile tootemporarily utilizzare un motore di sincronizzazione hello toohost controller di dominio.

server del motore di sincronizzazione Hello non archivia qualsiasi stato sugli oggetti hello in modo è possibile ricompilare il database di hello dai dati hello in Active Directory e Azure AD. Hello **sourceAnchor** attributo è usato toojoin hello oggetti locale e cloud hello. Se si ricompila hello cloud, quindi il motore di sincronizzazione hello associa gli oggetti insieme nuovamente su reinstallazione hello server con gli oggetti locali esistenti. gli aspetti di Hello è necessario toodocument e salvare sono hello apportate alla configurazione server toohello, ad esempio le regole di filtro e la sincronizzazione. Queste configurazioni personalizzate dovranno essere riapplicate prima di avviare la sincronizzazione.

### <a name="have-a-spare-standby-server---staging-mode"></a>Avere un server di standby di riserva, in modalità di gestione temporanea
Nel caso di un ambiente più complesso, è consigliabile avere uno o più server di standby. Durante l'installazione, è possibile abilitare un server toobe in **modalità di gestione temporanea**.

Per altre informazioni, vedere le [modalità di gestione temporanea](#staging-mode).

### <a name="use-virtual-machines"></a>Usare macchine virtuali
Un metodo comune e supportato è di tipo motore di sincronizzazione toorun hello in una macchina virtuale. Nel caso in cui hello host dispone di un problema, immagine di hello con server hello del motore di sincronizzazione può essere migrato tooanother server.

### <a name="sql-high-availability"></a>Disponibilità elevata di SQL
Se non si utilizza SQL Server Express con Azure AD Connect hello, disponibilità elevata per SQL Server deve inoltre essere considerata. soluzioni a disponibilità elevata Hello supportate includono il clustering di SQL e AOA (gruppi di disponibilità AlwaysOn). mentre il mirroring è una delle soluzioni non supportate.

È stato aggiunto il supporto per SQL AOA tooAzure AD Connect versione 1.1.524.0. È necessario abilitare SQL AOA prima di installare Azure AD Connect. Durante l'installazione, Azure AD Connect rileva se istanza SQL hello fornita è abilitato per SQL AOA o meno. Se SQL AOA è abilitata, Azure AD Connect ulteriormente determina se SQL AOA è toouse configurato di replica sincrona o asincrona. Quando si configurano hello listener del gruppo di disponibilità, è consigliabile impostare hello RegisterAllProvidersIP proprietà too0. In questo modo Azure AD Connect utilizza attualmente tooSQL tooconnect SQL Native Client e SQL Native Client non supporta l'utilizzo di hello della proprietà MultiSubNetFailover.

## <a name="appendix-csanalyzer"></a>Appendice CSAnalyzer
Vedere la sezione hello [verificare](#verify) sulla toouse questo script.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**  

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)  
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)  
