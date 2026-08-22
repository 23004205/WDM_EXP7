### EX7 Implementation of Link Analysis using HITS Algorithm
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
