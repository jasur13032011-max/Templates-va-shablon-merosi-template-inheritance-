# Templates-va-shablon-merosi-template-inheritance-
Mana Django’da context uzatish, base.html merosxo‘rligi, sikl/shartlar va shablon filtri ishlatilgan to'liq va sodda misol:

1. View tayyorlash (views.py)
View funksiyasi orqali ma'lumotlar lug‘at (context) shaklida shablonga uzatiladi:

Python
from django.shortcuts import render

def article_list(view_request):
    context = {
        'page_title': 'Maqolalar ro\'yxati',
        'articles': [
            {'title': 'django shablonlari haqida', 'author': 'Ali', 'is_published': True},
            {'title': 'python asoslari', 'author': 'Vali', 'is_published': False},
            {'title': 'web dasturlash kirish', 'author': 'Sami', 'is_published': True},
        ]
    }
    return render(view_request, 'articles/index.html', context)
2. Bosh shablon tayyorlash (base.html)
Boshqa shablonlar uchun asos bo'lib xizmat qiladigan va umumiy tuzilmani saqlaydigan tayanch shablon:

HTML
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}Mening Saytim{% endblock %}</title>
</head>
<body>
    <header>
        <h1>Veb-sayt Sarlavhasi</h1>
        <hr>
    </header>

    <main>
        {% block content %}
        <!-- Shu yerga bolalar shabloni ma'lumot joylaydi -->
        {% endblock %}
    </main>

    <footer>
        <hr>
        <p>&copy; 2026 Mening Saytim</p>
    </footer>
</body>
</html>
3. Sahifa shabloni tayyorlash (articles/index.html)
Ushbu shablon base.html dan nusxa oladi ({% extends %}), tegishli bloklarni to'ldiradi hamda {% for %}, {% if %} va filterlardan foydalanadi:

HTML
{% extends "base.html" %}

{% block title %}
    {{ page_title|title }}
{% endblock %}

{% block content %}
    <h2>{{ page_title|upper }}</h2>

    <p>Jami maqolalar soni: {{ articles|length }} ta</p>

    <ul>
        {% for article in articles %}
            {% if article.is_published %}
                <li>
                    <strong>{{ article.title|capfirst }}</strong> — Muallif: {{ article.author }}
                </li>
            {% else %}
                <li style="color: gray;">
                    <em>{{ article.title|capfirst }} (Qoralama)</em>
                </li>
            {% endif %}
        {% empty %}
            <li>Hozircha hech qanday maqola mavjud emas.</li>
        {% endfor %}
    </ul>
{% endblock %}
Ishlatilgan elementlar sharhi:
Context uzatish: render(view_request, 'articles/index.html', context)

Shablon merosi: {% extends "base.html" %} va {% block title %}, {% block content %}

Ma'lumot chiqarish: {{ page_title }} hamda {{ article.title }}

Mantiqiy teglar: {% for article in articles %} va {% if article.is_published %}

Shablon filtrlari:

|upper — Matnni barcha harflarini katta qiladi.

|length — Ro'yxatdagi elementlar sonini sanaydi.

|capfirst — Faqat birinchi harfni katta qiladi.

|title — Har bir so'zning birinchi harfini katta qiladi.

Mavzuga oid boshqa loyiha namunalari yoki tushunchalarni o'rganishni istaysizmi?

Custom shablon filtri yaratish

Static fayllarni ulang
