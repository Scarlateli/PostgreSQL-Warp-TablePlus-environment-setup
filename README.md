# postgresql-warp-tableplus

macOS local environment to practice SQL end-to-end with **PostgreSQL**, **Warp** (terminal) and **TablePlus** (GUI).  
Scope: from **data modeling → schema → tables → views → functions → queries** in a realistic local setup.

> Tools: PostgreSQL 14+, Warp Terminal, TablePlus (macOS)

## Quick start (macOS, Homebrew)
```bash
brew install postgresql@14
brew services start postgresql@14
createdb meu_teste
psql meu_teste
```

## Setup

### 1. Install PostgreSQL
```bash
brew install postgresql@14
brew services start postgresql@14
```

### 2. Create test database
```bash
createdb meu_teste
```

### 3. Connect with psql
```bash
psql meu_teste
```

### 4. Install TablePlus (GUI)
Download from [TablePlus website](https://tableplus.com/) or:
```bash
brew install --cask tableplus
```

## Connection Details
- **Host**: localhost
- **Port**: 5432
- **Database**: meu_teste
- **User**: your macOS username
- **Password**: (usually none for local setup)

## Practice Areas

### Data Modeling
- Entity-relationship design
- Normalization
- Primary/foreign keys

### Schema & Tables
```sql
CREATE SCHEMA practice;
CREATE TABLE practice.users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Views
```sql
CREATE VIEW practice.active_users AS
SELECT * FROM practice.users
WHERE created_at > CURRENT_DATE - INTERVAL '30 days';
```

### Functions
```sql
CREATE OR REPLACE FUNCTION practice.get_user_count()
RETURNS INTEGER AS $$
BEGIN
    RETURN (SELECT COUNT(*) FROM practice.users);
END;
$$ LANGUAGE plpgsql;
```

## Useful Commands

### psql commands
```sql
\l          -- list databases
\c dbname   -- connect to database
\dt         -- list tables
\d table    -- describe table
\q          -- quit
```

### Common queries
```sql
-- Basic CRUD
INSERT INTO practice.users (name, email) VALUES ('João', 'joao@example.com');
SELECT * FROM practice.users;
UPDATE practice.users SET name = 'João Silva' WHERE id = 1;
DELETE FROM practice.users WHERE id = 1;
```

## Resources
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQL Tutorial](https://www.w3schools.com/sql/)
- [TablePlus Documentation](https://docs.tableplus.com/)