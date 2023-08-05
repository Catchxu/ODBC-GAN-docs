# og.align.Align_SRT

<div id = 'SRT'></div>
!!! abstract "Class"
    <b>og.align.Align_SRT(<i>n_epochs=1500, learning_rate=1e-4, pretrain=True, GPU=True, verbose=True, log_interval=300, weight=None, random_state=100, fast=False, slice='Vertical', patch_size=48</i>)</b>

Find spot pairs with gene expression, position and slice image as SRT mode of ODBC-GAN.

[og.align.Align_SRT](#SRT) has two important functions [fit](#fit) and [fit_mult](#fit_mult). This class has been integrated in [og.obs_align](./obs_align.md) as SRT mode.

**Parameters**:

- **n_epochs**: `int` (default: `1500`)

    Number of train epochs.

- **learning_rate**: `float` (default: `1e-4`)

    Learning rate for Adam optim.

- **pretrain**: `bool` (default: `True`)

    If `True`, load pretrained weight for ODBC-GAN.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `300`)

    Interval of epochs between two adjacent printed information.

- **weight**: `Optional[Dict]` (default: `None`)

    Weight for every part of loss. If `None`, `weight` should be set as `{'w_rec': 50, 'w_adv': 1, 'w_gp': 10}`.

- **random_state**: `Optional[int]` (default: `100`)

    Random state to control all kinds of random seeds.

- **fast**: `bool` (default: `False`)

    If `True`, fast mode will be used.

- **slice**: `Literal['Vertical', 'Horizontal']` (default: `'Vertical'`)

    Slice type of SRT data.

- **patch_size**: `int` (default: `48`)

    Side length of every patch.

<div id = 'fit'></div>
!!! info "Function of [og.align.Align_SRT](#SRT)"
    <b>fit(<i>input, reference, input_image, ref_image, log=True</i>)</b>

Find spot pairs between two batches.

**Parameters**:

- **input**: `anndata.AnnData`

    Input adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **reference**: `anndata.AnnData`

    Reference adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **input_image**: `numpy.ndarray`

    Input H&E image.

- **ref_image**: `numpy.ndarray`

    Reference H&E image for reference data.

- **log**: `bool` (default: `True`)

    If `True`, print the loggers.

**Returns**:

- **idx**: `pandas.DataFrame`

    Results of observations alignment. Every column contains `obs_names` in reference data and input data. Every row means the observation pairs among reference data and input data.

<div id = 'fit_mult'></div>
!!! info "Function of [og.align.Align_SRT](#SRT)"
    <b>fit(<i>input, reference, input_image, ref_image</i>)</b>

Find spot pairs among multiple batches.

**Parameters**:

- **input**: `List[anndata.AnnData]`

    List of input adata. Every adata has the same genes.

- **reference**: `anndata.AnnData`

    Reference adata of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **input_image**: `List[numpy.ndarray]`

    List of input H&E images.

- **ref_image**: `numpy.ndarray`

    Reference H&E image for reference data.

**Returns**:

- **idx**: `pandas.DataFrame`

    Results of observations alignment. Every column contains `obs_names` in reference data and input data. Every row means the observation pairs among reference data and input data.

!!! warning
    - `input` and `reference` should have the same genes.
    - `input_image` and `ref_image` are required. And the position of every spot on image should contain in `input.obsm['spatial']` and `ref.obsm['spatial']`.
    - Every object in `input` and `input_image` should be matched.
    - When `'slice='Vertical'` and `slice='Horizontal'`, different hyperparameters may be used.