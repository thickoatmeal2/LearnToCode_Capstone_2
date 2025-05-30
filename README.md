# LearnToCode_Capstone_2
Jake's Sandwiches POS
   A Java console application for ordering sandwiches at Jake's Sandwiches.
Features

Displays ASCII art for "Jake's Sandwhiches" at startup.
Order multiple sandwiches in 3 sizes (4": $5.50, 8": $7.00, 12": $8.50), customized one at a time.
Choose from 4 bread types (white, wheat, rye, wrap).
Add regular (free: lettuce, peppers, onions, tomatoes, jalapeños, cucumbers, pickles, guacamole, mushrooms) and premium toppings (meats: $1.00/$2.00/$3.00, cheeses: $0.75/$1.50/$2.25), with extra premium toppings at additional cost ($0.50/$1.00/$1.50 for meats, $0.30/$0.60/$0.90 for cheeses).
Add free sauces (mayo, mustard, ketchup, ranch, thousand islands, vinaigrette, au jus, sauce).
Option to toast sandwiches.
Add drinks (Small: $2.00, Medium: $2.50, Large: $3.00) and chips ($1.50).
Detailed checkout with all items, toppings, and total cost.
Saves order details to a CSV receipt file in receipts folder (named yyyyMMdd-HHmmss.csv).
View previous receipts by listing and selecting from saved CSV files.
Basic order management with confirm/cancel.

Directory

Source files: pluralsight/workshops/DELIcious/com/pluralsight.
Receipts: pluralsight/workshops/DELIcious/receipts.

Running
cd pluralsight/workshops/DELIcious
javac com/pluralsight/*.java
java com.pluralsight.Driver

Compilation Fix
   Resolved size has private access in com.pluralsight.Sandwich by adding getSize() to Sandwich.
Interesting Code
// PosApp.java: viewPreviousReceipts
private void viewPreviousReceipts() {
    try {
        Path receiptsDir = Paths.get("receipts");
        if (!Files.exists(receiptsDir)) {
            System.out.println("No receipts found. The receipts folder does not exist.");
            return;
        }
        List<Path> receiptFiles = Files.list(receiptsDir)
            .filter(path -> path.toString().endsWith(".csv"))
            .sorted()
            .collect(Collectors.toList());
        if (receiptFiles.isEmpty()) {
            System.out.println("No receipts found in the receipts folder.");
            return;
        }
        System.out.println("\nAvailable Receipts:");
        for (int i = 0; i < receiptFiles.size(); i++) {
            System.out.println((i + 1) + ") " + receiptFiles.get(i).getFileName());
        }
        System.out.print("Select a receipt number (0 to cancel): ");
        int choice = scanner.nextInt();
        scanner.nextLine();
        if (choice == 0) {
            return;
        }
        if (choice < 1 || choice > receiptFiles.size()) {
            System.out.println("Invalid selection. Returning to home screen.");
            return;
        }
        Path selectedReceipt = receiptFiles.get(choice - 1);
        System.out.println("\nReceipt: " + selectedReceipt.getFileName());
        System.out.println("Contents:");
        List<String> lines = Files.readAllLines(selectedReceipt);
        for (String line : lines) {
            System.out.println(line);
        }
    } catch (IOException e) {
        System.out.println("Error reading receipts: " + e.getMessage());
    }
}







The Deli app is a console application that simulates a Deli for the user. When the app runs, the user is taken to the starting screen. From there the user can choose to start a new order, or the user can exit the app. If the user opts to begin a new order, the user then proceeds to the order screen.
From the order screen, the user can opt to order a sandwhich, chips, a drink, or they can proceed to checkout or exit the app. 
From the order sandwhich screen, the user is able to order a 4", 8", or 12" sandwich, select a type of bread, select between premium toppings such as meat and cheese, select regular toppings, and select wether they want the sandwhich toasted or not. After the user completes their sandwhich order, they are returned to the original order screen.



![Screenshot 2025-05-30 084150](https://github.com/user-attachments/assets/5d4bb976-6324-4405-ad6f-aaadc9f3916e)


Interesting piece of code: The POSapp automatically gives the customer an 8" sandwhich if they input an invalid input. Similarly if a user inputs an invalid type of bread, the recieve white bread as a default. This is useful because it accounts for human error, and it is an example of how the code mimicks real world behavior. 


![Screenshot 2025-05-30 084716](https://github.com/user-attachments/assets/edb4d551-8a68-480e-b128-feb59bbb4e5d)
