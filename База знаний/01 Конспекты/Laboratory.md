# Laboratory
  
https://dev.belapple.ru:7004/api/v2/journal_expertise/prepare/indicators.xlsx
```json
{
    "ids": [
        116,
        117,
        118,
        119,
        120,
        121,
        122,
        123,
        124,
        125
    ],
    "date_begin": null,
    "date_end": null,
    "filters": {
        "storage_uuid": null,
        "variety_uuid": null,
        "garden_uuid": null,
        "mark_uuid": null
    }
}
```

  
https://dev.belapple.ru:7004/api/v2/journal_expertise/prepare/acts.xlsx
Набор id документов
```json
{
    "ids": [
        116,
        119,
        121,
        122,
        123
    ]
}
```

Отправка веса бина
```ts
{  
    puid: string  
    sampling_qr_uuid: string | null  
    variety_uuid: string | null | undefined  
    sample_type: number | null  
    weight_sample: number  
}
```

//https://dev.belapple.ru:7004/api/v2/journal_expertise?date_begin=2026-08-02&date_end=2026-08-09&page=1&limit=10  
// Получение списка экспертиз
```ts
const expertiseList = {  
    "data": [  
        {  
            "id": 116,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 5,  
            "titratable_acidity": 0.2,  
            "date_time_sampling": "2026-03-18T06:07:18Z",  
            "weight_sample": 4.5,  
            "organoleptic_score": 9,  
            "hardness": 6.4,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": 26,  
            "streich_index": 3.76,  
            "act_uuid": "019cffae-ee0c-7528-b4d9-4a83d14dcbe0",  
            "note": "Общее примечание к экспертизе №116",  
            "puid": null  
        },  
        {  
            "id": 117,  
            "sampling_qr_uuid": "019b30e4-3bd6-726d-a60b-e7fe68620014",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": null,  
            "sample_type": 1,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T06:08:53Z",  
            "weight_sample": 2.5,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": null,  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 118,  
            "sampling_qr_uuid": "019b30e4-3bd6-726d-a60b-e7fe68620014",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": null,  
            "sample_type": 1,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T06:12:11Z",  
            "weight_sample": 1.89,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": null,  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 119,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 4,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T06:12:59Z",  
            "weight_sample": 2.69,  
            "organoleptic_score": null,  
            "hardness": 11,  
            "sugar_brix": 11,  
            "calibre": 11,  
            "weight": 11,  
            "vitreous": 3,  
            "ikp_score_5": 3,  
            "ikp_score_10": 9,  
            "sai": 11,  
            "streich_index": 0.33,  
            "act_uuid": "019cffae-ee48-7438-ba83-d8e2b148f571",  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 120,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 3,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T06:13:51Z",  
            "weight_sample": null,  
            "organoleptic_score": null,  
            "hardness": 0,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": 0,  
            "streich_index": 0,  
            "act_uuid": null,  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 121,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 2,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T06:15:45Z",  
            "weight_sample": 7.3,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": "019cffae-ee88-7519-87c9-55f4d33f35af",  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 122,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 3,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T07:59:37Z",  
            "weight_sample": 1.56,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": "019cfffa-c5a6-701e-86d7-43f9ef0aee2e",  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 123,  
            "sampling_qr_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": "019b2723-c0c3-7715-992f-8c286862000b",  
            "sample_type": 3,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T08:00:39Z",  
            "weight_sample": 1.568,  
            "organoleptic_score": null,  
            "hardness": 10.5,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": 0,  
            "streich_index": 10.5,  
            "act_uuid": "019cfffa-c5e8-7dbb-86aa-f17f3377fcf2",  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 124,  
            "sampling_qr_uuid": "019b30e4-3bd6-726d-a60b-e7fe68620014",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": null,  
            "sample_type": 1,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T08:23:14Z",  
            "weight_sample": 2.589,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": null,  
            "note": null,  
            "puid": null  
        },  
        {  
            "id": 125,  
            "sampling_qr_uuid": "019b30e4-3bd6-726d-a60b-e7fe68620014",  
            "variety_uuid": "019b36f1-a817-7948-98fc-d12f68620002",  
            "mark_uuid": null,  
            "garden_uuid": null,  
            "storage_uuid": null,  
            "sample_type": 1,  
            "titratable_acidity": null,  
            "date_time_sampling": "2026-03-18T08:23:39Z",  
            "weight_sample": 2.357,  
            "organoleptic_score": null,  
            "hardness": null,  
            "sugar_brix": null,  
            "calibre": null,  
            "weight": null,  
            "vitreous": null,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "sai": null,  
            "streich_index": null,  
            "act_uuid": null,  
            "note": null,  
            "puid": null  
        }  
    ],  
    "meta": {  
        "current_page": 1,  
        "total_pages": 6,  
        "total_records": 51,  
        "filters": {  
            "variety_arr": [  
                "019b36f1-a818-719a-bdf7-88f468620002",  
                "019b36f1-a817-7948-98fc-d12f68620002"  
            ],  
            "storage_arr": [  
                "019b2723-c0c3-7715-992f-8c286862000b"  
            ],  
            "garden_arr": [],  
            "mark_arr": []  
        }    }  
}
```

//https://dev.belapple.ru:7004/api/v2/expertise_details?journal_id=116  
// Получение деталей по экпертизе
```ts
[  
    {  
        "id": 45,  
        "journal_id": 116,  
        "hardness": 4,  
        "dot_1": 1,  
        "dot_2": null,  
        "dot_3": 7,  
        "sugar_brix": 13.3,  
        "ikp_score_5": 9,  
        "ikp_score_10": 11,  
        "calibre": 920,  
        "streich_index": 0.03,  
        "weight": 256,  
        "sai": 67,  
        "vitreous": 0,  
        "note": "Примечание к экспертизе яблока №1"  
    },  
    {  
        "id": 62,  
        "journal_id": 116,  
        "hardness": 14.7,  
        "dot_1": 12,  
        "dot_2": 21,  
        "dot_3": 11,  
        "sugar_brix": null,  
        "ikp_score_5": null,  
        "ikp_score_10": null,  
        "calibre": null,  
        "streich_index": 14.67,  
        "weight": null,  
        "sai": 0,  
        "vitreous": null,  
        "note": null  
    },  
    {  
        "id": 63,  
        "journal_id": 116,  
        "hardness": 7,  
        "dot_1": 7,  
        "dot_2": 7,  
        "dot_3": 7,  
        "sugar_brix": 7,  
        "ikp_score_5": 3,  
        "ikp_score_10": 7,  
        "calibre": 7,  
        "streich_index": 0.33,  
        "weight": 7,  
        "sai": 35,  
        "vitreous": null,  
        "note": null  
    },  
    {  
        "id": 67,  
        "journal_id": 116,  
        "hardness": 0,  
        "dot_1": null,  
        "dot_2": null,  
        "dot_3": null,  
        "sugar_brix": null,  
        "ikp_score_5": null,  
        "ikp_score_10": null,  
        "calibre": null,  
        "streich_index": 0,  
        "weight": null,  
        "sai": 0,  
        "vitreous": null,  
        "note": null  
    }  
]
```

//https://dev.belapple.ru:7004/api/v2/journal_expertise/116  
Отправка изменения экспертизы 
На верхнем уровне отправляем комментарий к экспертизе и основную экспертизу
В details добавляем expertiseDetails, значения, которые меняем и тип изменений, в delete только id
```json
const patchExpertiseDelails = {  
    "puid": "019fe69a-7c5c-74e5-9ffe-db1459fb87c4",  
    "titratable_acidity": 0.2,  
    "organoleptic_score": 9,  
    "weight_sample": 4.5,  
    "note": "Общее примечание к экспертизе №116",  
    "details": {  
        "post": [{  
            "sai": 20,  
            "streich_index": null,  
            "titrated_acidity": 0.2,  
            "hardness": 2,  
            "dot_1": 1,  
            "dot_2": 2,  
            "dot_3": 3,  
            "sugar_brix": 4,  
            "calibre": null,  
            "weight": null,  
            "vitreous": 1,  
            "ikp_score_5": null,  
            "ikp_score_10": null,  
            "note": null,  
            "journal_id": 116,  
            "edit": true  
        }],  
        "patch": [  
            {  
                "id": 45,  
                "journal_id": 116,  
                "hardness": 3.3,  
                "dot_1": 1,  
                "dot_2": 2,  
                "dot_3": 7,  
                "sugar_brix": 13.3,  
                "ikp_score_5": 9,  
                "ikp_score_10": 11,  
                "calibre": 920,  
                "streich_index": 0.03,  
                "weight": 256,  
                "sai": 67,  
                "vitreous": 0,  
                "note": "Примечание к экспертизе яблока №1",  
                "edit": true  
            }  
        ],  
        "delete": [62]  
    }  
}
```

