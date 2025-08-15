import { useState, useEffect } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, signInWithCustomToken, onAuthStateChanged, signInAnonymously } from 'firebase/auth';
import { getFirestore, collection, doc, onSnapshot, setDoc, updateDoc, deleteDoc } from 'firebase/firestore';

// Main App component
const App = () => {
  const [db, setDb] = useState(null);
  const [auth, setAuth] = useState(null);
  const [userId, setUserId] = useState(null);
  const [isAuthReady, setIsAuthReady] = useState(false);
  const [currentDate, setCurrentDate] = useState(new Date());
  const [events, setEvents] = useState([]);
  const [newEvent, setNewEvent] = useState({ title: '', date: '' });
  const [message, setMessage] = useState('');

  // 1. Firebase Initialization & Authentication
  useEffect(() => {
    // Check for the required global variables
    const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
    const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
    const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

    if (Object.keys(firebaseConfig).length > 0) {
      const app = initializeApp(firebaseConfig);
      const firestoreDb = getFirestore(app);
      const firebaseAuth = getAuth(app);

      setDb(firestoreDb);
      setAuth(firebaseAuth);

      const unsubscribe = onAuthStateChanged(firebaseAuth, async (user) => {
        if (user) {
          setUserId(user.uid);
        } else {
          // Sign in anonymously if no user is found
          try {
            await signInAnonymously(firebaseAuth);
          } catch (error) {
            console.error('Error signing in anonymously:', error);
          }
        }
        setIsAuthReady(true);
      });

      // Sign in with the custom token if provided
      if (initialAuthToken) {
        signInWithCustomToken(firebaseAuth, initialAuthToken).catch(error => {
          console.error("Error signing in with custom token:", error);
        });
      }

      return () => unsubscribe();
    } else {
      console.error("Firebase configuration is missing.");
    }
  }, []);

  // 2. Fetch events from Firestore
  useEffect(() => {
    if (db && userId) {
      const q = collection(db, `artifacts/${__app_id}/users/${userId}/events`);
      const unsubscribe = onSnapshot(q, (querySnapshot) => {
        const fetchedEvents = [];
        querySnapshot.forEach((doc) => {
          fetchedEvents.push({ ...doc.data(), id: doc.id });
        });
        setEvents(fetchedEvents);
      }, (error) => {
        console.error("Error fetching events:", error);
      });

      return () => unsubscribe();
    }
  }, [db, userId, isAuthReady]);

  // Handle input changes for new event form
  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setNewEvent(prev => ({ ...prev, [name]: value }));
  };

  // 3. Save a new event to Firestore
  const handleAddEvent = async (e) => {
    e.preventDefault();
    if (!newEvent.title || !newEvent.date) {
      setMessage("Please fill in both title and date.");
      return;
    }
    if (!db || !userId) {
      setMessage("Firebase not ready. Please wait.");
      return;
    }

    try {
      const newEventRef = doc(collection(db, `artifacts/${__app_id}/users/${userId}/events`));
      await setDoc(newEventRef, {
        title: newEvent.title,
        date: newEvent.date,
        createdAt: new Date().toISOString()
      });
      setMessage("Event added successfully!");
      setNewEvent({ title: '', date: '' });
    } catch (error) {
      console.error("Error adding event:", error);
      setMessage("Failed to add event. Check the console for details.");
    }
  };

  // 4. Delete an event from Firestore
  const handleDeleteEvent = async (id) => {
    if (!db || !userId) {
      setMessage("Firebase not ready.");
      return;
    }

    try {
      await deleteDoc(doc(db, `artifacts/${__app_id}/users/${userId}/events`, id));
      setMessage("Event deleted successfully!");
    } catch (error) {
      console.error("Error deleting event:", error);
      setMessage("Failed to delete event. Check the console for details.");
    }
  };

  // Calendar logic
  const daysOfWeek = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
  const today = new Date();
  const startOfMonth = new Date(currentDate.getFullYear(), currentDate.getMonth(), 1);
  const endOfMonth = new Date(currentDate.getFullYear(), currentDate.getMonth() + 1, 0);
  const numDays = endOfMonth.getDate();
  const startDay = startOfMonth.getDay();
  const daysInMonth = Array.from({ length: numDays }, (_, i) => i + 1);

  const prevMonth = () => {
    setCurrentDate(new Date(currentDate.getFullYear(), currentDate.getMonth() - 1, 1));
  };
  const nextMonth = () => {
    setCurrentDate(new Date(currentDate.getFullYear(), currentDate.getMonth() + 1, 1));
  };

  const getEventsForDay = (day) => {
    const dateString = `${currentDate.getFullYear()}-${String(currentDate.getMonth() + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
    return events.filter(event => event.date === dateString);
  };

  // Tailwind CSS styling
  const containerStyle = "p-8 w-full max-w-4xl mx-auto font-sans";
  const cardStyle = "bg-white shadow-xl rounded-2xl p-6 mb-8 text-gray-800";
  const headerStyle = "flex justify-between items-center mb-6";
  const buttonStyle = "p-2 rounded-full bg-gray-200 text-gray-700 hover:bg-gray-300 transition-colors";
  const calendarGridStyle = "grid grid-cols-7 gap-2 text-center";
  const dayHeaderStyle = "font-bold text-gray-500";
  const dayBoxStyle = "h-24 p-2 border border-gray-200 rounded-lg flex flex-col items-center justify-start relative overflow-hidden";
  const todayStyle = "border-2 border-blue-500";
  const eventStyle = "text-xs bg-blue-500 text-white rounded-md px-1 py-0.5 mt-1 truncate w-full";
  const formStyle = "flex flex-col gap-4";
  const inputStyle = "p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500";
  const submitButtonStyle = "p-2 rounded-lg bg-blue-600 text-white font-bold hover:bg-blue-700 transition-colors";
  const messageStyle = "mt-4 text-center";
  const deleteButtonStyle = "absolute top-1 right-1 text-red-500 text-sm hover:text-red-700 transition-colors";

  return (
    <div className={containerStyle}>
      <div className={cardStyle}>
        <div className={headerStyle}>
          <button className={buttonStyle} onClick={prevMonth}>&lt;</button>
          <h2 className="text-2xl font-bold">
            {currentDate.toLocaleString('default', { month: 'long', year: 'numeric' })}
          </h2>
          <button className={buttonStyle} onClick={nextMonth}>&gt;</button>
        </div>
        <div className={calendarGridStyle}>
          {daysOfWeek.map(day => (
            <div key={day} className={dayHeaderStyle}>{day}</div>
          ))}
          {Array.from({ length: startDay }).map((_, i) => (
            <div key={`empty-${i}`} className="h-24"></div>
          ))}
          {daysInMonth.map(day => {
            const isToday = day === today.getDate() && currentDate.getMonth() === today.getMonth() && currentDate.getFullYear() === today.getFullYear();
            const dayEvents = getEventsForDay(day);
            return (
              <div key={day} className={`${dayBoxStyle} ${isToday ? todayStyle : ''}`}>
                <div className="font-semibold text-sm">{day}</div>
                {dayEvents.map(event => (
                  <div key={event.id} className={eventStyle}>
                    {event.title}
                    <button
                      className={deleteButtonStyle}
                      onClick={() => handleDeleteEvent(event.id)}
                      title="Delete event"
                    >
                      &times;
                    </button>
                  </div>
                ))}
              </div>
            );
          })}
        </div>
      </div>
      <div className={cardStyle}>
        <h3 className="text-xl font-semibold mb-4">Add New Event</h3>
        <form onSubmit={handleAddEvent} className={formStyle}>
          <input
            type="text"
            name="title"
            placeholder="Event Title"
            value={newEvent.title}
            onChange={handleInputChange}
            className={inputStyle}
          />
          <input
            type="date"
            name="date"
            value={newEvent.date}
            onChange={handleInputChange}
            className={inputStyle}
          />
          <button type="submit" className={submitButtonStyle}>Add Event</button>
        </form>
        {message && <div className={messageStyle}>{message}</div>}
      </div>
      {userId && (
        <div className="mt-4 text-center text-gray-500 text-sm">
          User ID: <span className="font-mono">{userId}</span>
        </div>
      )}
    </div>
  );
};

export default App;
