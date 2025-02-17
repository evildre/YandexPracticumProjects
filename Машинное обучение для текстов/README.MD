## Проект: Модерация комментариев для интернет-магазина

### Описание задачи
Интернет-магазин «Викишоп» запустил сервис, позволяющий пользователям редактировать и дополнять описания товаров. Для эффективной модерации создан инструмент, который классифицирует комментарии на токсичные и нетоксичные. Основная метрика качества модели — F1, с минимальным требованием > 0.75.

### Использованные данные
Данные о комментариях включают:
- Текст комментария.
- Метку (`toxic`): 1 — токсичный, 0 — нетоксичный.

#### Основные характеристики датасета:
- Количество записей: 159,281.
- Пропуски: отсутствуют.
- Средняя длина комментария: 367 символов.
- Медианная длина: 190 символов.
- Количество токсичных комментариев: 16,185 (10%).
- Количество нетоксичных комментариев: 143,096 (90%).

### Этапы работы

1. **Предобработка данных:**
   - Удалены символы, не принадлежащие английскому алфавиту.
   - Приведение текста к нижнему регистру.
   - Токенизация и лемматизация текста.
   - Удалены комментарии длиной 0 символов.
   - Данные разделены на тренировочную (80%), валидационную (10%) и тестовую (10%) выборки.

2. **Обучение моделей:**
   - **Логистическая регрессия:**
     - Использованы методы векторизации: BOW и TF-IDF.
     - Метрика F1: ~0.78.
   - **CatBoost:**
     - Включен встроенный предобработчик текста.
     - Лучшая метрика F1: ~0.78 на валидационной выборке.
   - **LightGBM:**
     - Использованы аналогичные методы векторизации.
     - Метрика F1: ~0.76.

3. **Использование BERT:**
   - Модель `unitary/toxic-bert` от Google.
   - Предобработаны данные: удалены тексты длиной > 512 символов.
   - Обучена логистическая регрессия на эмбеддингах BERT.
   - Достигнута метрика F1 > 0.9 на тестовой выборке.

### Итоги
- **Лучшая модель:** BERT с логистической регрессией.
- **Метрика F1:** > 0.9.
- **Рекомендация:** Использовать модель на основе BERT для классификации токсичных комментариев.

### Вывод
Модель BERT показала превосходные результаты, значительно превышающие минимальные требования по метрике F1. Данный инструмент рекомендуется для внедрения в сервис модерации интернет-магазина «Викишоп».

