# og._dataset.Build_graph

!!! abstract "Class"
    <b>og._dataset.Build_graph(<i>adata, image, n_neighbors=3, patch_size=48, train_mode=True</i>)</b>

Build a graph for spatial transcriptomics data by [dgl](https://www.dgl.ai/).

Graph is contained in attribute `g`.

**Parameters**:

- **adata**: `anndata.AnnData`

    Input data of shape `n_obs` × `n_vars`. Rows correspond to cells and columns to genes.
    Position information is contained in `adata.obsm['spatial']`.

- **image**: `numpy.ndarray`

    H&E image of input data.

- **n_neighbors**: `int` (default: `3`)

    Number of neighbors to generate adjacency matrix.

- **patch_size**: `int` (default: `48`)

    Side length of every patch.

- **train_mode**: `bool` (default: `True`)

    If `True`, patches will pass through color jitter, random horizontal flip, and random rotation.

**Attributes**:

- **g**: `dgl.Graph`

    Graph object built.

    Nodes are the observations in `adata`.

    Edges indicate how close the two observations' positions are.

    `g.ndata['patch']`, image patch of every spot.

    `g.ndata['x']`, gene expression vector of every spot.

    `g.ndata['position']`, position of every spot.

!!! note
    If in pre-training, `train_mode=True` can provide data augmentation to train your model.

**Example**:
```python
import ODBCGAN as og

builder = og._dataset.Build_graph(adata, image)
g = builder.g
```