# og.detect.Detect_SC

!!! abstract "Class"
    <div id = 'SC'><b>og.detect.Detect_SC(<i>n_epochs=400, learning_rate=3e-4, sample_rate=1, mem_dim=1024, update_size=64, shrink_thres=9e-3, temperature=1, n_critic=2, pretrain=True, GPU=True, verbose=True, log_interval=100, random_state=100, weight=None</i>)</b></div>

Detect outlier cells with gene expression as SC mode of ODBC-GAN.

[og.detect.Detect_SC](#SC) has two important functions [fit](#fit) and [predict](#predict). This class has been integrated in [og.outlier_detect](./outlier_detect.md) as SC mode.

**Parameters**:

- **n_epochs**: `int` (default: `400`)

    Number of train epochs.

- **learning_rate**: `float` (default: `3e-4`)

    Learning rate for Adam optim.

- **sample_rate**: `float` (default: `1`)

    Proportion of the actual train data to the input train data. Consider taking a smaller `sample_rare` when input train data is large-scale.

- **mem_dim**: `float` (default: `1024`)

    Number of embeddings stored in the memory bank. Larger `mem_dim` doesn't always mean better results, which means ODBC-GAN is insensitive to the size of memory bank.

- **update_size**: `int` (default: `64`)

    Number of embeddings updated in every epoch.

- **shrink_thres**: `float` (default: `9e-3`)

    Shrinkage threshold for attention score in the memory unit.

- **temperature**: `float` (default: `1`)

    Temperature hyperparameter for attention score in the memory unit.

- **n_critic**: `int` (default: `2`)

    Number of times the discriminator is updated in a epoch. Moreover, generator is only updated once in a epoch.

- **pretrain**: `bool` (default: `True`)

    If `True`, load pretrained weight for ODBC-GAN.

- **GPU**: `bool` (default: `True`)

    If `True`, run ODBC-GAN on GPU.

- **verbose**: `bool` (default: `True`)

    If `True`, print detailed information of every epoch.

- **log_interval**: `int` (default: `100`)

    Interval of epochs between two adjacent printed information.

- **random_state**: `Optional[int]` (default: `100`)

    Random state to control all kinds of random seeds.

- **weight**: `Optional[Dict]` (default: `None`)

    Weight for every part of loss. If `None`, `weight` should be set as `{'w_rec': 50, 'w_adv': 1, 'w_enc': 1, 'w_gp': 10}`

!!! info "Function of [og.detect.Detect_SC](#SC)"
    <div id = 'fit'><b>fit(<i>train</i>)</b></div>

Learn information of normal cells on train data by full-batch.

**Parameters**:

- **train**: `anndata.AnnData`

    Train data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

!!! info "Function of [og.detect.Detect_SC](#SC)"
    <div id = 'predict'><b>predict(<i>test</i>)</b></div>

Detect outlier cells on test data by full-batch.

**Parameters**:

- **test**: `anndata.AnnData`

    Test data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.

**Returns**:

- **result**: `pandas.DataFrame`

    Results of outlier detection. `result['cell_idx']` contains `test.obs_names`, and `result['score']` contains the anomaly scores of every observation. 

!!! warning
    - [fit](#fit) must be run before [predict](#predict).
    - `train` and `test` should have the same genes.