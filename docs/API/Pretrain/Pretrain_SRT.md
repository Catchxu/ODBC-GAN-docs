# og._pretrain.Pretrain_SRT

!!! info "Function"
    <b>Pretrain_SRT(<i>adata, image, n_epochs=200, batch_size=128, learning_rate=1e-5, GPU=True, verbose=True, log_interval=10, random_state=None, norm_type='Batch'</i>)</b>

Pretrain gene generator in SRT mode by mini-batch.

**Parameters**:

- **adata**: `anndata.AnnData`

    Train data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **image**: `numpy.ndarray`

    H&E image of train data.

- **n_epochs**: `int` (default: `200`)

    Number of train epochs.

- **batch_size**: `int` (default: `128`)

    Batch size of train data.

- **learning_rate**: `float` (default: `1e-5`)

    Learning rate for Adam optim.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `10`)

    Interval of epochs between two adjacent printed information.

- **random_state**: `Optional[int]` (default: `None`)

    Random state to control all kinds of random seeds.

- **norm_type**: `Literal['Batch', 'Instance']` (default: `'Batch'`)

    Type of normalization layers. If `'Batch'`, batch normalization. If `'Instance'`, instance normalization.

!!! note
    - `norm_type='Instance'` is suitable for batch correction task.
    - `norm_type='Batch'` is suitable for other tasks.
    - Implement mini-batch train by [og._dataset.Build_graph](../Dataset/Build_graph.md).