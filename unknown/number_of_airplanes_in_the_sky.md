#Number of airplanes in the sky

[Lintcode](http://www.lintcode.com/en/problem/number-of-airplanes-in-the-sky/)

題意：

Given an interval list which are flying and landing time of the flight. How many airplanes are on the sky at most?

Example
For interval list ```[[1,10],[2,3],[5,8],[4,7]]```, return 3

Note
If landing and flying happens at the same time, we consider landing should happen at first.

解題思路：

- 只有在有飛機起飛還是降落時，數目才會改變，因此只要check這兩個狀況發生的時間點即可

- 每個起飛或落降的時間點，產出一個pair為(plane, time)，按照時間(time)排序，在每個時間點，檢查是起飛還是降落

        - 起飛的話，則count加一
        - 降落的話，則count減一
        
        
暴力法：花O(N^2)，針對每一塊，去掃看有沒有重疊的，若有則更新。

另可用掃描線來優化，達到O(N)

- 可想像掃描線是在時間軸上的一條虛擬的線
- s代表升起，t代表降落，Ti代表時間i
- 把每個降落升起分別設為**(s1,Ti)**，對Ti作排序
- count + 1 代表起點，若又有另一個升起則count再加一，降落則減一

程式碼如下：

```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */

class Solution {
    /**
     * @param intervals: An interval array
     * @return: Count of airplanes are in the sky.
     */
     
    public class TimeEdge implements Comparator<TimeEdge>{
        int time;
        int flag;
        public TimeEdge(int time, int flag) {
            this.time = time;
            this.flag = flag;
        }
        
        public int compare(TimeEdge e1, TimeEdge e2) {
            if (e1.time == e2.time) {
                return e1.flag - e2.flag;
            } else {
                return e1.time - e2.time;
            }
        }
        
        public TimeEdge(){}
    }
    public int countOfAirplanes(List<Interval> airplanes) { 
        
        if (airplanes == null || airplanes.size() == 0) {
            return 0;
        }
        
        
        ArrayList<TimeEdge> timeList = new ArrayList<TimeEdge>();
        for (Interval airplane : airplanes) {
            timeList.add(new TimeEdge(airplane.start, 1));
            timeList.add(new TimeEdge(airplane.end, 0));
        }
        
        Collections.sort(timeList, new TimeEdge());
        
        int max = 0;
        int count = 0;
        for (TimeEdge time : timeList) {
            if (time.flag == 1) {
                count++;
            } else {
                count--;
            }
            if (count > max) {
                max = count;
            }
        }
        
        return max;
    }
}

```