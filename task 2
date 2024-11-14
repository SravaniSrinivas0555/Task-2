-- Database Schema for Hotel Booking System

-- 1. Customers Table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone_number VARCHAR(15),
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 2. Rooms Table
CREATE TABLE Rooms (
    room_id INT PRIMARY KEY AUTO_INCREMENT,
    room_number VARCHAR(10) UNIQUE NOT NULL,
    room_type VARCHAR(50) NOT NULL,
    price_per_night DECIMAL(10, 2) NOT NULL,
    max_occupancy INT NOT NULL,
    status ENUM('available', 'booked', 'maintenance') DEFAULT 'available',
    description TEXT
);

-- 3. Reservations Table
CREATE TABLE Reservations (
    reservation_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    room_id INT,
    check_in_date DATE NOT NULL,
    check_out_date DATE NOT NULL,
    total_amount DECIMAL(10, 2) NOT NULL,
    reservation_status ENUM('confirmed', 'checked-in', 'checked-out', 'canceled') DEFAULT 'confirmed',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id) ON DELETE CASCADE,
    FOREIGN KEY (room_id) REFERENCES Rooms(room_id) ON DELETE CASCADE
);

-- 4. Payments Table
CREATE TABLE Payments (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    reservation_id INT,
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    amount DECIMAL(10, 2) NOT NULL,
    payment_method ENUM('credit_card', 'debit_card', 'cash', 'online') NOT NULL,
    payment_status ENUM('completed', 'pending', 'failed') DEFAULT 'completed',
    FOREIGN KEY (reservation_id) REFERENCES Reservations(reservation_id) ON DELETE CASCADE
);

-- Sample Queries

-- Insert new customer
INSERT INTO Customers (first_name, last_name, email, phone_number, address)
VALUES ('John', 'Doe', 'johndoe@example.com', '1234567890', '123 Main St, City');

-- Add a room
INSERT INTO Rooms (room_number, room_type, price_per_night, max_occupancy, description)
VALUES ('101', 'Deluxe', 120.00, 2, 'Deluxe room with king-sized bed and city view');

-- Create a reservation
INSERT INTO Reservations (customer_id, room_id, check_in_date, check_out_date, total_amount)
VALUES (1, 1, '2024-11-15', '2024-11-20', 600.00);

-- Record a payment
INSERT INTO Payments (reservation_id, amount, payment_method)
VALUES (1, 600.00, 'credit_card');

-- Check availability of a room
SELECT * FROM Rooms
WHERE room_id = 1 AND status = 'available';

-- List all reservations of a customer
SELECT r.*, c.first_name, c.last_name
FROM Reservations r
JOIN Customers c ON r.customer_id = c.customer_id
WHERE c.customer_id = 1;

-- Calculate total earnings
SELECT SUM(amount) AS total_earnings FROM Payments WHERE payment_status = 'completed';
