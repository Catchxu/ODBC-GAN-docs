# og.detect.Classify_SC

!!! abstract "Class"
    <div id = 'SC'><b>og.detect.Classify_SC(<i>n_subtypes, n_epochs=10, learning_rate=1e-6, weight_decay=0, alpha=1, pretrain=True, GPU=True, verbose=True, log_interval=1, random_state=100</i>)</b></div>

Detect outlier cell subtypes with gene expression as SC mode of ODBC-GAN.

[og.detect.Classify_SC](#SC) has one important function [fit](#fit). This class has been integrated in [og.subtype_detect](./subtype_detect.md) as SC mode.

**Parameters**:

- **n_subtypes**: `Union[int, Literal['auto']]`

    Number of outlier subtypes. If `n_subtypes='auto'`, ODBC-GAN will automatically determine the number of subtypes.

- **n_epochs**: `int` (default: `10`)

    Number of train epochs.

- **learning_rate**: `float` (default: `1e-6`)

    Learning rate for Adam optim.

- **weight_decay**: `float` (default: `0`)

    Weight decay for Adam optim.

- **alpha**: `int` (default: `1`)

    Hyperparameter of [DESC loss](https://www.nature.com/articles/s41467-020-15851-3).

- **pretrain**: `bool` (default: `True`)

    If `True`, load pretrained weight for ODBC-GAN.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `1`)

    Interval of epochs between two adjacent printed information.

- **random_state**: `Optional[int]` (default: `100`)

    Random state to control all kinds of random seeds.

!!! info "Function of [og.detect.Classify_SC](#SC)"
    <div id = 'fit'><b>fit(<i>z, res</i>)</b></div>

Detect subtypes of outlier cells via deep clustering.

**Parameters**:

- **z**: `numpy.ndarray`

    Embedding of gene expression vector.

- **res**: `numpy.ndarray`

    Residual loss of gene expression vector.

**Returns**:

- **pred**: `numpy.ndarray`

    Predict subtype label of every outlier.

!!! warning
    - `train` and `outlier` should have the same genes.
    - `n_subtypes=None` is suitable, if and only if the number of subtypes is unknown in advance.
    - If set `n_epochs` very large, consider setting `weight_decay > 0`.