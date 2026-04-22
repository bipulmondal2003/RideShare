# 🚗 RideShare - Carpooling Platform

A modern, full-stack carpooling application enabling drivers and passengers to share rides cost-effectively with real-time notifications and complete user management.

---

## ✨ Features

### Core Features
- **User Authentication** - JWT-based login with 3 roles (Driver, Passenger, Admin)
- **Ride Management** - Create, edit, search, and manage rides with status tracking
- **Booking System** - Request/approve bookings with automatic waitlist management
- **Real-time Chat** - Socket.io messaging between driver and passenger
- **Rating System** - 5-star ratings with trust score calculation
- **Recurring Rides** - Daily/weekly rides with automatic generation
- **Multi-seat Bookings** - Book multiple seats in one transaction
- **Admin Panel** - User management, analytics, ride monitoring, reports

### Advanced Features
- Real-time notifications via Socket.io
- Ride waypoints (intermediate stops)
- User reporting system with admin moderation
- Ban/unban user functionality
- Live seat availability updates
- Automatic waitlist promotion
- Monthly recurring ride patterns

---

## 🛠 Technology Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | HTML5, CSS3, Vanilla JavaScript, Socket.io |
| **Backend** | Node.js, Express.js, Mongoose ODM |
| **Database** | MongoDB |
| **Real-time** | Socket.io v4 |
| **Auth** | JWT (12-hour tokens) |
| **Build** | npm, nodemon (dev) |

---

## 📁 Project Structure
```
carpooling/
├── backend/                          # Node.js server
│   ├── controllers/                  # Business logic layer
│   │   ├── authController.js         # User registration & login
│   │   ├── rideController.js         # Ride CRUD operations
│   │   ├── bookingController.js      # Booking & waitlist logic
│   │   ├── messageController.js      # In-app chat
│   │   ├── ratingController.js       # Star ratings & reviews
│   │   ├── reportController.js       # User reports
│   │   └── adminController.js        # Admin dashboard & moderation
│   ├── models/                       # Database schemas (Mongoose)
│   │   ├── User.js                   # User model with trust score
│   │   ├── Ride.js                   # Ride with recurring & waypoints
│   │   ├── Booking.js                # Booking with multi-seat support
│   │   ├── Message.js                # Chat messages
│   │   ├── Rating.js                 # Star ratings with uniqueness
│   │   └── Report.js                 # User reports & moderation
│   ├── routes/                       # API endpoint definitions
│   │   ├── api.js                    # All API routes (45+ endpoints)
│   │   └── auth.js                   # Auth routes (register, login)
│   ├── middleware/                   # Request processing
│   │   └── auth.js                   # JWT validation & role checks
│   ├── scripts/                      # One-time utilities
│   │   └── createAdmin.js            # Admin seeder script
│   ├── socket.js                     # Socket.io configuration
│   ├── server.js                     # Express app & server entry
│   └── package.json                  # Dependencies & scripts
│
├── frontend/                         # Browser-based UI
│   ├── src/                          # Core application
│   │   ├── index.html                # Landing page (home)
│   │   ├── styles.css                # Complete design system
│   │   ├── app.js                    # Shared utilities & Socket.io
│   │   │                             # - AuthManager class
│   │   │                             # - Theme management
│   │   │                             # - Navigation builder
│   │   │                             # - Helper functions
│   │   └── socket.io.js              # (loaded from server)
│   │
│   ├── pages/                        # User-facing pages
│   │   ├── login.html                # Sign in form
│   │   ├── signup.html               # Registration with role selector
│   │   ├── dashboard.html            # Driver dashboard
│   │   ├── passenger-dashboard.html  # Passenger dashboard
│   │   ├── search-ride.html          # Ride search & filter
│   │   ├── offer-ride.html           # Create/edit ride (driver)
│   │   ├── my-rides.html             # Driver's rides list
│   │   ├── my-bookings.html          # Passenger's bookings list
│   │   ├── ride-details.html         # View single ride
│   │   ├── ride-bookings.html        # Driver: manage ride bookings
│   │   ├── profile.html              # User profile & settings
│   │   ├── chat.html                 # Real-time messaging
│   │   ├── rate.html                 # Post-ride rating form
│   │   │
│   │   └── admin/                    # Admin panel pages
│   │       ├── dashboard.html        # Platform analytics
│   │       ├── users.html            # User management
│   │       ├── rides.html            # Ride management
│   │       ├── bookings.html         # Booking management
│   │       └── reports.html          # User report moderation
│   │
│   └── components/                   # (Reserved for reusable components)
│
├── .env                              # Environment variables
├── .gitignore                        # Git ignore file
├── package.json                      # Project metadata
├── README.md                         # Quick start guide

---

  change admin--------------
PS D:\Projects\RideShare\backend> npm run seed:admin
> carpooling-platform@2.0.0 seed:admin
> node backend/scripts/createAdmin.js
Connected to MongoDB
✅ Admin created: rajmondal3503@gmail.com
   Password: Raaz@2003



## 🚀 Quick Start

### Prerequisites
- Node.js v14+
- MongoDB 4.0+
- npm 6+

### Installation

```bash
# 1. Clone/Extract project
cd carpooling

# 2. Install dependencies
npm install

# 3. Create .env file
cat > .env << EOF
MONGODB_URI=mongodb://localhost:27017/rideshare
JWT_SECRET=your-secret-key-here-change-in-production
NODE_ENV=development
PORT=4000
EOF

# 4. Start MongoDB
mongoos

# 5. Create admin user (optional)
npm run seed:admin

# 6. Start server
npm run dev

# 7. Open browser
http://localhost:4000
```

**Default Admin Credentials:**
- Email: admin@rideshare.com
- Password: Admin123!

---

## 📡 API Endpoints

### Authentication
```
POST   /api/auth/register      - Create new user
POST   /api/auth/login         - Login user
GET    /api/auth/me            - Get current user
```

### Rides
```
GET    /api/rides              - Get all active rides
POST   /api/rides              - Create new ride
GET    /api/rides/search       - Search rides by location/date
GET    /api/rides/my-rides     - Driver's rides
PUT    /api/rides/:id/status   - Update ride status
PUT    /api/rides/:id/cancel   - Cancel ride
DELETE /api/rides/:id          - Delete ride
```

### Bookings
```
POST   /api/bookings           - Book a seat
GET    /api/bookings/my-bookings - Passenger's bookings
PUT    /api/bookings/:id/accept   - Driver accepts booking
PUT    /api/bookings/:id/reject   - Driver rejects booking
PUT    /api/bookings/:id/cancel   - Cancel booking
GET    /api/bookings/waitlist/:rideId - View waitlist
```

### Messages
```
GET    /api/messages/:bookingId    - Get chat messages
POST   /api/messages/:bookingId    - Send message
GET    /api/messages/unread        - Get unread count
```

### Ratings
```
POST   /api/ratings            - Submit rating
GET    /api/ratings/user/:userId - Get user ratings
GET    /api/ratings/check/:bookingId - Check if rated
```

### Reports
```
POST   /api/reports            - Report user
GET    /api/reports/my         - Get my reports
```

### Admin
```
GET    /api/admin/stats        - Dashboard statistics
GET    /api/admin/users        - Manage users
GET    /api/admin/rides        - Manage rides
GET    /api/admin/bookings     - Manage bookings
GET    /api/admin/reports      - View reports
PUT    /api/admin/users/:id/ban     - Ban user
PUT    /api/admin/users/:id/unban   - Unban user
PUT    /api/admin/reports/:id/resolve - Resolve report
```

---

## 🗄️ Database Models

### User
```javascript
{
  _id, email, password (hashed), name, phone,
  userType: 'driver' | 'passenger' | 'admin',
  avatar, bio, trustScore, ratingSum, totalRatings,
  isBanned, banReason, reportCount,
  createdAt, updatedAt
}
```

### Ride
```javascript
{
  _id, driver (User), from, to, date, time, price,
  totalSeats, availableSeats, car, notes,
  status: 'active' | 'started' | 'en-route' | 'completed' | 'cancelled',
  waypoints: [{location, order}],
  recurring: {enabled, type: 'daily'|'weekly', groupId, occurrences},
  waitlist: [{passenger, seats, joinedAt}],
  cancellationReason, createdAt, updatedAt
}
```

### Booking
```javascript
{
  _id, ride (Ride), passenger (User), seats,
  totalPrice, status: 'pending'|'confirmed'|'completed'|'cancelled'|'waitlisted',
  paid: Boolean, paymentMethod, cancellationReason,
  passengerRated, driverRated,
  bookingDate, createdAt, updatedAt
}
```

### Message
```javascript
{
  _id, booking (Booking), ride (Ride),
  sender (User), receiver (User), content,
  readAt, createdAt
}
```

### Rating
```javascript
{
  _id, booking (Booking), ride (Ride),
  rater (User), ratee (User), score: 1-5,
  comment, type: 'passenger-to-driver' | 'driver-to-passenger',
  createdAt
}
```

### Report
```javascript
{
  _id, reporter (User), reported (User), ride (Ride),
  reason, status: 'pending' | 'resolved',
  adminNote, resolvedBy (User), createdAt, updatedAt
}
```

---

## 🔐 Authentication Flow

```
User Input (Email/Password)
    ↓
Validation & Hash Check
    ↓
JWT Token Generated (12-hour expiry)
    ↓
Token stored in localStorage
    ↓
Included in Authorization header for all requests
    ↓
Middleware verifies token on protected routes
```

**Token Format:**
```
Authorization: Bearer <JWT_TOKEN>
```
---

## 🔄 Real-time Features (Socket.io)

### Events Emitted by Server
- `new_booking_request` → Driver gets notification
- `booking_status_changed` → Passenger gets status update
- `ride_status_changed` → All passengers on ride
- `ride_cancelled` → All passengers affected
- `seats_updated` → Real-time seat count
- `waitlist_promoted` → Passenger moves from waitlist
- `new_message` → Chat message received
- `new_notification` → Generic notification

### Client-Server Connection
```javascript
// Auto-connects on page load
const socket = io();

// Join user-specific room
socket.emit('join_user_room', userId);

// Join ride room
socket.emit('join_ride_room', rideId);

// Join booking chat
socket.emit('join_booking_chat', bookingId);
```

---

## 👤 User Workflows

### Driver Workflow
1. Sign up as Driver
2. Offer a ride (set from, to, date, price, seats)
3. Add waypoints if needed
4. Set recurring pattern (daily/weekly)
5. View bookings from passengers
6. Accept/reject bookings
7. Update ride status: Started → En-route → Completed
8. Receive ratings from passengers
9. View earnings and trip history

### Passenger Workflow
1. Sign up as Passenger
2. Search rides by location and date
3. View available rides with filters
4. Book seat(s) or join waitlist
5. Message driver before ride
6. Rate driver after completion
7. View booking history and expenses
8. Track ratings received

### Admin Workflow
1. Access admin dashboard
2. View platform statistics
3. Manage users (ban/unban)
4. Monitor all rides and bookings
5. Moderate user reports
6. Manage resolved reports
7. View revenue analytics

---

## 🎨 UI Features

- **Responsive Design** - Works on desktop, tablet, mobile
- **Dark/Light Theme** - Toggle theme preference
- **Toast Notifications** - Real-time alerts (success, error, info)
- **Loading States** - Visual feedback during operations
- **Form Validation** - Client-side + server-side
- **Empty States** - Helpful messages when no data
- **Error Handling** - Clear error messages for all failures
- **Smooth Animations** - Fade-in, slide effects
- **Mobile Menu** - Hamburger menu on small screens

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Cannot connect to MongoDB"** | Ensure MongoDB is running: `mongod` |
| **"Port 4000 already in use"** | Change PORT in .env or kill process |
| **"Socket not connected"** | Refresh page, restart npm run dev |
| **"Messages not showing real-time"** | Check Socket.io connection in console |
| **"Login fails with valid credentials"** | Check MongoDB has user data, clear cache |
| **"Rides not appearing in search"** | Ensure ride status is 'active', date is future |
| **"Trust score not updating"** | Ensure ride is marked 'completed' before rating |
| **"Buttons not responding"** | Check browser console for JavaScript errors |

---

## 📊 Environment Variables

```bash
# MongoDB
MONGODB_URI=mongodb://localhost:27017/rideshare

# JWT
JWT_SECRET=your-secret-key-min-32-chars

# Server
NODE_ENV=development   # or production
PORT=4000

# Email (optional for future)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

---

## 🚦 Ride Status Flow

```
active (Available for booking)
    ↓
started (Driver started ride)
    ↓
en-route (Driver is on the way)
    ↓
completed (Ride finished, can rate)

OR

cancelled (At any point by driver or admin)
```

**Status Change Rules:**
- Can only progress forward (no going backwards)
- Cannot update cancelled or completed rides
- Bookings auto-complete when ride completes
- Passengers notified of status changes

---

## 🎯 Testing Checklist

- [ ] User registration works
- [ ] User login works
- [ ] Search rides returns results
- [ ] Book seat successfully
- [ ] Receive booking notification
- [ ] Chat message sends/receives
- [ ] Ride status updates
- [ ] Rating submitted
- [ ] Trust score updated
- [ ] Admin can ban users
- [ ] Reports visible in admin panel
- [ ] Mobile responsive

---

## 📝 Notes

- JWT tokens expire after 12 hours
- Passwords are hashed with bcrypt
- All dates in ISO 8601 format
- Prices in USD
- Ride dates must be future dates
- Seats must be between 1-7
- No ride can have more than 7 seats
- Ratings scale: 1 (terrible) to 5 (excellent)
- Trust score is average of all ratings
- Banned users cannot login or use platform

---

## 📞 Support

For issues or questions:
1. Check browser console (F12 → Console)
2. Check server logs (terminal where npm run dev runs)
3. Verify MongoDB connection
4. Check .env file for correct values
5. Review error messages carefully

---

## 📄 License

This project is provided as-is for educational and commercial use.

---

## 🎉 Ready to Use

The project is fully functional and production-ready. Extract, install dependencies, start MongoDB, and run `npm run dev`. All features are working with no errors.

For feature enhancements, refer to ADVANCED_FEATURES_GUIDE.md for 22 additional features to implement.

---


## 📈 Deployment

### Heroku Deployment

```bash
# 1. Create Heroku app
heroku create rideshare-app

# 2. Set environment variables
heroku config:set MONGODB_URI=your-mongodb-uri
heroku config:set JWT_SECRET=your-secret-key
heroku config:set NODE_ENV=production

# 3. Deploy
git push heroku main

# 4. View logs
heroku logs --tail
```

### MongoDB Atlas Setup
1. Create cluster on MongoDB Atlas
2. Get connection string
3. Add to MONGODB_URI in .env
4. Ensure IP whitelist allows your server

### Server Requirements
- Node.js 14+ runtime
- 512MB+ RAM
- MongoDB database
- HTTPS certificate (for production)

**Last Updated:** April 2024  
**Version:** 2.0 (Complete Implementation with Fixes)  
**Status:** Production Ready ✅
#   R i d e S h a r e  
 