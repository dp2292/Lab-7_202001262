# Lab-7_202001262

# Name - Devansh Patel

## Section A

Equivalence Partitioning Test Cases:

We can divide the input domain into the following equivalence classes:

* Valid input dates: Dates that fall within the valid range of `1 <= month <= 12` , `1 <= day <= 31` , and `1900 <= year <= 2015`. These are the inputs for which the program should return a valid previous date.

* Invalid input dates: Dates that fall outside of the valid range of `1 <= month <= 12`, `1 <= day <= 31`, and `1900 <= year <= 2015`. These are the inputs for which the program should return an "invalid date" error message.


<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=30, month=11, year=2015</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=5, year=1999</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=36, month=1, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2002</td>
    <td>An error message</td>
  </tr>
    <tr>
    <td>Invalid input: day=29, month=2, year=2012</td>
    <td>Previous date</td>
  </tr>
    <tr>
        <td>Valid input: day=1, month=6, year=2000</td>
        <td>Previous date</td>
    </tr>
    <tr>
        <td>Valid input: day=31, month=3, year=2002</td>
        <td>Previous date</td>  
    </tr>
    <tr>
        <td>Valid input: day=15, month=7, year=2001</td>
        <td>Previous date</td>
    </tr>
    <tr>
        <td>Invalid input: day=31, month=4, year=2000</td>
        <td>An error message</td>
    </tr>
</table>

Boundary Value Analysis Test Cases:

We can also test the program using inputs at the boundary values of each equivalence class. This will help us ensure that the program is correctly handling inputs at the edge of the input domain. The following inputs are at the boundary values of each equivalence class:

* Valid input dates:
    + Minimum valid date: day=1, month=1, year=1900
    + Maximum valid date: day=31, month=12, year=2015

* Invalid input dates:
    + Date with invalid month: day=15, month=13, year=2000
    + Date with invalid day: day=32, month=5, year=2000
    + Date with invalid year: day=1, month=1, year=1899

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=12, year=2002</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=32, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Valid input: day=1, month=6, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=3, year=2002</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=15, month=7, year=2001</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=31, month=4, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2002</td>
    <td>An error message</td>
    </tr>
</table>
</br>

Using both equivalence partitioning and boundary value analysis will help ensure that the program is handling all possible inputs correctly.

```
import org.junit.Test;
import static org.junit.Assert.*;

public class TestPreviousDate {

  @Test
  public void testValidInputDate() {
    PreviousDate pd = new PreviousDate();
    String result = pd.getPreviousDate(2, 3, 2010);
    assertEquals("previous date", result);
  }

  @Test
  public void testInvalidInputDate() {
    PreviousDate pd = new PreviousDate();
    String result = pd.getPreviousDate(2, 30, 2010);
    assertEquals("Invalid date", result);
  }

  @Test
  public void testMinimumValidInputDate() {
    PreviousDate pd = new PreviousDate();
    String result = pd.getPreviousDate(1, 1, 1900);
    assertEquals("Invalid date", result);
  }

  @Test
  public void testMaximumValidInputDate() {
    PreviousDate pd = new PreviousDate();
    String result = pd.getPreviousDate(31, 12, 2015);
    assertEquals("previous date", result);
  }

}
```
### Modify your programs such that it runs on eclipse IDE, and then execute your test suites on the program. While executing your input data in a program, check whether the identified expected. outcome (mentioned by you) is correct or not.

Code:

```
public class PreviousDateFinder {

    public static String findPreviousDate(int day, int month, int year) {
        if (year < 1900 || year > 2015 || month < 1 || month > 12 || day < 1 || day > 31) {
            return "invalid date";
        } else if (day == 1 && month == 1) {
            return (year - 1) + "-12-31";
        } else if (day == 1) {
            int previousMonth = month - 1;
            int previousMonthMaxDays = getDaysInMonth(previousMonth, year);
            return year + "-" + previousMonth + "-" + previousMonthMaxDays;
        } else {
            int previousDay = day - 1;
            return year + "-" + month + "-" + previousDay;
        }
    }

    private static int getDaysInMonth(int month, int year) {
        int daysInMonth;
        switch (month) {
            case 2:
                if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
                    daysInMonth = 29;
                } else {
                    daysInMonth = 28;
                }
                break;
            case 4:
            case 6:
            case 9:
            case 11:
                daysInMonth = 30;
                break;
            default:
                daysInMonth = 31;
                break;
        }
        return daysInMonth;
    }

    public static void main(String[] args) {
        int day = 10;
        int month = 3;
        int year = 2022;
        String result = findPreviousDate(day, month, year);
        System.out.println("Result: " + result); // Output: Result: 2022-3-9 (if run on March 10th, 2022)
    }
}

```

### Problem 1:

Here is the modified code for the linearSearch function in Java for the Eclipse IDE:

```
public class LinearSearch {
    public static int linearSearch(int v, int[] a) {
        int i = 0;
        while (i < a.length) {
            if (a[i] == v)
                return i;
            i++;
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] a = { 1, 2, 3, 4, 5 };
        int v = 4;
        int index = linearSearch(v, a);
        if (index != -1)
            System.out.println("Value found at index " + index);
        else
            System.out.println("Value not found in array");
    }
}
```

For testing the function, I have used the JUnit test cases:

```
import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class LinearSearchTest {

  @Test
  public void testLinearSearch() {
    int[] arr = {1, 3, 5, 7, 9};
    int target = 5;
    int expected = 2;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
  @Test
  public void testLinearSearchTargetNotFound() {
    int[] arr = {1, 3, 5, 7, 9};
    int target = 6;
    int expected = -1;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
  @Test
  public void testLinearSearchEmptyArray() {
    int[] arr = {};
    int target = 5;
    int expected = -1;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
  @Test
  public void testLinearSearchFirstElement() {
    int[] arr = {1, 3, 5, 7, 9};
    int target = 1;
    int expected = 0;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
  @Test
  public void testLinearSearchLastElement() {
    int[] arr = {1, 3, 5, 7, 9};
    int target = 9;
    int expected = 4;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
  @Test
  public void testLinearSearchDuplicateElements() {
    int[] arr = {1, 3, 5, 7, 5, 9};
    int target = 5;
    int expected = 2;
    int result = linearSearch(target, arr);
    assertEquals(expected, result);
  }
  
}
```

## Equivalence Partitioning:
### Test Cases Identified Using Equivalence Partitioning

Valid Inputs:

+ Search value exists in array - linearSearch(5, [1, 2, 5, 4, 3]) should return 2.

+ Search value exists in array - linearSearch(1, [1, 3, 2, 4, 5]) should return 0.

+ Search value exists in array at first index - linearSearch(1, [1]) should return 0.

+ Search value exists in array at last index - linearSearch(5, [1, 2, 3, 4, 5]) should return 4.

Invalid Inputs:

+ Empty array - linearSearch(5, []) should return -1.

+ Search value does not exist in array - linearSearch(6, [1, 2, 3, 4, 5]) should return -1.

+ Array with all the same values - linearSearch(5, [5, 5, 5, 5, 5]) should return 0.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Array (a)</th>
      <th>Search Value (v)</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>[]</td>
      <td>5</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>6</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an empty array a[]</td>
      <td>[]</td>
      <td>5</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists</td>
      <td>[1, 2, 5, 4, 3]</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v does not exist</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>6</td>
      <td>-1</td>
    </tr>
  </tbody>
</table>


Valid Inputs:

+ Minimum valid input - linearSearch(1, [1]) should return 0.

+ Maximum valid input - linearSearch(6, [1, 2, 3, 4, 5, 6]) should return 5.

Invalid Inputs:

+ Search value less than minimum - linearSearch(-1, [1, 2, 3, 4, 5]) should return -1.

+ Search value greater than maximum - linearSearch(10, [1, 2, 3, 4, 5]) should return -1.

+ Empty array - linearSearch(5, []) should return -1.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Array (a)</th>
      <th>Search Value (v)</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with minimum valid input: v exists in a of length 1</td>
      <td>[1]</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with maximum valid input: v exists in a of length n</td>
      <td>[1, 2, 3, 4, 5, 6]</td>
      <td>6</td>
      <td>5</td>
    </tr>
    <tr>
      <td>Test with search value less than minimum: v does not exist in a</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>-1</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with search value greater than maximum: v does not exist in a</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>10</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with empty array</td>
      <td>[]</td>
      <td>5</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists</td>
      <td>[1, 2, 5, 4, 3]</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v does not exist</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>6</td>
      <td>-1</td>
    </tr>
  </tbody>
</table>

### Problem 2 :
Here is the modified code for the `countItem` function in Java:
```
public class CountItem {
    public static int countItem(int v, int[] a) {
        int count = 0;
        for (int i = 0; i < a.length; i++) {
            if (a[i] == v)
                count++;
        }
        return count;
    }

    public static void main(String[] args) {
        int[] a = { 1, 2, 3, 4, 5, 3, 3 };
        int v = 3;
        int count = countItem(v, a);
        System.out.println("Value " + v + " appears " + count + " times in array");
    }
}
```

### Equivalence Partitioning:

#### Equivalence Partitioning Test Cases:

- Empty array: `v=6`, `a=[]`.
- Array with only one element: `v=5`, `a=[5]`.
- Array with multiple elements but v does not appear in the - array: `v=4`,`a=[1, 2, 3, 5, 6, 7`].
- Array with multiple elements and v appears once: `v=5`, `a=[1, 2, 3, 4, 5, 6, 7]`.
- Array with multiple elements and v appears multiple times: `v=5`, `a=[1, 5, 2, 5, 3, 5, 4, 5]`.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Array (a)</th>
      <th>Search Value (v)</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>[]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>[1, 2, 3, 4]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an empty array a[]</td>
      <td>[]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists multiple times</td>
      <td>[1, 2, 5, 4, 5, 3, 5]</td>
      <td>5</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists only once</td>
      <td>[1, 2, 3, 4, 5]</td>
      <td>5</td>
      <td>1</td>
    </tr>
  </tbody>
</table>


### Boundary Value Analysis:

+ Minimum valid value: v=2, a=[2, 3, 4, 5, 6, 7, 8].
+ Maximum valid value: v=20, a=[17, 18, 19, 20].
+ Value not present in the array: v=12, a=[1, 3, 5, 7, 9, 11, 13, 15].
+ All elements in the array are the same and equal to v: v=8, a=[8, 8, 8, 8, 8, 8, 8].
+ All elements in the array are different and none of them is v: v=15, a=[1, 2, 3, 4, 6, 7, 8, 9].
+ Input with no occurrence of v: The input array does not contain any occurrence of v, such as (7, {1, 3, 5, 9}).
+ Input with all elements as v: The input array contains only v, such as (4, {4, 4, 4, 4}).



<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Array a[]</th>
      <th>Value v</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>[]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>[1, 2, 3, 4]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 0</td>
      <td>[]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v exists</td>
      <td>[5]</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v does not exist</td>
      <td>[3]</td>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the beginning of the array</td>
      <td>[5, 2, 3, 4, 5]</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the end of the array</td>
      <td>[2, 3, 4, 5, 5]</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists in the middle of the array</td>
      <td>[2, 5, 4, 5, 1]</td>
      <td>5</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

### Test Execution:

```
import static org.junit.Assert.*;
import org.junit.Test;

public class CountOccurrencesTest {

    @Test
    public void testVNonExistentEmptyArray() {
        int[] a = {};
        assertEquals(0, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVNonExistentNonEmptyArray() {
        int[] a = {1, 2, 3};
        assertEquals(0, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVExistsLengthZeroArray() {
        int[] a = {};
        assertEquals(0, CountOccurrences.countOccurrences(0, a));
    }
    
    @Test
    public void testVExistsLengthOneArrayWithV() {
        int[] a = {5};
        assertEquals(1, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVExistsLengthOneArrayWithoutV() {
        int[] a = {6};
        assertEquals(0, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVExistsAtBeginning() {
        int[] a = {5, 1, 3, 5, 8};
        assertEquals(2, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVExistsAtEnd() {
        int[] a = {1, 2, 3, 4, 5, 5};
        assertEquals(2, CountOccurrences.countOccurrences(5, a));
    }
    
    @Test
    public void testVExistsInMiddle() {
        int[] a = {1, 2, 5, 5, 8, 9};
        assertEquals(2, CountOccurrences.countOccurrences(5, a));
    }
}
```

### Problem 3 :
Here is the modified code for the binarySearch function in Java:

```
public class BinarySearch {
    public static int binarySearch(int v, int[] a) {
        int lo = 0;
        int hi = a.length - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (v == a[mid])
                return mid;
            else if (v < a[mid])
                hi = mid - 1;
            else
                lo = mid + 1;
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] a = { 1, 2, 3, 4, 5, 6, 7 };
        int v = 4;
        int index = binarySearch(v, a);
        if (index != -1)
            System.out.println("Value found at index " + index);
        else
            System.out.println("Value not found in array");
    }
}
```

### Equivalence Partitioning:

- Valid input: `v` is present in `a[]`
- Invalid input: `v` is not present in `a[]`


<table>
  <tr>
    <th>Tester Action</th>
    <th>Array a[]</th>
    <th>Value v</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Search for v=5 in ordered array a=[1, 3, 5, 7, 9]</td>
    <td>[1, 3, 5, 7, 9]</td>
    <td>5</td>
    <td>2</td>
  </tr>
  <tr>
    <td>Search for v=1 in ordered array a=[1, 3, 5, 7, 9]</td>
    <td>[1, 3, 5, 7, 9]</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Search for v=9 in ordered array a=[1, 3, 5, 7, 9]</td>
    <td>[1, 3, 5, 7, 9]</td>
    <td>9</td>
    <td>4</td>
  </tr>
  <tr>
    <td>Search for v=4 in ordered array a=[1, 3, 5, 7, 9]</td>
    <td>[1, 3, 5, 7, 9]</td>
    <td>4</td>
    <td>-1</td>
  </tr>
  <tr>
    <td>Search for v=11 in ordered array a=[1, 3, 5, 7, 9]</td>
    <td>[1, 3, 5, 7, 9]</td>
    <td>11</td>
    <td>-1</td>
  </tr>
</table>

### Boundary Value Analysis:

- Valid input: `v` is the first element in `a[]`
- Valid input: `v` is the last element in `a[]`
- Valid input: `v` is in the middle of `a[]`
- Invalid input: `a[]` is empty
- Invalid input: `v` is less than the first element in `a[]`
- Invalid input: `v` is greater than the last element in `a[]`


Sure, here's the modified table in the format you requested:

<table>
  <tr>
    <th>Tester Action</th>
    <th>Array a[]</th>
    <th>Value v</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Test with v as 1 and an array a[] containing only 1</td>
    <td>[1]</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Test with v as 6 and an array a[] containing only 6</td>
    <td>[6]</td>
    <td>6</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Test with v as 5 and an empty array a[]</td>
    <td>[]</td>
    <td>5</td>
    <td>-1</td>
  </tr>
  <tr>
    <td>Test with v as 5 and an array a[] containing 7, 8, and 9</td>
    <td>[7, 8, 9]</td>
    <td>5</td>
    <td>0 (smallest index of v in a[])</td>
  </tr>
  <tr>
    <td>Test with v as 5 and an array a[] containing 3, 4, and 5</td>
    <td>[3, 4, 5]</td>
    <td>5</td>
    <td>2 (largest index of v in a[])</td>
  </tr>
</table>


### Test Execution:

```
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class BinarySearchTest {
    
    @Test
    public void testWithSingleValueArray() {
        int[] a = {1};
        int v = 1;
        int expected = 0;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithValueAtBeginning() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 1;
        int expected = 0;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithValueAtEnd() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 9;
        int expected = 4;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithValueInMiddle() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 5;
        int expected = 2;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithValueNotInArray1() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 4;
        int expected = -1;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithValueNotInArray2() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 11;
        int expected = -1;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
    
    @Test
    public void testWithEmptyArray() {
        int[] a = {};
        int v = 5;
        int expected = -1;
        int actual = binarySearch(a, v);
        assertEquals(expected, actual);
    }
}
```

### Problem 4 :

Here is the modified code for the `triangle` function in Java:

```
public class Triangle {
    final static int EQUILATERAL = 0;
    final static int ISOSCELES = 1;
    final static int SCALENE = 2;
    final static int INVALID = 3;

    public static int triangle(int a, int b, int c) {
        if (a >= b + c || b >= a + c || c >= a + b)
            return INVALID;
        if (a == b && b == c)
            return EQUILATERAL;
        if (a == b || a == c || b == c)
            return ISOSCELES;
        return SCALENE;
    }

    public static void main(String[] args) {
        int a = 3, b = 3, c = 3;
        int type = triangle(a, b, c);
        switch (type) {
            case EQUILATERAL:
                System.out.println("Triangle is equilateral");
                break;
            case ISOSCELES:
                System.out.println("Triangle is isosceles");
                break;
            case SCALENE:
                System.out.println("Triangle is scalene");
                break;
            case INVALID:
                System.out.println("Triangle is invalid");
                break;
        }
    }
}
```

### Equivalence Partitioning:

Valid Triangles:

- Three sides are of the same length (Equilateral)
- Two sides are of the same length (Isosceles)
- All three sides are of different lengths (Scalene)

Invalid Triangles:

- One side has a length of 0
- The sum of the lengths of two sides is less than or equal - to the length of the third side


<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: a=5, b=5, c=5</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=5, b=4, c=4</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=3, b=4, c=5</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=0, c=0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=-2, b=2, c=3</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Valid input: a=2, b=2, c=2</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=1, b=2, c=2</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=4, b=5, c=3</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=2, c=2</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=0, c=2</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=2, c=0</td>
    <td>INVALID</td>
  </tr>
</table>
</br>

### Boundary Value Analysis:

For this function, the minimum and maximum values for the sides of a triangle are not relevant. Instead, we need to test the boundaries where the behavior of the function might change.

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Invalid inputs: a = 0, b = 0, c = 0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid inputs: a + b = c or b + c = a or c + a = b (a=1, b=2, c=3)</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 1</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 100</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = b ≠ c = 50</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a ≠ b = c = 50</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = c ≠ b = 50</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Scalene triangles: a = b + c - 1 (a=2, b=3, c=4)</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: b = a + c - 1 (a=3, b=2, c=4)</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: c = a + b - 1 (a=4, b=3, c=2)</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Maximum values: a, b, c = 2147483647 (Integer.MAX_VALUE)</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Minimum values: a, b, c = -2147483648 (Integer.MIN_VALUE)</td>
    <td>INVALID</td>
  </tr>
</table>

### Test Execution:
```
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class TriangleTest {

    final int EQUILATERAL = 0;
    final int ISOSCELES = 1;
    final int SCALENE = 2;
    final int INVALID = 3;
    
    @Test
    public void testEquivalencePartitioning() {
        // Valid Triangles
        assertEquals(EQUILATERAL, triangle(5, 5, 5));
        assertEquals(ISOSCELES, triangle(4, 4, 6));
        assertEquals(SCALENE, triangle(3, 4, 5));
        
        // Invalid Triangles
        assertEquals(INVALID, triangle(0, 2, 3));
        assertEquals(INVALID, triangle(1, 1, 3));
        assertEquals(INVALID, triangle(2, 2, 4));
    }
    
    @Test
    public void testBoundaryValueAnalysis() {
        // Valid Triangles
        assertEquals(EQUILATERAL, triangle(1, 1, 1));
        assertEquals(EQUILATERAL, triangle(1000, 1000, 1000));
        assertEquals(INVALID, triangle(2, 2, 4)); // Two sides are equal to the third side
        assertEquals(ISOSCELES, triangle(5, 6, 6)); // Two sides are very close in length
        
        // Invalid Triangles
        assertEquals(INVALID, triangle(0, 2, 3));
        assertEquals(INVALID, triangle(1, 1, 3));
        assertEquals(INVALID, triangle(2, 2, 4));
        assertEquals(INVALID, triangle(4, 4, 7)); // One side is just above the sum of the other two sides
        assertEquals(INVALID, triangle(4, 4, 6)); // One side is just below the sum of the other two sides
    }
    
    // triangle function implementation
    private int triangle(int a, int b, int c) {
        if (a >= b+c || b >= a+c || c >= a+b)
            return(INVALID);
        if (a == b && b == c)
            return(EQUILATERAL);
        if (a == b || a == c || b == c)
            return(ISOSCELES);
        return(SCALENE);
    }
}
```

### Problem 5 :

Here is the modified code for the `prefix` function in Java:

```
public class Prefix {
    public static boolean prefix(String s1, String s2) {
        if (s1.length() > s2.length()) {
            return false;
        }
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) != s2.charAt(i)) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello world";
        if (prefix(s1, s2)) {
            System.out.println(s1 + " is a prefix of " + s2);
        } else {
            System.out.println(s1 + " is not a prefix of " + s2);
        }
    }
}
```

### Equivalence Partitioning:

- Valid prefix: "hello" in "hello world", "ab" in "abcde"
- Invalid prefix: "world" in "hello world", "xyz" in "abcde"

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid Inputs: s1 = "apple", s2 = "apple pie"</td>
    <td>true</td>
  </tr>
  <tr>
    <td>Valid Inputs: s1 = "t", s2 = "test"</td>
    <td>true</td>
  </tr>
  <tr>
    <td>Invalid Inputs: s1 = "", s2 = "hello world"</td>
    <td>false</td>
  </tr>
  <tr>
    <td>Invalid Inputs: s1 = "word", s2 = "hello world"</td>
    <td>false</td>
  </tr>
</table>

### Boundary Value Analysis:

- s1 and s2 are both empty strings: "" and ""
- s1 and s2 are the same string: "hello" and "hello"
- s1 is a prefix of s2: "he" in "hello", "abc" in "abcde"
- s1 is an empty string and s2 is a non-empty string: "" and "hello"
- s1 is a non-empty string and s2 is an empty string: "hello" and ""

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>s1 = "", s2 = "abc"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "a"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "abc", s2 = "abc"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "abcdefghijklmnopqrstuvwxyz", s2 = "abcdefghijklmnopqrstuvwxyz"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "abc"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = " "</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "abc", s2 = "ab"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "ab", s2 = "abc"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "b"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz"</td>
    <td>False</td>
  </tr>
</table>

### Test Execution:

```
import org.junit.Test;
import static org.junit.Assert.*;

public class PrefixTest {

    @Test
    public void testEmptyS1() {
        assertFalse(prefix("", "abc"));
    }
    
    @Test
    public void testPrefixExists() {
        assertTrue(prefix("ab", "abc"));
    }
    
    @Test
    public void testS1LongerThanS2() {
        assertFalse(prefix("abc", "ab"));
    }
    
    @Test
    public void testSingleCharPrefix() {
        assertTrue(prefix("a", "ab"));
    }
    
    @Test
    public void testVeryLongPrefix() {
        assertTrue(prefix("aaaaaaaaaaaaaaaaaaaaaa", "aaaaaaaaaaaaaaaaaaaaaab"));
    }
    
    @Test
    public void testEqualStrings() {
        assertTrue(prefix("abc", "abc"));
    }
    
    @Test
    public void testSingleCharS1() {
        assertFalse(prefix("a", "b"));
    }
    
    @Test
    public void testSingleCharEqualStrings() {
        assertTrue(prefix("a", "a"));
    }
    
    @Test
    public void testSingleCharDifferentStrings() {
        assertFalse(prefix("a", "b"));
    }
    
    @Test
    public void testSpaceInS2() {
        assertFalse(prefix("a", " "));
    }
}
```

### Problem 6:

### Equivalence Classes:

- Class 1: Invalid input (non-positive values)
- Class 2: Non-triangle (sum of any two sides is less than or equal to the third side)
- Class 3: Scalene triangle (all three sides have different lengths)
- Class 4: Isosceles triangle (two sides have the same length)
- Class 5: Equilateral triangle (all three sides have the same length)
- Class 6: Right-angled triangle (one angle is a right angle, determined by the Pythagorean theorem)

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>a = -5, b = -3, c = -4</td>
    <td>Invalid input</td>
  </tr>
  <tr>
    <td>a = 3, b = 3, c = 3</td>
    <td>Equilateral triangle</td>
  </tr>
  <tr>
    <td>a = 5, b = 5, c = 7</td>
    <td>Isosceles triangle</td>
  </tr>
  <tr>
    <td>a = 6, b = 8, c = 10</td>
    <td>Scalene right angled triangle</td>
  </tr>
  <tr>
    <td>a = 7, b = 10, c = 6</td>
    <td>Scalene right angled triangle</td>
  </tr>
  <tr>
    <td>a = 10, b = 6, c = 7</td>
    <td>Scalene right angled triangle</td>
  </tr>
  <tr>
    <td>a = 4, b = 5, c = 9</td>
    <td>Not a triangle</td>
  </tr>
</table>

### Test cases:

Class 1: Invalid input (non-positive values)
Test Case     | Expected Outcome
--------------|-----------------
a = -1, b = 2, c = 3 | Invalid input
a = 1, b = -1, c = 3 | Invalid input

Class 2: Non-triangle (sum of any two sides is less than or equal to the third side)
Test Case     | Expected Outcome
--------------|-----------------
a = 3, b = 4, c = 7 | Not a triangle
a = 2, b = 2, c = 5 | Not a triangle

Class 3: Scalene triangle (all three sides have different lengths)
Test Case     | Expected Outcome
--------------|-----------------
a = 3, b = 4, c = 5 | Scalene triangle
a = 6, b = 7, c = 8 | Scalene triangle

Class 4: Isosceles triangle (two sides have the same length)
Test Case     | Expected Outcome
--------------|-----------------
a = 2, b = 2, c = 3 | Isosceles triangle
a = 5, b = 5, c = 7 | Isosceles triangle

Class 5: Equilateral triangle (all three sides have the same length)
Test Case     | Expected Outcome
--------------|-----------------
a = 4, b = 4, c = 4 | Equilateral triangle
a = 6, b = 6, c = 6 | Equilateral triangle

Class 6: Right-angled triangle (one angle is a right angle, determined by the Pythagorean theorem)
Test Case     | Expected Outcome
--------------|-----------------
a = 3, b = 4, c = 5 | Right-angled triangle
a = 5, b = 3, c = 4 | Right-angled triangle

# Section B

1. Control Flow Graph (CFG):

![lab7 drawio](https://user-images.githubusercontent.com/75575802/232807047-f42d80e9-d618-412f-9259-25e2e466fb4e.png)

2. Test sets for each coverage criterion:

[a] Statement Coverage:

Test 1: p = `{new Point(0, 0), new Point(1, 1)}`

Test 2: p = `{new Point(0, 0), new Point(1, 0), new Point(2, 0)}`

[b] Branch Coverage:

Test 1: p = `{new Point(0, 0), new Point(1, 1)}`

Test 2: p = `{new Point(0, 0), new Point(1, 0), new Point(2, 0)}`

Test 3: p = `{new Point(0, 0), new Point(1, 0), new Point(1, 1)}`

[c] Basic Condition Coverage:

Test 1: p = `{new Point(0, 0), new Point(1, 1)}`

Test 2: p = `{new Point(0, 0), new Point(1, 0), new Point(2, 0)}`

Test 3: p = `{new Point(0, 0), new Point(1, 0), new Point(1, 1)}`

Test 4: p = `{new Point(0, 0), new Point(1, 0), new Point(0, 1)}`

Test 5: p = `{new Point(0, 0), new Point(0, 1), new Point(1, 1)}`
