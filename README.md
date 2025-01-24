# 🚗 CarTopia

Welcome to **CarTopia**, a modern web application designed for buying and selling cars. This platform allows users, dealers, and admins to interact seamlessly, providing a sleek and user-friendly experience for everyone involved.

---

## 📖 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [License](#license)

---

## 🔍 About the Project

The Car Marketplace application allows users to:
- **Search for cars** with filters (make, model, price, year, etc.).
- **View detailed car listings** with images and important specifications.
- **Interact with dealers** by viewing their listings and leaving ratings.

The platform also enables dealers to post and manage their car listings after admin approval, ensuring a trusted ecosystem for buyers. Admins oversee the platform, managing dealers, users, and car listings.

---

## ✨ Features

### General Features
- Modern and responsive user interface.
- Filtered search with pagination (20 results per page).
- Detailed car listings with images and dealer information.

### Role-Specific Features
- **Guest:**
  - Browse car listings and view details.
- **User:**
  - Register/login to create car listings and rate dealers (after confirmed purchases).
- **Dealer:**
  - Apply for a dealer account (requires admin approval).
  - Manage personal car listings (add/edit/delete).
- **Admin:**
  - Approve or deny dealer registration requests.
  - Manage all car listings and moderate platform activity.

---

## 🛠 Technologies Used

### Frontend
- **Next.js**: For server-side rendering and a dynamic user interface.
- **TailwindCSS**: For modern, responsive, and customizable styling.

### Backend
- **Node.js** with **Express**: For building RESTful APIs.
- **PostgreSQL**: As the relational database for data storage.

### Others
- **JSON Web Tokens (JWT)**: For secure authentication and role-based access.
- **Vercel**: For hosting the frontend.
- **Heroku/DigitalOcean**: For hosting the backend and database.

---

## ⚙️ Installation

To set up the project locally, follow these steps:

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/car-marketplace.git
   cd car-marketplace
   ```
2. **Install Dependencies**
   - Frontend
   ```bash
   cd frontend
   npm install
   ```
   - Backend
   ```bash
   cd backend
   npm install
   ```
3. **Set Up Envirement Variables**
  - Create a `.env` file in the backend directory and configure the following variables:
   ```
    DATABASE_URL=your-database-url
    JWT_SECRET=your-jwt-secret
    EMAIL_SERVICE_CONFIG=your-email-service-config
   ```
4. **Run the Application**
   - Frontend
     ```bash
     cd frontend
     npm run dev
     ```
   -Backend
   ```bash
   cd backend
   npm start
   ```
5. **Access the Application**
   - Open your browser and go to `http://localhost:3000`.

---

## 📁 Project Structure

### Frontend (Next.js)
```
frontend/ 
├── components/           -Reusable UI components 
├── pages/                -Next.js pages 
├── styles/               -TailwindCSS styling 
└── public/               -Static assets
```

### Backend (Node.js)
```
backend/ 
├── controllers/          -API endpoint logic 
├── models/               -Database models 
├── routes/               -API routes 
├── middlewares/          -Authentication & validation logic 
└── utils/                -Utility functions
```

---

## 🔗 API Endpoints

### Authentication
| Endpoint               | Method | Description                     |
|------------------------|--------|---------------------------------|
| `/api/users/register`  | POST   | Register a new user.            |
| `/api/users/login`     | POST   | Login for users and dealers.    |

### Cars
| Endpoint               | Method | Description                     |
|------------------------|--------|---------------------------------|
| `/api/cars`            | GET    | Fetch all car listings.         |
| `/api/cars/:id` | GET | Fetch a single car by ID. |
| `/api/cars` | POST | Add a new car (Dealer/Admin). |
| `/api/cars/:id` | PUT | Update a car listing. |
| `/api/cars/:id` | DELETE | Delete a car listing. |

### Dealers
| Endpoint               | Method | Description                     |
|------------------------|--------|---------------------------------|
| `/api/dealers/register`  | POST   | Apply for dealer registration.            |
| `/api/dealers/approve`     | PUT   | Approve dealer registration (Admin).    |

--- 

## 📜 License

This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute this software as long as you include the original license file.

See the [LICENSE](./LICENSE) file for more details.
