## Assignment 2: Enhanced Blog Application

### Objective
Enhance the basic blog application by adding user authentication using Laravel UI with Bootstrap. Create an admin panel for managing blog posts and users with distinct roles for admin and author.

## Guidelines

#### 1. Setup and Initialise Project (1 point)
- Ensure your development environment is set up with the basic blog application from Assessment 1.
- Create a new branch in your GitHub repository for this feature: `git checkout -b feature/auth-admin-panel`.

#### 2. Setup MongoDB (2 points)

#### 3. Install Laravel UI and Set Up Authentication (2 points)
- Install Laravel UI package: `composer require laravel/ui`.
- Generate the authentication scaffolding: `php artisan ui bootstrap --auth`.
- Run the required commands to set up Bootstrap: `npm install && npm run dev`.
- Update the master layout to include Bootstrap styling.

_Middleware (bonus) [moved to step 8](#8-bonus-create-middleware-for-admin--optionally-author-access-and-apply-to-relevant-routes-2-points)._

#### 4. Define Admin and Author Routes (1 point)
- Define routes in `routes/web.php` for the admin panel with Admin prefix.
- Create routes for managing users and blog posts within the admin panel.
- (_Optionally_) Use separate prefixes for admin and author routes [[as suggested in the forum](https://mylearn.une.edu.au/mod/forum/discuss.php?d=2344727#p6713365)]:
    - Admin Routes: `/admin/*` (e.g., `/admin/register`, `/admin/login`, `/admin/dashboard`)
    - Author Routes: `/author/*` (e.g., `/author/register`, `/author/login`, `/author/dashboard`)
- **OR** Combine Admin _and_ Author routes under the same admin prefix.
- (_Bonus_) Protect routes using middleware to restrict access based on roles.

#### 5. Create Admin Controllers (2 points)
- Generate controllers for managing users and blog posts:
    - `php artisan make:controller Admin/UserController`
    - `php artisan make:controller Admin/PostController`
    - `php artisan make:controller Author/PostController`
        - (_Optional_, or add the author logic in the admin controllers)
- Implement CRUD operations with appropriate validation.

#### 6. Create Blade Views for Admin Panel (4 points)
- Download bootstrap examples from [Bootstrap Examples](https://getbootstrap.com/docs/5.3/examples/)
    - Use the **dashboard template** for the admin panel layout.
    - Use the **form template** to create your forms.
    - OR use your own
- Create new master layout(s):
    - Admin views (`admin.blade.php`): for user and post management.
    - Author views (`author.blade.php`): for managing their own posts.
        - (_Optional_, or just use the admin layout)
- Create new management views for listing, creating, editing, and deleting users and posts.
- Ensure the views use Bootstrap components for styling and are consistent with the overall application design.

#### 7. Enhance User Management (2 points)
- Add roles to users and implement role-based access control:
    - `admin`, `author`, and `user` roles.
    - Update the registration process to allow assigning roles.
    - create a new migration to add roles in the database.
- Ensure only admins can access user management functionalities.
- _More detailed information on role privileges in [next section](#detailed-role-requirements)._

#### 8. (_Bonus_) Create Middleware for Admin (& _Optionally_ Author) Access and Apply to Relevant Routes (2 points)
- Generate middleware to restrict access to the admin panel:
    - `php artisan make:middleware AdminMiddleware`
- Implement the middleware to check if the authenticated user is an admin.
- Apply middleware to the admin routes.

#### 9. Testing (2 points)
- Manually test the authentication system.
- Test each admin functionality by creating, reading, updating, and deleting users and blog posts.
- Ensure that non-admin users cannot access the admin panel.

#### 10. GitHub (2 points)
- Regularly commit your changes and push them to a GitHub repository.

#### 11. Report (2 points)
- Write a brief report in the `README.md` file describing your approach, any challenges faced, and the GitHub repository URL.

## Detailed Role Requirements:

1. **Admin Role:**
    - Full access to post management and user management.
    - Can create, update, delete, and view _all_ posts.
    - Can create, update, delete, and manage all users (authors and users).

2. **Author Role:**
    - Can register via `/author/register`.
    - Limited access post management (posts they own).
    - Can create, update, delete, and view **only their own posts**.
    - Cannot access user management or other authors' posts.

3. **User Role:**
    - Users are **not** part of this assignment but will be handled in Assignment 3.

### Registration and Login:

- **Admin Registration:**
    - Only one admin should be created through a seeder.
    - Admin cannot be registered via the public registration form.
    - Authors can log in via `/admin/login` and be redirected to `/admin/dashboard`.

- **Author Registration** (_Optional_, or add author functionality in the admin stuff):
    - Authors can register via `/author/register`.
    - Authors can log in via `/author/login` and be redirected to `/author/dashboard`.

- **Middleware (_Bonus_):**
    - Ensure that only accounts with the `admin` role can access routes prefixed with `/admin`.
    - Ensure that only accounts with the `author` role can access routes prefixed with `/author`.