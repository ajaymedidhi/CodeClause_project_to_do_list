# CodeClause_project_to_do_list
In this code, i created a dynamic to-do-list using html,css and javascript


<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous" />
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
    <script src="https://kit.fontawesome.com/5f59ca6ad3.js" crossorigin="anonymous"></script>
</head>

<body>
    <div class="todos-bg-container">
        <div class="container">
            <div class="row">
                <div class="col-12">
                    <h1 class="todos-heading">Todos</h1>
                    <h1 class="create-task-heading">
                        Create <span class="create-task-heading-subpart">Task</span>
                    </h1>
                    <input type="text" id="todoUserInput" class="todo-user-input" placeholder="What needs to be done?" />
                    <button class="button" id="addTodoButton">Add</button>
                    <h1 class="todo-items-heading">
                        My <span class="todo-items-heading-subpart">Tasks</span>
                    </h1>
                    <ul class="todo-items-container" id="todoItemsContainer"></ul>
                    <button class="button" id="saveTodoButton">Save</button>
                </div>
            </div>
        </div>
    </div>
</body>

</html>

#CSS CODE
@import url('https://fonts.googleapis.com/css2?family=Bree+Serif&family=Caveat:wght@400;700&family=Lobster&family=Monoton&family=Open+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Playfair+Display+SC:ital,wght@0,400;0,700;1,700&family=Playfair+Display:ital,wght@0,400;0,700;1,700&family=Roboto:ital,wght@0,400;0,700;1,400;1,700&family=Source+Sans+Pro:ital,wght@0,400;0,700;1,700&family=Work+Sans:ital,wght@0,400;0,700;1,700&display=swap');

.todos-bg-container {
    background-color: #f9fbfe;
    height: 100vh;
}

.todos-heading {
    text-align: center;
    font-family: "Roboto";
    font-size: 46px;
    font-weight: 500;
    margin-top: 20px;
    margin-bottom: 20px;
}

.create-task-heading {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 700;
}

.create-task-heading-subpart {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 500;
}

.todo-items-heading {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 700;
}

.todo-items-heading-subpart {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 500;
}

.todo-items-container {
    margin: 0px;
    padding: 0px;
}

.todo-item-container {
    margin-top: 15px;
}

.todo-user-input {
    background-color: white;
    width: 100%;
    border-style: solid;
    border-width: 1px;
    border-color: #e4e7eb;
    border-radius: 10px;
    margin-top: 10px;
    padding: 15px;
}

.button {
    color: white;
    background-color: #4c63b6;
    font-family: "Roboto";
    font-size: 18px;
    border-width: 0px;
    border-radius: 4px;
    margin-top: 20px;
    margin-bottom: 50px;
    padding-top: 5px;
    padding-bottom: 5px;
    padding-right: 20px;
    padding-left: 20px;
}

.label-container {
    background-color: #e6f6ff;
    width: 100%;
    border-style: solid;
    border-width: 5px;
    border-color: #096f92;
    border-right: none;
    border-top: none;
    border-bottom: none;
    border-radius: 4px;
}

.checkbox-input {
    width: 20px;
    height: 20px;
    margin-top: 12px;
    margin-right: 12px;
}

.checkbox-label {
    font-family: "Roboto";
    font-size: 16px;
    font-weight: 400;
    width: 82%;
    margin: 0px;
    padding-top: 10px;
    padding-bottom: 10px;
    padding-left: 20px;
    padding-right: 20px;
    border-radius: 5px;
}

.delete-icon-container {
    text-align: right;
    width: 18%;
}

.delete-icon {
    padding: 15px;
}

.checked {
    text-decoration: line-through;
}

#Javascript Code 
let addTodoButton = document.getElementById("addTodoButton");
let saveTodoButton = document.getElementById("saveTodoButton");

function getTodoListFromLocalStorage() {
    let stringifiedTodoList = localStorage.getItem("todoList");
    let parsedTodoList = JSON.parse(stringifiedTodoList);
    if (parsedTodoList === null) {
        return [];
    } else {
        return parsedTodoList;
    }
}

let todoList = getTodoListFromLocalStorage();
let todosCount = todoList.length;

saveTodoButton.onclick = function() {
    localStorage.setItem("todoList", JSON.stringify(todoList));
};

function onAddTodo() {
    let userInputElement = document.getElementById("todoUserInput");
    let userInputValue = userInputElement.value;

    if (userInputValue === "") {
        alert("Enter Valid Text");
        return;
    }

    todosCount = todosCount + 1;

    let newTodo = {
        text: userInputValue,
        uniqueNo: todosCount,
        isChecked: false
    };
    todoList.push(newTodo);
    createAndAppendTodo(newTodo);
    userInputElement.value = "";
}

addTodoButton.onclick = function() {
    onAddTodo();
};

function onTodoStatusChange(checkboxId, labelId, todoId) {
    let checkboxElement = document.getElementById(checkboxId);
    let labelElement = document.getElementById(labelId);
    labelElement.classList.toggle("checked");

    let todoObjectIndex = todoList.findIndex(function(eachTodo) {
        let eachTodoId = "todo" + eachTodo.uniqueNo;

        if (eachTodoId === todoId) {
            return true;
        } else {
            return false;
        }
    });

    let todoObject = todoList[todoObjectIndex];

    if (todoObject.isChecked === true) {
        todoObject.isChecked = false;
    } else {
        todoObject.isChecked = true;
    }

}

function onDeleteTodo(todoId) {
    let todoElement = document.getElementById(todoId);
    todoItemsContainer.removeChild(todoElement);

    let deleteElementIndex = todoList.findIndex(function(eachTodo) {
        let eachTodoId = "todo" + eachTodo.uniqueNo;
        if (eachTodoId === todoId) {
            return true;
        } else {
            return false;
        }
    });

    todoList.splice(deleteElementIndex, 1);
}

function createAndAppendTodo(todo) {
    let todoId = "todo" + todo.uniqueNo;
    let checkboxId = "checkbox" + todo.uniqueNo;
    let labelId = "label" + todo.uniqueNo;

    let todoElement = document.createElement("li");
    todoElement.classList.add("todo-item-container", "d-flex", "flex-row");
    todoElement.id = todoId;
    todoItemsContainer.appendChild(todoElement);

    let inputElement = document.createElement("input");
    inputElement.type = "checkbox";
    inputElement.id = checkboxId;
    inputElement.checked = todo.isChecked;

    inputElement.onclick = function() {
        onTodoStatusChange(checkboxId, labelId, todoId);
    };

    inputElement.classList.add("checkbox-input");
    todoElement.appendChild(inputElement);

    let labelContainer = document.createElement("div");
    labelContainer.classList.add("label-container", "d-flex", "flex-row");
    todoElement.appendChild(labelContainer);

    let labelElement = document.createElement("label");
    labelElement.setAttribute("for", checkboxId);
    labelElement.id = labelId;
    labelElement.classList.add("checkbox-label");
    labelElement.textContent = todo.text;
    if (todo.isChecked === true) {
        labelElement.classList.add("checked");
    }
    labelContainer.appendChild(labelElement);

    let deleteIconContainer = document.createElement("div");
    deleteIconContainer.classList.add("delete-icon-container");
    labelContainer.appendChild(deleteIconContainer);

    let deleteIcon = document.createElement("i");
    deleteIcon.classList.add("far", "fa-trash-alt", "delete-icon");

    deleteIcon.onclick = function() {
        onDeleteTodo(todoId);
    };

    deleteIconContainer.appendChild(deleteIcon);
}

for (let todo of todoList) {
    createAndAppendTodo(todo);
}
