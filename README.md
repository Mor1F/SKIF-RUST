Понял! Тогда давай пошагово: **создадим базу, таблицы, заполним их данными и выполним запрос** для подсчёта сотрудников в каждом магазине в **PostgreSQL (pgAdmin)**.

---

### ✅ 1. Создание базы данных (в pgAdmin можно создать через интерфейс, но SQL тоже возможен):

```sql
CREATE DATABASE magaziny_db;
```

*После этого подключитесь к `magaziny_db` и выполните следующий код:*

---

### ✅ 2. Создание таблиц:

```sql
-- Таблица магазинов
CREATE TABLE magaziny (
    id_magazina SERIAL PRIMARY KEY,
    nazvanie VARCHAR(100) NOT NULL,
    adres VARCHAR(150)
);

-- Таблица сотрудников
CREATE TABLE sotrudniki (
    id_sotrudnika SERIAL PRIMARY KEY,
    fio VARCHAR(100) NOT NULL,
    id_magazina INT REFERENCES magaziny(id_magazina)
);
```

---

### ✅ 3. Вставка тестовых данных:

```sql
-- Добавим магазины
INSERT INTO magaziny (nazvanie, adres) VALUES
('Магнит', 'ул. Ленина, 10'),
('Пятёрочка', 'пр. Победы, 25'),
('Дикси', 'ул. Советская, 5');

-- Добавим сотрудников
INSERT INTO sotrudniki (fio, id_magazina) VALUES
('Иванов И.И.', 1),
('Петров П.П.', 1),
('Сидоров С.С.', 2);
```

---

### ✅ 4. Запрос: количество сотрудников в каждом магазине

```sql
SELECT 
    m.nazvanie,
    m.adres,
    COUNT(s.id_sotrudnika) AS kolichestvo_sotrudnikov
FROM 
    magaziny m
LEFT JOIN 
    sotrudniki s ON m.id_magazina = s.id_magazina
GROUP BY 
    m.nazvanie, m.adres;
```

---

### 🔍 Результат:

| nazvanie  | adres            | kolichestvo\_sotrudnikov |
| --------- | ---------------- | ------------------------ |
| Магнит    | ул. Ленина, 10   | 2                        |
| Пятёрочка | пр. Победы, 25   | 1                        |
| Дикси     | ул. Советская, 5 | 0                        |

---

Если нужно — могу помочь оформить всё как отчёт или .sql-файл для импорта.
