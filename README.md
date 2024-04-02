# DL-Actigraphy-Self-Learning-Tutorial

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>minute</th>
      <th>lastSyncTime</th>
      <th>activeness</th>
      <th>mode</th>
      <th>steps</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-05-30</td>
      <td>1176</td>
      <td>1559174400</td>
      <td>31</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-05-30</td>
      <td>1177</td>
      <td>1559174400</td>
      <td>25</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-05-30</td>
      <td>1178</td>
      <td>1559174400</td>
      <td>27</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-05-30</td>
      <td>1179</td>
      <td>1559174400</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-05-30</td>
      <td>1180</td>
      <td>1559174400</td>
      <td>22</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

###
# **Plot a single patient's Actigraphy (2 weeks)**
<img src='results/Actigraphy Scatterplot.png'>

###
# **Visualize Actigraphy Data Aggregated Across All Days**
<img src='results/Actigraphy Data Overlapped Everyday.png'>

###
# **Visualize Kernel Density Estimation**
I'm going to try to determine sleeping with Gaussian kernel density estimation. Observe the hot-zones, which represent regions of sleeping activity. We can threshold the heat and develop bounds for periods of sleep. Finally we use those bounds to add a new column to the dataframe for sleep vs. wake.
###
<img src='results/KDE Plot of Activeness over the Day.png'>

###
## We may encounter outlier hot-zones in poor data, so should add another algorithm to find peaks in this cyclical context.
I will use the [bycycle](https://bycycle-tools.github.io/bycycle/index.html) Python library for this. This geometrical approach for determining bounds is more robust.
<img src='results/KDE and Identified Sleep Periods.png'>

###
<img src='results/Activeness and Detected Sleep Periods.png'>

Once we have computed the bounds for sleep regions, we can apply it back to the original actigraphy data and we do this for all patients
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>minute</th>
      <th>lastSyncTime</th>
      <th>activeness</th>
      <th>mode</th>
      <th>steps</th>
      <th>hour</th>
      <th>datetime</th>
      <th>date_diff</th>
      <th>timestamp</th>
      <th>sleep_wake_label</th>
      <th>TimeNumeric</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-05-30</td>
      <td>1176</td>
      <td>1559174400</td>
      <td>0.173184</td>
      <td>0</td>
      <td>0.0</td>
      <td>19</td>
      <td>2019-05-31 14:36:00</td>
      <td>NaT</td>
      <td>1559313360</td>
      <td>wake</td>
      <td>876.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-05-30</td>
      <td>1177</td>
      <td>1559174400</td>
      <td>0.139665</td>
      <td>0</td>
      <td>0.0</td>
      <td>19</td>
      <td>2019-05-31 14:37:00</td>
      <td>0 days</td>
      <td>1559313420</td>
      <td>wake</td>
      <td>877.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-05-30</td>
      <td>1178</td>
      <td>1559174400</td>
      <td>0.150838</td>
      <td>0</td>
      <td>0.0</td>
      <td>19</td>
      <td>2019-05-31 14:38:00</td>
      <td>0 days</td>
      <td>1559313480</td>
      <td>wake</td>
      <td>878.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-05-30</td>
      <td>1179</td>
      <td>1559174400</td>
      <td>0.027933</td>
      <td>0</td>
      <td>0.0</td>
      <td>19</td>
      <td>2019-05-31 14:39:00</td>
      <td>0 days</td>
      <td>1559313540</td>
      <td>wake</td>
      <td>879.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-05-30</td>
      <td>1180</td>
      <td>1559174400</td>
      <td>0.122905</td>
      <td>0</td>
      <td>0.0</td>
      <td>19</td>
      <td>2019-05-31 14:40:00</td>
      <td>0 days</td>
      <td>1559313600</td>
      <td>wake</td>
      <td>880.0</td>
    </tr>
  </tbody>
</table>
</div>