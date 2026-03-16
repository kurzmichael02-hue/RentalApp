# RentalApp

A Java console application for managing a vehicle rental business — built as a semester project at DHBW Mannheim (Semester 2, TINF24IT1).

The idea was pretty simple: a rental company wants to go digital. So I built a full CRUD system for vehicles and customers, with role-based access, sorting, reporting, and file export — all running in the terminal.

---

## What it does

**Vehicle management** — add, edit, delete, and search cars, electric cars, and motorcycles. Each type has its own attributes (battery capacity for EVs, bike type and 0–100 acceleration for motorcycles, etc.).

**Customer management** — store customer profiles with name, address, and email. Link them to rentals.

**Rental workflow** — interactive checkout and return process including a handover protocol (mileage, fuel/charge level, damage notes).

**Sorting** — sort the full fleet by value, manufacturer, mileage, or rental status using custom `Comparator` implementations.

**Reporting** — view currently rented vehicles, fleet statistics (count by type, rental rate, total fleet value), and export everything to a file.

**Role-based access** — admin login (`admin` / `secret`) unlocks create, edit, delete, and export features. Regular users can browse and sort.

---

## Project structure

```
de.s242010.RentalApp/
├── RentalApp.java          # Main class — menu, login, all business logic

de.s242010.customer/
├── Customer.java           # Customer model with auto-generated ID

de.s242010.vehicle/
├── Rentable.java           # Abstract base class (id, value, isRented, customer ref)
├── Vehicle.java            # Extends Rentable — VIN, plate, mileage, fuel, power
├── Car.java                # Extends Vehicle — conventional car
├── ElectricCar.java        # Extends Car — adds battery capacity + charging power
├── Motorcycle.java         # Extends Vehicle — adds bike type + 0-100 boost
├── Vehiclecomp.java        # Comparator: sort by value
├── Vehiclemanucomp.java    # Comparator: sort by manufacturer
├── VehicleMileageComp.java # Comparator: sort by mileage
└── VehicleRentalStatusComp.java  # Comparator: sort by rental status
```

---

## Class hierarchy

```
Rentable  (abstract)
└── Vehicle
    ├── Car
    │   └── ElectricCar
    └── Motorcycle
```

`Rentable` is the top-level abstract class — it handles the shared stuff: unique ID (auto-incremented), description, value, rental status, and the customer reference. `Vehicle` extends it with everything vehicle-specific (VIN, license plate, mileage, etc.). From there, `Car`, `ElectricCar`, and `Motorcycle` each add their own type-specific fields.

---

## How to run

**Option 1 — JAR file**
```bash
java -jar RentalApp.jar
```

**Option 2 — From source (Eclipse)**
Import as *Existing Projects into Workspace*, then run `RentalApp.java` as a Java Application.

**Login credentials**
| Role | Username | Password |
|------|----------|----------|
| Admin | `admin` | `secret` |
| User | anything else | anything |

---

## Tech stack

- **Language:** Java (JDK 21)
- **Module:** `de.s242010.RentalApp`
- **Data structures:** `ArrayList` with Java Collections
- **OOP concepts:** Inheritance, abstract classes, interfaces, `Comparator`, encapsulation, polymorphism
- **I/O:** Console (Scanner), file export via `PrintWriter` + `java.nio.file`

---

## Export

Admin users can export the full vehicle list to a file:

```
export/export.txt
```

The file is created relative to the working directory and lists all vehicle attributes separated by dashes.

---

## Status

✅ Completed — DHBW Mannheim, Semester 2 (submitted June 2025)
