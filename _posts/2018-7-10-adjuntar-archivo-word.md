---
layout: post
title: Insertar o Adjuntar un archivo de Excel en Word con Python
---

Estaba buscando una manera de poder adjuntar un objeto dentro de un documento de word con python, y encontre una librería que trabaja con archvos .docx pero que no me fue de mucha ayuda.

Al final pude lograr adjuntar el objeto en word con la ayuda de la librería win32com de la cual no encontré mucha documentación pero que en https://msdn.microsoft.com/en-us/vba/word-vba/articles/object-model-word-vba-reference pude encontrar metodos que son compatibles a la hora implementarse la librería win32com en python.

Pero mejor vayamos directo al código.

## Aquí el código en Python

```Python

#importamos el cliente de win32com para poder interactuar
#con la suite de office
import win32com.client as win32

#Llamamos a la aplicacion Word
word = win32.gencache.EnsureDispatch('Word.Application')
#Le decimos que la aplicación sea visible
word.Visible = True
#Abrimos un nuevo documento de word
docx = word.Documents.Add()  

#Aquí tenemos el path del archivo que se desea adjuntar
doc_path1='C:\\Users\\admin\\Escritorio\\demo.xlsx'
#Aquí tenemos el path del icono
doc_path2='C:\\Program Files (x86)\\Microsoft Office\\root\\Office16\\EXCEL.EXE'
#En esta línea de código agregamos el objeto que en este caso será un archivo xlsx
docx.InlineShapes.AddOLEObject(FileName=doc_path1,DisplayAsIcon=1,IconLabel="xlsx",IconFileName=doc_path2)
```

Espero les sirva :)

![una serpiente](data:image/png;base64,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)