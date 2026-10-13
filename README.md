# Wuhan-Univ-Bus-Routing

**Final Project for the Fundamentals of Data Structures Course (2021) instructed by Prof. Liang Zhao**

# Finding the Shortest Campus Shuttle Route — Implementing Dijkstra's Algorithm for the Single-Source Shortest Path Problem

**Author:** Diwen Zhu  
**Affiliation:** School of Philosophy, Wuhan University

## Abstract

This project implements Dijkstra's algorithm to solve the single-source shortest path problem in a directed acyclic graph (DAG), using campus shuttle routing as a practical application.

In this model, campus shuttle stops are represented as vertices. A directed edge exists between two vertices if there is a direct, traversable route between the corresponding stops, and the weight of each edge represents the distance along that route.

The graph is represented using an adjacency list implemented through custom vertex, edge, directed graph, and linked stack classes. An interactive command-line interface is provided, along with separate implementations of algorithms for single-source shortest paths, minimum spanning trees, and other graph operations.

Experimental results demonstrate that the program successfully computes the shortest paths between campus locations. The implemented Dijkstra's algorithm has a time complexity of **O(n²)**.

---

## 1. Background and Motivation

Suppose Wuhan University is hosting a group of visitors. A driver is tasked with transporting them from a designated departure point to their destination on a campus shuttle bus. Along the way, the shuttle passes several campus landmarks, allowing the visitors to enjoy a brief sightseeing tour of the university.

There are multiple possible routes between the departure point and the destination.

However, suppose our driver is unfamiliar with the campus road network. The roads are not necessarily straightforward, and the driver must rely on navigation to find the way. Given the complexity of the interconnected campus roads, it is difficult to determine the shortest route simply by looking at a map.

Meanwhile, the visitors may be in a hurry. Perhaps they are hungry and eager to get to the cafeteria!

Therefore, we need to find the **shortest route** from the departure point to the destination.

After all, as the Chinese saying goes, *"Food is the first necessity of the people."*

---

## 2. Problem Description

Dijkstra's algorithm can be used to determine the shortest paths from a specified source vertex to all other vertices in a graph.

To implement this algorithm, a directed graph is constructed to model the campus transportation network.

The graph's logical structure and storage representation are described in Section 3.

### 2.1 Input

The user constructs a directed graph by entering its edges in the following string format:

`Vertex1>Vertex2:Weight`

Each vertex represents a campus shuttle stop at Wuhan University.

If a direct route exists between two stops and is accessible to the shuttle, a directed edge connects the corresponding vertices. The weight of this edge represents the distance between the two stops.

Users enter one edge at a time in the console, following the specified format, and press **Enter** to confirm each entry.

**Example:**

`信息学部二食堂>教五楼:1300`

This input represents a directed edge from the Second Cafeteria on the Information Science Campus to Teaching Building No. 5, with an edge weight of 1300.

### 2.2 Output

The program provides an interactive command-line interface with multiple functional options.

**Option 5: Single-Source Shortest Path** is used to solve the campus shuttle routing problem.

When the user selects this option, the program prompts them to enter a source vertex, representing the shuttle's departure point.

After the user enters the source vertex and presses **Enter**, the program computes the shortest paths from that vertex to all other reachable vertices in the graph.

The results are displayed in the console as a table containing three columns:

- **Label:** The name of the destination vertex.
- **Distance:** The shortest distance from the source vertex to the destination vertex.
- **Parent:** The predecessor vertex along the shortest path.

The predecessor information can be used to reconstruct the shortest route from the source to each reachable destination.

---

## 3. Graph Structure and Data Representation

### 3.1 Logical Structure

The underlying logical structure is a **graph**, consisting of vertices and edges.

In this project, the campus shuttle transportation network is modeled as a **directed acyclic graph (DAG)**.

Each campus shuttle stop corresponds to a vertex, while each direct route between two stops corresponds to a directed edge.

The direction of an edge indicates the permitted direction of shuttle travel, and its weight represents the distance along the corresponding route.

### 3.2 Storage Structure

The graph is stored using an **adjacency list**.

An adjacency list combines the advantages of arrays and linked lists, allowing efficient access to vertices while supporting flexible insertion and deletion of edges.

The implementation consists of the following core classes:

- **`LinkedVertex`**

  Represents a vertex in the graph.

  Each `LinkedVertex` object contains two main components:
  
  1. A label identifying the vertex, such as `信息学部二食堂` (Second Cafeteria, Information Science Campus).
  2. A linked list containing all outgoing directed edges originating from that vertex.

- **`LinkedEdge`**

  Represents a directed, weighted edge.

  Each `LinkedEdge` object contains:
  
  1. The source vertex.
  2. The destination vertex.
  3. The weight of the edge.

- **`LinkedDirectedGraph`**

  Represents the directed graph.

  This class maintains a dictionary of vertices, allowing the program to efficiently retrieve a vertex object using its label.

  Through this dictionary, the program can quickly access the linked list of outgoing edges associated with a particular vertex.

---

## 4. Design and Implementation of the Main Algorithms

### 4.1 Shortest Path Algorithm (Dijkstra's Algorithm)

Dijkstra's algorithm is based on a **greedy strategy**.

The algorithm maintains a set `S` containing vertices whose shortest distances from the source have been finalized.

Initially, `S` contains only the source vertex.

At each iteration, the algorithm selects the unvisited vertex with the smallest tentative distance from the source and adds it to `S`.

It then examines the outgoing edges of the selected vertex and updates the tentative distances of its unvisited neighbors whenever a shorter path is found.

This process continues until all reachable vertices have been processed.

#### Algorithm Steps

**Step 1: Initialization**

Create a result table, implemented as a dictionary, to store the following information for each vertex:

- **Distance:** The current shortest known distance from the source vertex.
- **Parent:** The predecessor vertex on the currently known shortest path.

Initially:

- Set the distance of the source vertex to `0`.
- Set the distances of all other vertices to infinity.
- Set the predecessor of every vertex to `None`.

Create a collection containing all unvisited vertices.

**Step 2: Iterative Processing**

Repeat the following operations:

1. Among all unvisited vertices, find the vertex `u` with the smallest tentative distance from the source.

2. Mark `u` as visited.

3. Traverse all outgoing edges of `u`.

4. For each adjacent vertex `v`, determine whether the path through `u` provides a shorter distance than the currently recorded distance to `v`.

5. If a shorter path is found, update:
   - The shortest known distance to `v`.
   - The predecessor of `v`, setting it to `u`.

This update operation is commonly referred to as **edge relaxation**.

**Step 3: Termination**

The algorithm terminates when either:

- All vertices have been visited; or
- All remaining unvisited vertices have an infinite tentative distance, indicating that they are unreachable from the source.

The algorithm then returns the result table containing the shortest-path distances and predecessor information.

### 4.2 Additional Algorithms

In addition to Dijkstra's algorithm, the project implements the following graph algorithms:

- **Depth-First Search (DFS)-Based Topological Sorting:**

  Uses a stack-based approach to generate a topological ordering of the vertices in a directed acyclic graph.

- **Prim's Algorithm:**

  Implements the minimum spanning tree algorithm to construct a spanning tree with the minimum total edge weight for a connected, weighted, undirected graph.

---

## 5. Experimental Results and Performance Analysis

### 5.1 Experimental Results

Using the interactive command-line interface, a directed graph was successfully constructed to represent routes between several locations on the Wuhan University campus.

The locations included:

- **网安基地 (Cybersecurity Base)**
- **信息学部二食堂 (Second Cafeteria, Information Science Campus)**
- **教五楼 (Teaching Building No. 5)**
- **工学部菜场 (Engineering Campus Market)**

After selecting **Option 5** and entering a source vertex, the program successfully computed and displayed the shortest-path information from the specified source to the other reachable vertices.

The output included the shortest distance to each destination vertex and its predecessor along the corresponding shortest path.

These experimental results verified the correctness of the Dijkstra's algorithm implementation for the tested graph.

### 5.2 Performance Analysis

Consider a graph containing:

- `n` vertices
- `e` edges

The space and time complexities of the implementation are analyzed below.

#### Space Complexity

The graph is stored using an adjacency list.

The storage requirements consist of:

- `O(n)` space for storing the vertices.
- `O(e)` space for storing the edges.

Therefore, the overall space complexity of the graph representation is:

**O(n + e)**

For a campus transportation network with relatively many vertices but comparatively few edges, the adjacency-list representation is more space-efficient than an adjacency matrix, which requires `O(n²)` space.

#### Time Complexity

**1. Initialization**

Initializing the result table requires traversing all vertices.

The time complexity of this step is:

`O(n)`

**2. Main Iteration**

The main loop executes at most `n` times, processing one vertex per iteration.

During each iteration:

- The algorithm searches the remaining unvisited vertices to identify the vertex with the smallest tentative distance. This operation takes `O(n)` time.
- It traverses the outgoing edges of the selected vertex to perform edge relaxation.

Since the implementation uses a linear search rather than a priority queue to select the next vertex, the total time spent selecting vertices is:

`O(n) × O(n) = O(n²)`

Additionally, each edge is examined at most once during the relaxation process, resulting in `O(e)` total time for edge relaxation.

Therefore, the overall time complexity is:

`O(n² + e)`

For a graph with `n` vertices, the number of edges is at most `O(n²)`. Consequently, the overall time complexity simplifies to:

**O(n²)**

#### Complexity Summary

| Component | Complexity |
|-----------|------------|
| Graph storage (adjacency list) | `O(n + e)` |
| Initialization | `O(n)` |
| Minimum-distance vertex selection | `O(n²)` |
| Edge relaxation | `O(e)` |
| **Overall time complexity** | **`O(n²)`** |

The adjacency-list representation is particularly suitable for relatively sparse graphs, such as campus transportation networks, because it reduces memory consumption compared with an adjacency matrix.

---

Below is submitted as the final assignment for the course Data Structure Foundation in 2021 instructed by Prof. Liang Zhao.
## 中文原文
# 校车最短行驶路径——Dijkstra算法实现单源点最短路径求解

**作者：** 武汉大学 哲学学院 朱迪文

## 摘要 
使用Dijkstra算法实现求非环有向图中的单源点最短路径求解，并运用于校车最短行驶路径问题，校车经过各站点为顶点，若之间存在可通行直接路径，则其代表顶点间存在边，边的权重为路径距离。通过顶点类、边类、有向图类、链栈类实现图的邻接表表示，建立用户交互界面，单独定义单源点最短路径、最小生成树等算法。结果显示成功获取最短路径，该算法时间复杂度为O（n²）。

---

## 一、选题背景
假设武汉大学要接待一匹宾客，由司机驾驶校园大巴将宾客从出发点送至到达点，图中经过一些校园站点（顺便游览学校走马观花）。从出发点到到达点有很多条道路，假设司机不是老司机，道路也不是康庄大道，司机依靠导航驾驶，道路错综复杂，司机没法一眼看出哪条路最近，而宾客又比较着急，比如，饿了，赶着去吃饭，好吧要找一条最短的路径，民以食为天很重要。

---

## 二、问题描述
Dijkstra算法可用于求解图中某源点到其余各顶点的最短路径，为实现Dijkstra算法，使用邻接矩阵存储有向图，具体逻辑结构即存储结构描述见三。

### 1. 问题输入
用户以字符串“顶点1>顶点2:权重”的形式输入有向图的所有边，武汉大学各站点为顶点，其间若存在校车可通行的直接路径，则其代表的顶点间存在变，其间的道路距离为边的权重。用户在控制台以“顶点1>顶点2:权重”格式输入一条边，点击回车确认输入完毕。
> 示例：`信息学部二食堂>教五楼:1300`

### 2. 问题输出
系统提供一个用户操作交互界面，具有丰富的功能选项。其中第5个选项用于解决本问题。若用户选择第5项：单源点最短路径。系统将提示用户输入计算最短路径的起始源点（即客车的出发地）。输入回车后，系统在控制台打印输出该源点到图中其他所有可达顶点的最短路径信息，以矩阵形式展示。
* 矩阵包含三列：**顶点名称（Label）**、**到源点的最短距离（Distance）**、**在最短路径上的前驱节点（Parent）**。

---

## 三、逻辑结构和存储结构设计

### 1. 逻辑结构
逻辑结构为图，图由顶点和边构成。本案例中，校园客车行驶的路线构成一个非环有向图。各站点为顶点，站点间的直达路径为有向边，边的箭头指向客车行驶方向，边的权重为距离。

### 2. 存储结构
使用**邻接表（Adjacency List）**来存储图。邻接表结合了数组与链表的优势，既能够随机存取顶点，又能够灵活增删边。
* 每一个顶点对应一个`LinkedVertex`对象。顶点中包含两部分信息：顶点的标签（如“信息学部二食堂”）和一个包含所有以该顶点为起点的有向边的链表。
* 每一个有向边对应一个`LinkedEdge`对象。边包含：边的起点、边的终点以及边的权重。
* 图对应一个`LinkedDirectedGraph`对象。它维护一个顶点的字典，使得可以通过顶点标签快速索引到对应的顶点对象，从而快速获取该顶点的出边链表。

---

## 四、主要算法的设计与实现

### 1. 最短路径算法（Dijkstra）
Dijkstra算法的核心思想是贪心策略：设置一个顶点集合S，初始时只包含源点。每次从未加入S的顶点中，选择一个当前距离源点最近的顶点加入S，并以该顶点为媒介更新其他未加入S的顶点到源点的距离，直到所有顶点处理完毕。

#### 算法步骤：
1. **初始化：** 创建一个结果矩阵（字典形式），记录每个顶点到源点的当前最短距离（初始为无穷大，源点自身为0）和前驱节点（初始为None）。创建一个集合表示所有未访问的顶点。
2. **循环迭代：** * 在所有未访问的顶点中，寻找当前距离源点最近的顶点 `u`。
   * 将 `u` 标记为已访问。
   * 遍历顶点 `u` 的所有出边，若通过 `u` 到达相邻顶点 `v` 的路径距离小于 `v` 当前记录的距离，则更新 `v` 的最短距离和前驱节点。
3. **结束：** 当所有顶点都被访问过，或者剩余未访问顶点的当前最短距离都是无穷大时，算法结束，返回结果矩阵。

### 2. 其他辅助算法
* **深度优先搜索（DFS）的拓扑排序：** 基于栈结构，用于对无环有向图进行拓扑序列的输出。
* **普里姆（Prim）算法：** 用于求解图的最小生成树。

---

## 五、实验结果及性能分析

### 1. 实验结果
在控制台交互界面中，成功构建了包含“网安基地”、“信息学部二食堂”、“教五楼”、“工学部菜场”等校园地标的有向图。选择功能5并输入起点后，程序准确打印出了该起点到其余各顶点的最短路径及前驱节点，验证了算法实现的正确性。

### 2. 性能分析
对于包含 $n$ 个顶点和 $e$ 条边的图：
* **空间复杂度：** 采用邻接表存储，空间复杂度为 $O(n + e)$，在顶点多、边稀疏的校园路线图中相比邻接矩阵大大节省了空间。
* **时间复杂度：** * 初始化结果矩阵需要遍历所有顶点，耗时 $O(n)$。
  * 外层主循环需要执行 $n$ 次以访问每一个顶点。在每次循环内，需要遍历剩余未访问顶点找出最小值，耗时 $O(n)$；同时需要遍历当前顶点的出边进行距离松弛。
  * 整个查找和松弛过程的累计时间复杂度为 $O(n) \times O(n) = O(n^2)$。因此，该 Dijkstra 算法实现的总时间复杂度为 **$O(n^2)$**。
