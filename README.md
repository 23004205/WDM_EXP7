### EX7 Implementation of Link Analysis using HITS Algorithm
### DATE: 22.08.2026
### AIM: To implement Link Analysis using HITS Algorithm in Python.
### Description:
<div align = "justify">
The HITS (Hyperlink-Induced Topic Search) algorithm is a link analysis algorithm used to rank web pages. It identifies authority and hub pages 
in a network of web pages based on the structure of the links between them.

### Procedure:
1. ***Initialization:***
    <p>    a) Start with an initial set of authority and hub scores for each page.
    <p>    b) Typically, initial scores are set to 1 or some random values.
  
2. ***Construction of the Adjacency Matrix:***
    <p>    a) The web graph is represented as an adjacency matrix where each row and column correspond to a web page, and the matrix elements denote the presence or absence of links between pages.
    <p>    b) If page A has a link to page B, the corresponding element in the adjacency matrix is set to 1; otherwise, it's set to 0.

3. ***Iterative Updates:***
    <p>    a) Update the authority scores based on the hub scores of pages pointing to them and update the hub scores based on the authority scores of pages they point to.
    <p>    b) Calculate authority scores as the sum of hub scores of pages pointing to the given page.
    <p>    c) Calculate hub scores as the sum of authority scores of pages that the given page points to.

4. ***Normalization:***
    <p>    a) Normalize authority and hub scores to prevent them from becoming too large or small.
    <p>    b) Normalize by dividing by their Euclidean norms (L2-norm).

5. ***Convergence Check:***
    <p>    a) Check for convergence by measuring the change in authority and hub scores between iterations.
    <p>    b) If the change falls below a predefined threshold or the maximum number of iterations is reached, the algorithm stops.

6. ***Visualization:***
    <p>    Visualize using bar chart to represent authority and hub scores.

### Program:
```
import numpy as np
import matplotlib.pyplot as plt


def hits_algorithm(adjacency_matrix, max_iterations=100, tol=1.0e-6):

    num_nodes = len(adjacency_matrix)

    # Initialize authority and hub scores
    authority_scores = np.ones(num_nodes)
    hub_scores = np.ones(num_nodes)

    for i in range(max_iterations):

        # Authority update
        new_authority_scores = np.dot(
            adjacency_matrix.T,
            hub_scores
        )

        # Normalize authority scores
        new_authority_scores = (
            new_authority_scores /
            np.linalg.norm(new_authority_scores)
        )

        # Hub update
        new_hub_scores = np.dot(
            adjacency_matrix,
            new_authority_scores
        )

        # Normalize hub scores
        new_hub_scores = (
            new_hub_scores /
            np.linalg.norm(new_hub_scores)
        )

        # Check convergence
        authority_diff = np.linalg.norm(
            new_authority_scores - authority_scores
        )

        hub_diff = np.linalg.norm(
            new_hub_scores - hub_scores
        )

        # Update scores
        authority_scores = new_authority_scores
        hub_scores = new_hub_scores

        if authority_diff < tol and hub_diff < tol:
            break

    return authority_scores, hub_scores


# 4-node adjacency matrix
# If Node i has a link to Node j, value = 1
adj_matrix = np.array([
    [0, 1, 1, 0],
    [0, 0, 1, 1],
    [0, 0, 0, 1],
    [1, 0, 1, 0]
])


# Run HITS algorithm
authority, hub = hits_algorithm(adj_matrix)


# Display results
print("HITS Algorithm Results")
print("----------------------")

for i in range(len(authority)):
    print(
        f"Node {i}: "
        f"Authority Score = {authority[i]:.4f}, "
        f"Hub Score = {hub[i]:.4f}"
    )


# Bar chart of Authority vs Hub scores
nodes = np.arange(len(authority))
bar_width = 0.35

plt.figure(figsize=(8, 6))

plt.bar(
    nodes - bar_width / 2,
    authority,
    bar_width,
    label='Authority',
    color='blue'
)

plt.bar(
    nodes + bar_width / 2,
    hub,
    bar_width,
    label='Hub',
    color='green'
)

plt.xlabel('Node')
plt.ylabel('Scores')
plt.title('Authority and Hub Scores for Each Node')

plt.xticks(
    nodes,
    [f'Node {i}' for i in range(len(authority))]
)

plt.legend()
plt.tight_layout()
plt.show()
```


### Output:

<img width="556" height="132" alt="image" src="https://github.com/user-attachments/assets/40972dad-8900-4f37-a477-78d82f0f2278" />

<img width="838" height="627" alt="image" src="https://github.com/user-attachments/assets/bb6bdd57-0ecf-4c2f-92f8-952553ee7bd1" />

### Result:
Therefore, Link Analysis using HITS Algorithm in Python is implemented and executed successfully.

