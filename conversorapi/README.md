# Challenge2
Se creo la clase principal donde se crea menu y calculos, para mostrarlos por pantalla 

package com.conversor.ChallengeOracleConver.Principal;

import java.util.Scanner;

public class Principal {
    public static void main(String[] args) {
        int opcion = 0;
        Consultarapi consulta = new Consultarapi();


        System.out.println("-------------------------------");
        System.out.println("-------------------------------");
        System.out.println("CONVERSOR DE DIVISAS");

        String menu = """
                ***-------------------------------------****
                ***Seleccioné la opción según corresponda***
                ***--------------------------------------***
                1) Dolar => Peso Argentino
                2) Peso Argentino => Dólar
                3) Dólar => Real Brasileño
                4) Real Brasileño => Dólar
                5) Dólar => Peso Colombiano
                6) Peso Colombiano => Dólar
                7) Salir
                Elija una opción válida:
                """;
        Scanner teclado = new Scanner (System.in);
        //System.out.println("Ingrese valor que desea convertir");
        while(opcion != 7){
            System.out.println(menu);
            opcion = teclado.nextInt();

            switch (opcion){
                case 1:
                    System.out.println("Ingrese valor en USD:");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        //System.out.println(conversor);
                        Double tasaDeCambioARS = conversor.conversion_rates().get("ARS");
                        if (tasaDeCambioARS != null) {
                            double resultado = valor * tasaDeCambioARS;
                            System.out.println("El valor ingresado en USD es: " +valor +"."+ " El cambio a Peso Argentino es: " + resultado + "ARS");
                        }else{
                            System.out.println("Error conversión");
                        }
                    }catch (RuntimeException e){
                        System.out.println(e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 2:
                    System.out.println("Ingrese valor Peso Argentino");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        //Tasa de cambio de Argentino a USD
                        Double tasaDeCambioUSDaARS = conversor.conversion_rates().get("ARS");
                        if (tasaDeCambioUSDaARS != null) {
                            double resultado = valor / tasaDeCambioUSDaARS;
                            System.out.println("El valor en peso Argentino es: " +valor +" "+ "Cambio a USD es: " + resultado + "USD");
                        }else{
                            System.out.println("Error conversión");
                        }
                    }catch (RuntimeException e){
                        System.out.println(e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 3:
                    System.out.println("Ingrese valor en USD:");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        Double tasaDeCambio = conversor.conversion_rates().get("BRL");
                        if (tasaDeCambio != null) {
                            double resultado = valor * tasaDeCambio;
                            System.out.println("El valor ingresado en USD es: " +valor +" "+ "Cambio a Peso Brasileño es: " + resultado + "BRL");
                        }else{
                            System.out.println("Error conversión");
                        }
                    }catch (RuntimeException e){
                        System.out.println(e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 4:
                    System.out.println("Ingrese valor se Peso Brasilero:");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        Double tasaDeCambioBRLaUSD = conversor.conversion_rates().get("BRL");
                        if (tasaDeCambioBRLaUSD != null) {
                            double resultado = valor/tasaDeCambioBRLaUSD;
                            System.out.println("El valor en peso brasilero es: " +valor +"."+ "Cambio a USD es: " + resultado);
                        }else{
                            System.out.println("Error en tasa ");
                        }
                    }catch (RuntimeException e){
                        System.out.println("Error conversión" + e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 5:
                    System.out.println("Ingrese valor en USD:");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        Double tasaDeCambio = conversor.conversion_rates().get("COP");
                        if (tasaDeCambio != null) {
                            double resultado = valor * tasaDeCambio;
                            System.out.println("El valor ingresado en USD es: " +valor +" "+ "Cambio a Peso Colombiano es: " + resultado);
                        }else{
                            System.out.println("Error conversión");
                        }
                    }catch (RuntimeException e){
                        System.out.println(e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 6:
                    System.out.println("Ingrese valor en peso Colombiano:");
                    try {
                        double valor = teclado.nextDouble();
                        Conversor conversor = consulta.buscaConversor(valor, opcion);
                        //System.out.println(conversor);
                        Double tasaDeCambioCOPaUSD = conversor.conversion_rates().get("COP");
                        if (tasaDeCambioCOPaUSD != null) {
                            double resultado = valor / tasaDeCambioCOPaUSD;
                            System.out.println("El valor de Peso Colombiano es: " +valor +" "+ "Cambio a USD es: " + resultado);
                        }else{
                            System.out.println("Error conversión");
                        }
                    }catch (RuntimeException e){
                        System.out.println(e.getMessage());
                        System.out.println("fin");
                    }
                    break;
                case 7:
                    System.out.println("Salir");
                    break;
                default:
                    System.out.println("Opción inválida");
                    break;
            }
        }

    }
}

Clae converso Un Record llamado Converso donde se ingresaran varables, los get y set, ya se encuentran incorporados

package com.conversor.ChallengeOracleConver.Principal;

import java.time.LocalDateTime;
import java.util.Map;

public record Conversor(String result,
                        //String documentation,
                        //String terms_of_use,
                        int time_last_update_unix,
                        //LocalDateTime time_last_update_utc,
                        int time_next_update_unix,
                        //LocalDateTime Time_next_update_utc,
                        String base_code,
                        Map<String,Double> conversion_rates,
                        double ARS,
                        double USD,
                        double BRL,
                        double CLP,
                        double COP) {
}

Otra clase que es la consulta a la Api

package com.conversor.ChallengeOracleConver.Principal;

import com.google.gson.Gson;

import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Consultarapi {

    public Conversor buscaConversor(double valor, int opcion){
        URI direccion = URI.create("https://v6.exchangerate-api.com/v6/acb1cb2b5e56dfde530be725/latest/USD");

        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(direccion)
                .build();

        try {
            HttpResponse<String> response = client
                    .send(request, HttpResponse.BodyHandlers.ofString());
            return new Gson().fromJson(response.body(), Conversor.class);
        } catch (IOException | InterruptedException e) {
            System.out.println("Eroor en la solicitud http: " +e.getMessage());
            throw new RuntimeException(e);
        }


    }
}
