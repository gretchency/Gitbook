# BloomFilter

```java
public class BloomFilter {
    private int size;
    private final int[] seeds = {5, 6, 7, 8, 9};
    private int[] bloomFilter;
    
    public BloomFilter(int size) {
        this.size = size;
        bloomFilter = new int[size];
    }
    
    public void add(String s) {
        for (int seed: seeds) {
            bloomFilter[hash(s, seed)]++;
        }
    }
    
    public boolean mightContains(String s) {
        for (int seed: seeds) {
            if (bloomFilter[hash(s, seed)] != 0) return true;
        }
        
        return false;
    }
    
    public void remove(String s) {
        if (!mightContains(s)) return;
        for (int seed: seeds) {
            bloomFilter[hash(s, seed)]--;
        }
    }
    
    private int hash(String s, int seed) {
        return 0;
    }
}
```