# API

Start the API documentation as:

```python
import ODBCGAN as og
```

## Main functions

ODBC-GAN has integrated different API to some main functions. These main functions can be used straightforward for implementing outlier detection, batch correction and subtype detection by one-step.

| <center>API</center> | <center>Description</center> |
|---|---|
| [og.outlier_detect(mode='SC')](./Outlier/outlier_detect.md)  | Detect outlier cells |
| [og.outlier_detect(mode='SRT')](./Outlier/outlier_detect.md) | Detect outlier spots |
| [og.subtype_detect(mode='SC')](./Subtype/subtype_detect.md) | Detect subtypes of outlier cells |
| [og.subtype_detect(mode='SRT')](./Subtype/subtype_detect.md) | Detect subtypes of outlier spots |
| [og.obs_align(mode='SC')](./Align/obs_align.md) | Find cell pairs among SC data |
| [og.batch_correct(mode='SRT', slice='Vertical')](./Align/obs_align.md) | Find spot pairs among SRT (vertical) data |
| [og.batch_correct(mode='SRT', slice='Horizontal')](./Align/obs_align.md) | Find spot pairs among SRT (horizontal) data |
| og.batch_correct(mode='SC') | Correct batch effects among SC data |
| og.batch_correct(mode='SRT', slice='Vertical') | Correct batch effects among SRT (vertical) data |
| og.batch_correct(mode='SRT', slice='Horizontal') | Correct batch effects among SRT (horizontal) data |