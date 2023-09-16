
Базовое задние:
1) Переписать код в соответствии с Single Responsibility Principle:
 
```agsl


   public class Employee {
   private String name;
   private Date dob;
   private int baseSalary;
   
   public Employee(String name, Date dob, int baseSalary) {
   this.name = name;
   this.dob = dob;
   this.baseSalary = baseSalary;
   }
   
  public String getEmpInfo() {
   return "name - " + name + " , dob - " + dob.toString();
   }
   
  public int calculateNetSalary() {
   int tax = (int) (baseSalary * 0.25);//calculate in otherway
   return baseSalary - tax;
   }
   }
 ```


Ответ: Метод calculateNetSalary вынесен в отдельный класс calculateNetSalary вынесен в класс EmployeeSalary
```agsl

public class Employee {
private String name;
private Date dob;
private int baseSalary;

public Employee(String name, Date dob, int baseSalary) {
this.name = name;
this.dob = dob;
this.baseSalary = baseSalary;
}
public String getEmpInfo() {
return "name - " + name + " , dob - " + dob.toString();
}
}
```
отдельный класс для учета заработной платы служащего 
```agsl

public class EmployeeSalary  {          
private int baseSalary;

public int calculateNetSalary() {
int tax = (int) (baseSalary * 0.25);//calculate in otherway
return baseSalary - tax;
}
}
```


2) Переписать код SpeedCalculation в соответствии с Open-Closed Principle:
   ```agsl

   public class SpeedCalculation {
   public double calculateAllowedSpeed(Vehicle vehicle) {
   
   if (vehicle.getType().equalsIgnoreCase("Car")) {
   return vehicle.getMaxSpeed() * 0.8;
   } else if (vehicle.getType().equalsIgnoreCase("Bus")) {
   return vehicle.getMaxSpeed() * 0.6;
   }
   return 0.0;
   }
   }
   public class Vehicle {
   int maxSpeed;
   String type;
   
   public Vehicle(int maxSpeed, String type) {
   this.maxSpeed = maxSpeed;
   this.type = type;
   }
   public int getMaxSpeed() {
   return this.maxSpeed;
   }
   public String getType() {
   return this.type;
   
   }
   }
   ```
   **ОТВЕТ** 
   создайте два дополнительных класса Car и Bus(наследников Vehicle), напишите метод calculateAllowedSpeed().
   Использование этого метода позволит сделать класс SpeedCalculation соответствующим OCP
```agsl

   public  class Car extendsVehicle {
   double k = 0.8;
   // logic
   }
   public  class Bus extendsVehicle {
   double k = 0.6;
   // logic
   }
   public class SpeedCalculation {
   public double calculateAllowedSpeed(Vehicle vehicle) {
    return vehicle.getMaxSpeed() * k;
   } 
   }
   
   
```  
    
   
3) Переписать код в соответствии с Interface Segregation Principle:
```agsl
   public interface Shape {
   double area();
   double volume();
   }
   public class Circle implements Shape {
   private double radius;
   public Circle(double radius) {
   this.radius = radius;
   }
   @Override
   public double area() {
   return 2 * 3.14 * radius;
   }
   @Override
   public double volume() {
   throw new UnsupportedOperationException();
   }
   }
   
   public class Cube implements Shape {
   private int edge;
   public Cube(int edge) {
   this.edge = edge;
   }
   @Override
   public double area() {
   return 6 * edge * edge;
   }
   @Override
   public double volume() {
   return edge * edge * edge;
   }
   }
   ```
**ОТВЕТ**
  ```agsl
 public interface Shape3D {
   double area();
   double volume();
   }
   public interface Shape2D {
   double area();
   }
   
   public class Circle implements Shape2D{
   private double radius;
   public Circle(double radius) {
   this.radius = radius;
   }
   @Override
   public double area() {
   return 2 * 3.14 * radius;
   }
   
public class Cube implements Shape3D{
private int edge;
public Cube(int edge) {
this.edge = edge;
}
@Override
public double area() {
return 6 * edge * edge;
}
@Override
public double volume() {
return edge * edge * edge;
}
}
```

 
 
 Задачи со *(подсказок нет!, это же сложные задания)
4) Переписать код в соответствии с Liskov Substitution Principle:
```agsl


public class Rectangle {
   private int width;
   private int height;
   
   public void setWidth(int width) {
   this.width = width;
   }
   public void setHeight(int height) {
   this.height = height;
   }
   public int area() {
   return this.width * this.height;
   }
   }
   
   public class Square extends Rectangle {
   @Override
   public void setWidth(int width) {
   super.width = width;
   super.height = width;
   }
   @Override
   public void setHeight(int height) {
   super.width = height;
   super.height = height;
   }
   }
```
**ОТВЕТ**:
```agsl
 public class Square extends Rectangle {
   @Override
   public void setWidth(int width) {
   super.width = width; // здесь оставить как и прямоугольника 
   }
   @Override
   public void setHeight(int height) {
   super.height = height; // здесь оставить как и прямоугольника 
   }
```



5) Переписать код в соответствии с Dependency Inversion Principle:
```agsl

   public class Car {
   private PetrolEngine engine;
   
   public Car(PetrolEngine engine) {
   this.engine = engine;
   }
   public void start() {
   this.engine.start();
   }
   }
   public class PetrolEngine {
   public void start() {
   }
   }
   ```
ОТВЕТ
```agsl

   public class Car {
   private Engine engine;
   
   public Car(Engine engine) {
   this.engine = engine;
   }
   public void start() {
   this.engine.start();
   }
   }
      
   public class Engine {
   public void start() {
   }
   
   public class PetrolEngine extends Engine {
   public String type = petrol;
   }
   }
   public class DieselEngine extends Engine {
   public String type = diesel;
   }
   }
   
   
   }
```

