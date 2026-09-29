# VehicleParkingManagement-package main;

import java.util.Scanner;

import model.Car;
import model.Bike;
import model.Vehicle;
import model.ParkingSlot;
import model.VehicleType;
import service.ParkingService;

public class Main {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        ParkingService parkingService = new ParkingService();

        ParkingSlot carSlot = new ParkingSlot(1, VehicleType.CAR);
        ParkingSlot bikeSlot = new ParkingSlot(2, VehicleType.BIKE);

        boolean running = true;

        while (running) {

            System.out.println("\n================================");
            System.out.println("   VEHICLE PARKING MANAGEMENT");
            System.out.println("================================");
            System.out.println("1. Add Car");
            System.out.println("2. Add Bike");
            System.out.println("3. Show Vehicles");
            System.out.println("4. Search Vehicle");
            System.out.println("5. Calculate Parking Fee");
            System.out.println("6. Show Parking Rules");
            System.out.println("7. Show Total Vehicles");
            System.out.println("8. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {

                case 1:

                    System.out.print("Enter car number: ");
                    String carNumber = scanner.nextLine().trim().toUpperCase();

                    System.out.print("Enter owner name: ");
                    String carOwner = scanner.nextLine().trim();

                    System.out.print("Enter number of doors: ");
                    int doors = scanner.nextInt();
                    scanner.nextLine();

                    Car car = new Car(carNumber, carOwner, doors);

                    parkingService.addVehicle(car, carSlot);

                    break;

                case 2:

                    System.out.print("Enter bike number: ");
                    String bikeNumber = scanner.nextLine().trim().toUpperCase();

                    System.out.print("Enter owner name: ");
                    String bikeOwner = scanner.nextLine().trim();

                    System.out.print("Does the bike have gears? (yes/no): ");
                    String gearInput = scanner.nextLine().trim();

                    boolean hasGear;

                    if (gearInput.equalsIgnoreCase("yes")) {
                        hasGear = true;
                    } else {
                        hasGear = false;
                    }

                    Bike bike = new Bike(bikeNumber, bikeOwner, hasGear);

                    parkingService.addVehicle(bike, bikeSlot);

                    break;

                case 3:

                    parkingService.showVehicles();

                    break;

                case 4:

                    System.out.print("Enter vehicle number to search: ");
                    String searchNumber = scanner.nextLine().trim();

                    Vehicle foundVehicle =
                            parkingService.searchVehicle(searchNumber);

                    if (foundVehicle != null) {

                        System.out.println("Vehicle found:");
                        System.out.println(foundVehicle);

                    } else {

                        System.out.println("Vehicle not found.");
                    }

                    break;

                case 5:

                    System.out.print("Enter vehicle number: ");
                    String feeVehicleNumber =
                            scanner.nextLine().trim();

                    Vehicle feeVehicle =
                            parkingService.searchVehicle(feeVehicleNumber);

                    if (feeVehicle == null) {

                        System.out.println("Vehicle not found.");
                        continue;
                    }

                    System.out.print("Enter parking hours: ");
                    int hours = scanner.nextInt();
                    scanner.nextLine();

                    parkingService.displayFee(feeVehicle, hours);

                    // Type casting example
                    if (feeVehicle instanceof Car) {

                        Car selectedCar = (Car) feeVehicle;

                        System.out.println(
                                "This is a car with "
                                        + selectedCar.getNumberOfDoors()
                                        + " doors."
                        );
                    }

                    break;

                case 6:

                    parkingService.displayParkingRules();

                    break;

                case 7:

                    System.out.printf(
                            "Total vehicles parked: %d%n",
                            ParkingService.getTotalVehicles()
                    );

                    break;

                case 8:

                    System.out.println("Exiting the system...");
                    running = false;

                    break;

                default:

                    System.out.println("Invalid choice.");
                    continue;
            }
        }

        scanner.close();

        System.out.println("Thank you for using Vehicle Parking Management System.");
    }
}
