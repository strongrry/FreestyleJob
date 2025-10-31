// ✅ Jenkins Declarative Pipeline (Windows + Node.js 환경용)
pipeline {
    agent any

    // 🌍 전역 환경 변수 설정
    environment {
        // Node.js 실행 경로를 Jenkins 서비스 환경에 강제로 등록
        PATH = "C:\\Program Files\\nodejs;%PATH%"
    }

    stages {

        // 🗂️ 1️⃣ Git 저장소에서 소스 코드 체크아웃
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        // 📦 2️⃣ npm 패키지 설치
        stage('Install') {
            steps {
                bat '''
                echo === INSTALL 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm install
                '''
            }
        }

        // 🧪 3️⃣ 테스트 실행
        stage('Test') {
            steps {
                bat '''
                echo === TEST 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm test
                '''
            }
        }

        // 🚀 4️⃣ 애플리케이션 실행 (main 브랜치일 때만)
        stage('Start') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.GIT_BRANCH == 'origin/main' }
                }
            }
            steps {
                bat '''
                echo === START 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm run start
                '''
            }
        }
    }

    // 📋 파이프라인 완료 후 후처리
    post {
        success {
            echo '✅ Pipeline 성공적으로 완료!'
        }
        failure {
            echo '❌ Pipeline 실패!'
        }
    }
}