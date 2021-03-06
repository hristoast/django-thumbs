![Django-thumbs logo](djangothumbs.jpg)
# Django-thumbs
----

Django-thumbs is the easiest way to create thumbnails for your ImageFields with Django.
You can integrate it easily in your code and it works with any StorageBackend. 

## Features
----

 * Easy to integrate in your code (no database changes, works as an ImageField)
 * Works perfectly with any StorageBackend
 * Generates thumbnails after image is uploaded into memory
 * Deletes thumbnails when the image file is deleted
 * Provides easy access to the thumbnails' URLs (similar method as with ImageField)

## Installation

 1. Download `thumbs.py`
 1. Import it in your _models.py_ and replace `ImageField` with `ImageWithThumbsField` in your model
 1. Add a `sizes` attribute with a list of sizes you want to use for the thumbnails 
 1. Make sure your have defined `MEDIA_URL` or `STATIC_URL` in your settings.py
 1. That's it!

## Working Example

_models.py_

    from django.db import models
    from thumbs import ImageWithThumbsField

    class Person(models.Model):
        photo = ImageWithThumbsField(upload_to='images', sizes=((125,125),(200,200)))
        second_photo = ImageWithThumbsField(upload_to='images')

In this example we have a `Person` model with 2 image fields.

You can see the field `second_photo` doesn't have a sizes attribute. This field works exactly the same way as a normal `ImageField`.

The field `photo` has a `sizes` attribute specifying desired sizes for the thumbnails. This field works the same way as `ImageField` but it also creates the desired thumbnails when uploading a new file and deletes the thumbnails when deleting the file.

With `ImageField` you retrieve the URL for the image with: `someone.photo.url` With `ImageWithThumbsField` you retrieve it the same way. You also retrieve the URL for every thumbnail specifying its size: In this example we use `someone.photo.url_125x125` and `someone.photo.url_200x200` to get the URL of both thumbnails. 

## Uninstall

At any time you can go back and use `ImageField` again without altering the database or anything else. Just replace `ImageWithThumbsField` with `ImageField` again and make sure you delete the `sizes` attribute. Everything will work the same way it worked before using django-thumbs. Just remember to delete generated thumbnails in the case you don't want to have them anymore. 
