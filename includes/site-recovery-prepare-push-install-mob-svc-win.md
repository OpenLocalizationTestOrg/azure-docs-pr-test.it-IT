### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Preparare un'installazione push in un computer Windows

1. Verificare che vi sia connettività di rete tra il computer di Windows hello e server di elaborazione hello.
2. Creare un account di che tale server di elaborazione hello può usare computer hello tooaccess. Hello account deve disporre dei diritti di amministratore (locale o dominio). (Utilizzare questo account solo per l'installazione push hello e per gli aggiornamenti dell'agente).

   > [!NOTE]
   > Se non si utilizza un account di dominio, disattivare il controllo di accesso remoto nel computer locale hello. controllo di accesso remoto, nella chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System hello toodisable aggiungere un nuovo valore DWORD: **LocalAccountTokenFilterPolicy**. Impostare il valore di hello troppo**1**. toodo in un comando su richiesta, eseguire hello comando seguente:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. In Windows Firewall nel computer di hello desiderato tooprotect, selezionare **Consenti app o funzionalità attraverso Firewall**. Abilitare **Condivisione file e stampanti** e **Strumentazione gestione Windows (WMI)**. Per i computer appartenenti al dominio tooa, è possibile configurare le impostazioni del firewall hello utilizzando un oggetto Criteri di gruppo (GPO).

   ![Impostazioni del firewall](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Aggiungere account hello creati in CSPSConfigtool.
    1.  Accedi a server di configurazione tooyour.
    2.  Aprire **cspsconfigtool.exe**. (È disponibile come collegamento sul desktop hello e nella cartella %ProgramData%\home\svsystems\bin hello.)
    3.  In hello **Gestisci account** , selezionare **Aggiungi Account**.
    4.  Aggiungere account hello creato.
    5.  Immettere le credenziali di hello che è utilizzare quando si abilita la replica per un computer.
