# UKOM Exam Preparation Platform

Professional exam preparation platform for UKOM (Uji Kompetensi) certification with interactive tryouts, full simulation exams, and admin question management.

## 🚀 Quick Start

### Online (Replit)
The application is deployed on Replit. Visit the live URL to access it directly.

### Local Setup
To run this application on your computer:

```bash
# 1. Install dependencies
npm install

# 2. Setup PostgreSQL database and environment variables
# See SETUP_LOCAL.md for detailed instructions

# 3. Sync database schema
npm run db:push

# 4. Start development server
npm run dev
```

Then open: **http://localhost:5000**

**For detailed setup instructions, see [SETUP_LOCAL.md](./SETUP_LOCAL.md)**

---

## 📚 Features

### Student Features
- ✅ **Tryout Mode**: Practice per subject with 100 questions per section, 100-minute timer
- ✅ **Simulasi Mode**: Full UKOM simulation with 180 questions, 180-minute timer
- ✅ **Question Bookmarking**: Mark questions to review later
- ✅ **Answer Tracking**: Auto-save answers as you work
- ✅ **Results Analysis**: See scores, percentages, and performance breakdown
- ✅ **Responsive Design**: Works on desktop, tablet, and mobile

### Admin Features
- 🔑 **Secure Login**: Email/password authentication (admin@local / admin123!)
- 📝 **Question Management**: Add, edit, delete exam questions
- 🏷️ **Organization**: Filter by subject and section
- 🔍 **Search**: Find questions quickly
- 📊 **Bank Management**: Full control over exam question bank

---

## 🛠️ Technology Stack

### Frontend
- React 18 + TypeScript
- Vite (fast build tool)
- Shadcn/ui + Tailwind CSS
- React Hook Form + Zod validation
- TanStack Query (React Query)
- Wouter (lightweight routing)

### Backend
- Express.js + TypeScript
- PostgreSQL + Drizzle ORM
- Passport.js for authentication
- Express Session management

### Development Tools
- Vite HMR (hot module replacement)
- TypeScript strict mode
- ESLint + Prettier ready
- Drizzle Kit for migrations

---

## 📋 System Requirements

### For Local Development
- Node.js 18+ ([download](https://nodejs.org/))
- PostgreSQL 12+ ([download](https://www.postgresql.org/))
- npm or yarn package manager

### Optional
- Git for version control
- VS Code or your preferred editor

---

## 🎯 How to Use

### As a Student
1. Open homepage
2. Choose **Tryout** or **Simulasi**
3. Select subject and section (Tryout) or start directly (Simulasi)
4. Answer questions within time limit
5. Use bookmark feature for difficult questions
6. Submit exam to see results

### As an Admin
1. Click **Login Admin** on homepage
2. Use your admin credentials (contact administrator for access)
3. Manage questions:
   - **View**: See all questions filtered by subject/section
   - **Add**: Create new questions with image support
   - **Edit**: Update existing questions
   - **Delete**: Remove questions from bank

---

## 📂 Project Structure

```
ukom-prep/
├── client/                    # React Frontend
│   ├── src/
│   │   ├── pages/            # Page components (exam, results, admin, etc)
│   │   ├── components/       # Reusable UI components
│   │   ├── hooks/            # Custom React hooks
│   │   ├── lib/              # Utilities & helpers
│   │   └── main.tsx          # Entry point
│   └── index.html
├── server/                    # Express Backend
│   ├── routes.ts             # API endpoints
│   ├── storage.ts            # Database operations
│   ├── db.ts                 # Database connection
│   ├── replitAuth.ts         # Authentication setup
│   └── app.ts                # Express app setup
├── shared/                    # Shared Code
│   └── schema.ts             # Data models & Zod schemas
├── SETUP_LOCAL.md            # Local development guide
├── .env.example              # Example environment variables
├── package.json              # Dependencies
├── vite.config.ts            # Vite configuration
├── tsconfig.json             # TypeScript configuration
└── drizzle.config.ts         # Drizzle ORM configuration
```

---

## 🗄️ Database Schema

### Key Tables
- **users**: User accounts (from auth system)
- **questions**: Exam questions with options and answers
- **exam_sessions**: Exam attempts and scores
- **exam_answers**: Individual answers per question
- **sessions**: Session storage for authentication

---

## 🔒 Security Features

- Session-based authentication
- Password protection for admin panel
- Input validation with Zod schemas
- SQL injection prevention via ORM
- Environment variables for secrets
- HTTPS ready for production

---

## 📖 Available Commands

```bash
# Development
npm run dev              # Start dev server with hot reload

# Database
npm run db:push        # Sync schema to database
npm run db:studio      # Open visual database manager

# Building
npm run build          # Build for production
npm run preview        # Preview production build

# Code Quality
npm run type-check     # Check TypeScript errors
npm run lint           # Run linter (if configured)
```

---

## 🐛 Troubleshooting

### "Cannot connect to database"
- Verify PostgreSQL is running
- Check DATABASE_URL in .env.local
- Ensure database exists: `psql -U postgres -c "CREATE DATABASE ukom_prep;"`

### "Port 5000 is already in use"
- Kill process: `lsof -i :5000 | grep LISTEN | awk '{print $2}' | xargs kill -9`
- Or use different port (modify vite.config.ts)

### "Module not found" errors
- Run `npm install` again
- Delete node_modules and reinstall: `rm -rf node_modules package-lock.json && npm install`

### Database schema issues
- Force sync: `npm run db:push --force`
- Check migrations were applied correctly

See [SETUP_LOCAL.md](./SETUP_LOCAL.md) for more detailed troubleshooting.

---

## 🚀 Deployment

To deploy to production:

1. **Prepare**:
   ```bash
   npm run build
   npm run type-check
   ```

2. **Choose platform**:
   - Replit (native support)
   - Heroku, Railway, Vercel, etc.

3. **Configure**:
   - Set environment variables on platform
   - Provision PostgreSQL database
   - Set SESSION_SECRET

4. **Deploy**:
   - Follow platform-specific instructions
   - Run migrations: `npm run db:push`
   - Start server: `npm run dev` or equivalent

---

## 📞 Support

### Common Issues
- Check browser console (F12) for errors
- Check terminal logs for backend issues
- Verify all environment variables are set
- Ensure database connection is working

### Resources
- [SETUP_LOCAL.md](./SETUP_LOCAL.md) - Complete local setup guide
- [.env.example](./.env.example) - Environment variable template
- TypeScript documentation
- Express.js documentation
- PostgreSQL documentation

---

## 📝 License

This project is created for educational purposes.

---

## ✨ Features Coming Soon

- [ ] Simulasi mode with distributed questions across all subjects
- [ ] Advanced analytics and performance tracking
- [ ] Question explanation system
- [ ] Multiple user authentication
- [ ] Progress history and statistics
- [ ] Mobile app version

---

**Happy Learning! 📚**

For questions or issues, refer to the setup guide and troubleshooting section above.
