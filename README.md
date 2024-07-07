# javascript-to-do-list


### HTML CODE
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Work To-Dos</h1>
        <form id="taskForm">
            <input type="text" id="title" placeholder="Title" required>
            <input type="text" id="description" placeholder="Description" required>
            <input type="date" id="dueDate" required>
            <button type="submit">Add Task</button>
        </form>
        <ul id="taskList"></ul>
    </div>
    <script src="app.js"></script>
</body>
</html>

~~~
### CSS CODE
~~~
body {
    font-family: Arial, sans-serif;
    background-color: #208dd1;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background: #6c7782;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
    width: 400px;
    max-width: 100%;
}

h1 {
    margin-top: 0;
}

form {
    display: flex;
    flex-direction: column;
}

input, button {
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    background-color: #28a745;
    color: #fff;
    cursor: pointer;
    border: none;
}

button:hover {
    background-color: #218838;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

li.complete {
    text-decoration: line-through;
    color: #888;
}


~~~

### javascript
~~~
class Task {
    constructor(title, description, dueDate) {
        this.title = title;
        this.description = description;
        this.dueDate = dueDate;
        this.completed = false;
    }
}

class ToDoList {
    constructor() {
        this.tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        this.taskList = document.getElementById('taskList');
        this.taskForm = document.getElementById('taskForm');
        this.taskForm.addEventListener('submit', this.addTask.bind(this));
        this.render();
    }

    addTask(event) {
        event.preventDefault();
        const title = document.getElementById('title').value;
        const description = document.getElementById('description').value;
        const dueDate = document.getElementById('dueDate').value;
        const newTask = new Task(title, description, dueDate);
        this.tasks.push(newTask);
        this.saveTasks();
        this.render();
        this.taskForm.reset();
    }

    editTask(index) {
        const title = prompt('Enter new title:', this.tasks[index].title);
        const description = prompt('Enter new description:', this.tasks[index].description);
        const dueDate = prompt('Enter new due date:', this.tasks[index].dueDate);
        if (title && description && dueDate) {
            this.tasks[index].title = title;
            this.tasks[index].description = description;
            this.tasks[index].dueDate = dueDate;
            this.saveTasks();
            this.render();
        }
    }

    deleteTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
        this.render();
    }

    toggleComplete(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
        this.saveTasks();
        this.render();
    }

    saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }

    render() {
        this.taskList.innerHTML = '';
        this.tasks.forEach((task, index) => {
            const taskItem = document.createElement('li');
            taskItem.className = task.completed ? 'complete' : '';
            taskItem.innerHTML = `
                <span>${task.title} - ${task.description} (Due: ${task.dueDate})</span>
                <div>
                    <button onclick="toDoList.toggleComplete(${index})">${task.completed ? 'Incomplete' : 'Complete'}</button>
                    <button onclick="toDoList.editTask(${index})">Edit</button>
                    <button onclick="toDoList.deleteTask(${index})">Delete</button>
                </div>
            `;
            this.taskList.appendChild(taskItem);
        });
    }
}

const toDoList = new ToDoList();

### OUTPUT

![image](https://github.com/Ragupathi1/javascript-to-do-list/assets/143526042/11da9928-1b88-4262-8b81-a67ae0b25799)

![image](https://github.com/Ragupathi1/javascript-to-do-list/assets/143526042/d601d0f4-2f41-45eb-9a27-91f441fa3a92)



### RESULT:
Thus the program has been completed successfully.
