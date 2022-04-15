# Сервис локаций

Ответственность: создание, изменение,просмотр и удаление записи об аудиториях и прочих помещениях Университета

## Сценарий использования

![image](https://user-images.githubusercontent.com/49455695/163052384-5c24193e-b9ce-46af-a84e-52163810835b.png)

## Пользовательские истории

Как Организатор я хочу изменить место _моего_ мероприятия

Как Участник я хочу знать когда проводится такое-то мероприятия использующие оборудование

Как Руководитель я оцениваю загруженность помещений по времени

## Модель данных
![image](https://user-images.githubusercontent.com/49455695/163052336-ca81e223-d4ac-46a0-91e2-69d4b9202e9a.png)
```sql
create database IF NOT EXISTS location_db;

use location_db;

create table times(
	id INT NOT NULL AUTO_INCREMENT,
    time_start datetime NOT NULL,
    time_end datetime not null,
    CONSTRAINT time_id_pk PRIMARY KEY (id)
);

create table equipment(
	id INT NOT NULL AUTO_INCREMENT,
    name varchar(20) not null,
    description varchar(20),
    conditions  varchar(25),
    CONSTRAINT pet_id_pk PRIMARY KEY (id)
);

create table location(
	id INT NOT NULL AUTO_INCREMENT,
    id_time int not null,
    id_equipment int not null,
    name varchar(25) NOT NULL,
    description varchar(25) not null,
  
    CONSTRAINT person_id_pk PRIMARY KEY (id),
    CONSTRAINT  id_time_uq UNIQUE(id_time),
    FOREIGN KEY (id_time)  REFERENCES location_db.times(id),
    FOREIGN KEY (id_equipment)  REFERENCES location_db.equipment(id)
    
);
```
## API сервиса

get /api/location </br>
get /api/location/{id}</br>
delete /api/location/{id}</br>
post /api/location</br>
``` json
{
    "name": "Актовый зал",
    "description": "Хороший",
    "busyId": {
        "timeStart": "2022-04-06 18:00:00",
        "timeEnd": "2022-04-06 20:00:00"
    },
    "equipment":{
        "id": 5
    }
}
```
