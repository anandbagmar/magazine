    public class MyClass {
      public static int test_my_return() {
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