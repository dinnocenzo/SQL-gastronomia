# SQL-gastronomia

SQL queries and data analysis of gastronomy venues by neighborhood, category, and commune in Buenos Aires.

## Tech Stack

- SQL (MySQL)

## Project Structure

```
SQL-gastronomia/
├── oferta_gastronomica.sql   # Main SQL script with data fix and analytical queries
├── .gitignore
├── LICENSE
└── README.md
```

## Setup / Installation

1. Ensure you have MySQL installed and running.
2. Create or connect to a database (the script uses `test`):
   ```sql
   CREATE DATABASE IF NOT EXISTS test;
   USE test;
   ```
3. Import or create the `oferta_gastronomica` table with the relevant gastronomy data before running the queries.
4. Run the SQL script:
   ```bash
   mysql -u your_user -p test < oferta_gastronomica.sql
   ```

## Usage

The script `oferta_gastronomica.sql` contains the following operations:

### Data Fix

Corrects a character encoding issue in the `barrio` (neighborhood) column:

```sql
UPDATE oferta_gastronomica
SET barrio = 'Nuñez'
WHERE barrio = 'NuÃƒÂ±ez';
```

### Analytical Queries

**Neighborhoods with the most pubs:**
```sql
SELECT categoria, barrio, count(*) as cantidad
FROM oferta_gastronomica
GROUP BY barrio, categoria
HAVING categoria = 'PUB'
ORDER BY cantidad DESC;
```

**Venues by category:**
```sql
SELECT categoria, count(*) as cantidad
FROM oferta_gastronomica
GROUP BY categoria
ORDER BY cantidad DESC;
```

**Restaurants by commune:**
```sql
SELECT comuna, count(*) as cantidad
FROM oferta_gastronomica
GROUP BY comuna, categoria
HAVING categoria = 'RESTAURANTE'
ORDER BY cantidad DESC;
```

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
