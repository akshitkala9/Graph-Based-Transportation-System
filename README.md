# Graph-Based Transportation System

## Overview

The Transportation Network Analysis System is a Java Swing-based application that models cities and roads as a weighted graph. Users can create transportation networks interactively and analyze them using various graph algorithms.

## Features

* Add cities dynamically through the graphical interface
* Connect cities using weighted roads
* Interactive graph visualization
* Breadth First Search (BFS) Traversal
* Dijkstra's Shortest Path Algorithm
* Prim's Minimum Spanning Tree (MST)
* Reachability Analysis
* Source city highlighting
* MST edge visualization
* User-friendly Java Swing GUI

## Technologies Used

* Java
* Java Swing
* Graph Data Structures
* BFS Algorithm
* Dijkstra's Algorithm
* Prim's Algorithm
* Object-Oriented Programming (OOP)

## How to Run

### Compile

```bash
javac TransportationNetworkAdvanced.java
```

### Run

```bash
java TransportationNetworkAdvanced
```

## Usage

1. Click **Add City** and place cities on the canvas.
2. Enter custom city names.
3. Click **Add Road** and connect two cities.
4. Enter the road distance.
5. Select a source city.
6. Run BFS, Dijkstra, Reachability Analysis, or Prim MST.
7. View results in the output panel.

## Algorithms Implemented

### Breadth First Search (BFS)

Used for graph traversal and exploring all reachable cities from a source.

### Dijkstra's Algorithm

Calculates the shortest distance from the selected source city to all other cities.

### Prim's Minimum Spanning Tree (MST)

Finds the minimum-cost network connecting all cities.

### Reachability Analysis

Determines which cities can be reached from the selected source city.

## Future Enhancements

* Save and Load Networks
* Delete Cities and Roads
* DFS Traversal
* Drag-and-Drop City Movement
* Real Map Integration

## Author

Akshit Kala

## License

This project is developed for educational and learning purposes.
