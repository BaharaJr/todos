# 🚀 Full-Stack Todo

Welcome to the Full-Stack Developer challenge. You will build a scalable system starting from a simple Todo app using Raw SQL and graduating to a complex E-commerce platform using TypeORM.

## 🛠 Tech Stack
- **Backend:** NestJS
- **Database:** PostgreSQL (using `pg` driver for Raw SQL)
- **Frontend:** React (Vite)
- **Styling:** Tailwind CSS + Radix UI
- **Validation:** Zod
- **Language:** TypeScript

---

## 📜 Coding Standards & Conventions
- **Variables/Functions:** `camelCase` (e.g., `fetchTodos`).
- **Classes/Interfaces:** `PascalCase` (e.g., `TodoService`).
- **Documentation:** Use **TSDoc** for all service methods.
- **Types:** No `any`. Use `z.infer` for types where possible.

---

## 🔄 Incremental Review Workflow (Important!)
To ensure you get feedback early, do not wait until the end of the Phase to push code. Follow this "Feature-by-Feature" workflow:

1. **Fork & Clone:** Fork [BaharaJr/todos](https://github.com/BaharaJr/todos) and clone it locally.
2. **Phase Branch:** Create a branch for the current phase: `git checkout -b phase-1-todo`.
3. **Draft PR:** Immediately push an empty commit and open a **Draft Pull Request** in the original repo.
4. **Feature Development:** 
   - Work on a single feature (e.g., `POST /todos` API).
   - **Commit & Push:** Once that specific feature works:
     ```bash
     git add .
     git commit -m "feat: implement create todo endpoint with zod validation"
     git push origin phase-1-todo
     ```
5. **Request Review:** Drop a comment in the PR: *"Finished the Create API, ready for review."* and BaharaJr as a reviewer
6. **Repeat:** Continue this for the List, Update, and Delete features.
