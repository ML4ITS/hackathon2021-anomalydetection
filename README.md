# Hackathon 2021: Anomaly Detection Problem

## Scope:
The aim is to perform __Unsupervised Anomaly Detection__ on a __Radio Access Network (RAN)__ dataset shared by a Telenor Business Unit, with  the possibility of leveraging the information on the position of the base stations.


## Context:
In the Telecom domain, efficient and accurate Anomaly  Detection is vital to be able to continuously monitor the network’s base stations’ key metrics and alert for possible incidents in time. With constant upgrades in the network infrastructure, the coming of 5G and the exponential increase of devices and antennas, it is unfeasible to carry out such detection without relying on data-driven models that automate this task.

Most commonly, the anomalies to be detected do not concern single measurements but come from systems recording several counters, that  is, generating multivariate time series. The difficulty in detecting anomalies in multivariate time series arises from the fact that the contexts and the correlations between the different  features, time windows and neighbouring base stations have to be taken into account and examined. 
This is particularly important in the Telecom context because anomalies, mostly corresponding to failures in the network or misconfiguration of the parameters’ settings,  are especially hard to recognise as they are not easily distinguishable from  the “normal” behaviour.

## Data

The data that will be shared from Telenor concerns:
- Hourly aggregated RAN technical counters coming from 403 cells belonging to 31 different base stations
- Relative distance matrix of the cells.

### Data Counters

All counters are normalised.

|column name|data type|description|
|-----------|---------|-----------|
|`timestamp`|timestamp|the metrics values correspond to the hour following the timestamp|
|`cell_name`|string|name of the cell|
|`avail_period_duration`|double|hourly rate the cell was available|
|`bandwidth`|decimal(20,1)|total available bandwidth for the sector in PRBs (3G is also mapped into PRB like measures (12,5 PRBs per carrier)|
|`num_voice_attempts`|double|total number of voice related attempts| 
|`num_data_attempts`|double|total number of data related attempts|
|`voice_failure_rate`|double|total voice failure rate|
|`data_failure_rate`|double|total data failure rate|
|`unavail_unplan_rate`|double|hourly rate the cell was unplanned unavailable|
|`unavail_total_rate`|double|total unavailable hourly rate|
|`voice_setup_failure_rate`|double|voice related setup failure rate|
|`voice_drop_rate`|double|voice related drop rate|
|`data_setup_failure_rate`|double|data related setup failure rate|
|`data_drop_rate`|double|data related drop rate|
|`thp_rate_tt_kpi`|double|amount of Downlink data transfered per user over the estimated user throughput|
|`ho_failure_rate`|double|handover failure rate (inter-, intra- frequency, inter-,intra-technology)|

The cell name is a string of numbers and digits that have a particular meaning, corresponding to the hierarchical structure of the base station.
- **_Base stations_** - also called **_sites_** -  beam radio signals to a 360° area around them.
- Each site is divided into three **_sectors_** covering an area of 120°.
- Multiple **_cells_** belong to each sector, each running at a prescribed frequency. Cells in the  same sector running on the same frequency are identified by their **_carrier number_**.  The numbering corresponds  to their installation order.

There are two types of cells:
  * **_coverage_** cells: run at lower frequencies (700, 800, 900 MHz) and aim  to “cover” a larger area around the site.
  * **_capacity_** cells: run at higher frequencies (1800, 2100,  2600  MHz) and serve a smaller area around the site, with a better quality signal.


Keeping in mind this structure above, the `cell_name` is of the form `'XX_ija'`, where:
* `XX` in `{00,01,02,..,30}` and denotes the site the cell belongs to;
* `i` in `{1,2,3}` denotes the sector  the cell belongs to;
* `j` in `{1,2,...}` denotes the carrier;
* `a` in `{'Z','X','Y','W','V','R','Q'}` denotes the technology and frequency of the cell based on the table below.

|key|technology|frequency|
|---|----------|---------|
|`'Z'`|4G|2600MHz|
|`'X'`|4G|1800MHz|
|`'Y'`|4G|2100MHz|
|`'W'`|4G|800MHz|
|`'V'`|2G|900MHz|
|`'R'`|3G|2100MHz|
|`'Q'`|3G|900MHz|



## Row sample in CSV format
```csv
timestamp,cell_name,avail_period_duration,bandwidth,num_voice_attempts,num_data_attempts,voice_failure_rate,data_failure_rate,unavail_unplan_rate,unavail_total_rate,voice_setup_failure_rate,voice_drop_rate,data_setup_failure_rate,data_drop_rate,thp_rate_tt_kpi,ho_failure_rate
2020-09-09 13:00:00+00:00,00_11Z,1.0,1.0,0.160213,0.128572,0.4,0.018830,0.0,0.348986,0.5,0.5,0.052767,0.003127,7.125096e-05,0.335624
2020-04-13 09:00:00+00:00,01_31Z,1.0,1.00000,0.025367,0.054606,0.4,0.018782,0.0,0.348986,0.5,0.5,0.052632,0.003128,0.000088,0.333333
2020-08-24 17:00:00+00:00,00_32Z,1.0,1.00000,0.008011,0.019009,0.4,0.018782,0.0,0.348986,0.5,0.5,0.052632,0.003128,0.000136,0.333333
2020-06-22 05:00:00+00:00,02_31X,1.0,0.49975,0.013351,0.039680,0.4,0.019254,0.0,0.348986,0.5,0.5,0.053073,0.003448,0.000070,0.339683
2020-08-26 19:00:00+00:00,03_31Y,1.0,0.49975,0.004005,0.006780,0.4,0.018782,0.0,0.348986,0.5,0.5,0.052632,0.003128,0.000099,0.333333

```



