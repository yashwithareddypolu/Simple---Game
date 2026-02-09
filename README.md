# Simple---Game
A simple program to write a basic number guess game where it has 4 levels (different range of numbers)  it gives hints based on the number you entered and you can continue game if you are interested after attempting once.
import java.util.*;

class Main {

    static Scanner sc = new Scanner(System.in);
    static Random r = new Random();

    public static void main(String[] args) {

        System.out.println("=================================");
        System.out.println("       GUESS THE NUMBER       ");
        System.out.println("=================================");

        while (true) {

            int[] settings = chooseDifficulty();
            int maxNum = settings[0];
            int maxAttempts = settings[1];

            playGame(maxNum, maxAttempts);

            System.out.print("\nPlay again? (yes/no): ");
            String response = sc.next().toLowerCase();
            if (!response.equals("yes") && !response.equals("y")) {
                break;
            }
        }

        System.out.println("\nThanks for playing! ");
        sc.close();
    }

    // 🔹 Difficulty Selection (Efficient & Clean)
    static int[] chooseDifficulty() {

        while (true) {

            System.out.println("\nSelect Difficulty:");
            System.out.println("1. Easy (1 - 50)");
            System.out.println("2. Medium (1 - 100)");
            System.out.println("3. Hard (1 - 500)");
            System.out.println("4. Advanced (1 - 1000)");
            System.out.print("Enter choice (1-4): ");

            if (!sc.hasNextInt()) {
                System.out.println(" Invalid input. Enter a number.");
                sc.nextLine();
                continue;
            }

            int choice = sc.nextInt();

            switch (choice) {
                case 1: return new int[]{50, 5};
                case 2: return new int[]{100, 15};
                case 3: return new int[]{500, 25};
                case 4: return new int[]{1000, 40};
                default:
                    System.out.println(" Choose between 1 and 4.");
            }
        }
    }

    // 🔹 Game Logic (Clean & Efficient)
    static void playGame(int maxNum, int maxAttempts) {

        int secretNumber = r.nextInt(maxNum) + 1;
        int minRange = 1;
        int maxRange = maxNum;
        int attempts = 0;

        System.out.println(" Guess the number between 1 and " + maxNum);
        System.out.println("You have " + maxAttempts + " attempts.");

        while (attempts < maxAttempts) {

            System.out.println("\nRange: [" + minRange + " - " + maxRange + "]");
            System.out.print("Attempt " + (attempts + 1) + "/" + maxAttempts + " → Enter guess: ");

            if (!sc.hasNextInt()) {
                System.out.println(" Invalid input. Attempt counted.");
                sc.nextLine();
                attempts++;
                continue;
            }

            int guess = sc.nextInt();
            attempts++;

            if (guess < minRange || guess > maxRange) {
                System.out.println("⚠ Stay inside the range!");
                continue;
            }

            if (guess < secretNumber) {
                minRange = guess + 1;
                System.out.println(" Too Low!");
            }
            else if (guess > secretNumber) {
                maxRange = guess - 1;
                System.out.println(" Too High!");
            }
            else {
                System.out.println(" Correct! You guessed it in " + attempts + " attempts.");
                return;
            }
        }

        System.out.println(" Game Over! The number was: " + secretNumber);
    }
}
