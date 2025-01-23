### Indirection (Опосредствование)

###### Введение посредника для уменьшения прямой связанности между классами или компонентами.

```ts
class Database {
  query(sql: string) {
    // Выполнение запроса
  }
}

class DataAccessLayer {
  private database: Database;

  constructor(database: Database) {
    this.database = database;
  }

  executeQuery(sql: string) {
    this.database.query(sql);
  }
}

const database = new Database();
const dataAccessLayer = new DataAccessLayer(database);
dataAccessLayer.executeQuery("SELECT * FROM users");

/* Здесь DataAccessLayer служит посредником между кодом и базой данных, уменьшая прямую связанность. */
```
