# og.align.Align_SC

<div id = 'SC'></div>
!!! abstract "Class"
    <b>og.align.Align_SC(<i>n_epochs=1000, learning_rate=1e-3, pretrain=True, GPU=True, verbose=True, log_interval=200, weight=None, random_state=100, fast=False</i>)</b>

Find cell pairs with gene expression as SC mode of ODBC-GAN.

[og.align.Align_SC](#SC) has two important functions [fit](#fit) and [fit_mult](#fit_mult). This class has been integrated in [og.obs_align](./obs_align.md) as SC mode.

**Parameters**:

- **n_epochs**: `int` (default: `1000`)

    Number of train epochs.

- **learning_rate**: `float` (default: `1e-3`)

    Learning rate for Adam optim.

- **pretrain**: `bool` (default: `True`)

    If `True`, load pretrained weight for ODBC-GAN.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `200`)

    Interval of epochs between two adjacent printed information.

- **weight**: `Optional[Dict]` (default: `None`)

    Weight for every part of loss. If `None`, `weight` should be set as `{'w_rec': 50, 'w_adv': 1, 'w_gp': 10}`.

- **random_state**: `Optional[int]` (default: `100`)

    Random state to control all kinds of random seeds.

- **fast**: `bool` (default: `False`)

    If `True`, fast mode will be used.

<div id = 'fit'></div>
!!! info "Function of [og.align.Align_SC](#SC)"
    <b>fit(<i>input, reference, log=True</i>)</b>

Find cell pairs between two batches.

**Parameters**:

- **input**: `anndata.AnnData`

    Input adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **reference**: `anndata.AnnData`

    Reference adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **log**: `bool` (default: `True`)

    If `True`, print the loggers.

**Returns**:

- **idx**: `pandas.DataFrame`

    Results of observations alignment. Every column contains `obs_names` in reference data and input data. Every row means the observation pairs among reference data and input data.

<div id = 'fit_mult'></div>
!!! info "Function of [og.align.Align_SC](#SC)"
    <b>fit(<i>input, reference</i>)</b>

Find cell pairs among multiple batches.

**Parameters**:

- **input**: `List[anndata.AnnData]`

    List of input adata. Every adata has the same genes.

- **reference**: `anndata.AnnData`

    Reference adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

**Returns**:

- **idx**: `pandas.DataFrame`

    Results of observations alignment. Every column contains `obs_names` in reference data and input data. Every row means the observation pairs among reference data and input data.

!!! warning
    `input` and `reference` should have the same genes.
