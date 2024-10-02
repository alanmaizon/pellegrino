# pellegrino
ERD for a travel agency
```mermaid
erDiagram
    CUSTOMER {
        int id PK
        string name
        string email
        string phone
        string address
        datetime created_at
    }

    FLIGHT {
        int id PK
        string airline
        string flight_number
        string origin
        string destination
        datetime departure_time
        datetime arrival_time
        float price
        int available_seats
    }

    HOTEL {
        int id PK
        string name
        string location
        float price_per_night
        int available_rooms
    }

    TOUR {
        int id PK
        string name
        string destination
        datetime start_date
        datetime end_date
        float price
        int available_spots
    }

    BOOKING {
        int id PK
        int customer_id FK
        int flight_id FK
        int hotel_id FK
        int tour_id FK
        datetime booking_date
        string status
        float total_price
    }

    EMPLOYEE {
        int id PK
        string name
        string email
        string role
    }

    INVENTORY_UPDATE {
        int id PK
        int employee_id FK
        int flight_id FK
        int hotel_id FK
        int tour_id FK
        string update_type
        datetime update_time
        float new_price
    }

    MANAGER {
        int id PK
        string name
        string email
    }

    REPORT {
        int id PK
        int manager_id FK
        datetime report_date
        string report_type
        text content
    }

    CUSTOMER ||--o{ BOOKING : "makes"
    FLIGHT ||--o{ BOOKING : "part of"
    HOTEL ||--o{ BOOKING : "part of"
    TOUR ||--o{ BOOKING : "part of"
    EMPLOYEE ||--o{ INVENTORY_UPDATE : "makes"
    INVENTORY_UPDATE ||--o{ FLIGHT : "updates"
    INVENTORY_UPDATE ||--o{ HOTEL : "updates"
    INVENTORY_UPDATE ||--o{ TOUR : "updates"
    MANAGER ||--o{ REPORT : "generates"
