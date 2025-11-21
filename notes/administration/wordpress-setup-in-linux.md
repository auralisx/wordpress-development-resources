This note tries to deploy WordPress in a way that mirrors modern best industry standard practices used by professionals which is secure, maintainable and performant without overcomplicating the setup. It focuses on simplicity and ease of use while maintaining best practices.

# Industry standard architecture

Apache is still an excellent choice for many users as it is widely available, easy to use, and has a large community of users and developers who can provide support and assistance. It is the default web server used by many shared hosting providers as nginx doesn't shine in shared environments. But for sites that expects a lot of traffic and speed matters, Nginx is a better choice. A lot of websites are migrating to Nginx. A more detailed explanation of the difference between Apache and Nginx can be found on [apache vs nginx vs litespeed](https://www.wpbeginner.com/opinion/apache-vs-nginx-vs-litespeed/) and [nginx-vs-apache](https://kinsta.com/blog/nginx-vs-apache/).

> [!NOTE]
> Hybrid setup (e.g., Nginx as reverse proxy in front of Apache, where nginx handles static content and apache handles dynamic content) are common in use but is not really needed for most cases. Adding both adds complexity without significant benefit, thanks to a more mature softwares at present. You should only put apache behind nginx if you absolutely need it. The hybrid stack exists but it is not the best practice anymore.

| Layer | Component | Reasoning |
|-------|-----------|-----------|
| Web Server | Nginx | Fast, lightweight, excellent with static assets and reverse proxying. |
| Application | PHP-FPM | More secure and memory efficient than mod_php, allowing for better resource management and scalability. |
| Database | MariaDB | MariaDB is a community-developed fork of MySQL, offering improved performance, security, and scalability. MariaDB or MySQL is still standard. Other databases like PostgreSQL or SQLite can also be used depending on the specific requirements of the application. |
| Caching | OPcache (PHP) + Redis or Memcached | OPcache improves PHP performance by storing precompiled script bytecode in shared memory, reducing the overhead of parsing and compiling PHP code. Redis and Memcached are popular in-memory data stores that can be used for caching frequently accessed data, improving application performance. |
| Updates | WP-CLI | WP-CLI is a command-line interface for WordPress, allowing for easy management and automation of WordPress tasks. |


# Step-by-Step Setup (Arch Linux)

1. Install packages
I am on Arch linux so I will use pacman to install the packages. The package manager or package name can differ in different distributions so it's advisable to do some research before installing packages.

> [!NOTE]
> I am following the installation and configuration guide available on Arch Wiki. You can view the wiki pages for more details > [PHP](https://wiki.archlinux.org/title/PHP), [WordPress](https://wiki.archlinux.org/title/WordPress), [MariaDB](https://wiki.archlinux.org/title/MariaDB) and [Nginx](https://wiki.archlinux.org/title/Nginx).

```
sudo pacman -S nginx php-fpm mariadb wp-cli
```
> [!NOTE]
> I am just installing core packages. You can install additional packages or extensions as per your requirements. You can find more about the recommended server environment with php extensions list for WordPress in [Server Environment](https://make.wordpress.org/hosting/handbook/server-environment/).
