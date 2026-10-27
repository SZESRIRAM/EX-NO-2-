## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.

STEP-2: Read the keyword from the user.

STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.

STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.

STEP-5: Display the obtained cipher text.




Program:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
int main()
{
    char key[100], text[200], prepared[400];
    char cipher[400], decrypted[400], matrix[5][5];
    int used[26] = {0};
    int i, j, k = 0, len = 0;
    int r1, c1, r2, c2;
    char a, b, temp;
    printf("Enter the keyword: ");
    scanf("%99s", key);
    printf("Enter the plaintext: ");
    scanf("%199s", text);
    for (i = 0; key[i] != '\0'; i++)
    {
        temp = tolower(key[i]);
        if (temp == 'j')
            temp = 'i';
        if (temp >= 'a' && temp <= 'z' && !used[temp - 'a'])
        {
            matrix[k / 5][k % 5] = temp;
            used[temp - 'a'] = 1;
            k++;
        }
    }
    used['j' - 'a'] = 1;
    for (i = 0; i < 26; i++)
    {
        if (!used[i])
        {
            matrix[k / 5][k % 5] = 'a' + i;
            k++;
        }
    }
    printf("\nKey Matrix:\n");
    for (i = 0; i < 5; i++)
    {
        for (j = 0; j < 5; j++)
            printf("%c ", matrix[i][j]);
        printf("\n");
    }
    for (i = 0; text[i] != '\0'; i++)
    {
        text[i] = tolower(text[i]);
        if (text[i] == 'j')
            text[i] = 'i';
    }
    i = 0;
    while (text[i] != '\0')
    {
        a = text[i++];
        prepared[len++] = a;
        if (text[i] == '\0' || a == text[i])
        {
            prepared[len++] = (a == 'x') ? 'q' : 'x';
        }
        else
        {
            prepared[len++] = text[i++];
        }
    }
    prepared[len] = '\0';
    for (i = 0; i < len; i += 2)
    {
        a = prepared[i];
        b = prepared[i + 1];
        for (j = 0; j < 25; j++)
        {
            if (matrix[j / 5][j % 5] == a)
            {
                r1 = j / 5;
                c1 = j % 5;
            }
            if (matrix[j / 5][j % 5] == b)
            {
                r2 = j / 5;
                c2 = j % 5;
            }
        }
        if (r1 == r2)
        {
            cipher[i] = matrix[r1][(c1 + 1) % 5];
            cipher[i + 1] = matrix[r2][(c2 + 1) % 5];
        }
        else if (c1 == c2)
        {
            cipher[i] = matrix[(r1 + 1) % 5][c1];
            cipher[i + 1] = matrix[(r2 + 1) % 5][c2];
        }
        else
        {
            cipher[i] = matrix[r1][c2];
            cipher[i + 1] = matrix[r2][c1];
        }
    }
    cipher[len] = '\0';
    printf("\nEncrypted text: %s\n", cipher);
    for (i = 0; i < len; i += 2)
    {
        a = cipher[i];
        b = cipher[i + 1];
        for (j = 0; j < 25; j++)
        {
            if (matrix[j / 5][j % 5] == a)
            {
                r1 = j / 5;
                c1 = j % 5;
            }
            if (matrix[j / 5][j % 5] == b)
            {
                r2 = j / 5;
                c2 = j % 5;
            }
        }
        if (r1 == r2)
        {
            decrypted[i] = matrix[r1][(c1 + 4) % 5];
            decrypted[i + 1] = matrix[r2][(c2 + 4) % 5];
        }
        else if (c1 == c2)
        {
            decrypted[i] = matrix[(r1 + 4) % 5][c1];
            decrypted[i + 1] = matrix[(r2 + 4) % 5][c2];
        }
        else
        {
            decrypted[i] = matrix[r1][c2];
            decrypted[i + 1] = matrix[r2][c1];
        }
    }
    decrypted[len] = '\0';
    if (len > 0 && decrypted[len - 1] == 'x')
        decrypted[len - 1] = '\0';
    printf("Decrypted text: %s\n", decrypted);
    return 0;
}
```





Output:
<img width="251" height="200" alt="image" src="https://github.com/user-attachments/assets/df6fa681-5d43-4d24-a0ec-d86be20e77c8" />
