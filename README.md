# PHPMyAdmin-Import limit-Max

*Note: Replace `/etc/php.ini` with your actual `php.ini` path (e.g., `/etc/php/8.1/fpm/php.ini`).*

### Option A: The "One-Click" `sed` Method
Run this single command to automatically update all four values to 512M/300s:

```bash
sudo sed -i 's/^upload_max_filesize = .*/upload_max_filesize = 512M/; s/^post_max_size = .*/post_max_size = 512M/; s/^memory_limit = .*/memory_limit = 512M/; s/^max_execution_time = .*/max_execution_time = 300/' /etc/php.ini
```
*(Note: If the values don't change, they might be commented out with a `;`. Use Option B to uncomment them).*

---

### Option B: The Manual `nano` Method
1. **Open** the file:
   ```bash
   sudo nano /etc/php.ini
   ```
2. **Search** for each setting by pressing `Ctrl+W`, typing the name (e.g., `upload_max_filesize`), and pressing `Enter`.
3. **Edit** the values (remove the `;` at the start of the line if it is commented out):
   ```ini
   upload_max_filesize = 512M
   post_max_size = 512M
   memory_limit = 512M
   max_execution_time = 300
   ```
4. **Save** and exit: Press `Ctrl+O`, `Enter`, then `Ctrl+X`.

---

### Final Step: Restart Services
Apply the changes by restarting PHP and your web server:

```bash
# For Apache
sudo systemctl restart php-fpm && sudo systemctl restart apache2

# OR for Nginx
sudo systemctl restart php-fpm && sudo systemctl restart nginx
```
*(Adjust `php-fpm` to your specific version if needed, e.g., `php8.1-fpm`)*.
