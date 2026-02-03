# Advance_Mathematics_Assignment

## Probability Density Function (PDF) Estimation Project

This project focuses on estimating the **Probability Density Function (PDF)** of transformed air quality data using a mathematically grounded and student-specific approach. A non-linear transformation is applied to real-world NO₂ air quality data, followed by parameter estimation using the **Method of Moments**.

The objective of this assignment is to combine concepts from probability theory, statistics, and numerical computing to learn the parameters of a Gaussian-like distribution from data.



## 1. Project Overview

Air quality datasets often contain noise and non-linear variations. To simulate such realistic perturbations, the original NO₂ data is transformed using a sinusoidal function whose parameters are derived from the student roll number. The transformed data is then modeled using a continuous probability density function.



## 2. Methodology

The project is divided into two main technical phases:

### Step 1: Data Transformation

Let `x` denote the original NO₂ air quality measurements. A new variable `z` is generated using a non-linear transformation:

[ z = x + a_r \sin(b_r x) ]

This transformation introduces controlled oscillatory noise into the data.

**Parameter Definitions:**

* ( a_r = 0.05 \times (r \bmod 7) )
* ( b_r = 0.3 \times ((r \bmod 5) + 1) )

where `r` is the university roll number. This ensures that each student works with a unique transformed dataset.



### Step 2: PDF Parameter Estimation (Learning Phase)

The probability density of the transformed variable `z` is modeled as:

[ \hat{p}(z) = c \cdot e^{-\lambda (z - \mu)^2} ]

This function resembles a Gaussian distribution and its parameters are estimated using the **Method of Moments**.

**Learned Parameters:**

* **μ (Mean / Location):** Sample mean of `z`
* **λ (Scale):** ( \frac{1}{2\sigma^2} ), where ( \sigma^2 ) is the variance of `z`
* **c (Normalization Constant):** ( \frac{1}{\sqrt{2\pi\sigma^2}} ), ensuring total probability equals 1



## 3. Results Summary

Based on the roll number **102317254**, the following parameters were obtained:

| Parameter       | Description              | Value     |
| --------------- | ------------------------ | --------- |
| Roll Number (r) | Input                    | 102317254 |
| ( a_r )         | Transformation amplitude | 0.10      |
| ( b_r )         | Transformation frequency | 1.50      |
| μ               | Learned mean             | 25.816375 |
| λ               | Learned scale            | 0.001461  |
| c               | Normalization constant   | 0.021569  |

<img width="684" height="445" alt="image" src="https://github.com/user-attachments/assets/0e86d2ba-f150-4d39-9c15-49b96e1cf9d1" />



## 4. Visualization

The final output includes:

* A **normalized histogram** of the transformed data `z`
* An **overlaid learned PDF curve** using the estimated parameters

This visualization demonstrates how well the learned distribution fits the transformed data.



## 5. Technologies Used

* **Python 3**
* NumPy
* Pandas
* Matplotlib
* SciPy (for numerical support)



## 6. Key Learning Outcomes

* Practical application of non-linear data transformations
* Parameter estimation using the Method of Moments
* Understanding Gaussian-like PDFs and normalization
* Data visualization and interpretation



## 7. Conclusion

This project successfully demonstrates how statistical theory can be applied to real-world datasets through transformation and distribution learning. The student-specific parameterization ensures originality, while the results validate the effectiveness of the estimation technique.


