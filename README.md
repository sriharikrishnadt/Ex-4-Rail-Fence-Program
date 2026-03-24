# Ex-5 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void encrypt(char *plaintext, char *key, char *ciphertext) {
    int textLen = strlen(plaintext);
    int keyLen  = strlen(key);

    for (int i = 0, j = 0; i < textLen; i++) {
        char currentChar = plaintext[i];

        if (isalpha(currentChar)) {
            char base = isupper(currentChar) ? 'A' : 'a';
            int keyShift = tolower(key[j % keyLen]) - 'a';

            ciphertext[i] = (currentChar - base + keyShift) % 26 + base;
            j++;
        } else {
            ciphertext[i] = currentChar;
        }
    }

    ciphertext[textLen] = '\0';
}

void decrypt(char *ciphertext, char *key, char *plaintext) {
    int textLen = strlen(ciphertext);
    int keyLen  = strlen(key);

    for (int i = 0, j = 0; i < textLen; i++) {
        char currentChar = ciphertext[i];

        if (isalpha(currentChar)) {
            char base = isupper(currentChar) ? 'A' : 'a';
            int keyShift = tolower(key[j % keyLen]) - 'a';

            plaintext[i] = (currentChar - base - keyShift + 26) % 26 + base;
            j++;
        } else {
            plaintext[i] = currentChar;
        }
    }

    plaintext[textLen] = '\0';
}

int main() {
    char plaintext[1024];
    char key[1024];
    char ciphertext[1024];
    char decrypted[1024];

    printf("Enter plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("Enter key (alphabetic only): ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';

    encrypt(plaintext, key, ciphertext);
    printf("Encrypted text: %s\n", ciphertext);

    decrypt(ciphertext, key, decrypted);
    printf("Decrypted text: %s\n", decrypted);

    return 0;
}

```

# OUTPUT:

<img width="1700" height="886" alt="image" src="https://github.com/user-attachments/assets/9e2a723d-6ad3-468e-a0fa-19a952ab14ad" />


# RESULT:

 The implement of Vigenere Cipher substitution technique using C program is successful.
