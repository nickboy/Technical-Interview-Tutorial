#Building Outline

[Lintcode](http://www.lintcode.com/en/problem/building-outline/#)

題意：

Given N buildings in a x-axis，each building is a rectangle and can be represented by a triple (start, end, height)，where start is the start position on x-axis, end is the end position on x-axis and height is the height of the building. Buildings may overlap if you see them from far away，find the outline of them。

An outline can be represented by a triple, (start, end, height), where start is the start position on x-axis of the outline, end is the end position on x-axis and height is the height of the outline.



解題思路：



```java
public class Solution {
    /**
     * @param buildings: A list of lists of integers
     * @return: Find the outline of those buildings
     */
    class Edge implements Comparator<Edge> {
        int pos;
        int height;
        boolean isStart;
        public Edge(int pos, int height, boolean isStart) {
            this.pos= pos;
            this.height = height;
            this.isStart = isStart;
        }
        // 
        public int compare(Edge e1, Edge e2) {
            // 先比誰在前面
            if (e1.pos != e2.pos) {
                return Integer.compare(e1.pos, e2.pos);
            }
            // 若都是上升則比較高度
            if (e1.isStart && e2.isStart) {
                return Integer.compare(e1.height, e2.height);
            }
            //若都是下降則比下降
            if (!e1.isStart && !e2.isStart) {
                return Integer.compare(e1.height, e2.height);
            }
            
            // 表示只有其中一邊是start
            return e1.isStart ? -1 : 1;
        }
        
        public Edge() {}
    }
    
    private ArrayList<ArrayList<Integer>> output(ArrayList<ArrayList<Integer>> res) {
        
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (res.size() > 0) {
            int pre = res.get(0).get(0);
            int height = res.get(0).get(1);
            for (int i = 1; i < res.size(); i++) {
                ArrayList<Integer> now = new ArrayList<Integer>();
                int id = res.get(i).get(0);
                if (height > 0) {
                    now.add(pre);
                    now.add(id);
                    now.add(height);
                    ans.add(now);
                }
                pre = id;
                height = res.get(i).get(1);
            }
        }
        
        return ans;
    }
    public ArrayList<ArrayList<Integer>> buildingOutline(int[][] buildings) {
        
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        
        if (buildings == null || buildings.length == 0) {
            return res;
        }
        
        
        // 先把所有邊全加入 list 中，並標記是start或是end
        List<Edge> edges = new ArrayList<Edge>();
        for (int[] building : buildings) {
            Edge startEdge = new Edge(building[0], building[2], true);
            edges.add(startEdge);
            Edge endEdge = new Edge(building[1], building[2], false);
            edges.add(endEdge);
        }
        
        // sort edges according to position, height, and if the edge is start or end
        Collections.sort(edges, new Edge());
        
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>();
        ArrayList<Integer> now = null;
        for (Edge edge : edges) {
            if (edge.isStart) {
                if (heap.isEmpty() || edge.height > heap.peek()) {
                    now = new ArrayList<Integer>(Arrays.asList(edge.pos, edge.height));
                    res.add(now);
                }
                heap.add(edge.height);
            } else {
                heap.remove(edge.height);
                if (heap.isEmpty() || edge.height > heap.peek()) {
                    if (heap.isEmpty()) {
                        now = new ArrayList<Integer>(Arrays.asList(edge.pos, 0));
                    } else {
                        now = new ArrayList<Integer>(Arrays.asList(edge.pos, heap.peek()));
                    }
                    
                    res.add(now);
                }
            }
        }
        
        return output(res);
    }
}

```