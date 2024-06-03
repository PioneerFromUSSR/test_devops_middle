Задания по разработке, развертыванию и автоматизации веб-приложения на Python с использованием различных технологий
Задание 1: Разработка веб-сервера на Python
Цель: Написать простое веб-приложение на Python, которое будет запущено на порту 80 и отвечать статической страницей.
 
Задачи:
 
Создать базовое веб-приложение с использованием фреймворка Flask.
Приложение должно слушать порт 80 и отдавать HTML-страницу с приветственным текстом.
Задание 2: Упаковка приложения в Docker
Цель: Создать Dockerfile для упаковки Python приложения.
 
Задачи:
 
Написать Dockerfile, который будет включать все необходимые зависимости и запускать приложение.
Собрать образ и опубликовать его в публичном репозитории (например, Docker Hub).
Задание 3: Создание CI/CD пайплайна
Цель: Разработать пайплайн для полного цикла разработки: сборка, версионирование, тестирование (включая безопасность) и развертывание.
 
Задачи:
 
Использовать инструменты автоматизации (например, Jenkins, GitLab CI или GitHub Actions) для создания пайплайна.
Настроить процессы сборки, тестирования (включая проверку на уязвимости) и автоматического развертывания приложения.
Задание 4: Написание Ansible роли для развертывания приложения
Цель: Создать Ansible роль для развертывания веб-приложения на отдельном сервере.
 
Задачи:
 
Использовать Jinja для параметризации конфигураций приложения.
Настроить роль для развертывания Docker контейнера с приложением на целевом сервере.
Задание 5: Создание инфраструктуры с помощью Terraform
Цель: Использовать Terraform для развертывания экземпляров EC2 в AWS.
 
Задачи:
 
Создать конфигурацию Terraform, которая позволяет развертывать несколько экземпляров с разными параметрами (t2.medium, t2.large).
Использовать модуль flatten для генерации уникальных имен для каждого экземпляра.
Задание 6: Развертывание приложения на Kubernetes
Цель: Организовать развертывание приложения на Kubernetes.
 
Задачи:
 
Создать необходимые манифесты для деплоя приложения (Deployment, Service, Ingress).
Выбрать и настроить контроллер Ingress, объяснить выбор.
Настроить Application Load Balancers (ALBs) для работы с Kubernetes кластером.
Эти задания охватывают полный цикл разработки и развертывания веб-приложения, включая автоматизацию процессов и обеспечение гибкости и масштабируемости инфраструктуры.
