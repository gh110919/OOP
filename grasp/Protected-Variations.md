### Protected Variations (Защищенные вариации)

###### Защита от изменений с помощью создания стабильных интерфейсов, которые изолируют части системы.

```ts
interface Database {
  query(sql: string): void;
}

class MySQLDatabase implements Database {
  query(sql: string): void {
    // Логика MySQL-запроса
  }
}

class PostgreSQLDatabase implements Database {
  query(sql: string): void {
    // Логика PostgreSQL-запроса
  }
}

class DataAccessLayer {
  private database: Database;

  constructor(database: Database) {
    this.database = database;
  }

  executeQuery(sql: string): void {
    this.database.query(sql);
  }
}

const mysqlDatabase = new MySQLDatabase();
const dataAccessLayer = new DataAccessLayer(mysqlDatabase);
dataAccessLayer.executeQuery("SELECT * FROM users");

// Позднее можем заменить MySQL на PostgreSQL, не изменяя DataAccessLayer
const postgreSQLDatabase = new PostgreSQLDatabase();
const newDataAccessLayer = new DataAccessLayer(postgreSQLDatabase);
newDataAccessLayer.executeQuery("SELECT * FROM products");

/* Здесь интерфейс Database защищает DataAccessLayer от изменений конкретных реализаций базы данных. */
```
