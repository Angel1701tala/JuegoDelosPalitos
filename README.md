# JuegoDelosPalitos

package juegoDeLosPalitos;
import java.util.Random;
import java.util.Scanner;

import java.util.Random;
import java.util.Scanner;

public class JuegoDePalitos {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random rand = new Random();

        System.out.println("!El juego de los palitos!");

        int palitos = 21;
        boolean turnoJugador1 = true;

        System.out.println("¿seleciota?");
        System.out.println ("1 = Jugador 1, 2 = Jugador 2");
        int opcion = sc.nextInt();
        if (opcion == 2) {
            turnoJugador1 = false;
        }

        while (palitos > 0) {
            System.out.println("Quedan -|" + palitos + "|- palito.");

            if (turnoJugador1) {
                System.out.println("Jugador 1.");
                System.out.println("¿Cuántos palitos quieres quitar? (1 o 2)");

                int palitosQuitados = sc.nextInt();
                while (palitosQuitados < 1 || palitosQuitados > 2 || palitosQuitados > palitos) {
                    System.out.println("¡Debes quitar 1 o 2 palitos!");
                    System.out.println("¿Cuántos palitos quieres quitar? (1 o 2)");
                    palitosQuitados = sc.nextInt();
                }

                palitos -= palitosQuitados;
                turnoJugador1 = false;
            } else {
                System.out.println("Turno de la máquina...");

                int palitosQuitados;

                if (palitos == 1 || palitos == 2) {
                    palitosQuitados = palitos;
                } else {
                    int mejorJugada = minimax(palitos - 2, false, 1);

                    if (mejorJugada == 1) {
                        palitosQuitados = 1;
                    } else {
                        palitosQuitados = 2;
                    }
                }

                System.out.println("La máquina quitó " + palitosQuitados + " palitos.");
                palitos -= palitosQuitados;
                turnoJugador1 = true;
            }
        }

        String jugadorGanador = turnoJugador1 ? "Jugador 2" : "Jugador 1";
        System.out.println("¡Felicidades, " + jugadorGanador + "! Has ganado el juego.");
    }

    public static int minimax(int palitosRestantes, boolean maximizar, int profundidad) {
        if (palitosRestantes == 0) {
            return maximizar ? -1 : 1;
        } else if (profundidad >= 4) {
            return 0;
        }

        if (maximizar) {
            int mejorValor = Integer.MIN_VALUE;

            for (int i = 1; i <= 2 && i <= palitosRestantes; i++) {
                int valorActual = minimax(palitosRestantes - i, false, profundidad + 1);
                mejorValor = Math.max(mejorValor, valorActual);
            }

            return mejorValor;
        } else {
            int mejorValor = Integer.MAX_VALUE;

            for (int i = 1; i <= 2 && i <= palitosRestantes; i++) {
                int valorActual = minimax(palitosRestantes - i, true, profundidad + 1);
                mejorValor = Math.min(mejorValor, valorActual);
            }

            return mejorValor;
        }
    }
           
