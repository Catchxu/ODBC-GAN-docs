# og.subtype_detect

!!! info "Function"
    <div id = 'sub'><b>og.subtype_detect(<i>train, outlier, n_subtypes, train_image=None, outlier_image=None, z_x=None, res_x=None, z_img=None, res_img=None, mode='SC', detect_para={}, **kwargs</i>)</b></div>

Detect outlier cell subtypes in SC mode, and outlier spot subtypes in SRT mode.

Integrate two main classes [og.detect.Classify_SC](./Classify_SC.md) and [og.detect.Classify_SRT](./Classify_SRT.md) to implement outlier subtype detection.

Hyperparameters (`n_epochs`, `learning_rate`, and etc.) are allowed for changing the default configuration. Detailed hyperparameter description can be see in [og.detect.Classify_SC](./Classify_SC.md) and [og.detect.Classify_SRT](./Classify_SRT.md).

[og.subtype_detect](#sub) implements subtype detection via deep clustering integrated the embedding and residual loss of every outlier observation.

**Parameters**:

- **train**: `anndata.AnnData`

    Train data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.
    Aim to train a better model for providing latent embedding presentation.

- **outlier**: `anndata.AnnData`

    Outlier data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.
    Aim to generate latent embedding vectors used for deep clustering.

- **n_subtypes**: `Union[int, Literal['auto']]`

    Number of outlier subtypes. If `n_subtypes='auto'`, ODBC-GAN will automatically determine the number of subtypes.

- **train_image**: `Optional[numpy.ndarray]` (default: `None`)

    H&E image of train data. Required for SRT mode.

- **outlier_image**: `Optional[numpy.ndarray]` (default: `None`)

    H&E image of outlier data. Required for SRT mode.

- **z_x**: `Optional[numpy.ndarray]` (default: `None`)

    Embedding of gene expression vector. If `z_x is None`, `outlier.X` will be used to generate embedding.

- **res_x**: `Optional[numpy.ndarray]` (default: `None`)

    Residual loss of gene expression vector. If `res_x is None`, `outlier.X` will be used to generate residual loss.

- **z_img**: `Optional[numpy.ndarray]` (default: `None`)

    Embedding of image patch. If `z_img is None`, `outlier_image` will be used to generate embedding.

- **res_img**: `Optional[numpy.ndarray]` (default: `None`)

    Residual loss of image patch. If `z_img is None`, `outlier_image` will be used to generate residual loss.

- **mode**: `Literal['SC', 'SRT']` (default: `'SC'`)

    Working mode of ODBC-GAN. 

- **detect_para**: `Dict` (default: `{}`)

    Hyperparameters for [og.outlier_detect](../Outlier/outlier_detect.md).

**Returns**:

- **pred**: `numpy.ndarray`

    Predict subtype label of every outlier.

!!! note
    - Call [og.outlier_detect](../Outlier/outlier_detect.md) to generate embedding and residual loss.
    - If both of embedding and residual loss aren't `None`, they will be straightforward used for subtype detection with ignoring `outlier` and `outlier_image`.
    - `detect_para` can tuning [og.outlier_detect](../Outlier/outlier_detect.md) for better latent embedding presentation.

!!! warning
    - `train` and `outlier` should have the same genes.
    - In SRT mode, `train_image` and `outlier_image` are required. And the position of every spot on image should contain in `train.obsm['spatial']` and `outlier.obsm['spatial']`.
    - `n_subtypes=None` is suitable, if and only if the number of subtypes is unknown in advance.
    - Run [og.outlier_detect](../Outlier/outlier_detect.md) to find out outliers at first, and find the best a set of hyperparameters. Then, `detect_para` stores these hyperparameters, [og.subtype_detect](#sub) will detect outlier subtypes.

**Example**:
```python
import scanpy as sc
import ODBCGAN as og

train = sc.read('train.h5ad')
test = sc.read('outlier.h5ad')

# use default config
og.subtype_detect(train, outlier, n_subtypes=3, mode='SC')

# tune hyperparameters of og.subtype_detect
og.subtype_detect(train, outlier, n_subtypes=3, mode='SC', learning_rate=1e-4)

# tune hyperparameters of og.outlier_detect
params = {'learning_rate': 1e-4}
og.subtype_detect(train, outlier, n_subtypes=3, mode='SC', detect_para=params)
```