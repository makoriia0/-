# Білет №8 Інтерактивний календар подій (JavaScript)
Практичне завдання
<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Інтерактивний Календар Подій</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .calendar { display: grid; grid-template-columns: repeat(7, 1fr); gap: 5px; }
        .day { border: 1px solid #ccc; padding: 10px; position: relative; }
        .event { background-color: #ffeb3b; padding: 5px; margin-top: 5px; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); }
        .modal-content { background: white; padding: 20px; margin: 100px auto; width: 300px; }
        .close { cursor: pointer; }
        footer { margin-top: 20px; font-size: 0.9em; text-align: center; }
    </style>
</head>
<body>

<h1>Інтерактивний Календар Подій</h1>
<div id="calendar" class="calendar"></div>

<div id="eventModal" class="modal">
    <div class="modal-content">
        <span class="close" onclick="closeModal()">&times;</span>
        <h2>Подія</h2>
        <input type="text" id="eventInput" placeholder="Введіть подію">
        <button onclick="addEvent()">Додати подію</button>
    </div>
</div>

<footer>
    <p>Created by Mariia KOLOS</p>
</footer>

<script>
    const calendarElement = document.getElementById('calendar');
    const eventModal = document.getElementById('eventModal');
    let selectedDate = null;
    const events = {};

    function createCalendar(year, month) {
        calendarElement.innerHTML = '';
        const date = new Date(year, month, 1);
        const daysInMonth = new Date(year, month + 1, 0).getDate();

        for (let i = 1; i <= daysInMonth; i++) {
            const dayDiv = document.createElement('div');
            dayDiv.className = 'day';
            dayDiv.innerText = i;
            dayDiv.onclick = () => openModal(i);

            const eventList = events[`${year}-${month + 1}-${i}`] || [];
            eventList.forEach(event => {
                const eventDiv = document.createElement('div');
                eventDiv.className = 'event';
                eventDiv.innerText = event;
                dayDiv.appendChild(eventDiv);
            });

            calendarElement.appendChild(dayDiv);
        }
    }

    function openModal(day) {
        selectedDate = `2024-11-${day < 10 ? '0' + day : day}`;
        eventModal.style.display = 'block';
    }

    function closeModal() {
        eventModal.style.display = 'none';
        document.getElementById('eventInput').value = '';
    }

    function addEvent() {
        const eventInput = document.getElementById('eventInput');
        const eventText = eventInput.value.trim();
        if (eventText) {
            events[selectedDate] = events[selectedDate] || [];
            events[selectedDate].push(eventText);
            createCalendar(2024, 10); // Місяці в JavaScript починаються з 0
            closeModal();
        }
    }

    // Ініціалізація календаря для листопада 2024 року
    createCalendar(2024, 10);
</script>

</body>
</html>
