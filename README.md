# Integer-to-English-Words

Convert a non-negative integer num to its English words representation.

Example 1:

Input: num = 123
Output: "One Hundred Twenty Three"
Example 2:

Input: num = 12345
Output: "Twelve Thousand Three Hundred Forty Five"
Example 3:

Input: num = 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
 

Constraints:

0 <= num <= 231 - 1

# SOLUTION 

* Intuition

The goal is to convert an integer into its English words representation. The solution breaks down the number into manageable parts (thousands, millions, billions) and converts each part into words using predefined mappings for single digits, teens, and tens. By systematically processing each segment, we can build the full English representation of the number.

* Approach
  
Base Case: If the number is 0, return "Zero".
Segmenting the Number: The number is divided into groups of three digits (thousands, millions, billions) using integer division and modulus operations.
Mapping Numbers to Words: For each group:
Use a helper function to convert numbers less than 1000 into words.
Append the corresponding scale (Thousand, Million, Billion) to the result.
Concatenation: Build the final string by concatenating the words for each group, ensuring proper spacing.
Trimming: Remove any trailing spaces from the final result.

Time Complexity
The time complexity of the algorithm is O(n), where n is the number of digits in the input number. Each group of three digits is processed separately, and the conversion for each group is constant time due to the fixed number of mappings.

Space Complexity
The space complexity is O(1) if we consider the space used for the output string as part of the result. However, if we consider the output string separately, it can be considered O(m), where m is the length of the output string.

Step-by-Step Solution
For num = 123

Initial Input:

num = 123
Check if num == 0: It is not, so we proceed.
Processing the Thousands:

Call numberToWordsHelper(123 % 1000) which is numberToWordsHelper(123).
Inside numberToWordsHelper(123):
result = ""
Since 123 > 99, append "One Hundred " (because 123 / 100 = 1).
Update num = 123 % 100 = 23.
Since 23 >= 20, append "Twenty " (because 23 / 10 = 2).
Update num = 23 % 10 = 3.
Append "Three " (because 3 > 0).
Return result = "One Hundred Twenty Three ".
Final Assembly:

Now, result = "One Hundred Twenty Three ".
Since num is 0, there are no more groups to process (millions or billions).
Trim the trailing space: result = "One Hundred Twenty Three".
Output:

The final output for num = 123 is "One Hundred Twenty Three".

# JAVA CODE 

class Solution {

    public String numberToWords(int num) {
    
    if(num == 0)
    
        return "Zero";
        
    String[] bigString = new String[]{"Thousand","Million","Billion"};
    
    String result =  numberToWordsHelper(num%1000);
    
    num = num/1000;
    
    if(num > 0 && num%1000>0){
    
        result = numberToWordsHelper(num%1000) + "Thousand " + result;
    }
    num = num/1000;
    
    if(num > 0 && num%1000>0){
    
        result = numberToWordsHelper(num%1000) + "Million " + result;
        
    }
    num = num/1000;
    
    if(num > 0){
    
        result = numberToWordsHelper(num%1000) + "Billion " + result;
    }
    
    return result.trim();
}

public String numberToWordsHelper(int num){

    String[] digitString = new String[]{"Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
    
    String[] teenString = new String[]{"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen","Eighteen", "Nineteen"};
    
    String[] tenString = new String[]{"","","Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    
    String result = "";
    
    if(num > 99){
    
        result += digitString[num/100] + " Hundred ";
    }
    num = num % 100;
    
    if(num < 20 && num > 9){
    
        result += teenString[num%10]+" ";
        
    }else{
    
        if(num > 19){
        
            result += tenString[num/10]+" ";
        }
        num = num % 10;
        
        if(num > 0)
        
            result += digitString[num]+" ";
    }
    return result;
}
}
