---
title: "Graph Convolution Neural Network"
date: 2023-03-24
# weight: 1
# aliases: ["/first"]
tags: ["GNN"]
author: "Orange"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
type: post
---
### GCN
GCN originates from the article [SEMI-SUPERVISED CLASSIFICATION WITH GRAPH CONVOLUTIONAL NETWORKS](https://arxiv.org/pdf/1609.02907.pdf). Suppose there is a undirected graph `G(V,E)` with vertices V and edges E. It has an adjacency matrix `A`(VxV). Each node has a feature and the feature matrix is `X`(VxN) We want to classify the nodes into M categories using neural network `f(X,A)`. 
$$
f(X,A) = softmax(\hat{A} ReLU(\hat{A} XW(0))W(1))
$$
where
$$
\hat{A} = D^{-\frac{1}{2}}AD^{-\frac{1}{2}}
$$
It computes the symmetrically normalized adjacency matrix of G.

D denotes as degree matrix of G

$$
D_{ii} = \sum_{j\in nbr(i)}A_{ij}
$$

### code
I first generated code from ChatGPT and then I modified it. GPT makes mistakes!

```python

class GraphConvolution(tf.keras.layers.Layer):
    def __init__(self, input_dim, output_dim):
        super(GraphConvolution, self).__init__()
        self.output_dim = output_dim
        self.input_dim = input_dim
        # self.support_dim = support_dim
        # self.activation = activation
        self.w = self.add_weight("weight0", [input_dim, output_dim], initializer='glorot_uniform', trainable = True)
        print(self.w)
        # self.W = self.add_weight(name='W', shape=(self.input_dim, self.output_dim), initializer='glorot_uniform', trainable=True)
        
    def call(self, inputs):
        X, A = inputs
        outputs = list()
        # AXW
        # for i in range(self.support_dim):
        #   pre = tf.matmul(X[:,i,:], self.weights[i])
        #   outputs.append(tf.matmul(A[:,i,:], pre))
        pre = tf.matmul(X,self.w)
        outputs = tf.matmul(A, pre)

        return outputs


class GCN(tf.keras.models.Model):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super(GCN, self).__init__()
        self.input_dim = input_dim
        self.hidden_dim = hidden_dim
        self.output_dim = output_dim
        self.gc1 = GraphConvolution(input_dim, hidden_dim)
        self.gc2 = GraphConvolution(hidden_dim, output_dim)
        
    def call(self, inputs):
        X, A = inputs
        H = tf.nn.relu(self.gc1([X, A]))
        Y = self.gc2([H, A])
        return Y


def normalize_adjacency_matrix(adj_matrix):
    # Compute the degree matrix
    degree_matrix = np.diag(np.sum(adj_matrix, axis=1))

    # Compute the inverse of the degree matrix
    inverse_degree_matrix = np.linalg.inv(degree_matrix)

    # Compute the symmetrically normalized adjacency matrix
    sqrt_inverse_degree_matrix = np.sqrt(inverse_degree_matrix)
    normalized_adj_matrix = np.dot(np.dot(sqrt_inverse_degree_matrix, adj_matrix), sqrt_inverse_degree_matrix)

    return normalized_adj_matrix

# Example usage
# Generate a simple graph with 4 nodes and 5 edges
adj_matrix = np.array([[0, 1, 0, 1],
                       [1, 0, 1, 0],
                       [0, 1, 0, 1],
                       [1, 0, 1, 0]])


# Normalize the adjacency matrix
normalized_adj_matrix = np.zeros([2,4,4])
normalized_adj_matrix[0,:,:] = tf.convert_to_tensor(np.reshape(normalize_adjacency_matrix(adj_matrix+np.identity(adj_matrix.shape[0])),[1,4,4]))
normalized_adj_matrix[1,:,:] = tf.convert_to_tensor(np.reshape(normalize_adjacency_matrix(adj_matrix+np.identity(adj_matrix.shape[0])),[1,4,4]))

print(normalized_adj_matrix)
# Define the input features for each node
X = np.array([[[1, 0],
              [0, 1],
              [1, 1],
              [0, 0]],
        [[1, 0],
              [0, 1],
              [1, 1],
              [0, 0]]])

# Define the target outputs for each node
Y = np.array([[[1],
              [0],
              [1],
              [0]],
        [[1],
              [0],
              [1],
              [0]]])

X = tf.cast(X, tf.float32)

# Define the GCN model
gcn = GCN(input_dim=2, hidden_dim=4, output_dim=1)


# Compile the model
gcn.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=0.01), loss='binary_crossentropy')
# print(X, normalized_adj_matrix)
# Train the model on the graph data
# gcn.fit(x=[X, normalized_adj_matrix], y=Y, epochs=50)
gcn([X,normalized_adj_matrix])
```

### Reference
great books about GCN: [GRL](https://www.cs.mcgill.ca/~wlh/grl_book/files/GRL_Book-Chapter_5-GNNs.pdf)

Thank you, ChatGPT, you help me understand the GCN.
