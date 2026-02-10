# Advance_Mathematics_Assignment

# Advance-Mathematics_Assi2

# Probability Density Function (PDF) Estimation Project

This project implements a non-linear data transformation and parameter estimation model for Air Quality data ($NO_2$) using a student-specific parameterized approach.

---

## 1. Methodology

The project is divided into two primary technical phases: Data Transformation and PDF Learning.

### Step 1: Data Transformation

The original feature $x$ (Air Quality Index for $NO_2$) is transformed into a new variable $z$ using a non-linear function to simulate real-world data perturbations.

**Transformation Formula:**

$$z = x + a_r \sin(b_r x)$$

**Parameters:**

The parameters $a_r$ and $b_r$ are derived from the University Roll Number ($r$) to ensure unique data distributions:

* $a_r = 0.05 \times (r \pmod 7)$
* $b_r = 0.3 \times (r \pmod 5 + 1)$

### Step 2: Parameter Estimation (PDF Learning)

We model the probability density of the transformed variable $z$ using the following function:

$$\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}$$

The parameters are "learned" using the **Method of Moments**, which treats the target function as a variation of the Gaussian distribution:

* **$\mu$ (Location):** The sample mean of the transformed data $z$.
* **$\lambda$ (Scale):** Calculated as $1 / (2\sigma^2)$, where $\sigma^2$ is the variance of $z$.
* **$c$ (Normalization):** The peak height required to ensure the total area under the curve equals 1.

---

## 2. Dataset Information

- **Dataset Name:** India Air Quality Dataset
- **Source:** Kaggle
- **Dataset Link:** https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data
- **Feature Used:** NO₂ (Nitrogen Dioxide) concentration
- **File:** Data_1.csv
- **Encoding:** latin1
- **Description:** The dataset contains air quality measurements collected across multiple Indian cities. The NO₂ feature is selected for transformation and probability density function estimation.

---

## 3. Implementation Details

### Libraries Used

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

### Code Workflow

1. **Load Data:** Read NO₂ values from CSV file
2. **Clean Data:** Remove NaN values from the dataset
3. **Calculate Parameters:** Compute $a_r$ and $b_r$ from roll number
4. **Transform Data:** Apply non-linear transformation to generate $z$ values
5. **Estimate Parameters:** Calculate $\mu$, $\lambda$, and $c$ using Method of Moments
6. **Visualize:** Plot histogram of transformed data and estimated PDF curve

### Key Functions

**Data Loading:**
```python
data = pd.read_csv("Data_1.csv", encoding="latin1")
no2_values = data["no2"].values
no2_values = no2_values[~np.isnan(no2_values)]
```

**Parameter Calculation:**
```python
a_val = 0.05 * (roll_no % 7)
b_val = 0.3 * ((roll_no % 5) + 1)
```

**Data Transformation:**
```python
z_data = no2_values + a_val * np.sin(b_val * no2_values)
```

**Parameter Estimation:**
```python
mean_z = np.mean(z_data)
var_z = np.var(z_data)
lambda_hat = 1 / (2 * var_z)
c_hat = 1 / np.sqrt(2 * np.pi * var_z)
```

**PDF Estimation:**
```python
z_range = np.linspace(np.min(z_data), np.max(z_data), 100)
pdf_estimate = c_hat * np.exp(-lambda_hat * (z_range - mean_z) ** 2)
```

---

## 4. Results Table

Based on the provided Roll Number (**102317239**), the calculated constants and learned parameters are as follows:

| Parameter | Logic / Source | Calculated Value |
| :--- | :--- | :--- |
| **Roll Number ($r$)** | Input | 102317239 |
| **$a_r$** | $0.05 \times (102317239 \pmod 7)$ | 0.10 |
| **$b_r$** | $0.3 \times (102317239 \pmod 5 + 1)$ | 1.50 |
| **$\mu$ (Learned)** | `np.mean(z_data)` | 25.814687 |
| **$\lambda$ (Learned)** | $1 / (2 \times \text{Var}(z))$ | 0.001461 |
| **$c$ (Learned)** | $1 / \sqrt{2\pi \times \text{Var}(z)}$ | 0.021567 |

### Calculation Breakdown

**For Roll Number 102317239:**

* $a_r = 0.05 \times (102317239 \bmod 7) = 0.05 \times 2 = 0.10$
* $b_r = 0.3 \times ((102317239 \bmod 5) + 1) = 0.3 \times (4 + 1) = 1.50$

---

## 5. Result Graph

The visualization shows:

1. **Blue Histogram:** Distribution of transformed $z$ values (normalized density)
2. **Red Curve:** Estimated probability density function $\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}$

The plot demonstrates how well the estimated PDF fits the empirical distribution of the transformed data.

### PDF Estimation Plot

<img width="704" height="517" alt="image" src="https://github.com/user-attachments/assets/fd6978f5-ec04-4a2b-b5b9-1f98fee4a5f5" />

**Figure:** Comparison of observed transformed NO₂ data histogram with the estimated probability density function. The red curve represents the learned Gaussian-like distribution obtained through the Method of Moments. The histogram uses 50 bins with density normalization, and the PDF is evaluated over 100 linearly spaced points.

---

## 6. Visualization Details

### Plot Configuration

- **Figure Size:** 8 x 5 inches
- **Histogram:**
  - Bins: 50
  - Density: True (normalized)
  - Alpha: 0.6 (transparency)
  - Label: "Observed z values"
- **PDF Curve:**
  - Color: Red
  - Line Width: 2
  - Points: 100 (linearly spaced)
  - Label: "Estimated PDF"
- **Axes:**
  - X-axis: z values
  - Y-axis: Probability Density
  - Legend: Displayed

---

## 7. Mathematical Background

### Transformation Rationale

The non-linear transformation $z = x + a_r \sin(b_r x)$ introduces:
- **Amplitude modulation:** Controlled by $a_r$
- **Frequency modulation:** Controlled by $b_r$
- **Data perturbation:** Simulates real-world noise and variability

### Method of Moments

The Method of Moments estimates parameters by equating:
1. Sample moments with theoretical moments
2. First moment (mean): $\mu = E[z]$
3. Second moment (variance): $\sigma^2 = \text{Var}(z)$

For the Gaussian-like PDF $\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}$:

**Parameter Derivations:**

1. **Mean Parameter ($\mu$):**
   $$\mu = \frac{1}{n} \sum_{i=1}^{n} z_i$$

2. **Scale Parameter ($\lambda$):**
   $$\lambda = \frac{1}{2\sigma^2}$$
   where $\sigma^2 = \frac{1}{n} \sum_{i=1}^{n} (z_i - \mu)^2$

3. **Normalization Constant ($c$):**
   $$c = \frac{1}{\sqrt{2\pi\sigma^2}}$$
   This ensures $\int_{-\infty}^{\infty} \hat{p}(z) dz = 1$

---

## 8. Key Features

✅ **Roll Number Parameterization:** Unique transformation for each student  
✅ **Non-linear Transformation:** Sinusoidal perturbation of NO₂ data  
✅ **Method of Moments:** Statistical parameter estimation  
✅ **Gaussian-like PDF:** Closed-form probability density function  
✅ **Data Visualization:** Histogram vs. estimated PDF comparison  
✅ **Normalized Distribution:** Ensures proper probability density properties

---

## 9. Usage Instructions

### Prerequisites

```bash
pip install numpy pandas matplotlib
```

### Running the Code

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/Advance-Mathematics_Assi2.git
cd Advance-Mathematics_Assi2
```

2. **Ensure Data_1.csv is in the same directory**

3. **Run the Jupyter notebook:**
```bash
jupyter notebook Advance_Mathematics_Assignment.ipynb
```

Or execute as Python script:
```bash
python advance_math_assignment.py
```

### Expected Output

```
Estimated Parameters:
lambda = 0.001461
mu     = 25.814687
c      = 0.021567
```

Followed by the visualization plot.

---

## 10. File Structure

```
Advance-Mathematics_Assi2/
│
├── Advance_Mathematics_Assignment.ipynb    # Main Jupyter notebook
├── Data_1.csv                              # Air quality dataset
├── README.md                               # This documentation
└── requirements.txt                        # Python dependencies
```

---

## 11. Theoretical Insights

### Why This Transformation?

The sinusoidal transformation serves multiple purposes:
1. **Non-linearity:** Creates complex relationships between original and transformed data
2. **Periodicity:** Introduces cyclic patterns similar to real-world phenomena
3. **Controlled Distortion:** Parameters $a_r$ and $b_r$ control magnitude and frequency

### PDF Estimation Approach

Unlike parametric maximum likelihood estimation, the Method of Moments:
- Directly relates sample statistics to distribution parameters
- Provides closed-form solutions
- Requires minimal computational resources
- Works well for Gaussian-like distributions

### Limitations

- Assumes Gaussian-like distribution structure
- May not capture multimodal distributions
- Sensitive to outliers in mean and variance estimation
- Limited flexibility compared to non-parametric methods

---

## 12. Observations

### Distribution Characteristics

- **Central Tendency:** The mean ($\mu = 25.81$) represents the center of the transformed distribution
- **Spread:** Low $\lambda$ (0.001461) indicates high variance, suggesting wide data dispersion
- **Shape:** Gaussian-like bell curve fits the transformed NO₂ data reasonably well
- **Peak Height:** Normalization constant $c = 0.0216$ ensures proper probability density

### Model Performance

- The estimated PDF captures the general shape of the empirical distribution
- Histogram and PDF curve show good alignment in the central region
- Some deviations may occur in the tails due to Gaussian assumption
- 50 histogram bins provide sufficient granularity for comparison

---

## 13. Conclusion

This project successfully demonstrates:

1. **Data Transformation:** Effective application of roll-number-specific non-linear transformation
2. **Parameter Estimation:** Successful use of Method of Moments for PDF learning
3. **Visualization:** Clear comparison between empirical and estimated distributions
4. **Statistical Modeling:** Practical implementation of theoretical concepts

The Gaussian-like PDF provides a reasonable approximation of the transformed NO₂ data distribution, validating the chosen methodology. The parameterized approach ensures unique results for different students while maintaining consistent analytical framework.

---

## 14. Future Enhancements

Potential improvements to this project:

- **Non-parametric Methods:** Implement Kernel Density Estimation for comparison
- **Goodness-of-Fit Tests:** Add Kolmogorov-Smirnov or Chi-square tests
- **Multiple Distributions:** Test Laplace, Cauchy, or Student's t distributions
- **Cross-Validation:** Split data for training and validation
- **Outlier Detection:** Identify and handle anomalous NO₂ values
- **Interactive Visualization:** Use Plotly for dynamic exploration
- **Confidence Intervals:** Add uncertainty quantification for parameters
- **Time Series Analysis:** Incorporate temporal patterns in air quality data

---

## 15. References

- **Dataset:** India Air Quality Data - Kaggle
- **Method:** Method of Moments - Statistical Parameter Estimation
- **Distribution:** Gaussian (Normal) Distribution
- **Libraries:** NumPy, Pandas, Matplotlib

---

## 16. Contact & Contribution

For questions, suggestions, or contributions:

- **GitHub:** [Your GitHub Profile]
- **Email:** [Your Email]

Feel free to fork this repository and submit pull requests for improvements!

---

## License

This project is available for educational and research purposes.

---

**Note:** Replace roll number 102317239 with your actual roll number to generate unique results. The transformation parameters and estimated PDF will automatically adjust accordingly.
