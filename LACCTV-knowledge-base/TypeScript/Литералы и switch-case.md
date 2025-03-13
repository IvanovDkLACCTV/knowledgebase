Вот пример использования **литеральных типов** с конструкцией `switch-case` в TypeScript. Этот код иллюстрирует проверку различных вариантов и гарантирует, что все возможные значения охвачены:

### 📊 **Пример: Управление статусами заказа**

```typescript
type OrderStatus = "pending" | "shipped" | "delivered" | "cancelled";

function processOrder(status: OrderStatus): void {
  switch (status) {
    case "pending":
      console.log("Заказ ожидает обработки.");
      break;
    case "shipped":
      console.log("Заказ отправлен.");
      break;
    case "delivered":
      console.log("Заказ доставлен.");
      break;
    case "cancelled":
      console.log("Заказ отменён.");
      break;
    default:
      // Этот блок никогда не выполнится, если тип OrderStatus корректен.
      const _exhaustiveCheck: never = status;
      throw new Error(`Неизвестный статус: ${status}`);
  }
}

processOrder("shipped");    // ✅ Вывод: Заказ отправлен.
processOrder("cancelled");  // ✅ Вывод: Заказ отменён.
// processOrder("unknown"); // ❌ Ошибка: Тип '"unknown"' не соответствует типу 'OrderStatus'.
```

---

### 🔍 **Разбор кода:**

1. **Литеральный тип `OrderStatus`** ограничивает возможные значения.
2. **Конструкция `switch-case`** проверяет каждое значение.
3. **Защита `default` с `never`**:
    - Используем `never` для проверки **исчерпывающего охвата** (exhaustiveness check).
    - Если добавится новый статус, TypeScript выдаст ошибку, если его не обработать.

---

### 📦 **Почему это полезно?**

- ✅ Гарантирует, что **все варианты** охвачены.
- ✅ Если появится новый статус, TypeScript напомнит, что нужно обновить `switch`.
- ✅ Улучшает **типобезопасность** и предотвращает ошибки.