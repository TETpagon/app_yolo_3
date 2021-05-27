# Демонстрационное приложение

## Предисловие
Приложение разрабатывалось для оценивания сложности интеграции Intel OpenVINO Toolkit в рабочие проекты.
Для работы приложения необходимо наличие модели Yolo v3 в IR-формате.

### Конвертация в IR-формат
В случае если модель из репозитория не подходит, для получения собственной модели необходимо выполнить следующие действия (в качестве модели Yolo v3 можно использовать и другие репозитории):
1. Клонировать 
```
git clone https://github.com/mystic123/tensorflow-yolo-v3.git
```
2. В папке проекта перейти на необходимый коммит:
```
git checkout ed60b90
```
3. Скачать наименования классов датасета COCO, на котором обучалась модель, или использовать свой классы
4. Скачать веса модели ([yolov3.weights](https://pjreddie.com/media/files/yolov3.weights) или [yolov3-tiny.weights](https://pjreddie.com/media/files/yolov3-tiny.weights)) или натренировать модель самому
5. Заморозить
```
python3 convert_weights_pb.py --class_names coco.names --data_format NHWC --weights_file yolov3.weights
```
6. Конвертировать в IR-формат:
```
python3 mo_tf.py
--input_model /path/to/yolo_v3.pb
--transformations_config $MO_ROOT/extensions/front/tf/yolo_v3.json
--batch 1
```

## Запуск приложения
Для запуска приложения необходимо выполнить команду:
```
python app.py
```
Рабочие параметры указываются внутри файла.
