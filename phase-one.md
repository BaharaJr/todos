## Phase 1 Detailed Project Description

### **Overview**
The goal of this project is to build a high-performance, persistent Todo application. Unlike a simple "in-memory" beginner project, this will require you to set up a real PostgreSQL database and communicate with it using manual SQL queries. This ensures you understand how data is stored, retrieved, and validated before you start using automated tools.

### **Core Features to Implement**
1.  **Create Tasks:** A user should be able to type a task name and a description into a form.
2.  **View Tasks:** A list that displays all tasks currently stored in the database.
3.  **Toggle Status:** A checkbox to mark a task as "Complete" or "Pending."
4.  **Delete Tasks:** A button to permanently remove a task from the database.
5.  **Edit Tasks:** A button that opens a **Radix UI Dialog** to change the text of an existing task.

### **Technical Implementation Details**

#### **1. Database (The Manual Way)**
Instead of letting a library create tables for you, you will do it yourself.
*   **Action:** Install PostgreSQL and use a tool like `psql` or `pgAdmin`.
*   **SQL Task:** Run the following command to initialize your project:
    ```sql
    CREATE TABLE todos (
        id SERIAL PRIMARY KEY,
        title VARCHAR(255) NOT NULL,
        description TEXT,
        is_completed BOOLEAN DEFAULT false,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```

#### **2. Backend (NestJS + Raw SQL)**
*   **The Database Driver:** Use the `pg` (node-postgres) library to create a connection pool.
*   **The Service:** Your NestJS service should not use an ORM. You must write the logic manually:
    *   *Example:* `this.db.query('INSERT INTO todos (title) VALUES ($1)', [dto.title])`.
*   **Validation:** Create a **Zod Schema** for the incoming request. If the user sends an empty title or a title longer than 100 characters, the API should return a `400 Bad Request` before it even touches the database.

#### **3. Frontend (React + Radix + Tailwind)**
*   **State Management:** Use `useEffect` and `fetch` (or Axios) to get the list of todos when the page loads.
*   **Styling:** Use **Tailwind CSS** to build a modern, "Linear-style" UI (dark mode, clean borders, subtle shadows).
*   **Components:** 
    *   Use **Radix UI Checkbox** for the "is_completed" status.
    *   Use **Radix UI Dialog** for the "Edit" popup to ensure your app is accessible (Keyboard navigation, focus trapping).

### **The "Why" Behind This Phase**
*   **Why Raw SQL?** Most bugs in large apps happen at the database level. Knowing how to write a manual `INSERT` or `SELECT` makes you a better debugger.
*   **Why Zod?** In the real world, users (and hackers) will try to send "broken" data to your server. Zod acts as your first line of defense.
*   **Why Radix UI?** It provides unstyled, accessible components. This forces you to learn how to style things yourself with Tailwind while keeping the app professional and usable for everyone.

### **Phase 1 Definition of Done (DoD)**
- [ ] I can refresh the browser and my tasks are still there (Persistence).
- [ ] I cannot add a task with an empty title (Zod Validation).
- [ ] I am using `pg.Pool` to manage database connections in NestJS.
- [ ] My UI is responsive and looks good on both mobile and desktop.
- [ ] There is no "ghost" code or unused TypeScript `any` types.
