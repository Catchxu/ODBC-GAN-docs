# og.detect.Classify_SRT

<div id = 'SRT'></div>
!!! abstract "Class"
    <b>og.detect.Classify_SRT(<i>n_subtypes, n_epochs=10, learning_rate=1e-6, weight_decay=0, alpha=1, pretrain=True, GPU=True, verbose=True, log_interval=1, random_state=100, patch_size=48</i>)</b>

Detect outlier spot subtypes with gene expression, position and slice image as SRT mode of ODBC-GAN.

[og.detect.Classify_SRT](#SRT) has one important function [fit](#fit). This class has been integrated in [og.subtype_detect](./subtype_detect.md) as SRT mode.

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

- **patch_size**: `int` (default: `48`)

    Side length of every patch.

<div id = 'fit'></div>
!!! info "Function of [og.detect.Classify_SRT](#SRT)"
    <b>fit(<i>z_x, res_x, z_img, res_img</i>)</b>

Detect subtypes of outlier spots via deep clustering.

**Parameters**:

- **z_x**: `numpy.ndarray`

    Embedding of gene expression vector.

- **res_x**: `numpy.ndarray`

    Residual loss of gene expression vector.

- **z_img**: `numpy.ndarray`

    Embedding of image patch.

- **res_img**: `numpy.ndarray`

    Residual loss of image patch.

**Returns**:

- **pred**: `numpy.ndarray`

    Predict subtype label of every outlier.

!!! warning
    - `train` and `outlier` should have the same genes.
    - `n_subtypes=None` is suitable, if and only if the number of subtypes is unknown in advance.
    - If set `n_epochs` very large, consider setting `weight_decay > 0`.
    - `train_image` and `test_image` are required. And the position of every spot on image should contain in `train.obsm['spatial']` and `test.obsm['spatial']`.