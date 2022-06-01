package com.example.billcom;

import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    private static ArrayList<Appliance> appliances;
    private static Scanner scanner;

    public static void main(String[] args) {

        appliances = new ArrayList<>();
        System.out.println("Calculate feature");

        showInitialOptions();

    }
    private static void showInitialOptions(){
        System.out.println("Options:" +
                "\n\t1. Edit" +
                "\n\t2. Save" +
                "\n\t3. Delete" +
                "\n\t4. Create");

        scanner = new Scanner(System.in);
        int choice = scanner.nextInt();
        switch (choice){
            case 1:
                edit();
                break;

            case 2:
                save();
                break;

            case 3:
                delete();
                break;

            case 4:
                create();
                break;

            default:
                break;
        }
    }
    public static void create(){
        scanner = new Scanner(System.in);
        System.out.println("Enter Appliance name: ");
        String applianceName = scanner.next();
        System.out.println("Enter Electric Capacity: ");
        float electricCapacity = scanner.nextFloat();
        System.out.println("How many hours in a day used: ");
        float hoursUsed = scanner.nextFloat();
        System.out.println("How many days in a month used: ");
        float daysUsed = scanner.nextFloat();

        Appliance newAppliance = new Appliance(applianceName, electricCapacity, daysUsed, hoursUsed);
        appliances.add(newAppliance);
        showInitialOptions();
    }
    public static void delete(){

        if (appliances.size() <= 0){
            System.out.println("No appliances to delete");
            showInitialOptions();
            return;
        }

        scanner = new Scanner(System.in);
        System.out.println("Enter the number of corresponding appliance to delete.");
        int iterations = 1;
        for (Appliance appliance : appliances){
            System.out.println(iterations + ".");
            appliance.printDetails();
            iterations++;
        }
        System.out.println("Enter number to delete: ");
        int choice = scanner.nextInt();

        if (choice - 1 > appliances.size()){
            System.out.println("Invalid choice");
            showInitialOptions();
        }
        appliances.remove(choice - 1);
        showInitialOptions();
    }
    public static void edit(){
        scanner = new Scanner(System.in);
        System.out.println("Enter the number of corresponding appliance to edit.");
        int iterations = 1;
        for (Appliance appliance : appliances){
            System.out.println(iterations + ".");
            appliance.printDetails();
            iterations++;
        }

        System.out.println("Enter number to edit: ");
        int choice = scanner.nextInt();
        int indexOfChoice = choice - 1;

        if (indexOfChoice > appliances.size()){ //pwedeng magkamali yung user
            System.out.println("Invalid choice. ");
            showInitialOptions();
            return;
        }

        boolean isEditing = true;
        while (isEditing){
            appliances.get(indexOfChoice).printDetails();
            System.out.println("Enter detail to edit: ");
            int choiceToEdit = scanner.nextInt();
            switch (choiceToEdit){
                case 1:
                    System.out.println("Enter new name: ");
                    String newName = scanner.next();
                    appliances.get(indexOfChoice).setApplianceName(newName);
                    break;

                case 2:
                    System.out.println("Enter new electric capacity: ");
                    float newElectricCapacity = scanner.nextFloat();
                    appliances.get(indexOfChoice).setElectricCapacity(newElectricCapacity);
                    break;

                case 3:
                    System.out.println("Enter new hours used: ");
                    float newHoursUsed = scanner.nextFloat();
                    appliances.get(indexOfChoice).setHoursUsed(newHoursUsed);
                    break;

                case 4:
                    System.out.println("Enter new days used: ");
                    float newDaysUsed = scanner.nextFloat();
                    appliances.get(indexOfChoice).setDaysUsed(newDaysUsed);
                    break;

                default:
                    break;
            }
            System.out.println("Continue editing this appliance? \n" +
                    "1 YES\n" +
                    "2 NO\n");
            int choiceToContinueEditing = scanner.nextInt();
            if (choiceToContinueEditing == 1){
                isEditing = true;
            }else{
                isEditing = false;
            }
        }
        showInitialOptions();
    }
    public static void save(){
        //code to save current arraylist to db
        System.out.println("saved..");
        showInitialOptions();
    }
}
