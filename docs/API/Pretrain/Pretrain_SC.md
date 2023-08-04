# og._pretrain.Pretrain_SC

!!! info "Function"
    <b>Pretrain_SC(<i>train, n_epochs=50, batch_size=32, learning_rate=0.0005, GPU=True, verbose=True, log_interval=10, random_state=None, norm_type='Batch'</i>)</b>

Pretrain gene generator in SC mode by mini-batch.

**Parameters**:

- **train**: `anndata.AnnData`

    Train data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

- **n_epochs**: `int` (default: `50`)

    Number of train epochs.

- **batch_size**: `int` (default: `32`)

    Batch size of train data.

- **learning_rate**: `float` (default: `0.0005`)

    Learning rate for Adam optim.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `10`)

    Interval of epochs between two adjacent printed information.

- **random_state**: `Optional[int]` (default: `None`)

    Random state to control all kinds of random seeds.

- **norm_type**: `Literal['Batch', 'Instance']` (default: `Batch`)

    Type of normalization layers. If `'Batch'`, batch normalization. If `'Instance'`, instance normalization.

!!! note
    - `norm_type='Instance'` is suitable for batch correction task.
    - `norm_type='Batch'` is suitable for other tasks.