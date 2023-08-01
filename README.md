- 👋 Hi, I’m @venkatesh354
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
venkatesh354/venkatesh354 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

import org.json.JSONObject;

public class WeatherApp {
    private static final String API_KEY = "YOUR_API_KEY"; // Replace this with your actual API key from OpenWeatherMap

    public static void main(String[] args) {
        while (true) {
            System.out.println("Select an option:");
            System.out.println("1. Get weather");
            System.out.println("2. Get Wind Speed");
            System.out.println("3. Get Pressure");
            System.out.println("0. Exit");

            int choice = getUserChoice();

            switch (choice) {
                case 1:
                    getWeather();
                    break;
                case 2:
                    getWindSpeed();
                    break;
                case 3:
                    getPressure();
                    break;
                case 0:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    private static int getUserChoice() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            return Integer.parseInt(reader.readLine());
        } catch (Exception e) {
            return -1;
        }
    }

    private static void getWeather() {
        try {
            String urlString = "https://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=" + API_KEY;
            String response = makeApiRequest(urlString);
            JSONObject weatherData = new JSONObject(response);
            String description = weatherData.getJSONArray("weather").getJSONObject(0).getString("description");
            double temperature = weatherData.getJSONObject("main").getDouble("temp");
            System.out.println("Weather in London:");
            System.out.println("Weather: " + description);
            System.out.println("Temperature: " + temperature + " K\n");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void getWindSpeed() {
        try {
            String urlString = "https://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=" + API_KEY;
            String response = makeApiRequest(urlString);
            JSONObject weatherData = new JSONObject(response);
            double windSpeed = weatherData.getJSONObject("wind").getDouble("speed");
            System.out.println("Wind Speed in London: " + windSpeed + " m/s\n");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void getPressure() {
        try {
            String urlString = "https://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=" + API_KEY;
            String response = makeApiRequest(urlString);
            JSONObject weatherData = new JSONObject(response);
            double pressure = weatherData.getJSONObject("main").getDouble("pressure");
            System.out.println("Pressure in London: " + pressure + " hPa\n");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static String makeApiRequest(String urlString) throws Exception {
        URL url = new URL(urlString);
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
}
