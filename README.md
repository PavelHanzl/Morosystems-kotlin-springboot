# Morosystems: Spring Boot App

Tento projekt monitorovuje využití paměti klientů. Zahrnuje backend server Spring boot, PostgreSQL databázi, dva Spring Boot klienty a frontend aplikaci v Reactu.

## Popis

- **Server a Databáze**: Po spuštění pomocí Docker Compose se vytvoří server (port 443) s integrovanou PostgreSQL databází (port 5432).
- **Klienti**: Vytvoří se dva klienti (porty 8081 a 8082) z jednoho Docker obrazu. Tito klienti se připojují k serveru pomocí WebSockets zabezpečených TLS (s self-signed certifikátem) a periodicky odesílají data o využití paměti na server.
- **Frontend Aplikace**: Jednoduchá React aplikace s Bootstrapem (přístupná na localhost:3000) pro výpis a filtrování dat získaných ze serveru z REST api endpointu (localhost:443/api/data).

## Funkce

- Simulace využití paměti v klientech.
- Automatické opětovné připojení klientů při neočekávaném přerušení.
- Dynamické filtrování dat v React aplikaci.

## Lokální Spuštění

Projekt je možné spustit z Dockeru, ale jsou zde přidány také podmínky pro správné fungování v případě lokálního spuštění.

## Docker Spuštění

### Příprava
- **Gradlew Soubor**: Pro správné spuštění v Dockeru může být třeba upravit konec řádků v souboru `gradlew` v root adresářích Spring Boot aplikací sysinfoclient a sysinfoserver. Použijte následující příkaz v PowerShell:

  ```powershell
  (Get-Content -Raw gradlew) -replace "`r`n", "`n" | Set-Content gradlew

- **NPM Instalace**:
Pokud se po provedení```docker compose up```
nepodaří spustit react frontend aplikaci a objeví se v konzoli chybovoá hláška 
```sh: 1: react-scripts: not found```

    Bude potřeba v root složce frontend-app provést příkaz:

    ```bash
    npm i react-scripts
    ```

### Spuštění
Nyní by již nemělo nic bránit spustit projekt v Dockeru včetně všech jeho kontejnerů.

Pro spuštění projektu v Dockeru použijte příkaz:

```bash
docker-compose up
```