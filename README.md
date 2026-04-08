## 🚀 Jenkins + Python Flask CI/CD

### 📌 Prerequisites

Install Java and Jenkins first.

Then install required tools on your Jenkins server:

```bash
sudo yum install -y git python3 python3-pip
```

---

## ⚙️ Jenkins Pipeline

Use the following pipeline in your Jenkins job:

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Abinash003A/cicd-python-cod-test.git'
            }
        }

        stage('Test') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                pytest
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                source venv/bin/activate
                nohup python3 app.py > app.log 2>&1 &
                '''
            }
        }
    }
}
```

---

## 📷 Output

<img width="801" height="247" alt="image" src="https://github.com/user-attachments/assets/1f2931ad-de25-4a43-99b5-52d192b6c7e1" />

---

## 📝 Notes

* The Flask app runs in the background using `nohup`
* Logs are stored in `app.log`
* If you rerun the pipeline, you may get:

  ```
  Address already in use
  ```

  because the previous process is still running

---

## ✅ Summary

* Jenkins handles CI pipeline
* Python virtual environment is used for dependencies
* Flask app runs in background
