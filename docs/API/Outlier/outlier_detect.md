# og.outlier_detect

!!! info "Function"
    <b>og.outlier_detect(<i>train, test, train_image=None, test_image=None, mode='SC', **kwargs</i>)</b>

Detect outlier cells in SC mode, and outlier spots in SRT mode.

Integrate two main classes [og.detect.Detect_SC](./Detect_SC.md) and [og.detect.Detect_SRT](./Detect_SRT.md) to implement outlier detection.

Hyperparameters (`n_epochs`, `learning_rate`, and etc.) are allowed for changing the default configuration. Detailed hyperparameter description can be see in [og.detect.Detect_SC](./Detect_SC.md) and [og.detect.Detect_SRT](./Detect_SRT.md).

**Parameters**:

- **train**: `anndata.AnnData`

    Train data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **test**: `anndata.AnnData`

    Test data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **train_image**: `Optional[numpy.ndarray]` (default: `None`)

    H&E image of train data. Required for SRT mode.

- **test_image**: `Optional[numpy.ndarray]` (default: `None`)

    H&E image of test data. Required for SRT mode.

- **mode**: `Literal['SC', 'SRT']` (default: `'SC'`)

    Working mode of ODBC-GAN. 

**Returns**:

- **result**: `pandas.DataFrame`

    Results of outlier detection. `result['cell_idx']` contains `test.obs_names`, and `result['score']` contains the anomaly scores of every observation.  

!!! warning
    - When testing on different datasets, it's necessary to tune hyperparameters on the default configuration for better performance results.
    - `train` and `test` should have the same genes.
    - In SRT mode, `train_image` and `test_image` are required. And the position of every spot on image should contain in `train.obsm['spatial']` and `test.obsm['spatial']`.

**Example**:
```python
import scanpy as sc
import ODBCGAN as og

train = sc.read('train.h5ad')
test = sc.read('test.h5ad')

# use default config
og.outlier_detect(train, test, mode='SC')

# tune hyperparameters
og.outlier_detect(train, test, mode='SC', learning_rate=1e-4)
```