# Food-Wate-Management

# FoodBridge - Food Waste Reduction Platform

A web-based platform designed to reduce food waste by connecting hotels and restaurants with NGOs (such as orphanages and old age homes). The platform enables efficient food donation management with real-time tracking and expiry monitoring.

## 🌟 Features

- **Surplus Food Logging**: Hotels and restaurants can log surplus food with detailed information
- **NGO Matching**: Automatic matching system to connect food donors with nearby NGOs
- **Real-time Countdown Timer**: Track food expiry with live countdown timers
- **Donation Tracking**: Complete donation history and analytics
- **User Management**: Separate dashboards for donors (hotels/restaurants) and recipients (NGOs)
- **Location-based Matching**: Find nearby NGOs for efficient food distribution
- **Notification System**: Real-time alerts for new donations and expiring food

## 🛠️ Tech Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Backend**: Node.js, Express.js
- **Database**: MongoDB
- **Real-time Updates**: WebSocket/Socket.io
- **Authentication**: JWT (JSON Web Tokens)

## 📋 Prerequisites

Before running this project, make sure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [MongoDB](https://www.mongodb.com/) (v4.4 or higher)
- [Git](https://git-scm.com/)

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/foodbridge-platform.git
cd foodbridge-platform
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Create a `.env` file in the root directory:

```env
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/foodbridge
DB_NAME=foodbridge

# Server Configuration
PORT=3000
NODE_ENV=development

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d

# Email Configuration (Optional)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_EMAIL=your_email@gmail.com
SMTP_PASSWORD=your_email_password

# Google Maps API (Optional)
GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```

### 4. Database Setup

Start MongoDB service:

```bash
# On Windows
net start MongoDB

# On macOS (using Homebrew)
brew services start mongodb-community

# On Linux
sudo systemctl start mongod
```

The application will automatically create the necessary collections on first run.

### 5. Run the Application

```bash
# Development mode
npm run dev

# Production mode
npm start
```

Visit `http://localhost:3000` in your browser.

## 📁 Project Structure

```
foodbridge-platform/
│
├── public/                 # Static frontend files
│   ├── css/
│   │   ├── style.css      # Main stylesheet
│   │   ├── dashboard.css   # Dashboard styles
│   │   └── responsive.css  # Mobile responsive styles
│   ├── js/
│   │   ├── main.js        # Main JavaScript file
│   │   ├── dashboard.js   # Dashboard functionality
│   │   ├── timer.js       # Countdown timer logic
│   │   └── auth.js        # Authentication handling
│   ├── images/            # Static images
│   └── index.html         # Landing page
│
├── src/                   # Backend source code
│   ├── controllers/       # Route controllers
│   │   ├── authController.js
│   │   ├── donationController.js
│   │   └── userController.js
│   ├── models/           # MongoDB models
│   │   ├── User.js
│   │   ├── Donation.js
│   │   └── NGO.js
│   ├── routes/           # API routes
│   │   ├── auth.js
│   │   ├── donations.js
│   │   └── users.js
│   ├── middleware/       # Custom middleware
│   │   ├── auth.js
│   │   └── validation.js
│   ├── utils/           # Utility functions
│   │   ├── database.js
│   │   └── email.js
│   └── app.js           # Express app configuration
│
├── views/               # HTML templates
│   ├── dashboard-donor.html
│   ├── dashboard-ngo.html
│   ├── login.html
│   └── register.html
│
├── .env.example         # Environment variables example
├── .gitignore          # Git ignore file
├── package.json        # NPM dependencies
├── server.js           # Server entry point
└── README.md          # Project documentation
```

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update user profile

### Donations
- `GET /api/donations` - Get all donations
- `POST /api/donations` - Create new donation
- `GET /api/donations/:id` - Get specific donation
- `PUT /api/donations/:id` - Update donation
- `DELETE /api/donations/:id` - Delete donation
- `POST /api/donations/:id/claim` - Claim donation (NGO)

### Users
- `GET /api/users/ngos` - Get all registered NGOs
- `GET /api/users/donors` - Get all donors
- `PUT /api/users/location` - Update user location

## 📊 Database Schema

### Users Collection
```javascript
{
  _id: ObjectId,
  name: String,
  email: String,
  password: String (hashed),
  userType: String, // 'donor' or 'ngo'
  phone: String,
  address: {
    street: String,
    city: String,
    state: String,
    zipCode: String,
    coordinates: {
      lat: Number,
      lng: Number
    }
  },
  verified: Boolean,
  createdAt: Date,
  updatedAt: Date
}
```

### Donations Collection
```javascript
{
  _id: ObjectId,
  donorId: ObjectId,
  foodType: String,
  quantity: Number,
  unit: String,
  expiryTime: Date,
  description: String,
  status: String, // 'available', 'claimed', 'completed'
  claimedBy: ObjectId, // NGO ID
  pickupTime: Date,
  location: {
    address: String,
    coordinates: {
      lat: Number,
      lng: Number
    }
  },
  createdAt: Date,
  updatedAt: Date
}
```

## 🎨 Frontend Features

### Real-time Countdown Timer
The platform includes a sophisticated countdown timer system that:
- Displays remaining time until food expiry
- Changes color based on urgency (green → yellow → red)
- Automatically updates donation status when expired
- Sends notifications before expiry

### Responsive Design
- Mobile-first design approach
- Bootstrap-like grid system
- Touch-friendly interface for mobile devices

### Interactive Dashboard
- Different views for donors and NGOs
- Real-time updates using WebSocket
- Interactive maps for location-based matching

## 🔒 Security Features

- Password hashing using bcrypt
- JWT-based authentication
- Input validation and sanitization
- Rate limiting on API endpoints
- CORS configuration
- SQL injection prevention (NoSQL injection for MongoDB)

## 📱 Usage

### For Hotels/Restaurants (Donors):
1. Register as a donor
2. Log surplus food with details and expiry time
3. View nearby NGOs interested in donations
4. Track donation status and history
5. Receive notifications when food is claimed

### For NGOs (Recipients):
1. Register as an NGO
2. Browse available food donations
3. Claim suitable donations
4. Coordinate pickup with donors
5. Track donation history and impact



**Made with ❤️ to reduce food waste and help communities in need.**
