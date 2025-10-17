Name: Riley Lidot
Date: 10/13/25
Class: CISC-191
# Inventory control system - Version 1.0 
You are creating a drug company's inventory control system. You visit each
aisle and update the inventory based on the physical presence of each item
on the shelf. The aisles are divided into sections.
The sections are: Painkillers, Bandages, Equipment
## Painkillers
- Name of the item, drug company name, expiry date, age group
## Bandages
- Name of the item, company name, expiry date, age group, water proof (Y/N)
## Equipment
- Name of the item, company name, item weight (lbs)
# Midterm Questions
1. Write a parent class, and three derived classes. In each class,
the user should be able to update or display the items. Use at
least one override and overload method.
## My Solution Code for InventoryV1:

```
import java.util.ArrayList;
import java.util.Scanner;
class InventoryItem {
String name;
String company;
double weight;
public InventoryItem(String name, String company, double weight) {
this.name = name;
this.company = company;
this.weight = weight;
}
public void display() {
System.out.println("Name: " + name + ", Company: " + company + ", Weight: " + weight + "
lbs");
}
public void update(String name) {
this.name = name;
}
public void update(String name, String company, double weight) {
this.name = name;
this.company = company;
this.weight = weight;
}
}
class Painkillers extends InventoryItem {
public Painkillers(String name, String company, double weight) {
super(name, company, weight);
}
@Override
public void display() {
System.out.println("[Painkiller]");
super.display();
}
}
class Bandages extends InventoryItem {
public Bandages(String name, String company, double weight) {
super(name, company, weight);
}
@Override
public void display() {
System.out.println("[Bandage]");
super.display();
}
}
class Equipment extends InventoryItem {
public Equipment(String name, String company, double weight) {
super(name, company, weight);
}
@Override
public void display() {
System.out.println("[Equipment]");
super.display();
}
}
public class InventoryV1 {
public static void main(String[] args) {
ArrayList<InventoryItem> inventory = new ArrayList<>();
inventory.add(new Painkillers("Aspirin", "MediCorp", 0.5));
inventory.add(new Bandages("Gauze Roll", "HealthPro", 0.2));
inventory.add(new Equipment("Thermometer", "TempCheck", 1.0));
for (InventoryItem item : inventory) {
item.display();
}
}
}
```

## 2. Inventory control system - Version 2.0 
You are enhancing version 1 of the inventory control system where
you used pre-written derived exceptions by the Exception class on
the user inputs. Catch any two possible invalid user inputs.
## My Solution Code for InventoryV2:
```
import java.util.InputMismatchException;
import java.util.Scanner;
public class InventoryV2 {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
try {
System.out.print("Enter item weight (lbs): ");
double weight = sc.nextDouble();
if (weight < 0) {
throw new IllegalArgumentException("Weight cannot be negative!");
}
System.out.print("Enter item name: ");
String name = sc.next();
InventoryItem painkiller = new Painkillers(name, "MediCorp", weight);
painkiller.display();
} catch (InputMismatchException e) {
System.out.println("Invalid input! Please enter a numeric value for weight.");
} catch (IllegalArgumentException e) {
System.out.println("Error: " + e.getMessage());
} finally {
sc.close();
}
}
}
```
## 3. Inventory control system - Version 3.0
You are enhancing version 1 or 2 of the inventory control system
where you used customized derived exception by the Exception class
on the user input. Catch any one possible invalid user input.
## My Solution Code for InventoryV3:
```
class InvalidExpiryDateException extends Exception {
public InvalidExpiryDateException(String message) {
super(message);
}
}
class AdvancedDrug extends InventoryItem {
String expiryDate;
String ageGroup;
public AdvancedDrug(String name, String company, double weight, String expiryDate, String
ageGroup) {
super(name, company, weight);
this.expiryDate = expiryDate;
this.ageGroup = ageGroup;
}
@Override
public void display() {
System.out.println("[Advanced Drug]");
System.out.println("Name: " + name + ", Company: " + company + ", Weight: " + weight +
", Expiry Date: " + expiryDate + ", Age Group: " + ageGroup);
}
}
public class InventoryV3 {
public static void main(String[] args) {
try {
AdvancedDrug d1 = new AdvancedDrug("PainAway", "PharmaLife", 0.5, "2020-01-01",
"Adult");
validateExpiry(d1.expiryDate);
d1.display();
} catch (InvalidExpiryDateException e) {
System.out.println("Custom Exception Caught: " + e.getMessage());
}
}
public static void validateExpiry(String expiryDate) throws InvalidExpiryDateException {
if (expiryDate.compareTo("2025-01-01") < 0) {
throw new InvalidExpiryDateException("The drug has expired!");
}
}
}
```
