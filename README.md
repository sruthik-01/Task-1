# Task 1
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

public class APIDataDashboard {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Name: ");
        String name = sc.nextLine();

        try {
            String apiUrl = "https://api.agify.io/?name=" + name;

            URL url = new URL(apiUrl);

            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("User-Agent", "Mozilla/5.0");

            int responseCode = con.getResponseCode();

            if (responseCode == 200) {

                BufferedReader br = new BufferedReader(
                        new InputStreamReader(con.getInputStream()));

                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }

                br.close();

                System.out.println("\nAPI Response:");
                System.out.println(response.toString());

            } else {
                System.out.println("Error: Unable to fetch data.");
            }

        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }

        sc.close();
    }
}