- 👋 Hi, I’m @venkatesh354
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
venkatesh354/venkatesh354 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.util.Scanner;
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Map;
import java.util.HashMap;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import org.json.JSONObject;

public class WeatherApp {

    public static String getWeatherData(String date) throws IOException {
        // Replace 'YOUR_API_KEY' with your actual API key from OpenWeatherMap
        String apiKey = "YOUR_API_KEY";
        String baseUrl = "http://api.openweathermap.org/data/2.5/weather?q=" + date + "&appid=" + apiKey;

        URL url = new URL(baseUrl);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");
        BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String inputLine;
        StringBuilder response = new StringBuilder();

        while ((inputLine = in.readLine()) != null) {
            response.append(inputLine);
        }
        in.close();
        return response.toString();
    }

    public static void printWeatherInfo(JSONObject data) {
        if (data != null) {
            double temperature = data.getJSONObject("main").getDouble("temp");
            System.out.println("Temperature: " + temperature + "°C");
        } else {
            System.out.println("Error fetching weather data.");
        }
    }

    public static void printWindSpeed(JSONObject data) {
        if (data != null) {
            double windSpeed = data.getJSONObject("wind").getDouble("speed");
            System.out.println("Wind Speed: " + windSpeed + " m/s");
        } else {
            System.out.println("Error fetching weather data.");
        }
    }

    public static void printPressure(JSONObject data) {
        if (data != null) {
            double pressure = data.getJSONObject("main").getDouble("pressure");
            System.out.println("Pressure: " + pressure + " hPa");
        } else {
            System.out.println("Error fetching weather data.");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Get weather");
            System.out.println("2. Get Wind Speed");
            System.out.println("3. Get Pressure");
            System.out.println("0. Exit");

            System.out.print("Enter your choice: ");
            String choice = scanner.nextLine();

            if (choice.equals("1")) {
                System.out.print("Enter the date: ");
                String date = scanner.nextLine();
                try {
                    String weatherData = getWeatherData(date);
                    JSONObject jsonData = new JSONObject(weatherData);
                    printWeatherInfo(jsonData);
                } catch (IOException e) {
                    System.out.println("Error: " + e.getMessage());
                }
            } else if (choice.equals("2")) {
                System.out.print("Enter the date: ");
                String date = scanner.nextLine();
                try {
                    String weatherData = getWeatherData(date);
                    JSONObject jsonData = new JSONObject(weatherData);
                    printWindSpeed(jsonData);
                } catch (IOException e) {
                    System.out.println("Error: " + e.getMessage());
                }
            } else if (choice.equals("3")) {
                System.out.print("Enter the date: ");
                String date = scanner.nextLine();
                try {
                    String weatherData = getWeatherData(date);
                    JSONObject jsonData = new JSONObject(weatherData);
                    printPressure(jsonData);
                } catch (IOException e) {
                    System.out.println("Error: " + e.getMessage());
                }
            } else if (choice.equals("0")) {
                System.out.println("Terminating the program.");
                break;
            } else {
                System.out.println("Invalid choice. Please try again.");
            }
        }

        scanner.close();
    }
}
