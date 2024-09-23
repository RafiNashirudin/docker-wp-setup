### 1. **Introduction**
   - Panduan ini memandu Anda dalam menerapkan WordPress menggunakan Docker dan Docker Compose.

### 2. **Prerequisites**
   - Tools yang dibutuhkan:
     - Docker & Docker Compose
     - Git (opsional, jika mengambil dari repository)
     - Server Linux (misal: Ubuntu 20.04)

### 3. **Step-by-Step Deployment**

#### Step 1: **Install Docker dan Docker Compose**
   ```bash
   sudo apt update
   sudo apt install docker.io
   sudo apt install docker-compose
   ```

#### Step 2: **Setup Docker Compose File**
   Buat `docker-compose.yml` untuk mengatur container WordPress dan MySQL:
   ```yaml
   version: '3.1'

   services:
     db:
       image: mysql:5.7
       volumes:
         - db_data:/var/lib/mysql
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: example

     wordpress:
       image: wordpress:latest
       ports:
         - "8080:80"
       restart: always
       environment:
         WORDPRESS_DB_HOST: db:3306
         WORDPRESS_DB_PASSWORD: example
       volumes:
         - wordpress_data:/var/www/html

   volumes:
     db_data:
     wordpress_data:
   ```

#### Step 3: **Deploy the Containers**
   Jalankan perintah di directory yang berisi file `docker-compose.yml`:
   ```bash
   docker-compose up -d
   ```

#### Step 4: **Access WordPress**
   - Buka browser dan akses `http://<server_ip>:8080` untuk menyelesaikan instalasi WordPress.