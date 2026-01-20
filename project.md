### **🛠 Project Initialization (Days 1–2)**

#### **1. Database Setup**
- [ ] **Install PostgreSQL:** Ensure Postgres is running locally.
- [ ] **Create Database:** Create a new database named `todo_app`.
- [ ] **Manual Table Creation:** Run the provided `CREATE TABLE` query in your SQL editor (e.g., pgAdmin or `psql`).
- [ ] **Test Connectivity:** Use a simple script or tool to verify you can connect to the DB.

#### **2. Backend Setup (NestJS)**
- [ ] **Project Init:** Run `nest new backend` (choose npm).
- [ ] **Install Dependencies:** `npm install pg zod` and `npm install -D @types/pg`.
- [ ] **Env Config:** Create a `.env` file with `DATABASE_URL`, `DB_PORT`, `DB_USER`, etc.
- [ ] **Database Module:** Create a `DatabaseModule` that provides a `PG_CONNECTION` (a `pg.Pool` instance).

#### **3. Frontend Setup (React + Vite)**
- [ ] **Project Init:** Run `npm create vite@latest frontend -- --template react-ts`.
- [ ] **Tailwind Setup:** Install Tailwind CSS and its dependencies. Configure `tailwind.config.js`.
- [ ] **Radix UI Setup:** Install `@radix-ui/react-checkbox` and `@radix-ui/react-dialog`.

---

### **📡 Backend API Development (Days 3–5)**

#### **1. Data Validation (Zod)**
- [ ] **Define Schema:** Create a `todo.schema.ts` using Zod for creating and updating tasks.
- [ ] **Validation Pipe:** Create a custom `ZodValidationPipe` to validate incoming `@Body()` data in your controllers.

#### **2. Todo Service (Raw SQL)**
- [ ] **Documentation:** Use **TSDoc** to document every method.
- [ ] **`findAll()`:** Write `SELECT * FROM todos ORDER BY created_at DESC`.
- [ ] **`create()`:** Write `INSERT INTO todos (title, description) VALUES ($1, $2) RETURNING *`.
- [ ] **`update()`:** Write `UPDATE todos SET is_completed = $1 WHERE id = $2`.
- [ ] **`delete()`:** Write `DELETE FROM todos WHERE id = $1`.

#### **3. Controller**
- [ ] **REST Endpoints:** Implement `GET /todos`, `POST /todos`, `PATCH /todos/:id`, and `DELETE /todos/:id`.

---

### **🎨 Frontend UI Development (Days 6–9)**

#### **1. Components & Layout**
- [ ] **Task List Component:** Build a container to display the list of todos.
- [ ] **Todo Item:** Create a row component for a single task using Tailwind for styling.
- [ ] **Input Form:** Build the "Add Task" form at the top of the page.

#### **2. Radix UI Integration**
- [ ] **Checkbox:** Replace standard HTML checkboxes with **Radix Checkbox** for the "Done" state.
- [ ] **Edit Modal:** Implement **Radix Dialog** so that when a user clicks "Edit," a modal pops up with the current task details.

#### **3. State & Logic**
- [ ] **Fetching Data:** Use `useEffect` to fetch todos from your NestJS API.
- [ ] **Mutations:** Implement functions to handle adding, toggling, and deleting tasks (updating the UI immediately after the API call).

---

### **🏁 Final Polish (Day 10)**

- [ ] **Error Handling:** Ensure the frontend shows an error message if the API fails (e.g., if Zod validation rejects a short title).
- [ ] **TS Conventions:** Double-check that all variables are `camelCase`, types are `PascalCase`, and there are **zero** `any` types.
- [ ] **README Update:** Add a "Phase 1" section to your `README.md` with:
    - How to setup the database.
    - How to run the backend (`npm run start:dev`).
    - How to run the frontend (`npm run dev`).

---

### **💡 Pro-Tip for Phase One**
When writing your **Raw SQL** in NestJS, always use **parameterized queries** to prevent SQL injection:
```typescript
/**
 * ✅ Correct Way (Safe)
 */
const query = 'INSERT INTO todos (title) VALUES ($1) RETURNING *';
const values = [todoDto.title];
await this.db.query(query, values);

/**
 * ❌ Wrong Way (Unsafe)
 */
const query = `INSERT INTO todos (title) VALUES ('${todoDto.title}')`;
await this.db.query(query);
```
