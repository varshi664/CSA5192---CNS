#include <stdio.h>
#include <string.h>

// Function to remove spaces and duplicate letters from the key
void preprocessKey(char *key) {
    int i, j, k = 0;
    int keyLen = strlen(key);
    int table[26] = {0};
    
    for (i = 0; i < keyLen; i++) {
        if (key[i] == ' ') {
            continue;
        }
        if (!table[key[i] - 'A']) {
            key[k++] = key[i];
            table[key[i] - 'A'] = 1;
        }
    }
    
    for (i = 0; i < 26; i++) {
        if (i != ('J' - 'A') && !table[i]) {
            key[k++] = 'A' + i;
        }
    }
    key[k] = '\0';
}

// Function to generate the Playfair cipher table
void generatePlayfairTable(char *key, char table[5][5]) {
    int keyLen = strlen(key);
    int k = 0;

    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            table[i][j] = key[k++];
        }
    }
}

// Function to find the row and column of a character in the Playfair table
void findPosition(char table[5][5], char ch, int *row, int *col) {
    if (ch == 'J') ch = 'I';
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (table[i][j] == ch) {
                *row = i;
                *col = j;
                return;
            }
        }
    }
}

// Function to encrypt a digraph using the Playfair cipher
void encryptPlayfair(char table[5][5], char in1, char in2, char *out1, char *out2) {
    int row1, col1, row2, col2;
    findPosition(table, in1, &row1, &col1);
    findPosition(table, in2, &row2, &col2);

    if (row1 == row2) {
        *out1 = table[row1][(col1 + 1) % 5];
        *out2 = table[row2][(col2 + 1) % 5];
    } else if (col1 == col2) {
        *out1 = table[(row1 + 1) % 5][col1];
        *out2 = table[(row2 + 1) % 5][col2];
    } else {
        *out1 = table[row1][col2];
        *out2 = table[row2][col1];
    }
}

int main() {
    char key[50];
    char plaintext[100];
    char ciphertext[100];
    char table[5][5];
    
    printf("Enter the key (no spaces, all caps): ");
    scanf("%s", key);
    
    printf("Enter the plaintext (all caps): ");
    scanf("%s", plaintext);
    
    preprocessKey(key);
    generatePlayfairTable(key, table);
    
    int i = 0;
    int length = strlen(plaintext);
    int outIndex = 0;
    
    while (i < length) {
        char in1, in2, out1, out2;
        in1 = plaintext[i];
        i++;
        
        if (i < length) {
            in2 = plaintext[i];
        } else {
            in2 = 'X';
        }
        
        encryptPlayfair(table, in1, in2, &out1, &out2);
        ciphertext[outIndex++] = out1;
        ciphertext[outIndex++] = out2;
        i++;
    }
    
    ciphertext[outIndex] = '\0';
    
    printf("Ciphertext: %s\n", ciphertext);
    
    return 0;
}
