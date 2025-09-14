# Complete Node.js Authentication System

A robust and secure authentication system built with Node.js, TypeScript, Express, Prisma, and PostgreSQL. This project provides user registration, login, and protected route functionality with JWT token-based authentication.

## Features

- User Registration and Login
- JWT Token-based Authentication
- Password Hashing with bcryptjs
- TypeScript Support
- PostgreSQL Database with Prisma ORM
- Protected Routes with Authentication Middleware
- CORS Configuration
- Input Validation and Error Handling

## Tech Stack

- **Runtime**: Node.js
- **Language**: TypeScript
- **Framework**: Express.js
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcryptjs
- **Development**: Nodemon, ts-node-dev

## Prerequisites

Before running this project, make sure you have the following installed:

- Node.js (v16 or higher)
- npm or yarn
- PostgreSQL database

## Installation

1. **Clone the repository**

   ```bash
   git clone <your-repository-url>
   cd completenodejsauthentication
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root directory:

   ```env
   DATABASE_URL="postgresql://username:password@localhost:5432/your_database_name"
   JWT_SECRET="your-super-secret-jwt-key"
   PORT=3000
   HOST=localhost
   ```

4. **Set up the database**

   ```bash
   # Generate Prisma client
   npx prisma generate

   # Run database migrations
   npx prisma db push

   # (Optional) Open Prisma Studio to view your database
   npx prisma studio
   ```

## Usage

### Development Mode

Start the development server with hot reload:

```bash
npm run dev
```

The server will start at `http://localhost:3000`

### API Endpoints

#### Authentication

- **POST** `/api/auth/register` - Register a new user

  ```json
  {
  	"username": "john_doe",
  	"email": "john@example.com",
  	"password": "securepassword123"
  }
  ```

- **POST** `/api/auth/login` - Login user
  ```json
  {
  	"email": "john@example.com",
  	"password": "securepassword123"
  }
  ```

#### Protected Routes

- **GET** `/api/user/:id` - Get user by ID (requires authentication)
  - Header: `x-auth-token: Bearer <your-jwt-token>`

### Example Usage with cURL

1. **Register a new user:**

   ```bash
   curl -X POST http://localhost:3000/api/auth/register \
   -H "Content-Type: application/json" \
   -d '{
     "username": "john_doe",
     "email": "john@example.com",
     "password": "securepassword123"
   }'
   ```

2. **Login:**

   ```bash
   curl -X POST http://localhost:3000/api/auth/login \
   -H "Content-Type: application/json" \
   -d '{
     "email": "john@example.com",
     "password": "securepassword123"
   }'
   ```

3. **Access protected route:**
   ```bash
   curl -X GET http://localhost:3000/api/user/1 \
   -H "x-auth-token: Bearer <your-jwt-token>"
   ```

## Project Structure

```
├── prisma/
│   └── schema.prisma          # Database schema
├── src/
│   ├── controllers/
│   │   └── authController.ts  # Authentication controllers
│   ├── middlewares/
│   │   └── authMiddleware.ts  # Authentication middleware
│   ├── routes/
│   │   └── authRoutes.ts      # API routes
│   ├── services/
│   │   └── authServices.ts    # Business logic
│   ├── utils/
│   │   ├── jwt.ts            # JWT utilities
│   │   └── types.ts          # TypeScript types
│   └── index.ts              # Application entry point
├── .env                      # Environment variables
├── .gitignore               # Git ignore file
├── package.json             # Dependencies and scripts
├── tsconfig.json            # TypeScript configuration
└── README.md                # Project documentation
```

## Database Schema

The project uses a simple User model:

```prisma
model User {
  id        Int      @id @default(autoincrement())
  username  String
  email     String   @unique
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

## Security Features

- **Password Hashing**: Passwords are hashed using bcryptjs with salt rounds
- **JWT Tokens**: Secure token-based authentication with expiration
- **CORS Protection**: Configured CORS for specific origins
- **Input Validation**: Email uniqueness and password validation
- **Error Handling**: Comprehensive error handling throughout the application

## Scripts

- `npm run dev` - Start development server with hot reload
- `npm test` - Run tests (currently not implemented)

## Environment Variables

| Variable       | Description                      | Required |
| -------------- | -------------------------------- | -------- |
| `DATABASE_URL` | PostgreSQL connection string     | Yes      |
| `JWT_SECRET`   | Secret key for JWT signing       | Yes      |
| `PORT`         | Server port (default: 3000)      | No       |
| `HOST`         | Server host (default: localhost) | No       |

## Error Handling

The API returns appropriate HTTP status codes:

- `200` - Success
- `201` - Created
- `400` - Bad Request (validation errors)
- `401` - Unauthorized (invalid/missing token)
- `500` - Internal Server Error

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

**Spicarr Coding**

## Acknowledgments

- Express.js for the web framework
- Prisma for the excellent ORM
- JWT for secure token-based authentication
- bcryptjs for password hashing

---

For any questions or issues, please open an issue in the repository.
