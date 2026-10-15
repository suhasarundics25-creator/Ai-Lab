def dfs(start, goal):
    stack = [(start, [])]
    visited = {tuple(start)}

    while stack:
        state, path = stack.pop()

        if state == goal:
            print("Solution found!")
            for s in path + [state]:
                for i in range(0, 9, 3):
                    print(s[i:i+3])
                print()
            return

        zero = state.index(0)
        row, col = divmod(zero, 3)

        # Up, Down, Left, Right
        moves = [(-1, 0), (1, 0), (0, -1), (0, 1)]

        for dr, dc in moves:
            r, c = row + dr, col + dc

            if 0 <= r < 3 and 0 <= c < 3:
                pos = r * 3 + c
                new_state = state.copy()
                new_state[zero], new_state[pos] = (
                    new_state[pos], new_state[zero]
                )

                key = tuple(new_state)

                if key not in visited:
                    visited.add(key)
                    stack.append((new_state, path + [state]))

    print("No solution found")


start = [1, 2, 3,
         4, 0, 6,
         7, 5, 8]

goal = [1, 2, 3,
        4, 5, 6,
        7, 8, 0]

dfs(start, goal)
