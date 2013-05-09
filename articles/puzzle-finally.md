## Puzzle - Finally
Each issue we have a little puzzle. This month's is a coding challenge from the land of Java. No [obscure reference about Java here](/link_me) just a simple function and a question of execution order.

The first person to respond with the **correct answer** and **why** gets their name in the winners circle for next issue.

###### Exhibit A
What is the result of this function?

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
What is the result of this function?

```java
    class MarketEdgeRealised {
      int value;
    }
 
    public MarketEdgeRealised deliverBusinessValue() {
      MarketEdgeRealised realised = new MarketEdgeRealised();
      try {
        realised.value = 20;
        throw new Exception();
      } catch (Exception e) {
        realised.value = 30;
        return realised;
      } finally {
        realised.value = 50;
      }
    }
```

Send your answers to magazine@thoughtworks.com