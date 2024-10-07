# jogodavelha
jogovelhajava




package com.example.myjavafxapp;

import java.util.Scanner;



public class JogoDaVelha1 {
    private char[][] tabuleiro;
    private char jogadorAtual;

    public JogoDaVelha1() {
        tabuleiro = new char[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                tabuleiro[i][j] = ' ';
            }
        }
        jogadorAtual = 'X'; // O jogador X começa
    }

    public void exibirTabuleiro() {
        System.out.println("  0 1 2");
        for (int i = 0; i < 3; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < 3; j++) {
                System.out.print(tabuleiro[i][j]);
                if (j < 2) System.out.print("|");
            }
            System.out.println();
            if (i < 2) System.out.println("  -----");
        }
    }

    public boolean jogar(int linha, int coluna) {
        if (linha >= 0 && linha < 3 && coluna >= 0 && coluna < 3 && tabuleiro[linha][coluna] == ' ') {
            tabuleiro[linha][coluna] = jogadorAtual;
            return true;
        }
        return false;
    }

    public boolean verificarVencedor() {
        // Verifica linhas, colunas e diagonais
        for (int i = 0; i < 3; i++) {
            if ((tabuleiro[i][0] == jogadorAtual && tabuleiro[i][1] == jogadorAtual && tabuleiro[i][2] == jogadorAtual) ||
                    (tabuleiro[0][i] == jogadorAtual && tabuleiro[1][i] == jogadorAtual && tabuleiro[2][i] == jogadorAtual)) {
                return true;
            }
        }
        return (tabuleiro[0][0] == jogadorAtual && tabuleiro[1][1] == jogadorAtual && tabuleiro[2][2] == jogadorAtual) ||
                (tabuleiro[0][2] == jogadorAtual && tabuleiro[1][1] == jogadorAtual && tabuleiro[2][0] == jogadorAtual);
    }

    public boolean tabuleiroCheio() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (tabuleiro[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }

    public void trocarJogador() {
        jogadorAtual = (jogadorAtual == 'X') ? 'O' : 'X';
    }

    public static void main(String[] args) {
        JogoDaVelha1 jogo = new JogoDaVelha1();
        Scanner scanner = new Scanner(System.in);
        boolean jogoAtivo = true;

        while (jogoAtivo) {
            jogo.exibirTabuleiro();
            System.out.println("Jogador " + jogo.jogadorAtual + ", insira a linha e a coluna (0-2, separados por espaço): ");
            int linha = scanner.nextInt();
            int coluna = scanner.nextInt();

            if (jogo.jogar(linha, coluna)) {
                if (jogo.verificarVencedor()) {
                    jogo.exibirTabuleiro();
                    System.out.println("Parabéns! Jogador " + jogo.jogadorAtual + " venceu!");
                    jogoAtivo = false;
                } else if (jogo.tabuleiroCheio()) {
                    jogo.exibirTabuleiro();
                    System.out.println("O jogo terminou em empate!");
                    jogoAtivo = false;
                } else {
                    jogo.trocarJogador();
                }
            } else {
                System.out.println("Movimento inválido! Tente novamente.");
            }
        }
        scanner.close();
    }
}
