# Product Requirements Document (PRD)

## Car Marketplace Web Application

---

### 1. Overview
The application is a car marketplace with a modern user interface. It allows users to search for cars, view detailed listings, and interact with dealers. It supports role-based access for guests, registered users, dealers, and admins. 

---

### 2. Architecture
- **Frontend:** Next.js with TailwindCSS
- **Backend:** Node.js with Express
- **Database:** PostgreSQL 
- **Authentication:** JSON Web Tokens (JWT)
- **Deployment:** 
  - Frontend: Vercel
  - Backend: Heroku 

---

### 3. Roles & Permissions
| **Role**   | **Capabilities**                                                                                         |
|------------|----------------------------------------------------------------------------------------------------------|
| Guest      | Perform searches, view car listings, and read car details, register/login.                               |
| User       | Post car listings, and leave dealer ratings after confirmed purchases.                                   |
| Dealer     | Apply for dealer account approval, manage their car listings (add/edit/delete).                          |
| Admin      | Manage all users, approve/reject dealer applications, and delete or update car listings.                 |

---

### 4. User Flow

#### **Guest**
1. Access the homepage with a filtered search form.
2. Perform searches and view car listings (20 per page).
3. Open car details by clicking on car cards.

#### **User**
1. Register/login.
2. Post car listings.
3. Leave dealer ratings (after purchase confirmation).

#### **Dealer**
1. Apply for a dealer account (admin approval required).
2. Add, edit, or delete car listings.

#### **Admin**
1. Approve/deny dealer registration requests.
2. Manage all car listings (CRUD operations).
3. Moderate user activity (e.g., suspend accounts).

---

### 5. Application Pages

#### **Frontend (Next.js):**
- `pages/index.js`: Homepage with filtered search.
- `pages/cars/[id].js`: Car details page.
- `pages/auth/login.js`: Login form.
- `pages/auth/register.js`: Registration form.
- `pages/dealer/apply.js`: Dealer application form.
- `pages/admin/index.js`: Admin dashboard.

#### **Components:**
- `CarCard.js`: Reusable car listing card.
- `SearchForm.js`: Search filters.
- `Layout.js`: Header, footer, and global layout.
- `Pagination.js`: Pagination for car listings.

#### **UI Design:**
- TailwindCSS is used for responsive design.
- Animations with Framer Motion for transitions.

---

### 6. Database Schema
#### **Users Table**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255),
    role ENUM('guest', 'user', 'dealer', 'admin') DEFAULT 'guest',
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
#### **Cars Table**
```sql
CREATE TABLE cars (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255),
    description TEXT,
    price DECIMAL(10, 2),
    make VARCHAR(100),
    model VARCHAR(100),
    year INT,
    mileage INT,
    image_url TEXT,
    dealer_id INT REFERENCES users(id) ON DELETE CASCADE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
#### **Dealer applications Table**
```sql
CREATE TABLE dealer_applications (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id) ON DELETE CASCADE,
    business_name VARCHAR(255),
    business_email VARCHAR(255),
    status ENUM('pending', 'approved', 'rejected') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
#### **Ratings Table**
```sql
CREATE TABLE ratings (
    id SERIAL PRIMARY KEY,
    dealer_id INT REFERENCES users(id) ON DELETE CASCADE,
    user_id INT REFERENCES users(id) ON DELETE CASCADE,
    rating INT CHECK(rating >= 1 AND rating <= 5),
    review TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### 7. Backend API Endpoints

| **Endpoint**            | **Method** | **Role**             | **Description**                              |
|--------------------------|------------|----------------------|----------------------------------------------|
| `/api/cars`             | GET        | Guest/User/Dealer    | Fetch filtered car listings.                |
| `/api/cars/:id`         | GET        | Guest/User/Dealer    | Fetch car details.                          |
| `/api/cars`             | POST       | Dealer/Admin         | Create a car listing.                       |
| `/api/cars/:id`         | PUT        | Dealer/Admin         | Update a car listing.                       |
| `/api/cars/:id`         | DELETE     | Dealer/Admin         | Delete a car listing.                       |
| `/api/dealers/register` | POST       | Guest                | Submit dealer registration request.         |
| `/api/dealers/approve`  | PUT        | Admin                | Approve dealer registration.                |
| `/api/users/register`   | POST       | Guest                | Register a user.                            |
| `/api/users/login`      | POST       | Guest                | User/Dealer/Admin login.                    |
| `/api/ratings`          | POST       | User                 | Add a rating for a dealer.                  |

---

### 8. Authentication
- **Method:** JSON Web Tokens (JWT)
- **Access Control:**
  - Middleware for role-based permissions in the backend.

---

### 9. Deployment
- **Frontend:** Deploy on Vercel.
- **Backend:** Deploy on Heroku.

---

### 10. Future Enhancements
- **Search Suggestions:** Autocomplete in search.
- **Email Notifications:** Notify users about dealer approvals and updates.
- **Favorites:** Allow users to save favorite car listings.

---

### 11. Summary
This document outlines the functional and non-functional requirements for the car marketplace application. The monolithic architecture ensures fast deployment while maintaining scalability. By leveraging modern technologies like Next.js and Node.js, the application will provide a seamless user experience for all roles.


