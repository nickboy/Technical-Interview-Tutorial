# Topological Sorting

> Given an directed graph, a topological order of the graph nodes is defined as follow:

> * For each directed edge A -> B in graph, A must before B in the order list.
> * The first node in the order can be any node in the graph with no  nodes direct to it.

> Find any topological order for the given graph.

```java
public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
    // write your code here
    ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();
    if ( graph == null || graph.size() == 0 ) {
        return result;
    }
    
    HashMap<DirectedGraphNode, Integer> map = new HashMap<DirectedGraphNode, Integer>();
    DirectedGraphNode current, neighbor;
    for ( int i = 0 ; i < graph.size() ; i++ ) {
        current = graph.get(i);
        if ( !map.containsKey(current) ) {
            map.put(current, 0);
        }
        for ( int j = 0 ; j < current.neighbors.size() ; j++ ) {
            neighbor = current.neighbors.get(j);
            if ( map.containsKey(neighbor) ) {
                map.put(neighbor, map.get(neighbor)+1);
            } else {
                map.put(neighbor, 1);
            }
        }
    }
    
    Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
    for ( int i = 0 ; i < graph.size() ; i++ ) {
        if ( map.get(graph.get(i)) == 0 ) {
            queue.offer(graph.get(i));
        }
    }
    
    while ( !queue.isEmpty() ) {
        int size = queue.size();
        for ( int i = 0 ; i < size ; i++ ) {
            current = queue.poll();
            result.add(current);
            if ( current.neighbors != null ) {
                for ( int j = 0 ; j < current.neighbors.size() ; j++ ) {
                    neighbor = current.neighbors.get(j);
                    map.put(neighbor, map.get(neighbor)-1);
                    if ( map.get(neighbor) == 0 ) {
                        queue.offer(neighbor);
                    }
                }
            }
        }
    }
    return result;
}
```
