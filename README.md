# EXAM (SINAV) UYGULAMASI

Son kullanıcının uygulamaya girip soruları cevapladığı ve cevapları gönderdikten sonra sonuç ekranında durumunu gördüğü bir uygulama. 
Mevcut HTML çalışan örnek uygulama için [tıklayın](https://www.mindset.com.tr/deneme)

## TASARIM
- Zeplin uygulamasında tüm ekranların tasarımlarını görebilirsiniz. Davet için [tıklayın](https://zpl.io/Md7qPxJ)
- Bu uygulama için öncelik HTML ve CSS olarak tasarım birebir aynısının olması değil. Genel yapının benzemesi yeterli, daha çok ReactJs tarafı bizim için öncelikli. Ancak tasarımı birebir yapabilirseniz bu artı bir değer.

## İŞ AKIŞI
- Kullanıcı uygulama linkine giriş yapar. 
- İstenilen bilgileri doldurur ve sınava başlar.
- Sorular ekrana sırayla gelir. Sorulara cevap verebilir, soruyu geçebilir, önceki soruya dönebilir. 
- 3 Farklı soru tipi var. 
-- Radio btn : Birden fazla seçenek olacak(seçenek sayısı değişken) ve kullanıcı birini seçebilir.
-- Check btn : Birden fazla seçenek olacak(seçenek sayısı değişken) ve kullanıcı birden fazla seçebilir.
-- Text : Text olarak cevap yazabilir.
- Soruların ilerlemesi bir loading bar şeklinde gösterilmeli ve soru ilerledikçe bu bar güncellenmeli. Kaçıncı soruda olduğu ve sınavı bitirmesine ne kadar kaldığı belli olmalı.
- Kullanıcı sınavı istediği zaman bitirebilir.
- Sınav bittikten sonra dönen mesaj son kullanıcıya gösterilir.
- Sınav başladığında toplam bir süre belirtilmiş ise kullanıcıya bu süre gösterilmeli ve zamanlayıcı ile sürekli ekranda azalmalı. 
- Süre bitiminde sınav otomatik tamamlanmalı ve sonuç ekranına yönlendirilmeli.

## ADIMLAR ve API İSTEKLERİ
### 1. ADIM
Kullanıcı uygulamaya girince kullanıcı bilgileri almak için bir form açılır. Form içerisinde alınacak bilgiler aşağıdaki gibi;
#### from inputs
- > `customer_name` *zorunlu
- > `customer_email` *zorunlu
- > `customer_phone` *zorunlu
- > `customer_position`
- > `customer_sector`
- > `exam` *zorunlu

Bu değerler gönderilmeden kontrol edilmeli ve gereken uyarılar ekranda gösterilmeli.

### 2. ADIM	
Form değerleri POST istegi ile gönderilir ve kullanıcıya ait oturum başlatılır.

Örnek istek(POST): 
```html
http://bootcamp.com.tr/public/api/examcustomer?customer=&customer_name=Deneme Deneme&customer_email=deneme@deneme.com&customer_phone=05555555555&customer_position=Pozisyon&customer_sector=Sektör 1&exam=eyJpdiI6ImM1UzJwOHZqUFJORW5ucEdGcHNjbWc9PSIsInZhbHVlIjoiK1ZWN2VYQmtXc0k1enlMZ21Pa0VQUT09IiwibWFjIjoiNDI0NGEwMmMwYWFhNjIyYWNiYmMxYjQ1NmNhYmQ0MjEyMWE1NzgzNWI4NmNjNjM1NGU5YWUwMDA4YzE3OTU0NyIsInRhZyI6IiJ9
```


### 3. ADIM
Kullanıcı oturumu başladıktan sonra dönen sonuç içinde sınav detayları alınır ve sorular gösterilmeye başlar. 
Oturum detaylarını erişebilmek için dönen cevap içindeki `cid` değeri ile GET isteğinde bulunabilirsiniz.
Örnek istek (GET): 
```html
http://bootcamp.com.tr/public/api/examcustomer/eyJpdiI6IlNteGZpU1JmVXZyMWtWL1g3VmRJNGc9PSIsInZhbHVlIjoid2phSlJSaVo3c1pIZ3NLRjE3NnovUT09IiwibWFjIjoiYjhkNzM3ZmM2NzMxYjM1OWYyNWI5MTMwY2VmODU5ZTU5OTQ0YmQ4NWQ4ZjZlYzZmOWRhYzdjMzBjOWE4NDA0MiIsInRhZyI6IiJ
```

Dönen örnek cevap:
```json
{
    "status": "ok",
    "message": "",
    "data": [
        {
            "question_count": 0,
            "correct_count": 0,
            "wrong_count": 0,
            "blank_count": 0,
            "total_point": 0,
            "total_time": 0,
            "status": 1,
            "cid": "eyJpdiI6Ikw0U2dIc1hNamxKWjNTQkJ6NFBkUXc9PSIsInZhbHVlIjoieVluQTRTVzF5VVVnYWRiQWtLVVNIQT09IiwibWFjIjoiZTQwMzc0ZDY1MDcyMzU5ZjY5MTU3OTIxYzM1NmZiMTBkODMzMGI3MWRlM2ZhMzEyOWJjZTAxODQxN2VhZGQ4OCIsInRhZyI6IiJ9",
            "exam": {
                "name": "Sınav 1",
                "description": "sınav 1 açıklama",
                "time": 1000,
                "rating_type": 1,
                "status": 1,
                "cid": "eyJpdiI6IjdZcExPZEw0RUZpblVMZDR2OCtVSkE9PSIsInZhbHVlIjoiZ0lIZWpDdEpERHNENmZySjlwUjd5Zz09IiwibWFjIjoiZDI4OGYwMmRmYWY2OWJhYmRkNzk0YmU1ZDZmZjE5Y2JmNzBjOWM5YjU2YmViZmM5NjkwNWIzMjA2MGJlY2Q1MCIsInRhZyI6IiJ9"
            },
            "questions": [
                {
                    "id": 1,
                    "type": 1,
                    "point": 25,
                    "orderby": 1,
                    "question": "Soru 1",
                    "description": "Soru açıklama",
                    "required": 2,
                    "status": 1,
                    "cid": "eyJpdiI6IlNEQ1VCd3J1dkZndFFHVEJMNHdnb1E9PSIsInZhbHVlIjoiVVpNajBFaS9vZ1BDUjZqSHdxOU8wUT09IiwibWFjIjoiMDEyNmRmOWJhMzJmZDE5Y2VhZGQ5OWVkYjU1MzcyYzVlZGIyNzI3OGY4MThkYTkwZWM4ZGIxMzNkMDhkZDM3ZiIsInRhZyI6IiJ9",
                    "options": [
                        {
                            "id": 1,
                            "orderby": 1,
                            "option": "Cevap 1.1",
                            "correct_status": 1,
                            "status": 1,
                            "cid": "eyJpdiI6ImhlQnR4RE16SFlZMmIyWmlCRzF2WkE9PSIsInZhbHVlIjoicU40dXQveGttaXZCRzBJUXdRL0VGQT09IiwibWFjIjoiZTZlMTM2MGJlNjQ1YzFkNDcwZWI3ZTI3YTdlMzkwOTFiMDllNGUyOWQyMjAyYTA2YTE4OTRkZTk0YTFjYzFmNiIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 2,
                            "orderby": 2,
                            "option": "Cevap 1.2",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6InFBeGF1aDRQU2dhcUtxajNlZDRWZUE9PSIsInZhbHVlIjoiWStyd293OVkrVFdtNVI2VndZS01CUT09IiwibWFjIjoiYmRlMzk1YTBhOTNmMmM0Yjk2MDk1NmM1MzJiNjc1MjFhMmYxZmMyZTAwNTgyMmFjNDU5MDgzODkzMTA3ZDE4NSIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 3,
                            "orderby": 3,
                            "option": "Cevap 1.3",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6IlprdUZkK0VPVHRjWGx2MUJ4NVVJdmc9PSIsInZhbHVlIjoidFNQcVhrSUw1WGlyNlg2dGFwYTI2QT09IiwibWFjIjoiZmFmYmVjMjE1NDVmNjliOWJhMGYxZmM1OGM0NjE0YTRmNGY0NzBkMDE2NzliM2MyNjM1ZTFjMDc3MzkzNWY0ZCIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 4,
                            "orderby": 4,
                            "option": "Cevap 1.4",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6IlZubXp3NGRqM0MwOGJzcWZaRWxNVGc9PSIsInZhbHVlIjoieGN3TGdJcHhoRk1oVDNyMnd4MndhZz09IiwibWFjIjoiNTdjNTI1ZTBjN2E2Y2FlODMwODZjOTJiNmM2NDk4MWFkNzk2YTNjMzFmMWJlMGFlMzY3M2UzNjYzYmE3MjNjNCIsInRhZyI6IiJ9"
                        }
                    ]
                },
                {
                    "id": 2,
                    "type": 2,
                    "point": 25,
                    "orderby": 2,
                    "question": "Soru 2",
                    "description": "",
                    "required": 2,
                    "status": 1,
                    "cid": "eyJpdiI6Im4rcUZWM1V2VDhlYWVHbk1FMlh2L0E9PSIsInZhbHVlIjoiZWFQSWdsVWl3M2FzQW4xQytnNGdKUT09IiwibWFjIjoiMzAwY2VkNWM0OWQxMTJmMjc5NTgwNzY5Njk0ZGIxZmNjZTA3MWIwNmY1Mzc0ZmQ1YjE4Mjk2YWNkYjRjZWM5MyIsInRhZyI6IiJ9",
                    "options": [
                        {
                            "id": 5,
                            "orderby": 1,
                            "option": "Cevap 2.1",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6ImNPVG5DTDY3TFFwMXkrcDJpMklrYlE9PSIsInZhbHVlIjoiY0hveHR2RDFaSmNxSjJTVFhYZEdnZz09IiwibWFjIjoiMWQ1NWEwYWNhMjRjMjcxMzMzM2NmNTM5MWQyOTJhMTA3NGEzYmFlZDQwZjJmNWQ0NDQyOTEzZjU5OGE2NmE3NyIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 6,
                            "orderby": 2,
                            "option": "Cevap 2.2",
                            "correct_status": 1,
                            "status": 1,
                            "cid": "eyJpdiI6Ijc1cmFxanBVdmVLZjZ5M1VOMGlKZXc9PSIsInZhbHVlIjoibUpBQVVseXdoTnVtdzVUR29CTmkrZz09IiwibWFjIjoiMzQwMjkxMzZlYzU1YmM3Njg3Y2I2YjZhZWY3M2MzMDg3YTM3YWQzMDg3ZjBmYTFiMzVjZDJhMjc0YzgzNDc2YiIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 7,
                            "orderby": 3,
                            "option": "Cevap 2.3",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6InA3dkNlYmY2TzVIYkFCQmF0dzVOWnc9PSIsInZhbHVlIjoia2VaNmVUdG5MTHNNSUx6eFBhWVpoZz09IiwibWFjIjoiOGJjNjc4ZWY2NjQ0MjhhYTk0YjM1NDE2NjczZjZlODU4NWIwYWNkNTBkNzI2OTJkYTQ3OWUwOWNiYzdjMDQ2MiIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 8,
                            "orderby": 4,
                            "option": "Cevap 2.4",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6IkRWclpINEdPOS9ZUytoVW4zeVJWRnc9PSIsInZhbHVlIjoiN3BIRENiNThtUmR2WVdPNXhBZHN4dz09IiwibWFjIjoiMjI2ZmI5YTA2MTAzMWU4NGRhZGUyMDA4MDZmMTczNWVmYzA1NmI4YjY1MzIzOTdjOTAxMjE1YzY2MjMwNTE5MCIsInRhZyI6IiJ9"
                        }
                    ]
                },
                {
                    "id": 3,
                    "type": 1,
                    "point": 25,
                    "orderby": 3,
                    "question": "Soru 3",
                    "description": "",
                    "required": 2,
                    "status": 1,
                    "cid": "eyJpdiI6Ijd3dmlOYWNPd05qZWx4N0NIelo3SXc9PSIsInZhbHVlIjoibng2cWRxUUF3M21uQ3U1Q0JaVDJRZz09IiwibWFjIjoiNDdhM2ZkOGVjY2ZiMzdiYmU5ODk4NTM3MTU2ODc4MzBiNDMwN2YwY2JlODk2ZWU5NzY0ZTJhY2Q2ODhiODExMSIsInRhZyI6IiJ9",
                    "options": [
                        {
                            "id": 9,
                            "orderby": 1,
                            "option": "Cevap 3.1",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6Im1vVmgzTFVIbnB5Myswa0hHK2JzN2c9PSIsInZhbHVlIjoiUHFkV0lMMWlPa3E3RWhPTFJLMm45UT09IiwibWFjIjoiZjJjY2I0ODhkODUwOGMwYmJkNDZhNDIzMDUxZmNiNDJlMTU4MDA2ZmNmZmEyNmE3OWIyNTMwODFkMDEzZmQ2NyIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 10,
                            "orderby": 2,
                            "option": "Cevap 3.2",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6IkF4MFo5bTlmcGdXeGw2QkpqSEs5UVE9PSIsInZhbHVlIjoiODdhTnlwUEhpZnkzUjk5RGw0WFZ6QT09IiwibWFjIjoiOGZkZTE0OTU3NDM4NDlmNWZiOTI4YTQ0ZDAwMGY4YWY3MTU4Y2QwNzk4NjM4MDdkYzkwZTQwMmQyMTcwZDdiNyIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 11,
                            "orderby": 3,
                            "option": "Cevap 3.3",
                            "correct_status": 1,
                            "status": 1,
                            "cid": "eyJpdiI6IkdTOXVEbVBlQjFoWlJ2akREbjhCYkE9PSIsInZhbHVlIjoibkhTYVROd3R6SWxQRnlqcGl2ZDBYdz09IiwibWFjIjoiZjQ5YWEyNmRhNmY5MTM4Yzc5MjdlNThhYTQ3OWU5MTI0ZGE0ZDkyZDNjM2ZiYjk2M2MxNjdhYWI0YWIzYzJhZSIsInRhZyI6IiJ9"
                        },
                        {
                            "id": 12,
                            "orderby": 4,
                            "option": "Cevap 3.4",
                            "correct_status": 2,
                            "status": 1,
                            "cid": "eyJpdiI6Ik9FRFF5L29KWWhVOC83di9WYVcycVE9PSIsInZhbHVlIjoiVEtqcGoyd2IrRVpra01IQUE0ejEwdz09IiwibWFjIjoiMWRjNTk0Y2U0YjdiYjQ2Zjg3YmIxYTYwODQ0YTYwZDU4YjJlYTRmNzhiMDQyOGNiNmY0OGMyYTIzNWYwNWE2MCIsInRhZyI6IiJ9"
                        }
                    ]
                },
                {
                    "id": 4,
                    "type": 3,
                    "point": 25,
                    "orderby": 4,
                    "question": "Soru 4",
                    "description": "Açıklama",
                    "required": 1,
                    "status": 1,
                    "cid": "eyJpdiI6IkJGMDVYQVFVZlBOOWhERkllWUUyUVE9PSIsInZhbHVlIjoiWWt3U09XS2ZqWWc5WUtNcHBUUHlBQT09IiwibWFjIjoiNDc0ZWVmOWIwYTIwZWNkOWFhYjFmNmJlMGI5YTM0NzM3ZWFiYmJhN2NmZmIwN2ViY2IwY2ZjNTI1MzhhMTBiYyIsInRhZyI6IiJ9",
                    "options": []
                }
            ]
        }
    ],
    "http_code": 200
}
```


### 4.ADIM
Sınav bitir ile birlikte soruların cevapları dizi olarak POST edilir. 2. Adımda dönen `cid` değeri PUT isteğinin sonunda gönderilmeli.
Örnek istek(PUT): 
```html
http://bootcamp.com.tr/public/api/examcustomer/eyJpdiI6IkhmVFR6K3NIQ3F6eHlHMHZQQWlTZmc9PSIsInZhbHVlIjoiSTVKRHBwZWhoZkZuQTQvMjd4Q3FNQT09IiwibWFjIjoiMmE3Y2MxYWYzMGUzNTliMzgyYzk0NjgxMGViMDZkNjBhMjBmOWY4NTI4MTM5OTJkZDExMzA5ZjRhMDNlNjAwNyIsInRhZyI6IiJ9
```
PUT edilecek örnek data;
```json
{
    "answers":[
        {
            "question":"eyJpdiI6ImdvWFl2aThGNDZhQVJzVkZSc0xKcFE9PSIsInZhbHVlIjoiRjZseWVMcisyZnBsSGJqQy9XUkRWZz09IiwibWFjIjoiYmM2YWViNDFmMzAwMDM1MDdjOWVjOTljMDBmMDdmMmNlNzE5YzBiMWE4OGFmZGNjZGIzNjU1NGY0Njg5OWQ4NSIsInRhZyI6IiJ9",
            "option":"eyJpdiI6Img0M0RZQ1JjSE16SDNFeXY0ZUgzNmc9PSIsInZhbHVlIjoiY01vNFdqL0E1RDVJNWxJNmdtQkd4Zz09IiwibWFjIjoiY2Q4MTE2ZjA4ZTdhNTBiYjI3Yjc0ZDNiMzYyMGRlYWMwZWJjZmE4MWFhMWYwYzVmMmU1M2Q4MTBkNjVmMWZlZSIsInRhZyI6IiJ9",
            "answer": "Cevap 1.1"
        },
        {
            "question":"eyJpdiI6IjBRRTBLSmplRGZwMk5kSkFMbTM2cWc9PSIsInZhbHVlIjoieWNjaHI4L3gwN3VWZHRBSWVxNFArQT09IiwibWFjIjoiNzc2ZTc0NWZhM2ZhOWNmN2RkMzJmYTEyNDk2OTM4MjJjMTU3OTE3NWVhZGRmNjkwNmY5YWJiYWFiZmQ2MmMwYiIsInRhZyI6IiJ9",
            "option":"eyJpdiI6IkROQlFhQ05KRDVCZVphd3BPaEJlWnc9PSIsInZhbHVlIjoic3dZbmYwWnJQVXJMYndBN2kydisrdz09IiwibWFjIjoiYWRiNWJjMWJkNTBlNmM3NTAwMGRlNzNhZTFiYTcyNDM4NWUwNWRmYWRlYTliZTA4YzYzYzU0NDg4OGY3MDBlZSIsInRhZyI6IiJ9",
            "answer": "cevap 2.1"
        }
    ]
}
```

### 5. ADIM
Cevaplar gönderildikten sonra gelen mesaj ekranda gösterilir.
Dönen örnek cevap:
```json
```

## PROJE TESLİMİ
- Github üzerinde projeyi iletmeniz yeterli.
- Docker üründe image dosyası olarak paylaşmanız artı bir durum.
- Gerek görülmesi durumunda kodların anlatımı ve uygulama anlatımını online görüşme ile iletmeniz bekleniyor.

## DESTEK

Tüm sorularınız için deneme@mindset.com.tr email adresinde iletişime geçebilirsiniz.

