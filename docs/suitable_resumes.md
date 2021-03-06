# Список подходящих для отклика резюме

Для того, чтобы определить, каким из своих резюме пользователь может откликнуться на вакансию c идентификатором `vacancy_id`, 
необходимо отправить запрос `GET` на `/vacancies/{vacancy_id}/suitable_resumes`.

В случае успеха придёт ответ со статусом HTTP `200 OK`, содержащий список сокращенных представлений резюме пользователя, 
которыми возможно откликнуться на данную вакансию:

```json
{
  "found": 1,
  "per_page": 1,
  "page": 1,
  "pages": 1,
  "items": [
      {
          "id": "14831542000d1f366b4c5a6a751b329b70039e",
          "title": "Дизайнер резюме",
          "url": "https://api.hh.ru/resumes/14831542000d1f366b4c5a6a751b329b70039e",
          "created_at": "2013-11-03T00:43:20+0400",
          "updated_at": "2013-11-22T12:25:18+0400",
          "alternate_url": "https://hh.ru/resume/14831542000d1f366b4c5a6a751b329b70039e",
          "access": {
                "type": {
                    "id": "clients",
                    "name": "видно всем компаниям, зарегистрированным на HeadHunter"
                }
            },
            "status": {
                "id": "published",
                "name": "опубликовано"
            },
            "first_name": "Иван",
            "last_name": "Иванов",
            "middle_name": "Иванович",
            "age": 19,
            "area": {
                "id": "1",
                "name": "Москва",
                "url": "https://api.hh.ru/areas/1"
            },
            "certificate": [
                {
                    "achieved_at": "2015-01-01",
                    "owner": null,
                    "title": "тест",
                    "type": "custom",
                    "url": "http://example.com/"
                }
            ],
            "education": {
                "primary": [
                    {
                        "name": "Российский государственный социальный университет, Москва",
                        "name_id": "39420",
                        "organization": "Факультет информационных технологий",
                        "organization_id": null,
                        "result": "Информатика",
                        "result_id": null,
                        "year": 2012
                    }
                ]
            },
            "total_experience": {
                "months": 118
            },
            "experience": [
                {
                    "position": "пастух",
                    "start": "2010-01-01",
                    "end": null,
                    "company": "Рога и копыта",
                    "industries": [
                        {
                            "id": "51.643",
                            "name": "Благоустройство и уборка территорий и зданий"
                        },
                        {
                            "id": "29.503",
                            "name": "Земледелие, растениеводство, животноводство"
                        }
                    ],
                    "company_url": "http://example.com/",
                    "area": {
                        "id": "1",
                        "name": "Москва",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "company_id": null,
                    "employer": null
                },
                {
                    "start": "2005-01-01",
                    "end": "2009-03-01",
                    "company": "HeadHunter",
                    "area": {
                        "id": "1",
                        "name": "Москва",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "industries": [
                        {
                            "id": "7.513",
                            "name": "Интернет-компания (поисковики, платежные системы, соц.сети, информационно-познавательные и развлекательные ресурсы, продвижение сайтов и прочее)"
                        }
                    ],
                    "company_url": "https://hh.ru",
                    "company_id": "1455",
                    "employer": {
                        "alternate_url": "https://hh.ru/employer/1455",
                        "id": "1455",
                        "logo_urls": {
                            "90": "https://hh.ru/employer/logo/1455"
                        },
                        "name": "HeadHunter",
                        "url": "https://api.hh.ru/employers/1455"
                    }
                }
            ],
            "gender": {
                "id": "male",
                "name": "Мужской"
            },
            "salary": {
                "amount": 1000000,
                "currency": "RUR"
            },
            "photo": {
                "medium": "https://hh.ru/...",
                "small": "https://hh.ru/...",
                "id": "1337"
            },
            "negotiations_history": {
                "url": "https://api.hh.ru/resumes/14831542000d1f366b4c5a6a751b329b70039e/negotiations_history"
            }
        }
    ],
    "overall": {
        "not_published": 0,
        "already_applied": 0,
        "unavailable": 0    
    }
}
```

 имя | тип | значение
 --- | --- | ---
 id | строка | Идентификатор резюме
 title | строка | Желаемая должность
 created_at | строка | Дата и время создания резюме
 updated_at | строка | Дата и время последнего обновления резюме
 url | строка | Ссылка на данное резюме в api
 alternate_url | строка | Ссылка на данное резюме на сайте

Остальные поля сокращенного представления резюме аналогичны [полям при редактировании](resumes.md#resume-keys).

При пустом списке невозможно понять, есть ли у пользователя резюме, но они все не подходят, или же их нет. Для этого выдаётся 
дополнительная информация в ключе `overall`:

ключ | значение
--- | ---
not_published | количество неопубликованных резюме пользователя
already_applied | количество резюме, которыми пользователь уже откликался на эту вакансию
unavailable | количество резюме пользователей, которыми по другим причинам невозможно откликнуться (конфликтующие настройки видимости резюме и т.п.)

Запрос возможно выполнить только соискателем, для других типов авторизации будет возвращен HTTP статус `403 Forbidden`.
