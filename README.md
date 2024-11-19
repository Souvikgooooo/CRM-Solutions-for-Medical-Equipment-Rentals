# Book Rental CRM Project

The **Medical Equipment Rental CRM system** automates the management of medical equipment rentals, customer interactions, billing, and reminders for overdue equipment. This system leverages Salesforce components such as objects, validation rules, flows, Apex classes, and dashboards to deliver a streamlined rental experience. The primary goal is to enhance the rental process by providing automated reminders, real-time availability updates, and efficient billing management, ensuring healthcare providers have timely access to essential equipment.

## Objectives

The project aims to achieve the following business goals:
- To automate and streamline the process of renting medical equipment to customers, reducing manual effort and increasing operational efficiency.
- To track customer interactions, equipment availability, rental histories, and membership statuses in an organized manner for improved customer relationship management (CRM).
- To generate timely billing and reminders for late fees, enhancing customer experience and ensuring prompt returns of rented equipment.

### Specific Outcomes
- A fully functioning CRM platform for managing medical equipment rentals, billing, and customer information.
- Implementation of an automated billing system that accurately calculates rental fees and late charges.
- Integration of overdue equipment reminder functionality to minimize delays in returns.
- Easy tracking of customer details, rental history, and payment statuses for administrative staff.


## Salesforce Key Features and Concepts Utilized

- **Custom Objects**: Used to define the "Medical Equipment," "Customer," and "Rental Process" objects.
- **Formula Fields**: Utilized in the Rental Process object to calculate total rental amounts and manage late fees.
- **Automated Workflows**: Implemented to send reminders for overdue equipment based on return dates and due date logic.
- **Validation Rules**: Applied to ensure accurate and consistent data input across the system (e.g., ensuring a rental fee is always applied when equipment is rented).
- **Relationships**: Lookup fields to manage associations between Medical Equipment, Customers, and Rental records.
- **Apex Triggers**: For handling complex operations like updating inventory or customer records when a rental transaction occurs.

## Apex Code 
```java
public class MedicalEquipmentBookingHandler {
    public static void sendNotification(List<Equipment_Bookings__c> bookingList) {
        for (Equipment_Bookings__c booking : bookingList) {
            // Example of sending email (customize fields as needed)
            Messaging.SingleEmailMessage email = new Messaging.SingleEmailMessage();
            email.setToAddresses(new List<String>{booking.Patient_Name__c});
            email.setSubject('Booking Confirmation');
            String body = 'Dear Customer, your booking has been confirmed.';
            email.setPlainTextBody(body);
            Messaging.sendEmail(new List<Messaging.SingleEmailMessage>{email});
        }
    }
}
```
## Apex Trigger 
```java
trigger MedicalEquipmentBookings on Equipment_Bookings__c (before insert) {
    for (Equipment_Bookings__c booking : Trigger.new) {
        // Determine Equipment Type
        if (booking.Equipment_Type__c == 'X-Ray') {
            if (booking.Rental_Duration__c == 1) {
                booking.Amount__c = 1000; // Amount for 1-month X-Ray rental
            } else if (booking.Rental_Duration__c == 2) {
                booking.Amount__c = 2000; // Amount for 2-month X-Ray rental
            }
        } else if (booking.Equipment_Type__c == 'MRI Machine') {
            if (booking.Rental_Duration__c == 1) {
                booking.Amount__c = 3000; // Amount for 1-month MRI rental
            } else if (booking.Rental_Duration__c == 3) {
                booking.Amount__c = 6000; // Amount for 3-month MRI rental
            } else if (booking.Rental_Duration__c == 6) {
                booking.Amount__c = 12000; // Amount for 6-month MRI rental
            }
        } else if (booking.Equipment_Type__c == 'CT Scanner') {
            if (booking.Rental_Duration__c == 2) {
                booking.Amount__c = 5000; // Amount for 2-month CT Scanner rental
            } else if (booking.Rental_Duration__c == 4) {
                booking.Amount__c = 10000; // Amount for 4-month CT Scanner rental
            }
        } else {
            // Default or unmatched cases
            booking.Amount__c = 0; // Set to 0 or handle as per business logic
        }
    }
}
```


## Testing and Validation

The project has been thoroughly tested through:
- **Unit Testing**: Apex classes and triggers have been unit tested to ensure functionality.
- **User Interface Testing**: Manual and automated tests have been conducted on the UI to ensure smooth customer interactions.

## Key Scenarios Addressed by Salesforce
- Booking Management: Automates the creation and management of medical equipment bookings (e.g., X-Ray, MRI, CT Scan) with details like equipment type, rental duration, and customer information.
- Customer Communication: Sends confirmation emails to customers upon successful booking, ensuring they are notified about the rental details and equipment delivery.
- Equipment Availability Updates: Automatically updates the available stock of medical equipment as bookings are made or canceled, helping to manage inventory.
- Rental Duration and Billing: Manages different rental durations (e.g., 1 month, 2 months, 3 months) for each type of medical equipment and updates billing amounts accordingly.
- Late Returns and Penalties: Identifies late returns and applies late fees, ensuring proper penalties are charged for equipment that is returned past the due date.
- Record Updates: Ensures accurate record updates for equipment, patient information, and billing during each phase of the booking process (renting, returning, updating).
- Automated Workflow: Implements a smooth workflow for creating, updating, and closing bookings based on triggers, reducing manual work and improving efficiency.
- Custom Alerts and Notifications: Configures custom notifications and reminders for customers, helping them stay informed about the booking status, due dates, and potential penalties.
- Reporting and Analytics: Provides insights into booking trends, revenue, equipment usage, and customer behavior by utilizing Salesforce's reporting and dashboard features.
- These scenarios enable a more efficient and streamlined management system for medical equipment rentals, improving both internal processes and customer satisfaction.


## Documentation

For a detailed description of the project, including objectives, key features, and testing, refer to the project documentation:
📝 [Project Documentation](https://docs.google.com/document/d/1VxfKImkAsb5neQ3cq0rNk_chs-wnVO99g2Czeb7VWIA/edit?usp=sharing)

## Video Link
For a detailed demonstration video click here: 🎥 [Video Link]()

---

Feel free to explore the project and contribute if you'd like to enhance its features or improve the functionality!
