# 🚗 Used Cars Pricing Analysis & EDA Project

## 🎯 1. Project Objective
Is project ka main objective `used_cars_mock.csv` dataset ka automated Exploratory Data Analysis (EDA) karna tha taaki yeh pata lagaya ja sake ki kaunse key features used cars ki resale price ko sabse zyada determine karte hain. Isme humne mileage, vehicle age, brand prestige, aur fuel efficiency jaise factors ke pricing impact ko test aur analyze kiya hai.

---

## 🛠️ 2. Data Cleaning & Preprocessing Pipeline
Raw data ke andar majood "broken data" aur structural irregularities ko corporate standards ke mutabik clean karne ke liye ek strict pipeline implement ki gayi:

* **Missing Values Treatment:** `mileage` column ke andar majood **306 missing (`NaN`) fields** ko uske **median** value se fill kiya gaya taaki data ka distribution kharab na ho.
* **Logical Truncation (Anomalies Removal):** Unrealistic aur physically impossible data points ko drop kiya gaya:
    * **Future Cars:** Jin gaadiyon ka manufacturing year > 2025 tha (jaise saal 2030 tak ki gaadiyan), unhe remove kiya gaya.
    * **Negative Mileage:** Negative mileage inputs (jaise -500.0) ko completely drop kiya gaya.
    * **Categorical Typos:** `fuel_type` column me majood invalid data aur text errors (jaise 'XYZ') ko filter out kiya gaya.
    * **Zero Pricing:** Operational errors jaise jin gaadiyon ki price $0 thi, unhe hataya gaya.
* **Statistical Outlier Control:** Dataset me $999,999 jaise highly inflated aur distortive pricing spikes the. Inhe **Interquartile Range ($IQR$) filtering** ($Q1 - 1.5 \times IQR$ se $Q3 + 1.5 \times IQR$) ka use karke isolate aur remove kiya gaya.

---

## 📊 3. Key Findings & Insights (Aapke Analysis Ke Mutabik)

* **The Depreciation Rule (Age vs Price):** Heatmap aur correlation analysis se yeh clear insight milta hai ki dataset ke saare numerical features me se `price` aur `car_age` ke beech ek kafi strong negative correlation **($-0.85$ ke paas)** hai. Iska matlab hai ki gaadi ki umar badhne se uski price bohot tezi se ghatti hai.
* **The Mileage Factor:** High mileage wali gaadiyon ki resale price me bada drop dekha gaya hai, jo sidhe taur par depreciation ka ek main negative driver hai.
* **Brand Value Cushion:** Premium brand status aur achhi vehicle condition resale price ko cushion karte hain aur value drop hone se bachate hain.
* **Transmission Demand:** Automatic transmission wali used cars ki resale value aur market demand manual variants ke mukable kafi behtar milti hai.
* **Temporal Isolation:** Analysis se pata chala ki `sale_month` ka kisi bhi dusre feature ke sath koi strong correlation nahi hai, yaani mahine ka pricing par koi direct asar nahi padta.

---

## 🏁 4. Analytical Summary & Operational Risk Matrix
Future machine learning models (jaise Linear Regression, Random Forest, ya Neural Networks) ki predictive accuracy ke liye raw data ke bajaye is cleaned slice ka use karna mandatory hai.

| Data State | Model Readiness | Risk / Impact on Predictive Accuracy |
| :--- | :---: | :--- |
| **Raw Data** (`df`) | ❌ Unready | **High Risk:** Outliers ($999k), negative mileages aur future years model ko skewed aur biased bana denge. |
| **Clean Data** (`df_clean`) |  Ready | **Optimal:** Reliable prediction matrix jo standard ML algorithms ke liye ek stable baseline degi. |

---

## ⚙️ 5. Tech Stack & Library Framework
* **Language:** Python 3.x
* **Data Manipulation:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn (`sns.heatmap`, `sns.boxplot`, `sns.scatterplot`, Histograms)
