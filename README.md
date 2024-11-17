Frontend (React + MUI)
1. Contact Form
Purpose:

Allows users to input new contact details.
Ensures that data like name, email, and phone are collected correctly.
Key Features:

Fields: First Name, Last Name, Email, Phone, Company, Job Title.
Validation: Ensures that no field is left empty.
Design: Material UI (MUI) components for a professional and responsive UI.
Submission: Sends the entered data to the backend API via a POST request.
Code Highlights:

useState manages form state for controlled inputs.
Form submission calls the fetchContacts() function to update the contacts table dynamically without refreshing the page.
2. Contact Table
Purpose:

Displays a list of all contacts retrieved from the backend.
Provides sorting, pagination, and action buttons for each contact.
Key Features:

Sorting: Users can sort contacts based on fields (e.g., name, company).
Pagination: Limits the number of contacts displayed on a single page for large datasets.
Actions: Includes Edit and Delete buttons for each row.
Code Highlights:

MUI's Table and TablePagination components ensure the table is interactive and responsive.
handleDelete() triggers an API call to remove a contact and updates the table view.
3. App Component
Purpose:

Acts as the main controller for the frontend.
Fetches contact data, renders the form and table components, and manages state for the application.
Key Features:

Integrates the ContactForm and ContactTable components.
Handles API interactions via Axios for GET, POST, and DELETE requests.
Centralizes data fetching (fetchContacts()) to ensure the UI updates dynamically.
Backend (Node.js + Express)
1. API Design
Endpoints:

POST /contacts

Accepts a JSON object from the frontend to add a new contact.
Validates required fields (e.g., First Name, Email).
Handles duplicate entries by checking email/phone uniqueness.
GET /contacts

Retrieves all contact entries from the database.
Returns a JSON array to populate the frontend table.
PUT /contacts/

Updates contact details for a given ID.
Ensures that the new data is valid before saving changes.
DELETE /contacts/

Deletes a contact from the database by ID.
Returns a success status if the operation is completed.
Error Handling:

Ensures meaningful error messages for validation failures or server issues.
For instance, a duplicate email might return a 400 Bad Request with an appropriate message.
2. Database Integration
Database Used: MongoDB

Why MongoDB?

Schema flexibility: MongoDB allows JSON-like documents, making it easy to manage the dynamic nature of contact information.
Scalability: Well-suited for growing datasets with minimal schema changes.
Quick development: Integration with Mongoose simplifies data modeling.
Schema Design:

javascript
Copy code
const contactSchema = new mongoose.Schema({
  firstName: { type: String, required: true },
  lastName: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  phone: { type: String, required: true },
  company: String,
  jobTitle: String,
});
Mongoose Benefits:

Automatically enforces the schema at the application level.
Simplifies CRUD operations with built-in methods like find(), save(), and findByIdAndUpdate().
Workflow Description
Adding a Contact:

User fills out the contact form and submits it.
The frontend sends a POST request to /contacts.
Backend validates the input, saves the new contact in the database, and returns success.
Frontend updates the contact table dynamically.
Viewing Contacts:

On page load, the frontend sends a GET request to /contacts.
Backend retrieves all contacts and sends them to the frontend.
Contacts are displayed in the table with pagination and sorting.
Editing a Contact:

User clicks the Edit button for a contact, opening a pre-filled form.
After editing, the updated data is sent via a PUT request to /contacts/:id.
Backend updates the database and returns the updated contact.
Frontend refreshes the table to show the updated data.
Deleting a Contact:

User clicks the Delete button for a contact.
The frontend sends a DELETE request to /contacts/:id.
Backend removes the contact and returns success.
Frontend refreshes the table to remove the deleted contact.
Challenges and Solutions
Pagination and Sorting:

Challenge: Implementing these features in both the frontend and backend for large datasets.
Solution: MUI’s TablePagination handles the frontend, while MongoDB’s skip() and limit() methods manage backend pagination.
Validation:

Challenge: Ensuring valid email, phone, and required fields at both frontend and backend.
Solution: Use frontend libraries like Yup for real-time validation and backend checks for server-side security.
Concurrency Issues:

Challenge: Handling simultaneous updates/deletions on the same contact.
Solution: Use unique identifiers (MongoDB’s _id) and ensure atomicity in operations.
Error Handling:

Challenge: Communicating clear errors to the user (e.g., "Email already exists").
Solution: Standardized error messages and frontend feedback.
How to Run
Frontend Setup:
Navigate to the project folder: cd contact-management.
Install dependencies: npm install.
Start the development server: npm start.
Backend Setup:
Navigate to the backend folder: cd backend.
Install dependencies: npm install.
Start MongoDB locally or connect to a cloud instance.
Run the server: node server.js.
