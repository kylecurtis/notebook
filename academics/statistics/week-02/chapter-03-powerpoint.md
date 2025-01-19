# Graphing Quantitative Data

<br>

---

<br>

## 3 Graphs For Quantitative Data

| Type of Graph | Advantage |
| :--- | :--- |
| Dot Plot | Retains individual data |
| Histogram | Displays **shape** |
| Box Plot | Displays **center** and **spread** |

> NOTE: When asked to describe quantitative data, look for (investigate) `shape`, `center`, and `spread`.

<br>

---

<br>

## Shape

- **Symmetric**: Left and right side are symmetrical (mountain, etc.).
- **Right Skewed**: Tail end lowers on the right (Left side half-pipe).
- **Left Skewed**: Tail end lowers on the left side (right side half-pipe).
- **Uniform**: All the heights are about the same.

<br>

#### Other Attributes for Shape

- **Outliers**: Unusual data compared with the other data (look for gaps).
- **Modes**: 
	- **Unimodal**: One hump
	- **Bimodal**: Two humps
	- **Multimodal**: Many humps

> NOTE: More than one mode = more than one variable / attribute. Try to separate them to achieve a Unimodal graph.

<br>

#### Center Depends On Shape

If shape is symmetric:

- Use **mean** (average):

$\bar{x} = \frac{x_1 + x_2 + \cdots}{n}$

> NOTE: This value is pulled in the direction of outliers. We let the calculator calculate this!

<br>

If shape is skewed:

- Use **median**.

> NOTE: This value will have half the data values below and and half above it.

<br>

#### Spread Depends On Shape

If shape is symmetric:

- Use Standard Deviation (SD)

$S = \sqrt{\frac{(x_1 - \bar{x})^2 + (x_2 - \bar{x})^2 + \cdots} {n - 1}}$

> NOTE: We let the calculator calculate this!

<br> 

If the shape is skewed:

- Use Interquartile Range (IQR)

$IQR = Q_3 - Q_1$

> NOTE: The calculator can calculate the 3rd and 1st quarter, and we will take the difference between the two to measure the spread.

<br>

---

<br>

## Dot Plot

- Retains Individual
- Label Both Axes
- Scale on Both Axes
- Title
- Shows Shape
- Shows Modes
- Shows Outliers

<br>

## Histogram

- Stores Data in Bins
- Label Both Axes
- Scale on Both Axes
- Title
- Shows Shape
- Shows Modes
- Shows Outliers

<br>

## Box Plot

- Label Axis
- Scale on Axis
- Title
- Shows Center
- Shows Spread

> Any data on the left of the Left Fence (Min), and right of the Right Fence (Max), are outliers (and dotted).

<br>

#### Big Picture

- Always graph both (box and histogram) using same scale to get big picture of shape, center and spread.
- Histogram = shape.
- Box Plot = center and spread.

<br>

---

<br>

## Graphing Data (Calculator)

<br>

#### Entering The Data

1. Find and press the `stat` button (under the `del` button).
2. Under the `EDIT` tab, select `Edit...` (or press `1`) to add data to lists (use L1 for one data set).
3. To clear the list, hover over `L1` and press `clear` + `enter`.
4. Hovering over the last row in the column will show how many entries there are (`L1(15)` for example).

<br>

#### Graphing The Data

1. With all the data entered, press the `stat` button again, then navigate to the `CALC` tab by using the right arrow.
2. Under the `CALC` tab, select `1-Var Stats` (or press `1`) to select single variable statistics.
3. Choose the list where the data is set (L1 should be default). To choose another set, press `2nd` + the number after the `L` (for example, `2nd` + `2` for L2).
4. FreqList should be left blank.
5. With `Calculate` hovered, press `enter` to calculate the stats.

> NOTE:  $\bar{x}$ is the average.
> NOTE: Sx is the standard deviation.

<br>

#### 5 Number Summary

> NOTE: These are needed to graph box plot (take note of the values).

- `minX`
- `Q1`
- `Med`
- `Q3`
- `maxX`

<br>

---

<br>

## Graph A Histogram

1. Get to the `stat plot` menu by pressing `2nd` + `y=`.
2. In the `STAT PLOTS` menu, enable *ONLY* one plot (to avoid overlap) by pressing `1`, hover over `On` and press `enter`.
3. For the `Type`, select the histogram, which is the 3rd option from the left, and press `enter`.
4. `Xlist` should be the list where the data is held (L1). To choose another list, press `2nd` + list number.
5. `Freq` should be `1` (values are only counted once).
6. `Color` can be any value you want.

<br>

#### Custom Window

1. Get to the `WINDOW` menu by pressing the `window` button (at the top).

> NOTE: 
> - These window values are determined by the data you entered.
> - `Xmin`and `Xmax` determine the minimum and maximum numbers that the graph will target for displaying (starting and ending values for the bottom of the graph).
> - Choosing `6` means that it will display up to 5.
> - `Xscl` determines how many x value groups will be (number of pets for example).
> - `Ymin` and `Ymax` determine the minimum and maximum numbers that the graph will target for displaying (starting and ending values for the left side of the graph).
> - `Yscl` also determines how many y value groups will be (# of students for example)

2. Next press the `graph` button at the top to view the histogram.
3. Pressing the `trace` button will allow the individual values to be selected and shown.

<br>

#### Automatic Window

1. To get the calculator to graph based on what it thinks is best, press `zoom` + `9`.

> NOTE: This is doing the windows menu values itself which might not be exactly what you would set manually.


<br>

## Graph A Box Plot (Modified Box Plot)

1. Go to the `STAT PLOTS` menu by pressing `2nd` + `y=`.
2. Select the only plot that should be turned on (`1` for example).
3. Under `Type`, select the box plot with the dots (4th value from the left) and press `enter`.
4. `Xlist` should be the list where the data is (L1), and `Freq` should be `1`.
5. `Mark` and `Color` can be anything, but box mark is better.
6. A custom window can be set (like above) or you can press `zoom` + `9`.
7. `trace` allows to view the 5 number summary.
8. No dots on either side mean there are no outliers, and vise versa if there are dots.

<br>

---

<br>

## Graphing Data (Frequency Table)

> NOTE: It is easier to enter the data as a **frequency table** instead because of the repeating data values.

1. Enter the data by pressing `stat` + `1` for `Edit...`.
2. Hover over L1 and press `clear` + `enter`.
3. If you delete the column, press `stat` + `5` + `enter` to `SetUpEditor`.
4. For L1, enter the number of values (pets for example)
5. For L2, enter the frequency (number of values there are).
6. Enter the `CALC` menu by pressing `stat` and right arrow to navigate to `CALC`.
7. Select `1-Var Stats` by pressing `1` (or enter while it's highlighted).
8. For `List`, select L1
9. For `FreqList`, press `2nd` + 2 for L2
10. Enter Calculate

<br>

#### Graphing The Data (Histogram)

1. Go to `STAT PLOTS` menu by pressing `2nd` + `y=` and select `1`.
2. Make sure Plot1 is On, and select histogram type.
3. For `Xlist`, choose L1
4. For `Freq`, choose L2 by pressing `2nd` + `2`.
5. You can do manual window, or `zoom` + `9`.

<br>

#### Graphing The Data (Box Plot)

1. Go to `STAT PLOTS` menu by pressing `2nd` + `y=` and select `1`.
2. Make sure Plot1 is On, and select the box plot type.
3. Make sure `Xlist` is L1, and `Freq` is L2.
4. You can do manual window, or `zoom` + `9`.

<br>

---

<br>

## General Graphing Steps (and Info)

> TODO: ADD MORE INFO HERE LATER

**Spread (IQR)** = Q3 - Q1

<br>

---

<br>

## How Do We Know About Outliers?

#### Left Fence

Left Fence = Q1 - 1.5(IQR)

> Are there any values smaller than the answer? No? -> No Outliers. Yes? -> They are outliers.

<br>

#### Right Fence

Right Fence = Q3 + 1.5(IQR)

> Are there any values larger than the answer? No? -> No outliers. Yes? -> They are outliers.
