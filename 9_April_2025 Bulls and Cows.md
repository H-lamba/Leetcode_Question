# Bulls and Cows

**Description :-** You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:
- The number of "bulls", which are digits in the guess that are in the correct position.
- The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.
The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

## Examples

```
 

Example 1:

Input: secret = "1807", guess = "7810"
Output: "1A3B"
Explanation: Bulls are connected with a '|' and cows are underlined:
"1807"
  |
"7810"
Example 2:

Input: secret = "1123", guess = "0111"
Output: "1A1B"
Explanation: Bulls are connected with a '|' and cows are underlined:
"1123"        "1123"
  |      or     |
"0111"        "0111"
Note that only one of the two unmatched 1s is counted as a cow since the non-bull digits can only be rearranged to allow one 1 to be a bull.

```


## My Approach

Initialize counters for bulls and cows.
First pass through secret and guess:
- If characters at the same position match → it's a bull.
- Else, store unmatched characters in two maps: secretMap and guessMap.
Second pass:
- For each character in guessMap, check if it exists in secretMap.
- If yes, add the minimum count from both maps to cows (since only the common minimum can form cows).
Return result in the format "xAyB" (e.g., "1A2B").

## Code 
``` cpp
class Solution {
public:
    string getHint(string secret, string guess) {
        int bulls = 0;
        int cows = 0;
        unordered_map <char, int> shash;
        unordered_map <char , int> ghash;
        for(int i = 0; i<secret.size(); i++)
        {
                if(secret[i]== guess[i])
                bulls++;
                else
                {
                    shash[secret[i]]++;
                    ghash[guess[i]]++;
                }
        }
        for(auto i : ghash)
        {
            char ch = i.first;
            if(shash.count(ch))
            {
                cows = cows+min(shash[ch],i.second);
            }
        }
     return to_string(bulls) + "A" + to_string(cows) + "B";
    }
};
```

Thanks for visiting 😊
