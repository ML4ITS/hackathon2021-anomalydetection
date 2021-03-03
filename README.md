# Hackathon 2021: Anomaly Detection Problem

## Scope:
The aim is to perform unsupervised Anomaly Detection on a Radio Access Network (RAN) dataset shared by a Telenor Business Unit, with  the possibility of leveraging the information on the position of the base stations.


## Context:
In the Telecom domain, efficient and accurate Anomaly  Detection is vital to be able to continuously monitor the network’s base station’s key metrics and alert for possible incidents in time. With constant upgrades in the network infrastructure, the coming of 5G and the exponential increase of devices and antennas, it is unfeasible to carry out such detection without relying on data-driven models that automate this task.

Most commonly, the anomalies to be detected do not concern single measurements but come from systems recording several counters, that  is, generating multivariate time series. The difficulty in detecting anomalies in multivariate time series arises from the fact that the contexts and the correlations between the different  features, time windows and neighbouring base stations have to be taken into account and examined. 
This is particularly important in the Telecom context because anomalies, mostly corresponding to failures in the network or misconfiguration of the parameters’ settings,  are especially hard to recognise as they are not easily distinguishable from  the “normal” behaviour.

## Data

The data that will be shared from Telenor concerns:
- Hourly aggregated network technical counters coming from the Radio Access Network (RAN)
- Relative distance matrix of the base stations.
All metrics are normalised.

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



## Row sample in CSV format
```csv
timestamp,cell_name,avail_period_duration,bandwidth,num_voice_attempts,num_data_attempts,voice_failure_rate,data_failure_rate,unavail_unplan_rate,unavail_total_rate,voice_setup_failure_rate,voice_drop_rate,data_setup_failure_rate,data_drop_rate,thp_rate_tt_kpi,ho_failure_rate
2020-09-09 13:00:00+00:00,00_11Z,1.0,1.0,0.1602136181575434,0.12857222027229231,0.4,0.01883078837099315,0.0,0.34898612593383144,0.5,0.5,0.05276769509981851,0.0031275001818314055,7.125096202606257e-05,0.3356242840778923
```



