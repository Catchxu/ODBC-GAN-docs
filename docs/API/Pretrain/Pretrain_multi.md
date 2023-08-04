# og._pretrain.Pretrain_multi

!!! info "Function"
    <b>Pretrain_SRT(<i>adata, image, n_epochs=200, batch_size=128, patch_size=48, learning_rate=1e-5, GPU=True, verbose=True, log_interval=10, random_state=None</i>)</b>

Pretrain transformer fusion block in SRT mode by mini-batch.

**Parameters**:

- **adata**: `Union[anndata.AnnData, List[anndata.AnnData]]`

    Input adata or list of input adata. Every adata has the same genes.

- **image**: `Union[numpy.ndarray, List[numpy.ndarray]]`

    Input H&E image or list of input H&E images.

- **n_epochs**: `int` (default: `200`)

    Number of train epochs.

- **batch_size**: `int` (default: `128`)

    Batch size of train data.

- **patch_size**: `int` (default: `48`)

    Side length of every patch.

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

!!! note
    Implement mini-batch train by [og._dataset.Build_graph](../Dataset/Build_graph.md) or [og._dataset.Build_multi_graph](../Dataset/Build_multi_graph.md).

!!! Warning
    Pretrain weight of gene generator and image generator will be loaded. Make sure the pretrain weight exists.