# Rails App with PostgreSQL

This guide will walk you through setting up a new Rails application with PostgreSQL as the database.

## Steps to Create and Configure Rails App with PostgreSQL

### 1. Create a New Rails Application

Run the following command to create a new Rails application with PostgreSQL as the database, skipping Turbolinks:

```bash
rails _7.0.5_ new hello --skip-turbolinks --database=postgresql
```

### 2. Install PostgreSQL
Ensure that PostgreSQL is installed on your machine. You can install it using Homebrew (for macOS):

```bash
brew install postgresql@15
```

Start PostgreSQL:
```bash
brew services start postgresql@15
```
### 3. Configure database.yml
After creating the Rails app, navigate to the config/database.yml file and configure it to use your PostgreSQL settings.

Example of config/database.yml:
```yml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: 5
  username: <%= ENV['PG_USER'] %>   # Using environment variable for username
  password: <%= ENV['PG_PASSWORD'] %>  # Using environment variable for password
  host: <%= ENV['PG_HOST'] || 'localhost' %>  # Default to localhost if PG_HOST not set
  port: <%= ENV['PG_PORT'] || 5432 %>  # Default to 5432 if PG_PORT not set

development:
  <<: *default
  database: hello_development

test:
  <<: *default
  database: hello_test

production:
  <<: *default
  database: hello_production

```

### 4. Set Up Environment Variables
To securely store your database credentials, you can set up environment variables.

For macOS using Zsh (or Bash):
Add these lines to your ~/.zshrc (or ~/.bash_profile for Bash) to set environment variables:

```bash
export PG_USER=your_postgresql_user
export PG_PASSWORD=your_postgresql_password
export PG_HOST=localhost
export PG_PORT=5432
```

After editing the file, apply the changes:

```bash
source ~/.zshrc  # or source ~/.bash_profile if using Bash
```

### 5. Create the Database
Run the following command to create the databases for development and test:

```bash
rails db:create
```
This command will create the databases hello_development and hello_test in PostgreSQL.

### 6. Run Migrations
Once the databases are created, run the migrations to set up the schema:

```bash
rails db:migrate
```

### 7. Start the Rails Server
Now that everything is set up, start the Rails server:

```bash
rails server
```
Your Rails application should now be running, and PostgreSQL is successfully configured as your database.

### 8. Check Database in PGAdmin
To verify that your tables were created and the database is set up correctly, you can open PGAdmin and connect to your PostgreSQL server. You should see the hello_development and hello_test databases listed.









