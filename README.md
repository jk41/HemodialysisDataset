# HemodialysisDataset

The dataset consists of three files containing timeseries entries, an overview of all treatment sessions and an overview of all patients. To reduce the amount of data only a subset of patients has records in the timeseries data. This modified dataset originates from the following paper:

Lin, CJ., Chen, YY., Pan, CF. et al. Dataset supporting blood pressure prediction for the management of chronic hemodialysis. Sci Data 6, 313 (2019). https://doi.org/10.1038/s41597-019-0319-8                                                                                                                                 
## Tasks
To get into a discussion please prepare a short presentation (15min) on the following questions and tasks.
+ What is hemodialysis about?
+ What are challenges patients and doctors are facing in this domain? What is intradialytic hypotension (IDH)?
+ Identify three influencing factors that may be correlated to IDH.
+ Finally perform an exploratory data analysis and investigate the influence of the previously identified factors on IDH using the given dataset.

## Overview of columns
The different datasets can by link by `patient_id` and  `treatment_id`. In the treatment overview and patient data columns starting with `min`, `max` and `avg` are computed by calculating the minimum, maximum and average value of the respected column regarding a single treatment or a specific patient. A description of the columns is given in the tables below. Columns starting with `min`, `max`, `avg` are not listed.

### Timeseries dataset
| Column  | Description |
| ------- | ----------- |
| `patient_id`                      | Patient ID |
| `date_of_treatment`               |	Date of treatment |
| `session_number`                  |	Number of session for patient |
| `minute_of_treatment`	            | Minute of measurement |
| `tsp_dialysisstart`	              | Date and time of dialysis start |
| `tsp_dialysisend`	                | Date and time of dialysis end |
| `dialysis_lengh_in_m`             |	Duration of dialysis session |
| `sbp_systolic_blood_pressure`     |	Systolic blood pressure [mmHg] |
| `dbp_diastolic_blood_pressure`    |	Diastolic blood pressure [mmHg] |
| `dialysate_temp_value`            |	Dialysate temperature [°C] |
| `conductivity`                    |	Conductivity of dialysate [mS/cm] |
| `uf_ultrafiltration_rate`         |	Ultrafiltration rate [l/h] |
| `blood_flow`                      |	Blood flow [ml/min] |
| `bp_measurement_number`	          | Count of blood pressure measurement. |
| `is_hypotension`                  |	If `sbp_systolic_blood_pressure` is lower than 90mmHg the entry is marked as true. |
| `ts_measurement`                  |	The absolute timestamp of the measurement averaged to 1 minute. |
| `change_sbp_to_last_m`	          | Shows how the systolic blood pressure has changed in comparison to one minute ago. |
| `change_dbp_to_last_m`	          | Shows how the diastolic blood pressure has changed in comparison to one minute ago. |
| `change_uf_to_last_m`	            | Shows how the Ultrafiltration Rate was changed in comparison to one minute ago. |
| `uf_was_stopped_counter`	        | One if Ultrafiltration Rate was set to zero and one minute ago it was not zero. |
| `blood_flow_was_stopped_counter`	| One if blood_flow Rate was set to zero and one minute ago it was not zero. |
| `change_blood_flow_to_last_m`	    | Shows how the Blood Flow was changed in comparison to one minute ago. |
| `change_conductivity_to_last_m`	  | Shows how the conductivity was changed in comparison to one minute ago. |
| `treatment_id`	                  | Treatment ID |

### Timeseries overview
| Column  | Description |
| ------- | ----------- |
| `patient_id`                      |	Patient ID |
| `date_of_treatment`	              | Date of treatment |
| `session_number`	                | Number of session for patient |
| `birthday`	                      | Birthday |
| `first_dialysis`	                | Date of first dialysis |
| `has_diabetes`	                  | Boolean indicating if a patient has diabetes. |
| `gender`	                        | Gender oft he patient |
| `age_at_first_dialysis`	          | Calculated from “Year of first dialysis” – “year of birth” |
| `time_in_hypotension_m`	          | count of minutes in timeseries where is_hypotension = true |
| `pct_time_in_hypotension`	        | Calculated from `time_in_hypotension_m` / `dialysis_lengh_in_m` [%] |
| `dialysis_lengh_in_m`	            | Duration of dialysis session [min] |
| `uf_was_stopped_counter`	        | How often was Ultrafiltration Rate set to zero during this dialysis session. |
| `blood_flow_was_stopped_counter`  |	How often was blood_flow set to zero during this dialysis session. |
| `is_hypotension_nadir_lt_90`      |	If `sbp_systolic_blood_pressure` was at least once lower than 90mmHg during the session the entry is marked as true. |
| `is_hypotension_drop_ge_20`	      | If `sbp_systolic_blood_pressure` was at least once lower than 90mmHg during the session the entry is marked as true. |
| `number_of_bp_measurements`	      | Total number of blood pressure measurements |
| `age_at_treatment`	              | Calculated from “Year of dialysis session” – “year of birth” |
| `years_since_first_treatment`	    | Calculated from “Year of dialysis session” – “year of first dialysis” |
| `weightstart`	                    | Patient’s weight at the beginning of the session |
| `dryweight`	                      | Target weight of the session |
| `weightend`                       |	Patient’s weight at the end of the session |
| `diff_to_dry_start`	              | difference between `dryweight` (target weight) and `weightstart` (weight before dialysis) |
| `diff_to_dry_end`	                | difference between `dryweight` (target weight) and `weightend` (weight after dialysis) |
| `weight_loss`	                    | difference between `weightstart` (weight before dialysis) and `weightend` (weight after dialysis) |
| `body_temperature`	              | Patients’s temperature |
| `treatment_id`	                  | Treatment ID |

### Patient dataset
| Column  | Description |
| ------- | ----------- |
| `patient_id`	                    | Patient ID |
| `birthday`	                     	| Birthday |
| `first_dialysis`	                | Date of first dialysis |
| `age_at_first_dialysis`           	| Calculated from “Year of first dialysis” – “year of birth” |
| `has_diabetes`	                  	| Boolean indicating if a patient has diabetes. |
| `gender`	                        | Gender oft he patient |
| `num_treatments`	                | How many treatments do we have in the dataset for this specific patient |
| `num_hypotension_nadir_lt_90`     	|	Shows how many treatments of this patient have at least one hypotension defined by a systolic blood pressure less than 90 mmHg. |
| `num_hypotension_drop_ge_20`	    | Shows how many treatments of this patient have at least one hypotension defined by a drop of systolic blood presser greater or equal than 20 mmHg. |
| `has_timeseries_in_small_subset`  | Boolean indicating if this patient ID is present in the timeseries data |
