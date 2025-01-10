# Leetcode---916
Word Subsets
// code in java
import java.util.*;

public class Solution {
    public List<String> wordSubsets(String[] A, String[] B) {
        int[] bmax = new int[26];
        for (String b : B) {
            int[] bCount = count(b);
            for (int i = 0; i < 26; ++i) {
                bmax[i] = Math.max(bmax[i], bCount[i]);
            }
        }
        List<String> result = new ArrayList<>();
        for (String a : A) {
            int[] aCount = count(a);
            boolean valid = true;
            for (int i = 0; i < 26; ++i) {
                if (aCount[i] < bmax[i]) {
                    valid = false;
                    break;
                }
            }
            if (valid) {
                result.add(a);
            }
        }
        return result;
    }

    private int[] count(String word) {
        int[] count = new int[26];
        for (char c : word.toCharArray()) {
            count[c - 'a']++;
        }
        return count;
    }
}
