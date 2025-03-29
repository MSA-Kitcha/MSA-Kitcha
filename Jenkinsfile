pipeline {
    agent any

    environment {
        // Docker Hub에 로그인하기 위한 Jenkins Credentials (id: dockerHubCredentials)
        REGISTRY_CREDENTIALS = credentials('dockerHubCredentials')
        // Docker 이미지 태그에 사용할 Docker Hub 리포지토리명
        DOCKER_REPO = "99koo"
    }
    
    stages {
        stage('Checkout') {
            steps {
                // 깃 레포(MSA-Kitcha) + 서브모듈 모두 체크아웃
                checkout scm
                sh """
                  git submodule update --init --recursive
                """
            }
        }
/*
        stage('Build & Push Config') {
            steps {
                dir('MSA-Kitcha-BE') {
                    script {
                        sh """
                          docker build -f Config-server/Dockerfile -t \${DOCKER_REPO}/config:latest .
                        """
                        sh """
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/config:latest
                        """
                    }
                }
            }
        }
        
        stage('Build & Push Eureka') {
            steps {
                dir('MSA-Kitcha-BE') {
                    script {
                        sh """
                          docker build -f eureka/Dockerfile -t \${DOCKER_REPO}/eureka:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/eureka:latest
                        """
                    }
                }
            }
        }

        stage('Build & Push Gateway') {
            steps {
                dir('MSA-Kitcha-BE') {
                    script {
                        sh """
                          docker build -f API-Gateway/Dockerfile -t \${DOCKER_REPO}/gateway:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/gateway:latest
                        """
                    }
                }
            }
        }
    */
        stage('Build & Push Authentication') {
            steps {
                dir('MSA-Kitcha-Authentication') {
                    script {
                        sh """
                          echo "📂 현재 디렉토리 위치:"
                          pwd

                          echo "📄 디렉토리 내 파일 목록:"
                          ls -al
                          
                          docker build -t \${DOCKER_REPO}/auth:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/auth:latest
                        """
                    }
                }
            }
        }

        stage('Build & Push Board') {
            steps {
                dir('MSA-Kitcha-Board') {
                    script {
                        sh """
                          docker build -t \${DOCKER_REPO}/board:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/board:latest
                        """
                    }
                }
            }
        }
        
        stage('Build & Push Article') {
            steps {
                dir('MSA-Kitcha-Article') {
                    script {
                        sh """
                          docker build -t \${DOCKER_REPO}/article:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/article:latest
                        """
                    }
                }
            }
        }

        stage('Build & Push FE') {
            steps {
                dir('MSA-Kitcha-FE') {
                    script {
                        sh """
                          docker build -t \${DOCKER_REPO}/frontend:latest .
                          echo \${REGISTRY_CREDENTIALS_PSW} | docker login -u \${REGISTRY_CREDENTIALS_USR} --password-stdin
                          docker push \${DOCKER_REPO}/frontend:latest
                        """
                    }
                }
            }
        }
    }
}
