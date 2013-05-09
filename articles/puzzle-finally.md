## Puzzle - Finally
Each issue we have a little puzzle. This month's is a coding challenge from the land of Java. No [obscure reference about Java here](/link_me) just a simple function and a question of execution order.

The first person to 

###### Exhibit A
This
```java
    public class MarketEdge {
      public static int deliverBusinessValue() {
        int value = 10;
        
        try {
          value = 20;
          throw new Exception();
        } catch (Exception e) {
          value = 30;
          return value;  
        } finally {
          value = 50;
        }
      }
    }
```

###### Exhibit B

This one is a lit

