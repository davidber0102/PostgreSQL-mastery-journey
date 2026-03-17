# PostgreSQL Mastery Journey 🚀
Libro 'Mastering PostgreSQL 13,Fourth Edition,Build, administer, and maintain database applications efficiently with PostgreSQL 13,Hans-Jürgen Schönig
Dominar PostgreSQL no es memorizar comandos. Es entender cómo piensa el motor.

Este repositorio documenta un proceso real de aprendizaje basado en práctica, optimización y casos aplicados.

---

## 🎯 Objetivo
Construir dominio sólido en PostgreSQL desde fundamentos hasta nivel avanzado, aplicando:
- Modelado de datos
- Optimización de consultas
- Administración de base de datos
- Funcionalidades avanzadas

---

## 📂 Estructura del Proyecto

```
postgresql-mastery-journey/
│
├── 01_fundamentals/
├── 02_administration/
├── 03_performance/
├── 04_advanced/
├── datasets/
└── projects/
```

---

# 01 FUNDAMENTALS

## data_types.sql
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## indexes.sql
```sql
-- Basic index
CREATE INDEX idx_users_name ON users(name);

-- Partial index
CREATE INDEX idx_users_active ON users(name)
WHERE age > 18;
```

---

# 02 ADMINISTRATION

## roles_users.sql
```sql
-- Create role
CREATE ROLE dev_user WITH LOGIN PASSWORD 'secure_password';

-- Grant privileges
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA public TO dev_user;
```

## backup_restore.sql
```sql
-- Backup (command line)
-- pg_dump -U postgres -d mydb -F c -f backup.dump

-- Restore
-- pg_restore -U postgres -d mydb backup.dump
```

---

# 03 PERFORMANCE

## explain_analyze.sql
```sql
EXPLAIN ANALYZE
SELECT * FROM users WHERE name = 'David';
```

## indexing_strategies.sql
```sql
-- Composite index
CREATE INDEX idx_users_name_age ON users(name, age);

-- GIN index for JSON
CREATE TABLE events (
    id SERIAL PRIMARY KEY,
    data JSONB
);

CREATE INDEX idx_events_data ON events USING GIN(data);
```

---

# 04 ADVANCED

## partitioning.sql
```sql
CREATE TABLE sales (
    id SERIAL,
    sale_date DATE,
    amount NUMERIC
) PARTITION BY RANGE (sale_date);

CREATE TABLE sales_2024 PARTITION OF sales
FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

## json_features.sql
```sql
SELECT data->>'name' AS name
FROM events;
```

---

# PROJECT: REAL WORLD CASE

## real_world_case.sql
```sql
-- Example GIS-like structure
CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    latitude NUMERIC,
    longitude NUMERIC,
    category VARCHAR(50),
    year INT
);

-- Index for filtering
CREATE INDEX idx_locations_category_year ON locations(category, year);

-- Query optimization
EXPLAIN ANALYZE
SELECT * FROM locations
WHERE category = 'security' AND year = 2024;
```

---

# 🧠 Filosofía

Cada archivo representa una pieza del dominio.
Cada query tiene intención.
Cada índice tiene propósito.

---

# 🔥 Siguiente paso

No te quedes aquí.
Ejecuta, rompe, optimiza… y vuelve a construir mejor.
