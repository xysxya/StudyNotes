# Searching Arrays

If an array is sorted, binary search is more effcient than linear search for finding an element in the array.

## The Linear Search Approach

The linear search approach compares the key element key sequentially with each element in the array. It contunues to do so until the key matches an element in the array, or the array is exhaused without a match being found. If a match is made, the linear search returns index of the element in the array that maches the key. If no match is found, the search returns -1.

```java
public class LinearSearch {
    public static int linearSearch(int[] list,int key){
        for (int i = 0; i < list.length; i++) {
            if(key==list[i]){
                return i;
            }
        }
        return -1;
    }
}
```
