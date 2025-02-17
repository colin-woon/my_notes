- ## composer create-project laravel/laravel project-name
# Setup and Config DB
- edit the values in .env (connection,host,port,database,root,pwd)
- you can see the configurations in config/database.php
- if migration goes wrong, either sql server not running or configuration problem


# Artisan Commands 
`php artisan`
	`help <command-name>` - shows how to for command 
	`list` - lists all commands
	`serve` - runs local web server
	`migrate` - updates database schema (needs migration files + DB connection xxxxxxxto work)
	`migration:rollback`
	`make:migration <migration-name>`
	`make:model <ModelName>`
		`-m (creates migration file too)`
	`make:controller <ControllerName>`
	`make:test <TestName>`
	`make:seeder <SeederName>`
	`make:middleware <MiddlewareName>`
	`optimize`
	`route:list` - list all registered routes
	`test` - run test
	`cache:clear` 
	`config:clear`
	`view:clear` - clear compiled views
	
# Models & Migrations
## Migrations
- up() creates tables, you can input the column fields later
- down() drops or rollsback existing table
# Eloquent ORM


