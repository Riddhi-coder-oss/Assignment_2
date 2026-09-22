def findShortest(graph_nodes, graph_from, graph_to, ids, val):
    from collections import deque

    graph = [[] for _ in range(graph_nodes + 1)]

    for i in range(len(graph_from)):
        u = graph_from[i]
        v = graph_to[i]
        graph[u].append(v)
        graph[v].append(u)

    queue = deque()
    distance = [-1] * (graph_nodes + 1)
    source = [-1] * (graph_nodes + 1)

    for i in range(1, graph_nodes + 1):
        if ids[i - 1] == val:
            queue.append(i)
            distance[i] = 0
            source[i] = i

    if len(queue) < 2:
        return -1

    while queue:
        

current = queue.popleft()

        for neighbour in graph[current]:

            if distance[neighbour] == -1:
                distance[neighbour] = distance[current] + 1
                source[neighbour] = source[current]
                queue.append(neighbour)

            elif source[neighbour] != source[current]:
                return distance[current] + distance[neighbour] + 1

    return -1
