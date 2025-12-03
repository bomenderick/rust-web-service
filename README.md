# rust-web-service
Rust RESTful API with Axum, Sqlx, Postgres, Redis, and more..

## Installation

Start by cloning the repository and navigating into it:
```bash
git clone https://github.com/bomenderick/rust-web-service.git
cd rust-web-service
```

Make sure to update the `.env` file to reflect your database credentials. If you do not have a database set up, follow this guide:

### Install Redis (for caching)
```bash
sudo pacman -S redis
sudo systemctl start redis
sudo systemctl enable redis # Auto-start Redis on boot
redis-cli ping # Check if Redis is running
```

### Install PostgreSQL
```bash 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
sudo pacman -S postgresql
sudo -iu postgres initdb -D /var/lib/postgres/data # Initialize database
sudo systemctl start postgresql
sudo systemctl enable postgresql # Auto-start PostgreSQL on boot
```

### Create a Database and User
```bash
sudo -iu postgres psql # Open PostgreSQL as superuser
```

```sql
SELECT usename FROM pg_user; -- Show existing users
CREATE USER myuser WITH PASSWORD 'mypassword'; -- Create a new user

\l -- List databases
CREATE DATABASE mydb OWNER myuser; -- Create a database

\c mydb -- Connect to the database
SELECT nspname, pg_catalog.pg_get_userbyid(nspowner) FROM pg_catalog.pg_namespace WHERE nspname = 'public'; -- Check database permissions
ALTER SCHEMA public OWNER TO myuser; -- Assign ownership to myuser

ALTER USER myuser WITH SUPERUSER; -- Grant superuser privileges (optional)

exit
```

### Run the Application
```bash
cargo run
```

You should see:
```
2025-12-03T22:24:24.779778Z  INFO rust_web_service: Connecting to pg: postgresql://rust:rust@localhost:5432/rustdb
2025-12-03T22:24:24.781145Z  INFO rust_web_service: Connecting to cache: redis://localhost:6389
2025-12-03T22:24:24.945507Z DEBUG rust_web_service: listening on 127.0.0.1:3000
```

### Test the API
Et voila ! You can now visit http://127.0.0.1:3000/swagger-ui/ to interact with the API.
