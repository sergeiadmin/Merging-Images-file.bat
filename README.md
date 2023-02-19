This program merges all images located in the images folder. When the start.bat file is clicked, the program runs, and the merged result will be in the same folder as start.bat, named result.

What is it for? It is used to merge a large number of references in a simple way without resorting to other software...

This is my first program posted on Github. If you have any questions related to developing a new program or creating another one with a good idea, I am open to discussion.

Folder image:
________________________________________________________________________________________________

<img src="https://sun9-13.userapi.com/impg/eQeu8beo5yShHSfLnsVG5s233E47UHyZO-UyGw/WpksKjOh1y0.jpg?size=764x298&quality=96&sign=9425609c39d6b3caf9d23fcdf0b35eec&type=album" alt="Image description">

train.py coding:
____________________________________________________________________________________________

import os
from PIL import Image

# Пути к папке проекта и папке с изображениями
project_path = os.path.abspath('.')
images_path = os.path.join(project_path, 'image')

# Определяем размер квадрата
size = 512

# Список изображений
images = []

# Проходим по всем изображениям в папке и добавляем их в список
for filename in os.listdir(images_path):
    filepath = os.path.join(images_path, filename)
    try:
        with Image.open(filepath) as image:
            # Масштабируем изображение по максимальной стороне
            width, height = image.size
            if width > height:
                new_width = size
                new_height = int(height / width * size)
            else:
                new_height = size
                new_width = int(width / height * size)
            image = image.resize((new_width, new_height))
            images.append(image)
    except:
        pass

# Создаем новое изображение, склеивая все изображения из списка
result_width = size * int(len(images) ** 0.5)  # вычисляем ширину итогового изображения
result_height = size * int(len(images) ** 0.5)  # вычисляем высоту итогового изображения
result_image = Image.new('RGB', (result_width, result_height))  # создаем пустое изображение

for i, image in enumerate(images):
    row = i // int(len(images) ** 0.5)  # вычисляем номер строки
    col = i % int(len(images) ** 0.5)  # вычисляем номер столбца
    result_image.paste(image, (col * size, row * size))  # вставляем изображение на позицию

# Сохраняем итоговое изображение
result_image_path = os.path.join(project_path, 'result.jpg')
result_image.save(result_image_path)

print(f"Итоговое изображение сохранено в {result_image_path}")

____________________________________________________________________

Thank you for your attention, I hope this code will be useful to you.
