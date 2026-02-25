# Inventory Management System

A full-stack web application for managing inventory with real-time updates, analytics, and a modern user interface. This system allows users to track products, monitor stock levels, and analyze inventory data with interactive charts and dashboards.

> 🎓 **Group Project** — This is a collaborative team project. 

---

## Features

- 🔐 **User Authentication** — Secure registration and login system with JWT tokens
- 📦 **Product Management** — Create, read, update, and delete products
- 📊 **Analytics Dashboard** — Visual analytics with charts and inventory insights
- 🔄 **Real-time Updates** — Socket.io integration for live inventory updates
- 📱 **Responsive Design** — Modern UI built with React and Tailwind CSS
- 🎨 **Beautiful Charts** — Interactive data visualization using Recharts
- 🔍 **Product Search & Filter** — Easy product discovery and management

---


## Tech Stack

### Frontend
- **React 18** — Modern React with hooks
- **TypeScript** — Type-safe development
- **Vite** — Fast build tool and dev server
- **React Router** — Client-side routing
- **Tailwind CSS** — Utility-first CSS framework
- **Zustand** — Lightweight state management
- **React Query** — Data fetching and caching
- **Recharts** — Chart and data visualization
- **Socket.io Client** — Real-time communication
- **Lucide React** — Beautiful icons

### Backend
- **Node.js** — JavaScript runtime
- **Express** — Web application framework
- **MongoDB** — NoSQL database
- **Mongoose** — MongoDB object modeling
- **JWT** — JSON Web Token authentication
- **bcrypt** — Password hashing
- **Socket.io** — Real-time bidirectional communication
- **Zod** — Schema validation

---

## My Contribution — MongoDB & Server-Side Item Management

As part of this group project, my responsibility was to implement the **MongoDB database connection** and all **server-side CRUD operations** for inventory items.

### MongoDB Connection (`server/config/`)

- Configured the Mongoose connection using the `MONGODB_URI` environment variable
- Handled connection events (connected, error, disconnected) with proper logging
- Ensured the database connection is established before the Express server starts accepting requests

### Item Data Model (`server/models/`)

Defined a Mongoose schema for inventory items with fields such as:
- `name` — Product name (unique identifier)
- `category` — Product category
- `quantity` — Stock quantity
- `price` — Unit price
- `description` — Optional product description
- `createdAt` / `updatedAt` — Timestamps

### Server-Side API Routes (`server/routes/`)

#### ➕ Add Item — `POST /products`

Handles creating a new inventory item:
1. Validates the incoming request body using the Zod schema
2. Checks if a product with the same name already exists in MongoDB
3. Creates and saves a new `Product` document to the database
4. Emits a real-time Socket.io event (`product:created`) to notify connected clients
5. Returns the newly created product with a `201 Created` response

```js
// Example request body
{
  "name": "Wireless Mouse",
  "category": "Electronics",
  "quantity": 50,
  "price": 29.99,
  "description": "Ergonomic wireless mouse"
}
```

#### ✏️ Update Item — `PUT /products/:name`

Handles updating an existing inventory item by name:
1. Finds the product in MongoDB by its `name` parameter
2. Validates the update fields using Zod
3. Applies the updates using `findOneAndUpdate` with `{ new: true }` to return the updated document
4. Emits a real-time Socket.io event (`product:updated`) to all connected clients
5. Returns the updated product with a `200 OK` response

```js
// Example request body
{
  "quantity": 35,
  "price": 24.99
}
```

#### 🗑️ Delete Item — `DELETE /products/:name`

Handles deleting an inventory item by name:
1. Finds and removes the product from MongoDB using `findOneAndDelete`
2. Returns `404 Not Found` if no product matches the given name
3. Emits a real-time Socket.io event (`product:deleted`) to notify connected clients
4. Returns a `200 OK` response with a success message upon deletion

```js
// Example response
{
  "message": "Product 'Wireless Mouse' deleted successfully"
}
```

---

## Prerequisites

Before running this application, make sure you have the following installed:

- **Node.js** (v14 or higher)
- **npm** or **yarn**
- **MongoDB** (local installation or MongoDB Atlas account)

---

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/bahasuru-naya/inventory-management-system.git
   cd inventory-management-system
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root directory:
   ```env
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   PORT=5000
   ```

   > **Note**: Replace `your_mongodb_connection_string` with your actual MongoDB URI (MongoDB Atlas or local) and `your_jwt_secret_key` with a secure random string.

---

## Running the Application

### Development Mode

1. **Start the backend server**
   ```bash
   npm run server
   ```
   The server will run on `http://localhost:5000`

2. **Start the frontend development server** (in a separate terminal)
   ```bash
   npm run dev
   ```
   The application will run on `http://localhost:5173`

3. **Access the application**

   Open your browser and navigate to `http://localhost:5173`

### Production Build

1. **Build the frontend**
   ```bash
   npm run build
   ```

2. **Preview the production build**
   ```bash
   npm run preview
   ```

---

## Project Structure

```
inventory-management-system/
├── server/                 # Backend code (Node.js + Express)
│   ├── config/            # MongoDB connection configuration
│   ├── middleware/        # Express middleware (auth, error handling)
│   ├── models/            # Mongoose models (Product, User)
│   ├── routes/            # API routes (products, auth)
│   ├── services/          # Business logic
│   ├── socket/            # Socket.io real-time event handlers
│   ├── validators/        # Zod input validation schemas
│   └── index.js           # Server entry point
├── src/                   # Frontend code (React + TypeScript)
│   ├── components/        # React components
│   │   ├── analytics/     # Analytics components
│   │   ├── products/      # Product components
│   │   └── ui/            # Reusable UI components
│   ├── hooks/             # Custom React hooks
│   ├── pages/             # Page components
│   │   ├── Dashboard.tsx  # Main dashboard
│   │   ├── Products.tsx   # Product management
│   │   ├── Analytics.tsx  # Analytics page
│   │   ├── Login.tsx      # Login page
│   │   └── Registration.tsx # Registration page
│   ├── services/          # API services
│   ├── store/             # State management (Zustand)
│   ├── types/             # TypeScript types
│   ├── App.tsx            # Main App component
│   └── main.tsx           # Entry point
├── public/                # Static assets
├── .env                   # Environment variables (create this)
├── package.json           # Dependencies and scripts
├── tailwind.config.js     # Tailwind CSS configuration
├── tsconfig.json          # TypeScript configuration
└── vite.config.ts         # Vite configuration
```

---



## Usage

1. **Registration** — Create a new account on the registration page
2. **Login** — Sign in with your credentials
3. **Dashboard** — View inventory overview and key metrics
4. **Products** — Add, edit, or delete products from your inventory
5. **Analytics** — Monitor inventory trends and product statistics

---

## Troubleshooting

### White Screen Error

If you encounter a white screen when opening the application:

1. Open browser developer tools (F12)
2. Go to the Console tab
3. Run the following command:
   ```javascript
   localStorage.clear()
   ```
4. Reload the browser

This clears the local storage and resolves authentication state issues.

### MongoDB Connection Error

If you see MongoDB connection errors:
- Verify your `MONGODB_URI` in the `.env` file
- Ensure MongoDB service is running (if using local MongoDB)
- Check your network connection (if using MongoDB Atlas)
- Verify that your IP address is whitelisted in MongoDB Atlas

### Port Already in Use

If you get a port conflict error:
- Change the `PORT` value in your `.env` file, or kill the process:
  ```bash
  # On Windows
  netstat -ano | findstr :5000
  taskkill /PID <PID> /F

  # On Linux/Mac
  lsof -ti:5000 | xargs kill -9
  ```

---


## Contributing

Contributions are welcome! For group members:

1. Fork or create a feature branch (`git checkout -b feature/your-feature`)
2. Commit your changes (`git commit -m 'Add some feature'`)
3. Push to the branch (`git push origin feature/your-feature`)
4. Open a Pull Request for review

---

## License

This project is open source and available under the [MIT License](LICENSE).
