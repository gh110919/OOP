### Indirection (Опосредствование)

###### Введение посредника для уменьшения прямой связанности между классами или компонентами.

```
Представьте себе транспортную систему с пересадочными станциями. 
Вместо того, чтобы каждая автобусная линия проходила через все районы города, 
есть центральная пересадочная станция, 
где пассажиры могут пересесть на другие маршруты. 
Это уменьшает количество прямых линий и делает систему более управляемой. 
Таким образом, посредник (пересадочная станция) 
помогает уменьшить прямую связанность между разными маршрутами, 
делая всю транспортную сеть более гибкой и эффективной.
```

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

/* 
Здесь DataAccessLayer служит посредником между кодом 
и базой данных, уменьшая прямую связанность. 
*/
```
