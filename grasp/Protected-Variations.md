### Protected Variations (Защищенные вариации)

###### Защита от изменений с помощью создания стабильных интерфейсов, которые изолируют части системы.

```
Представьте себе, что вы строите дом на берегу моря. 
Для защиты дома от возможных ураганов и штормов, 
вы устанавливаете прочные стены и окна. 
Эти стены и окна действуют как барьер, 
защищая внутренние помещения от внешних изменений, 
вызванных погодой. Подобным образом в программировании, 
стабильные интерфейсы изолируют различные части системы от изменений, 
создавая защитные барьеры, 
которые обеспечивают устойчивость и надежность всей системы.
```

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
