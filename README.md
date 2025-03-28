# Cryptography---19CS412-classical-techqniques

# Caeser Cipher

Using Caeser Cipher method with different key values.

## AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.

2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.

3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.

4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26

5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:

DEVELOPED BY : AMRUTHAVARSHINI GOPAL

REGISTER NO : 212223230013
```
#include <stdio.h> 
#include <string.h> 
 
#include <ctype.h> 
void main() 
 
{ 
    char plain[10],cipher[10]; 
    int key,i,length; 
    int result; 
    printf("\n Enter the plain text:"); 
    scanf("%s", plain); 
    printf("\n Enter the key value:"); 
    scanf("%d", &key); 
    printf("\n \n \t PLAIN TEXt: %s", plain); 
    printf("\n \n \t ENCRYPTED TEXT:"); 
    for(i=0, length = strlen(plain); i<length; i++) 
    { 
         
        cipher[i]=plain[i] + key; 
        if (isupper(plain[i]) && (cipher[i] > 'Z')) 
        cipher[i] = cipher[i] - 26; 
        if (islower(plain[i]) && (cipher[i] > 'z')) 
        cipher[i] = cipher[i] - 26; 
        printf("%c", cipher[i]); 
 
    } 
    printf("\n \n \t AFTER DECRYPTION : "); 
    for(i=0;i<length;i++) 
    { 
         
        plain[i]=cipher[i]-key; 
        if(isupper(cipher[i])&&(plain[i]<'A')) 
        plain[i]=plain[i]+26; 
        if(islower(cipher[i])&&(plain[i]<'a')) 
        plain[i]=plain[i]+26; 
        printf("%c",plain[i]); 
    }    
}
```

## OUTPUT:

Simulating Caesar Cipher

![image](https://github.com/user-attachments/assets/9a36deb8-b9bd-4602-b492-83ee22359374)

Input : amrutha

Encrypted Message : cotwvjc 

Decrypted Message : amrutha

## RESULT:

The program is executed successfully.

---------------------------------

# PlayFair Cipher

Using Playfair Cipher method with different key values.

## AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:

The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:

1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.

2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).

3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).

4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.

To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:

DEVELOPED BY : AMRUTHAVARSHINI GOPAL

REGISTER NO : 212223230013
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#define SIZE 30
// Function to convert the string to lowercase
void toLowerCase(char plain[], int ps) {
    for (int i = 0; i < ps; i++) {
        if (plain[i] >= 'A' && plain[i] <= 'Z') {
            plain[i] += 32; // Convert to lowercase
        }
    }
}
// Function to remove all spaces in a string
int removeSpaces(char *plain, int ps) {
    int count = 0;
    for (int i = 0; i < ps; i++) {
        if (plain[i] != ' ') {
            plain[count++] = plain[i];
        }
    }
    plain[count] = '\0';
    return count;
}
// Function to generate the 5x5 key square
void generateKeyTable(char key[], int ks, char keyT[5][5]) {
    int i, j, k;
    int *dicty = (int *)calloc(26, sizeof(int)); // A 26 character hashmap to store count of the alphabet

    for (i = 0; i < ks; i++) {
        if (key[i] != 'j') {
            dicty[key[i] - 97] = 2;
        }
    }
    dicty['j' - 97] = 1;

    i = 0;
    j = 0;
    for (k = 0; k < ks; k++) {
        if (dicty[key[k] - 97] == 2) {
            dicty[key[k] - 97] -= 1;
            keyT[i][j] = key[k];
            j++;
            if (j == 5) {
                i++;
                j = 0;
            }
        }
    }

    for (k = 0; k < 26; k++) {
        if (dicty[k] == 0) {
            keyT[i][j] = (char)(k + 97);
            j++;
            if (j == 5) {
                i++;
                j = 0;
            }
        }
    }
    free(dicty);
}
// Function to search for the characters of a digraph in the key square and return their position
void search(char keyT[5][5], char a, char b, int arr[]) {
    if (a == 'j') a = 'i';
    if (b == 'j') b = 'i';

    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (keyT[i][j] == a) {
                arr[0] = i;
                arr[1] = j;
            } else if (keyT[i][j] == b) {
                arr[2] = i;
                arr[3] = j;
            }
        }
    }
}
// Function to find the modulus with 5
int mod5(int a) {
    return (a % 5);
}
// Function for preparing the plaintext
int prepare(char str[], int *ptrs) {
    // Handle odd length by adding a filler character
    if (*ptrs % 2 != 0) {
        str[(*ptrs)++] = 'x';
    }
    str[*ptrs] = '\0';
    return *ptrs;
}
// Function for performing the encryption
void encrypt(char str[], char keyT[5][5], int ps) {
    int a[4];
    for (int i = 0; i < ps; i += 2) {
        if (i + 1 == ps) { // If odd length and no filler, skip last character
            break;
        }
        search(keyT, str[i], str[i + 1], a);
        if (a[0] == a[2]) {
            str[i] = keyT[a[0]][mod5(a[1] + 1)];
            str[i + 1] = keyT[a[0]][mod5(a[3] + 1)];
        } else if (a[1] == a[3]) {
            str[i] = keyT[mod5(a[0] + 1)][a[1]];
            str[i + 1] = keyT[mod5(a[2] + 1)][a[1]];
        } else {
            str[i] = keyT[a[0]][a[3]];
            str[i + 1] = keyT[a[2]][a[1]];
        }
    }
}
// Function for performing the decryption
void decrypt(char str[], char keyT[5][5], int ps) {
    int a[4];

    for (int i = 0; i < ps; i += 2) {
        if (i + 1 == ps) { // If odd length and no filler, skip last character
            break;
        }
        search(keyT, str[i], str[i + 1], a);
        if (a[0] == a[2]) {
            str[i] = keyT[a[0]][mod5(a[1] + 4)];
            str[i + 1] = keyT[a[0]][mod5(a[3] + 4)];
        } else if (a[1] == a[3]) {
            str[i] = keyT[mod5(a[0] + 4)][a[1]];
            str[i + 1] = keyT[mod5(a[2] + 4)][a[1]];
        } else {
            str[i] = keyT[a[0]][a[3]];
            str[i + 1] = keyT[a[2]][a[1]];
        }
    }
    // Remove trailing filler character 'x' if it was added
    if (ps > 0 && str[ps - 1] == 'x') {
        str[ps - 1] = '\0';
    }
}
// Function to encrypt using Playfair Cipher
void encryptByPlayfairCipher(char str[], char key[]) {
    char keyT[5][5];
    int ks, ps;
    ks = strlen(key);
    ks = removeSpaces(key, ks);
    toLowerCase(key, ks);
    ps = strlen(str);
    toLowerCase(str, ps);
    ps = removeSpaces(str, ps);
    ps = prepare(str, &ps); // Prepare plaintext
    generateKeyTable(key, ks, keyT);
    encrypt(str, keyT, ps);
}
// Function to decrypt using Playfair Cipher
void decryptByPlayfairCipher(char str[], char key[]) {
    char keyT[5][5];
    int ks, ps;
    ks = strlen(key);
    ks = removeSpaces(key, ks);
    toLowerCase(key, ks);
    ps = strlen(str);
    toLowerCase(str, ps);
    ps = removeSpaces(str, ps);
    generateKeyTable(key, ks, keyT);
    decrypt(str, keyT, ps);
}
// Driver code
int main() {
    char str[SIZE], key[SIZE];
    // Get input from user
    printf("Enter the key: ");
    fgets(key, SIZE, stdin);
    key[strcspn(key, "\n")] = '\0'; // Remove trailing newline
    printf("Enter the plaintext: ");
    fgets(str, SIZE, stdin);
    str[strcspn(str, "\n")] = '\0'; // Remove trailing newline
    // Encrypt using Playfair Cipher
    encryptByPlayfairCipher(str, key);
    printf("Cipher text: %s\n", str);
    // Decrypt the ciphertext
    decryptByPlayfairCipher(str, key);
    printf("Decrypted text: %s\n", str);
    return 0;
}
```

## OUTPUT:

![image](https://github.com/user-attachments/assets/c852a00a-e276-40d7-abd1-2f97ad3c3e5e)

Key text: hello 

Plain text: hey 

Cipher text: hello

## RESULT:

The program is executed successfully.

---------------------------

# Hill Cipher

Using Hill Cipher method with different key values.

## AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:

The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.

To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).

The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.

## PROGRAM:

DEVELOPED BY : AMRUTHAVARSHINI GOPAL

REGISTER NO : 212223230013
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
// Hill cipher key matrix and its inverse
int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
// Key array for mapping
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
// Encode function
void encode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}
// Decode function
void decode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0';
}
int main() {
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;
    strcpy(msg, "amrutha");
    printf("Simulation of Hill Cipher\n");
    printf("Input message : %s\n", msg);
    // Convert message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }
    // Remove spaces (if needed)
    n = strlen(msg) % 3;
    // Append padding text 'X' if needed
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }
    printf("Padded message : %s\n", msg);
    // Encoding
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char ret[4];
        encode(a, b, c, ret);
        strcat(enc, ret);
    }
    printf("Encoded message : %s\n", enc);
    // Decoding
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char ret[4];
        decode(a, b, c, ret);
        strcat(dec, ret);
    }
    printf("Decoded message : %s\n", dec);
    return 0;
}
```
## OUTPUT:

Simulating Hill Cipher

![image](https://github.com/user-attachments/assets/cffdf0bf-088c-46b8-9847-2da09b3ba228)

Input Message : amrutha

Padded Message : AMRUTHAXX

Encrypted Message : GSPUHNOLR 

Decrypted Message : AMRUTHAXX

## RESULT:

The program is executed successfully.

-------------------------------------------------

# Vigenere Cipher

Using Vigenere Cipher method with different key values.

## AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:

The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:

DEVELOPED BY : AMRUTHAVARSHINI GOPAL

REGISTER NO : 212223230013
```
#include <stdio.h>
#include <string.h>
// Function to perform Vigenere encryption
void vigenereEncrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);
    for (int i = 0; i < textLen; i++) {
        char c = text[i];
        if (c >= 'A' && c <= 'Z') {
            // Encrypt uppercase letters
            text[i] = ((c - 'A' + key[i % keyLen] - 'A') % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            // Encrypt lowercase letters
            text[i] = ((c - 'a' + key[i % keyLen] - 'A') % 26) + 'a';
        }
    }
}
// Function to perform Vigenere decryption
void vigenereDecrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);
    for (int i = 0; i < textLen; i++) {
        char c = text[i];

        if (c >= 'A' && c <= 'Z') {
            // Decrypt uppercase letters
            text[i] = ((c - 'A' - (key[i % keyLen] - 'A') + 26) % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            // Decrypt lowercase letters
            text[i] = ((c - 'a' - (key[i % keyLen] - 'A') + 26) % 26) + 'a';
        }
    }
}
int main() {
    const char *key = "VAR"; 
    char message[] = "saveethaengineeringcollege";
    printf("Simulating Vigenere Cipher:\n");
    // Print the original plain text
    printf("Original Message: %s\n", message);
    // Print the key used
    printf("Key: %s\n", key);
    // Encrypt the message
    vigenereEncrypt(message, key);
    printf("Encrypted Message: %s\n", message);
    // Decrypt the message back to the original
    vigenereDecrypt(message, key);
    printf("Decrypted Message: %s\n", message);
    return 0;
}
```
## OUTPUT:

Simulating Vigenere Cipher

![image](https://github.com/user-attachments/assets/baff8b81-9230-4620-a083-f1ff252d94d9)

Input Message : saveethaengineeringcollege

Encrypted Message : namzekcavigzievmiebcfglvbe

Decrypted Message : saveethaengineeringcollege

## RESULT:

The program is executed successfully.

-----------------------------------------------------------------------

# Rail Fence Cipher

Using Rail Fence Cipher method with different key values.

## AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:

In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:

DEVELOPED BY : AMRUTHAVARSHINI GOPAL

REGISTER NO : 212223230013
```
#include <stdio.h>
#include <string.h>
int main() {
    int i, j, len, rails, count, dir;
    char str[1000];
    int code[100][1000] = {0};  // Initialize the entire array to 0
    printf("Enter a Secret Message:\n");
    scanf("%s",str);
    len = strlen(str);
    printf("Enter number of rails:\n");
    scanf("%d", &rails);
    count = 0;
    i = 0;
    dir = 1;  
    for (j = 0; j < len; j++) {
        code[i][j] = str[j];
        // Change direction if we reach the top or bottom rail
        if (i == 0) {
            dir = 1;
        } else if (i == rails - 1) {
            dir = -1;
        }
        i += dir;
    }
    printf("Encrypted Message:\n");
    // Print the encrypted message
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] != 0) {
                printf("%c", code[i][j]);
            }
        }
    }
    printf("\n");
    return 0;
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/ca3fc962-1bad-4391-a1fa-fd1eb596c6e7)

Enter a Secret Message: amrutha

Enter number of rails: 3

Encrypted Message: atmuhra

## RESULT:

The program is executed successfully.
