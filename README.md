# School Management Dashboard

A comprehensive full-stack school management system built with Next.js, featuring role-based access control for administrators, teachers, students, and parents.

## Overview

This is a modern, feature-rich school management dashboard designed to streamline educational administration. The application provides a centralized platform for managing students, teachers, classes, assignments, exams, attendance, and more. Built with performance and user experience in mind, it offers intuitive interfaces for different user roles with appropriate access controls.

## Features

### 🔐 Authentication & Authorization
- Secure authentication using Clerk
- Role-based access control (Admin, Teacher, Student, Parent)
- Protected routes with middleware-based authorization
- Session management and user metadata handling

### 👥 User Management
- **Admin Dashboard**: Complete oversight of all system entities
- **Teacher Portal**: Manage classes, lessons, assignments, and student records
- **Student Portal**: View assignments, exams, results, attendance, and announcements
- **Parent Portal**: Monitor child's academic progress, attendance, and school events

### 📚 Academic Management
- **Classes & Subjects**: Organize classes by grade levels and assign subjects
- **Lessons**: Schedule and manage daily lessons with time slots
- **Exams & Assignments**: Create, manage, and track academic assessments
- **Results**: Record and view student performance scores
- **Attendance**: Track student attendance for lessons with present/absent status

### 📢 Communication & Events
- **Announcements**: School-wide or class-specific announcements
- **Events**: Calendar-based event management for school activities
- **Real-time Updates**: Dynamic data updates across the dashboard

### 📊 Analytics & Reporting
- **Dashboard Charts**: Visual analytics for attendance, student counts, and finances
- **Performance Metrics**: Track student and class performance over time
- **User Statistics**: Overview cards showing counts for different user types

### 🎨 User Interface
- Responsive design with Tailwind CSS
- Interactive calendar views for events and schedules
- Data tables with pagination and search functionality
- Modal forms for creating and editing records
- Toast notifications for user feedback

## Tech Stack

### Frontend
- **Next.js 14.2.5** - React framework with App Router
- **React 18** - UI library
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **React Hook Form** - Form state management
- **Zod** - Schema validation
- **Recharts** - Data visualization and charts
- **React Big Calendar** - Calendar component for events

### Backend
- **Next.js API Routes** - Server-side API endpoints
- **Prisma ORM** - Database toolkit and ORM
- **PostgreSQL** - Relational database

### Authentication & Services
- **Clerk** - Authentication and user management
- **Next Cloudinary** - Image upload and management

### Development Tools
- **Docker** - Containerization for PostgreSQL database
- **ESLint** - Code linting
- **ts-node** - TypeScript execution for seed scripts

## Getting Started

### Prerequisites

- Node.js 18+ installed
- Docker and Docker Compose (for local database)
- A Clerk account (for authentication)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd full-stack-school
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   DATABASE_URL="postgresql://username:password@localhost:5432/database_name"
   NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_publishable_key
   CLERK_SECRET_KEY=sk_test_your_secret_key
   ```

4. **Start PostgreSQL database**
   
   Using Docker Compose:
   ```bash
   docker-compose up -d postgress
   ```
   
   Or use your own PostgreSQL instance and update the `DATABASE_URL` accordingly.

5. **Set up the database**
   ```bash
   # Generate Prisma Client
   npx prisma generate
   
   # Run migrations (if needed)
   npx prisma migrate deploy
   
   # Seed the database with sample data
   npx prisma db seed
   ```

6. **Run the development server**
   ```bash
   npm run dev
   ```

7. **Open your browser**
   
   Navigate to [http://localhost:3000](http://localhost:3000)

### Production Build

```bash
# Build the application
npm run build

# Start production server
npm start
```

## Environment Variables

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@localhost:5432/dbname` |
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk publishable API key (public) | `pk_test_...` |
| `CLERK_SECRET_KEY` | Clerk secret API key (private) | `sk_test_...` |

### Getting Clerk Keys

1. Sign up or log in to [Clerk Dashboard](https://dashboard.clerk.com)
2. Create a new application or select an existing one
3. Navigate to **API Keys** section
4. Copy your **Publishable Key** and **Secret Key**
5. Add them to your `.env` file

### Setting Up User Roles in Clerk

After creating users in Clerk Dashboard:

1. Go to **Users** → Select a user
2. Navigate to **Metadata** tab
3. Under **Public metadata**, add:
   ```json
   {
     "role": "admin"
   }
   ```
4. Use one of: `"admin"`, `"teacher"`, `"student"`, or `"parent"`

## Project Structure

```
full-stack-school/
├── prisma/
│   ├── schema.prisma          # Database schema definition
│   ├── seed.ts                # Database seeding script
│   └── migrations/            # Database migration files
├── public/                     # Static assets (images, icons)
├── src/
│   ├── app/                   # Next.js App Router pages
│   │   ├── (dashboard)/       # Dashboard routes (protected)
│   │   │   ├── admin/        # Admin dashboard
│   │   │   ├── teacher/      # Teacher dashboard
│   │   │   ├── student/      # Student dashboard
│   │   │   ├── parent/       # Parent dashboard
│   │   │   └── list/         # List pages (students, teachers, etc.)
│   │   └── [[...sign-in]]/   # Authentication pages
│   ├── components/            # React components
│   │   ├── forms/            # Form components
│   │   └── ...               # Other UI components
│   ├── lib/                   # Utility functions and configurations
│   │   ├── actions.ts        # Server actions
│   │   ├── data.ts           # Data fetching functions
│   │   ├── prisma.ts         # Prisma client instance
│   │   └── settings.ts       # Route access configuration
│   └── middleware.ts         # Next.js middleware for route protection
├── docker-compose.yml         # Docker configuration for PostgreSQL
├── Dockerfile                 # Docker configuration for the app
├── next.config.mjs           # Next.js configuration
├── tailwind.config.ts        # Tailwind CSS configuration
└── package.json              # Project dependencies and scripts
```

## Usage

### User Flow

#### For Administrators

1. **Login**: Sign in with admin credentials configured in Clerk
2. **Dashboard**: View overview of all system entities (students, teachers, classes)
3. **Manage Users**: Create, update, and delete teachers, students, and parents
4. **Manage Classes**: Organize classes by grade levels and assign supervisors
5. **Manage Subjects**: Create subjects and assign them to teachers
6. **View Analytics**: Monitor attendance trends, student counts, and financial data

#### For Teachers

1. **Login**: Sign in with teacher credentials
2. **Dashboard**: View assigned classes and students
3. **Manage Lessons**: Create and schedule lessons for assigned classes
4. **Create Assessments**: Add exams and assignments for students
5. **Record Results**: Enter student scores for exams and assignments
6. **Track Attendance**: Mark student attendance for lessons
7. **View Announcements**: Stay updated with school announcements

#### For Students

1. **Login**: Sign in with student credentials
2. **Dashboard**: View personal academic information
3. **View Assignments**: See assigned tasks and due dates
4. **Check Exams**: View upcoming and past exam schedules
5. **View Results**: Check scores for exams and assignments
6. **Attendance**: Monitor personal attendance records
7. **Events & Announcements**: Stay informed about school activities

#### For Parents

1. **Login**: Sign in with parent credentials
2. **Dashboard**: View child's academic overview
3. **Monitor Progress**: Track child's results and performance
4. **Attendance**: Check child's attendance records
5. **School Events**: View upcoming school events and announcements
6. **Academic Calendar**: See exam and assignment schedules

### Key Features Usage

- **Search & Filter**: Use search bars and filters on list pages to find specific records
- **Pagination**: Navigate through large datasets using pagination controls
- **Forms**: Use modal forms to create and edit records with validation
- **Calendar**: View events and schedules in calendar format
- **Charts**: Analyze data through interactive charts and graphs

## Database Schema

The application uses PostgreSQL with the following main entities:

- **Admin, Teacher, Student, Parent** - User roles
- **Grade, Class, Subject** - Academic organization
- **Lesson** - Scheduled classes
- **Exam, Assignment** - Assessments
- **Result** - Student performance records
- **Attendance** - Student attendance tracking
- **Event, Announcement** - Communication and scheduling








