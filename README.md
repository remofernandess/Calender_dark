# Calender_dark
import { useState } from "react";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import Dashboard from "./components/Dashboard";
import Profile from "./components/Profile";
import Login from "./components/Login";
import CalendarView from "./components/CalendarView";
import { ThemeProvider } from "./components/ThemeProvider";
import { AnimatePresence } from "framer-motion";

function App() {
  const [user, setUser] = useState(null);
  const [darkMode, setDarkMode] = useState(false);

  return (
    <ThemeProvider darkMode={darkMode} setDarkMode={setDarkMode}>
      <Router>
        <div className={`min-h-screen ${darkMode ? 'bg-gray-900 text-white' : 'bg-gray-100'} flex items-center justify-center p-4`}>
          <AnimatePresence mode="wait">
            <Routes>
              <Route path="/" element={<Login setUser={setUser} />} />
              <Route path="/dashboard" element={user ? <Dashboard user={user} /> : <Login setUser={setUser} />} />
              <Route path="/profile" element={user ? <Profile user={user} /> : <Login setUser={setUser} />} />
              <Route path="/calendar" element={user ? <CalendarView user={user} darkMode={darkMode} /> : <Login setUser={setUser} />} />
            </Routes>
          </AnimatePresence>
        </div>
      </Router>
    </ThemeProvider>
  );
}

export default App;
