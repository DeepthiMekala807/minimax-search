import math
tree = {
    'A': ['B1', 'B2', 'B3'],
    'B1': ['C1', 'C2', 'C3'],
    'B2': ['C4', 'C5', 'C6'],
    'B3': ['C7', 'C8', 'C9'],
    'C1': [],
    'C2': [],
    'C3': [],
    'C4': [],
    'C5': [],
    'C6': [],
    'C7': [],
    'C8': [],
    'C9': []
}
heuristic_values = {
    'C1': 12,
    'C2': 10,
    'C3': 3,
    'C4': 5,
    'C5': 8,
    'C6': 10,
    'C7': 11,
    'C8': 2,
    'C9': 12,
}

def minimax(node, depth, maximizing_player):
    if depth == 0 or not tree[node]:
        return heuristic_values.get(node, 0)

    if maximizing_player:
        max_eval = -math.inf
        for child in tree[node]:
            eval = minimax(child, depth - 1, False)
            max_eval = max(max_eval, eval)
        return max_eval
    else:
        min_eval = math.inf
        for child in tree[node]:
            eval = minimax(child, depth - 1, True)
            min_eval = min(min_eval, eval)
        return min_eval

def find_optimal_path(node, depth, maximizing_player):
    if depth == 0 or not tree[node]:
        return [node]

    if maximizing_player:
        best_value = -math.inf
        best_path = []
        for child in tree[node]:
            value = minimax(child, depth - 1, False)
            if value > best_value:
                best_value = value
                best_path = [node] + find_optimal_path(child, depth - 1, False)
        return best_path
    else:
        best_value = math.inf
        best_path = []
        for child in tree[node]:
            value = minimax(child, depth - 1, True)
            if value < best_value:
                best_value = value
                best_path = [node] + find_optimal_path(child, depth - 1, True)
        return best_path
optimal_path = find_optimal_path('A', 3, True)
print("Optimal Path:", optimal_path)
