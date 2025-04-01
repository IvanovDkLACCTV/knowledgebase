
## MVC (Model-View-Controller) модель

### Основные компоненты MVC:

1. **Model** - содержит данные и бизнес-логику
    
2. **View** - отвечает за отображение данных пользователю
    
3. **Controller** - обрабатывает пользовательский ввод, управляет потоком данных между Model и View
    

### Как работает MVC:

1. Пользователь взаимодействует с View (например, нажимает кнопку)
    
2. View передаёт действие Controller'у
    
3. Controller обрабатывает запрос, возможно изменяя Model
    
4. Model уведомляет View об изменениях
    
5. View обновляется, отражая изменения в Model

## MCP (Model-Controller-Presenter) модель

MCP (Model-Controller-Presenter) - это архитектурный паттерн, похожий на MVC, но с некоторыми отличиями в распределении ответственностей. Давайте разберём его работу и реализацию в разных технологиях.
### Основные компоненты MCP:

1. **Model** - так же содержит данные и бизнес-логику (аналогично MVC)
    
2. **Controller** - обрабатывает входящие запросы, но не управляет представлением
    
3. **Presenter** - подготавливает данные для View и управляет логикой представления

### Ключевые отличия от MVC:

1. **Presenter вместо View**:
    
    - В MVC View пассивно отображает данные
        
    - В MCP Presenter активно управляет тем, как данные представляются
        
    - Presenter содержит логику преобразования данных для отображения
        
2. **Разделение ответственности**:
    
    - В MVC View может напрямую обращаться к Model
        
    - В MCP Presenter является единственным посредником между Model и View
        
3. **Тестируемость**:
    
    - Presenter легче тестировать, так как он не зависит от UI-фреймворка
        
    - В MVC логика представления часто смешана с View, что усложняет тестирование

## Сравнительная таблица MVC и MCP

|Аспект|MVC|MCP|
|---|---|---|
|Компонент отображения|View (пассивный)|Presenter (активный)|
|Связь с данными|View может читать Model|Presenter управляет данными для отображения|
|Логика представления|Часто в View|В Presenter|
|Тестируемость|Сложнее (из-за связи View-Model)|Легче (Presenter изолирован)|
|Подходит для|Простых приложений|Сложных приложений с комплексным представлением данных|

## Когда использовать MCP вместо MVC

MCP предпочтительнее, когда:

1. Требуется сложная обработка данных перед отображением
    
2. Необходимо поддерживать несколько представлений одних и тех же данных
    
3. Важна высокая тестируемость компонентов представления
    
4. Нужно четко разделить логику представления от бизнес-логики
    

MVC проще и подходит для:

1. Быстрой разработки простых приложений
    
2. Случаев, когда не требуется сложная трансформация данных для отображения
    
3. Проектов с малым количеством вариантов представления данных
    

## Вывод

MCP - это эволюция MVC, предлагающая более строгое разделение ответственности, особенно в части представления данных. Presenter в MCP берёт на себя задачи, которые в MVC часто распределены между Controller и View, что делает архитектуру более чистой и поддерживаемой для сложных проектов.

### Пример MCP в React Native:

```javascript


// Model (аналогично MVC)
class UserModel {
  constructor() {
    this.users = [];
  }

  addUser(user) {
    this.users.push(user);
    return this.users;
  }
}

// Controller
class UserController {
  constructor(model) {
    this.model = model;
  }

  addUser(user) {
    return this.model.addUser(user);
  }
}

// Presenter
const UserPresenter = ({ controller }) => {
  const [users, setUsers] = useState([]);
  const [input, setInput] = useState('');

  const handleAddUser = () => {
    const newUsers = controller.addUser({ name: input });
    setUsers(newUsers);
    setInput('');
  };

  const formattedUsers = users.map(user => ({
    ...user,
    name: user.name.toUpperCase(),
    createdAt: new Date().toLocaleString()
  }));

  return (
    <View>
      <TextInput value={input} onChangeText={setInput} />
      <Button title="Add User" onPress={handleAddUser} />
      <FlatList
        data={formattedUsers}
        renderItem={({ item }) => (
          <Text>{item.name} - created at {item.createdAt}</Text>
        )}
      />
    </View>
  );
};
```

### Пример MVC в React Native:

```javascript

// Model
class CounterModel {
  constructor() {
    this.value = 0;
    this.listeners = [];
  }

  increment() {
    this.value++;
    this.notify();
  }

  addListener(listener) {
    this.listeners.push(listener);
  }

  notify() {
    this.listeners.forEach(listener => listener(this.value));
  }
}

// View
const CounterView = ({ value, onIncrement }) => (
  <View>
    <Text>Value: {value}</Text>
    <Button title="Increment" onPress={onIncrement} />
  </View>
);

// Controller
class CounterController {
  constructor(model) {
    this.model = model;
  }

  handleIncrement() {
    this.model.increment();
  }
}

// Связывание компонентов
const model = new CounterModel();
const controller = new CounterController(model);
const App = () => {
  const [value, setValue] = useState(0);
  
  useEffect(() => {
    model.addListener(setValue);
  }, []);

  return (
    <CounterView 
      value={value} 
      onIncrement={() => controller.handleIncrement()} 
    />
  );
};  ```