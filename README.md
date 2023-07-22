package codsoft;

import java.util.Scanner;

//BankAccount class represents the user's bank account
class BankAccount {
 private double balance;

 public BankAccount(double initialBalance) {
     balance = initialBalance;
 }

 public double getBalance() {
     return balance;
 }

 public void deposit(double amount) {
     balance += amount;
 }

 public boolean withdraw(double amount) {
     if (amount <= balance) {
         balance -= amount;
         return true;
     }
     return false;
 }
}

//ATM class represents the ATM machine
class ATM {
 private BankAccount bankAccount;
 private Scanner scanner;

 public ATM(BankAccount account) {
     bankAccount = account;
     scanner = new Scanner(System.in);
 }

 public void showOptions() {
     System.out.println("Welcome to the ATM");
     System.out.println("1. Check Balance");
     System.out.println("2. Withdraw");
     System.out.println("3. Deposit");
     System.out.println("4. Quit");
 }

 public void processOption(int option) {
     switch (option) {
         case 1:
             checkBalance();
             break;
         case 2:
             withdraw();
             break;
         case 3:
             deposit();
             break;
         case 4:
             System.out.println("Thank you for using the ATM. Goodbye!");
             System.exit(0);
             break;
         default:
             System.out.println("Invalid option. Please try again.");
     }
 }

 private void checkBalance() {
     double balance = bankAccount.getBalance();
     System.out.println("Your account balance is: " + balance);
 }

 private void withdraw() {
     System.out.print("Enter the amount to withdraw: ");
     double amount = scanner.nextDouble();
     if (amount <= 0) {
         System.out.println("Invalid amount. Please try again.");
         return;
     }

     boolean success = bankAccount.withdraw(amount);
     if (success) {
         System.out.println("Withdrawal successful. Please take your cash.");
     } else {
         System.out.println("Insufficient balance. Withdrawal failed.");
     }
 }

 private void deposit() {
     System.out.print("Enter the amount to deposit: ");
     double amount = scanner.nextDouble();
     if (amount <= 0) {
         System.out.println("Invalid amount. Please try again.");
         return;
     }

     bankAccount.deposit(amount);
     System.out.println("Deposit successful. Thank you for banking with us!");
 }
}

//Main class to run the ATM program
public class Main {
 @SuppressWarnings("resource")
public static void main(String[] args) {
     BankAccount account = new BankAccount(1000.0); // Assuming initial balance is $1000
     ATM atm = new ATM(account);

     while (true) {
         atm.showOptions();
         System.out.print("Enter your option: ");
         int option = new Scanner(System.in).nextInt();
         atm.processOption(option);
         System.out.println();
     }
 }
}
