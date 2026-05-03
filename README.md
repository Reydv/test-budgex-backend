# Budgex Backend

## Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/download)
- [Docker](https://docs.docker.com/get-docker/)

---

## Setup

### 1. Clone repo dari akunku

(ini sementara, nanti kalo udah di repo pdbl pake repo pdbl)

```bash
git clone https://github.com/Reydv/test-budgex-backend.git
cd test-budgex-backend
```

### 2. copy paste file example, ilangin .example nya

Isi file .env sama appsetting.json, valuenya harus sama
kalo command cp gak bisa copy paste manual aja

```bash
cp .env.example .env
cp appsettings.json.example appsettings.json
```

`.env` — credentials for the PostgreSQL container:
```
POSTGRES_PASSWORD=yourpassword
POSTGRES_USER=youruser
POSTGRES_DB=yourdb
```

`appsettings.json` — connection string for the backend, must match `.env`:
```json
{
  "ConnectionStrings": {
    "Default": "Host=localhost;Port=5432;Database=yourdb;Username=youruser;Password=yourpassword"
  }
}
```

### 3. Start the database

```bash
docker compose up -d
```

### 4. Restore dependencies

kalo gak bisa coba tambahin `-p:AllowMissingPrunePackageData=true`, di os ku ada issue itu soalnya

```bash
dotnet restore 
```

### 5. Run the backend

```bash
dotnet run
```

You should see:
```
Now listening on: http://localhost:5221
```

### 6. Validate database connection

Open your browser and go to:
```
http://localhost:5221/test-db
```

If everything is working you will see:
```
Database connected!
```

---

## Stopping the database

ini buat stop/hapus containernya, kalo aku biasanya pake portainer buat ngatur container, jadi gak bisa jamin ini bakal bisa

```bash
docker compose down
```

Your data is safe, it is saved in the Docker volume and will still be there next time you run `docker compose up -d`.