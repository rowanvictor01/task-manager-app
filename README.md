# 📝 Task Manager App (Vue.js)

A simple and modular task manager app built using **Vue 3** and the **Composition API**. Users can add, view, and delete tasks — with support for future features like task filtering, editing, and completion toggles.

---

## 🚀 Features

- Add new tasks with a name and description
- Display a list of tasks
- Delete tasks individually
- Clean separation of components
- Uses `props` and `emits` for parent-child communication
- Unique task IDs for stable filtering and deletion

---

## 📁 Folder Structure

src/  
├── components/  
│ ├── Header.vue  
│ ├── TaskList.vue  
│ └── TaskItem.vue  
├── App.vue  
└── main.js  

---

## 🧩 Components Breakdown

| Component      | Role |
|----------------|------|
| **App.vue**    | Main logic and state. Holds task data and handles add/delete. |
| **TaskList.vue** | Renders the list of tasks and passes each to `TaskItem`. |
| **TaskItem.vue** | Displays a single task and emits actions like delete. |
| **Header.vue** | (Optional) A simple header or title bar. |

---

## 🧠 Tech Stack

- [Vue.js 3 Composition API](https://vuejs.org/)
- JavaScript
- HTML
- CSS

---

## 📦 Project Setup

```bash
npm install
npm run dev
```

## 📌 Future Enhancements

- [ ] Mark tasks as complete/incomplete
- [ ] Set tasks as priority
- [ ] Edit existing tasks
- [ ] Filter tasks by status (All, Completed, Priority)
- [ ] Persist data with localStorage or a backend

## 📸 Screenshots

_work in progress_

## 🧑‍💻 Author

Made with ❤️ by [rowanvictor01](https://github.com/rowanvictor01)  
If you found this helpful or interesting, feel free to ⭐ the repo!

---

