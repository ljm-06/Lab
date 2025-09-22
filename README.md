package martin;

import java.util.*;

class Item{
	String code;
	String name;
	int quantity;
	
	Item(String code, String name, int quantity){
		this.code = code;
		this.name = name;
		this.quantity = quantity;
	}
	
	public String toString() {
		
		return code + "|" + name + "|" + quantity;
		
	}
	
}

class Truck {
	String plate;
	String driver;
	
	Truck(String plate, String driver){
		this.plate = plate;
		this.driver = driver;
	}
	
	public String toString() {
		
		return plate + "|" + driver;
		
	}

}


public class labexam {

	public static void main(String[] args) {
			ArrayDeque<Item> warehouseStack = new ArrayDeque<>();
			ArrayDeque<Truck> truckQueue = new ArrayDeque<>();
			Scanner sc = new Scanner (System.in);


			int choice = -1;

		    while (choice != 0) {
		        System.out.println("\n=== Warehouse Loading System ===");
		        System.out.println("[1] Store item (push");
		        System.out.println("[2] View warehouse stack");
		        System.out.println("[3] Register arriving truck (enqueue)");
		        System.out.println("[4] View waiting trucks");
		        System.out.println("[5] Load next truck (pop item + poll truck");
		        System.out.println("[0] Exit");
		        System.out.print("Enter choice: ");
		        choice = Integer.parseInt(sc.nextLine());

		        if (choice == 1) {
		            System.out.print("Enter code: ");
		            String c = sc.nextLine();
		            System.out.print("Enter name: ");
		            String n = sc.nextLine();
		            System.out.print("Enter quantity: ");
		            int q = sc.nextInt();

		            Item i = new Item(c, n, q);
		            warehouseStack.push(i);
		            System.out.println("Stored: " + i);

		        } else if (choice == 2) {
		            if (warehouseStack.isEmpty()) {
		                System.out.println("Warehouse is empty.");
		            } else {
		                System.out.println("TOP →");
		                for (Item i : warehouseStack) {
		                    System.out.println(i);
		                }
		                System.out.println("← BOTTOM");
		            }

		        } else if (choice == 3) {
		            System.out.print("Enter plate number: ");
		            String p = sc.nextLine();
		            System.out.print("Enter driver: ");
		            String d = sc.nextLine();

		            Truck t = new Truck(p, d);
		            truckQueue.offer(t);
		            System.out.println("Registered: " + t);

		        } else if (choice == 4) {
		            if (truckQueue.isEmpty()) {
		                System.out.println("No trucks waiting.");
		            } else {
		                System.out.println("FRONT →");
		                for (Truck t : truckQueue) {
		                    System.out.println(t);
		                }
		                System.out.println("← REAR");
		            }

		        } else if (choice == 5) {
		            if (warehouseStack.isEmpty() || truckQueue.isEmpty()) {
		                System.out.println("Cannot load. Either no items in warehouse or no trucks.");
		            } else {
		                Item i = warehouseStack.pop();
		                Truck t = truckQueue.poll();
		                System.out.println("Loaded: " + i + " → " + t);
		                System.out.println("Remaining items in warehouse: " + warehouseStack.size());
		                System.out.println("Remaining trucks waiting: " + truckQueue.size());
		            }

		        } else if (choice == 0) {
		            System.out.println("Exiting program...");
		        } else {
		            System.out.println("Invalid choice. Try again.");
		        }
		    }

	}

}
