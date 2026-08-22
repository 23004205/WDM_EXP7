### EX7 Implementation of Link Analysis using HITS Algorithm
    
    for i in range(max_iterations):
        # Authority update
        new_authority_scores = np.dot(adjacency_matrix.T, hub_scores)
        new_authority_scores /= np.sum(new_authority_scores)
        # Hub update

        new_hub_scores = np.dot(adjacency_matrix, new_authority_scores)
        new_hub_scores /= np.sum(new_hub_scores)

        # Check convergence
        authority_diff = np.sum(np.abs(new_authority_scores - authority_scores))
        hub_diff = np.sum(np.abs(new_hub_scores - hub_scores))

        if authority_diff < tol and hub_diff < tol:
            break
        
        authority_scores = new_authority_scores
        hub_scores = new_hub_scores
    
    return authority_scores, hub_scores

# Example adjacency matrix (replace this with your own data)
# For simplicity, using a random adjacency matrix
adj_matrix = np.array([
    [0, 1, 1, 0],
    [0, 0, 1, 1],
    [1, 1, 0, 0],
    [0, 0, 1, 0]
])

# Run HITS algorithm
authority, hub = hits_algorithm(adj_matrix)
for i in range(len(authority)):
    print(f"Node {i}: Authority Score = {authority[i]:.4f}, Hub Score = {hub[i]:.4f}")

# bar chart of authority vs hub scores

nodes = np.arange(len(authority))
bar_width = 0.35
plt.figure(figsize=(8, 6))
plt.bar(nodes - bar_width/2, authority, bar_width, label='Authority', color='blue')
plt.bar(nodes + bar_width/2, hub, bar_width, label='Hub', color='green')
plt.xlabel('Node')
plt.ylabel('Scores')
plt.title('Authority and Hub Scores for Each Node')
plt.xticks(nodes, [f'Node {i}' for i in nodes])
plt.legend()
plt.tight_layout()
plt.show()
```

### Output:
<img width="781" height="566" alt="image" src="https://github.com/user-attachments/assets/af08ce41-ef5e-459f-b6d1-337a27992ca5" />

### Result:
The HITS algorithm calculates authority and hub scores of web pages iteratively using the web link structure and adjacency matrix.
