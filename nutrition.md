# Table of Contents

- [General knowledge](#general-knowledge)
- [BMR](#bmr-basal-metabolic-rate)
- [TDEE](#tdee-total-daily-energy-expenditure)
  - [Target](#target)
- [Macro](#macro-macronutrient)
  - [Carb](#carb)
  - [Protein](#protein)
  - [Fat](#fat)
- [Macro Cheat Sheet](#macro-cheat-sheet)

## General knowledge

- 1kg body weight equivalent to 7700 calories.
- Should be apply in 12 weeks.
- Recalculate every 1 week.

## BMR (Basal Metabolic Rate)

- Is the amount of energy expended by the body at rest to maintain basic physiological functions such as breathing, circulation, and cell production.
- Represents the minimum number of calories your body needs to function while at complete rest.
- Formula: [Harris Benedict equation](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7784146)
  - For men
    ```bash
    BMR = 66.473 + 13.7516 * ${Weight(kg)} + 5.0033 * ${Height(cm)} – 6.755 * ${Age(years)}
    ```
  - For women
    ```bash
    BMR = 655.0955 + 9.5634 * ${Weight(kg)} + 1.8496 * ${Height(cm)} – 4.6756 * ${Age(years)}
    ```

## TDEE (Total Daily Energy Expenditure)

- Is maintenance calories
- Is a crucial factor when considering caloric intake for weight management.
- Represents the total number of calories an individual burns in a day, taking into account their Basal Metabolic Rate (BMR), physical activity, and the thermic effect of food.
- Formula:

  ```bash
  TDEE = ${BMR} * ${Activity Multipliers}
  ```

  `Activity Multipliers` is determined by:

  - Sedentary = 1.2
  - Lightly active = 1.375
  - Moderately active = 1.55
  - Very active = 1.725
  - Extra active = 1.9

### Target

| Cutting (weight loss)           | Maintenance Calories | Bulking (Muscle gain)           |
| ------------------------------- | -------------------- | ------------------------------- |
| `${TDEE} - ${Deficit calories}` | `${TDEE}`            | `${TDEE} + ${Surplus calories}` |

- Deficit & Surplus range: 100 ~ 500 calories
- Recommended: `250` calories

## Macro (Macronutrient)

- Are essential nutrients that the body requires in relatively large amounts to function properly.
- Three main types of macronutrients: protein, carb, fat.
- Recommended macro split: [40/30/30](https://www.ideafit.com/nutrition/the-science-behind-40-30-30)

### Carb

- Primary source of energy for the body, especially the brain and muscles.
- 1g carb = 4 calories
- Formula:
  ```bash
  Carb(g) = ${TDEE Target} * ${Macro Carb Percent} / 4
  ```

### Protein

- Essential for building and repairing tissues, including muscles. It also plays a role in various physiological functions in the body.
- Suggested range for `Amount of Protein` intake is around `2g` to `2.5g` of protein per 1kg of body weight.
- 1g protein = 4 calories
- Formula:

  ```bash
  Protein(g) = ${TDEE Target} * ${Macro Protein Percent} / 4
  ```

### Fat

- Important for energy storage, hormone production, and the absorption of fat-soluble vitamins (A, D, E, and K).
- 1g fat = 9 calories
- Formula:
  ```bash
  Fat(g) = ${TDEE Target} * ${Macro Fat Percent} / 9
  ```

## Macro Cheat Sheet

<table>
  <thead>
    <tr>
      <th>Categories</th>
      <th>Food</th>
      <th>Carb(g)</th>
      <th>Protein(g)</th>
      <th>Fat(g)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan=2>Carbohydrates</td>
      <td>100g com</td><td>30</td><td>3</td><td>1</td>
    </tr>
    <tr>
      <td>100g khoai lang</td><td>25</td><td>2</td><td>0.2</td>
    </tr>
    <tr>
      <td rowspan=7>Proteins</td>
      <td>100g uc ga</td><td>0</td><td>32</td><td>4</td>
    </tr>
    <tr>
      <td>100g thit heo nac</td><td>0</td><td>31</td><td>4</td>
    </tr>
    <tr>
      <td>100g thit bo</td><td>0</td><td>25</td><td>15</td>
    </tr>
    <tr>
      <td>100g ca loc</td><td>1</td><td>25</td><td>5</td>
    </tr>
    <tr>
      <td>100g tom</td><td>2</td><td>24</td><td>1</td>
    </tr>
    <tr>
      <td>100g ca chep</td><td>0</td><td>22</td><td>4</td>
    </tr>
    <tr>
      <td>1 qua trung ga</td><td>0.6</td><td>7</td><td>5</td>
    </tr>
    <tr>
      <td rowspan=1>Fats</td>
      <td>100g trai bo</td><td>10</td><td>3</td><td>80</td>
    </tr>
    <tr>
      <td rowspan=2>Vegetables</td>
      <td>100g bong cai xanh</td><td>5</td><td>3</td><td>0.3</td>
    </tr>
    <tr>
      <td>100g rau cai xanh</td><td>4</td><td>3</td><td>0.3</td>
    </tr>
    <tr>
    <td rowspan=2>Fruits</td>
      <td>1 qua tao</td><td>24</td><td>0.5</td><td>0.2</td>
    </tr>
    <tr>
      <td>1 qua chuoi tieu</td><td>23</td><td>1.3</td><td>0.3</td>
    </tr>
  </tbody>
</table>

---
