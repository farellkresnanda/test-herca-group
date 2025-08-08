# Tahap 1: Gunakan image frontend sebagai sumber file
FROM kresnandaf/herca-frontend:latest as frontend-builder

# Tahap 2: Gunakan image Nginx sebagai base
FROM nginx:alpine

# Salin file konfigurasi Nginx kustom dari direktori host
COPY default.conf /etc/nginx/conf.d/default.conf

# Salin file hasil build frontend dari tahap pertama ke Nginx's web root
COPY --from=frontend-builder /usr/share/nginx/html /usr/share/nginx/html

# Ekspos port dan jalankan Nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
