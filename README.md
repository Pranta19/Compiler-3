#include <stdio.h>
#include <string.h>
#include <ctype.h>

int isKeyword(char *word) {
    char *k[] = {"int", "float", "if", "else", "while", "return"};
    for (int i = 0; i < 6; i++)
        if (strcmp(word, k[i]) == 0) return 1;
    return 0;
}

int main() {
    char code[] = "int x = 10; float y = x + 5;";
    char token[20];
    int i = 0, j = 0;

    while (code[i] != '\0') {
        if (isalnum(code[i]) || code[i] == '_') {
            token[j++] = code[i];
        } else {
            token[j] = '\0';
            if (j > 0) {
                if (isKeyword(token)) printf("Keyword: %s\n", token);
                else if (isdigit(token[0])) printf("Number: %s\n", token);
                else printf("Identifier: %s\n", token);
                j = 0;
            }
            if (strchr("=+;-", code[i])) printf("Symbol: %c\n", code[i]);
        }
        i++;
    }

    return 0;
}
