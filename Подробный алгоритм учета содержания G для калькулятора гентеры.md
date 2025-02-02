### **1. Учет содержания G ≥ 50%**

#### **Входные данные:**
- **Последовательность:** строка символов, например: `ACGTTGGGCCGGG`.
- **Токены, учитывающие G:**  
    В расчет включаются:
    - `G`, а также модифицированные варианты (`+G`, `mG`, `oG`, `fG`, `rG`).
- **Пороговое значение:**  
    Содержание G ≥ 50% от длины последовательности (в токенах).

#### **Алгоритм:**

1. **Считаем длину последовательности:**
    - Учитываем все токены, которые являются буквами 
      (`A`, `C`, `G`, `T`) или их модифицированными вариантами.
    - Пример:  
        Последовательность: `ACGTTG+rG/mG/CC+G`.  
        Учитываемые токены: `A, C, G, T, T, G, rG, mG, C, C, +G`.  
        **Общая длина = 11 токенов.**
2. **Считаем количество G:**
    - Учитываем все токены `G` и их модифицированные варианты:  
        `G, +G, oG, mG, fG, rG`.
    - Пример:  
        `GrGmG+G` → 4 токена.
        
3. **Вычисляем процентное содержание G:**
    - Формула:  
        **`процент G = (кол-во G / длина последовательности) × 100`**.
    - Пример:  
        **`(4 / 11) × 100 ≈ 36.36%`**
		- повышающий коэффициент не применяется.
        
4. **Применяем коэффициент:**
    - Если **процент G ≥ 50%**:
	    - применяется повышающий коэффициент `1.3`.

- Итоговая стоимость:  
    **`стоимость = базовая стоимость × коэффициент.`**

---

### **2. Учет G-повторов**

#### **Входные данные:**

- **Последовательность:** строка символов, например: `GGGACGGGGTTGGAAGGG`.
- **Паттерны повторов:**
    - `GGG-x-GGG`, где `x` — любые токены (до 6 символов).
    - `GGGGGG` — непрерывная последовательность из 6 и более G.
    - `GGGG-x-GGGG`, где `x` — любые токены (до 6 символов).

#### **Алгоритм:**

1. **Ищем паттерны:**
    - Проверяем, присутствуют ли в последовательности следующие повторяющиеся структуры:
        - `GGG-x-GGG` (`x` ≤ 6 токенов), от 2 повторений структуры.
        - `GGGGGG` (6 и более G подряд), от 1 повторения структуры.
        - `GGGG-x-GGGG` (`x` ≤ 6 токенов), от 1 повторения структуры.
	- `G` может быть в следующих вариациях:
		- `G`, `+G`, `oG`, `mG`, `fG`, `rG`
          
2. **Примеры поиска:**
    - Последовательность: `GGGACGGGGTTGGAAGGG`.
        - `GGG-x-GGG`:  
            `GGG` → `GGGACGGG` → два повтора.
        - `GGGGGG`:  
            Встречается как `GGGGGG`.
        - `GGGG-x-GGGG`:  
            Нет подходящих паттернов.
            
3. **Применяем коэффициент:**
    - Если найдено хотя бы одно соответствие, добавляем повышающий коэффициент `1.3`.

- Итоговая стоимость:  
    **`стоимость = базовая стоимость × коэффициент.`**

---

### **3. Пример расчетов**

#### **Пример 1: Содержание G ≥ 50%**

- Последовательность: `GCGGGTTGCG`.
- Базовая стоимость: `100 у.е.`.
- **Длина:** 10.
- **G:** 6.
- **Процент:** `(6 / 10) × 100 = 60%`.
- **Итог:**  
    **`стоимость = 100 × 1.3 = 130 у.е.`.**

---

#### **Пример 2: G-повторы**

- Последовательность: `GGGACGGGGTААААTGGGAAGGG`.
- Базовая стоимость: `100 у.е.`.
- **Паттерн:** `GGG-x-GGG` (2 повторения структуры).
- **Итог:**  
    **`стоимость = 100 × 1.3 = 130 у.е.`.**
