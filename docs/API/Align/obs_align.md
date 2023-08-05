# og.obs_align

!!! info "Function"
    <b>og.obs_align(<i>input, reference, input_image=None, ref_image=None, mode='SC', slice=None</i>)</b>

Find cell pairs in SC mode, and spot pairs in SRT mode.

Integrate two main classes [og.align.Align_SC](./Align_SC.md) and [og.align.Align_SRT](./Align_SRT.md) to implement observations alignment.

Hyperparameters (`n_epochs`, `learning_rate`, and etc.) are allowed for changing the default configuration. Detailed hyperparameter description can be see in [og.align.Align_SC](./Align_SC.md) and [og.align.Align_SRT](./Align_SRT.md).

**Parameters**:

- **input**: `Union[anndata.AnnData, List[anndata.AnnData]]`

    Input adata or list of input adata. Every adata has the same genes.

- **reference**: `anndata.AnnData`

    Reference data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **input_image**: `Optional[Union[numpy.ndarray, List[numpy.ndarray]]]` (default=`None`)

    Input H&E image or list of input H&E images.

- **ref_image**: `Optional[numpy.ndarray]` (default=`None`)

    Reference H&E image for reference data.

- **mode**: `Literal['SC', 'SRT']` (default: `'SC'`)

    Working mode of ODBC-GAN. 

- **slice**: `Optional[Literal['Vertical', 'Horizontal']]` (default: `None`)

    Slice type of SRT data.

**Returns**:

- **idx**: `pandas.DataFrame`

    Results of observations alignment. Every column contains `obs_names` in reference data and input data. Every row means the observation pairs among reference data and input data.

!!! warning
    - `input` and `reference` should have the same genes.
    - In SRT mode, `input_image` and `ref_image` are required. And the position of every spot on image should contain in `input.obsm['spatial']` and `ref.obsm['spatial']`.
    - In SRT mode, every object in `input` and `input_image` should be matched.

**Example**:
```python
import scanpy as sc
import ODBCGAN as og

adata1 = sc.read('adata1.h5ad')  # reference data
adata2 = sc.read('adata2.h5ad')
adata3 = sc.read('adata3.h5ad')

# two batch
og.obs_align(adata2, adata1, mode='SC')

# multi-batch
og.obs_align([adata2, adata3], adata1, mode='SC')

# fast mode
og.obs_align(adata2, adata1, mode='SC', fast=True)

# tune hyperparameters
og.obs_align(adata2, adata1, mode='SC', learning_rate=1e-4)
```