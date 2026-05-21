<h1>ExpNo 8 : Solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python</h1> 
<h3>Name: ALMAS AASMEEN J               </h3>
<h3>Register Number/Staff Id: 212224060016       </h3>
<H3>Aim:</H3>
<p>
    To solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python
</p>
<h3>Procedure:</h3>
Input and Output
<br>Input:
This algorithm will take three words.
<br> B A S E<br>
    B A L L<br>
           ----------<br>
           G A M E S<br>

Output:
It will show which letter holds which number from 0 – 9.
For this case it is like this.

              B A S E                         2 4 6 1
              B A L L                         2 4 5 5
             ---------                       ---------
            G A M E S                       0 4 9 1 6
Algorithm
For this problem, we will define a node, which contains a letter and its corresponding values.<br>

isValid(nodeList, count, word1, word2, word3)<br>

Input − A list of nodes, the number of elements in the node list and three words.<br>

Output − True if the sum of the value for word1 and word2 is same as word3 value.<br>

Begin<br>
   m := 1<br>
   for each letter i from right to left of word1, do<br>
      ch := word1[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>
      val1 := val1 + (m * nodeList[j].value)<br>
      m := m * 10<br>
   done<br>

   m := 1<br>
   for each letter i from right to left of word2, do<br>
      ch := word2[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val2 := val2 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   m := 1<br>
   for each letter i from right to left of word3, do<br>
      ch := word3[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val3 := val3 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   if val3 = (val1 + val2), then<br>
      return true<br>
   return false<br>
End<br>
<hr>
<h2>Sample Input and Output:</h2>
SEND = 9567<br>
MORE = 1085<br>
<hr>
MONEY = 10652<br>
<hr>

# Define a Node structure (letter + assigned value)
class Node:
    def __init__(self, letter, value):
        self.letter = letter
        self.value = value

# Function to calculate the numeric value of a word based on assigned values
def word_value(word, nodeList):
    m = 1
    val = 0
    for i in range(len(word) - 1, -1, -1):  # right to left
        ch = word[i]
        for node in nodeList:
            if node.letter == ch:
                val += m * node.value
                break
        m *= 10
    return val

# Validation function: checks if word1 + word2 = word3
def isValid(nodeList, word1, word2, word3):
    val1 = word_value(word1, nodeList)
    val2 = word_value(word2, nodeList)
    val3 = word_value(word3, nodeList)
    return val3 == (val1 + val2)

# Main driver function
from itertools import permutations

def solve(word1, word2, word3):
    letters = set(word1 + word2 + word3)
    letters = list(letters)
    if len(letters) > 10:
        print("Too many unique letters!")
        return

    for perm in permutations(range(10), len(letters)):
        nodeList = [Node(letters[i], perm[i]) for i in range(len(letters))]

        # Leading letters cannot be zero
        if any(node.value == 0 and node.letter in [word1[0], word2[0], word3[0]] for node in nodeList):
            continue

        if isValid(nodeList, word1, word2, word3):
            print("Solution Found:")
            for node in nodeList:
                print(f"{node.letter} = {node.value}")
            print(f"\n{word1} = {word_value(word1, nodeList)}")
            print(f"{word2} = {word_value(word2, nodeList)}")
            print(f"{word3} = {word_value(word3, nodeList)}")
            return  # Stop after finding the first valid solution

    print("No solution found.")

# Example usage:
solve("SEND", "MORE", "MONEY")

<img width="663" height="502" alt="image" src="https://github.com/user-attachments/assets/625e2911-aac2-4cd3-a481-1584c22f3ba2" />

<h2>Result:</h2>
<p> Thus a Cryptarithmetic Problem was solved using Python successfully</p>

