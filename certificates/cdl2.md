```

#include <stdio.h>

char str[20];
int i = 0;

// A -> ab | a
int A() {
    if (str[i] == 'a') {
        i++;
        if (str[i] == 'b') {
            i++;
            return 1; // A -> ab
        }
        return 1; // A -> a
    }
    return 0;
}

// S -> cAd
int S() {
    if (str[i] == 'c') {
        i++;
        if (A()) {
            if (str[i] == 'd') {
                i++;
                return 1;
            }
        }
    }
    return 0;
}

int main() {
    int x;
    printf("Enter String: ");
    scanf("%s", str);
    x = S();

    // Check also that entire input is consumed
    if (x == 1 && str[i] == '\0') 
        printf("Accepted\n");
    else 
        printf("Not accepted\n");

    return 0;
}

```
