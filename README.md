# Домашнее задание к занятию «Управляющие конструкции в коде Terraform» Макаров Денис

### Цели задания

1. Отработать основные принципы и методы работы с управляющими конструкциями Terraform.
2. Освоить работу с шаблонизатором Terraform (Interpolation Syntax).

------

### Чек-лист готовности к домашнему заданию

1. Зарегистрирован аккаунт в Yandex Cloud. Использован промокод на грант.
2. Установлен инструмент Yandex CLI.
3. Доступен исходный код для выполнения задания в директории [**03/src**](https://github.com/netology-code/ter-homeworks/tree/main/03/src).
4. Любые ВМ, использованные при выполнении задания, должны быть прерываемыми, для экономии средств.

------

### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
Убедитесь что ваша версия **Terraform** ~>1.8.4
Теперь пишем красивый код, хардкод значения не допустимы!
------

### Задание 1

1. Изучите проект.
2. Заполните файл personal.auto.tfvars.
3. Инициализируйте проект, выполните код. Он выполнится, даже если доступа к preview нет.

Примечание. Если у вас не активирован preview-доступ к функционалу «Группы безопасности» в Yandex Cloud, запросите доступ у поддержки облачного провайдера. Обычно его выдают в течение 24-х часов.

Приложите скриншот входящих правил «Группы безопасности» в ЛК Yandex Cloud или скриншот отказа в предоставлении доступа к preview-версии.

### Решение:

1.Изучил проект.

2.Заполнил файл personal.auto.tfvars.

3.Инициализировал проект, выполнил код.

Скриншот входящих правил «Группы безопасности» в ЛК Yandex Cloud представлен на скриншоте ниже:

![группы](https://github.com/user-attachments/assets/90063832-7488-4ec7-a0f9-2553d0413159)


------

### Задание 2

1. Создайте файл count-vm.tf. Опишите в нём создание двух **одинаковых** ВМ  web-1 и web-2 (не web-0 и web-1) с минимальными параметрами, используя мета-аргумент **count loop**. Назначьте ВМ созданную в первом задании группу безопасности.(как это сделать узнайте в документации провайдера yandex/compute_instance )
2. Создайте файл for_each-vm.tf. Опишите в нём создание двух ВМ для баз данных с именами "main" и "replica" **разных** по cpu/ram/disk_volume , используя мета-аргумент **for_each loop**. Используйте для обеих ВМ одну общую переменную типа:
```
variable "each_vm" {
  type = list(object({  vm_name=string, cpu=number, ram=number, disk_volume=number }))
}
```  
При желании внесите в переменную все возможные параметры.
4. ВМ из пункта 2.1 должны создаваться после создания ВМ из пункта 2.2.
5. Используйте функцию file в local-переменной для считывания ключа ~/.ssh/id_rsa.pub и его последующего использования в блоке metadata, взятому из ДЗ 2.
6. Инициализируйте проект, выполните код.

### Решение:

1. Создал файл count-vm.tf и описал в нем 2 одинаковые виртуальные машины, которые будут называться web-1 и web-2:

![создание машин](https://github.com/user-attachments/assets/48d98299-8e20-496d-ba04-3373de718af8)

Назначил виртуальной машине созданную в первом задании группу безопасности:

![безопасность](https://github.com/user-attachments/assets/30b51c98-5f74-4842-a590-98d722cf63ce)

2. Создал файл for_each-vm.tf. В нем описал создание двух ВМ с именами "main" и "replica" разных по cpu/ram/disk , используя мета-аргумент for_each loop:

![for_each](https://github.com/user-attachments/assets/c70bc0be-7090-4928-a385-a9937234ce83)

3. ВМ с именами "main" и "replica" создаются после создания ВМ web-1 и web-2:

![vm](https://github.com/user-attachments/assets/0f104afd-fa4f-497f-8df1-b07ba922a3dd)

4. Для считывания файла ключа использую local-переменную и использую ее в блоке metadata:

![locals](https://github.com/user-attachments/assets/389ec0a2-fcf9-4475-a52b-f4f369771afc)

![metadata](https://github.com/user-attachments/assets/3abdfad7-9240-402b-9e02-9b77ebca4348)

5. Инициализировал проект, выполнил код. Создалось 7 объектов - сеть, подсеть, группа безопасности и 4 виртуальные машины:

На данном скриншоте представлено 5 виртуальных машин, так как делал скриншоты после выполнения всего задания.

![vm_oblako](https://github.com/user-attachments/assets/7fe791b9-096e-4545-a73a-61e80755c33e)

------

### Задание 3

1. Создайте 3 одинаковых виртуальных диска размером 1 Гб с помощью ресурса yandex_compute_disk и мета-аргумента count в файле **disk_vm.tf** .
2. Создайте в том же файле **одиночную**(использовать count или for_each запрещено из-за задания №4) ВМ c именем "storage"  . Используйте блок **dynamic secondary_disk{..}** и мета-аргумент for_each для подключения созданных вами дополнительных дисков.

### Решение:

1. Создал 3 одинаковых диска:

![disk](https://github.com/user-attachments/assets/614e3534-9d68-47c6-b3e9-eb15c2f70a63)

2. Создал виртуальную машину storage и используя мета-аргумент for_each подключил к ней созданные диски:

![vm storage](https://github.com/user-attachments/assets/407c97ad-095e-4514-b0eb-5d406ddef8f3)

![disk oblako](https://github.com/user-attachments/assets/ac78f2f8-67e2-4280-addb-856894e4e943)

------

### Задание 4

1. В файле ansible.tf создайте inventory-файл для ansible.
Используйте функцию tepmplatefile и файл-шаблон для создания ansible inventory-файла из лекции.
Готовый код возьмите из демонстрации к лекции [**demonstration2**](https://github.com/netology-code/ter-homeworks/tree/main/03/demo).
Передайте в него в качестве переменных группы виртуальных машин из задания 2.1, 2.2 и 3.2, т. е. 5 ВМ.
2. Инвентарь должен содержать 3 группы и быть динамическим, т. е. обработать как группу из 2-х ВМ, так и 999 ВМ.
3. Добавьте в инвентарь переменную  [**fqdn**](https://cloud.yandex.ru/docs/compute/concepts/network#hostname).
``` 
[webservers]
web-1 ansible_host=<внешний ip-адрес> fqdn=<полное доменное имя виртуальной машины>
web-2 ansible_host=<внешний ip-адрес> fqdn=<полное доменное имя виртуальной машины>

[databases]
main ansible_host=<внешний ip-адрес> fqdn=<полное доменное имя виртуальной машины>
replica ansible_host<внешний ip-адрес> fqdn=<полное доменное имя виртуальной машины>

[storage]
storage ansible_host=<внешний ip-адрес> fqdn=<полное доменное имя виртуальной машины>
```
Пример fqdn: ```web1.ru-central1.internal```(в случае указания имени ВМ); ```fhm8k1oojmm5lie8i22a.auto.internal```(в случае автоматической генерации имени ВМ зона изменяется). нужную вам переменную найдите в документации провайдера или terraform console.
4. Выполните код. Приложите скриншот получившегося файла. 

Для общего зачёта создайте в вашем GitHub-репозитории новую ветку terraform-03. Закоммитьте в эту ветку свой финальный код проекта, пришлите ссылку на коммит.   
**Удалите все созданные ресурсы**.

### Решение:

1. Создал файл ansible.tf, по примеру из лекции написал код с использованием функции tepmplatefile:

![ansible](https://github.com/user-attachments/assets/edcba96a-476e-47cd-b843-307b36c472a0)

Шаблон инвентари файла был использован из лекции.

2. Инвентари файл получился с 3 группами.

Результат выполнения представлен на скриншоте ниже:

![host](https://github.com/user-attachments/assets/a10bcfac-9762-4a66-8e0f-2a741d6ffeed)

------



