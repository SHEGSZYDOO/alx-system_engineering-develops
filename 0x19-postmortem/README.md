After ALX's System Engineering & DevOps project 0x19 was released at approximately 06:00 West African Time (WAT) in Nigeria, an outage occurred on an isolated Ubuntu 20.04 container running an Apache web server. Instead of the expected HTML file defining a simple Holberton WordPress site, GET requests on the server resulted in 600 Internal Server Errors.
The issue was identified by a bug debugger named Bamidele at approximately 19:20 PST, who then followed the following steps to resolve the issue:
1. Checked running processes using ps aux and found that two apache2 processes (running as root and www-data) were running properly.
2. Determined that the web server was serving content located in /var/www/html/ by looking in the sites-available folder of the /etc/apache2/ directory.
3. Ran strace on the PID of the root Apache process in one terminal and curled the server in another. However, strace provided no useful information.
4. Repeated step 3 on the PID of the www-data process, and strace revealed an -1 ENOENT (No such file or directory) error occurring upon an attempt to access the file /var/www/html/wp-includes/class-wp-locale.phpp.
5. Looked through files in the /var/www/html/ directory one-by-one and located the erroneous .phpp file extension using Vim pattern matching. The error was found in the wp-settings.php file (Line 137: require_once( ABSPATH . WPINC . '/class-wp-locale.php' );).
6. Removed the trailing p from the line.
7. Tested another curl on the server, and it returned a 200 response code.
8. Created a Puppet manifest (0-strace_is_your_friend.pp) to automate the fixing of any identical errors that may occur in the future. The manifest replaces any phpp extensions in the file /var/www/html/wp-settings.php with php.
In summary, the issue was caused by a typo: the WordPress app was encountering a critical error in wp-settings.php when trying to load the file class-wp-locale.phpp. The correct file name was class-wp-locale.php, which was located in the wp-content directory of the application folder. The patch involved a simple fix of removing the trailing p from the erroneous file extension.
To prevent similar outages in the future, the following measures are recommended:
• Test the application before deploying to identify and address issues earlier.
• Enable uptime monitoring services such as UptimeRobot to detect and alert instantly upon outage of the website.
Despite the creation of the Puppet manifest to automate the fixing of such errors, it is still essential to be vigilant in testing and monitoring the system to prevent outages caused by simple errors like typos.
