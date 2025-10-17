# Sem-in-skill-exam
KL University’s online store wants a feature where students can click on a product and view detailed information in a pop-up without leaving the page.  Display a list of products (name, price, short description). When a user clicks a product, open a pop-up showing full details, including an image and extended description.

const eventsData = [
  { date: '2025-10-15', title: 'Meeting', description: 'Project meeting at 10 AM' },
  { date: '2025-10-17', title: 'Birthday Party', description: 'Celebrate Nikhil\'s birthday' },
  { date: '2025-10-20', title: 'Conference', description: 'Tech conference in the city' },
];

const Calendar = () => {
  const [selectedDate, setSelectedDate] = useState(null);
  const [events, setEvents] = useState([]);

  const currentDate = new Date();
  const month = currentDate.getMonth();
  const year = currentDate.getFullYear();

  const getDaysInMonth = (month, year) => new Date(year, month + 1, 0).getDate();

  const handleDateClick = (date) => {
    const formattedDate = ${year}-${String(month + 1).padStart(2, '0')}-${String(date).padStart(2, '0')};
    setSelectedDate(formattedDate);
    const filteredEvents = eventsData.filter(event => event.date === formattedDate);
    setEvents(filteredEvents);
  };

  const daysInMonth = getDaysInMonth(month, year);
  const days = Array.from({ length: daysInMonth }, (_, i) => i + 1);

  return (
    <div>
      <h1>Calendar for {currentDate.toLocaleString('default', { month: 'long' })} {year}</h1>
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(7, 1fr)', gap: '10px' }}>
        {days.map(day => (
          <div
            key={day}
            onClick={() => handleDateClick(day)}
            style={{
              padding: '20px',
              border: '1px solid #ccc',
              cursor: 'pointer',
              backgroundColor: selectedDate === ${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')} ? '#add8e6' : '#fff'
            }}
          >
            {day}
          </div>
        ))}
      </div>
      {selectedDate && (
        <div>
          <h2>Events on {selectedDate}:</h2>
          {events.length > 0 ? (
            events.map((event, index) => (
              <div key={index}>
                <h3>{event.title}</h3>
                <p>{event.description}</p>
              </div>
            ))
          ) : (
            <p>No events for this date.</p>
          )}
        </div>
      )}
    </div>
  );
};
