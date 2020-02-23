# Extract HashMap Values
-------------
```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

    public class extractHashMap {

        public static void main(String[] args) {

            Map<String, Integer> hashMap = new HashMap<String, Integer>();

            hashMap.put("Key1", 1);
            hashMap.put("Key2", 2);
            hashMap.put("Key3", 3);
            hashMap.put("Key4", 4);
            hashMap.put("Key5", 5);

            // 방법1
            Iterator<String> keys = hashMap.keySet().iterator();
            while (keys.hasNext()){
                String key = keys.next();
                System.out.println("KEY : " + key); // Key2 , Key1, Key4, Key3, Key5
            }

            // 방법2
            Set set = hashMap.keySet();
            Iterator iterator = set.iterator();
            while(iterator.hasNext()){
                String key = (String) iterator.next();
                System.out.println("KEY : " + key); // Key2 , Key1, Key5, Key4, Key3
            }

            // 방법3
            Set set2 = hashMap.entrySet();
            Iterator iterator2 = set2.iterator();
            while(iterator2.hasNext()){
                Entry<String,Integer> entry = (Entry)iterator2.next();
                String key = (String)entry.getKey();
                int value = (Integer)entry.getValue();
                System.out.println("hashMap Key : " + key);
                System.out.println("hashMap Value : " + value);
            }
        }
    }
```
