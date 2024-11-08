# Database Configuration and Migration
### Configuring a Database Connection
In Laravel (a popular PHP framework), you need to configure the database connection settings in the `config/database.php` file or the `.env` environment file. This includes specifying the database type (e.g., MySQL, PostgreSQL, SQLite), database name, username, password, and other related settings.

Example in `.env` file:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database
DB_USERNAME=root
DB_PASSWORD=secret
```
The Laravel framework will use these values to establish a connection to the database when you run queries or interact with models.

### Migrations and Schema Building
Migrations in Laravel are like version control for your database. They allow you to define the structure of your database (tables, columns, indexes) in code, making it easier to share and maintain the database schema.

- **Creating Migrations**: You can create a migration using the Artisan CLI with the command:
  ```bash
  php artisan make:migration create_users_table
  ```
  This will create a migration file where you can define the table's structure.
  
- **Schema Building**: Inside the migration, you use Laravel's schema builder to define tables and columns:
  ```php
  Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->timestamps();
  });
  ```

### Rolling Back Migrations
If you need to undo the changes made by a migration, you can "rollback" the migration. This is useful when testing or fixing errors in your schema.

To rollback a migration:
```bash
php artisan migrate:rollback
```
This will undo the last batch of migrations. You can also use `php artisan migrate:reset` to rollback all migrations or `php artisan migrate:fresh` to drop all tables and re-run all migrations.

# Models and Relationships
### Creating Models
In Laravel, a model represents a table in the database and provides an easy way to interact with that table. You can create a model using Artisan:
```bash
php artisan make:model User
```

This creates a `User` model class, which typically resides in the `app/Models` directory. By default, Laravel will assume that the model corresponds to a table with the plural, snake_case version of the model name (e.g., `users` table for `User` model).

### Defining Relationships
Models in Laravel can define relationships with other models. Common relationships include:

- **One-to-One**: A one-to-one relationship means one record in one table is associated with one record in another table. Example: A `User` model has one `Profile` model.
  ```php
  class User extends Model
  {
      public function profile()
      {
          return $this->hasOne(Profile::class);
      }
  }
  ```

- **One-to-Many**: A one-to-many relationship means one record in one table is associated with multiple records in another table. Example: A `Post` model has many `Comment` models.
  ```php
  class Post extends Model
  {
      public function comments()
      {
          return $this->hasMany(Comment::class);
      }
  }
  ```

- **Many-to-Many**: A many-to-many relationship means multiple records in one table are associated with multiple records in another table. This is typically implemented with a pivot table. Example: A `Student` model belongs to many `Course` models, and vice versa.
  ```php
  class Student extends Model
  {
      public function courses()
      {
          return $this->belongsToMany(Course::class);
      }
  }
  ```

- **Polymorphic**: Polymorphic relationships allow a model to belong to more than one other model using a single association. Example: A `Comment` model could be associated with both `Post` and `Video` models.
  ```php
  class Comment extends Model
  {
      public function commentable()
      {
          return $this->morphTo();
      }
  }
  ```

### Eloquent Methods for Querying Data
Eloquent is Laravel’s **ORM (Object-Relational Mapping)** that provides an easy, expressive syntax for interacting with your database. Some common methods for querying data include:

- All records:
  ```php
  $users = User::all();
  ```
  
- Find by primary key:
  ```php
  $user = User::find(1); // Find user with ID 1
  ```
  
- Where conditions:
  ```php
  $users = User::where('status', 'active')->get();
  ```
  
- Order by:
  ```php
  $users = User::orderBy('name', 'asc')->get();
  ```
  
- Limit:
  ```php
  $users = User::limit(10)->get();
  ```
  
- Paginate:
  ```php
  $users = User::paginate(10); // For pagination
  ```

  # Eloquent CRUD Operations
  ### Inserting, Updating, and Deleting Records
  Eloquent provides a simple interface for CRUD operations:

  - Inserting:
    ```php
    $user = new User();
    $user->name = 'John Doe';
    $user->email = 'john@example.com';
    $user->save();
    ```
    
  - Updating:
    ```php
    $user = User::find(1);
    $user->name = 'Jane Doe';
    $user->save();
    ```
    
  - Deleting:
    ```php
    $user = User::find(1);
    $user->delete();
    ```

You can also use the `destroy` method to delete multiple records by their IDs:
  ```php
  User::destroy([1, 2, 3]);
  ```

### Query Scopes
Query scopes are custom query methods that you can define in your model to reuse common queries. For example, you can define a scope to fetch only active users:

```php
class User extends Model
{
    public function scopeActive($query)
    {
        return $query->where('status', 'active');
    }
}

// Usage:
$activeUsers = User::active()->get();
```
Scopes allow for more readable and reusable code.

### Soft Deletes and Restoring Records
Soft deletes allow you to mark records as deleted without actually removing them from the database. This is useful when you want to keep historical data.
- **Enable Soft Deletes**: To enable soft deletes, you need to add the SoftDeletes trait in your model:
  ```php
  use Illuminate\Database\Eloquent\SoftDeletes;

  class User extends Model
  {
      use SoftDeletes;
  }
  ```
  
- **Soft Deleting**
  ```php
  $user = User::find(1);
  $user->delete(); // This will soft delete the user
  ```
  
- **Restoring Soft Deleted Records**
  ```php
  $user = User::withTrashed()->find(1); // Find even soft deleted users
  $user->restore(); // Restore the soft deleted user
  ```

- **Force Deleting**: If you want to permanently delete a soft-deleted record:
  ```php
  $user = User::withTrashed()->find(1);
  $user->forceDelete();
  ```
