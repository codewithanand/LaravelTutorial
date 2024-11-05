# Laravel
### Introduction
Laravel is popular PHP framework which can be used to develop web applications. It is based on MVC (Model-View-Controller) architecture, which helps to keep codes structured and organized.

### Why Laravel?
- Simple and clean coding structure
- Built-in features and tools which speeds up development
- Simple and efficient interaction with database using Eloquent ORM
- Keep database structured and version controlled using Migration System
- Modular and Scalable Applications
- Built in CSRF and XSS protection make it more secure

### Laravel vs Other PHP Frameworks
| Feature	| Laravel |	Symfony |	CodeIgniter |	Yii |	Phalcon |	Zend Framework |
|---------|---------|---------|-------------|-----|---------|----------------|
| Ease of Learning |	Moderate |	Moderate-Hard |	Easy |	Moderate |	Hard |	Hard |
| Performance |	Good |	Good |	Very Good |	Very Good |	Excellent |	Good |
| Community |	Large |	Large |	Moderate |	Moderate |	Small |	Moderate |
| Rapid Development |	Excellent |	Good |	Excellent |	Good |	Good |	Moderate |
| Scalability |	High |	High |	Moderate |	High |	High |	Very High |
| Built-in Features |	Extensive |	Extensive |	Minimal |	Good |	Limited |	Good |

# Installation
If you don't have PHP and Composer installed on your local machine, the following commands will install PHP, Composer, and the Laravel installer on macOS, Windows, or Linux:
### macOS
```

/bin/bash -c "$(curl -fsSL https://php.new/install/mac)"

```
### Windows
```

Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://php.new/install/windows'))

```
### Linux
```

/bin/bash -c "$(curl -fsSL https://php.new/install/linux)"

```
If you already have PHP and Composer installed, you may install the Laravel installer via Composer:
```

composer global require laravel/installer

```

# Creating Laravel Project
After you have setup environment, you can create a new laravel project by the following command:
```

laravel new example-app

```
Once the application has been created, you can start Laravel's local development server, queue worker, and Vite development server using the dev Composer script:
```
cd example-app
npm install && npm run build
composer run dev
```
Once you have started the development server, your application will be accessible in your web browser at http://localhost:8000.
