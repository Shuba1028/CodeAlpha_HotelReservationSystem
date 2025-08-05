# 🏨 CodeAlpha Hotel Reservation System

This project is a **console-based hotel reservation system in Java**, developed during the **CodeAlpha Java Internship**.  
Users can view rooms, book a room under their name, and cancel a reservation — all through a simple terminal interface.

---

## 💡 Features

- 🏠 View available hotel rooms
- 🛏️ Book a room (Standard, Deluxe, Suite)
- ❌ Cancel a booking
- 🧠 Simple input handling & room availability check
- 💻 100% console-based Java application

---

## 🖥️ Code
import java.util.*;

class Room {
    int number;
    String category;
    boolean isBooked;

    Room(int number, String category) {
        this.number = number;
        this.category = category;
        this.isBooked = false;
    }
}

public class Main {
    static List<Room> rooms = new ArrayList<>();
    static Map<Integer, String> bookings = new HashMap<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeRooms();

        while (true) {
            System.out.println("\n🏨 Hotel Reservation System");
            System.out.println("1. View Available Rooms");
            System.out.println("2. Book a Room");
            System.out.println("3. Cancel a Booking");
            System.out.println("4. Exit");
            System.out.print("Select option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    viewAvailableRooms();
                    break;
                case 2:
                    bookRoom();
                    break;
                case 3:
                    cancelBooking();
                    break;
                case 4:
                    System.out.println("Thanks for using Hotel Reservation System.");
                    return;
                default:
                    System.out.println("Invalid option.");
            }
        }
    }

    static void initializeRooms() {
        rooms.add(new Room(101, "Standard"));
        rooms.add(new Room(102, "Deluxe"));
        rooms.add(new Room(103, "Suite"));
        rooms.add(new Room(104, "Standard"));
        rooms.add(new Room(105, "Deluxe"));
    }

    static void viewAvailableRooms() {
        System.out.println("\nAvailable Rooms:");
        for (Room room : rooms) {
            if (!room.isBooked) {
                System.out.println("Room " + room.number + " - " + room.category);
            }
        }
    }

    static void bookRoom() {
        System.out.print("Enter your name: ");
        scanner.nextLine(); // consume newline
        String name = scanner.nextLine();

        System.out.print("Enter room number to book: ");
        int roomNum = scanner.nextInt();

        for (Room room : rooms) {
            if (room.number == roomNum) {
                if (!room.isBooked) {
                    room.isBooked = true;
                    bookings.put(roomNum, name);
                    System.out.println("Room " + roomNum + " successfully booked under name: " + name);
                    return;
                } else {
                    System.out.println("Room already booked.");
                    return;
                }
            }
        }

        System.out.println("Room not found.");
    }

    static void cancelBooking() {
        System.out.print("Enter room number to cancel: ");
        int roomNum = scanner.nextInt();

        if (bookings.containsKey(roomNum)) {
            bookings.remove(roomNum);
            for (Room room : rooms) {
                if (room.number == roomNum) {
                    room.isBooked = false;
                    break;
                }
            }
            System.out.println("Booking for room " + roomNum has been canceled.");
        } else {
            System.out.println("No booking found for that room.");
        }
    }
}
## 🖥️ Sample Output
🏨 Hotel Reservation System

View Available Rooms
Book a Room
Cancel a Booking
Exit

Select option: 1

Available Rooms:
Room 101 - Standard
Room 102 - Deluxe
Room 103 - Suite

