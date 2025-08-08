# Tahap 1: Gunakan image frontend sebagai sumber file statis.
# Nama image harus sesuai dengan yang Anda dorong ke Docker Hub.
FROM kresnandaf/herca-frontend:latest as frontend-builder

# Tahap 2: Gunakan image backend sebagai sumber file PHP.
# Nama image harus sesuai dengan yang Anda dorong ke Docker Hub.
FROM kresnandaf/herca-backend:latest as backend-builder

# Tahap 3: Bangun image Nginx final.
FROM nginx:alpine

# Salin file konfigurasi Nginx kustom.
# Ini adalah file default.conf yang sudah kita buat.
COPY default.conf /etc/nginx/conf.d/default.conf

# Salin file hasil build frontend dari tahap pertama ke Nginx's web root.
# Pastikan jalur ini benar untuk file frontend Anda.
COPY --from=frontend-builder /usr/share/nginx/html /usr/share/nginx/html

# Salin direktori public backend dari tahap kedua ke lokasi yang benar.
# Ini penting untuk melayani index.php.
COPY --from=backend-builder /var/www/html/public /var/www/html/public

# Ekspos port dan jalankan Nginx.
EXPOSE 80
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]
