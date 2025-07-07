#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
void repeat_and_print(int times, char *str) {
    for (int i = 0; i < times; i++) {
        printf("%s ", str);
    }
}
int main() {
    char input[] = "3[2[a],3[c]]";
    int i = 0, repeat_outer = 0, repeat_inner;
    char buffer[100], part[50];
    int buf_idx = 0;
       while (isdigit(input[i])) {
        repeat_outer = repeat_outer * 10 + (input[i] - '0');
        i++;
    }
    if (input[i] == '[') i++; 
       buffer[0] = '\0';
    while (input[i] && input[i] != ']') {
        repeat_inner = 0;
               while (isdigit(input[i])) {
            repeat_inner = repeat_inner * 10 + (input[i] - '0');
            i++;
        }
        if (input[i] == '[') i++;  
        int part_idx = 0;
        while (input[i] && isalpha(input[i])) {
            part[part_idx++] = input[i++];
        }
        part[part_idx] = '\0';

        if (input[i] == ']') i++; 
        if (input[i] == ',') i++;  
             for (int j = 0; j < repeat_inner; j++) {
            strcat(buffer, part);
            strcat(buffer, " ");
        }
    }
       for (int j = 0; j < repeat_outer; j++) {
        printf("%s", buffer);
    }
    printf("\n");
    return 0;
}
