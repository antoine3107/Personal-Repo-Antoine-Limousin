## Testing

# I] Summary of the purpose of the code tested

The code I have modified and tested involves resetting the display of a hangman game. 
It updates the hangman image, displays the hidden word and updates the number of remaining attempts.

Here is the code I worked on, before and then after the changes made.

```
 /*!
	 * Resets the display to the initial image and
	 * the appropriate number of visible labels
	 */
 private void ResetDisplay(string word)
 {
     
 }
```

```
 /*!
	 * Resets the display to the initial image and
	 * the appropriate number of visible labels
	 */
 private void ResetDisplay(string word)
 {
     // Reset hangman image and update UI for hidden word and remaining attempts.

     for (int i = 0; i < 12; i++)
     {
         if (i < word.Length)
         {
             char letter = word[i];
             Label letterLabel = this.FindByName<Label>("Letter" + (i + 1));
             letterLabel.Text = char.IsWhiteSpace(letter) ? " " : letter.ToString();
         }
         else
         {
             Label letterLabel = this.FindByName<Label>("Letter" + (i + 1));
             letterLabel.Text = " ";
         }
     }

     RemainingAttemptsLabel.Text = $"Remaining Attempts: {remainingAttempts}";
 }
```

The code I provide resets the display, updating the labels corresponding to the letters of the hidden word and displaying the number of remaining attempts.

The purpose of the test is to check that the display reset is working as expected. 
It checks whether the letters of the word are correctly displayed or hidden and whether the number of remaining attempts is correctly displayed.

## II] Importance of testing

It is essential to test the display reset in a hangman game, as this ensures that the user interface correctly reflects the state of the game. 
Players need to see the hidden word correctly updated, the letters correctly displayed or hidden, and the number of remaining attempts. 
Errors in this part of the code could mislead players and affect the game experience.

Limitations of the tests :

A potential limitation of these tests is that they only check the user interface, but do not guarantee that the underlying game logic is correct. 
For example, the code may display the hidden word correctly, but this does not necessarily mean that the game awards points correctly or declares a win or loss. 
Another limitation is that the tests do not check the robustness of the code in the face of incorrect or malicious input.

## III] Why the original code may not have included these tests

The original code may not have included these tests for a number of reasons. The original developer may have assumed that resetting the display was a simple task and worked correctly without the need for detailed testing. 
However, it is important to stress that tests are essential to ensure the robustness of the code, particularly in interactive applications such as games.