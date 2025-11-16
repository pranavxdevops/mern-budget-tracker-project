# BudgetApp - A Smart Expense Tracker

BudgetApp is a modern, full-stack MERN application designed to provide a seamless and intelligent way to manage personal finances. It features real-time budget tracking, an AI-powered insights engine, and proactive alerts to help users stay on top of their spending.


 🔴 Live Demo Links

- **Frontend:** https://mern-budget-tracker-project.vercel.app/
- **Backend:** https://budget-tracker-api-as6k.onrender.com


✨ Key Features

- **JWT Authentication:** Secure user registration and login with token-based authentication.
- **Onboarding Experience:** A guided welcome for new users to help them get started.
- **Dynamic Budgeting:** Users can create custom spending categories with unique colors and set monthly budgets for each.
- **Real-time Expense Tracking:** An intuitive interface to add expenses, with instant visual feedback on budget consumption.
- **Smart Over-Budget Alerts:** Highly specific, user-friendly notifications that pinpoint exactly which category went over budget and by how much.
- **⭐ AI-Powered Smart Insights:** A dedicated page that analyzes historical spending data to provide:
  - **Monthly Trend Analysis:** Compares current spending to the previous month.
  - **Anomaly Detection:** Automatically flags categories with unusually high spending compared to the 3-month average.
  - **Smart Budget Recommendations:** Suggests optimized budgets for the next month based on spending habits.
- **Responsive & Modern Design:** A beautiful, mobile-first interface built with Tailwind CSS that works flawlessly on all devices.
- **Fluid Animations:** Smooth and satisfying animations powered by Framer Motion for an enhanced and professional user experience.


### 🛠️ Tech Stack

**Backend:**
- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JSON Web Token (JWT), Bcrypt.js

**Frontend:**
- **Framework:** React (bootstrapped with Vite)
- **Styling:** Tailwind CSS
- **Animations:** Framer Motion
- **API Communication:** Axios
- **Routing:** React Router
- **UI:** Heroicons, React Hot Toast

**Deployment:**
- **Frontend:** Vercel
- **Backend:** Render
- **Database:** MongoDB Atlas

---

### 🚀 Getting Started

**Prerequisites:**
- Node.js (v18 or higher)
- npm or yarn
- A MongoDB Atlas account (or a local MongoDB instance)

**1. Clone the repository:**
```bash
git clone https://github.com/aswin3032/mern-budget-tracker-project
cd budget-tracker

2. Backend Setup:

code
Bash
cd backend
npm install

# Create a .env file from the example
cp .env.example .env

# Open the .env file and add your MongoDB connection string (MONGO_URI)
# and a secret key for JWT (JWT_SECRET).

node server.js

The backend will be running on http://localhost:5000

3. Frontend Setup:

Open a new terminal window

cd ../frontend
npm install

# Create a .env file from the example
cp .env.example .env

# The VITE_API_URL should point to your running backend. The default is already correct.

npm run dev

The application will be running at http://localhost:5173


📝 API Endpoints


Method	Endpoint	          Description	            Auth Required
POST	/api/auth/register	  Register a new user	            No
POST	/api/auth/login	      Log in a user	                    No
GET	    /api/auth/user	      Get current user's data	        Yes
GET	    /api/categories	      Get all of the user's categories	Yes
POST	/api/categories	      Create a new category	            Yes
DELETE	/api/categories/:id   Delete a category	                Yes
POST	/api/budgets	      Set or update a budget	        Yes
GET	    /api/budgets	      Get budgets for a given month	    Yes
POST	/api/expenses      	  Add a new expense	                Yes
GET	    /api/expenses/month	  Get expenses for a given month	Yes
GET	    /api/reports/monthly  Get the monthly summary report	Yes
GET	    /api/insights	      Get AI-powered spending insights	Yes
PUT	    /api/user/preferences Update user notification settings	Yes