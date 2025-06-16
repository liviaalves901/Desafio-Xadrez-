#include <stdio.h>
#include <stdlib.h>

#define TAM 8

// Função para verificar se a posição está dentro do tabuleiro
int dentroTabuleiro(int x, int y) {
    return x >= 0 && x < TAM && y >= 0 && y < TAM;
}

// Função para verificar se o movimento é válido para um cavalo
int movimentoValido(int x1, int y1, int x2, int y2) {
    int dx = abs(x2 - x1);
    int dy = abs(y2 - y1);
    return (dx == 2 && dy == 1) || (dx == 1 && dy == 2);
}

// Função para imprimir o tabuleiro
void imprimirTabuleiro(int cavaloX, int cavaloY, int finalX, int finalY) {
    for (int i = 0; i < TAM; i++) {
        for (int j = 0; j < TAM; j++) {
            if (i == cavaloX && j == cavaloY)
                printf(" ♞ ");
            else if (i == finalX && j == finalY)
                printf(" ✪ ");
            else
                printf(" . ");
        }
        printf("\n");
    }
    printf("\n");
}

int main() {
    int cavaloX = 0, cavaloY = 0;  // posição inicial
    int finalX = 7, finalY = 7;    // posição alvo

    printf("==== DESAFIO DO CAVALO NO XADREZ ====\n");
    printf("Leve o cavalo (♞) até a posição final (✪)!\n\n");

    while (cavaloX != finalX || cavaloY != finalY) {
        imprimirTabuleiro(cavaloX, cavaloY, finalX, finalY);

        int novoX, novoY;
        printf("Digite a nova posição do cavalo (linha e coluna de 0 a 7): ");
        scanf("%d %d", &novoX, &novoY);

        if (!dentroTabuleiro(novoX, novoY)) {
            printf("Movimento fora do tabuleiro. Tente novamente.\n\n");
            continue;
        }

        if (!movimentoValido(cavaloX, cavaloY, novoX, novoY)) {
            printf("Movimento inválido para um cavalo! Tente novamente.\n\n");
            continue;
        }

        cavaloX = novoX;
        cavaloY = novoY;
    }

    imprimirTabuleiro(cavaloX, cavaloY, finalX, finalY);
    printf("Parabéns! Você completou o desafio do cavalo! 🏆\n");

    return 0;
}
