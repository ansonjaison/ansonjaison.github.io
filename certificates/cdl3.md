```

#include <stdio.h>
#include <string.h>

char str[100];
int i = 0;
int E();
int E_();
int T();
int T_();
int F();

// Match "id"
int match_id() {
    if (str[i] == 'i' && str[i + 1] == 'd') {
        i += 2;
        return 1;
    }
    return 0;
}

// F → (E) | id
int F() {
    if (str[i] == '(') {
        i++;
        if (E()) {
            if (str[i] == ')') {
                i++;
                return 1;
            }
        }
        return 0;
    }
    return match_id();
}

// T' → * F T' | ε
int T_() {
    if (str[i] == '*') {
        i++;
        if (F()) return T_();
        return 0;
    }
    return 1;  // ε
}

// T → F T'
int T() {
    if (F()) return T_();
    return 0;
}

// E' → + T E' | ε
int E_() {
    if (str[i] == '+') {
        i++;
        if (T()) return E_();
        return 0;
    }
    return 1;  // ε
}

// E → T E'
int E() {
    if (T()) return E_();
    return 0;
}

int main() {
    printf("Enter the expression: ");
    scanf("%s", str);

    i = 0;
    if (E() && str[i] == '\0')
        printf("Accepted\n");
    else
        printf("Not accepted\n");

    return 0;
}

```
