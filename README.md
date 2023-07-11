# Домашнее задание к занятию «Хранение в K8s. Часть 2»

### Цель задания

В тестовой среде Kubernetes нужно создать PV и продемострировать запись и хранение файлов.

### Задание 1

**Что нужно сделать**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 
4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

### Задание 2

**Что нужно сделать**

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

## Ответ:

### Задание 1

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.

2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/01ef18dc-339b-4e57-a830-075281cc51aa)

3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/d2d70265-7816-4fa2-8236-b8bbc6fa63b9)

4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/cfd5e328-3152-493e-b3ef-de3350aec7a5)
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/ee639e8f-5ea8-4a5e-896f-41449703c808)

PV сохранился, но находится в состоянии Released. Политика возврата Retain позволяет вручную высвобождать ресурс. Когда файл PersistentVolumeClaim удаляется, то PersistentVolumeвсе еще существует, и том считается «освобожденным»(Released). Но он пока недоступен для другого требования, поскольку данные предыдущего заявителя остаются на томе.

5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
   
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/c36c9a7a-975a-4582-8701-88e14ba184f0)

Файл остался, так как ReclaimPolicy: Retain сохраняет файлы после удаления pv.

6. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

[task1.yaml](https://github.com/askarpoff/kuber_ex7/blob/main/task1.yaml)

------

### Задание 2

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
   
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/231bd7e7-09be-4ded-a5da-c195a1078068)
  
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
![image](https://github.com/askarpoff/kuber_ex7/assets/108946489/6ee796b6-4fb3-48e9-8300-dbfde6d56cb2)

  
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.
   
[task2.yaml](https://github.com/askarpoff/kuber_ex7/blob/main/task2.yaml)

[sc2.yaml](https://github.com/askarpoff/kuber_ex7/blob/main/sc2.yaml)
