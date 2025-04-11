# Part 3: Docker Volumes

This part demonstrates my understanding of Docker volumes by creating, mounting, and persisting data across containers using volumes.

---

## 🧩 Step-by-Step Instructions

### ✅ Step 1: Create a Docker Volume

```bash
docker volume create my_volume
Creates a persistent volume named my_volume that can be mounted in Docker containers.

✅ Step 2: Run an NGINX Container with the Volume
bash
Copy
Edit
docker run -d -p 8080:80 --name nginx-volume-container -v my_volume:/usr/share/nginx/html nginx
Runs an NGINX server in detached mode.

Mounts my_volume to /usr/share/nginx/html so content from the volume is served by NGINX.

Maps port 8080 on the host to port 80 inside the container.

✅ Step 3: Verify the Container is Running
bash
Copy
Edit
docker ps
Checks the list of running containers.

✅ Step 4: Check the Website on Your Browser
Open http://localhost:8080
You should see the default NGINX welcome page.

✅ Step 5: Create index.html on the Host
bash
Copy
Edit
echo "This is my custom content" > index.html
Creates a simple HTML file with custom content.

✅ Step 6: Copy index.html to the Container Volume
bash
Copy
Edit
docker cp index.html nginx-volume-container:/usr/share/nginx/html/index.html
Copies the file into the volume inside the container.

✅ Step 7: Refresh the Browser
Go to http://localhost:8080
You should now see:

This is my custom content

✅ Step 8: Remove the NGINX Container
bash
Copy
Edit
docker rm -f nginx-volume-container
Stops and deletes the container.

✅ Step 9: Run an HTTPD Container Using the Same Volume
bash
Copy
Edit
docker run -d -p 8080:80 --name httpd-volume-container -v my_volume:/usr/local/apache2/htdocs/ httpd
Mounts the same volume to a different container using the HTTPD image.

✅ Step 10: Refresh Browser
Go to http://localhost:8080
You should still see:

This is my custom content

This proves the volume data persisted.

✅ Step 11: Update index.html on the Host
bash
Copy
Edit
echo "New HTTPD content" > index.html
Changes the content of the file.

✅ Step 12: Copy the New File into the HTTPD Container
bash
Copy
Edit
docker cp index.html httpd-volume-container:/usr/local/apache2/htdocs/index.html
Updates the content in the volume.

✅ Step 13: Check the Browser Again
Visit http://localhost:8080
Now it should display:

New HTTPD content

✅ Step 14: Remove the HTTPD Container
bash
Copy
Edit
docker rm -f httpd-volume-container
Deletes the container.

✅ Step 15: Restart NGINX with the Same Volume
bash
Copy
Edit
docker run -d -p 8080:80 --name nginx-volume-container -v my_volume:/usr/share/nginx/html nginx
✅ Step 16: Final Verification
Go to http://localhost:8080
You should still see:

New HTTPD content

This confirms that the volume persisted across different containers and sessions.

📝 Final Observations
Docker volumes are persistent and outlive containers.

Data added in one container using the volume is accessible in another container.

Volumes are ideal for storing data that must survive container restarts or recreations.

📦 Summary of Docker Commands Used
bash
Copy
Edit
docker volume create my_volume
docker run -d -p 8080:80 --name nginx-volume-container -v my_volume:/usr/share/nginx/html nginx
docker run -d -p 8080:80 --name httpd-volume-container -v my_volume:/usr/local/apache2/htdocs/ httpd
docker cp index.html container_name:/path
docker rm -f container_name
docker ps
🔗 GitHub Repository
https://github.com/your-username/your-repo-name