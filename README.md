import java.util.Scanner;

class Record {  // initialise the class for the actual record of the loans
    private String recordId;  // identifier of the different columns on the table
    private String customerId;
    private String loanType;
    private double interestRate;
    private double amountLeftToPay;
    private int loanTermLeft;

    public Record() {  // has default values
        this.recordId = "";
        this.customerId = ""; // intialise the string to have a combination of both letters and words
        this.loanType = "";
        this.interestRate = 0.0;
        this.amountLeftToPay = 0.0; // intialise the numbers only
        this.loanTermLeft = 0; // can only be integer, not float
    }

    public Record(String recordId, String customerId, String loanType, double interestRate, double amountLeftToPay, int loanTermLeft) {
        this.recordId = recordId;
        this.customerId = customerId;
        this.loanType = loanType;
        this.interestRate = interestRate;
        this.amountLeftToPay = amountLeftToPay;
        this.loanTermLeft = loanTermLeft;
    }

    public void updateInformation(String recordId, String customerId, String loanType, double interestRate, double amountLeftToPay, int loanTermLeft) {
        this.recordId = recordId;
        this.customerId = customerId;
        this.loanType = loanType;      // method which updates the information on each column
        this.interestRate = interestRate;
        this.amountLeftToPay = amountLeftToPay;
        this.loanTermLeft = loanTermLeft;
    }

    public void displayRecord() {
        System.out.printf("%-10s %-10s %-10s %-10.2f %-10.2f %-10d\n", recordId, customerId, loanType, interestRate, amountLeftToPay, loanTermLeft);
    }

    public String getRecordId() {  // these are to validate the information, for example if you enter special characters instead of integers/letters then error handling.
        return recordId;
    }

    public String getCustomerId() {
        return customerId;
    }

    public String getLoanType() {
        return loanType;
    }

    public double getInterestRate() {
        return interestRate;
    }

    public double getAmountLeftToPay() {
        return amountLeftToPay;
    }

    public int getLoanTermLeft() {
        return loanTermLeft;
    }
}

public class XYZBank {  // Main class for the bank
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the maximum number of records: ");
        int maxRecords = scanner.nextInt();
        scanner.nextLine();

        Record[] records = new Record[maxRecords];

        // Input loan records
        for (int i = 0; i < maxRecords; i++) {
            System.out.println("Enter details for record " + (i + 1) + ":");

            String recordId;  // validates the record ID, the same goes for each column to ensure they are of the same type
            while (true) {
                System.out.print("Record ID (XXXXXX): ");
                recordId = scanner.nextLine();
                if (recordId.matches("[0-9]{6}")) {
                    break;
                } else {
                    System.out.println("Invalid input. Record ID must be a 6-digit number.");
                }
            }

            String customerId;
            while (true) {
                System.out.print("Customer ID (AAAXXX): ");
                customerId = scanner.nextLine();
                if (customerId.matches("[A-Z]{3}[0-9]{3}")) {
                    break;
                } else {
                    System.out.println("Invalid input, the Customer ID starts with 3 capital letters and then 3 digits.");
                }
            }

            String loanType;
            while (true) {
                System.out.print("Loan Type (Auto/Builder/Mortgage/Personal/Other): ");
                loanType = scanner.nextLine().trim().toLowerCase(); // this is in case the user enters their loan beginning with lower case.
                if (loanType.equals("auto") || loanType.equals("builder") || loanType.equals("mortgage") || loanType.equals("personal") || loanType.equals("other")) {
                    break;
                } else {
                    System.out.println("Invalid input. Loan Type must be Auto, Builder, Mortgage, Personal, or Other.");
                }
            }

            double interestRate;
            while (true) {
                System.out.print("Interest Rate: ");
                if (scanner.hasNextDouble()) {
                    interestRate = scanner.nextDouble();
                    if (interestRate >= 0) {
                        break;
                    } else {
                        System.out.println("Invalid input. Interest Rate must be a non-negative number.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a valid number.");
                    scanner.next();
                }
            }

            double amountLeftToPay;
            while (true) {
                System.out.print("Amount Left to Pay (in thousands pounds): ");
                if (scanner.hasNextDouble()) {
                    amountLeftToPay = scanner.nextDouble();
                    if (amountLeftToPay >= 0) {
                        break;
                    } else {
                        System.out.println("Invalid input. Amount Left to Pay must be a non-negative number.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a valid number.");
                    scanner.next();
                }
            }

            // Validate and input Loan Term Left
            int loanTermLeft;
            while (true) {
                System.out.print("Loan Term Left (in years): ");
                if (scanner.hasNextInt()) {
                    loanTermLeft = scanner.nextInt();
                    if (loanTermLeft >= 0) {
                        break;
                    } else {
                        System.out.println("Invalid input. Loan Term Left must be a non-negative integer.");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a valid integer.");
                    scanner.next(); // Consume invalid input
                }
            }

            records[i] = new Record(recordId, customerId, loanType, interestRate, amountLeftToPay, loanTermLeft);
            scanner.nextLine(); // Consume newline character
        }

        // Print records in tabular form
        System.out.println("\nLoan Records:");
        System.out.println("Record ID  Customer ID Loan Type Interest  Amount Left Term Left");
        for (Record record : records) {
            record.displayRecord();
        }

        scanner.close();
    }
}
