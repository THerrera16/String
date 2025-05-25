#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

// Velázquez Herrera Maria Thais Itzel 
bool tienenMismosCaracteres(const char *s1, const char *s2, int len) {
    int conteo[26] = {0};
    int i;
    for (i = 0; i < len; i++) {
        conteo[s1[i] - 'a']++;
        conteo[s2[i] - 'a']--;
    }
    for (i = 0; i < 26; i++) {
        if (conteo[i] != 0) return false;
    }
    return true;
}

bool esScramble(const char *s1, const char *s2, int len) {
    int i;
    if (strncmp(s1, s2, len) == 0) return true;
    if (!tienenMismosCaracteres(s1, s2, len)) return false;
    for (i = 1; i < len; i++) {
        if (esScramble(s1, s2, i) && esScramble(s1 + i, s2 + i, len - i)) {
            return true;
        }
        if (esScramble(s1, s2 + len - i, i) && esScramble(s1 + i, s2, len - i)) {
            return true;
        }
    }
   return false;
}
int main() {
    char s1[31], s2[31];
    printf("Ingrese la primera cadena (s1): ");
    scanf("%30s", s1);
    printf("Ingrese la segunda cadena (s2): ");
    scanf("%30s", s2);
    int len1 = strlen(s1);
    int len2 = strlen(s2);
    if (len1 != len2) {
        printf("Error: Las cadenas deben tener la misma longitud.\n");
        return 1;
    }
    if (esScramble(s1, s2, len1)) {
        printf("Resultado: true\n");
    } else {
        printf("Resultado: false\n");
    }
    return 0;
}
