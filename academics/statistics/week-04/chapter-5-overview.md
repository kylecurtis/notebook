## Chapter 5 - Part 1

- Describe the shape.
- Should the center be described using the mean or median?
- Should the spread be described using the Standard Deviation or the Interquartile Range?

> If the shape is fairly symmetric, we will use the mean and SD to describe the center and spread, respectively.

<br>

---

<br>

#### Normal Model

- Draw a symmetric, unimodal curve called a **Normal Curve**.
- The center is the mean.
- Each tick mark (z-score) is a distance of one Standard Deviation.
- Add and subtract by the Standard Deviation from the center on both sides.
- Values that are -2 < z< 2 are considered **typical**.
- Values that are z < -3 and z > 3 are considered **unusual**.
- The further from the center, the more unusual the values become.

![Example](https://miro.medium.com/v2/resize:fit:692/1*er9yh82tMZ85RWOSkKb-xA.png)

> NOTE: Under z-index 0, write the Mean, then increase or decrease by SD from the right and left of Mean respectively.

<br>

---

<br>

#### More Unusual

$z = \frac{(data) - (center)}{SD}$

> The z=score furthest from the center is more unusual. Which z-score is furthest from the center?

<br>

---

<br>

## Chapter 5 - Part 2


#### Finding Area Under the Normal Curve

It turns out that there is a specific amount of area under the curve bounded between these z-scores and we can use this area to predict the probability or its occurrence!

- For data that is unimodal and symmetric, about 68% fall within 1 SD of the mean, 95% fall within 2 SDs of the mean, and 99.7% fall within 3 SDs of the mean. This is the **68-95-99.7% Rule**.
<br>
- This rule is an approximation. We can get better accuracy using our calculator.
- Your calculator uses normalcdf(lower z, upper z) format.
- Follow these steps to calculate the area under the curve between -1 < z < 1:
	- 2nd VARS
	- #2 normalcdf(-1, 1) ENTER -- OR -- Lower: -1, Upper: 1, u-symbol = 0, o-symbol = 1
	- Paste
	- ENTER
- Normalcdf(-1, 1) = 0.6826894809
- About 68%

> NOTE: Use 100 or -100 to simulate everything above or below respectively.

<br>

---

<br>

## What If Area is Known?

- What if we know the area, but don't know the z-score?
- Your calculator uses invnorm(area on the left) format:
	- 2nd VARS
	- #3 invnorrm(0.05)
	- ENTER
- OR (Depending on Calculator):
	- Area: 0.05, u-symbol = 0, o-symbol = 1, Paste, Enter

<br>

- Find z-score for bottom 5%.
- invnorm(0.05) = -1.644853626 = z

<br>

---

<br>

Anna: 83, 83 -- 0, 0
Megan: 70, 89 -- 0.417, 1.167

1st:
Mean: 83
SD: 7

2nd:
Mean: 75
SD: 12

Must maintain 85 on all 