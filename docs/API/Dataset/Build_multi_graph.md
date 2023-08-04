# og._dataset.Build_multi_graph

!!! abstract "Class"
    <b>og._dataset.Build_multi_graph(<i>adata, image, n_neighbors=3, patch_size=48, train_mode=True</i>)</b>

Build a graph for multi-sample spatial transcriptomics data by [dgl](https://www.dgl.ai/).

Graph is contained in attribute `g`.

**Parameters**:

- **adata**: `List[anndata.AnnData]`

    List of input adata. Every adata has the same genes.

- **image**: `List[numpy.ndarray]`

    List of input H&E images.

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

!!! warning
    Every object in `adata` and `image` should be matched.

**Example**:
```python
import ODBCGAN as og

adata = [adata1, adata2, adata3]
image = [image1, image2, image3]

builder = og._dataset.Build_multi_graph(adata, image)
g = builder.g
```