# The Quaoar Case

Questo documento riassume l'attività di **Penetration Testing** di tipo Black Box condotta sulla macchina virtuale vulnerabile *Quaoar*. L'analisi è stata svolta come progetto per il corso di **Penetration Testing and Ethical Hacking (PTEH)** (Anno Accademico 2025/2026).

## Sintesi dell'Analisi

L'obiettivo dell'analisi è stato quello di simulare un attacco reale partendo da zero conoscenze dell'infrastruttura bersaglio, al fine di individuarne le debolezze architetturali, sfruttarle per ottenere l'accesso e, infine, elevare i privilegi per arrivare a comprometterla integralmente (root).

L'intera *Kill Chain* ha sfruttato una serie di gravi misconfigurazioni, evidenziando la totale mancanza di pratiche di *hardening* di base:

1. **Enumerazione e Vulnerability Mapping:** È stata individuata un'installazione di **WordPress** esposta in rete.
2. **Target Exploitation:** L'accesso al pannello di amministrazione del CMS è stato garantito dall'utilizzo di credenziali di default (`admin:admin`).
3. **Esecuzione di Codice Remoto (RCE):** Sfruttando la funzionalità *Theme Editor* attiva su WordPress, è stato iniettato un payload malevolo (Reverse Shell in PHP) all'interno del file `header.php`. Questo ha permesso di ottenere un primo accesso alla macchina con privilegi limitati (`www-data`).
4. **Privilege Escalation:** Durante l'esplorazione del sistema (Post-Exploitation), è stata rilevata la conservazione in chiaro delle password nei file di configurazione web. A causa della critica pratica del *password reuse*, la stessa password del database (`rootpassword!`) è risultata essere anche la password dell'account di sistema `root`, consentendo la totale acquisizione dei privilegi massimi.

## Remediation

Le raccomandazioni primarie emerse dal test includono:
- Rimozione tempestiva delle credenziali di default e applicazione di policy rigide per le password (divieto assoluto di password reuse tra DB e sistema).
- Hardening del CMS (disattivazione del *Theme Editor* dal `wp-config.php`).
- Aggiornamento sistematico e patching dei servizi obsoleti esposti dalla macchina.
- Disabilitazione dell'accesso SSH diretto per l'utente root.

---

**Autore:**  
Choaib Goumri 
*Università degli Studi di Salerno 


