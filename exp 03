#include <stdio.h>
#include <string.h>

#define MAX_STATES 10
#define MAX_SYMBOLS 5
#define MAX_TRANS 3

int trans_table[MAX_STATES][MAX_SYMBOLS][MAX_TRANS];
int e_closure[MAX_STATES][MAX_STATES];
int ptr;
int state_curr;

void find_e_closure(int x) {
    int i = 0;
    int y[MAX_STATES];
    int num_trans = 0;

    while (trans_table[x][0][i] != -1) {
        y[num_trans] = trans_table[x][0][i];
        i++;
        num_trans++;
    }

    for (int j = 0; j < num_trans; j++) {
        int already_present = 0;
        for (int k = 0; k < ptr; k++) {
            if (e_closure[state_curr][k] == y[j]) {
                already_present = 1;
                break;
            }
        }
        if (!already_present) {
            e_closure[state_curr][ptr++] = y[j];
            find_e_closure(y[j]);
        }
    }
}

int main() {
    int num_states = 3;

    printf("===========================================\n");
    printf("  EXP 3: Finding ε-Closure for NFA with ε-moves\n");
    printf("===========================================\n");

    for (int i = 0; i < MAX_STATES; i++) {
        for (int j = 0; j < MAX_SYMBOLS; j++) {
            for (int k = 0; k < MAX_TRANS; k++) {
                trans_table[i][j][k] = -1;
            }
        }
        for (int j = 0; j < MAX_STATES; j++) {
            e_closure[i][j] = -1;
        }
    }

    trans_table[0][0][0] = 1;
    trans_table[0][0][1] = 2;
    trans_table[1][0][0] = 2;

    for (int i = 0; i < num_states; i++) {
        e_closure[i][0] = i;
        state_curr = i;
        ptr = 1;
        find_e_closure(i);
    }

    printf("\nε-Closure for all states:\n");
    for (int i = 0; i < num_states; i++) {
        printf("ε-closure(%d) = { ", i);
        for (int j = 0; j < num_states; j++) {
            if (e_closure[i][j] != -1) {
                printf("%d ", e_closure[i][j]);
            }
        }
        printf("}\n");
    }

    return 0;
}
