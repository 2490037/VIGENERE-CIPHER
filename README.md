## VIGENERE-CIPHER


## EX. NO: 4 
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>


void generateKey(char text[], char key[], char newKey[]) {
    int textLen = strlen(text);
    int keyLen = strlen(key);
    int i, j = 0;

    for (i = 0; i < textLen; i++) {
        if (isalpha(text[i])) {
            newKey[i] = toupper(key[j % keyLen]);
            j++;
        } else {
            newKey[i] = text[i]; 
        }
    }
    newKey[i] = '\0';
}


void encrypt(char text[], char key[], char cipher[]) {
    int len = strlen(text);

    for (int i = 0; i < len; i++) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            cipher[i] = ((toupper(text[i]) - 'A' + (key[i] - 'A')) % 26) + base;
        } else {
            cipher[i] = text[i]; 
        }
    }
    cipher[len] = '\0';
}


void decrypt(char cipher[], char key[], char plain[]) {
    int len = strlen(cipher);

    for (int i = 0; i < len; i++) {
        if (isalpha(cipher[i])) {
            char base = isupper(cipher[i]) ? 'A' : 'a';
            plain[i] = ((toupper(cipher[i]) - 'A' - (key[i] - 'A') + 26) % 26) + base;
        } else {
            plain[i] = cipher[i];
        }
    }
    plain[len] = '\0';
}

int main() {
    char text[200], key[200], newKey[200], cipher[200], decrypted[200];

    printf("Enter text: ");
    scanf("%[^\n]s", text);

    printf("Enter key: ");
    scanf("%s", key);

    generateKey(text, key, newKey);

    encrypt(text, newKey, cipher);
    printf("Encrypted Text: %s\n", cipher);

    decrypt(cipher, newKey, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}
~~~
## OUTPUT
<img width="1915" height="1148" alt="Screenshot 2025-09-13 092157" src="https://github.com/user-attachments/assets/d92f2e11-c9d0-480e-b2d7-0ab7c3e261b3" />

## RESULT
The program has been successfully created and verified.
