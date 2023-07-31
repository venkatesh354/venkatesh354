- 👋 Hi, I’m @venkatesh354
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
venkatesh354/venkatesh354 is a ✨ special ✨ repository because its `WeatherApp.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.util.Scanner;
public class WeatherApp{
private static final String APP_PASSWORD = "Venky123";
private static final String BASE_URL = "https://api.weatherinformation.com/";
private static get double getWeatherData(String date){
 return 0;
  } 
 private static get double getWindSpeedData(String date){
 return 0;
 }
 private static get double getPressureData(String date){
 return 0;
 }
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("1. Get weather");
            System.out.println("2. Get Wind Speed");
            System.out.println("3. Get Pressure");
            System.out.println("0. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();

            switch (choice) {

                case 1:

                    System.out.print("Enter the date: ");

                    String date1 = scanner.next();

                    double temperature = getWeatherData(date1);

                    System.out.println("Temperature on " + date1 + ": " + temperature);

                    break;

                case 2:

                    System.out.print("Enter the date: ");

                    String date2 = scanner.next();

                    double windSpeed = getWindSpeedData(date2);

                    System.out.println("Wind Speed on " + date2 + ": " + windSpeed);

                    break;

                case 3:

                    System.out.print("Enter the date: ");

                    String date3 = scanner.next();

                    double pressure = getPressureData(date3);

                    System.out.println("Pressure on " + date3 + ": " + pressure);

                    break;

                case 0:

                    System.out.println("Exiting the program...");

                    scanner.close();

                    System.exit(0);

                    break;

                default:

                    System.out.println("Invalid choice. Please try again.");

            }

        }

    }

}

