# 🐍 Python Application with Jenkins CI/CD Pipeline 🚀

![image](https://github.com/user-attachments/assets/9a1a1e6c-e4cf-46d8-ab58-613a5d6e9977)


## 📌 Project Overview
This project demonstrates a simple Python application with a complete CI/CD pipeline using Jenkins, Docker, and GitHub. The application provides a command-line tool that adds two numbers together, with automated testing and continuous integration/deployment.

⚠️ **Note:** Ensure Docker Desktop is running in the background before executing any Docker-related commands.

---

## 🏗️ Project Components

### 📂 Project Structure
```
.
├── sources/
│   ├── add2vals.py      # 🎯 Main application entry point
│   ├── calc.py          # 🧮 Core calculation module
│   └── test_calc.py     # 🧪 Unit tests
├── dist/               # 📦 Compiled executables
├── requirements.txt    # 📜 Python dependencies
├── Jenkinsfile        # ⚙️ Pipeline configuration
├── docker-compose.yml # 🐳 Docker setup
└── README.md         # 📖 Project documentation
```

### 🐍 Python Application
- **add2vals.py**: 🎯 Handles command-line arguments and displays results.
- **calc.py**: 🧮 Core calculation module containing the addition logic.
- **test_calc.py**: 🧪 Unit tests for the calculation module.
- **requirements.txt**: 📜 Lists Python dependencies with specific versions.

### 🏗️ Jenkins Pipeline
- **Jenkinsfile**: ⚙️ Defines the CI/CD pipeline workflow.
- **docker-compose.yml**: 🐳 Configures Jenkins and its agents with volume mappings and network settings.

### 🐳 Docker Configuration
- **Jenkins container**: 🏗️ Main Jenkins server with persistent storage.
- **Jenkins agent container**: ⚡ For distributed builds.
- **Python build container**: 🏭 Used for building and testing the application.

---

## 🔧 Steps to Perform This Project

### Step 1: 🛠️ Setup Jenkins

#### 1️⃣ Pull Jenkins Image and Start Containers
```bash
docker-compose up -d
```

![WhatsApp Image 2025-04-03 at 00 06 03_9ae8110f](https://github.com/user-attachments/assets/5ffdce6f-da3c-459b-ae02-190e41c0d7c3)


#### 2️⃣ Get Initial Admin Password
```bash
docker-compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

#### 3️⃣ Access Jenkins 🌍
- Open a browser and go to: `http://localhost:8080`
- Enter the initial admin password from step **2️⃣**

  ![WhatsApp Image 2025-04-03 at 00 08 12_41fc77da](https://github.com/user-attachments/assets/b688fdde-a62f-48a1-ad60-8c2f8cb86856)


#### 4️⃣ Install Plugins 🔌
- Click **Install suggested plugins** and wait for installation to complete.

  ![WhatsApp Image 2025-04-03 at 00 05 37_1a21a46e](https://github.com/user-attachments/assets/475aa442-0b16-40e0-80f0-b16111b6d83d)

  ![WhatsApp Image 2025-04-03 at 00 07 32_d68f6942](https://github.com/user-attachments/assets/6d1871e7-a2bd-4114-84bf-cf0c8edcbdb1)



#### 5️⃣ Create First Admin User 👤
- Enter your desired username, password, and email.
- Click **Save and Continue**.

![WhatsApp Image 2025-04-03 at 00 11 12_e50b2566](https://github.com/user-attachments/assets/fb3a263b-a680-4b0a-bc76-2f4764d599a2)

#### 6️⃣ Configure Jenkins Instance ⚙️
- Keep the default URL: `http://localhost:8080/`
- Click **Save and Finish**.

  ![WhatsApp Image 2025-04-03 at 00 12 01_5770fb5e](https://github.com/user-attachments/assets/d4a067e7-55fa-4671-a0ca-130519ba4b62)

  ![WhatsApp Image 2025-04-03 at 00 12 40_7f1fef45](https://github.com/user-attachments/assets/9fbd4c2c-67a3-482d-b669-dd6276affeba)



#### 7️⃣ Create a Pipeline Project 🚀
- Click **New Item**
- Enter project name: `simple-python-pyinstaller-app`
- Select **Pipeline** and click **OK**
- In the pipeline configuration:
  - Scroll to the **Pipeline** section
  - Select **Pipeline script from SCM**
  - Choose **Git** as SCM
  - Enter repository URL: `https://github.com/Shelly151/Jenkins-Orchestration.git`
  - Enter branch specifier: `*/master`
  - Click **Save**

    ![WhatsApp Image 2025-04-03 at 00 13 41_bd01c482](https://github.com/user-attachments/assets/61ddd64d-2dc5-435b-80af-d2da60785c28)

    ![WhatsApp Image 2025-04-03 at 00 16 35_ff52c4e7](https://github.com/user-attachments/assets/163d25f5-823d-48e7-a226-7ed33af72634)



#### 8️⃣ Install and Configure Docker in Jenkins Container 🐳
```bash
# Install Docker inside Jenkins container
docker-compose exec jenkins bash -c "apt-get update && apt-get install -y docker.io"

# Start Docker service
docker-compose exec jenkins bash -c "service docker start"

# Verify Docker installation
docker-compose exec jenkins docker --version
```

![WhatsApp Image 2025-04-03 at 00 18 33_aad2d904](https://github.com/user-attachments/assets/3ed39d72-8bce-4c6f-8aaf-700825bb8c91)

![WhatsApp Image 2025-04-03 at 00 19 24_d828ee60](https://github.com/user-attachments/assets/8d281826-6836-47a4-964a-86d6ce070616)

![WhatsApp Image 2025-04-03 at 00 19 52_8ec9c381](https://github.com/user-attachments/assets/8cd2a95e-734f-41a6-859d-42b15ecd75c9)


#### 9️⃣ Install Docker Plugins 🔌
- Navigate to **Manage Jenkins > Manage Plugins**
- Under **Available** tab, search for and install:
  - **Docker Pipeline**
  - **Docker plugin**
  - **docker-build-step**
 
    ![WhatsApp Image 2025-04-03 at 00 20 51_9d827708](https://github.com/user-attachments/assets/6b6aa22f-4151-48b5-8848-692cca0e0669)

![WhatsApp Image 2025-04-03 at 00 22 28_93b962f9](https://github.com/user-attachments/assets/a9808a32-f568-4145-893c-358e1d673b2c)


#### 🔟 Restart Jenkins After Plugin Installation 🔄
```bash
docker-compose restart jenkins
```
- Wait for Jenkins to restart (~30 seconds)
- Verify Jenkins is running:
```bash
docker-compose ps
```
![WhatsApp Image 2025-04-03 at 00 23 10_69f0d488](https://github.com/user-attachments/assets/1e6ab944-b991-401d-99d4-45ccbae0101e)


#### 🔑 Sign in to Jenkins 🔐
- Use the credentials created in step **5️⃣**

#### ▶️ Run the Pipeline 🚦
- Go to **Jenkins Dashboard** → Open `simple-python-pyinstaller-app`
- Click **Build Now**

---

### Step 2: 🛠️ Testing the Executable

#### 📥 Download the Executable from Jenkins 💾
1. Open **Jenkins Dashboard**
2. Click on `simple-python-pyinstaller-app`
3. Click on the latest build number
4. Under **Build Artifacts**, download `add2vals`

⚠️ **Note:** The executable is a Linux version since Jenkins runs in a Linux container.

#### ▶️ Run the Executable on Windows Using WSL 💻
```bash
# Check if WSL is installed
wsl --version

# If not installed, run:
wsl --install

# Restart computer and verify installation:
wsl --version

# Open WSL terminal
wsl

# Navigate to the download directory in WSL
cd /mnt/c/Users/asus/OneDrive/Downloads

# Make the file executable
chmod +x add2vals

# Run the executable
./add2vals 5 3
```

---

## 📌 What Does PyInstaller Do?
**PyInstaller** creates a standalone executable from the Python application.

### 🔍 Phases of PyInstaller
1️⃣ **Analysis Phase**: Scans dependencies, identifies required files, and builds a dependency graph.
2️⃣ **Bundling Phase**: Packages dependencies, Python interpreter, and resources into a single executable.
3️⃣ **Output**: Generates an executable stored in the `dist/` directory.

### 🌟 Benefits of PyInstaller
✅ **Portability**: No Python installation required, easy distribution.
✅ **Dependency Management**: Includes all required libraries.
✅ **Cross-Platform Support**: Generates executables for Windows, Linux, and macOS.

---

## 🎯 Conclusion
This project successfully sets up a CI/CD pipeline with Jenkins, Docker, and PyInstaller. By following the steps above, you have:

✔️ Set up a Jenkins server with Docker support.
✔️ Created a pipeline that automatically builds, tests, and packages the application.
✔️ Generated a standalone executable that runs on any system.

🎉 **Thank You!**
If you found this guide helpful, consider:
- ⭐ **Starring this repository**
- 📢 **Sharing it with others**
- 🛠️ **Contributing improvements**
- 📝 **Reporting any issues you encounter**

**Happy coding! 🚀**
